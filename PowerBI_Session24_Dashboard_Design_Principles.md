# Session 24 — Dashboard Design Principles
## Module 5: Advanced Reporting | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory | Hands-On: Dashboard Design Review & Redesign Exercise

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply the 10 principles of effective dashboard design
2. Identify and fix common dashboard design mistakes
3. Choose appropriate color palettes and typography
4. Design for different audiences (Executive, Analyst, Operational)
5. Apply accessibility best practices

---

## 24.1 The 10 Principles of Dashboard Design

### Principle 1: Start with the Business Question

> "What decision will this dashboard help someone make?"

**Before designing, answer:**
- Who is the audience? (CEO, VP Sales, Store Manager, Analyst)
- What decisions do they make? (Allocate budget, adjust pricing, hire staff)
- What metrics drive those decisions? (Revenue, Margin, Headcount, NPS)
- How often do they check? (Daily, Weekly, Monthly)

| Audience | Needs | Dashboard Type |
|----------|-------|---------------|
| **C-Suite / VP** | High-level KPIs, trends, exceptions | Strategic — 5-7 metrics, big cards |
| **Manager** | Team performance, targets, drill-down | Tactical — comparison charts, scorecards |
| **Analyst** | Detailed data, filters, export capability | Analytical — tables, matrices, many filters |
| **Operations** | Real-time status, alerts | Operational — gauges, status indicators |

### Principle 2: Information Hierarchy (F-Pattern / Z-Pattern)

Users scan screens in an **F-pattern** (left to right, top to bottom):

```
┌─────────────────────────────────────────┐
│ ★★★★★★★★★★★★★★★★★★★★ (top = most seen) │ ← KPIs, headline numbers
│ ★★★★★★★★★★★★                           │ ← Key charts, trends
│ ★★★★★★★★                               │ ← Supporting visuals
│ ★★★★                                   │ ← Details, tables
│ ★★                                     │ ← Least viewed area
└─────────────────────────────────────────┘
```

**Placement Rule:** Most important information → top-left. Least important → bottom-right.

### Principle 3: Less is More

| Guideline | Target |
|-----------|--------|
| **Visuals per page** | 5–8 maximum |
| **KPI cards** | 3–6 across the top |
| **Colors** | 2–4 primary colors |
| **Fonts** | 1–2 font families |
| **Pages** | 3–7 for a typical report |
| **Slicers** | 2–4 per page |

> Every visual should answer a question. If you can't state what question a visual answers, remove it.

### Principle 4: Consistency

| Element | Keep Consistent |
|---------|----------------|
| **Colors** | Same color = same meaning everywhere (Blue = Revenue, Green = Profit) |
| **Font sizes** | Same hierarchy on every page (Title 18pt, Subtitle 14pt, Body 10pt) |
| **Layout** | Same grid, same padding, same visual positions |
| **Slicer placement** | Always in the same spot (top or left sidebar) |
| **Number formatting** | Same decimals, same units (₹ Lakhs, %, whole numbers) |
| **Titles** | Same format: "Metric by Dimension" (e.g., "Revenue by Region") |

### Principle 5: Use White Space

- **Don't fill every pixel** — space helps the eye focus
- **10-15px gaps** between visuals
- **Consistent margins** from the page edges
- **Group related visuals** with a subtle background shape, separated from unrelated ones by space

### Principle 6: Choose the Right Visual

| Question Type | Best Visual | Avoid |
|--------------|-------------|-------|
| How much? (single number) | **Card** | Chart |
| Compare categories | **Bar Chart** | Pie chart (if >5 categories) |
| Show trend over time | **Line Chart** | Bar chart (loses time continuity) |
| Part of whole (≤5 items) | **Donut Chart** | Pie chart with 10+ slices |
| Geographic distribution | **Map** | Table of city names |
| Detailed lookup | **Table / Matrix** | Chart (loses precision) |
| Status / achievement | **Gauge / KPI** | Bar chart |
| Correlation | **Scatter Plot** | Line chart |

### Principle 7: Tell a Story

Arrange visuals to guide the viewer through a narrative:

```
1. WHAT happened?      → KPI cards (Revenue, Orders, Margin)
2. HOW is it trending?  → Line chart (Monthly trend)
3. WHERE is it strong?  → Map or bar chart (by Region)
4. WHY did it change?   → Drill-through to detail
5. WHAT should we do?   → Annotations, targets, recommendations
```

### Principle 8: Make It Interactive (But Not Overwhelming)

| Good Interactivity | Bad Interactivity |
|-------------------|-------------------|
| 3 slicers for key dimensions | 10 slicers covering every field |
| Drill-through to detail page | Drill-through on every visual |
| Cross-filtering between charts | Confusing filter interactions |
| Clear Reset button | No way to clear filters |
| Bookmarks for common views | 20 bookmarks with no organization |

### Principle 9: Label Everything Clearly

| Element | Good Label | Bad Label |
|---------|-----------|-----------|
| Chart title | "Monthly Revenue Trend (₹ Lakhs)" | "Chart 1" |
| Y-axis | "Revenue (₹)" | Default unlabeled |
| Slicer | "Select Region" | "Region" |
| Card | "Total Revenue" with subtitle "FY2024 YTD" | "42.3" (no context) |
| Tooltip | Shows 3 relevant metrics | Shows raw field names |

### Principle 10: Design for the Minimum Viable Insight

> The simplest dashboard that answers the key business question is the best dashboard.

- Start with 3–5 visuals that answer the core question
- Add more only when users explicitly request them
- Every addition should justify its canvas space

---

## 24.2 Color Theory for Dashboards

### Choosing a Color Palette

| Palette Type | Use When | Example |
|-------------|----------|---------|
| **Sequential** | One variable, low-to-high | Light blue → Dark blue (revenue intensity) |
| **Diverging** | Above/below a midpoint | Green ← Gray → Red (profit vs loss) |
| **Categorical** | Distinct categories | Blue, Orange, Teal, Purple (Regions) |
| **Brand** | Company reports | Company brand colors |

### Color Best Practices

| Rule | Detail |
|------|--------|
| **Max 4 main colors** | Plus gray for secondary elements |
| **Use gray for context** | Gray = "everything else" — draws attention to colored items |
| **Red = bad / alert** | Don't use red for a category unless it means "warning" |
| **Green = good / positive** | Don't use green for a category unless it means "on track" |
| **Colorblind-safe** | 8% of men are red-green colorblind — use blue/orange instead |
| **Consistent meaning** | If blue = North on Page 1, blue must = North on all pages |
| **Dark backgrounds** | Avoid — harder to read, harder to print, less professional |

### Recommended Color Combinations

**Corporate Professional:**
- Primary: #1E3A5F (Dark Blue)
- Secondary: #4A90D9 (Medium Blue)
- Accent: #F2C94C (Gold)
- Alert: #E74C3C (Red)
- Success: #27AE60 (Green)
- Neutral: #95A5A6 (Gray)

**Modern Clean:**
- Primary: #2D3436 (Charcoal)
- Secondary: #0984E3 (Bright Blue)
- Accent: #00B894 (Teal)
- Alert: #D63031 (Red)
- Neutral: #B2BEC3 (Light Gray)

---

## 24.3 Typography Guidelines

### Font Selection

| Use | Recommended Font | Size |
|-----|-----------------|------|
| **Report title** | Segoe UI Semibold | 18–24pt |
| **Page title** | Segoe UI Semibold | 14–16pt |
| **Visual titles** | Segoe UI Semibold | 11–13pt |
| **Body text** | Segoe UI | 9–11pt |
| **KPI values** | Segoe UI Bold | 28–36pt |
| **KPI labels** | Segoe UI Light | 9–11pt |
| **Axis labels** | Segoe UI | 8–10pt |

> **Segoe UI** is Power BI's default font and works well. Stick with one font family unless branding requires otherwise.

### Typography Rules
1. **Maximum 2 font sizes** per visual (title + data)
2. **Left-align text** (not center or right, except numbers)
3. **Right-align numbers** in tables (for decimal alignment)
4. **No ALL CAPS** for body text — only for short labels if needed
5. **Bold for emphasis** — not color, not italics, not underline

---

## 24.4 Common Dashboard Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| **Too many visuals** | Overwhelming, no focus | Limit to 5–8 per page |
| **3D charts** | Distort values, look unprofessional | Always use 2D |
| **Pie chart with 10+ slices** | Impossible to compare | Use a bar chart instead |
| **Rainbow colors** | No meaning, visual noise | Use 2–4 purposeful colors |
| **No labels or titles** | Users can't understand the data | Label everything |
| **Dark background** | Hard to read, unprintable | Use white or light gray |
| **Cluttered layout** | No white space, visuals overlap | Use grid alignment with spacing |
| **Inconsistent formatting** | Looks unprofessional | Apply a theme, use templates |
| **No context** | "42.3" — is that good or bad? | Add targets, benchmarks, YoY comparison |
| **Too many slicers** | Confusion, slow performance | 2–4 key slicers max |

---

## 24.5 Dashboard Templates by Industry

### Retail / E-Commerce
```
KPIs: Revenue, Orders, AOV, Conversion, Cart Abandonment
Charts: Revenue trend, Top products, Category breakdown, Geographic sales
Slicers: Date range, Product category, Channel (Online/Store)
```

### Finance
```
KPIs: Revenue, EBITDA, Net Income, Cash Flow, Debt Ratio
Charts: P&L waterfall, Revenue vs budget, Expense breakdown, Monthly trend
Slicers: Fiscal period, Business unit, Cost center
```

### HR / People Analytics
```
KPIs: Headcount, Attrition %, Avg Tenure, Open Positions, Time to Hire
Charts: Headcount trend, Attrition by department, Diversity breakdown
Slicers: Department, Location, Job level
```

### Operations / Supply Chain
```
KPIs: On-time delivery %, Inventory turns, Order fulfillment, Defect rate
Charts: Delivery trend, Inventory levels, Supplier performance
Slicers: Warehouse, Product line, Date range
```

---

## 24.6 Accessibility Best Practices

| Practice | Why | How |
|----------|-----|-----|
| **Alt text on every visual** | Screen reader support | Select visual → Format → General → Alt Text |
| **Sufficient color contrast** | Readability for low vision | Dark text on light background (4.5:1 ratio) |
| **Don't rely on color alone** | Colorblind users | Use patterns, icons, labels in addition to color |
| **Tab order** | Keyboard navigation | View → Selection Pane → Tab Order |
| **Meaningful visual titles** | Screen reader announces titles | Not "Chart 1" — use "Revenue by Category" |
| **Data labels** | Values visible without hover | Turn on data labels for key visuals |

---

## 🔧 Hands-On Activity: Dashboard Review & Redesign

**Duration:** 25 minutes

### Part 1 — Review Your Existing Dashboard (10 min)

Open your Sales Dashboard and evaluate against the checklist:

**Design Score Card:**
| Criterion | Score (1-5) | Notes |
|-----------|------------|-------|
| Clear business question answered? | | |
| KPIs at the top? | | |
| 5–8 visuals per page? | | |
| Consistent colors? | | |
| Consistent fonts and sizes? | | |
| White space between visuals? | | |
| All visuals titled descriptively? | | |
| Slicers clearly labeled? | | |
| Numbers formatted with units? | | |
| Interactive (slicers, drill-through)? | | |

### Part 2 — Redesign (15 min)

Based on your review:
1. **Remove** any unnecessary visuals (does each one answer a question?)
2. **Apply a theme** for consistent colors
3. **Add/improve titles** on all visuals
4. **Align visuals** to grid (View → Snap to Grid)
5. **Add white space** between visual groups
6. **Add alt text** to at least 3 key visuals
7. **Set tab order** in the Selection Pane
8. **Format numbers** consistently (Currency with ₹, Percentages, Whole Numbers)
9. Save

---

## Session 24 — Key Takeaways

1. **Start with the business question** — the dashboard should drive a decision
2. **Less is more** — 5-8 visuals, 2-4 colors, 2-4 slicers
3. **Consistency** in colors, fonts, layout, and number formatting builds trust
4. **White space** is not wasted space — it improves readability
5. **Accessibility** (alt text, contrast, tab order) ensures everyone can use the dashboard

---

## Preparation for Session 25
- Review all techniques learned: Bookmarks, conditional formatting, RLS, design principles
- Have your best dashboard file open and ready
- Think about: What would an executive dashboard for your company look like?

---

*Session 24 of 30 | Module 5: Advanced Reporting*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
