# Session 14 — Formatting & Drill-Through
## Module 3: Data Visualization | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Apply Formatting, Build Drill-Through Pages

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply consistent formatting to visuals (colors, fonts, labels, titles)
2. Use Themes for report-wide styling
3. Build Drill-through pages for detail exploration
4. Implement Drill-down hierarchies within visuals
5. Add Tooltips pages for rich hover information

---

## 14.1 Visual Formatting Fundamentals

### The Format Pane

Select any visual → click the **Format** icon (paint roller 🎨) in the Visualizations pane.

### Key Format Categories

| Category | What You Control |
|----------|-----------------|
| **General** | Size, position, padding, border, shadow, background |
| **Title** | Title text, font, size, color, alignment |
| **Data Labels** | Show/hide values on bars/points, font, position |
| **Data Colors** | Color of each data series or category |
| **Axis** | Axis titles, font, range, gridlines |
| **Legend** | Position (top/bottom/left/right), font, colors |
| **Gridlines** | Show/hide horizontal and vertical gridlines |
| **Plot Area** | Background color of the chart area |
| **Border** | Visual border color, width, radius |
| **Shadow** | Drop shadow effect |
| **Header Icons** | Show/hide drill-down, filter, focus mode icons |

---

## 14.2 Best Formatting Practices

### Colors

| Practice | Why |
|----------|-----|
| Use **2–4 colors** maximum per visual | Too many colors = visual noise |
| Use **sequential colors** for ranked data | Dark → light for high → low |
| Use **diverging colors** for above/below target | Green (above) → Red (below) |
| **Consistent colors** across pages | "North" should be the same color everywhere |
| Avoid red/green only — consider colorblind users | Use blue/orange as alternative |

### Font Sizing Guide

| Element | Recommended Size |
|---------|-----------------|
| **Report Title** | 18–24pt, Bold |
| **Section Headers** | 14–16pt, Bold |
| **Card Values (KPIs)** | 28–36pt, Bold |
| **Card Labels** | 10–12pt, Regular |
| **Chart Titles** | 12–14pt, Bold |
| **Axis Labels** | 9–11pt, Regular |
| **Data Labels** | 8–10pt, Regular |
| **Slicer Text** | 10–12pt, Regular |

### Title Best Practices

| Bad Title | Good Title | Why |
|-----------|-----------|-----|
| "Revenue" | "Monthly Revenue (₹ Lakhs)" | Units and context |
| "Chart 1" | "Revenue by Product Category" | Descriptive |
| "Sales Data" | "Top 10 Products by Revenue — FY2024" | Specific, actionable |

---

## 14.3 Themes

### What Are Themes?

A **Theme** applies consistent colors, fonts, and formatting across the entire report in one click.

### Applying a Built-In Theme

1. **View** tab → **Themes** dropdown
2. Browse built-in themes (Classic, Executive, Innovation, etc.)
3. Click to apply — all visuals update immediately

### Custom Themes (JSON)

Create a `.json` file with custom brand colors and fonts:

```json
{
  "name": "Company Brand Theme",
  "dataColors": ["#1E3A5F", "#4A90D9", "#7BC4C4", "#F2C94C", "#E74C3C", "#95A5A6"],
  "background": "#FFFFFF",
  "foreground": "#333333",
  "tableAccent": "#1E3A5F",
  "textClasses": {
    "callout": { "fontSize": 28, "fontFace": "Segoe UI" },
    "title": { "fontSize": 14, "fontFace": "Segoe UI Semibold" },
    "header": { "fontSize": 12, "fontFace": "Segoe UI" },
    "label": { "fontSize": 10, "fontFace": "Segoe UI" }
  }
}
```

**Applying:** View → Themes → Browse for themes → select the `.json` file

### Theme Benefits

- **Brand consistency** across all reports in the organization
- **One-click** application — no manual formatting per visual
- **Shareable** — distribute the `.json` file to all report authors
- **Overridable** — individual visuals can still be customized after applying

---

## 14.4 Drill-Down (Within a Visual)

### What is Drill-Down?

**Drill-down** lets users explore data at progressively deeper levels within the same visual — from Year → Quarter → Month → Day.

### How It Works

A date field placed on the axis creates an automatic hierarchy:
```
Year → Quarter → Month → Day
```

A geographic field:
```
Country → State → City
```

A product field:
```
Category → Sub-Category → Product Name
```

### Drill-Down Controls (Visual Header Icons)

| Icon | Name | Behavior |
|------|------|----------|
| ↓ Single arrow down | **Drill Down** | Click a specific bar/point → go one level deeper for THAT item only |
| ⇊ Double arrow down | **Go to Next Level** | All items go one level deeper (Year → Quarter for all) |
| ↑ Arrow up | **Drill Up** | Go back up one level |
| ⊞ Expand All | **Expand All** | Show all levels at once (Year AND Quarter) |

### Enabling Drill-Down

1. Create a chart with a **hierarchy** on the axis
   - Drag Year, Quarter, Month to the X-axis (they stack as hierarchy)
   - OR: Drag a Date field — Power BI auto-creates the hierarchy
2. The drill-down icons appear in the visual header automatically
3. Users click icons or click directly on bars/points to drill

### Custom Hierarchies

1. In the **Fields** pane: drag one field onto another to create a hierarchy
2. Example: Drag "Sub-Category" onto "Category" → creates Category > Sub-Category hierarchy
3. OR: Right-click a field → **New Hierarchy** → drag other fields into it

---

## 14.5 Drill-Through (Across Pages)

### What is Drill-Through?

**Drill-through** navigates the user from a summary page to a **detail page** filtered to their selection. Like clicking on "Electronics" in a chart and landing on a page with full Electronics details.

### How Drill-Through Works

```
Page 1: Sales Overview                    Page 2: Product Detail
┌────────────────────────────┐           ┌────────────────────────────┐
│                            │           │  ← Back Button            │
│  [Bar: Revenue by Category]│           │  Category: Electronics    │
│                            │  Right-   │                            │
│  User right-clicks         │  Click    │  [Detailed table]          │
│  "Electronics" bar         │ ─────────►│  [Product-level charts]    │
│  → Drill through           │           │  [KPIs for Electronics]    │
│    → Product Detail        │           │                            │
│                            │           │  (All filtered to          │
│                            │           │   Electronics only)        │
└────────────────────────────┘           └────────────────────────────┘
```

### Building a Drill-Through Page

**Step 1: Create the detail page**
1. Add a new page → rename to "Product Detail"
2. Build the detailed visuals you want (tables, charts, cards)

**Step 2: Set the drill-through filter**
1. On the detail page, drag a field to the **Drill-through** filter well (in the Filters pane or Visualizations pane)
2. Example: Drag "Product Category" to Drill-through
3. Power BI auto-adds a **Back button** to the page

**Step 3: Test**
1. Go to the summary page
2. Right-click a data point (e.g., a bar for "Electronics")
3. Select **Drill through → Product Detail**
4. The detail page opens, filtered to "Electronics"
5. Click the **Back button** to return

### Drill-Through Best Practices

| Practice | Why |
|----------|-----|
| **Always have a Back button** | Users need to return to the summary |
| **Keep cross-report drill-through OFF** unless needed | Can confuse users |
| **Name detail pages clearly** | "Product Detail", "Customer Detail" |
| **Show the filter context** on the detail page | Add a Card showing the selected category |
| **Hide drill-through pages** from navigation if needed | Right-click tab → Hide Page |

---

## 14.6 Tooltip Pages

### What is a Tooltip Page?

A **custom Tooltip** is a mini-report page that appears when users hover over a data point — replacing the default tooltip.

### Building a Tooltip Page

**Step 1: Create the page**
1. Add a new page → rename to "Revenue Tooltip"
2. **Format the page:** Page Information → **Tooltip → On**
3. Page Size → **Tooltip** (auto-sizes to tooltip dimensions: 320×240 px)

**Step 2: Design the tooltip content**
- Add small visuals: Card, small chart, text
- Keep it simple — it's a hover popup, not a full page
- Example: Card showing Revenue + a mini bar chart of monthly trend

**Step 3: Assign to a visual**
1. Select the visual that should show this tooltip (e.g., a bar chart)
2. Format → Tooltip → **Type: Report Page** → **Page: Revenue Tooltip**

**Step 4: Test**
- Hover over a bar/point → the custom tooltip appears instead of the default

### Tooltip Tips
- Keep tooltip pages **small and simple** — 2–3 visuals max
- Show **context-specific** information not visible in the main chart
- Use for: monthly trends, breakdowns, comparison data, images

---

## 14.7 Conditional Formatting (Preview)

A quick preview — covered in depth in Session 22:

| Type | Effect | Example |
|------|--------|---------|
| **Background Color** | Cell/bar color based on value | Green for high revenue, red for low |
| **Font Color** | Text color based on value | Red text for negative values |
| **Data Bars** | In-cell bar charts | Bar length = value magnitude |
| **Icons** | Status icons (✅❌⚠️) | Checkmark for above target |
| **Web URL** | Clickable links | Link to detailed report |

---

## 🔧 Hands-On Activity: Formatting and Drill-Through

**Duration:** 25 minutes

### Part 1 — Formatting (10 min)
1. Apply a **Theme** to your report (View → Themes → choose one)
2. Customize one visual:
   - Change title text and font size
   - Add data labels
   - Change data colors to match a brand palette
   - Add a border and subtle shadow
3. Ensure consistent font sizes across all visuals

### Part 2 — Drill-Through (10 min)
4. Create a new page: **"Product Detail"**
5. Add visuals: Table (Product, Revenue, Qty), Line Chart (Monthly Revenue), 2 Cards
6. Drag "Product Category" to the **Drill-through** well
7. Go to the summary page → right-click a category bar → Drill through → Product Detail
8. Verify the Back button works

### Part 3 — Tooltip Page (5 min)
9. Create a new page → set as Tooltip page (Page Format → Tooltip → On)
10. Add a Card (Revenue) and a small bar chart (Revenue by Month)
11. Assign this tooltip to your main bar chart
12. Hover over a bar → verify custom tooltip appears
13. Save

---

## Session 14 — Key Takeaways

1. **Format pane** controls every visual aspect — titles, colors, labels, borders
2. **Themes** apply consistent styling across the entire report in one click
3. **Drill-down** explores data at deeper levels WITHIN a visual (Year → Month)
4. **Drill-through** navigates to a DETAIL PAGE filtered to the selected value
5. **Tooltip pages** show rich hover information — mini-reports on hover

---

## Preparation for Session 15
- Review your dashboard: Does it answer a clear business question?
- Think about: What layout would a CEO or VP want to see?
- Explore: What makes a dashboard "good" vs "cluttered"?

---

*Session 14 of 30 | Module 3: Data Visualization*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
