# Session 4 — Importing & Loading Data
## Module 1: Business Intelligence Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Import Multiple Files into Power BI

---

## Learning Objectives
By the end of this session, you will be able to:
1. Import data from Excel workbooks (tables, sheets, named ranges)
2. Import CSV files with correct delimiter and encoding settings
3. Combine multiple files using the Folder connector
4. Understand Load vs Transform Data decisions
5. Configure data refresh and understand gateways

---

## 4.1 The Import Process

### Decision Flow
```
Get Data → Navigator (Preview)
              │
              ├── Data looks clean? → Click "Load" → Data goes directly into Model
              │
              └── Data needs cleaning? → Click "Transform Data" → Opens Power Query Editor
                                                                       │
                                                                       └── Clean → Close & Apply → Data goes into Model
```

### Load vs Transform Data

| Option | When to Use |
|--------|-------------|
| **Load** | Data is already clean — correct headers, no blanks, right types |
| **Transform Data** | Data needs cleaning — wrong headers, nulls, type issues, formatting |

> **Best Practice:** ALWAYS click **Transform Data** first. Inspect before loading. Even "clean" data often has hidden issues.

---

## 4.2 Importing from Excel — Deep Dive

### What Power BI Can Import from Excel

| Element | Importable? | Quality | Notes |
|---------|-------------|---------|-------|
| **Tables** (Ctrl+T formatted) | ✅ | Best | Clean, named, structured — preferred |
| **Named Ranges** | ✅ | Good | Appears in Navigator by name |
| **Worksheets** | ✅ | Okay | Imports entire used range (may include blanks) |
| **Pivot Tables** | ❌ | — | Import the source data instead |
| **Charts** | ❌ | — | Rebuild in Power BI |
| **Macros / VBA** | ❌ | — | Not supported |
| **Cell Formatting** | ❌ | — | Colors, fonts, conditional formatting ignored |
| **Merged Cells** | ⚠️ | Poor | Causes null values — unmerge before importing |

### Best Practices for Excel Source Files

1. **Format data as a Table** (Ctrl+T) before importing
   - Named tables appear clearly in Navigator
   - Column headers are automatic
   - Data range is auto-detected
2. **No merged cells** — unmerge and fill down before importing
3. **No blank rows or columns** within the data range
4. **Consistent data types** per column — don't mix text and numbers
5. **Descriptive column headers** in Row 1 — avoid "Column1", "Field2"
6. **No totals/subtotals rows** — Power BI calculates these dynamically via DAX
7. **No multi-row headers** — one clean header row only
8. **Remove formatting-only rows** — blank rows used as visual separators

### Common Excel Import Problems

| Problem | What Happens | Solution |
|---------|-------------|----------|
| Merged cells | Null values in merged area | Unmerge → Fill Down in Excel or Power Query |
| Totals row at bottom | Inflates SUM calculations | Remove in Excel or filter out in Power Query |
| Multiple header rows | First row taken as header, rest as data | Promote correct row in Power Query |
| Hidden columns/rows | Still imported | Remove in Power Query if not needed |
| Data starts at Row 5 | Rows 1–4 become data rows | Skip rows / promote headers in Power Query |
| Named range vs sheet | Both appear in Navigator | Select the correct one |

---

## 4.3 Importing from CSV — Deep Dive

### CSV Import Settings Dialog

| Setting | Options | Default | When to Change |
|---------|---------|---------|----------------|
| **File Origin** | UTF-8, UTF-16, Windows-1252, etc. | Auto-detected | Special characters garbled |
| **Delimiter** | Comma, Tab, Semicolon, Pipe, Custom | Auto-detected | European CSVs (semicolon) |
| **Data Type Detection** | First 200 rows / Entire dataset | First 200 rows | Mixed types in long files |
| **Header** | First row is header / No header | Auto-detected | File starts with data, no headers |

### Common CSV Issues and Fixes

| Issue | Cause | Solution |
|-------|-------|----------|
| Garbled characters (ö, ñ, ₹) | Wrong encoding | Change File Origin to UTF-8 |
| All data in one column | Wrong delimiter | Change delimiter (semicolon for European) |
| Numbers: 1.000,50 | European number format | Set Locale in Power Query (Transform → Locale) |
| Missing headers | No header row in file | Uncheck "First row as header" |
| Extra quotes around values | Quoted CSV format | Power BI handles this automatically |
| Trailing commas | Extra empty column | Remove empty column in Power Query |
| Line breaks inside values | Multi-line text fields | Usually handled; check for split rows |

### CSV vs Excel: When to Use Which

| Factor | CSV | Excel |
|--------|-----|-------|
| **File size** | Handles very large files efficiently | Slower with 100K+ rows |
| **Data types** | No type info — Power BI guesses | Preserves some type information |
| **Multiple tables** | One table per file | Multiple sheets/tables per file |
| **Formulas** | No formulas — raw data only | Formulas may cause issues (import values) |
| **Best for** | System exports, data feeds | Manual business data, multi-sheet workbooks |

---

## 4.4 Importing Multiple Files — Folder Connector

### When to Use the Folder Connector
- You have **multiple files with the same structure** (same columns)
- Examples: Monthly sales reports, daily transaction logs, regional data files
- Files are all in one folder (or subfolders)

### Step-by-Step: Folder Connector

```
Step 1: Place all files in a single folder
           └── Sales_Data/
                ├── Sales_Jan2024.xlsx
                ├── Sales_Feb2024.xlsx
                ├── Sales_Mar2024.xlsx
                └── Sales_Apr2024.xlsx

Step 2: Get Data → Folder → Browse to the folder

Step 3: Power BI shows file listing → Click "Combine & Transform Data"

Step 4: Select the sample file and table/sheet to use as template

Step 5: Power BI auto-combines all files into ONE table
         - Adds a "Source.Name" column (file name) for tracking
         - Applies the same transformation to every file
```

### Folder Connector Advantages
- **Scalability:** Add new files to the folder → Refresh → Automatically included
- **Source tracking:** `Source.Name` column tells you which file each row came from
- **Consistency:** Same cleaning steps applied to every file
- **Automation:** Monthly files are auto-included without editing the query

### Folder Connector Requirements
- All files must have the **same column structure**
- Same file type (all Excel or all CSV — don't mix)
- Same sheet/table name if Excel
- Consistent column naming across files

---

## 4.5 Other Import Methods

### Enter Data (Manual Table)
- **Home → Enter Data** — type data directly into a table
- Best for: Small lookup tables, mapping tables, manual reference data
- Example: Region mapping, status codes, target values
- Limited to small datasets (not for large data entry)

### Blank Query (M Code)
- **Home → Get Data → Blank Query** — write M language directly
- For advanced users who need custom data connections
- Not needed for this course until advanced topics

### Dataflows
- Reusable data preparation in Power BI Service (cloud)
- Create once → use across multiple reports
- Enterprise feature — covered conceptually in Session 26+

---

## 4.6 Data Refresh

### Desktop Refresh
| Action | How |
|--------|-----|
| Manual refresh | Home → **Refresh** button |
| What it does | Re-queries ALL data sources and reloads |
| When to use | After source data changes |

### Service Refresh (after publishing)

| License | Max Scheduled Refreshes | Gateway Needed? |
|---------|------------------------|-----------------|
| **Pro** | 8 times per day | Yes, if on-premises source |
| **Premium Per User** | 48 times per day | Yes, if on-premises source |
| **Premium Capacity** | 48 times per day | Yes, if on-premises source |

### Data Gateway

A **gateway** is a bridge between on-premises data sources and Power BI Service.

```
On-Premises Data (Excel on file server, SQL Server)
        │
        ▼
   DATA GATEWAY (installed on a server in your network)
        │
        ▼
   Power BI Service (cloud) → Scheduled Refresh
```

| Gateway Type | For | Use Case |
|-------------|-----|----------|
| **Personal Mode** | One user | Individual reports with local files |
| **Standard (Enterprise)** | Shared | Team/org-wide scheduled refresh |

> **Note:** If your Excel file is on your laptop, you need a gateway for scheduled refresh. If it's on SharePoint/OneDrive, no gateway needed.

---

## 4.7 Data Source Settings

### Managing Connections
- **File → Options → Data Source Settings**
- View all data sources connected in the current file
- **Change Source** — update file path or server name
- **Edit Permissions** — manage credentials
- **Clear Permissions** — remove saved credentials

### Common Issue: "We couldn't find the file"
When you move or rename a source file:
1. Go to **Data Source Settings**
2. Select the source → **Change Source**
3. Browse to the new location
4. Click **OK** → Refresh

---

## 🔧 Hands-On Activity: Multi-Source Import Project

**Duration:** 25 minutes

### Setup
Create a folder called `PowerBI_Practice_Data` with these files:
- **Sales_Data.xlsx** — any sales dataset with columns: Date, Product, Region, Revenue, Quantity
- **Targets.csv** — columns: Region, Monthly_Target
- (Optional) **Sales_Jan.xlsx**, **Sales_Feb.xlsx** — same structure for Folder connector

### Tasks

**Task 1 — Import Excel**
1. Open Power BI Desktop → Home → Get Data → Excel Workbook
2. Select `Sales_Data.xlsx`
3. In Navigator: select the table → Click **Transform Data**
4. In Power Query: verify all column types are correct
5. Click **Close & Apply**

**Task 2 — Import CSV**
1. Home → Get Data → Text/CSV
2. Select `Targets.csv`
3. Verify delimiter and encoding
4. Click **Transform Data** → verify → **Close & Apply**

**Task 3 — Folder Connector (if multiple files prepared)**
1. Home → Get Data → Folder
2. Browse to the folder with monthly files
3. Click **Combine & Transform Data**
4. Select the sample table → Apply
5. Verify the combined table has a `Source.Name` column

### Verification Checklist
- [ ] Switch to **Table View** — all tables visible in Fields pane
- [ ] Column data types correct (dates are dates, numbers are numbers)
- [ ] No error rows or unexpected nulls
- [ ] Save as `Practice_Session4.pbix`

---

## Session 4 — Key Takeaways

1. Always click **Transform Data** before loading — inspect your data first
2. Format Excel data as **Tables (Ctrl+T)** before importing
3. **No merged cells**, no totals rows, no blank rows in source files
4. Use the **Folder connector** for combining multiple files of the same structure
5. **Data Source Settings** lets you update file paths when sources move
6. **Gateways** bridge on-premises data to Power BI Service for scheduled refresh

---

## Preparation for Session 5
- Keep `Practice_Session4.pbix` open — we'll use it in Session 5
- Think about what cleaning steps your data needs (duplicates, nulls, wrong types, unwanted columns)

---

*Session 4 of 30 | Module 1: Business Intelligence Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
