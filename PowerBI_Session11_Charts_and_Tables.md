# Session 11 — Charts & Tables
## Module 3: Data Visualization | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Bar, Column, Line, Pie, and Table Visuals

---

## Learning Objectives
By the end of this session, you will be able to:
1. Choose the right chart type for your data and business question
2. Build bar, column, line, pie/donut, and table visuals
3. Configure field wells (Axis, Values, Legend, Tooltips)
4. Apply basic formatting (titles, labels, colors)
5. Understand when NOT to use certain chart types

---

## 11.1 Choosing the Right Visual

### The Chart Selection Framework

| Business Question | Best Visual | Why |
|------------------|-------------|-----|
| Compare categories (Sales by Region) | **Bar / Column Chart** | Easy comparison of discrete values |
| Show trends over time | **Line Chart** | Continuous data, trends visible |
| Show part of whole (Market Share) | **Pie / Donut Chart** | Proportional breakdown |
| Show detailed data | **Table / Matrix** | Precise numbers, multiple columns |
| Show ranking (Top 10 products) | **Horizontal Bar Chart** | Sorted comparison |
| Show two measures together | **Combo Chart (Bar + Line)** | Dual-axis comparison |
| Show distribution | **Histogram / Scatter** | Spread of values |
| Show geographic data | **Map** | Location-based (Session 12) |
| Show a single KPI | **Card** | One big number (Session 13) |

### The "5-Second Rule"
> A good visual communicates its key message within 5 seconds. If the viewer needs longer, the visual needs improvement.

---

## 11.2 Bar and Column Charts

### Bar Chart (Horizontal) vs Column Chart (Vertical)

| Type | Best For | Orientation |
|------|----------|-------------|
| **Column Chart** | Comparing across categories, time series | Vertical bars |
| **Bar Chart** | Ranked lists, long category names | Horizontal bars |

### Variants

| Visual | Use When |
|--------|----------|
| **Clustered Column** | Compare multiple series side by side (Revenue vs Cost by Region) |
| **Stacked Column** | Show total + breakdown (Revenue by Region, colored by Product) |
| **100% Stacked Column** | Show proportional breakdown (% of revenue per product by region) |
| **Clustered Bar** | Same as Clustered Column but horizontal |
| **Stacked Bar** | Same as Stacked Column but horizontal |

### Building a Column Chart

**Steps:**
1. Click the **Clustered Column Chart** icon in Visualizations pane
2. Drag a **category** to the **X-axis** well (e.g., Product Category)
3. Drag a **measure** to the **Y-axis / Values** well (e.g., Revenue)
4. Optionally drag a field to **Legend** for color grouping (e.g., Region)

### Field Wells for Bar/Column Charts

| Well | Purpose | Example |
|------|---------|---------|
| **X-axis (Axis)** | Categories on the horizontal axis | Product Category, Region |
| **Y-axis (Values)** | Numbers to display (auto-aggregated) | SUM of Revenue |
| **Legend** | Color grouping | Region, Segment |
| **Tooltips** | Extra info shown on hover | Profit Margin, Order Count |
| **Small Multiples** | Grid of mini-charts | One chart per Year |

### Formatting Tips
- **Sort:** Click the "..." menu on the visual → Sort by → choose field and order
- **Data Labels:** Format pane → Data Labels → On (shows values on bars)
- **Title:** Format pane → Title → customize text, font, size
- **Colors:** Format pane → Data Colors → customize per category

---

## 11.3 Line Charts

### When to Use Line Charts
- **Time-series data** — Revenue over months, users over weeks
- **Trend identification** — is it going up, down, or flat?
- **Comparing trends** — multiple lines for different categories

### Variants

| Visual | Use When |
|--------|----------|
| **Line Chart** | Single or multiple trend lines |
| **Area Chart** | Trend with emphasis on volume (shaded area) |
| **Stacked Area** | Show cumulative total over time |
| **Line and Clustered Column** | Combo: bars for one measure, line for another |

### Building a Line Chart

1. Click **Line Chart** in Visualizations
2. Drag a **Date field** to **X-axis** (Power BI auto-creates hierarchy: Year > Quarter > Month)
3. Drag a **measure** to **Y-axis** (e.g., Revenue)
4. Optionally drag a field to **Legend** (e.g., Region → multiple lines)

### Line Chart Tips

| Tip | How |
|-----|-----|
| **Remove date hierarchy** | Click the "↕" icon on the axis to switch between hierarchy and continuous |
| **Add markers** | Format → Markers → On (dots on data points) |
| **Add trend line** | Format → Analytics → Trend Line → On |
| **Add constant line** | Format → Analytics → Constant Line → Value (e.g., target = 50000) |
| **Limit to 5 lines max** | More than 5 lines = unreadable; use Small Multiples instead |

---

## 11.4 Pie and Donut Charts

### When to Use (and When NOT to)

**Use When:**
- Showing **part of whole** (market share, budget allocation)
- **3–5 categories maximum**
- **Proportions** are the key message

**Do NOT Use When:**
- More than 5–6 categories (becomes unreadable)
- Comparing precise values (bar chart is better)
- Categories are similar in size (hard to distinguish)
- Showing trends over time (line chart instead)

### Pie vs Donut

| Type | Difference |
|------|-----------|
| **Pie** | Solid circle — classic |
| **Donut** | Hollow center — can show a KPI in the middle |

### Building a Donut Chart

1. Click **Donut Chart** in Visualizations
2. Drag category to **Legend** well (e.g., Product Category)
3. Drag measure to **Values** well (e.g., Revenue)
4. Format → Detail Labels → Show: Category + Percentage

### Pro Tip: The Bar Chart Alternative
> Whenever you're tempted to use a Pie chart, ask: "Would a sorted Bar chart communicate this better?" Usually, yes.

---

## 11.5 Tables and Matrices

### Table Visual

**What it is:** A flat grid of rows and columns — like an Excel spreadsheet.

**When to use:**
- Users need to see **exact numbers**
- Detailed line-item data
- Export-ready data views
- Multiple columns of different types

**Building a Table:**
1. Click **Table** in Visualizations
2. Drag fields to **Columns** well: Customer Name, Product, Revenue, Quantity

### Matrix Visual

**What it is:** A pivot table — rows, columns, and values with subtotals.

**When to use:**
- Cross-tabulation (Region × Product × Revenue)
- Hierarchical drill-down (Year → Quarter → Month)
- Comparing across two dimensions

**Building a Matrix:**
1. Click **Matrix** in Visualizations
2. Drag to **Rows**: Product Category
3. Drag to **Columns**: Year (or Quarter)
4. Drag to **Values**: Sum of Revenue

### Table vs Matrix

| Feature | Table | Matrix |
|---------|-------|--------|
| **Layout** | Flat grid | Pivot (rows × columns) |
| **Subtotals** | No | Yes (row + column totals) |
| **Drill-down** | No | Yes (hierarchies) |
| **Best for** | Detail lists | Cross-tabulation, summaries |

### Formatting Tables/Matrices

| Setting | Location | Effect |
|---------|----------|--------|
| **Column width** | Drag column borders | Resize |
| **Conditional formatting** | Format → Cell Elements → Background Color | Heat map style |
| **Row subtotals** | Format → Row Subtotals → On/Off | Show/hide totals |
| **Column subtotals** | Format → Column Subtotals → On/Off | Show/hide |
| **Stepped layout** | Format → Row Headers → Stepped Layout | Hierarchical indent |
| **Word wrap** | Format → Column Headers → Word Wrap | Wrap long headers |
| **Data bars** | Format → Cell Elements → Data Bars | In-cell bar charts |
| **URL links** | Set column as "Web URL" category | Clickable links |

---

## 11.6 Combo Charts

### Line and Clustered Column Chart

**When to use:** Compare two measures with different scales on the same visual.

**Example:** Revenue (bars, left axis) + Profit Margin % (line, right axis)

**Building:**
1. Click **Line and Clustered Column Chart**
2. Drag category to **X-axis** (e.g., Month)
3. Drag first measure to **Column Values** (e.g., Revenue)
4. Drag second measure to **Line Values** (e.g., Profit Margin)

**Tip:** Power BI auto-creates a dual Y-axis. Format each axis independently for appropriate scales.

---

## 11.7 Visual Interactions

### How Visuals Interact
- **Click a bar** in a bar chart → other visuals on the page **filter** to that selection
- This is called **cross-filtering** and is ON by default

### Interaction Types

| Type | Behavior | When to Use |
|------|----------|-------------|
| **Filter** | Other visual shows only matching data | Default for most visuals |
| **Highlight** | Other visual dims non-matching, highlights matching | Shows context within whole |
| **None** | No interaction | When a visual should be independent |

### Configuring Interactions
1. Select a visual → **Format** tab in Ribbon → **Edit Interactions**
2. Icons appear on other visuals: Filter 🔍 | Highlight 📊 | None 🚫
3. Click the desired interaction for each visual pair

---

## 🔧 Hands-On Activity: Build Core Visuals

**Duration:** 25 minutes

### Setup
Use your validated Star Schema model (Sales + Products + Customers + Date).

### Tasks

1. **Page 1 — "Sales Overview"**
   - **Clustered Column Chart:** Product Category (X-axis) vs Sum of Revenue (Y-axis)
   - **Line Chart:** Date (X-axis) vs Sum of Revenue (Y-axis), Legend = Region
   - **Donut Chart:** Customer Segment (Legend) vs Sum of Revenue (Values)
   - **Table:** Top 10 products by Revenue (with Product Name, Category, Revenue, Quantity)
   - Sort the column chart descending by Revenue
   - Add Data Labels to the column chart

2. **Page 2 — "Detailed Analysis"**
   - **Matrix:** Rows = Product Category, Columns = Year, Values = Sum of Revenue
   - Enable Row Subtotals and Column Subtotals
   - **Combo Chart:** Month (X-axis), Revenue (Column), Quantity (Line)
   - Add a Trend Line to the line portion

3. **Test cross-filtering:** Click a bar in the column chart — verify other visuals respond

4. Save the file

---

## Session 11 — Key Takeaways

1. **Choose visuals based on the business question** — not aesthetics
2. **Bar/Column:** compare categories | **Line:** show trends | **Pie/Donut:** part of whole (≤5 categories)
3. **Tables** for exact numbers; **Matrices** for cross-tabulation with subtotals
4. **Combo charts** compare two measures with different scales
5. **Cross-filtering** is automatic — clicking one visual filters others on the page

---

## Preparation for Session 12
- Think about: Do you have geographic data (City, State, Country, Lat/Long)?
- Review: What are Card visuals used for?

---

*Session 11 of 30 | Module 3: Data Visualization*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
