# Session 16 — DAX Introduction & Calculated Columns
## Module 4: DAX Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Write Your First DAX Calculated Columns

---

## Learning Objectives
By the end of this session, you will be able to:
1. Understand what DAX is and where it fits in Power BI
2. Write basic DAX syntax (functions, operators, references)
3. Create Calculated Columns using DAX
4. Differentiate between Calculated Columns and Measures
5. Apply common DAX functions: IF, SWITCH, FORMAT, RELATED

---

## 16.1 What is DAX?

**DAX (Data Analysis Expressions)** is the formula language of Power BI. It creates calculations that don't exist in your source data.

### Where DAX Fits

```
Source Data → Power Query (clean) → Data Model (structure) → DAX (calculate) → Visuals (display)
```

### DAX vs Excel Formulas

| Feature | Excel | DAX |
|---------|-------|-----|
| **Operates on** | Individual cells | Entire columns or tables |
| **Context** | Cell reference (A1, B2) | Row context or Filter context |
| **Recalculation** | When cell changes | When filters change (measures) or on refresh (columns) |
| **Similar functions** | SUM, IF, AVERAGE, FORMAT | Same names, different behavior |
| **Unique to DAX** | — | CALCULATE, FILTER, ALL, RELATED, Time Intelligence |

### DAX Syntax Basics

```dax
// Column reference
TableName[ColumnName]
'Table Name'[Column Name]     // Use quotes if table name has spaces

// Function syntax
FUNCTION_NAME(argument1, argument2, ...)

// Examples
SUM(Sales[Revenue])
IF(Sales[Revenue] > 50000, "High", "Low")
```

### DAX Operators

| Type | Operators | Example |
|------|-----------|---------|
| **Arithmetic** | + - * / ^ | `[Revenue] - [Cost]` |
| **Comparison** | = <> < > <= >= | `[Revenue] > 50000` |
| **Text** | & | `[FirstName] & " " & [LastName]` |
| **Logical** | && (AND) \|\| (OR) | `[Revenue] > 50000 && [Region] = "North"` |

---

## 16.2 Calculated Columns vs Measures

### Calculated Column

| Aspect | Detail |
|--------|--------|
| **What** | A new column added to a table, calculated row by row |
| **When computed** | During data refresh (stored in the model) |
| **Storage** | Takes memory — stored for every row |
| **Context** | Row context — evaluates per row |
| **Use for** | Categorizations, lookups, static labels, filter/slicer values |
| **Created via** | Modeling tab → New Column |
| **Icon in Fields** | Column icon (no calculator) |

### Measure

| Aspect | Detail |
|--------|--------|
| **What** | A dynamic calculation that responds to filters/context |
| **When computed** | At query time (when visuals render) |
| **Storage** | No storage — calculated on the fly |
| **Context** | Filter context — changes based on slicers, filters, row/column of a visual |
| **Use for** | Aggregations (Sum, Avg, Count), ratios, percentages, KPIs |
| **Created via** | Modeling tab → New Measure |
| **Icon in Fields** | Calculator icon (Σ) |

### When to Use Which

| Need | Use |
|------|-----|
| Categorize rows: "High", "Medium", "Low" | **Calculated Column** |
| Full name from first + last | **Calculated Column** |
| Year extracted from date | **Calculated Column** |
| Value for use as a slicer/filter | **Calculated Column** |
| Total Revenue (responds to filters) | **Measure** |
| Profit Margin % | **Measure** |
| Year-over-Year growth | **Measure** |
| Count of distinct customers | **Measure** |

> **Rule of Thumb:** If the result is the **same for every filter combination** → Calculated Column. If the result **changes when you filter** → Measure.

---

## 16.3 Creating Calculated Columns

### How to Create

1. Select the target table in the Fields pane
2. **Modeling** tab → **New Column**
3. The formula bar appears at the top
4. Type your DAX formula
5. Press Enter — the column appears in the table

### Example 1: Profit Column

```dax
Profit = Sales[Revenue] - Sales[Cost]
```

- Creates a new column called "Profit" in the Sales table
- Calculates for every row: Revenue minus Cost

### Example 2: Profit Margin %

```dax
Profit Margin = 
DIVIDE(Sales[Revenue] - Sales[Cost], Sales[Revenue], 0)
```

- `DIVIDE` is safer than `/` — handles divide-by-zero gracefully
- Third argument (0) is the alternate result when denominator is zero

### Example 3: Revenue Category (IF)

```dax
Revenue Category = 
IF(
    Sales[Revenue] > 100000, "Premium",
    IF(
        Sales[Revenue] > 50000, "Standard",
        "Economy"
    )
)
```

### Example 4: Revenue Category (SWITCH — Cleaner)

```dax
Revenue Band = 
SWITCH(
    TRUE(),
    Sales[Revenue] > 100000, "Premium",
    Sales[Revenue] > 50000, "Standard",
    Sales[Revenue] > 10000, "Regular",
    "Economy"
)
```

> **Best Practice:** Use `SWITCH(TRUE(), ...)` instead of nested `IF` for multiple conditions — much more readable.

### Example 5: Full Name (Text Concatenation)

```dax
Full Name = Customers[First Name] & " " & Customers[Last Name]
```

### Example 6: Year and Month from Date

```dax
Order Year = YEAR(Sales[OrderDate])
Order Month = FORMAT(Sales[OrderDate], "MMMM")
Order MonthNumber = MONTH(Sales[OrderDate])
Month-Year = FORMAT(Sales[OrderDate], "MMM YYYY")
```

### Example 7: Day of Week

```dax
Day Name = FORMAT(Sales[OrderDate], "DDDD")
Is Weekend = IF(WEEKDAY(Sales[OrderDate], 2) >= 6, "Weekend", "Weekday")
```

---

## 16.4 The RELATED Function

### What is RELATED?

`RELATED` pulls a value from a **related table** — like VLOOKUP across tables.

### Requirements
- A **relationship** must exist between the tables
- `RELATED` works from the **Many side** to the **One side** (Fact → Dimension)

### Example: Get Product Category in the Sales Table

```dax
Product Category = RELATED(Products[Category])
```

- This is evaluated in the **Sales** table (Many side)
- It pulls the Category from the **Products** table (One side)
- Uses the existing relationship on ProductID

### Example: Get Customer City

```dax
Customer City = RELATED(Customers[City])
```

### When to Use RELATED

| Scenario | Use RELATED? |
|----------|-------------|
| Need a dimension value in the fact table for filtering | ✅ Yes |
| Need a dimension value for a calculated column formula | ✅ Yes |
| Just need to show it in a visual | ❌ No — use the relationship directly |

> **Important:** `RELATED` only works in **Calculated Columns** (row context), not directly in Measures. For measures, use `CALCULATE` with filters (Session 18).

---

## 16.5 FORMAT Function

### Syntax
```dax
FORMAT(value, format_string)
```

### Common Format Strings

| Format String | Input | Output |
|--------------|-------|--------|
| `"#,##0"` | 42500 | 42,500 |
| `"#,##0.00"` | 42500 | 42,500.00 |
| `"₹#,##0"` | 42500 | ₹42,500 |
| `"0.0%"` | 0.185 | 18.5% |
| `"YYYY"` | 2024-03-15 | 2024 |
| `"MMMM"` | 2024-03-15 | March |
| `"MMM YYYY"` | 2024-03-15 | Mar 2024 |
| `"DDDD"` | 2024-03-15 | Friday |
| `"DD-MMM-YYYY"` | 2024-03-15 | 15-Mar-2024 |

> **Note:** `FORMAT` returns **Text**. Use it for display labels, not for calculations.

---

## 16.6 Other Useful Functions for Calculated Columns

| Function | Purpose | Example |
|----------|---------|---------|
| `LEFT(text, n)` | First n characters | `LEFT(Sales[ProductCode], 3)` → "PRD" |
| `RIGHT(text, n)` | Last n characters | `RIGHT(Sales[ProductCode], 4)` → "1234" |
| `LEN(text)` | Length of text | `LEN(Customers[Name])` |
| `UPPER(text)` | Convert to uppercase | `UPPER(Customers[City])` |
| `TRIM(text)` | Remove extra spaces | `TRIM(Customers[Name])` |
| `INT(number)` | Convert to integer | `INT(Sales[Revenue] / 1000)` |
| `ROUND(number, n)` | Round to n decimals | `ROUND(Sales[Margin], 2)` |
| `TODAY()` | Current date | `DATEDIFF(Sales[OrderDate], TODAY(), DAY)` |
| `DATEDIFF(start, end, interval)` | Difference between dates | `DATEDIFF(Sales[OrderDate], Sales[ShipDate], DAY)` |
| `BLANK()` | Return blank value | `IF(Sales[Revenue] = 0, BLANK(), Sales[Revenue])` |

---

## 16.7 Calculated Column Best Practices

| Practice | Why |
|----------|-----|
| **Use for categorization and labels** | Best use case — slicer/filter values |
| **Avoid for aggregations** | Use Measures instead (better performance) |
| **Keep column count low** | Each column consumes memory |
| **Use SWITCH over nested IF** | Readability and maintenance |
| **Use DIVIDE over division operator** | Handles divide-by-zero |
| **Use RELATED sparingly** | Only when you truly need the value in the fact table |
| **Format in the visual, not in DAX** | Don't use FORMAT for measures — format in the visual settings |

---

## 🔧 Hands-On Activity: Create Calculated Columns

**Duration:** 25 minutes

### Tasks

Using your Sales + Products + Customers Star Schema model:

1. **Profit Column:**
   ```dax
   Profit = Sales[Revenue] - Sales[Cost]
   ```

2. **Profit Margin:**
   ```dax
   Profit Margin = DIVIDE(Sales[Revenue] - Sales[Cost], Sales[Revenue], 0)
   ```

3. **Revenue Band:**
   ```dax
   Revenue Band = SWITCH(TRUE(), Sales[Revenue] > 100000, "Premium", Sales[Revenue] > 50000, "Standard", "Economy")
   ```

4. **Order Month-Year:**
   ```dax
   Order MonthYear = FORMAT(Sales[OrderDate], "MMM YYYY")
   ```

5. **Days to Ship** (if ShipDate exists):
   ```dax
   Days to Ship = DATEDIFF(Sales[OrderDate], Sales[ShipDate], DAY)
   ```

6. **Product Category** (using RELATED):
   ```dax
   Category = RELATED(Products[Category])
   ```

### Verification
- Switch to **Table View** — verify each new column has values
- Use "Revenue Band" as a **Slicer** — does it filter visuals correctly?
- Create a **Bar Chart:** Revenue Band (X-axis) vs Sum of Revenue (Y-axis)
- Save

---

## Session 16 — Key Takeaways

1. **DAX** is Power BI's formula language — creates calculations beyond source data
2. **Calculated Columns** are computed row-by-row during refresh — stored in the model
3. **Measures** (next session) are computed dynamically based on filter context
4. Use `SWITCH(TRUE(), ...)` for multi-condition logic instead of nested `IF`
5. Use `DIVIDE()` instead of `/` for safe division
6. `RELATED()` pulls values from a linked dimension table

---

## Preparation for Session 17
- Review: What is the difference between a column and a measure?
- Think about: What calculations in your dashboard should CHANGE when a user filters? (Those should be Measures)
- Preview: What does `SUM(Sales[Revenue])` do differently as a Measure vs a Column?

---

*Session 16 of 30 | Module 4: DAX Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
