# Session 8 — Star Schema Design
## Module 2: Data Modeling & Relationships | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Design and Build a Star Schema

---

## Learning Objectives
By the end of this session, you will be able to:
1. Explain the Star Schema and why it's the gold standard for Power BI
2. Differentiate Star Schema from Snowflake Schema and Flat Tables
3. Design a Star Schema from raw business data
4. Create a dedicated Date table
5. Implement a Star Schema in Power BI Model View

---

## 8.1 What is a Star Schema?

A **Star Schema** is a data model design where:
- One central **Fact table** (transactions/events) is surrounded by
- Multiple **Dimension tables** (descriptive lookups)
- Connected via one-to-many relationships

It's called "Star" because the diagram looks like a star:

```
                    ┌──────────┐
                    │   Date   │
                    │ Dimension│
                    └────┬─────┘
                         │ 1:*
    ┌──────────┐   ┌─────┴──────┐   ┌──────────┐
    │ Product  │───│            │───│ Customer │
    │Dimension │1:*│   SALES    │*:1│Dimension │
    └──────────┘   │   (Fact)   │   └──────────┘
                   └─────┬──────┘
                         │ 1:*
                    ┌────┴─────┐
                    │  Region  │
                    │Dimension │
                    └──────────┘
```

### Why Star Schema is the Gold Standard for Power BI

| Benefit | Explanation |
|---------|------------|
| **Performance** | VertiPaq engine is optimized for Star Schema — fastest compression and queries |
| **Simplicity** | Easy to understand — even non-technical users can navigate |
| **DAX compatibility** | DAX functions (CALCULATE, FILTER, ALL) work best with Star Schema |
| **Filter propagation** | Clean, predictable filter flow from dimensions to facts |
| **Scalability** | Easy to add new dimensions without restructuring |
| **Industry standard** | Used in every major BI platform — transferable knowledge |

---

## 8.2 Star Schema vs Other Designs

### Flat Table (One Big Table)

```
┌─────────────────────────────────────────────────────┐
│ OrderID | Date | Product | Category | Customer |    │
│ City | Region | Revenue | Quantity | Cost           │
│ (ALL data in ONE table — thousands of repeated      │
│  text values like "Electronics", "Mumbai", etc.)    │
└─────────────────────────────────────────────────────┘
```

| Factor | Flat Table | Star Schema |
|--------|-----------|-------------|
| **File size** | Large (redundant text) | Small (text stored once) |
| **Performance** | Slow | Fast |
| **Maintenance** | Hard (change product name in 10,000 rows) | Easy (change in 1 row) |
| **DAX** | Works but limited | Full power |
| **Scalability** | Difficult | Easy |

### Snowflake Schema (Normalized Dimensions)

```
                    ┌──────────┐
                    │   Date   │
                    └────┬─────┘
                         │
┌────────┐ ┌────────┐ ┌──┴───┐ ┌──────────┐
│Category│─│Product │─│SALES │─│ Customer │
└────────┘ └────────┘ └──┬───┘ └────┬─────┘
                         │          │
                    ┌────┴───┐ ┌────┴─────┐
                    │ Region │ │   City   │
                    └────────┘ └──────────┘
```

- Dimensions are further **normalized** into sub-tables (Category → Product → Sales)
- More tables, more joins, more complex
- **Not recommended for Power BI** — Star Schema performs better

| Factor | Star Schema | Snowflake Schema |
|--------|------------|-----------------|
| **Tables** | Fewer | More |
| **Complexity** | Simple | Complex |
| **Performance** | Faster in Power BI | Slower (more joins) |
| **Storage** | Slightly more | Slightly less |
| **Recommended?** | **Yes — for Power BI** | No — use in data warehouses only |

> **Power BI Best Practice:** Always **flatten (denormalize) your dimensions** into a Star Schema. If your source is a Snowflake, merge the dimension sub-tables in Power Query before loading.

---

## 8.3 Designing a Star Schema

### Step-by-Step Process

```
Step 1: Identify the BUSINESS PROCESS (what are you analyzing?)
           → Example: "Retail Sales Performance"

Step 2: Identify the GRAIN (what does one row of the fact table represent?)
           → Example: "One line item on a sales order"

Step 3: Identify the DIMENSIONS (who, what, where, when?)
           → Date, Product, Customer, Store, Region

Step 4: Identify the FACTS/MEASURES (what numbers do you want to analyze?)
           → Revenue, Quantity, Cost, Discount

Step 5: Identify the KEYS (how do tables connect?)
           → ProductID, CustomerID, StoreID, DateKey
```

### Design Template

| Design Element | Question to Ask | Answer |
|---------------|----------------|--------|
| **Business Process** | What am I analyzing? | Sales performance |
| **Grain** | What is one row? | One order line item |
| **Fact Table** | What numbers to measure? | Revenue, Qty, Cost, Discount |
| **Dimension: Date** | When did it happen? | Order Date, Ship Date |
| **Dimension: Product** | What was sold? | Product, Category, Brand |
| **Dimension: Customer** | Who bought it? | Name, Segment, City |
| **Dimension: Store/Region** | Where was it sold? | Store, Region, Zone |
| **Dimension: Salesperson** | Who sold it? | Rep, Team, Manager |

---

## 8.4 The Date Table — Most Important Dimension

### Why You Need a Dedicated Date Table

1. **Time Intelligence DAX** functions (YTD, QTD, MoM, YoY) **require** a Date table
2. A proper Date table has **one row per day** — no gaps
3. Contains pre-built columns for Year, Quarter, Month, Week, Day of Week
4. Provides consistent date hierarchies for drill-down

### Date Table Structure

| Column | Type | Example | Purpose |
|--------|------|---------|---------|
| **Date** | Date | 2024-01-15 | Primary Key (unique, no gaps) |
| **Year** | Whole Number | 2024 | Year grouping |
| **Quarter** | Text | Q1 | Quarter grouping |
| **QuarterNumber** | Whole Number | 1 | Sorting quarters correctly |
| **Month** | Text | January | Month name |
| **MonthNumber** | Whole Number | 1 | Sorting months correctly |
| **MonthYear** | Text | Jan 2024 | Axis labels |
| **WeekNumber** | Whole Number | 3 | ISO week |
| **DayOfWeek** | Text | Monday | Day name |
| **DayOfWeekNumber** | Whole Number | 1 | Sorting days correctly |
| **IsWeekend** | True/False | FALSE | Weekend filter |
| **FiscalYear** | Whole Number | FY2024 | If fiscal year differs from calendar |
| **FiscalQuarter** | Text | FQ3 | Fiscal quarter |

### Creating a Date Table in Power BI

**Method 1: DAX (Recommended)**
```dax
DateTable = 
ADDCOLUMNS(
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Quarter", "Q" & QUARTER([Date]),
    "QuarterNumber", QUARTER([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "MonthNumber", MONTH([Date]),
    "MonthYear", FORMAT([Date], "MMM YYYY"),
    "WeekNumber", WEEKNUM([Date]),
    "DayOfWeek", FORMAT([Date], "DDDD"),
    "DayOfWeekNumber", WEEKDAY([Date], 2),
    "IsWeekend", IF(WEEKDAY([Date], 2) >= 6, TRUE(), FALSE())
)
```

**Method 2: Power Query (M Language)**
- Use `List.Dates` to generate a date range
- Add columns for Year, Month, etc. using date functions

**Method 3: Excel**
- Create a date table in Excel → import into Power BI

> **After creating:** Mark as Date Table → Modeling tab → **Mark as Date Table** → Select the Date column. This enables Time Intelligence DAX functions.

---

## 8.5 Star Schema Design Examples

### Example 1: E-Commerce Analytics

```
                      ┌───────────────┐
                      │  Date Table   │
                      │───────────────│
                      │ Date (PK)     │
                      │ Year, Quarter │
                      │ Month, Day    │
                      └───────┬───────┘
                              │ 1:*
┌───────────────┐   ┌────────┴────────┐   ┌───────────────┐
│   Products    │   │                 │   │   Customers   │
│───────────────│   │   Orders        │   │───────────────│
│ ProductID(PK) │1:*│   (Fact)        │*:1│ CustomerID(PK)│
│ Name          │───│─────────────────│───│ Name          │
│ Category      │   │ OrderID         │   │ Segment       │
│ SubCategory   │   │ OrderDate (FK)  │   │ City, State   │
│ Brand         │   │ ProductID (FK)  │   └───────────────┘
│ ListPrice     │   │ CustomerID (FK) │
└───────────────┘   │ Revenue         │   ┌───────────────┐
                    │ Quantity        │   │   Shipping    │
                    │ Discount        │*:1│───────────────│
                    │ ShipMode (FK)   │───│ ShipMode (PK) │
                    │ Cost            │   │ Carrier       │
                    └─────────────────┘   │ SLA_Days      │
                                          └───────────────┘
```

### Example 2: HR Analytics

```
                      ┌───────────────┐
                      │  Date Table   │
                      └───────┬───────┘
                              │
┌───────────────┐   ┌────────┴────────┐   ┌───────────────┐
│  Departments  │   │                 │   │   Locations   │
│───────────────│   │  Employees      │   │───────────────│
│ DeptID (PK)   │1:*│  (Fact)         │*:1│ LocationID(PK)│
│ DeptName      │───│─────────────────│───│ City          │
│ CostCenter    │   │ EmployeeID      │   │ State         │
└───────────────┘   │ HireDate (FK)   │   │ Country       │
                    │ DeptID (FK)     │   └───────────────┘
                    │ LocationID (FK) │
                    │ Salary          │   ┌───────────────┐
                    │ PerformanceScore│   │   JobTitles   │
                    │ JobTitleID (FK) │*:1│───────────────│
                    │ AttritionFlag   │───│ JobTitleID(PK)│
                    └─────────────────┘   │ Title, Level  │
                                          │ PayGrade      │
                                          └───────────────┘
```

---

## 8.6 Common Star Schema Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Fact table has descriptive text columns | Bloated file, poor performance | Move text to dimensions, keep only IDs in fact |
| No Date table | Time Intelligence DAX won't work | Create a dedicated Date dimension |
| Snowflaked dimensions | Too many joins, complex model | Flatten/merge in Power Query |
| Multiple fact tables with no shared dimensions | Can't compare across facts | Create conformed dimensions (shared Date, Product) |
| Calculated columns in fact table | Slows refresh, bloats model | Use DAX Measures instead (Session 17) |
| Dimension has duplicate keys | Relationship fails (1:Many broken) | Remove duplicates in Power Query |

---

## 🔧 Hands-On Activity: Build a Complete Star Schema

**Duration:** 25 minutes

### Scenario
You have a raw sales dataset. Restructure it into a proper Star Schema.

### Starting Data (Flat Table — simulate with Enter Data or Excel)
| OrderID | OrderDate | ProductName | Category | CustomerName | City | Region | Revenue | Qty |
|---------|-----------|-------------|----------|-------------|------|--------|---------|-----|
| 1001 | 2024-01-15 | Laptop | Electronics | Priya | Mumbai | West | 65000 | 1 |
| 1002 | 2024-01-16 | Desk Chair | Furniture | Rahul | Delhi | North | 12000 | 2 |

### Tasks

1. **Create Dimension tables** in Power Query (or Enter Data):
   - **Products:** ProductID, ProductName, Category
   - **Customers:** CustomerID, CustomerName, City, Region
   - **Date Table:** Use DAX `CALENDARAUTO()` with Year, Month, Quarter columns
2. **Create Fact table:** Keep only OrderID, OrderDate, ProductID, CustomerID, Revenue, Qty
3. **Create relationships** in Model View:
   - Date[Date] → Sales[OrderDate] (1:Many)
   - Products[ProductID] → Sales[ProductID] (1:Many)
   - Customers[CustomerID] → Sales[CustomerID] (1:Many)
4. **Mark the Date table** as Date Table (Modeling → Mark as Date Table)
5. **Hide** all ID/FK columns from Report View
6. **Arrange** tables in star layout: Fact in center, Dimensions around
7. **Test:** Create a Matrix visual — Rows: Category, Columns: Quarter, Values: Sum of Revenue
8. Save as `Practice_Session8_StarSchema.pbix`

---

## Session 8 — Key Takeaways

1. **Star Schema** = one Fact table surrounded by Dimension tables — the gold standard for Power BI
2. **Always denormalize** dimensions — flatten Snowflake into Star in Power Query
3. **Date Table is mandatory** — create with `CALENDARAUTO()` DAX, mark as Date Table
4. Design process: Business Process → Grain → Dimensions → Facts → Keys
5. Keep **text in dimensions, numbers in facts** — never descriptive columns in the fact table

---

## Preparation for Session 9
- Review Power Query operations from Session 5
- Think about: What advanced transformations might your data need? (Pivot, Unpivot, Merge, Append)

---

*Session 8 of 30 | Module 2: Data Modeling & Relationships*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
