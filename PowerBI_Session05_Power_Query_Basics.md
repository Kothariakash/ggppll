# Session 5 — Power Query Basics
## Module 1: Business Intelligence Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Clean & Transform Data in Power Query

---

## Learning Objectives
By the end of this session, you will be able to:
1. Navigate the Power Query Editor interface
2. Apply essential data cleaning steps (remove columns, change types, handle nulls)
3. Understand Applied Steps and the M language foundation
4. Use common transformations: split, merge, replace, filter, sort
5. Build a repeatable cleaning pipeline for any dataset

---

## 5.1 What is Power Query?

**Power Query** is the data transformation engine inside Power BI (and Excel). It handles the **ETL** process — Extract, Transform, Load.

### Why Power Query?
| Without Power Query | With Power Query |
|--------------------|-----------------|
| Clean data manually in Excel every time | Clean once — refreshes automatically |
| Formulas break when data changes | Transformations are recorded as steps |
| Copy-paste between files | Connect and combine automatically |
| One person's process — no documentation | Steps are visible, editable, shareable |

### Key Concept: Power Query Records Steps, Not Results
- Every action you take in Power Query is recorded as a **step**
- Steps are listed in the **Applied Steps** pane (right side)
- When you refresh, Power Query **replays all steps** on the new data
- This makes your cleaning **repeatable and automatic**

---

## 5.2 Power Query Editor Interface

```
┌──────────────────────────────────────────────────────────────────┐
│  RIBBON (Home | Transform | Add Column | View)                  │
├──────────┬──────────────────────────────────┬────────────────────┤
│          │                                  │                    │
│ QUERIES  │       DATA PREVIEW               │  QUERY SETTINGS    │
│  PANE    │                                  │                    │
│          │  (Shows current state of data)   │  - Properties      │
│ (list    │                                  │    (query name)    │
│  of all  │  ┌─────┬─────┬─────┬─────┐      │                    │
│  tables) │  │Col1 │Col2 │Col3 │Col4 │      │  - Applied Steps   │
│          │  ├─────┼─────┼─────┼─────┤      │    ├ Source         │
│          │  │data │data │data │data │      │    ├ Navigation     │
│          │  │data │data │data │data │      │    ├ Changed Type   │
│          │  │data │data │data │data │      │    ├ Removed Cols   │
│          │  └─────┴─────┴─────┴─────┘      │    └ Filtered Rows  │
│          │                                  │                    │
├──────────┴──────────────────────────────────┴────────────────────┤
│  FORMULA BAR (shows M code for selected step)                   │
└──────────────────────────────────────────────────────────────────┘
```

### Opening Power Query
- **Method 1:** Home → Transform Data (opens all queries)
- **Method 2:** Right-click a table in Fields pane → Edit Query
- **Method 3:** When importing data → click "Transform Data" instead of "Load"

### Ribbon Tabs in Power Query

| Tab | Key Functions |
|-----|---------------|
| **Home** | Close & Apply, Remove Columns, Keep/Remove Rows, Data Types, Merge/Append Queries |
| **Transform** | Transpose, Pivot/Unpivot, Replace Values, Split Column, Group By, Fill Down |
| **Add Column** | Custom Column, Conditional Column, Column from Examples, Index Column |
| **View** | Formula Bar, Column Quality, Column Distribution, Column Profile |

---

## 5.3 Essential Power Query Operations

### Operation 1: Remove Unnecessary Columns

**Why:** Fewer columns = smaller file, faster performance, cleaner model.

**How:**
- Select column(s) to KEEP → Right-click → **Remove Other Columns**
- OR: Select column(s) to REMOVE → Right-click → **Remove Columns**

> **Best Practice:** Use "Remove Other Columns" (keep what you need). If new columns appear in source data later, they won't accidentally load.

---

### Operation 2: Change Data Types

**Why:** Correct types are essential for calculations, sorting, and relationships.

**How:**
- Click the icon in the column header (ABC, 123, 📅)
- Choose the correct type from the dropdown
- OR: Select column → Home → Data Type dropdown

| Icon | Current Type | Change To |
|------|-------------|-----------|
| ABC | Text | — |
| 123 | Whole Number | — |
| 1.2 | Decimal Number | — |
| 📅 | Date | — |
| ABC→123 | Text containing numbers | Decimal or Whole Number |
| ABC→📅 | Text containing dates | Date |

**Handling Type Change Errors:**
- If some values can't convert (e.g., "N/A" in a number column): **Error** rows appear
- Fix: Replace errors first (Replace Values → Replace "N/A" with `null`), then change type

---

### Operation 3: Remove/Replace Null and Error Values

**Remove rows with nulls:**
- Select column → Home → **Remove Rows → Remove Blank Rows**

**Replace nulls with a value:**
- Select column → Transform → **Replace Values**
- Find: `null` → Replace with: `0` (or "Unknown", etc.)

**Remove error rows:**
- Select column → Home → **Remove Rows → Remove Errors**

**Replace errors:**
- Select column → Transform → **Replace Errors** → Enter replacement value

---

### Operation 4: Rename Columns

**Why:** Clean, descriptive names make reports easier to build and read.

**How:**
- Double-click the column header → Type new name
- OR: Right-click → Rename

**Naming Conventions:**
| Bad Name | Good Name |
|----------|-----------|
| col1 | Order Date |
| amt | Revenue |
| cust_nm | Customer Name |
| qty | Quantity Sold |
| PRODUCT_CATEGORY | Product Category |

> **Best Practice:** Use Title Case with spaces: "Order Date", "Product Category", "Total Revenue"

---

### Operation 5: Filter Rows

**How:**
- Click the dropdown arrow (▼) on a column header
- Uncheck values to exclude
- Use **Text Filters**, **Number Filters**, or **Date Filters** for advanced filtering

**Common Filters:**
| Filter Type | Examples |
|------------|---------|
| **Text** | Contains, Does Not Contain, Begins With, Ends With |
| **Number** | Greater Than, Less Than, Between, Top N |
| **Date** | After, Before, Between, In the Previous N days |
| **Null** | Remove null/blank rows |

---

### Operation 6: Sort Rows

**How:**
- Click column header → Sort Ascending (A→Z, 1→9) or Descending
- Right-click column → Sort Ascending / Sort Descending

---

### Operation 7: Split Column

**Why:** One column contains multiple data points that should be separate.

**Example:**
```
Before: "Mumbai, Maharashtra"  →  After: City = "Mumbai", State = "Maharashtra"
Before: "John Smith"           →  After: First = "John", Last = "Smith"
```

**How:**
- Select column → Transform → **Split Column** → By Delimiter (comma, space, etc.)
- OR: Split by number of characters, by positions

---

### Operation 8: Replace Values

**How:**
- Select column → Transform → **Replace Values**
- Enter: Value to Find → Value to Replace With

**Common Uses:**
| Find | Replace With | Why |
|------|-------------|-----|
| "N/A" | `null` | Clean missing data indicators |
| "-" | `null` | Clean dash placeholders |
| "Yes" | "TRUE" | Standardize boolean values |
| "Bangalore" | "Bengaluru" | Standardize city names |
| "Q1" | "Quarter 1" | Expand abbreviations |

---

### Operation 9: Merge Columns

**Why:** Combine two columns into one.

**How:**
- Select multiple columns (Ctrl+Click) → Transform → **Merge Columns**
- Choose separator (space, comma, dash, custom)

**Example:**
```
First Name + Last Name → Full Name (separator: space)
"John" + "Smith" → "John Smith"
```

---

### Operation 10: Add Custom Column

**Why:** Create new columns based on logic or calculations.

**How:**
- Add Column → **Custom Column**
- Write a formula using M syntax

**Examples:**
```m
// Profit calculation
[Revenue] - [Cost]

// Categorization
if [Revenue] > 100000 then "High" else if [Revenue] > 50000 then "Medium" else "Low"

// Text extraction
Text.Start([Product Code], 3)    // First 3 characters

// Date extraction
Date.Year([Order Date])          // Extract year
```

---

### Operation 11: Conditional Column

**Why:** Add a column with values based on if/then rules — no code needed.

**How:**
- Add Column → **Conditional Column**
- Use the GUI to set conditions:

```
If [Region] equals "North"  → Output: "Zone A"
If [Region] equals "South"  → Output: "Zone B"
If [Region] equals "East"   → Output: "Zone C"
Else → "Zone D"
```

---

### Operation 12: Fill Down / Fill Up

**Why:** Fix null values caused by merged cells in Excel.

**Before:**
| Region | Sales |
|--------|-------|
| North | 500 |
| null | 300 |
| null | 400 |
| South | 600 |
| null | 200 |

**After Fill Down:**
| Region | Sales |
|--------|-------|
| North | 500 |
| North | 300 |
| North | 400 |
| South | 600 |
| South | 200 |

**How:** Select column → Transform → **Fill → Down**

---

## 5.4 Applied Steps — Your Transformation Recipe

### Understanding Applied Steps
- Every action creates a **step** in the Applied Steps pane
- Steps execute **top to bottom** in sequence
- Click any step to see the data at that point
- **Delete** a step: click the X next to it
- **Reorder** steps: right-click → Move Up/Down (careful — may break dependencies)
- **Rename** steps: right-click → Rename (makes steps self-documenting)

### Example Applied Steps
```
1. Source                    → Connected to Excel file
2. Navigation               → Selected "Sales" table
3. Promoted Headers         → Used first row as headers
4. Changed Type             → Set column data types
5. Removed Columns          → Kept only needed columns
6. Filtered Rows            → Removed rows where Status = "Cancelled"
7. Replaced Value           → Changed "N/A" to null
8. Added Custom Column      → Created "Profit" = Revenue - Cost
9. Changed Type1            → Set Profit column to Decimal
```

> **Key Insight:** This recipe replays automatically every time you refresh. Change the source file → Refresh → same cleaning applies.

---

## 5.5 The M Language (Introduction)

- Every Power Query step generates **M code** behind the scenes
- Visible in the **Formula Bar** (View → Formula Bar if not visible)
- You don't need to write M code — the GUI generates it for you
- But understanding it helps for debugging and advanced scenarios

### Example M Code (auto-generated)
```m
let
    Source = Excel.Workbook(File.Contents("C:\Data\Sales.xlsx"), null, true),
    Sales_Table = Source{[Item="Sales",Kind="Table"]}[Data],
    #"Promoted Headers" = Table.PromoteHeaders(Sales_Table, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",
        {{"Date", type date}, {"Revenue", type number}, {"Region", type text}}),
    #"Removed Columns" = Table.RemoveColumns(#"Changed Type", {"Column5", "Notes"}),
    #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [Revenue] > 0)
in
    #"Filtered Rows"
```

> **For this course:** You won't need to write M code. But know it exists and powers everything in Power Query.

---

## 5.6 Column Quality, Distribution & Profile

### Data Profiling Tools (View Tab)

| Tool | What It Shows | Use For |
|------|--------------|---------|
| **Column Quality** | % Valid, % Error, % Empty per column | Spotting data quality issues at a glance |
| **Column Distribution** | Bar chart of distinct vs unique values | Understanding cardinality |
| **Column Profile** | Full statistics (min, max, avg, count, nulls) | Deep dive into one column |

**How to Enable:**
- Power Query → **View** tab → Check **Column Quality**, **Column Distribution**, **Column Profile**

> **Important:** By default, profiling is based on **first 1,000 rows**. Change to **entire dataset**: click "Column profiling based on top 1000 rows" in the status bar → select "Column profiling based on entire dataset."

---

## 🔧 Hands-On Activity: Data Cleaning Pipeline

**Duration:** 25 minutes

### Dataset
Use the sales data imported in Session 4 (or any dataset with at least 6 columns and some quality issues).

### Cleaning Tasks

1. **Open Power Query:** Home → Transform Data
2. **Enable profiling:** View → check Column Quality + Column Distribution
3. **Remove unnecessary columns** (keep only business-relevant ones)
4. **Rename columns** to clean Title Case names
5. **Change data types:** ensure dates are Date, numbers are Decimal/Whole
6. **Handle nulls:** Replace null values in a text column with "Unknown"
7. **Filter rows:** Remove rows where Revenue = 0 or negative
8. **Add a Custom Column:** Create "Revenue Category"
   - If Revenue > 100000 → "High"
   - If Revenue > 50000 → "Medium"
   - Else → "Low"
9. **Fill Down:** If any column has null patterns from merged cells
10. **Review Applied Steps:** Rename each step descriptively
11. **Close & Apply**

### Verification
- Switch to **Table View** — verify cleaned data
- Check that the new "Revenue Category" column exists with correct values
- Save the file

---

## Session 5 — Key Takeaways

1. **Power Query** is your data cleaning engine — clean once, refresh automatically
2. Every action is recorded as an **Applied Step** — your transformation recipe
3. **Essential operations:** Remove columns, Change types, Filter rows, Replace values, Add custom columns
4. Enable **Column Quality/Distribution/Profile** to spot issues fast
5. Always click **Transform Data** (not Load) — inspect before loading
6. M language powers everything behind the scenes — GUI generates it for you

---

## Module 1 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 1 | Introduction to BI | Understand BI concepts and Power BI ecosystem |
| 2 | Power BI Interface | Navigate Desktop — views, panes, ribbon |
| 3 | Data Types & Sources | Connect to Excel, CSV, Web; set correct types |
| 4 | Importing Data | Multi-source import, Folder connector, refresh |
| 5 | Power Query Basics | Clean and transform data with repeatable steps |

### Module 1 → Module 2 Bridge
You can now **connect to data and clean it**. In Module 2 (Sessions 6–10), you'll learn to **model** that data — creating relationships between tables, building Star Schemas, and validating data quality.

---

## Preparation for Session 6
- Have at least 2–3 related tables loaded (e.g., Orders + Products + Customers)
- Think about how these tables relate to each other (what columns connect them?)
- Review: What is a Primary Key? What is a Foreign Key?

---

*Session 5 of 30 | Module 1: Business Intelligence Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
