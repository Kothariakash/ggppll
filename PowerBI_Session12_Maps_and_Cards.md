# Session 12 — Maps, Cards & Gauge Visuals
## Module 3: Data Visualization | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build Map, Card, Multi-Row Card, and Gauge Visuals

---

## Learning Objectives
By the end of this session, you will be able to:
1. Build map visuals using geographic data (city, state, country, lat/long)
2. Create Card and Multi-Row Card visuals for KPI display
3. Build Gauge visuals for target tracking
4. Understand data categorization for geographic columns
5. Choose the right visual for single-value and location-based data

---

## 12.1 Map Visuals

### Map Types in Power BI

| Visual | Best For | Data Needed |
|--------|----------|-------------|
| **Map (Bubble)** | Show locations with size-encoded values | City/Country + a measure |
| **Filled Map** | Color regions by value (choropleth) | State/Country + a measure |
| **ArcGIS Map** | Advanced geospatial analysis | Location + measures |
| **Azure Map** | Enterprise mapping with custom layers | Lat/Long + measures |
| **Shape Map** | Custom geographic shapes (TopoJSON) | Region code + measure |

### Building a Bubble Map

1. Click **Map** in Visualizations pane
2. Drag a geographic field to **Location** well (e.g., City, State, or Country)
3. Drag a measure to **Bubble Size** (e.g., Sum of Revenue)
4. Optionally drag a field to **Legend** for color grouping
5. Optionally drag to **Tooltips** for extra hover info

### Building a Filled Map

1. Click **Filled Map** in Visualizations
2. Drag a geographic field to **Location** (e.g., State, Country)
3. Drag a measure to **Values** (e.g., Sum of Revenue)
4. Color intensity shows the value — darker = higher

### Data Categorization for Maps

**Problem:** Power BI may not recognize "Mumbai" as a city or "Maharashtra" as a state.

**Fix — Set Data Category:**
1. Select the geographic column in Table View or Model View
2. **Column Tools** tab → **Data Category** dropdown
3. Choose: City, State/Province, Country/Region, Latitude, Longitude, Postal Code

| Data Category | Examples |
|--------------|---------|
| **City** | Mumbai, Delhi, Bangalore |
| **State or Province** | Maharashtra, Karnataka, Tamil Nadu |
| **Country/Region** | India, United States, Canada |
| **Postal Code** | 400001, 110001 |
| **Latitude** | 19.0760 |
| **Longitude** | 72.8777 |
| **Continent** | Asia, Europe |

### Using Latitude and Longitude

For precise location plotting:
1. Drag **Latitude** to the Latitude well
2. Drag **Longitude** to the Longitude well
3. Much more accurate than city/country name geocoding

### Map Best Practices

| Practice | Why |
|----------|-----|
| Always set Data Category for geo columns | Prevents misplotting |
| Use Lat/Long for precise locations | City names can be ambiguous ("Delhi" exists in multiple countries) |
| Limit bubble count to ~100 | Too many = visual clutter |
| Add Country context for city-level data | "Mumbai, India" is clearer than just "Mumbai" |
| Use Filled Map for state/country level | Better than many overlapping bubbles |
| Avoid maps if geography isn't the insight | A bar chart sorted by revenue is often clearer |

### Map Troubleshooting

| Issue | Cause | Fix |
|-------|-------|-----|
| Points plotted in wrong country | Ambiguous city names | Add Country column or use Lat/Long |
| No map displayed | Bing Maps disabled | File → Options → Security → Enable Map visuals |
| Blank map | Data Category not set | Set Data Category on geographic column |
| Too many points | Performance issue | Aggregate to state/country level |

---

## 12.2 Card Visuals

### What is a Card?

A **Card** displays a single aggregated value — a big, bold number. It's the most common visual for KPIs and headline metrics.

### When to Use Cards
- **Headline KPIs:** Total Revenue, Total Customers, Average Order Value
- **At-a-glance numbers** at the top of a dashboard
- **Context setting:** Show the "big picture" before detailed charts

### Building a Card

1. Click **Card** in Visualizations
2. Drag a measure to **Fields** well (e.g., Sum of Revenue)
3. Power BI displays the aggregated number prominently

### Card Formatting

| Setting | Location | Effect |
|---------|----------|--------|
| **Display units** | Format → Callout Value → Display Units | Auto, Thousands (K), Millions (M), Billions (B) |
| **Decimal places** | Format → Callout Value → Value decimal places | 0, 1, 2 |
| **Font size** | Format → Callout Value → Font size | Make it large and prominent |
| **Category label** | Format → Category Label → On/Off | Show/hide the field name below |
| **Custom label** | Format → Category Label → Custom → text | e.g., "Total Revenue (₹)" |
| **Background** | Format → General → Background | Color the card background |
| **Border** | Format → General → Border | Add visual border |

### Card Layout Pattern

A typical dashboard top section:

```
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│ ₹42.3 Cr │ │  12,500  │ │  ₹3,384  │ │  18.5%   │
│ Revenue  │ │ Orders   │ │ Avg Order│ │ Margin   │
└──────────┘ └──────────┘ └──────────┘ └──────────┘
```

---

## 12.3 Multi-Row Card

### What is a Multi-Row Card?

Displays **multiple values** in a compact card format — one row per category.

### When to Use
- Show KPIs broken down by category (Revenue by Region)
- Display multiple metrics in a small space
- Quick summary without a full chart

### Building a Multi-Row Card

1. Click **Multi-Row Card** in Visualizations
2. Drag a category to **Fields** (e.g., Region)
3. Drag measures to **Fields** (e.g., Revenue, Order Count)
4. Each category gets its own "row" with the metric values

---

## 12.4 Gauge Visual

### What is a Gauge?

A **Gauge** (speedometer) shows a single value against a target — how close you are to a goal.

### When to Use
- **Target tracking:** Actual vs Target revenue
- **Progress monitoring:** % of quota achieved
- **Threshold visualization:** Are we in green, yellow, or red zone?

### Building a Gauge

1. Click **Gauge** in Visualizations
2. Drag the actual value to **Value** (e.g., Actual Revenue)
3. Drag the target to **Target Value** (e.g., Target Revenue)
4. Optionally set **Min** and **Max** values

### Gauge Configuration

| Well | Purpose | Example |
|------|---------|---------|
| **Value** | Current/actual number | Sum of Revenue |
| **Minimum Value** | Left end of the gauge | 0 |
| **Maximum Value** | Right end of the gauge | 100000 |
| **Target Value** | Target line/marker | Target Revenue |

### Gauge Formatting

| Setting | Effect |
|---------|--------|
| **Gauge Axis → Min/Max** | Set scale range |
| **Target → Color/Line Width** | Customize target marker |
| **Data Colors** | Color of the gauge fill |
| **Conditional formatting** | Change color based on value vs target (green/red) |

### Gauge Limitations
- Shows only **one value** — not good for comparisons
- Can waste space if not sized well
- Consider a **Card with conditional formatting** as an alternative

---

## 12.5 KPI Visual

### What is a KPI Visual?

Shows a metric with its **trend** and **target status** — value + direction + goal.

### Building a KPI

1. Click **KPI** in Visualizations
2. **Indicator:** The metric to track (e.g., Revenue)
3. **Trend Axis:** Time dimension for the sparkline (e.g., Month)
4. **Target:** The goal value (e.g., Target Revenue)

### KPI Display Elements
```
┌─────────────────────────┐
│   ₹42.3 Cr              │  ← Current Value
│   ▲ 8.5%                │  ← % vs Target (green = above, red = below)
│   ~~~~~~~~              │  ← Trend sparkline
│   Target: ₹39.0 Cr      │  ← Target value
└─────────────────────────┘
```

---

## 12.6 Choosing Between Single-Value Visuals

| Visual | Shows | Best For |
|--------|-------|----------|
| **Card** | One big number | Headline KPI, no target comparison |
| **Multi-Row Card** | Multiple values by category | Summary breakdown |
| **Gauge** | Value vs target (speedometer) | Progress toward a goal |
| **KPI** | Value + trend + target | Performance with direction |

---

## 🔧 Hands-On Activity: Build Maps and KPI Cards

**Duration:** 25 minutes

### Tasks

**Page: "Geographic Analysis"**
1. **Bubble Map:** Location = City (set Data Category), Bubble Size = Revenue, Legend = Region
2. **Filled Map:** Location = State, Values = Revenue (color intensity)
3. Test: Click a region on the map → do other visuals filter?

**Page: "KPI Dashboard" (top section)**
4. **4 Cards** across the top:
   - Card 1: Total Revenue (display in Lakhs or Cr)
   - Card 2: Total Orders (COUNTROWS)
   - Card 3: Average Order Value
   - Card 4: Distinct Customer Count
5. Format each card: large font, custom label, appropriate decimal places

**Additional Visuals:**
6. **Gauge:** Value = Current Month Revenue, Target = Monthly Target
7. **KPI:** Indicator = Revenue, Trend Axis = Month, Target = Target Revenue
8. **Multi-Row Card:** Show Revenue by Region (top 4 regions)

9. Save the file

---

## Session 12 — Key Takeaways

1. **Set Data Category** on geographic columns — City, State, Country — for maps to work correctly
2. **Bubble Map** for point locations; **Filled Map** for shading regions by value
3. **Card** = one big number; **Multi-Row Card** = multiple values; **Gauge** = value vs target
4. **KPI visual** shows value + trend sparkline + target comparison
5. Use **Lat/Long** for precise map plotting; city names can be ambiguous

---

## Preparation for Session 13
- Think about: What interactive filters would help users explore the data?
- Review: What is a slicer? How is it different from a filter?

---

*Session 12 of 30 | Module 3: Data Visualization*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
