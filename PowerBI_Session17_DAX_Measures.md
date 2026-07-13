# Session 17 — DAX Measures
## Module 4: DAX Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Create Dynamic Measures for Business Reporting

---

## Learning Objectives
By the end of this session, you will be able to:
1. Understand filter context and how measures respond to it
2. Create explicit measures using SUM, COUNT, AVERAGE, MIN, MAX
3. Use CALCULATE to change filter context
4. Build ratio and percentage measures
5. Apply best practices for measure organization

---

## 17.1 Why Measures?

### The Problem with Implicit Measures
When you drag "Revenue" into a visual, Power BI auto-aggregates it (Sum, Count, etc.). This is an **implicit measure** — quick but limited.

| Feature | Implicit Measure | Explicit Measure |
|---------|-----------------|-----------------|
| **Created by** | Dragging a column into a visual | Writing DAX formula |
| **Reusable** | No — only in that visual | Yes — across all visuals and pages |
| **Formatting** | Per visual | Once — applied everywhere |
| **Complex logic** | Not possible | Full DAX power |
| **Best practice** | Quick exploration | Production reports |

> **Best Practice:** Always create **explicit measures** for any value shown in a report. Never rely on implicit aggregation for production dashboards.

---

## 17.2 Filter Context

### What is Filter Context?

Filter context is the set of **active filters** applied to a measure when it calculates. It changes based on:
- **Slicers** the user selects
- **Visual axes** (a bar for "Electronics" filters to Electronics)
- **Filter pane** settings
- **Cross-filtering** from other visuals
- **Drill-through** filters

### Example

Measure: `Total Revenue = SUM(Sales[Revenue])`

| Context | What the Measure Returns |
|---------|-------------------------|
| Card (no filter) | Sum of ALL revenue |
| Bar chart — "Electronics" bar | Sum of revenue for Electronics only |
| Slicer = "North" | Sum of revenue for North region only |
| Bar "Electronics" + Slicer "North" | Revenue for Electronics in North |
| Matrix cell: Q1 × North | Revenue for Q1 in North |

> **Key Insight:** The same measure formula returns **different values** depending on where and how it's used. This is the power of filter context.

---

## 17.3 Creating Measures

### How to Create

1. Select the table where the measure logically belongs (usually the Fact table)
2. **Modeling** tab → **New Measure**
3. Type the DAX formula in the formula bar
4. Press Enter

### Basic Aggregation Measures

```dax
Total Revenue = SUM(Sales[Revenue])

Total Cost = SUM(Sales[Cost])

Total Profit = SUM(Sales[Revenue]) - SUM(Sales[Cost])

Total Orders = COUNTROWS(Sales)

Total Quantity = SUM(Sales[Quantity])

Average Order Value = DIVIDE(SUM(Sales[Revenue]), COUNTROWS(Sales), 0)

Average Revenue = AVERAGE(Sales[Revenue])

Max Revenue = MAX(Sales[Revenue])

Min Revenue = MIN(Sales[Revenue])
```

### Aggregation Functions Reference

| Function | What It Does | Example |
|----------|-------------|---------|
| `SUM(column)` | Adds all values | `SUM(Sales[Revenue])` |
| `AVERAGE(column)` | Mean of all values | `AVERAGE(Sales[Revenue])` |
| `MIN(column)` | Smallest value | `MIN(Sales[OrderDate])` |
| `MAX(column)` | Largest value | `MAX(Sales[Revenue])` |
| `COUNT(column)` | Count non-blank values | `COUNT(Sales[OrderID])` |
| `COUNTA(column)` | Count non-blank (text+numbers) | `COUNTA(Sales[Notes])` |
| `COUNTROWS(table)` | Count rows in a table | `COUNTROWS(Sales)` |
| `COUNTBLANK(column)` | Count blank/null values | `COUNTBLANK(Sales[Discount])` |
| `DISTINCTCOUNT(column)` | Count unique values | `DISTINCTCOUNT(Sales[CustomerID])` |

---

## 17.4 Ratio and Percentage Measures

### Profit Margin %

```dax
Profit Margin % = 
DIVIDE(
    SUM(Sales[Revenue]) - SUM(Sales[Cost]),
    SUM(Sales[Revenue]),
    0
)
```

- Format as Percentage in the Modeling tab → Format → Percentage
- Returns 0 when Revenue is 0 (third argument of DIVIDE)

### Revenue Share %

```dax
Revenue Share % = 
DIVIDE(
    SUM(Sales[Revenue]),
    CALCULATE(SUM(Sales[Revenue]), ALL(Sales)),
    0
)
```

- Numerator: Revenue for current filter context (e.g., "Electronics")
- Denominator: Revenue for ALL sales (ignores all filters)
- Result: What % of total revenue does this category represent?

### Distinct Customer Count

```dax
Customer Count = DISTINCTCOUNT(Sales[CustomerID])
```

### Orders per Customer

```dax
Orders per Customer = 
DIVIDE(
    COUNTROWS(Sales),
    DISTINCTCOUNT(Sales[CustomerID]),
    0
)
```

---

## 17.5 CALCULATE — The Most Important DAX Function

### What is CALCULATE?

`CALCULATE` evaluates an expression in a **modified filter context**. It lets you override, add, or remove filters.

### Syntax

```dax
CALCULATE(expression, filter1, filter2, ...)
```

- **Expression:** The calculation to perform (usually a SUM, COUNT, etc.)
- **Filters:** Conditions that modify the filter context

### Example 1: Revenue for a Specific Region

```dax
North Revenue = 
CALCULATE(
    SUM(Sales[Revenue]),
    Sales[Region] = "North"
)
```

- Always returns North region revenue, regardless of slicer/filter selections

### Example 2: Revenue for Electronics Only

```dax
Electronics Revenue = 
CALCULATE(
    SUM(Sales[Revenue]),
    Products[Category] = "Electronics"
)
```

### Example 3: ALL — Remove All Filters

```dax
Total Revenue ALL = 
CALCULATE(
    SUM(Sales[Revenue]),
    ALL(Sales)
)
```

- `ALL(Sales)` removes ALL filters from the Sales table
- Always returns the grand total, regardless of slicers

### Example 4: Revenue Share % (Using CALCULATE + ALL)

```dax
Revenue % of Total = 
DIVIDE(
    SUM(Sales[Revenue]),
    CALCULATE(SUM(Sales[Revenue]), ALL(Sales)),
    0
)
```

### Example 5: ALLEXCEPT — Remove All Filters Except Specific Ones

```dax
Revenue % Within Region = 
DIVIDE(
    SUM(Sales[Revenue]),
    CALCULATE(SUM(Sales[Revenue]), ALLEXCEPT(Sales, Sales[Region])),
    0
)
```

- Removes all filters EXCEPT Region
- Shows each product's % share WITHIN its region

---

## 17.6 CALCULATE Filter Functions

| Function | Purpose | Example |
|----------|---------|---------|
| `ALL(table)` | Remove all filters from a table | `ALL(Sales)` |
| `ALL(column)` | Remove filter from one column | `ALL(Sales[Region])` |
| `ALLEXCEPT(table, col)` | Remove all filters except specified columns | `ALLEXCEPT(Sales, Sales[Region])` |
| `ALLSELECTED()` | Respect slicer selections but remove visual context | `ALLSELECTED(Sales)` |
| `FILTER(table, condition)` | Apply a row-by-row filter | `FILTER(Sales, Sales[Revenue] > 50000)` |
| `KEEPFILTERS(condition)` | Add filter without overriding existing ones | `KEEPFILTERS(Sales[Region] = "North")` |
| `REMOVEFILTERS(column)` | Same as ALL but more readable | `REMOVEFILTERS(Sales[Region])` |

---

## 17.7 Measure Formatting

### Setting Format in Modeling Tab

1. Select the measure in the Fields pane
2. **Measure Tools** tab appears in the Ribbon
3. Set: Format (Number, Currency, Percentage, etc.)
4. Set: Decimal places, Thousands separator

### Common Format Settings

| Measure Type | Format | Decimals | Example |
|-------------|--------|----------|---------|
| Revenue | Currency (₹) | 0 | ₹42,500 |
| Order Count | Whole Number | 0 | 12,500 |
| Average | Decimal | 2 | 3,384.50 |
| Percentage | Percentage | 1 | 18.5% |
| Large numbers | Auto (display units) | 1 | 42.5 Cr |

---

## 17.8 Measure Organization Best Practices

### Create a Measures Table

Instead of placing measures in the Sales table, create a dedicated **Measures table**:

1. **Modeling** tab → **New Table**
2. DAX: `_Measures = { BLANK() }`
3. This creates an empty table — it's just a container
4. Create all measures inside this table
5. Rename it to `_Measures` (underscore sorts it to the top)

### Folder Organization (Display Folders)

1. Select a measure → Properties pane → **Display Folder**
2. Type a folder name: "Revenue Measures", "Profit Measures", "Customer Measures"
3. Measures group into folders in the Fields pane

### Naming Conventions

| Pattern | Example | Use For |
|---------|---------|---------|
| `Total [Metric]` | Total Revenue | Sum measures |
| `Avg [Metric]` | Avg Order Value | Average measures |
| `[Metric] %` | Profit Margin % | Percentage measures |
| `[Metric] YoY` | Revenue YoY | Year-over-year measures |
| `# [Entity]` | # Customers | Count measures |

---

## 🔧 Hands-On Activity: Create Business Measures

**Duration:** 25 minutes

### Tasks

Create these measures in your Sales model:

**Basic Measures:**
1. `Total Revenue = SUM(Sales[Revenue])`
2. `Total Cost = SUM(Sales[Cost])`
3. `Total Profit = [Total Revenue] - [Total Cost]`
4. `Total Orders = COUNTROWS(Sales)`
5. `Total Quantity = SUM(Sales[Quantity])`

**Ratio Measures:**
6. `Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)`
7. `Avg Order Value = DIVIDE([Total Revenue], [Total Orders], 0)`
8. `# Customers = DISTINCTCOUNT(Sales[CustomerID])`

**CALCULATE Measures:**
9. `Revenue % of Total = DIVIDE([Total Revenue], CALCULATE([Total Revenue], ALL(Sales)), 0)`
10. `North Revenue = CALCULATE([Total Revenue], Sales[Region] = "North")`

### Verification
- Format each measure appropriately (Currency, Percentage, Whole Number)
- Create a **Matrix:** Product Category (Rows) × All measures (Values)
- Verify: Revenue % of Total sums to 100% across all categories
- Add a Slicer for Region → verify measures respond to filtering
- Verify: North Revenue stays constant regardless of Region slicer
- Save

---

## Session 17 — Key Takeaways

1. **Measures** are dynamic calculations that respond to filter context — create them explicitly
2. **Filter context** = the active filters (slicers, axes, filter pane) when a measure calculates
3. **CALCULATE** is the most important DAX function — it modifies filter context
4. **ALL** removes filters; **ALLEXCEPT** removes all except specified columns
5. Always use **DIVIDE()** instead of `/` for safe division
6. Organize measures in a `_Measures` table with display folders

---

## Preparation for Session 18
- Review: What is the difference between SUM, SUMX, and CALCULATE?
- Think about: How would you calculate "Revenue only for orders > ₹50,000"?
- Preview: Iterator functions (SUMX, AVERAGEX, COUNTX)

---

*Session 17 of 30 | Module 4: DAX Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
