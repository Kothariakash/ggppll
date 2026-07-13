# Session 29 — Capstone Project Build
## Module 6: Power BI Service & Capstone | Professional Power BI Certification
### Duration: 1 Hour | Type: Hands-On | Hands-On: Build an End-to-End Business Intelligence Solution

---

## Learning Objectives
By the end of this session, you will be able to:
1. Define and scope a real-world BI project
2. Apply all 28 sessions of learning into a single cohesive solution
3. Build a complete Power BI solution from data import to published dashboard
4. Document your approach and design decisions
5. Prepare for the capstone presentation (Session 30)

---

## 29.1 Capstone Project Overview

### The Assignment

> Build and present a **complete end-to-end Business Intelligence solution** using Power BI that demonstrates mastery of all skills learned in this course.

### Deliverables

| # | Deliverable | Description |
|---|-------------|-------------|
| 1 | **Power BI Report (.pbix)** | Multi-page interactive report with Star Schema, DAX, and advanced features |
| 2 | **Published Dashboard** | At least one dashboard in Power BI Service with pinned KPIs |
| 3 | **Presentation (5-10 min)** | Walk through the solution: data, model, visuals, insights |
| 4 | **Documentation** | Brief write-up of business problem, data sources, measures, and design decisions |

---

## 29.2 Choosing a Capstone Topic

### Option 1: Retail / E-Commerce Sales Dashboard

**Business Question:** How is our retail business performing across products, regions, and time periods?

**Dataset:** Sales transactions with products, customers, regions, dates

**Key Deliverables:**
- Revenue, Profit, Orders KPIs with YoY comparison
- Product category analysis with ranking
- Regional performance map
- Time intelligence: YTD, MoM, trends
- Drill-through to product detail

### Option 2: HR / People Analytics Dashboard

**Business Question:** What is our workforce composition and where are our retention challenges?

**Dataset:** Employee master data with hire dates, departments, salaries, attrition

**Key Deliverables:**
- Headcount, Attrition Rate, Avg Tenure KPIs
- Department and location breakdown
- Attrition trend analysis with YoY
- Salary distribution by grade/level
- Diversity metrics

### Option 3: Financial Performance Dashboard

**Business Question:** How is our company performing against budget targets across business units?

**Dataset:** Actuals vs budget by account, department, month

**Key Deliverables:**
- Revenue, EBITDA, Net Income KPIs
- Budget vs Actual variance with conditional formatting
- Monthly P&L trend
- Department expense breakdown
- YTD performance scorecard

### Option 4: Supply Chain / Operations Dashboard

**Business Question:** How efficient is our supply chain and where are the bottlenecks?

**Dataset:** Orders, shipments, inventory, suppliers

**Key Deliverables:**
- On-Time Delivery %, Fill Rate, Cycle Time KPIs
- Supplier performance scorecard
- Inventory levels by warehouse
- Order fulfillment trend
- Geographic distribution of delays

### Option 5: Custom Topic

Choose a dataset and business problem relevant to your own organization or interest. Ensure it has:
- At least 3 related tables (Star Schema)
- Date dimension for time intelligence
- Numeric measures for KPI calculations
- Categorical dimensions for slicing/filtering

---

## 29.3 Capstone Evaluation Rubric

### Scoring Criteria (100 Points Total)

| Category | Criteria | Points |
|----------|---------|--------|
| **Data Foundation (20)** | | |
| | Connects to at least 2 data sources | 5 |
| | Data cleaned in Power Query (types, nulls, transforms) | 5 |
| | Star Schema with proper relationships (1:Many) | 5 |
| | Date table created and marked | 5 |
| **DAX & Calculations (25)** | | |
| | At least 5 explicit measures (SUM, COUNT, DIVIDE) | 8 |
| | At least 2 time intelligence measures (YTD, YoY, MoM) | 7 |
| | Uses CALCULATE with filter modification | 5 |
| | Uses VAR for readable measure code | 5 |
| **Visualization & Design (25)** | | |
| | 3+ report pages with clear layout hierarchy | 5 |
| | Appropriate chart types for data (no 3D, no misused pie charts) | 5 |
| | Consistent theme, fonts, colors | 5 |
| | Interactive slicers with cross-filtering | 5 |
| | Drill-through page functional | 5 |
| **Advanced Features (15)** | | |
| | Bookmarks (toggle view or navigation) | 5 |
| | Conditional formatting (colors, icons, or data bars) | 5 |
| | Row-Level Security role defined | 5 |
| **Publishing & Sharing (10)** | | |
| | Report published to Power BI Service | 3 |
| | Dashboard created with pinned KPIs | 4 |
| | Scheduled refresh configured (or explained) | 3 |
| **Presentation (5)** | | |
| | Clear explanation of business problem and insights | 3 |
| | Professional delivery (within time limit) | 2 |

---

## 29.4 Build Guide — Step-by-Step

### Phase 1: Data Foundation (20 minutes)

**Step 1: Prepare Data Sources**
- Identify 2–3 related data files (Excel, CSV)
- Ensure they have a common key column (e.g., ProductID, CustomerID)
- Ensure at least one date column for time intelligence

**Step 2: Import & Transform in Power Query**
- Get Data → Import all sources
- Clean: Remove unnecessary columns, change data types
- Handle nulls and errors
- Rename columns descriptively
- Apply any needed transformations (unpivot, merge, split)
- Close & Apply

**Step 3: Build Star Schema**
- Switch to Model View
- Create/verify relationships (1:Many, Single direction)
- Create Date Table:
  ```dax
  DateTable = ADDCOLUMNS(CALENDARAUTO(), 
      "Year", YEAR([Date]), 
      "Quarter", "Q" & QUARTER([Date]),
      "Month", FORMAT([Date], "MMMM"),
      "MonthNumber", MONTH([Date]),
      "MonthYear", FORMAT([Date], "MMM YYYY")
  )
  ```
- Mark as Date Table
- Hide ID/FK columns
- Arrange tables in star layout

### Phase 2: DAX Measures (15 minutes)

**Step 4: Create Core Measures**
```dax
// Basic
Total Revenue = SUM(Sales[Revenue])
Total Cost = SUM(Sales[Cost])
Total Profit = [Total Revenue] - [Total Cost]
Total Orders = COUNTROWS(Sales)
# Customers = DISTINCTCOUNT(Sales[CustomerID])

// Ratios
Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)
Avg Order Value = DIVIDE([Total Revenue], [Total Orders], 0)

// Time Intelligence
Revenue YTD = TOTALYTD([Total Revenue], DateTable[Date])
Revenue LY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(DateTable[Date]))
Revenue YoY % = DIVIDE([Total Revenue] - [Revenue LY], [Revenue LY], 0)
Revenue Prev Month = CALCULATE([Total Revenue], DATEADD(DateTable[Date], -1, MONTH))
Revenue MoM % = DIVIDE([Total Revenue] - [Revenue Prev Month], [Revenue Prev Month], 0)

// Advanced
Revenue % of Total = DIVIDE([Total Revenue], CALCULATE([Total Revenue], ALL(Sales)), 0)
```

**Step 5: Create Conditional Formatting Measures**
```dax
YoY Color = IF([Revenue YoY %] >= 0, "#27AE60", "#E74C3C")
Margin Status = SWITCH(TRUE(), [Profit Margin %] >= 0.2, "Above Target", [Profit Margin %] >= 0.15, "Near Target", "Below Target")
```

### Phase 3: Visualization (15 minutes)

**Step 6: Page 1 — Executive Summary**
- Apply Theme
- 4–5 KPI Cards across top (Revenue, Profit, Orders, Margin, YoY %)
- 2 Slicers (Region dropdown, Year tiles)
- Line Chart: Monthly Revenue Trend (+ Revenue LY)
- Bar Chart: Revenue by Category (sorted descending)
- Map or Donut for geographic/segment view
- Navigation buttons

**Step 7: Page 2 — Detailed Analysis**
- Matrix with conditional formatting (heat map + icons)
- Additional charts relevant to your topic
- Synced slicers

**Step 8: Page 3 — Drill-Through Detail**
- Set drill-through filter (Product Category or Region)
- Detail table with data bars
- KPI cards for the selected context
- Back button

### Phase 4: Advanced Features (5 minutes)

**Step 9: Bookmarks**
- Create at least one toggle (Chart ↔ Table) with buttons

**Step 10: Conditional Formatting**
- Apply to at least one matrix/table (background color or icons)

**Step 11: RLS**
- Create at least one role (e.g., regional filter)
- Test with View as Roles

### Phase 5: Publish & Dashboard (5 minutes)

**Step 12: Publish**
- Home → Publish → select workspace

**Step 13: Create Dashboard**
- Pin KPI cards and key charts to a new Dashboard
- Arrange tiles

**Step 14: Configure Refresh**
- Set up scheduled refresh (or document what you would configure)

---

## 29.5 Capstone Checklist

Use this checklist to ensure completeness:

### Data Foundation
- [ ] 2+ data sources imported
- [ ] Power Query: types set, nulls handled, columns renamed
- [ ] Star Schema: Fact + Dimensions with 1:Many relationships
- [ ] Date table created with CALENDARAUTO and marked as Date Table
- [ ] ID/FK columns hidden from Report View

### DAX Measures
- [ ] 5+ explicit measures created
- [ ] At least 2 time intelligence measures (YTD, YoY, MoM)
- [ ] CALCULATE used with filter modification (ALL, ALLEXCEPT)
- [ ] VAR used in at least one measure
- [ ] DIVIDE used instead of division operator
- [ ] Measures formatted correctly (Currency, %, Whole Number)

### Visualization
- [ ] 3+ report pages
- [ ] KPI Cards at top of main page
- [ ] Appropriate chart types (bar, line, map, table/matrix)
- [ ] Consistent theme applied
- [ ] Slicers: 2-4 per page, correctly synced
- [ ] All visuals titled descriptively
- [ ] Drill-through page functional with Back button
- [ ] Navigation buttons between pages

### Advanced Features
- [ ] At least 1 Bookmark toggle (Chart ↔ Table)
- [ ] Conditional formatting on at least 1 visual
- [ ] RLS role created and tested
- [ ] Alt text on key visuals

### Publishing
- [ ] Report published to Power BI Service
- [ ] Dashboard created with pinned KPIs
- [ ] Scheduled refresh configured (or documented)

### Documentation
- [ ] Business problem statement written
- [ ] Data sources listed
- [ ] Key measures documented
- [ ] Design decisions explained

---

## 29.6 Documentation Template

### Capstone Project Documentation

```
PROJECT TITLE: [Your Dashboard Name]
AUTHOR: [Your Name]
DATE: [Date]

1. BUSINESS PROBLEM
   What business question does this dashboard answer?
   Who is the target audience?
   What decisions will this dashboard support?

2. DATA SOURCES
   | Source | Type | Description | Rows | Key Fields |
   |--------|------|-------------|------|------------|
   | Sales.xlsx | Excel | Transaction data | 10,000 | OrderID, Date, Revenue |
   | Products.csv | CSV | Product catalog | 200 | ProductID, Name, Category |
   | ... | ... | ... | ... | ... |

3. DATA MODEL
   - Star Schema: [Describe fact and dimension tables]
   - Date Table: CALENDARAUTO with Year, Quarter, Month
   - Relationships: [List all 1:Many relationships]

4. KEY MEASURES
   | Measure | Formula | Purpose |
   |---------|---------|---------|
   | Total Revenue | SUM(Sales[Revenue]) | Primary revenue metric |
   | Revenue YoY % | DIVIDE(...) | Year-over-year growth |
   | ... | ... | ... |

5. REPORT PAGES
   | Page | Purpose | Key Visuals |
   |------|---------|-------------|
   | Executive Summary | High-level KPIs | Cards, Line, Bar, Map |
   | Regional Detail | Regional breakdown | Matrix, Bar, Trend |
   | Product Detail | Drill-through | Table, Cards, Line |

6. ADVANCED FEATURES
   - Bookmarks: [Chart ↔ Table toggle on Page 1]
   - Conditional Formatting: [Heat map on regional matrix]
   - RLS: [Regional role filtering]

7. KEY INSIGHTS
   - [Insight 1: Revenue grew 12% YoY driven by Electronics]
   - [Insight 2: West region underperforming — 15% below target]
   - [Insight 3: Top 5 products contribute 60% of total revenue]

8. RECOMMENDATIONS
   - [Recommendation based on insights]
```

---

## 🔧 Hands-On Activity: Build Your Capstone

**Duration:** Full session (60 minutes)

### Time Allocation

| Phase | Duration | Activities |
|-------|----------|-----------|
| **Phase 1: Data** | 20 min | Import, clean, Star Schema, Date table |
| **Phase 2: DAX** | 15 min | Create all measures, format them |
| **Phase 3: Visuals** | 15 min | Build 3 pages, apply theme, slicers |
| **Phase 4: Advanced** | 5 min | Bookmark, conditional formatting, RLS |
| **Phase 5: Publish** | 5 min | Publish, create dashboard, save |

### If You Run Out of Time

Prioritize in this order:
1. ✅ Star Schema + Date table (foundation)
2. ✅ 5 core measures (calculations)
3. ✅ Page 1 with KPIs + 2 charts (visualization)
4. ✅ Publish to Service (deliverable)
5. ⬜ Additional pages, bookmarks, RLS (polish)

Complete any remaining items as homework before Session 30.

---

## Session 29 — Key Takeaways

1. The capstone integrates **all 28 sessions** into one deliverable
2. Follow the **phased approach:** Data → DAX → Visuals → Advanced → Publish
3. Use the **checklist** to ensure nothing is missed
4. **Document** your approach — it's part of the deliverable
5. **Start with the business question** — every design decision should serve that question

---

## Preparation for Session 30
- **Complete your capstone** — all phases finished, published to Service
- **Write your documentation** using the template in Section 29.6
- **Prepare your 5–10 minute presentation:**
  - Business problem and audience
  - Data sources and model design
  - Live demo of the dashboard (slicers, drill-through, toggle)
  - Key insights and recommendations
- **Practice** your presentation at least once

---

*Session 29 of 30 | Module 6: Power BI Service & Capstone*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
