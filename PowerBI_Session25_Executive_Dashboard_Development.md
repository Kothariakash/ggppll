# Session 25 — Executive Dashboard Development
## Module 5: Advanced Reporting | Professional Power BI Certification
### Duration: 1 Hour | Type: Hands-On | Hands-On: Build a Complete Executive Dashboard from Scratch

---

## Learning Objectives
By the end of this session, you will be able to:
1. Plan and wireframe an executive dashboard
2. Build a polished multi-page report using all Module 5 techniques
3. Integrate Bookmarks, Conditional Formatting, and RLS into one report
4. Apply professional design principles end-to-end
5. Prepare a dashboard for stakeholder presentation

---

## 25.1 Executive Dashboard Requirements

### The Brief

> Build a **Sales Performance Executive Dashboard** for the VP of Sales. The dashboard should provide a high-level overview of sales performance, enable drill-down into product and regional details, and support secure role-based access.

### Functional Requirements

| Requirement | Implementation |
|-------------|---------------|
| **KPI summary at a glance** | Cards: Revenue, Profit, Orders, Margin, Customers |
| **Trend analysis** | Line chart: Monthly revenue + YoY comparison |
| **Category breakdown** | Bar chart: Revenue by Product Category |
| **Regional analysis** | Map + matrix with conditional formatting |
| **Target comparison** | Gauge or scorecard with achievement % |
| **Detail drill-down** | Drill-through page for product/customer detail |
| **Toggle views** | Bookmarks: Chart ↔ Table toggle |
| **Data security** | RLS: Regional managers see only their data |
| **Reset filters** | Bookmark-based reset button |
| **Mobile ready** | Mobile layout configured |

---

## 25.2 Dashboard Wireframe

### Page 1: Executive Summary

```
┌──────────────────────────────────────────────────────────────────┐
│  [Logo] Sales Performance Dashboard — FY2024  [Region▼] [Year▼] │
├──────────┬──────────┬──────────┬──────────┬──────────────────────┤
│ ₹42.3 Cr │ ₹7.8 Cr  │  12,500  │  18.5%   │ ▲12% YoY           │
│ Revenue  │ Profit   │ Orders   │ Margin   │ Growth              │
│ ●Green   │ ●Green   │ ●Yellow  │ ●Red     │                      │
├──────────┴──────────┴──────────┴──────────┴──────────────────────┤
│ ┌────────────────────────────┐ ┌────────────────────────────────┐│
│ │ Monthly Revenue Trend      │ │ Revenue by Category            ││
│ │ (Line: Actual + LY)       │ │ (Bar: sorted desc)             ││
│ │ [📊Chart] [📋Table] toggle │ │                                ││
│ └────────────────────────────┘ └────────────────────────────────┘│
│ ┌────────────────────────────┐ ┌────────────────────────────────┐│
│ │ Regional Performance       │ │ Top 5 Products (Table)         ││
│ │ (Filled Map)              │ │ Product | Revenue | Margin     ││
│ └────────────────────────────┘ └────────────────────────────────┘│
│                        [🔄 Reset Filters]                        │
├──────────────────────────────────────────────────────────────────┤
│  [Executive Summary] [Regional Detail] [Product Detail]  ← Nav  │
└──────────────────────────────────────────────────────────────────┘
```

### Page 2: Regional Detail

```
┌──────────────────────────────────────────────────────────────────┐
│  Regional Performance Detail                 [Region▼] [Year▼]  │
├──────────────────────────────────────────────────────────────────┤
│ ┌────────────────────────────────────────────────────────────┐   │
│ │ Matrix: Region × Revenue | Profit | Margin% | YoY% | Achv% │   │
│ │ (with conditional formatting: heat map + icons)            │   │
│ └────────────────────────────────────────────────────────────┘   │
│ ┌────────────────────────────┐ ┌────────────────────────────┐   │
│ │ Revenue by Region (Bar)    │ │ Monthly Trend by Region     │   │
│ │ (horizontal, sorted)      │ │ (Line, multi-series)        │   │
│ └────────────────────────────┘ └────────────────────────────┘   │
│                                                                  │
│  [Executive Summary] [Regional Detail] [Product Detail]  ← Nav  │
└──────────────────────────────────────────────────────────────────┘
```

### Page 3: Product Detail (Drill-Through)

```
┌──────────────────────────────────────────────────────────────────┐
│  ← Back   Product Detail: [Selected Category]                   │
├──────────┬──────────┬──────────┬──────────────────────────────────┤
│ Revenue  │ Profit   │ Orders   │ Margin %                        │
│ (Card)   │ (Card)   │ (Card)   │ (Card)                          │
├──────────┴──────────┴──────────┴──────────────────────────────────┤
│ ┌─────────────────────────────────────────────────────────────┐  │
│ │ Table: Product Name | Revenue | Cost | Profit | Margin%     │  │
│ │ (with data bars on Revenue, icons on Margin%)              │  │
│ └─────────────────────────────────────────────────────────────┘  │
│ ┌─────────────────────────────────────────────────────────────┐  │
│ │ Monthly Revenue Trend (Line Chart for selected category)    │  │
│ └─────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

---

## 25.3 Build Checklist

### Phase 1: Data Foundation (Verify)
- [ ] Star Schema model validated (Sales, Products, Customers, Date, Regions)
- [ ] Date table marked as Date Table
- [ ] All relationships 1:Many, Single direction
- [ ] All ID/FK columns hidden

### Phase 2: Measures (Create/Verify)
- [ ] Total Revenue, Total Cost, Total Profit
- [ ] Gross Margin %, Profit Margin %
- [ ] Total Orders, # Customers, Avg Order Value
- [ ] Revenue LY, Revenue YoY %, Revenue MoM %
- [ ] Revenue YTD, Revenue YTD LY, YTD Growth %
- [ ] Achievement % (if targets table exists)
- [ ] Revenue % of Total
- [ ] Product Rank (RANKX)

### Phase 3: Conditional Formatting Measures
- [ ] Margin Color (hex code based on margin %)
- [ ] YoY Color (green/red based on positive/negative)
- [ ] Achievement Status (Above/Near/Below Target)

### Phase 4: Page 1 — Executive Summary
- [ ] Apply Theme
- [ ] 5 KPI Cards with conditional font color
- [ ] 2 Slicers (Region dropdown, Year tiles)
- [ ] Line Chart (Monthly Revenue + Revenue LY)
- [ ] Bar Chart (Revenue by Category, sorted descending)
- [ ] Filled Map (Revenue by State/Region)
- [ ] Top 5 Products Table (with data bars)
- [ ] Chart ↔ Table toggle (Bookmarks + Buttons)
- [ ] Reset Filters button (Bookmark)
- [ ] Navigation buttons to other pages

### Phase 5: Page 2 — Regional Detail
- [ ] Matrix with conditional formatting (heat map, icons)
- [ ] Regional bar chart
- [ ] Multi-line trend chart
- [ ] Synced slicers
- [ ] Navigation buttons

### Phase 6: Page 3 — Product Detail (Drill-Through)
- [ ] Drill-through filter on Product Category
- [ ] Back button
- [ ] KPI cards for selected category
- [ ] Product detail table with data bars and icons
- [ ] Monthly trend line for selected category

### Phase 7: Security & Polish
- [ ] RLS role created (at least one static or dynamic)
- [ ] RLS tested (View as Roles)
- [ ] Alt text on key visuals
- [ ] Tab order set
- [ ] Mobile layout configured
- [ ] All visuals named in Selection Pane
- [ ] Bookmark groups organized

### Phase 8: Validation
- [ ] Grand total matches source data
- [ ] Slicers filter all visuals correctly
- [ ] Drill-through works and Back button returns
- [ ] Chart ↔ Table toggle works
- [ ] Reset button clears all filters
- [ ] Navigation buttons work on every page
- [ ] RLS restricts data correctly
- [ ] No "(Blank)" values visible

---

## 25.4 Step-by-Step Build Guide

### Step 1: Set Up the Canvas
1. Apply a Theme (View → Themes → choose or import custom)
2. Set page size to 16:9 (Format → Canvas Settings)
3. Add company logo (Insert → Image) — top-left corner
4. Add report title text box: "Sales Performance Dashboard — FY2024"

### Step 2: Build KPI Cards
1. Create 5 Card visuals across the top
2. Fields: Total Revenue, Total Profit, Total Orders, Gross Margin %, Revenue YoY %
3. Format: Large font (28-32pt), appropriate display units, decimal places
4. Apply conditional font color on YoY % card (green/red)

### Step 3: Add Slicers
1. Region slicer: Dropdown style, Select All enabled, Search enabled
2. Year slicer: Tile/Button style, Single select
3. Position: top-right of the page

### Step 4: Build Main Visuals
1. **Line Chart:** X-axis = Month, Y-axis = Total Revenue + Revenue LY, Legend by series
2. **Bar Chart:** X-axis = Product Category, Y-axis = Total Revenue, sorted descending
3. **Filled Map:** Location = Region/State, Values = Total Revenue
4. **Table:** Product Name, Total Revenue (with data bars), Gross Margin % (with icons)
5. Filter table to Top 5 by Revenue (Filters pane → Top N)

### Step 5: Create Toggle (Bookmarks)
1. Create a Table visual overlapping the Line Chart (same position/size)
2. Selection Pane: Hide Table → create "Chart View" bookmark (uncheck Data)
3. Selection Pane: Show Table, Hide Chart → create "Table View" bookmark (uncheck Data)
4. Insert two buttons → link to bookmarks

### Step 6: Create Reset Button
1. Clear all slicers
2. Create "Reset All" bookmark (check Data, check Display)
3. Insert button → text "🔄 Reset" → link to "Reset All" bookmark

### Step 7: Build Remaining Pages
1. **Page 2:** Regional matrix with conditional formatting, bar chart, trend
2. **Page 3:** Drill-through page with Category filter, back button, detail visuals
3. Add Navigation buttons on all pages

### Step 8: Apply RLS
1. Modeling → Manage Roles → create at least one role
2. Test with View as Roles

### Step 9: Final Polish
1. Align all visuals (Format → Align → Distribute)
2. Add alt text to key visuals
3. Set tab order in Selection Pane
4. Configure Mobile Layout (View → Mobile Layout)
5. Name all visuals descriptively in Selection Pane

### Step 10: Validate and Save
1. Run through the validation checklist (Section 25.3, Phase 8)
2. Save as `Executive_Dashboard_Final.pbix`

---

## 25.5 Presentation Tips

### Presenting Your Dashboard to Stakeholders

| Tip | Detail |
|-----|--------|
| **Start with the "So What"** | "Revenue is up 12% YoY, but margins are declining" |
| **Walk through the layout** | Explain the information hierarchy top-to-bottom |
| **Demo interactivity** | Show slicer filtering, drill-through, toggle views |
| **Show RLS** | "Sales managers will only see their region" |
| **Highlight conditional formatting** | "Red cells need immediate attention" |
| **End with next steps** | "I recommend we focus on improving East region margins" |

### Common Stakeholder Questions to Prepare For

1. "Can I see this by [different dimension]?" → Add a slicer or create a bookmark
2. "How does this compare to last year?" → Show YoY measures
3. "Who else can see this data?" → Explain RLS roles
4. "Can this update automatically?" → Explain scheduled refresh
5. "Can I export the data?" → Show Export Data option in visuals

---

## 🔧 Hands-On Activity: Build the Executive Dashboard

**Duration:** 30+ minutes (extend as homework if needed)

Follow the **Step-by-Step Build Guide** in Section 25.4 to build the complete dashboard. Use the **Build Checklist** in Section 25.3 to track your progress.

**Minimum deliverable for this session:**
1. Page 1 with KPI Cards, Slicers, at least 3 chart visuals
2. Navigation to at least one additional page
3. At least one Bookmark toggle
4. Conditional formatting on at least one visual
5. Save as `Executive_Dashboard_Final.pbix`

**Homework (complete before Session 26):**
- Finish all 3 pages
- Add RLS, drill-through, and reset button
- Polish: theme, alignment, alt text, mobile layout

---

## Session 25 — Key Takeaways

1. **Plan before building** — wireframe the layout, define measures, list requirements
2. **Use a build checklist** — systematic approach prevents missed elements
3. **Integrate all Module 5 techniques:** Bookmarks, Conditional Formatting, RLS, Design Principles
4. **Validate thoroughly** — numbers, interactions, security, accessibility
5. **Present the story, not the tool** — stakeholders care about insights, not features

---

## Module 5 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 21 | Bookmarks & Tooltips | Toggle views, tab navigation, custom tooltip pages |
| 22 | Conditional Formatting | Color scales, rules, data bars, icons, DAX-driven colors |
| 23 | Row-Level Security | Static/Dynamic RLS, USERPRINCIPALNAME, role testing |
| 24 | Dashboard Design Principles | 10 principles, color theory, typography, accessibility |
| 25 | Executive Dashboard | End-to-end build, wireframe, presentation |

### Module 5 → Module 6 Bridge
You've built a **complete, secure, professionally designed executive dashboard**. In Module 6 (Sessions 26–30), you'll learn to **publish, share, and collaborate** using Power BI Service, and complete a **Capstone Project** that demonstrates all skills learned.

---

## Preparation for Session 26
- Create a **free Power BI account** at [app.powerbi.com](https://app.powerbi.com) (work or school email required)
- Have your finished `Executive_Dashboard_Final.pbix` file ready to publish
- Review: What is a Workspace in Power BI Service?

---

*Session 25 of 30 | Module 5: Advanced Reporting*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
