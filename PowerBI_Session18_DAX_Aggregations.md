# Session 18 — DAX Aggregations & Iterator Functions
## Module 4: DAX Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Advanced Aggregation Measures

---

## Learning Objectives
By the end of this session, you will be able to:
1. Differentiate between simple aggregators (SUM) and iterators (SUMX)
2. Use SUMX, AVERAGEX, COUNTX, MINX, MAXX for row-level calculations
3. Apply FILTER for conditional aggregations
4. Use CALCULATE with FILTER for advanced scenarios
5. Build Top N and conditional measures

---

## 18.1 Simple Aggregators vs Iterator Functions

### Simple Aggregators
Operate on a **single column** — aggregate all values in that column.

```dax
SUM(Sales[Revenue])         // Sum one column
AVERAGE(Sales[Revenue])     // Average one column
COUNT(Sales[OrderID])       // Count one column
MIN(Sales[OrderDate])       // Min of one column
MAX(Sales[Revenue])         // Max of one column
```

### Iterator Functions (X Functions)
Iterate **row by row** through a table, evaluate an expression per row, then aggregate the results.

```dax
SUMX(table, expression)     // Sum of expression evaluated per row
AVERAGEX(table, expression) // Average of expression per row
COUNTX(table, expression)   // Count of non-blank expression per row
MINX(table, expression)     // Min of expression per row
MAXX(table, expression)     // Max of expression per row
```

### When to Use Iterators

| Scenario | Simple Aggregator | Iterator |
|----------|------------------|----------|
| Sum of Revenue column | `SUM(Sales[Revenue])` ✅ | `SUMX(Sales, Sales[Revenue])` (same result, unnecessary) |
| Sum of (Revenue × Margin%) | ❌ Can't multiply then sum | `SUMX(Sales, Sales[Revenue] * Sales[MarginPct])` ✅ |
| Sum of row-level Profit | ❌ Need row-level calc | `SUMX(Sales, Sales[Revenue] - Sales[Cost])` ✅ |
| Average of (Price × Quantity) | ❌ | `AVERAGEX(Sales, Sales[Price] * Sales[Quantity])` ✅ |

> **Rule:** Use iterators when you need to **calculate something per row FIRST**, then aggregate the results.

---

## 18.2 SUMX — Detailed

### Syntax
```dax
SUMX(table, expression)
```

### How It Works (Conceptually)

```
Sales Table:
| Revenue | Cost   | → Expression: Revenue - Cost
|---------|--------|
| 50000   | 30000  | → 20000
| 12000   | 8000   | → 4000
| 45000   | 28000  | → 17000
                       ──────
SUMX Result:           41000  (sum of all row-level results)
```

### Examples

**Weighted Average Price:**
```dax
Weighted Avg Price = 
DIVIDE(
    SUMX(Sales, Sales[Price] * Sales[Quantity]),
    SUM(Sales[Quantity]),
    0
)
```

**Total Profit (without a Profit column):**
```dax
Total Profit X = SUMX(Sales, Sales[Revenue] - Sales[Cost])
```

**Revenue After Discount:**
```dax
Net Revenue = SUMX(Sales, Sales[Revenue] * (1 - Sales[DiscountPct]))
```

**Commission Calculation:**
```dax
Total Commission = 
SUMX(
    Sales,
    IF(Sales[Revenue] > 50000, Sales[Revenue] * 0.05, Sales[Revenue] * 0.03)
)
```

---

## 18.3 Other Iterator Functions

### AVERAGEX

```dax
// Average revenue per order, weighted by quantity
Avg Revenue Per Unit = 
AVERAGEX(Sales, DIVIDE(Sales[Revenue], Sales[Quantity], 0))
```

### COUNTX

```dax
// Count orders where revenue exceeds 50000
High Value Orders = 
COUNTX(
    FILTER(Sales, Sales[Revenue] > 50000),
    Sales[OrderID]
)
```

### MINX / MAXX

```dax
// Lowest profit margin order
Worst Margin = MINX(Sales, DIVIDE(Sales[Revenue] - Sales[Cost], Sales[Revenue], 0))

// Highest single order revenue
Best Order = MAXX(Sales, Sales[Revenue])
```

### RANKX

```dax
// Rank products by revenue
Product Rank = 
RANKX(
    ALL(Products[ProductName]),
    [Total Revenue],
    ,
    DESC,
    Dense
)
```

- `ALL(Products[ProductName])` — rank across all products (ignore current filter)
- `[Total Revenue]` — the measure to rank by
- `DESC` — highest revenue = rank 1
- `Dense` — no gaps in ranking (1, 2, 2, 3 instead of 1, 2, 2, 4)

---

## 18.4 FILTER Function

### What is FILTER?

`FILTER` returns a table where each row meets a condition. It's used inside other functions (CALCULATE, SUMX, COUNTX).

### Syntax
```dax
FILTER(table, condition)
```

### FILTER with CALCULATE

```dax
// Revenue from high-value orders only
High Value Revenue = 
CALCULATE(
    SUM(Sales[Revenue]),
    FILTER(Sales, Sales[Revenue] > 50000)
)
```

### FILTER with SUMX

```dax
// Total profit from premium products only
Premium Profit = 
SUMX(
    FILTER(Sales, RELATED(Products[Category]) = "Premium"),
    Sales[Revenue] - Sales[Cost]
)
```

### Multiple Conditions with FILTER

```dax
// Revenue from North region, Electronics category
North Electronics Revenue = 
CALCULATE(
    SUM(Sales[Revenue]),
    FILTER(Sales, Sales[Region] = "North"),
    Products[Category] = "Electronics"
)
```

### FILTER vs Direct CALCULATE Filter

| Approach | Syntax | Best For |
|----------|--------|----------|
| **Direct filter** | `CALCULATE(SUM(...), Column = "Value")` | Simple equality filters on a single column |
| **FILTER function** | `CALCULATE(SUM(...), FILTER(Table, condition))` | Complex conditions, row-by-row evaluation, AND/OR logic |

```dax
// These are equivalent for simple equality:
CALCULATE(SUM(Sales[Revenue]), Sales[Region] = "North")
CALCULATE(SUM(Sales[Revenue]), FILTER(ALL(Sales[Region]), Sales[Region] = "North"))

// But FILTER is needed for complex conditions:
CALCULATE(SUM(Sales[Revenue]), FILTER(Sales, Sales[Revenue] > 50000 && Sales[Quantity] > 5))
```

---

## 18.5 Conditional Aggregations

### Count with Condition (COUNTX + FILTER)

```dax
// Count of orders above average
Above Avg Orders = 
COUNTX(
    FILTER(Sales, Sales[Revenue] > [Avg Order Value]),
    Sales[OrderID]
)
```

### Sum with Condition

```dax
// Revenue only from returning customers (>1 order)
Returning Customer Revenue = 
SUMX(
    FILTER(
        VALUES(Sales[CustomerID]),
        CALCULATE(COUNTROWS(Sales)) > 1
    ),
    CALCULATE(SUM(Sales[Revenue]))
)
```

### Percentage of Total with Condition

```dax
// % of revenue from orders > 50K
High Value Revenue % = 
DIVIDE(
    CALCULATE(SUM(Sales[Revenue]), FILTER(Sales, Sales[Revenue] > 50000)),
    SUM(Sales[Revenue]),
    0
)
```

---

## 18.6 Top N Measures

### Top 5 Products by Revenue

```dax
Top 5 Revenue = 
CALCULATE(
    [Total Revenue],
    TOPN(5, ALL(Products[ProductName]), [Total Revenue], DESC)
)
```

### Contribution of Top 10 Products

```dax
Top 10 Contribution % = 
DIVIDE(
    CALCULATE(
        [Total Revenue],
        TOPN(10, ALL(Products[ProductName]), [Total Revenue], DESC)
    ),
    CALCULATE([Total Revenue], ALL(Products)),
    0
)
```

---

## 18.7 SELECTEDVALUE and HASONEVALUE

### SELECTEDVALUE

Returns the value if a single filter is active; otherwise returns a default.

```dax
Selected Region = SELECTEDVALUE(Sales[Region], "All Regions")
```

**Use case:** Show dynamic titles that change based on slicer selection.

```dax
Dynamic Title = "Revenue for " & SELECTEDVALUE(Sales[Region], "All Regions")
```

### HASONEVALUE

Returns TRUE if only one value is selected in the filter context.

```dax
Dynamic Metric = 
IF(
    HASONEVALUE(Products[Category]),
    "Category: " & SELECTEDVALUE(Products[Category]),
    "All Categories"
)
```

---

## 18.8 Common Aggregation Patterns Summary

| Pattern | DAX |
|---------|-----|
| Total of one column | `SUM(column)` |
| Row-level calculation then sum | `SUMX(table, expression)` |
| Count of rows | `COUNTROWS(table)` |
| Count of unique values | `DISTINCTCOUNT(column)` |
| Conditional count | `COUNTX(FILTER(table, condition), column)` |
| Conditional sum | `CALCULATE(SUM(column), condition)` |
| Percentage of total | `DIVIDE(SUM(col), CALCULATE(SUM(col), ALL(table)))` |
| Weighted average | `DIVIDE(SUMX(table, val*weight), SUM(weight))` |
| Rank | `RANKX(ALL(dimension), measure, , DESC)` |
| Top N value | `CALCULATE(measure, TOPN(N, ALL(dim), measure))` |

---

## 🔧 Hands-On Activity: Advanced Aggregation Measures

**Duration:** 25 minutes

### Tasks

1. **SUMX — Total Profit (row-level):**
   ```dax
   Total Profit X = SUMX(Sales, Sales[Revenue] - Sales[Cost])
   ```

2. **SUMX — Net Revenue after Discount:**
   ```dax
   Net Revenue = SUMX(Sales, Sales[Revenue] * (1 - Sales[DiscountPct]))
   ```
   (If no DiscountPct column, create one as a calculated column with random values)

3. **Conditional — High Value Order Count:**
   ```dax
   High Value Orders = CALCULATE(COUNTROWS(Sales), FILTER(Sales, Sales[Revenue] > 50000))
   ```

4. **Conditional — High Value Revenue %:**
   ```dax
   High Value % = DIVIDE([High Value Revenue], [Total Revenue], 0)
   ```

5. **RANKX — Product Rank:**
   ```dax
   Product Rank = RANKX(ALL(Products[ProductName]), [Total Revenue], , DESC, Dense)
   ```

6. **Weighted Average:**
   ```dax
   Weighted Avg Price = DIVIDE(SUMX(Sales, Sales[Price] * Sales[Quantity]), SUM(Sales[Quantity]), 0)
   ```

### Verification
- Create a Table visual: ProductName, Total Revenue, Product Rank → verify ranking
- Add a Card for High Value Orders → filter by region → verify count changes
- Save

---

## Session 18 — Key Takeaways

1. **Iterator functions (X)** calculate per row, then aggregate — essential for multi-column calculations
2. **SUMX** = sum of a row-level expression; **AVERAGEX** = average of a row-level expression
3. **FILTER** returns a filtered table — use inside CALCULATE or iterators for conditional aggregation
4. **RANKX** creates dynamic rankings — use `ALL` to rank across all values
5. Use **CALCULATE + FILTER** for complex conditional measures

---

## Preparation for Session 19
- Ensure your model has a **Date table** (from Session 8)
- Verify: Date table is marked as Date Table (Modeling → Mark as Date Table)
- Think about: How would you calculate "Revenue this year vs last year"?

---

*Session 18 of 30 | Module 4: DAX Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
