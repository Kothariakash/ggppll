# Session 20 — Business Metrics & KPI Reports
## Module 4: DAX Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Create KPI Reports with Profit Analysis & Sales Performance

---

## Learning Objectives
By the end of this session, you will be able to:
1. Define and build key business KPIs using DAX
2. Create Profit & Loss summary measures
3. Build sales performance scorecards with targets
4. Use conditional logic in measures for status indicators
5. Design a complete KPI report page

---

## 20.1 Common Business KPIs

### Sales KPIs

| KPI | DAX Formula | Format |
|-----|-------------|--------|
| **Total Revenue** | `SUM(Sales[Revenue])` | Currency |
| **Total Orders** | `COUNTROWS(Sales)` | Whole Number |
| **Average Order Value (AOV)** | `DIVIDE([Total Revenue], [Total Orders], 0)` | Currency |
| **Revenue per Customer** | `DIVIDE([Total Revenue], [# Customers], 0)` | Currency |
| **Basket Size** | `DIVIDE(SUM(Sales[Quantity]), [Total Orders], 0)` | Decimal |
| **Conversion Rate** | `DIVIDE([Total Orders], [Total Visits], 0)` | Percentage |

### Profitability KPIs

| KPI | DAX Formula | Format |
|-----|-------------|--------|
| **Gross Profit** | `[Total Revenue] - [Total COGS]` | Currency |
| **Gross Margin %** | `DIVIDE([Gross Profit], [Total Revenue], 0)` | Percentage |
| **Net Profit** | `[Gross Profit] - [Total Expenses]` | Currency |
| **Net Margin %** | `DIVIDE([Net Profit], [Total Revenue], 0)` | Percentage |
| **Markup %** | `DIVIDE([Gross Profit], [Total COGS], 0)` | Percentage |

### Customer KPIs

| KPI | DAX Formula | Format |
|-----|-------------|--------|
| **# Customers** | `DISTINCTCOUNT(Sales[CustomerID])` | Whole Number |
| **New Customers** | See Section 20.3 | Whole Number |
| **Repeat Rate** | See Section 20.3 | Percentage |
| **Customer Lifetime Value** | `DIVIDE([Total Revenue], [# Customers], 0)` | Currency |

### Growth KPIs

| KPI | DAX Formula | Format |
|-----|-------------|--------|
| **Revenue YoY %** | `DIVIDE([Total Revenue] - [Revenue LY], [Revenue LY], 0)` | Percentage |
| **Revenue MoM %** | `DIVIDE([Total Revenue] - [Revenue Prev Month], [Revenue Prev Month], 0)` | Percentage |
| **Revenue YTD** | `TOTALYTD(SUM(Sales[Revenue]), DateTable[Date])` | Currency |
| **YTD Growth %** | `DIVIDE([Revenue YTD] - [Revenue YTD LY], [Revenue YTD LY], 0)` | Percentage |

---

## 20.2 Profit Analysis Measures

### Building a P&L Summary

```dax
// Revenue
Total Revenue = SUM(Sales[Revenue])

// Cost of Goods Sold
Total COGS = SUM(Sales[Cost])

// Gross Profit
Gross Profit = [Total Revenue] - [Total COGS]

// Gross Margin %
Gross Margin % = DIVIDE([Gross Profit], [Total Revenue], 0)

// Operating Expenses (if separate table)
Total OpEx = SUM(Expenses[Amount])

// Operating Profit (EBIT)
Operating Profit = [Gross Profit] - [Total OpEx]

// Operating Margin %
Operating Margin % = DIVIDE([Operating Profit], [Total Revenue], 0)
```

### Profit by Category

```dax
// Category-level profit contribution
Category Profit Share = 
DIVIDE(
    [Gross Profit],
    CALCULATE([Gross Profit], ALL(Products[Category])),
    0
)
```

### Profit vs Previous Year

```dax
Gross Profit LY = 
CALCULATE([Gross Profit], SAMEPERIODLASTYEAR(DateTable[Date]))

Profit YoY Change = [Gross Profit] - [Gross Profit LY]

Profit YoY % = DIVIDE([Profit YoY Change], [Gross Profit LY], 0)
```

---

## 20.3 Customer Analysis Measures

### New vs Returning Customers

```dax
// First purchase date for each customer
Customer First Purchase = 
CALCULATE(
    MIN(Sales[OrderDate]),
    ALLEXCEPT(Sales, Sales[CustomerID])
)
```

**Note:** This is best as a calculated column in the Sales table or a separate customer summary table.

### New Customer Count (Measure approach)

```dax
New Customers = 
COUNTROWS(
    FILTER(
        VALUES(Sales[CustomerID]),
        CALCULATE(MIN(Sales[OrderDate])) = 
        CALCULATE(MIN(Sales[OrderDate]), ALL(DateTable))
    )
)
```

### Simpler approach — New Customers using DATESINPERIOD

```dax
// Customers whose first order is in the current period
New Customers This Period = 
VAR CurrentPeriodStart = MIN(DateTable[Date])
VAR CurrentPeriodEnd = MAX(DateTable[Date])
RETURN
COUNTROWS(
    FILTER(
        ALL(Sales[CustomerID]),
        VAR FirstOrder = CALCULATE(MIN(Sales[OrderDate]), ALL(DateTable))
        RETURN FirstOrder >= CurrentPeriodStart && FirstOrder <= CurrentPeriodEnd
    )
)
```

---

## 20.4 Target Comparison Measures

### Setup: Targets Table

Create or import a Targets table:

| Month | Region | Revenue Target | Order Target |
|-------|--------|---------------|-------------|
| 2024-01-01 | North | 500000 | 150 |
| 2024-01-01 | South | 450000 | 130 |
| 2024-02-01 | North | 520000 | 160 |

### Target Measures

```dax
Revenue Target = SUM(Targets[Revenue Target])

// Variance (Actual - Target)
Revenue Variance = [Total Revenue] - [Revenue Target]

// Achievement %
Achievement % = DIVIDE([Total Revenue], [Revenue Target], 0)

// Variance % 
Variance % = DIVIDE([Revenue Variance], [Revenue Target], 0)
```

### Status Indicator

```dax
Performance Status = 
VAR Achievement = [Achievement %]
RETURN
SWITCH(
    TRUE(),
    Achievement >= 1, "Above Target",
    Achievement >= 0.9, "Near Target",
    Achievement >= 0.75, "Below Target",
    "Critical"
)
```

### Status with Symbols (for conditional formatting)

```dax
Status Icon = 
VAR Achievement = [Achievement %]
RETURN
SWITCH(
    TRUE(),
    Achievement >= 1, "●",       // Green dot
    Achievement >= 0.9, "●",     // Yellow dot  
    "●"                          // Red dot
)
```

> Use **Conditional Formatting** (Session 22) to color these dynamically.

---

## 20.5 VAR — Variables in DAX

### Why Use Variables?

| Without VAR | With VAR |
|-------------|----------|
| Same sub-expression repeated multiple times | Calculate once, reference many times |
| Hard to read and debug | Clear, readable, maintainable |
| Slower (engine may re-evaluate) | Faster (computed once) |

### Syntax

```dax
Measure = 
VAR VariableName = expression
VAR AnotherVar = expression
RETURN
    result_using_variables
```

### Example: Profit Margin with VAR

```dax
Profit Margin % = 
VAR Revenue = SUM(Sales[Revenue])
VAR Cost = SUM(Sales[Cost])
VAR Profit = Revenue - Cost
RETURN
    DIVIDE(Profit, Revenue, 0)
```

### Example: YoY with Status

```dax
YoY Status = 
VAR CurrentRev = [Total Revenue]
VAR PrevRev = [Revenue LY]
VAR Change = CurrentRev - PrevRev
VAR ChangePct = DIVIDE(Change, PrevRev, 0)
RETURN
    IF(
        ISBLANK(PrevRev), 
        "No Prior Data",
        IF(ChangePct > 0.1, "Strong Growth",
            IF(ChangePct > 0, "Growth",
                IF(ChangePct > -0.1, "Decline", "Sharp Decline")
            )
        )
    )
```

---

## 20.6 Sales Performance Scorecard Design

### Scorecard Layout

```
┌──────────────────────────────────────────────────────────────────┐
│  Sales Performance Scorecard — Q1 FY2024                        │
├──────────┬──────────┬──────────┬──────────┬──────────┬──────────┤
│          │ Actual   │ Target   │ Variance │ Achv %   │ Status   │
├──────────┼──────────┼──────────┼──────────┼──────────┼──────────┤
│ Revenue  │ ₹42.3 Cr │ ₹40 Cr  │ +₹2.3 Cr │ 106%     │ ● Above  │
│ Orders   │ 12,500   │ 12,000  │ +500     │ 104%     │ ● Above  │
│ AOV      │ ₹3,384   │ ₹3,500  │ -₹116    │ 97%      │ ● Near   │
│ Margin   │ 18.5%    │ 20%     │ -1.5%    │ 92.5%    │ ● Below  │
│ Cust     │ 4,200    │ 4,000   │ +200     │ 105%     │ ● Above  │
└──────────┴──────────┴──────────┴──────────┴──────────┴──────────┘
```

### Building This in Power BI

**Option 1: Matrix Visual**
- Rows: KPI Name (from a KPI mapping table)
- Values: Actual, Target, Variance, Achievement %, Status

**Option 2: Table Visual with Measures**
- Create a KPI Mapping table (Enter Data): KPIName, SortOrder
- Create SWITCH-based measures that return different values per KPI

**Option 3: Multiple Card Groups**
- Group of cards for each KPI: Actual card + Target card + Variance card
- Use conditional formatting for status colors

---

## 20.7 Dynamic Measures with SWITCH

### Dynamic Metric Selector

Allow users to switch between metrics using a slicer:

**Step 1:** Create a disconnected Metric table (Enter Data):
| MetricName |
|------------|
| Revenue |
| Profit |
| Orders |
| Margin % |

**Step 2:** Create the dynamic measure:

```dax
Selected Metric = 
VAR SelectedName = SELECTEDVALUE(MetricSelector[MetricName], "Revenue")
RETURN
SWITCH(
    SelectedName,
    "Revenue", [Total Revenue],
    "Profit", [Gross Profit],
    "Orders", [Total Orders],
    "Margin %", [Gross Margin %],
    [Total Revenue]
)
```

**Step 3:** Add a Slicer for MetricSelector[MetricName] and use [Selected Metric] as the value in charts.

> **Note:** This is a **disconnected table** — it has no relationship to any other table. It only drives the SWITCH logic.

---

## 20.8 Measure Documentation

### Best Practice: Document Your Measures

```dax
// ================================================================
// Measure: Gross Margin %
// Purpose: Shows gross profit as a percentage of revenue
// Formula: (Revenue - COGS) / Revenue
// Owner: BI Team
// Last Updated: 2024-03-15
// Dependencies: Total Revenue, Total COGS
// ================================================================
Gross Margin % = 
VAR Revenue = [Total Revenue]
VAR COGS = [Total COGS]
RETURN DIVIDE(Revenue - COGS, Revenue, 0)
```

### Measure Description

1. Select a measure in the Fields pane
2. **Properties** pane → **Description** field
3. Type a description — it appears as a tooltip when users hover over the measure

---

## 🔧 Hands-On Activity: KPI Report with Profit Analysis

**Duration:** 25 minutes

### Tasks

**Part 1 — Create Business Measures (10 min)**

1. **Profitability:**
   ```dax
   Total COGS = SUM(Sales[Cost])
   Gross Profit = [Total Revenue] - [Total COGS]
   Gross Margin % = DIVIDE([Gross Profit], [Total Revenue], 0)
   ```

2. **Growth:**
   ```dax
   Revenue LY = CALCULATE(SUM(Sales[Revenue]), SAMEPERIODLASTYEAR(DateTable[Date]))
   Revenue YoY % = DIVIDE([Total Revenue] - [Revenue LY], [Revenue LY], 0)
   ```

3. **Customer:**
   ```dax
   # Customers = DISTINCTCOUNT(Sales[CustomerID])
   Revenue per Customer = DIVIDE([Total Revenue], [# Customers], 0)
   ```

**Part 2 — Build KPI Report Page (15 min)**

4. Create a new page: **"KPI Scorecard"**
5. **Top Row — 5 KPI Cards:**
   - Total Revenue, Gross Profit, Gross Margin %, Total Orders, # Customers
6. **Middle — Comparison Visuals:**
   - Clustered Bar Chart: Category vs Revenue + Revenue LY (side by side)
   - Line Chart: Monthly Revenue + Revenue LY (two trend lines)
7. **Bottom — Performance Matrix:**
   - Matrix: Region (Rows) × Revenue, Gross Profit, Margin %, YoY % (Values)
   - Format YoY % with conditional formatting (green positive, red negative)
8. **Slicers:** Year (Tile), Region (Dropdown)
9. Format all measures (Currency, Percentage, Whole Number)
10. Save

---

## Session 20 — Key Takeaways

1. **Define KPIs first** — Revenue, Profit, Orders, Growth, Customer metrics
2. **VAR** makes complex measures readable and efficient — calculate once, use many times
3. **Target comparison** = Actual, Target, Variance, Achievement %, Status
4. **Dynamic measures** with SWITCH + disconnected table let users choose metrics
5. **Document measures** with comments and descriptions for team collaboration

---

## Module 4 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 16 | DAX Intro & Calculated Columns | IF, SWITCH, RELATED, FORMAT |
| 17 | DAX Measures | SUM, COUNT, CALCULATE, ALL, filter context |
| 18 | DAX Aggregations | SUMX, FILTER, RANKX, conditional aggregations |
| 19 | Time Intelligence | YTD, YoY, MoM, DATEADD, Running Total, Moving Average |
| 20 | Business Metrics & KPI Reports | P&L measures, targets, scorecards, VAR |

### Module 4 → Module 5 Bridge
You now have **powerful DAX calculations driving your dashboards**. In Module 5 (Sessions 21–25), you'll learn **advanced reporting features** — Bookmarks, Tooltips, Conditional Formatting, Row-Level Security, and professional dashboard design.

---

## Preparation for Session 21
- Review: What are Bookmarks in Power BI?
- Think about: How would you show/hide visuals based on a button click?
- Explore: What is Conditional Formatting in a Matrix visual?

---

*Session 20 of 30 | Module 4: DAX Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
