# Session 21 — Bookmarks & Tooltips
## Module 5: Advanced Reporting | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Bookmark Navigation and Custom Tooltip Pages

---

## Learning Objectives
By the end of this session, you will be able to:
1. Create and manage Bookmarks to save report states
2. Build toggle views using Bookmarks + Buttons (e.g., Chart ↔ Table)
3. Create custom Tooltip report pages for rich hover information
4. Use the Selection Pane to show/hide visuals
5. Build a Bookmark-based tab navigation system

---

## 21.1 What Are Bookmarks?

A **Bookmark** captures and saves the current state of a report page, including:
- Which visuals are **visible or hidden**
- Current **filter and slicer** selections
- **Drill** state of visuals
- **Spotlight** or **focus** mode

Users can switch between bookmarks to change what they see — like saved views.

### Bookmark Use Cases

| Use Case | How |
|----------|-----|
| **Toggle Chart ↔ Table** | Two bookmarks: one shows chart (table hidden), one shows table (chart hidden) |
| **Show/Hide detail section** | Bookmark with detail panel visible vs hidden |
| **Reset filters** | Bookmark with all slicers cleared |
| **Storytelling / Presentation** | Series of bookmarks as a guided walkthrough |
| **Tab navigation** | Multiple bookmarks simulating tab-like pages on a single page |
| **Before/After comparison** | Two bookmark states showing different filter scenarios |

---

## 21.2 Creating Bookmarks

### Step-by-Step

1. **View** tab → **Bookmarks Pane** (opens on the right)
2. Set up the page exactly as you want it (filters, visible/hidden visuals)
3. Click **Add** in the Bookmarks pane
4. Rename the bookmark descriptively (e.g., "Chart View", "Table View")
5. Repeat for each state

### Bookmark Settings

Right-click a bookmark → **Update** or configure:

| Setting | Options | Default |
|---------|---------|---------|
| **Data** | Captures current filter/slicer state | On |
| **Display** | Captures visual visibility (show/hide) | On |
| **Current Page** | Captures which page is active | On |
| **All Visuals** | Applies to all visuals or selected visuals only | All Visuals |

> **Tip:** For toggle views (Chart ↔ Table), uncheck **Data** so the bookmark only controls visibility, not filters.

---

## 21.3 The Selection Pane

### What is the Selection Pane?

The **Selection Pane** lists every visual on the current page and lets you:
- **Show/Hide** visuals (eye icon 👁️)
- **Rename** visuals for easier management
- **Reorder** visual layers (front/back)
- **Lock** visuals to prevent accidental moves

### Opening the Selection Pane

- **View** tab → **Selection Pane**

### Selection Pane Operations

| Action | How |
|--------|-----|
| **Hide a visual** | Click the eye icon next to it (toggles visibility) |
| **Show a visual** | Click the eye icon again |
| **Rename** | Double-click the visual name |
| **Reorder** | Drag up/down (top = front, bottom = back) |
| **Tab order** | Set the tab/accessibility reading order |

### Naming Visuals (Best Practice)

| Default Name | Better Name |
|-------------|-------------|
| "Clustered Column Chart" | "Revenue by Category (Bar)" |
| "Card" | "KPI - Total Revenue" |
| "Slicer" | "Filter - Region" |
| "Table" | "Product Detail Table" |

> **Naming visuals** makes Bookmarks, Selection Pane, and Performance Analyzer much easier to use.

---

## 21.4 Building a Chart ↔ Table Toggle

### The Pattern

Two overlapping visuals (same size, same position) — one chart, one table. Use Bookmarks to switch between them.

### Step-by-Step

**Step 1: Create both visuals**
1. Create a **Bar Chart** (Revenue by Category)
2. Create a **Table** (Category, Revenue, Orders, Margin) — same data, different view
3. Position the Table exactly on top of the Bar Chart (same size and location)

**Step 2: Create Bookmarks**
4. Open **Selection Pane** — hide the Table (click eye icon) → only Chart visible
5. Open **Bookmarks Pane** → Add → rename to "Chart View"
6. Right-click bookmark → uncheck **Data** (we only want display changes)
7. In Selection Pane — hide Chart, show Table → only Table visible
8. Add another bookmark → rename to "Table View"
9. Right-click → uncheck **Data**

**Step 3: Create Toggle Buttons**
10. Insert → **Buttons** → Blank (or use icons/shapes)
11. Button 1: Text = "📊 Chart" → Format → **Action → On** → Type: **Bookmark** → Bookmark: "Chart View"
12. Button 2: Text = "📋 Table" → Format → **Action → On** → Type: **Bookmark** → Bookmark: "Table View"

**Step 4: Test**
- Click "📊 Chart" → bar chart appears
- Click "📋 Table" → table appears
- Slicers still work on both views

---

## 21.5 Bookmark-Based Tab Navigation

### The Pattern

Create "tabs" on a single page — clicking a tab changes which visuals are visible.

```
┌──────────────────────────────────────────────┐
│  [Overview]  [Sales]  [Customers]  [Region]  │  ← Tab buttons
├──────────────────────────────────────────────┤
│                                              │
│  Content changes based on selected tab       │
│                                              │
└──────────────────────────────────────────────┘
```

### Step-by-Step

1. **Create all visuals** for all tabs on the same page
2. Use the **Selection Pane** to organize:
   - Group "Overview" visuals → show only these
   - Group "Sales" visuals → hide these
   - Group "Customers" visuals → hide these
3. **Create a Bookmark** for each tab state (which visuals are visible)
4. **Create tab buttons** → link each to its bookmark
5. **Style active tab** differently (e.g., darker background for the selected tab)

### Tab Button Styling

| State | Style |
|-------|-------|
| **Active tab** | Bold text, dark background, underline |
| **Inactive tab** | Regular text, light background |
| **Hover** | Slight color change (set in Format → Style → Hover) |

---

## 21.6 Spotlight and Focus Mode

### Spotlight

- Select a visual → **Header icons (...)** → **Spotlight**
- Dims all other visuals on the page, highlighting the selected one
- Press **Esc** to exit

### Focus Mode

- Select a visual → **Header icons (...)** → **Focus Mode**
- Visual expands to fill the entire page
- Other visuals are temporarily hidden
- Press **Back to report** to exit

### Use in Presentations

- Create Bookmarks with spotlight on specific visuals
- Link to buttons for a guided presentation flow

---

## 21.7 Custom Tooltip Pages (Recap + Advanced)

### Quick Recap (from Session 14)

1. Create a new page → Format → **Tooltip → On** → Page Size: **Tooltip**
2. Add small visuals (cards, mini charts) to the tooltip page
3. Assign to a visual: Select visual → Format → Tooltip → Type: **Report Page** → choose tooltip page

### Advanced Tooltip Techniques

**Dynamic Tooltips Based on Context:**
- The tooltip page automatically receives the **filter context** of the data point being hovered
- Example: Hover over "Electronics" bar → tooltip shows Electronics monthly trend, top products, margin

**Multiple Tooltip Pages:**
- Create different tooltip pages for different visuals
- "Revenue Tooltip" for the revenue chart
- "Customer Tooltip" for the customer visual

**Tooltip Page Design Tips:**

| Tip | Why |
|-----|-----|
| Keep to **2–3 visuals** max | Tooltip is small — don't overcrowd |
| Use **Cards** for key numbers | Quick value display |
| Use a **mini line chart** for trends | Shows direction without detail |
| **No slicers** on tooltip pages | Tooltips are hover-only — no interaction |
| Match the **theme/colors** of the main report | Visual consistency |

### Tooltip Page Size Customization

Default: 320 × 240 px. You can customize:
- Format → Canvas Settings → Type: Custom
- Width: up to 500 px, Height: up to 400 px

---

## 21.8 Bookmark Groups

### Organizing Bookmarks

When you have many bookmarks, organize them into groups:

1. In Bookmarks Pane → click **...** → **Add Group**
2. Rename the group (e.g., "Tab Navigation", "Toggle Views", "Presentation")
3. Drag bookmarks into groups

### Presentation Mode with Bookmarks

1. Create a series of bookmarks as "slides"
2. View → **Bookmark Navigator** → cycles through bookmarks
3. Use **Previous/Next** buttons for slide-show-like presentation

---

## 🔧 Hands-On Activity: Bookmarks and Tooltips

**Duration:** 25 minutes

### Part 1 — Chart ↔ Table Toggle (10 min)
1. Create a **Bar Chart** (Category vs Revenue) and a **Table** (Category, Revenue, Orders)
2. Stack them on top of each other (same size/position)
3. Create two Bookmarks: "Chart View" and "Table View" (uncheck Data)
4. Create two buttons linked to the bookmarks
5. Test the toggle

### Part 2 — Custom Tooltip (8 min)
6. Create a Tooltip page ("Sales Tooltip")
7. Add: Card (Revenue), Card (Orders), mini Line Chart (Monthly Revenue)
8. Assign to the main bar chart
9. Test by hovering over different bars

### Part 3 — Reset Button (7 min)
10. Clear all slicers → create a bookmark called "Reset All"
11. Create a button → link to "Reset All" bookmark
12. Apply some filters → click the Reset button → verify all filters clear
13. Save

---

## Session 21 — Key Takeaways

1. **Bookmarks** save report state (visibility, filters, drill) — use for toggles, tabs, and presentations
2. **Selection Pane** controls show/hide and naming of visuals — essential for bookmark management
3. **Chart ↔ Table toggle** = two overlapping visuals + two bookmarks + two buttons
4. **Tooltip pages** show rich hover information — keep them small and focused
5. **Uncheck "Data"** in bookmark settings when you only want to control visual visibility

---

## Preparation for Session 22
- Review: What is conditional formatting in Excel?
- Think about: How would you color-code a matrix based on values (green = good, red = bad)?
- Explore: Format → Cell Elements in a Table/Matrix visual

---

*Session 21 of 30 | Module 5: Advanced Reporting*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
