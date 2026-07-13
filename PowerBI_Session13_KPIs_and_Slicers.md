# Session 13 — KPIs & Slicers
## Module 3: Data Visualization | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Interactive Slicers and KPI Layouts

---

## Learning Objectives
By the end of this session, you will be able to:
1. Build and configure Slicers for interactive filtering
2. Understand Slicer types (List, Dropdown, Between, Relative Date)
3. Sync slicers across multiple pages
4. Design effective KPI sections using Cards and Slicers
5. Control slicer-visual interactions

---

## 13.1 What is a Slicer?

A **Slicer** is a visual filter control placed directly on the report canvas. Users click slicer values to filter all other visuals on the page.

### Slicer vs Filter Pane

| Feature | Slicer | Filter Pane |
|---------|--------|-------------|
| **Visibility** | On the canvas — users see and interact | Side panel — often hidden or overlooked |
| **User-friendly** | Very — click/tap to filter | Less intuitive for business users |
| **Multiple selections** | Ctrl+Click or Select All | Checkbox list |
| **Space usage** | Takes canvas space | No canvas space |
| **Best for** | Key filters users need frequently | Background or advanced filters |

---

## 13.2 Slicer Types

### List Slicer (Default)

Shows all values as a vertical list with checkboxes.

**Best for:** Categories with 5–15 values (Region, Segment, Category)

**Building:**
1. Click **Slicer** in Visualizations
2. Drag a field to the **Field** well (e.g., Region)
3. Default: vertical list with checkboxes

### Dropdown Slicer

Compact — shows one value with a dropdown arrow.

**Best for:** Saving space when you have many categories

**How to switch:** Format → Slicer Settings → Style → **Dropdown**

### Tile / Button Slicer

Values displayed as clickable buttons/tiles in a horizontal row.

**Best for:** 3–6 categories displayed prominently (Year, Quarter)

**How to switch:** Format → Slicer Settings → Style → **Tile**

### Date Slicers

| Type | Use |
|------|-----|
| **Between** | Select a date range (From date → To date) |
| **Before** | All dates before a selected date |
| **After** | All dates after a selected date |
| **List** | Individual date values (rare — too many items) |
| **Dropdown** | Date dropdown (use for Year, Quarter, Month instead) |
| **Relative Date** | "Last 30 days", "This month", "Last quarter" — dynamic |

### Relative Date Slicer

**How to enable:**
1. Add a Date field to a Slicer
2. Click the dropdown arrow on the slicer header → **Relative Date**
3. Configure: "Last 30 Days", "This Quarter", "Last 12 Months", etc.

**Options:**
| Setting | Values |
|---------|--------|
| **Show items from** | Last / This / Next |
| **Period** | Days, Weeks, Months, Quarters, Years |
| **Count** | Number of periods (e.g., Last 3 Months) |
| **Anchor** | Today (dynamic) or a fixed date |

> **Best Practice:** Use **Relative Date** slicers for live dashboards — they auto-update without manual filter changes.

### Numeric Range Slicer

For numeric fields, the slicer becomes a slider with min/max handles.

**Best for:** Filtering by revenue range, age range, price range

---

## 13.3 Slicer Configuration

### Single vs Multi-Select

| Mode | Behavior | How to Set |
|------|----------|-----------|
| **Multi-select** (default) | Ctrl+Click to select multiple | Default behavior |
| **Single select** | Only one value at a time | Format → Selection → Single Select → On |

### Select All Option

- Format → Selection → **Show "Select all" option** → On
- Adds a "Select all" checkbox at the top of the list

### Search Box

- Format → Slicer Settings → **Search** → On
- Adds a search bar to the slicer — essential for long lists

### Slicer Header

- Format → Slicer Header → On/Off
- Customize title text (e.g., "Select Region" instead of just "Region")

---

## 13.4 Syncing Slicers Across Pages

### The Problem
By default, a slicer only affects the page it's on. Users expect selecting "North" on Page 1 to persist when they navigate to Page 2.

### How to Sync Slicers

1. Select the slicer
2. **View** tab → **Sync Slicers** (opens the Sync Slicers pane)
3. For each page, set two options:

| Column | Meaning |
|--------|---------|
| **Sync** (link icon) | The slicer selection carries to this page |
| **Visible** (eye icon) | The slicer is visible on this page |

### Common Sync Patterns

| Pattern | Sync | Visible | Use Case |
|---------|------|---------|----------|
| **Sync + Visible** | ✅ | ✅ | Slicer appears and works on this page |
| **Sync + Hidden** | ✅ | ❌ | Selection applies but slicer not shown (clean layout) |
| **No Sync** | ❌ | ❌ | Page is independent of this slicer |

### Sync Slicer Groups

- You can create **Slicer Groups** to sync different slicers to different page sets
- Advanced → named slicer groups
- Useful for complex reports with different filter needs per section

---

## 13.5 Slicer-Visual Interactions

### Controlling Which Visuals a Slicer Affects

By default, a slicer filters ALL visuals on the page. You can change this:

1. Select the Slicer
2. **Format** tab in Ribbon → **Edit Interactions**
3. Icons appear on each visual:
   - 🔍 **Filter** — slicer filters this visual (default)
   - 🚫 **None** — slicer does NOT affect this visual

### Common Use Case
- A "Year" slicer should filter all charts
- But a "Grand Total Revenue" card should always show ALL-TIME total
- Set the card interaction to **None** for the Year slicer

---

## 13.6 KPI Layout Design Patterns

### Pattern 1: KPI Bar + Slicers

```
┌──────────────────────────────────────────────────────────────┐
│ [Region ▼] [Year ▼] [Category ▼]          ← Slicer row     │
├──────────┬──────────┬──────────┬──────────┬──────────────────┤
│ ₹42.3 Cr │  12,500  │  ₹3,384  │  18.5%   │ ← KPI Cards    │
│ Revenue  │ Orders   │ Avg Order│ Margin   │                  │
├──────────┴──────────┴──────────┴──────────┴──────────────────┤
│                                                              │
│           Charts and detailed visuals below                  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### Pattern 2: Left Sidebar Slicers

```
┌──────────┬───────────────────────────────────────────┐
│          │  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐     │
│ Region   │  │ Rev  │ │Orders│ │ AOV  │ │Margin│     │
│ ☐ North  │  └──────┘ └──────┘ └──────┘ └──────┘     │
│ ☐ South  │                                           │
│ ☐ East   │  ┌─────────────────┐ ┌─────────────────┐  │
│ ☐ West   │  │                 │ │                 │  │
│          │  │   Chart 1       │ │   Chart 2       │  │
│ Year     │  │                 │ │                 │  │
│ ☐ 2023   │  └─────────────────┘ └─────────────────┘  │
│ ☐ 2024   │                                           │
│          │  ┌─────────────────────────────────────┐   │
│ Category │  │            Table / Matrix            │   │
│ [▼ All]  │  └─────────────────────────────────────┘   │
└──────────┴───────────────────────────────────────────┘
```

### Pattern 3: Top Tile Slicers (Buttons)

```
┌──────────────────────────────────────────────────────┐
│  [2022] [2023] [2024]    ← Year tiles (button style) │
│  [All] [North] [South] [East] [West]   ← Region     │
├──────────────────────────────────────────────────────┤
│  Dashboard content below                             │
└──────────────────────────────────────────────────────┘
```

---

## 13.7 Slicer Best Practices

| Practice | Why |
|----------|-----|
| **Limit to 3–5 slicers per page** | Too many = overwhelming and confusing |
| **Use Dropdown for long lists** | Saves canvas space |
| **Use Tiles for 3–6 items** | Quick visual selection |
| **Always add a "Select All" option** | Users need a way to reset |
| **Sync key slicers across pages** | Consistent filtering experience |
| **Use Relative Date for live dashboards** | Auto-updates without manual changes |
| **Add search for 15+ items** | Users can type to find values |
| **Position slicers consistently** | Same location on every page (top or left sidebar) |
| **Label slicers clearly** | "Select Region" not just "Region" |

---

## 🔧 Hands-On Activity: Interactive Slicer Dashboard

**Duration:** 25 minutes

### Tasks

**Part 1 — Build Slicers (10 min)**
1. Create a new page called "Interactive Dashboard"
2. Add 3 Slicers:
   - **Region** (List style, with Select All enabled)
   - **Year** (Tile/Button style, single-select)
   - **Product Category** (Dropdown style, with Search enabled)
3. Add 4 KPI Cards: Revenue, Orders, Avg Order Value, Profit Margin
4. Add 2 charts below: Column chart (Category × Revenue) + Line chart (Month × Revenue)

**Part 2 — Configure Interactions (5 min)**
5. Test: Click different slicer values — do all visuals respond?
6. Set the "Total Revenue" card to NOT be affected by the Year slicer (show all-time total)
7. Verify: Year slicer filters charts but NOT the all-time total card

**Part 3 — Sync Slicers (10 min)**
8. Create a second page "Regional Detail"
9. Add a Matrix: Region × Month × Revenue
10. View → Sync Slicers → Sync the Region slicer to both pages
11. Test: Select "North" on Page 1 → navigate to Page 2 → verify filter persists
12. Save

---

## Session 13 — Key Takeaways

1. **Slicers** are visual filter controls — more user-friendly than the Filter pane
2. **Types:** List, Dropdown, Tile, Date Range, Relative Date, Numeric Range
3. **Sync Slicers** across pages for a consistent filtering experience
4. **Edit Interactions** to control which visuals a slicer affects
5. **Design patterns:** KPI bar + slicers at top, or slicer sidebar on left

---

## Preparation for Session 14
- Review: What is conditional formatting in Excel?
- Think about: How would you enable users to navigate between dashboard pages?
- Explore: What is a "Drill-through" in Power BI?

---

*Session 13 of 30 | Module 3: Data Visualization*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
