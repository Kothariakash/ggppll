# Session 6 — Data Modeling Concepts
## Module 2: Data Modeling & Relationships | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Demo | Hands-On: Build a Data Model with Sales Dataset

---

## Learning Objectives
By the end of this session, you will be able to:
1. Explain what a data model is and why it matters
2. Differentiate between Fact tables and Dimension tables
3. Understand Primary Keys and Foreign Keys
4. Identify good vs bad data model design
5. Navigate Model View in Power BI Desktop

---

## 6.1 What is a Data Model?

A **data model** is the structure that defines how your tables relate to each other. It's the foundation of every Power BI report.

### Why Data Modeling Matters

| Without a data model | With a proper data model |
|---------------------|------------------------|
| All data in one giant flat table | Organized into related tables |
| Redundant data (same product name repeated 10,000 times) | Product name stored once, referenced by ID |
| Slow performance | Fast, compressed, efficient |
| Complex, error-prone calculations | Clean, reliable DAX measures |
| Hard to maintain when data changes | Easy to extend with new tables |

> **Key Insight:** A poor data model makes everything harder — DAX, visuals, performance, maintenance. A good model makes everything easier.

---

## 6.2 Fact Tables vs Dimension Tables

### Fact Tables (What happened)

| Characteristic | Description |
|---------------|-------------|
| **Contains** | Measurable events / transactions |
| **Columns** | Numeric values (Revenue, Quantity, Cost) + Foreign Keys |
| **Row count** | Large — thousands to millions of rows |
| **Grain** | Each row = one transaction / event |
| **Changes** | New rows added constantly (append) |
| **Also called** | Transaction table, event table |

**Example — Sales Fact Table:**

| OrderID | Date | ProductID | CustomerID | RegionID | Revenue | Quantity | Cost |
|---------|------|-----------|------------|----------|---------|----------|------|
| 1001 | 2024-01-15 | P-101 | C-201 | R-01 | 45000 | 3 | 30000 |
| 1002 | 2024-01-15 | P-205 | C-305 | R-02 | 12000 | 1 | 8000 |
| 1003 | 2024-01-16 | P-101 | C-201 | R-01 | 15000 | 1 | 10000 |

### Dimension Tables (Who, What, Where, When)

| Characteristic | Description |
|---------------|-------------|
| **Contains** | Descriptive attributes / lookup data |
| **Columns** | Text labels, categories, hierarchies |
| **Row count** | Small — dozens to thousands of rows |
| **Grain** | Each row = one unique entity |
| **Changes** | Rarely — updated, not appended |
| **Also called** | Lookup table, reference table, master table |

**Example Dimension Tables:**

**Products:**
| ProductID | Product Name | Category | Sub-Category | Brand |
|-----------|-------------|----------|-------------|-------|
| P-101 | Wireless Mouse | Electronics | Peripherals | Logitech |
| P-205 | Office Chair | Furniture | Seating | Godrej |

**Customers:**
| CustomerID | Customer Name | Segment | City | State |
|------------|--------------|---------|------|-------|
| C-201 | Priya Sharma | Corporate | Mumbai | Maharashtra |
| C-305 | Rahul Verma | SMB | Delhi | Delhi |

**Regions:**
| RegionID | Region | Zone |
|----------|--------|------|
| R-01 | West | Zone A |
| R-02 | North | Zone B |

### Quick Identification Guide

| Ask Yourself | If Yes → | Type |
|-------------|----------|------|
| Does this table contain numbers I want to SUM, AVG, COUNT? | → | **Fact** |
| Does this table describe WHO, WHAT, WHERE, WHEN? | → | **Dimension** |
| Does this table grow daily/weekly with new rows? | → | **Fact** |
| Does this table have a few hundred rows that rarely change? | → | **Dimension** |

---

## 6.3 Keys — The Glue Between Tables

### Primary Key (PK)
- A column (or set of columns) that **uniquely identifies** each row in a table
- Every dimension table must have a Primary Key
- No duplicates, no nulls allowed

**Examples:**
- Products table: `ProductID` (each product has a unique ID)
- Customers table: `CustomerID`
- Date table: `Date` (each date appears only once)

### Foreign Key (FK)
- A column in the Fact table that **references** the Primary Key of a Dimension table
- Can have duplicates (many orders for the same product)
- Creates the link between Fact and Dimension

**Example:**
```
Sales (Fact)                    Products (Dimension)
┌───────────┐                   ┌───────────┐
│ OrderID   │                   │ ProductID │ ← Primary Key (unique)
│ ProductID │───────────────────│ Name      │
│ Revenue   │   Foreign Key     │ Category  │
│ Quantity  │   (references     │ Brand     │
└───────────┘    ProductID)     └───────────┘
```

### Cardinality — How Many Match?

| Cardinality | Meaning | Example |
|------------|---------|---------|
| **One-to-Many (1:*)** | One dimension row → many fact rows | One Product → many Sales rows |
| **One-to-One (1:1)** | One row → one row | Employee → Employee Details |
| **Many-to-Many (*:*)** | Multiple rows on both sides | Students ↔ Courses (avoid in Power BI) |

> **In Power BI:** 95% of relationships are **One-to-Many**. The "One" side is the Dimension, the "Many" side is the Fact.

---

## 6.4 Model View in Power BI

### Navigating Model View
- Click the **Model View** icon (third icon on the left sidebar)
- You'll see all loaded tables as boxes
- Lines between boxes = relationships
- Drag tables to arrange them logically

### What You See in Model View

```
┌─────────────┐          ┌─────────────┐
│  Products   │          │  Customers  │
│─────────────│          │─────────────│
│ ProductID   │──┐       │ CustomerID  │──┐
│ Name        │  │       │ Name        │  │
│ Category    │  │  1:*  │ Segment     │  │  1:*
│ Brand       │  │       │ City        │  │
└─────────────┘  │       └─────────────┘  │
                 │                         │
            ┌────┴─────────────────────────┴────┐
            │            Sales (Fact)            │
            │───────────────────────────────────│
            │ OrderID | Date | ProductID         │
            │ CustomerID | Revenue | Quantity    │
            └───────────────────────────────────┘
```

### Model View Actions

| Action | How |
|--------|-----|
| **Create relationship** | Drag a column from one table to another |
| **Edit relationship** | Double-click the line between tables |
| **Delete relationship** | Right-click the line → Delete |
| **Hide column** | Right-click column → Hide in Report View |
| **Rearrange tables** | Drag table boxes to organize layout |

---

## 6.5 Good vs Bad Data Model Design

### Bad: The Flat Table (Everything in One Table)

| OrderID | Date | Product | Category | Customer | City | Region | Revenue | Qty |
|---------|------|---------|----------|----------|------|--------|---------|-----|
| 1001 | 2024-01-15 | Mouse | Electronics | Priya | Mumbai | West | 45000 | 3 |
| 1002 | 2024-01-15 | Chair | Furniture | Rahul | Delhi | North | 12000 | 1 |
| 1003 | 2024-01-16 | Mouse | Electronics | Priya | Mumbai | West | 15000 | 1 |

**Problems:**
- "Mouse", "Electronics", "Priya", "Mumbai", "West" repeated thousands of times
- File size bloated with redundant text
- Changing a product name requires updating every row
- No clean separation of facts and dimensions

### Good: Normalized Star Schema

```
                    ┌──────────┐
                    │   Date   │
                    └────┬─────┘
                         │
┌──────────┐      ┌──────┴──────┐      ┌──────────┐
│ Products │──────│    Sales    │──────│ Customers│
└──────────┘      │   (Fact)    │      └──────────┘
                  └──────┬──────┘
                         │
                    ┌────┴─────┐
                    │ Regions  │
                    └──────────┘
```

**Benefits:**
- Each piece of information stored **once**
- Small file size, fast performance
- Easy to extend (add a new dimension without touching Sales)
- Clean DAX calculations

---

## 6.6 Data Model Best Practices

1. **Separate Facts from Dimensions** — don't put everything in one table
2. **Every Dimension needs a unique key column** — no duplicates
3. **Hide Foreign Key columns** from Report View — users shouldn't see IDs
4. **Use descriptive table names** — "Products" not "Table1"
5. **Create a Date table** — essential for time intelligence (Session 19)
6. **Avoid Many-to-Many relationships** where possible
7. **Keep it simple** — the fewer tables, the better (but not at the cost of a flat table)
8. **No circular relationships** — Power BI doesn't allow them (table A → B → C → A)

---

## 🔧 Hands-On Activity: Build Your First Data Model

**Duration:** 20 minutes

### Setup
Import these tables (from Excel or Enter Data):
- **Sales** (Fact): OrderID, OrderDate, ProductID, CustomerID, Revenue, Quantity
- **Products** (Dimension): ProductID, ProductName, Category, SubCategory
- **Customers** (Dimension): CustomerID, CustomerName, Segment, City, State

### Tasks
1. Import all 3 tables into Power BI
2. Switch to **Model View**
3. Verify: Did Power BI auto-detect any relationships?
4. If not: drag `ProductID` from Sales to `ProductID` in Products
5. Drag `CustomerID` from Sales to `CustomerID` in Customers
6. Verify cardinality: both should be **1:Many** (Dimension:Fact)
7. Arrange tables: Fact in center, Dimensions around it
8. **Hide** the ID columns (ProductID, CustomerID) in Report View
9. Switch to Report View → create a simple bar chart: Product Category vs Sum of Revenue
10. Save as `Practice_Session6.pbix`

---

## Session 6 — Key Takeaways

1. A **data model** defines how tables relate — it's the foundation of every report
2. **Fact tables** contain measurable events (Revenue, Quantity); **Dimension tables** describe context (Product, Customer, Date)
3. **Primary Keys** uniquely identify rows in dimensions; **Foreign Keys** in facts reference them
4. Most relationships are **One-to-Many** (Dimension → Fact)
5. A well-designed model = fast performance, reliable calculations, easy maintenance

---

## Preparation for Session 7
- Keep `Practice_Session6.pbix` open
- Think about: What happens if two tables don't have a common column?
- Review: What is cardinality? What is cross-filter direction?

---

*Session 6 of 30 | Module 2: Data Modeling & Relationships*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
