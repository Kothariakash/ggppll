# Session 7 — Relationships in Power BI
## Module 2: Data Modeling & Relationships | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Create and Configure Relationships

---

## Learning Objectives
By the end of this session, you will be able to:
1. Create, edit, and delete relationships between tables
2. Understand cardinality types (1:1, 1:Many, Many:Many)
3. Configure cross-filter direction (Single vs Both)
4. Troubleshoot common relationship issues
5. Use the Manage Relationships dialog effectively

---

## 7.1 What Are Relationships?

A **relationship** is a connection between two tables based on a shared column. Relationships allow Power BI to:
- Combine data from multiple tables in a single visual
- Propagate filters from one table to another
- Enable DAX calculations that span tables

### How Filters Flow

```
User clicks "Electronics" in a slicer
        │
        ▼
Products table filtered → only Electronics rows
        │
        ▼ (relationship propagates the filter)
Sales table filtered → only rows with Electronics ProductIDs
        │
        ▼
Visual shows: Revenue for Electronics only
```

> **Key Concept:** Filters flow **from Dimension to Fact** — from the "One" side to the "Many" side.

---

## 7.2 Creating Relationships

### Method 1: Auto-Detect
- Power BI tries to detect relationships automatically when you load data
- Based on matching column names and data types
- Check Model View after loading — auto-detected relationships appear as lines
- **Always verify** — auto-detect can be wrong

### Method 2: Drag and Drop (Model View)
1. Open **Model View**
2. Drag a column from Table A → drop on matching column in Table B
3. Relationship line appears

### Method 3: Manage Relationships Dialog
1. **Modeling** tab → **Manage Relationships**
2. Click **New**
3. Select Table 1 and its key column
4. Select Table 2 and its key column
5. Configure: Cardinality, Cross-filter direction
6. Click **OK**

### Method 4: Auto-detect Prompt
- When loading new tables, Power BI may prompt: "Do you want to detect relationships?"
- Click Yes for auto-detection, then verify in Model View

---

## 7.3 Cardinality Types

### One-to-Many (1:*) — Most Common

```
Products (1 side)              Sales (* side)
┌─────────────┐                ┌─────────────┐
│ ProductID   │─── 1 : * ────│ ProductID   │
│ (unique)    │                │ (repeats)   │
└─────────────┘                └─────────────┘

Each product appears ONCE        Each product appears MANY times
in Products table                in Sales table
```

- **Use when:** One dimension record matches multiple fact records
- **Example:** One customer → many orders; One product → many sales
- **This is 95% of your relationships**

### One-to-One (1:1)

```
Employees                      Employee Details
┌─────────────┐                ┌─────────────┐
│ EmployeeID  │─── 1 : 1 ────│ EmployeeID  │
│ (unique)    │                │ (unique)    │
└─────────────┘                └─────────────┘
```

- **Use when:** Both tables have unique values in the key column
- **Example:** Employee master → Employee contact details (split for security)
- **Rare** — often indicates the tables should be merged

### Many-to-Many (*:*)

```
Students                       Courses
┌─────────────┐                ┌─────────────┐
│ StudentID   │─── * : * ────│ CourseID    │
│ (repeats)   │                │ (repeats)   │
└─────────────┘                └─────────────┘

One student takes MANY courses
One course has MANY students
```

- **Use when:** Both sides have duplicate values
- **Caution:** Can produce unexpected results — use carefully
- **Better approach:** Use a bridge table (junction table) to convert to two 1:Many relationships

### Cardinality Decision Guide

| Scenario | Cardinality |
|----------|------------|
| Products → Sales | 1:Many |
| Customers → Orders | 1:Many |
| Date → Sales | 1:Many |
| Employee → Employee_Details | 1:One |
| Products → Sales (with multiple product tables) | Many:Many (avoid if possible) |

---

## 7.4 Cross-Filter Direction

### Single Direction (Default — Recommended)

```
Products ────filter────► Sales
(1 side)                 (* side)

Filter flows ONE WAY: from Dimension to Fact
```

- Slicer on Product Category → filters Sales table ✅
- Slicer on Revenue range → does NOT filter Products table ❌
- **This is the correct default for Star Schema**

### Both Directions (Bidirectional)

```
Products ◄───filter───► Sales
(1 side)                 (* side)

Filter flows BOTH WAYS
```

- Slicer on Product Category → filters Sales ✅
- Filter on Sales → also filters Products ✅
- **Use Case:** When you need a visual to show "only products that have sales"
- **Caution:** Can cause ambiguous filter paths and performance issues

### When to Use Bidirectional

| Scenario | Direction |
|----------|-----------|
| Standard reporting (most cases) | **Single** |
| "Show only products that were sold" | **Both** |
| Many-to-Many via bridge table | **Both** (on the bridge) |
| Slicer on Fact filtering Dimension | **Both** |

> **Best Practice:** Start with **Single** direction. Only switch to Both when you have a specific need and understand the implications.

---

## 7.5 Active vs Inactive Relationships

### The Rule
- Power BI allows **only ONE active relationship** between any two tables
- Additional relationships between the same tables are **inactive** (shown as dashed lines)

### Why Multiple Relationships?

**Example:** Sales table has two date columns:
- `OrderDate` — when the order was placed
- `ShipDate` — when the order was shipped

Both reference the Date table, but only one can be **active**.

```
Date Table
    │
    ├── Active ──── Sales[OrderDate]     (solid line)
    │
    └── Inactive ── Sales[ShipDate]      (dashed line)
```

### Using Inactive Relationships
- The active relationship works automatically in visuals
- To use the inactive relationship, use the `USERELATIONSHIP` DAX function:

```dax
ShippedRevenue = CALCULATE(
    SUM(Sales[Revenue]),
    USERELATIONSHIP(Sales[ShipDate], 'Date'[Date])
)
```

---

## 7.6 Manage Relationships Dialog

### Opening
- **Modeling** tab → **Manage Relationships**

### Dialog Contents

| Column | Meaning |
|--------|---------|
| **Active** | Checkbox — is this relationship active? |
| **From Table** | The table on the Many (*) side |
| **From Column** | The foreign key column |
| **To Table** | The table on the One (1) side |
| **To Column** | The primary key column |
| **Cardinality** | 1:1, 1:Many, Many:1, Many:Many |
| **Cross Filter** | Single or Both |

### Editing a Relationship
1. Double-click a relationship line in Model View
   - OR select it in Manage Relationships → Edit
2. Modify cardinality or cross-filter direction
3. Click OK

---

## 7.7 Troubleshooting Relationships

### Problem 1: "A relationship cannot be created"
**Cause:** Data type mismatch between the two columns
**Fix:** Ensure both columns have the same data type in Power Query (both Text, or both Whole Number)

### Problem 2: Duplicate values on the "One" side
**Cause:** The dimension table has duplicate values in the key column
```
Products table:
ProductID = P-101  ← 
ProductID = P-101  ← Duplicate! Cannot be the "1" side
```
**Fix:** Remove duplicates in Power Query (Home → Remove Rows → Remove Duplicates)

### Problem 3: Ambiguous relationships
**Cause:** Multiple active paths between two tables
**Fix:** Deactivate one relationship, use `USERELATIONSHIP` in DAX

### Problem 4: Blank/null values in key columns
**Cause:** Some rows have no matching key
**Result:** Those rows won't match — they appear as "(Blank)" in visuals
**Fix:** Clean nulls in Power Query, or accept blanks and handle in visuals

### Problem 5: Many-to-Many unexpected results
**Cause:** Both sides have duplicates, DAX calculations may double-count
**Fix:** Introduce a bridge table, or use `CROSSFILTER` / `TREATAS` DAX functions

### Problem 6: Auto-detected relationship is wrong
**Cause:** Power BI matched columns by name but they aren't actually related
**Fix:** Delete the auto-detected relationship in Manage Relationships, create the correct one manually

---

## 7.8 Relationship Validation Checklist

Before building visuals, verify your relationships:

- [ ] Every Dimension table has a **unique key column** (no duplicates)
- [ ] Every relationship is **1:Many** (Dimension → Fact)
- [ ] Cross-filter direction is **Single** (unless you have a specific reason for Both)
- [ ] No **circular relationships** (A → B → C → A)
- [ ] Key columns have **matching data types** on both sides
- [ ] No **blank/null values** in key columns (or they're handled)
- [ ] Auto-detected relationships have been **verified** manually

---

## 🔧 Hands-On Activity: Relationship Building

**Duration:** 25 minutes

### Setup
Use the model from Session 6 with tables: Sales, Products, Customers.
Add a new table — **Regions** (RegionID, RegionName, Zone).

### Tasks

1. Open **Model View** — examine auto-detected relationships
2. If no relationships exist, create them:
   - Sales[ProductID] → Products[ProductID] (1:Many)
   - Sales[CustomerID] → Customers[CustomerID] (1:Many)
   - Sales[RegionID] → Regions[RegionID] (1:Many)
3. Verify each: **cardinality = 1:Many**, **cross-filter = Single**
4. Open **Manage Relationships** — review all connections
5. Test: Switch to Report View → create a stacked bar chart:
   - Axis: Product Category (from Products table)
   - Values: Sum of Revenue (from Sales table)
   - Legend: Region Name (from Regions table)
   - **If this works, your relationships are correct!**
6. Test cross-filtering: Add a slicer for Customer Segment → verify chart updates
7. **Hide** all ID columns (ProductID, CustomerID, RegionID) from Report View
8. Save

### Verification Questions
- Does filtering by Product Category correctly filter Revenue?
- Does the Region slicer update the Product chart?
- Are there any "(Blank)" values in your visuals? If so, why?

---

## Session 7 — Key Takeaways

1. **Relationships** connect tables and enable filters to flow between them
2. **1:Many** is the standard — Dimension (1) to Fact (Many)
3. Filters flow from **Dimension → Fact** (Single direction, default)
4. Use **Both** direction only when needed — keep Single as default
5. Only **one active relationship** between any two tables — use `USERELATIONSHIP` for extras
6. **Always verify** auto-detected relationships — they can be wrong

---

## Preparation for Session 8
- Research: What is a Star Schema? What is a Snowflake Schema?
- Think about: What would a Date table look like? (Date, Year, Month, Quarter, Day of Week)

---

*Session 7 of 30 | Module 2: Data Modeling & Relationships*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
