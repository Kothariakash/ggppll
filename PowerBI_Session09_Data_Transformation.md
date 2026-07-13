# Session 9 — Advanced Data Transformation
## Module 2: Data Modeling & Relationships | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Pivot, Unpivot, Merge, Append Queries

---

## Learning Objectives
By the end of this session, you will be able to:
1. Use Pivot and Unpivot to reshape data
2. Merge Queries (like VLOOKUP/JOIN) to combine tables
3. Append Queries to stack tables vertically
4. Apply Group By for aggregation in Power Query
5. Use advanced column transformations (Extract, Parse, Conditional)

---

## 9.1 Pivot and Unpivot

### Unpivot — Convert Columns to Rows

**When to use:** Data is in "wide" format (months as columns) and needs to be "tall" (months as rows).

**Before (Wide — Column per Month):**
| Product | Jan | Feb | Mar |
|---------|-----|-----|-----|
| Laptop | 50 | 60 | 55 |
| Mouse | 200 | 180 | 220 |

**After Unpivot (Tall — Month as Row):**
| Product | Month | Sales |
|---------|-------|-------|
| Laptop | Jan | 50 |
| Laptop | Feb | 60 |
| Laptop | Mar | 55 |
| Mouse | Jan | 200 |
| Mouse | Feb | 180 |
| Mouse | Mar | 220 |

**How to Unpivot:**
1. Select the columns you want to KEEP (e.g., Product)
2. Right-click → **Unpivot Other Columns**
3. Two new columns appear: **Attribute** (column names) and **Value** (cell values)
4. Rename: Attribute → "Month", Value → "Sales"

> **Best Practice:** Select columns to KEEP, then "Unpivot Other Columns." This way, if new month columns appear later, they're automatically unpivoted.

**Unpivot Options:**
| Option | Behavior |
|--------|----------|
| **Unpivot Columns** | Unpivots only selected columns |
| **Unpivot Other Columns** | Keeps selected, unpivots everything else (preferred) |
| **Unpivot Only Selected Columns** | Strict — only those exact columns |

---

### Pivot — Convert Rows to Columns

**When to use:** Data is "tall" and you need it "wide" — typically for reporting layouts.

**Before (Tall):**
| Product | Region | Revenue |
|---------|--------|---------|
| Laptop | North | 50000 |
| Laptop | South | 60000 |
| Mouse | North | 8000 |
| Mouse | South | 12000 |

**After Pivot (Wide):**
| Product | North | South |
|---------|-------|-------|
| Laptop | 50000 | 60000 |
| Mouse | 8000 | 12000 |

**How to Pivot:**
1. Select the column whose values become new column headers (e.g., Region)
2. Transform → **Pivot Column**
3. Choose the Values column (e.g., Revenue)
4. Choose the aggregation (Sum, Count, Don't Aggregate)

> **Note:** Pivoting is less common in Power BI because the matrix visual handles row/column layouts dynamically. Unpivot is far more frequently needed.

---

## 9.2 Merge Queries (JOIN / VLOOKUP Equivalent)

### What is Merge Queries?

**Merge** combines two tables horizontally by matching rows on a common column — similar to VLOOKUP in Excel or JOIN in SQL.

```
Orders Table                Products Table
┌───────┬───────────┐       ┌───────┬──────────┬──────────┐
│OrderID│ ProductID │       │ProdID │ ProdName │ Category │
├───────┼───────────┤       ├───────┼──────────┼──────────┤
│ 1001  │  P-101    │       │ P-101 │ Laptop   │ Electronics│
│ 1002  │  P-205    │       │ P-205 │ Chair    │ Furniture  │
│ 1003  │  P-101    │       │ P-310 │ Notebook │ Stationery │
└───────┴───────────┘       └───────┴──────────┴──────────┘

After MERGE (Left Outer Join on ProductID):

┌───────┬───────────┬──────────┬──────────┐
│OrderID│ ProductID │ ProdName │ Category │
├───────┼───────────┼──────────┼──────────┤
│ 1001  │  P-101    │ Laptop   │ Electronics│
│ 1002  │  P-205    │ Chair    │ Furniture  │
│ 1003  │  P-101    │ Laptop   │ Electronics│
└───────┴───────────┴──────────┴──────────┘
```

### How to Merge Queries
1. Power Query → Select the primary table (e.g., Orders)
2. Home → **Merge Queries**
3. Select the second table (e.g., Products)
4. Click the matching column in both tables (ProductID)
5. Choose the **Join Kind**
6. Click OK → Expand the new column to select which fields to bring in

### Join Kinds

| Join Kind | Returns | SQL Equivalent |
|-----------|---------|---------------|
| **Left Outer** | All rows from left + matching from right | LEFT JOIN |
| **Right Outer** | All rows from right + matching from left | RIGHT JOIN |
| **Full Outer** | All rows from both tables | FULL OUTER JOIN |
| **Inner** | Only rows that match in BOTH tables | INNER JOIN |
| **Left Anti** | Left rows with NO match in right | LEFT JOIN WHERE right IS NULL |
| **Right Anti** | Right rows with NO match in left | RIGHT JOIN WHERE left IS NULL |

### Most Common: Left Outer Join
- Keeps ALL rows from your main table
- Adds matching data from the lookup table
- Unmatched rows get `null` for the added columns
- **This is your VLOOKUP equivalent**

### When to Use Merge vs Relationships

| Scenario | Use |
|----------|-----|
| Need data from another table in a calculated column | **Merge** in Power Query |
| Need to combine for DAX measures and visuals | **Relationship** in Model View |
| Lookup table is only needed for a column, not as a dimension | **Merge** |
| Both tables appear independently in visuals | **Relationship** |

> **General Rule:** Prefer **Relationships** over Merge. Only Merge when you need to physically add columns to a table before loading.

---

## 9.3 Append Queries (UNION / Stack Tables)

### What is Append?

**Append** stacks tables **vertically** — combining rows from multiple tables with the same structure.

```
Q1 Sales                    Q2 Sales
┌───────┬─────────┐         ┌───────┬─────────┐
│ Month │ Revenue │         │ Month │ Revenue │
├───────┼─────────┤         ├───────┼─────────┤
│ Jan   │ 50000   │         │ Apr   │ 55000   │
│ Feb   │ 48000   │         │ May   │ 62000   │
│ Mar   │ 52000   │         │ Jun   │ 58000   │
└───────┴─────────┘         └───────┴─────────┘

After APPEND:
┌───────┬─────────┐
│ Month │ Revenue │
├───────┼─────────┤
│ Jan   │ 50000   │
│ Feb   │ 48000   │
│ Mar   │ 52000   │
│ Apr   │ 55000   │
│ May   │ 62000   │
│ Jun   │ 58000   │
└───────┴─────────┘
```

### How to Append
1. Power Query → Select any table
2. Home → **Append Queries** (or Append Queries as New)
3. Choose: **Two tables** or **Three or more tables**
4. Select tables to append → OK

### Append Options
| Option | Result |
|--------|--------|
| **Append Queries** | Adds rows to the current query |
| **Append Queries as New** | Creates a new combined query (original tables unchanged) |

### Requirements
- Tables should have the **same column names** (matching is by column name)
- If columns don't match: non-matching columns get `null` values
- Data types should be consistent across tables

### Append vs Folder Connector

| Feature | Append | Folder Connector |
|---------|--------|-----------------|
| **Setup** | Manual — select each table | Automatic — reads all files in folder |
| **New files** | Manually add and append | Auto-included on refresh |
| **Best for** | Combining different queries | Combining same-structure files |

---

## 9.4 Group By (Aggregation in Power Query)

### What is Group By?

**Group By** aggregates data — like a pivot table or SQL GROUP BY.

**Before:**
| Region | Product | Revenue |
|--------|---------|---------|
| North | Laptop | 50000 |
| North | Mouse | 8000 |
| North | Laptop | 45000 |
| South | Mouse | 12000 |
| South | Laptop | 60000 |

**After Group By (Region, Sum of Revenue):**
| Region | Total Revenue |
|--------|--------------|
| North | 103000 |
| South | 72000 |

### How to Group By
1. Select the column(s) to group by
2. Transform → **Group By**
3. Choose **Basic** (one aggregation) or **Advanced** (multiple)
4. Set: New column name, Operation (Sum, Count, Average, Min, Max), Column

### Available Aggregations

| Operation | Description |
|-----------|------------|
| **Sum** | Total of values |
| **Average** | Mean of values |
| **Min** | Smallest value |
| **Max** | Largest value |
| **Count Rows** | Number of rows |
| **Count Distinct** | Number of unique values |
| **All Rows** | Nested table of detail rows (advanced) |

### Advanced Group By — Multiple Aggregations
```
Group By: Region
  → Total Revenue = Sum of Revenue
  → Order Count = Count Rows
  → Avg Order Value = Average of Revenue
  → Top Sale = Max of Revenue
```

---

## 9.5 Advanced Column Operations

### Extract (from Text columns)

| Operation | Example | Result |
|-----------|---------|--------|
| **First Characters** | Extract first 3 from "PRD-12345" | "PRD" |
| **Last Characters** | Extract last 5 from "PRD-12345" | "12345" |
| **Range** | Characters 5-9 from "PRD-12345" | "12345" |
| **Text Before Delimiter** | Before "-" in "PRD-12345" | "PRD" |
| **Text After Delimiter** | After "-" in "PRD-12345" | "12345" |
| **Text Between Delimiters** | Between "[" and "]" in "[Active]" | "Active" |

**How:** Select column → Transform → Extract → choose operation

### Parse (from Date columns)

| Operation | From Date 2024-03-15 |
|-----------|---------------------|
| **Year** | 2024 |
| **Month** | 3 |
| **Day** | 15 |
| **Day of Week** | Friday |
| **Quarter** | 1 |
| **Week of Year** | 11 |

**How:** Select date column → Transform → Date → choose extraction

### Text Transformations

| Operation | Before | After |
|-----------|--------|-------|
| **Trim** | "  Mumbai  " | "Mumbai" |
| **Clean** | "Mumbai\n" | "Mumbai" |
| **UPPERCASE** | "mumbai" | "MUMBAI" |
| **lowercase** | "MUMBAI" | "mumbai" |
| **Capitalize Each Word** | "john smith" | "John Smith" |
| **Add Prefix** | "101" (prefix "PRD-") | "PRD-101" |
| **Add Suffix** | "2024" (suffix "-Q1") | "2024-Q1" |

---

## 9.6 Transformation Order Best Practices

### Recommended Order of Operations in Power Query

```
1. Source connection
2. Remove unnecessary COLUMNS (early = better performance)
3. Filter unnecessary ROWS (early = less data to process)
4. Change DATA TYPES
5. Rename COLUMNS
6. Handle NULLS and ERRORS (Replace Values)
7. MERGE queries (if needed)
8. UNPIVOT (if needed)
9. GROUP BY (if needed)
10. ADD calculated columns
11. Final type check
```

> **Key Principle:** Remove data you don't need **as early as possible** — every subsequent step processes less data.

---

## 🔧 Hands-On Activity: Advanced Transformations

**Duration:** 25 minutes

### Task 1 — Unpivot Monthly Data
1. Create (Enter Data) or import a table with: Product, Jan, Feb, Mar, Apr, May, Jun
2. Open in Power Query
3. Select "Product" column → Right-click → **Unpivot Other Columns**
4. Rename: Attribute → "Month", Value → "Revenue"
5. Change Revenue type to Decimal Number

### Task 2 — Merge Queries
1. Have two tables loaded: Orders (with ProductID) and Products (with ProductID, Name, Category)
2. Select Orders table → Home → **Merge Queries**
3. Match on ProductID → Left Outer Join
4. Expand the Products column → select ProductName and Category
5. Verify the merged data

### Task 3 — Group By
1. Using the Sales/Orders table
2. Transform → Group By → Group by Region
3. Add aggregations: Sum of Revenue, Count of Orders
4. Review the aggregated result

### Task 4 — Append
1. If you have Q1 and Q2 tables (same structure)
2. Select Q1 → Home → **Append Queries as New**
3. Select Q2 → OK
4. Verify combined row count = Q1 rows + Q2 rows

---

## Session 9 — Key Takeaways

1. **Unpivot** converts columns to rows — essential for "wide" data (months as columns)
2. **Merge Queries** = VLOOKUP/JOIN — combines tables horizontally on a common column
3. **Append Queries** = UNION — stacks tables vertically (same structure)
4. **Group By** aggregates data in Power Query — Sum, Count, Average by category
5. Remove unneeded columns and rows **early** in the transformation pipeline

---

## Preparation for Session 10
- Review your data model: Are all relationships correct?
- Think about: How would you validate that your data is complete and accurate?
- Consider: What quality checks would you run before building reports?

---

*Session 9 of 30 | Module 2: Data Modeling & Relationships*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
