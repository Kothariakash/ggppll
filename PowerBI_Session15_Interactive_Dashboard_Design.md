# Session 15 — Interactive Dashboard Design
## Module 3: Data Visualization | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Design a Complete Interactive Business Dashboard

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply dashboard design principles (layout, hierarchy, white space)
2. Build a complete multi-page interactive dashboard
3. Use navigation buttons for page switching
4. Apply the "Inverted Pyramid" information hierarchy
5. Conduct a dashboard review using a quality checklist

---

## 15.1 Dashboard Design Principles

### The 5-Second Rule
> A user should understand the key message of your dashboard within 5 seconds of looking at it.

### The Inverted Pyramid (Information Hierarchy)

```
┌──────────────────────────────────────────┐
│     TOP: KPIs & Headlines                │  ← What happened? (5 seconds)
│     (Cards, big numbers, status)         │
├──────────────────────────────────────────┤
│     MIDDLE: Trends & Comparisons         │  ← Why? (30 seconds)
│     (Charts, maps, key visuals)          │
├──────────────────────────────────────────┤
│     BOTTOM: Details & Drill-Down         │  ← Show me more (1-2 minutes)
│     (Tables, matrices, detail pages)     │
└──────────────────────────────────────────┘
```

### Layout Grid System

Use a consistent grid for visual alignment:

```
┌────────┬────────┬────────┬────────┐
│ Card 1 │ Card 2 │ Card 3 │ Card 4 │   Row 1: KPI Cards (20% height)
├────────┴────┬───┴────────┴────────┤
│             │                     │
│  Chart 1    │     Chart 2         │   Row 2: Main Visuals (50% height)
│             │                     │
├─────────────┴─────────────────────┤
│                                   │
│        Table / Matrix             │   Row 3: Detail (30% height)
│                                   │
└───────────────────────────────────┘
```

---

## 15.2 Layout Patterns

### Pattern 1: Executive Summary (Single Page)

```
┌──────────────────────────────────────────────────────────┐
│  COMPANY LOGO          Sales Dashboard — FY2024    [▼ Region] [▼ Year]  │
├──────────┬──────────┬──────────┬──────────┬──────────────┤
│ ₹42.3 Cr │ 12,500   │ ₹3,384   │  18.5%   │ ▲ 12% vs LY │
│ Revenue  │ Orders   │ AOV      │ Margin   │ Growth       │
├──────────┴──────────┴──────────┴──────────┴──────────────┤
│ ┌─────────────────────────┐  ┌─────────────────────────┐ │
│ │ Monthly Revenue Trend   │  │ Revenue by Category     │ │
│ │ (Line chart)            │  │ (Horizontal bar)        │ │
│ └─────────────────────────┘  └─────────────────────────┘ │
│ ┌─────────────────────────┐  ┌─────────────────────────┐ │
│ │ Revenue by Region (Map) │  │ Top 10 Products (Table) │ │
│ └─────────────────────────┘  └─────────────────────────┘ │
└──────────────────────────────────────────────────────────┘
```

### Pattern 2: Multi-Page Report

| Page | Purpose | Content |
|------|---------|---------|
| **Page 1: Executive Summary** | High-level KPIs and trends | Cards, trend line, top performers |
| **Page 2: Sales Analysis** | Detailed sales breakdown | Category, region, product charts |
| **Page 3: Customer Analysis** | Customer segments and behavior | Segment breakdown, top customers |
| **Page 4: Geographic View** | Location-based insights | Maps, regional comparison |
| **Page 5: Detail / Drill-through** | Line-item details | Tables, drill-through targets |

### Pattern 3: Left Navigation Sidebar

```
┌──────────┬───────────────────────────────────────────┐
│          │                                           │
│  🏠 Home │   Dashboard Content Area                  │
│  📊 Sales│                                           │
│  👥 Cust │   (Changes based on navigation selection) │
│  🗺️ Region│                                          │
│  📋 Detail│                                          │
│          │                                           │
│          │                                           │
│  [Logo]  │                                           │
└──────────┴───────────────────────────────────────────┘
```

---

## 15.3 Navigation Buttons

### Adding Navigation Buttons

1. **Insert** tab → **Buttons** → choose button type
2. OR: Insert → Shapes → format as a button

### Button Types

| Type | Purpose |
|------|---------|
| **Blank** | Custom button — add text and icon |
| **Back** | Returns to previous page (for drill-through) |
| **Bookmark** | Navigates to a saved bookmark state |
| **Page Navigation** | Navigates to a specific page |
| **Q&A** | Opens Q&A natural language query |
| **Web URL** | Opens an external link |
| **Information** | Shows an info tooltip |

### Configuring Page Navigation

1. Insert a button (or shape)
2. Format → **Action → On**
3. Type: **Page Navigation**
4. Destination: Select the target page
5. Add text/icon to the button for clarity

### Building a Navigation Bar

1. Create buttons for each page
2. Arrange horizontally (top) or vertically (left sidebar)
3. Use **consistent styling** — active page highlighted, others dimmed
4. Copy the nav bar to all pages for consistency
5. Update each button's destination on each page

### Navigation Best Practices

| Practice | Why |
|----------|-----|
| **Always include a "Home" button** | Users need to return to the overview |
| **Highlight the current page** | Users should know where they are |
| **Keep navigation consistent** | Same position and style on every page |
| **Use icons + text** | Icons alone can be ambiguous |
| **Limit to 5–7 pages max** | More pages = harder navigation |

---

## 15.4 White Space and Alignment

### White Space Rules

| Rule | Application |
|------|------------|
| **Consistent margins** | 10–15px padding around all visuals |
| **Consistent gaps** | Same spacing between all visuals |
| **Breathing room** | Don't fill every pixel — space helps readability |
| **Group related visuals** | Place related charts close together with shared background |

### Alignment Tools

- **View** tab → **Snap to Grid** (aligns visuals to invisible grid)
- **View** tab → **Gridlines** (shows the grid)
- **Format** tab → **Align** → Left/Right/Center/Top/Bottom/Distribute
- Use **Ctrl+Click** to select multiple visuals → align together

### Visual Grouping

Group related visuals with a background rectangle:
1. Insert → Shapes → Rectangle
2. Set fill color (light gray or brand color at 10% opacity)
3. No border or subtle border
4. Send to Back (right-click → Send to Back)
5. Place related visuals on top of the rectangle

---

## 15.5 Mobile Layout

### Designing for Mobile

1. **View** tab → **Mobile Layout**
2. A phone-shaped canvas appears
3. Drag visuals from the desktop layout onto the mobile canvas
4. Resize for mobile-friendly display

### Mobile Design Tips

| Tip | Why |
|-----|-----|
| **Cards at top** | KPIs should be immediately visible |
| **Stack vertically** | One visual per row on mobile |
| **Simplify** | Fewer visuals than desktop — key insights only |
| **Large touch targets** | Slicers and buttons need to be finger-friendly |
| **Test on actual phone** | Use Power BI Mobile app to verify |

---

## 15.6 Report Page Settings

### Page Size Options

| Size | Dimensions | Use Case |
|------|-----------|----------|
| **16:9** (default) | 1280 × 720 px | Standard widescreen display |
| **4:3** | 960 × 720 px | Presentations, older monitors |
| **Letter** | 816 × 1056 px | Print-ready reports |
| **Tooltip** | 320 × 240 px | Tooltip pages |
| **Custom** | Any size | Specific display requirements |

### Page Background

- Format → Canvas Background → Color / Image
- Use subtle background colors (light gray, off-white)
- Background images: use company watermark or subtle pattern at low transparency

### Page Wallpaper

- Fills the area OUTSIDE the report canvas
- Only visible in Power BI Service (not Desktop)
- Use for border effects or branding

---

## 15.7 Dashboard Quality Checklist

### Before Publishing — Review Against These Criteria

**Content & Accuracy**
- [ ] Dashboard answers a clear business question
- [ ] KPI cards at the top show the most important metrics
- [ ] All numbers are validated against source data
- [ ] No "(Blank)" values visible without explanation
- [ ] Date range is clear (title or slicer shows the period)

**Design & Layout**
- [ ] Consistent color scheme (2–4 colors)
- [ ] Consistent fonts and sizes across all visuals
- [ ] All visuals aligned to grid
- [ ] White space between visuals (not cramped)
- [ ] Related visuals grouped logically
- [ ] Title and subtitle on every page

**Interactivity**
- [ ] Slicers work correctly (test each one)
- [ ] Cross-filtering behaves as expected
- [ ] Drill-through pages are functional (test right-click)
- [ ] Navigation buttons work between pages
- [ ] Back buttons on detail pages
- [ ] Tooltip pages display correctly on hover

**Usability**
- [ ] A new user can understand the dashboard without training
- [ ] Visual titles are descriptive (not "Chart 1")
- [ ] Units are clear (₹, %, count, Cr, Lakhs)
- [ ] Legend is visible and understandable
- [ ] Mobile layout configured (if needed)

**Performance**
- [ ] Report opens in < 5 seconds
- [ ] Visual interactions respond quickly
- [ ] No unnecessary columns loaded (check Power Query)

---

## 🔧 Hands-On Activity: Build a Complete Dashboard

**Duration:** 30 minutes

### Scenario
Build a **Sales Performance Dashboard** for a retail company's VP of Sales.

### Requirements

**Page 1: Executive Summary**
1. **Title:** "Sales Performance Dashboard — FY2024"
2. **4 KPI Cards** across top: Revenue, Orders, AOV, Profit Margin
3. **2 Slicers:** Region (Dropdown), Year (Tile buttons)
4. **Line Chart:** Monthly Revenue Trend (with trend line)
5. **Bar Chart:** Revenue by Product Category (sorted descending)
6. **Donut Chart:** Revenue by Customer Segment
7. Apply a **Theme** and consistent formatting

**Page 2: Regional Analysis**
8. **Map:** Revenue by City/State (Bubble Map)
9. **Matrix:** Region × Quarter × Revenue (with subtotals)
10. **Bar Chart:** Top 5 Cities by Revenue
11. Copy slicers from Page 1 (or sync them)

**Page 3: Product Detail (Drill-Through)**
12. Set **Product Category** as drill-through filter
13. **Table:** Product Name, Revenue, Quantity, Avg Price
14. **Line Chart:** Monthly trend for the selected category
15. **2 Cards:** Category Revenue, Category Order Count
16. Verify Back button exists

**Navigation**
17. Add **Page Navigation buttons** on Pages 1 and 2
18. Ensure consistent button placement

**Final Steps**
19. Test all interactions: slicers, cross-filtering, drill-through
20. Run through the **Quality Checklist** above
21. Save as `Sales_Dashboard_Complete.pbix`

---

## Session 15 — Key Takeaways

1. **Inverted Pyramid:** KPIs at top → Charts in middle → Details at bottom
2. **Consistency is king:** same colors, fonts, spacing, and layout across pages
3. **Navigation buttons** make multi-page reports user-friendly
4. **White space and alignment** are as important as the visuals themselves
5. Always run a **quality checklist** before publishing

---

## Module 3 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 11 | Charts & Tables | Bar, Line, Pie, Table, Matrix, Combo charts |
| 12 | Maps & Cards | Geographic visuals, KPI Cards, Gauge, KPI visual |
| 13 | KPIs & Slicers | Interactive filtering, slicer types, sync across pages |
| 14 | Formatting & Drill-Through | Themes, formatting, drill-down, drill-through, tooltips |
| 15 | Dashboard Design | Layout patterns, navigation, quality checklist |

### Module 3 → Module 4 Bridge
You can now **build professional interactive dashboards**. In Module 4 (Sessions 16–20), you'll learn **DAX** — the formula language that powers calculated columns, measures, time intelligence, and advanced business metrics.

---

## Preparation for Session 16
- Open the DAX formula bar: In Report View, go to Modeling tab
- Review: What is the difference between a Column and a Measure?
- Think about: What calculations would make your dashboard more powerful? (Profit %, YoY growth, running totals)

---

*Session 15 of 30 | Module 3: Data Visualization*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
