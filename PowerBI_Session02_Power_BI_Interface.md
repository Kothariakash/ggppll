# Session 2 — Power BI Interface & Workspace
## Module 1: Business Intelligence Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Demo | Hands-On: Navigate Power BI Desktop

---

## Learning Objectives
By the end of this session, you will be able to:
1. Navigate the Power BI Desktop interface confidently
2. Identify and use the three views: Report, Table, and Model
3. Understand each pane: Filters, Visualizations, Fields, Format
4. Use essential keyboard shortcuts
5. Save and manage Power BI files

---

## 2.1 Installing Power BI Desktop

### System Requirements
| Requirement | Minimum | Recommended |
|------------|---------|-------------|
| **OS** | Windows 10 (64-bit) | Windows 11 (64-bit) |
| **RAM** | 2 GB | 8 GB+ |
| **Disk Space** | 1 GB free | SSD preferred |
| **.NET Framework** | 4.6.2+ | Latest |
| **Display** | 1440 x 900 | 1920 x 1080+ |

> **Note:** Power BI Desktop is **Windows-only**. Mac users need a Windows VM, Parallels, or use Power BI Service (web) for viewing.

### Installation Methods
1. **Microsoft Store** (Recommended) — Auto-updates, no admin rights needed
2. **Direct Download** from [powerbi.microsoft.com](https://powerbi.microsoft.com)
3. **Enterprise Deployment** via SCCM, Intune, or Group Policy

---

## 2.2 The Power BI Desktop Interface

### Three Views

| View | Icon | Purpose | When to Use |
|------|------|---------|-------------|
| **Report View** | 📊 | Build visuals, design report pages | Creating dashboards and reports |
| **Table View** | 📋 | View data in tabular format | Verifying data, checking calculated columns |
| **Model View** | 🔗 | Manage table relationships | Data modeling, Star Schema design (Session 6+) |

> **Tip:** Switch between views using the icons on the far-left sidebar.

### Interface Layout

```
┌──────────────────────────────────────────────────────────────────┐
│  RIBBON (Home | Insert | Modeling | View | Optimize | Help)     │
├──────────┬──────────────────────────────────┬────────────────────┤
│          │                                  │                    │
│  PAGES   │                                  │   FILTERS PANE     │
│  PANEL   │         REPORT CANVAS            │                    │
│          │                                  ├────────────────────┤
│  (tabs   │    (Drag visuals here)           │ VISUALIZATIONS     │
│   at     │                                  │    PANE            │
│  bottom) │                                  ├────────────────────┤
│          │                                  │   FIELDS PANE      │
│          │                                  │   (Data columns)   │
├──────────┴──────────────────────────────────┴────────────────────┤
│  STATUS BAR (Page info, View toggle, Zoom)                      │
└──────────────────────────────────────────────────────────────────┘
```

---

## 2.3 Ribbon Tabs — Detailed

### Home Tab
| Button | Function |
|--------|----------|
| **Get Data** | Connect to Excel, CSV, SQL, Web, 150+ sources |
| **Transform Data** | Open Power Query Editor for data cleaning |
| **Enter Data** | Manually type data into a table |
| **Recent Sources** | Quick access to previously used sources |
| **New Visual** | Add a new visualization to the canvas |
| **Publish** | Publish the report to Power BI Service |
| **Refresh** | Re-load data from all sources |

### Insert Tab
| Button | Function |
|--------|----------|
| **Text Box** | Add free-text annotations to the report |
| **Buttons** | Navigation buttons (Back, Bookmark, Q&A, etc.) |
| **Shapes** | Rectangles, ovals, lines for design |
| **Image** | Insert logos, icons, background images |
| **Q&A** | Natural language question box |
| **Smart Narrative** | AI-generated text summary of visuals |
| **Paginated Report** | Create pixel-perfect paginated reports |

### Modeling Tab
| Button | Function |
|--------|----------|
| **New Measure** | Create a DAX measure (Session 17) |
| **New Column** | Create a calculated column (Session 16) |
| **New Table** | Create a DAX-defined table |
| **Manage Relationships** | View/edit table relationships (Session 7) |
| **Q&A Setup** | Configure synonyms for Q&A feature |

### View Tab
| Button | Function |
|--------|----------|
| **Themes** | Apply pre-built or custom color themes |
| **Mobile Layout** | Design phone-optimized layout |
| **Gridlines** | Show alignment gridlines |
| **Snap to Grid** | Align visuals to grid |
| **Lock Objects** | Prevent accidental visual moves |
| **Selection Pane** | Show/hide/reorder visual layers |
| **Performance Analyzer** | Measure visual render times |

---

## 2.4 Panes — Detailed

### Filters Pane

| Filter Level | Scope | Use Case |
|-------------|-------|----------|
| **Visual-level** | Affects one visual only | Filter a chart to show only "Electronics" |
| **Page-level** | Affects all visuals on the current page | Show only 2024 data on this page |
| **Report-level** | Affects all pages in the report | Filter entire report to one region |
| **Drill-through** | Navigational filter across pages | Click on a product → see its detail page |

### Visualizations Pane

Three sub-sections:
1. **Visual types** — Grid of chart icons (bar, line, pie, map, table, etc.)
2. **Build** — Drag fields to Axis, Values, Legend, Tooltips
3. **Format** — Customize colors, labels, titles, borders

### Fields Pane

- Lists all **tables** and their **columns**
- **Σ** icon = numeric column (can be aggregated)
- **Calculator** icon = DAX measure
- **Calendar** icon = date column
- **Globe** icon = geographic column
- Drag fields from here onto visuals or into filter wells

---

## 2.5 Report Canvas Basics

### Adding Visuals
1. Click on a visual type in the Visualizations pane → empty visual appears on canvas
2. Drag fields from the Fields pane into the visual's field wells
3. OR: Select fields first → Power BI auto-suggests a visual

### Visual Field Wells
| Well | Purpose | Example |
|------|---------|---------|
| **Axis / Rows** | Categories (X-axis or rows) | Product Category, Month |
| **Values** | Numbers to display | Sum of Revenue, Count of Orders |
| **Legend** | Color grouping | Region, Segment |
| **Tooltips** | Extra info on hover | Profit Margin, Customer Count |
| **Small Multiples** | Grid of mini-charts by category | One chart per Region |

### Canvas Operations
| Action | How |
|--------|-----|
| **Move a visual** | Click and drag |
| **Resize** | Drag corner/edge handles |
| **Copy visual** | Ctrl+C → Ctrl+V |
| **Delete visual** | Select → Delete key |
| **Multi-select** | Ctrl+Click or rubber-band select |
| **Align visuals** | Format → Align (top, left, distribute) |

---

## 2.6 Pages

- Pages work like **tabs** in Excel — each page is a separate report view
- Typical report structure:
  - Page 1: **Executive Summary** (high-level KPIs)
  - Page 2: **Sales Analysis** (detailed trends)
  - Page 3: **Regional Breakdown** (geographic view)
  - Page 4: **Product Performance** (product-level detail)

### Page Operations
| Action | How |
|--------|-----|
| **Add page** | Click "+" at the bottom |
| **Rename** | Double-click the tab |
| **Duplicate** | Right-click → Duplicate Page |
| **Delete** | Right-click → Delete Page |
| **Reorder** | Drag tabs left/right |
| **Hide page** | Right-click → Hide Page (still accessible via drill-through) |

---

## 2.7 File Types

| Extension | Name | Purpose |
|-----------|------|---------|
| **.pbix** | Power BI Desktop file | Contains data model + queries + report (your working file) |
| **.pbit** | Power BI Template | Report structure without data — for sharing templates |
| **.pbids** | Data source connection | Pre-configured data source (no report/model) |

### File Size Considerations
- `.pbix` contains **imported data** — file size grows with data volume
- Typical sizes: 5 MB (small) → 50 MB (medium) → 500 MB+ (large)
- **1 GB limit** for Power BI Pro publishing
- Optimize with: Remove unused columns, aggregate data, use DirectQuery for huge datasets

---

## 2.8 Keyboard Shortcuts

### Navigation
| Shortcut | Action |
|----------|--------|
| Ctrl + F6 | Cycle between panes |
| Tab | Navigate between visuals on canvas |
| Escape | Deselect current visual |
| Ctrl + Shift + D | Duplicate current page |

### Editing
| Shortcut | Action |
|----------|--------|
| Ctrl + S | Save |
| Ctrl + Z | Undo |
| Ctrl + Y | Redo |
| Ctrl + C | Copy visual |
| Ctrl + V | Paste visual |
| Delete | Remove selected visual |
| Ctrl + A | Select all visuals on page |

### View
| Shortcut | Action |
|----------|--------|
| Ctrl + Shift + F | Toggle full-screen preview |
| Ctrl + 1 | Report View |
| Ctrl + 2 | Table View |
| Ctrl + 3 | Model View |
| Alt + F4 | Close Power BI Desktop |

---

## 🔧 Hands-On Activity: Explore the Interface

**Duration:** 20 minutes

### Task List:
1. **Open** Power BI Desktop
2. **Switch** between Report View, Table View, and Model View (left sidebar icons)
3. **Locate** the Filters, Visualizations, and Fields panes (right side)
4. Click **Home → Get Data** and browse the available data source connectors (don't import yet — just explore)
5. **Add a new blank page** → Rename it to "Practice Page"
6. **Insert a Text Box** (Insert tab) → Type "My First Power BI Report"
7. **Insert a Shape** (rectangle) → Change its color using Format options
8. **Add another page** → Rename to "Summary"
9. **Save** the file as `Practice_Session2.pbix`
10. **Close and reopen** the file to confirm it saved correctly

### Exploration Questions:
- How many data source connectors can you count in Get Data?
- Can you find the Performance Analyzer? (View tab)
- What happens when you right-click on a page tab?

---

## Session 2 — Key Takeaways

1. Power BI Desktop has **3 views**: Report (build visuals), Table (see data), Model (manage relationships)
2. The **Ribbon** organizes functions across Home, Insert, Modeling, View, and Help tabs
3. **Fields pane** = your data; **Visualizations pane** = your charts; **Filters pane** = your filters
4. All work is saved as `.pbix` files
5. **Learn the shortcuts** — Ctrl+S (save), Ctrl+Z (undo), Tab (navigate visuals)

---

## Preparation for Session 3
- Download a sample **Sales dataset** in Excel format (or use any business spreadsheet with headers)
- Download a sample **CSV file** (e.g., from Kaggle — search "sample sales data CSV")
- Keep Power BI Desktop open for the next session

---

*Session 2 of 30 | Module 1: Business Intelligence Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
