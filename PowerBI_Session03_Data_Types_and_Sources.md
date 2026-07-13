# Session 3 — Data Types & Data Sources
## Module 1: Business Intelligence Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Demo | Hands-On: Connect to Excel, CSV, Web

---

## Learning Objectives
By the end of this session, you will be able to:
1. Identify and apply correct data types in Power BI
2. Understand why data types matter for calculations and relationships
3. Navigate the 150+ data source connectors
4. Differentiate between Import, DirectQuery, and Live Connection modes
5. Connect Power BI to Excel, CSV, and Web sources

---

## 3.1 Data Types in Power BI

### Core Data Types

| Data Type | Icon | Examples | Notes |
|-----------|------|----------|-------|
| **Whole Number** | 123 | 1, 42, -100 | No decimals; use for IDs, counts |
| **Decimal Number** | 1.2 | 3.14, 99.99, -0.5 | Use for currency, percentages, precise values |
| **Fixed Decimal** | $ | ₹1,299.00 | Exactly 4 decimal places; best for financial data |
| **Text** | ABC | "Mumbai", "Product-A" | Strings, categories, codes |
| **Date** | 📅 | 2024-01-15 | Date only (no time component) |
| **Date/Time** | 📅🕐 | 2024-01-15 14:30:00 | Date with timestamp |
| **Time** | 🕐 | 14:30:00 | Time only (no date) |
| **True/False** | ✓/✗ | TRUE, FALSE | Boolean / logical values |
| **Binary** | 🔗 | (file content) | Used for images, file references |

### Data Type Selection Guide

| Your Data | Correct Type | Why |
|-----------|-------------|-----|
| Revenue, Price, Cost | Fixed Decimal or Decimal | Precise financial calculations |
| Quantity, Count, Age | Whole Number | No decimals needed |
| Product Name, City | Text | Categorical/descriptive |
| Order Date | Date | Enables time intelligence in DAX |
| Transaction Timestamp | Date/Time | Preserves time component |
| Is Active? Yes/No | True/False | Logical filtering |
| Employee ID, ZIP Code | Text | Even if numeric — never aggregated |

> **Golden Rule:** If you would never SUM or AVERAGE a number (like ZIP code, phone number, employee ID), store it as **Text**.

---

## 3.2 Why Data Types Matter

### Problem 1: Numbers Stored as Text
```
Column "Revenue" contains: "42500", "38000", "51000"
Type detected: Text

Result: SUM(Revenue) = ERROR ❌
Fix: Change type to Decimal Number in Power Query
```

### Problem 2: Dates Stored as Text
```
Column "Order Date" contains: "15-Jan-2024", "22-Feb-2024"
Type detected: Text

Result: Date axis on charts won't work ❌
        Time intelligence DAX functions fail ❌
Fix: Change type to Date in Power Query
```

### Problem 3: Mixed Types in a Column
```
Column "Amount" contains: 1500, "N/A", 2200, "-", 3100
Type detected: Text (because of "N/A" and "-")

Result: Cannot aggregate ❌
Fix: Replace "N/A" and "-" with null, then change type to Decimal
```

### Problem 4: Leading Zeros Lost
```
Column "PIN Code" contains: 01234, 00567
If stored as Number: becomes 1234, 567 ❌

Fix: Keep as Text type — preserves leading zeros
```

### Common Data Type Issues — Quick Reference

| Problem | Symptom | Fix in Power Query |
|---------|---------|-------------------|
| Numbers as text | Can't SUM/AVG | Change Type → Decimal Number |
| Dates as text | Timeline axis broken | Change Type → Date |
| Mixed types | Errors on type change | Replace errors first, then change type |
| Leading zeros lost | ZIP/PIN codes wrong | Keep as Text |
| European decimals | 1.000,50 misread | Set Locale (German/French) |
| True/False as 1/0 | Filters don't work intuitively | Change Type → True/False |

---

## 3.3 Data Sources in Power BI

Power BI connects to **150+ data sources**. Here are the key categories:

### File Sources

| Source | Extension | Best For | Notes |
|--------|-----------|----------|-------|
| **Excel** | .xlsx, .xls | Most common business data | Tables preferred over ranges |
| **CSV** | .csv | System exports, large datasets | Watch delimiter and encoding |
| **Text** | .txt, .tsv | Tab/pipe delimited files | Specify delimiter manually |
| **JSON** | .json | API responses, web data | Nested structures may need expansion |
| **XML** | .xml | Structured hierarchical data | Auto-parsed into tables |
| **PDF** | .pdf | Extracting tables from documents | Quality depends on PDF structure |
| **Parquet** | .parquet | Modern columnar data files | Efficient for large datasets |
| **Folder** | (directory) | Combine multiple files of same structure | Powerful for monthly files |

### Database Sources

| Source | Typical Use Case |
|--------|-----------------|
| **SQL Server** | Enterprise transactional data (most common in corporate) |
| **Azure SQL Database** | Cloud-hosted SQL |
| **MySQL** | Open-source web applications |
| **PostgreSQL** | Open-source analytics databases |
| **Oracle Database** | Large enterprise systems |
| **Amazon Redshift** | AWS cloud data warehouse |
| **Google BigQuery** | GCP cloud analytics |
| **Snowflake** | Modern cloud data warehouse |
| **SAP HANA** | SAP enterprise systems |

### Online Services

| Source | Use Case |
|--------|----------|
| **SharePoint Online List** | Team data stored in SharePoint |
| **SharePoint Folder** | Files stored in SharePoint document libraries |
| **Dynamics 365** | Microsoft CRM/ERP data |
| **Salesforce** | Sales CRM data |
| **Google Analytics** | Website traffic and behavior |
| **Azure DevOps** | Development project tracking |
| **Microsoft Dataverse** | Power Platform data |
| **GitHub** | Repository and issue data |

### Other Sources

| Source | Use Case |
|--------|----------|
| **Web** | Scrape HTML tables from any URL |
| **OData Feed** | REST API endpoints |
| **ODBC / OLE DB** | Legacy database connections |
| **R Script / Python Script** | Custom data processing and import |
| **Blank Query** | Write M code manually |
| **Enter Data** | Type data directly into a table |

---

## 3.4 Connection Modes

### Three Connection Modes

| Mode | How It Works | Data Location | When to Use |
|------|-------------|---------------|-------------|
| **Import** | Copies data into .pbix file | Inside Power BI | Default. Best for files, small-medium databases |
| **DirectQuery** | Sends queries to source live | Stays in source DB | Large databases, real-time requirements |
| **Live Connection** | Connects to existing models | SSAS or Power BI datasets | Enterprise shared models |

### Import vs DirectQuery — Detailed Comparison

| Feature | Import | DirectQuery |
|---------|--------|-------------|
| **Performance** | Fast (data in RAM) | Slower (queries source every interaction) |
| **File Size** | Larger (data embedded) | Smaller (metadata only) |
| **Data Freshness** | As of last refresh | Real-time / near real-time |
| **DAX Support** | Full | Limited (some functions unavailable) |
| **Power Query** | Full | Limited |
| **Max Dataset Size** | 1 GB (Pro) / 400 GB (Premium) | No limit (data stays in source) |
| **Offline Access** | Yes | No (needs source connection) |
| **Best For** | Files, small-medium DBs, most reports | Large DBs, real-time dashboards |

### Composite Mode
- Mix **Import + DirectQuery** in the same model
- Example: Import dimension tables (small, static) + DirectQuery fact tables (large, real-time)
- Requires Premium or PPU license

> **Recommendation for this course:** Always use **Import** mode. DirectQuery is an advanced topic for enterprise scenarios.

---

## 3.5 The Get Data Experience

### Step-by-Step: Get Data

```
Home Tab → Get Data → Choose Source → Configure Connection → Navigator → Load or Transform
```

### Navigator Window
When you connect to a source, the **Navigator** shows:
- List of available tables/sheets/entities
- **Preview pane** showing first rows of data
- **Select Multiple Items** checkbox for multi-table import
- **Load** button (skip Power Query) or **Transform Data** button (open Power Query first)

### Best Practice Flow
```
Get Data → Navigator Preview → ALWAYS click "Transform Data" → Inspect → Close & Apply
```

> **Never click Load directly** until you've verified data types, headers, and quality in Power Query.

---

## 🔧 Hands-On Activity: Connect to Multiple Sources

**Duration:** 20 minutes

### Task 1 — Import from Excel
1. Home → Get Data → **Excel Workbook**
2. Browse to a sample Excel file with sales data
3. In Navigator: select the table/sheet
4. Click **Transform Data** (not Load)
5. In Power Query: verify column types → Click **Close & Apply**

### Task 2 — Import from CSV
1. Home → Get Data → **Text/CSV**
2. Browse to a `.csv` file
3. Review: delimiter (comma/semicolon), encoding (UTF-8), header row detection
4. Click **Transform Data** → verify → **Close & Apply**

### Task 3 — Import from Web
1. Home → Get Data → **Web**
2. Paste URL: `https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)`
3. Navigator shows detected HTML tables → select one
4. Click **Transform Data** → review → **Close & Apply**

### Verification
- Switch to **Table View** — confirm all 3 tables loaded
- Check column headers and data types for each table
- Save as `Practice_Session3.pbix`

---

## Session 3 — Key Takeaways

1. **Data types must be correct** — numbers as numbers, dates as dates, IDs as text
2. Power BI connects to **150+ sources** — files, databases, cloud services, web
3. **Import mode** is the default and best for most scenarios
4. Always click **Transform Data** (not Load) to inspect before loading
5. Wrong data types cause broken charts, failed calculations, and incorrect relationships

---

## Preparation for Session 4
- Prepare 2-3 Excel files with similar structure (e.g., monthly sales reports)
- Have at least one CSV file ready
- Keep the files in a single folder for the Folder connector exercise

---

*Session 3 of 30 | Module 1: Business Intelligence Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
