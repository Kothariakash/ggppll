# Session 10 — Data Validation & Quality Assurance
## Module 2: Data Modeling & Relationships | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Validate Data Model & Data Quality

---

## Learning Objectives
By the end of this session, you will be able to:
1. Validate data completeness, accuracy, and consistency
2. Use Power Query profiling tools for quality assessment
3. Check relationship integrity in Model View
4. Build validation visuals (card checks, row counts, totals)
5. Apply a data quality checklist before building reports

---

## 10.1 Why Data Validation Matters

> "A beautiful dashboard built on bad data is worse than no dashboard at all."

### The Cost of Bad Data
| Issue | Business Impact |
|-------|----------------|
| Missing rows | Understated revenue, wrong KPIs |
| Duplicate rows | Overstated revenue, inflated counts |
| Wrong data types | Broken calculations, incorrect sorting |
| Null values in keys | Orphan rows, "(Blank)" in visuals |
| Incorrect relationships | Wrong numbers when filtering |

### When to Validate

```
Import Data → Clean (Power Query) → VALIDATE → Model → VALIDATE → Build Visuals → VALIDATE
```

Validation happens at **three stages:**
1. **After Power Query** — Is the data clean and complete?
2. **After Data Modeling** — Are relationships correct?
3. **After Building Visuals** — Do the numbers make sense?

---

## 10.2 Stage 1: Power Query Data Profiling

### Enable Profiling Tools
Power Query → **View** tab → check all three:
- ✅ Column Quality
- ✅ Column Distribution
- ✅ Column Profile

> **Important:** Click the status bar message "Column profiling based on top 1000 rows" → change to **"Column profiling based on entire dataset"**

### Column Quality

Shows three metrics per column header:

| Metric | Meaning | Action |
|--------|---------|--------|
| **Valid** | Percentage of correctly typed values | Should be 100% |
| **Error** | Percentage of values that failed type conversion | Investigate and fix |
| **Empty** | Percentage of null/blank values | Decide: replace, remove, or accept |

**Target:** 100% Valid, 0% Error for every column

### Column Distribution

Shows a bar chart per column:
| Metric | Meaning | What to Look For |
|--------|---------|-----------------|
| **Distinct** | Number of unique values | Key columns should equal row count |
| **Unique** | Values appearing exactly once | If Distinct = Unique, all values are unique (good for PKs) |

**Use for:**
- Verifying Primary Keys: Distinct count should equal total row count
- Spotting unexpected duplicates
- Checking cardinality of categorical columns

### Column Profile (select one column)

Shows detailed statistics:
| Statistic | Use |
|-----------|-----|
| **Count** | Total non-null values |
| **Error** | Error count |
| **Empty** | Null count |
| **Min / Max** | Range check — are values reasonable? |
| **Average** | Sanity check for numeric columns |
| **Standard Deviation** | Spread of values |
| **Value Distribution** | Frequency chart of top values |

---

## 10.3 Data Quality Checks in Power Query

### Check 1: Row Count Validation

**Why:** Ensure no rows were lost or duplicated during transformation.

**How:**
- Note the row count at the **Source** step (bottom-left of Power Query)
- Compare with row count at the **final step**
- If different: click through Applied Steps to find where rows were added/removed

**Expected:**
| Transformation | Row Count Should |
|---------------|-----------------|
| Remove duplicates | Decrease (by duplicate count) |
| Filter rows | Decrease |
| Append queries | Increase (sum of both tables) |
| Merge queries | Stay the same (Left Outer Join) |
| Unpivot | Increase (columns × rows) |

### Check 2: Null/Blank Analysis

For each column, check:
- **Key columns (IDs):** Should have 0% empty — nulls break relationships
- **Required fields (Name, Date):** Should have 0% empty
- **Optional fields (Phone, Notes):** Acceptable to have some blanks

### Check 3: Duplicate Detection

**For Dimension tables (Primary Key must be unique):**
1. Select the key column
2. Home → **Remove Rows → Remove Duplicates**
3. If row count changes → you had duplicates → investigate why

**For Fact tables (may have legitimate duplicates):**
- Check for exact duplicate rows (all columns identical)
- Select all columns → Remove Duplicates
- If count changes, true duplicates existed

### Check 4: Value Range Validation

| Column | Check | Flag If |
|--------|-------|---------|
| Revenue | Min ≥ 0 | Negative revenue (unless returns allowed) |
| Quantity | Min ≥ 1 | Zero or negative quantities |
| Date | Min/Max in expected range | Dates in 1900 or 2099 |
| Percentage | Between 0 and 1 (or 0-100) | Values outside expected range |
| Age | Between 18 and 100 | Unreasonable values |

### Check 5: Consistency Check

| Issue | Example | Fix |
|-------|---------|-----|
| Same entity, different names | "Mumbai" vs "MUMBAI" vs "mumbai" | Capitalize Each Word |
| Trailing spaces | "Delhi " vs "Delhi" | Trim |
| Inconsistent formats | "15/01/2024" vs "2024-01-15" | Standardize date format |
| Abbreviation mix | "Mah" vs "Maharashtra" | Replace Values |

---

## 10.4 Stage 2: Relationship Validation

### Check 1: Relationship Completeness

Open Model View and verify:

- [ ] Every Fact table FK has a relationship to a Dimension PK
- [ ] All relationships are **1:Many** (Dimension → Fact)
- [ ] Cross-filter direction is **Single** (unless specifically needed)
- [ ] No orphan tables (unconnected tables)
- [ ] No circular references

### Check 2: Referential Integrity

**Question:** Does every Foreign Key value in the Fact table have a matching Primary Key in the Dimension?

**Test:**
1. Create a Table visual: Dimension Key column + Count of Fact rows
2. If "(Blank)" appears → some Fact rows have no matching Dimension
3. **Fix options:**
   - Add the missing values to the Dimension table
   - Remove orphan rows from the Fact table
   - Accept and handle "(Blank)" in visuals with filters

### Check 3: Relationship Direction Test

**Test with a slicer:**
1. Add a Slicer for a Dimension column (e.g., Product Category)
2. Add a Card visual showing SUM of Revenue (from Fact table)
3. Click different slicer values → Card should update
4. If it doesn't update → relationship is broken or wrong direction

### Check 4: Cross-Table Calculation Test

Create a Matrix visual:
- Rows: Product Category (from Products dimension)
- Columns: Year (from Date dimension)
- Values: Sum of Revenue (from Sales fact)

If this works correctly and shows different values per cell → relationships are working.

---

## 10.5 Stage 3: Visual Validation (Sanity Checks)

### Build Validation Cards

Create a hidden "Validation" page with these card visuals:

| Card | DAX / Field | Expected Value | Check Against |
|------|-------------|---------------|---------------|
| **Total Revenue** | SUM(Sales[Revenue]) | Known total from source | Excel source file total |
| **Row Count** | COUNTROWS(Sales) | Known row count | Source file row count |
| **Distinct Products** | DISTINCTCOUNT(Sales[ProductID]) | Known product count | Products table row count |
| **Distinct Customers** | DISTINCTCOUNT(Sales[CustomerID]) | Known customer count | Customers table count |
| **Date Range** | MIN(Sales[OrderDate]) & MAX(Sales[OrderDate]) | Expected range | Source data date range |
| **Avg Order Value** | AVERAGE(Sales[Revenue]) | Reasonable range | Manual spot check |

### The "Grand Total" Test

1. In your source Excel file: manually SUM the Revenue column → note the total
2. In Power BI: create a Card visual with SUM(Sales[Revenue])
3. **These numbers must match exactly**
4. If they don't: investigate row filters, duplicates, or type conversion errors

### The "Cross-Tab" Test

1. Create a simple pivot in Excel: Revenue by Region
2. Create the same Matrix in Power BI: Region (rows) × Sum of Revenue
3. Compare every cell — they should match
4. Mismatches indicate relationship or filter issues

---

## 10.6 Common Data Quality Issues and Fixes

| Issue | Detection Method | Fix |
|-------|-----------------|-----|
| **Duplicate rows** | Row count higher than expected | Remove Duplicates in Power Query |
| **Missing rows** | Row count lower than expected | Check filters in Applied Steps |
| **Null keys** | "(Blank)" in visuals | Replace nulls or filter in Power Query |
| **Wrong data types** | Column Quality shows errors | Change Type in Power Query |
| **Broken relationships** | Slicer doesn't filter values | Re-create relationship in Model View |
| **Wrong cardinality** | Unexpected totals, double-counting | Verify 1:Many, check for duplicate keys |
| **Wrong grand total** | Total doesn't match source | Check for filters, duplicates, type errors |
| **Date gaps** | Timeline axis has gaps | Ensure Date table has continuous dates |
| **Inconsistent names** | "Mumbai" and "MUMBAI" as separate categories | Standardize in Power Query (Capitalize Each Word) |

---

## 10.7 Data Validation Checklist

Use this checklist before building any report:

### Power Query Checks
- [ ] All columns have correct data types
- [ ] Column Quality: 100% Valid, 0% Error for critical columns
- [ ] Row count matches expected count from source
- [ ] No unexpected nulls in key or required columns
- [ ] Dimension tables have unique primary keys (no duplicates)
- [ ] Text values are consistent (no case/spacing issues)
- [ ] Dates are in expected range
- [ ] Numeric values are in reasonable range

### Model Checks
- [ ] All necessary relationships exist
- [ ] All relationships are 1:Many (Dimension → Fact)
- [ ] Cross-filter direction is Single (default)
- [ ] No orphan (unconnected) tables
- [ ] Date table is marked as Date Table
- [ ] ID/FK columns are hidden from Report View

### Visual Checks
- [ ] Grand total matches source data exactly
- [ ] Slicer filtering works across all visuals
- [ ] No unexpected "(Blank)" values
- [ ] Cross-tab values match source pivot
- [ ] Distinct counts match expected counts

---

## 🔧 Hands-On Activity: Full Data Validation

**Duration:** 25 minutes

### Tasks

**Part 1 — Power Query Profiling (10 min)**
1. Open your Power BI file with Sales, Products, Customers tables
2. Home → Transform Data (open Power Query)
3. Enable: Column Quality + Column Distribution + Column Profile
4. Set profiling to "entire dataset" (status bar)
5. For each table, document:
   - Row count
   - Any columns with Error or Empty values
   - Key column: Distinct count = Row count?
6. Fix any issues found

**Part 2 — Relationship Validation (5 min)**
1. Close Power Query → Open Model View
2. Verify all relationships: cardinality, direction
3. Check for orphan tables
4. Create a Slicer (Product Category) + Card (Sum Revenue) → test filtering

**Part 3 — Visual Validation (10 min)**
1. Create a new page called "Data Validation" (hide it later)
2. Add Card visuals:
   - Total Revenue
   - Row Count (COUNTROWS)
   - Distinct Products
   - Min Date / Max Date
3. Compare Total Revenue with your source Excel file
4. If any mismatch → investigate and fix
5. Save the file

---

## Session 10 — Key Takeaways

1. **Validate at 3 stages:** after Power Query, after Modeling, after Visuals
2. **Column Quality/Distribution/Profile** in Power Query catches most data issues
3. **Grand Total test** — Power BI total must match source total exactly
4. **Slicer test** — if a slicer doesn't filter a visual, the relationship is broken
5. Build a **hidden Validation page** with card visuals for ongoing quality monitoring

---

## Module 2 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 6 | Data Modeling Concepts | Fact vs Dimension tables, keys |
| 7 | Relationships | Create, configure, troubleshoot relationships |
| 8 | Star Schema | Design Star Schema, build Date table |
| 9 | Data Transformation | Pivot, Unpivot, Merge, Append, Group By |
| 10 | Data Validation | Quality checks, relationship validation, sanity tests |

### Module 2 → Module 3 Bridge
You now have **clean data in a proper Star Schema with validated relationships**. In Module 3 (Sessions 11–15), you'll build **interactive visualizations** — charts, maps, KPIs, slicers, and complete dashboards.

---

## Preparation for Session 11
- Have a validated Star Schema model ready (Sales + Products + Customers + Date)
- Explore: What chart types are available in the Visualizations pane?
- Think about: What business questions should your dashboard answer?

---

*Session 10 of 30 | Module 2: Data Modeling & Relationships*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
