# Session 22 — Conditional Formatting
## Module 5: Advanced Reporting | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Apply Conditional Formatting to Tables, Matrices, and Cards

---

## Learning Objectives
By the end of this session, you will be able to:
1. Apply background color and font color rules to tables and matrices
2. Use data bars and icon sets for in-cell visualization
3. Create DAX measures for conditional formatting logic
4. Apply conditional formatting to cards and chart elements
5. Build heat maps and traffic-light scorecards

---

## 22.1 What is Conditional Formatting?

**Conditional Formatting** changes the appearance of visuals (colors, icons, bars) based on data values — making patterns, exceptions, and statuses immediately visible.

### Where Conditional Formatting Applies

| Visual Type | Supports Conditional Formatting |
|------------|-------------------------------|
| **Table** | Background color, Font color, Data bars, Icons, Web URL |
| **Matrix** | Background color, Font color, Data bars, Icons |
| **Card** | Callout value color, Background color |
| **Bar/Column Chart** | Bar color based on value |
| **KPI** | Status color |
| **Gauge** | Color based on value |

---

## 22.2 Accessing Conditional Formatting

### For Tables and Matrices

1. Select the Table or Matrix visual
2. In the **Visualizations** pane → **Format** (paint roller) → **Cell Elements**
3. OR: Click the **dropdown arrow** on a field in the Values well → **Conditional Formatting**

### Conditional Formatting Options

| Option | What It Does | Best For |
|--------|-------------|----------|
| **Background Color** | Cell background changes based on value | Heat maps, status indicators |
| **Font Color** | Text color changes based on value | Highlighting positive/negative |
| **Data Bars** | In-cell horizontal bar chart | Comparing magnitudes at a glance |
| **Icons** | Symbols (✅❌⚠️▲▼) based on rules | Status indicators |
| **Web URL** | Cell becomes a clickable hyperlink | Links to detail pages |

---

## 22.3 Background Color Formatting

### Method 1: Color Scale (Gradient)

Applies a color gradient based on value range.

**Configuration:**
| Setting | Option |
|---------|--------|
| **Format style** | Gradient |
| **What field should this be based on** | The measure/column to base colors on |
| **Minimum color** | Color for lowest value (e.g., light green) |
| **Center color** | Color for middle value (optional) |
| **Maximum color** | Color for highest value (e.g., dark green) |
| **Minimum value** | Auto or custom number |
| **Maximum value** | Auto or custom number |

**Result:** A heat map where darker = higher values.

### Method 2: Rules

Applies specific colors based on conditions.

**Configuration:**

```
Rule 1: If value >= 100000 → Background: Green
Rule 2: If value >= 50000 AND < 100000 → Background: Yellow
Rule 3: If value < 50000 → Background: Red
```

| Setting | Options |
|---------|---------|
| **Format style** | Rules |
| **Condition** | Is greater than, Is less than, Is between, etc. |
| **Value** | Number, Percentage, or Percentile |
| **Color** | Pick a color for that rule |
| **Add rule** | Click "+ Add Rule" for more conditions |

### Method 3: Field Value (DAX-Driven)

Use a DAX measure that returns a color code, and bind the formatting to that measure.

**Step 1:** Create a DAX measure that returns a hex color:
```dax
Revenue Color = 
VAR Val = [Total Revenue]
RETURN
SWITCH(
    TRUE(),
    Val >= 100000, "#27AE60",    // Green
    Val >= 50000, "#F39C12",     // Yellow
    "#E74C3C"                     // Red
)
```

**Step 2:** In Conditional Formatting → Format style: **Field value** → select the `Revenue Color` measure

> **This is the most powerful method** — full control via DAX logic.

---

## 22.4 Font Color Formatting

Same methods as background color, but changes text color instead.

### Common Pattern: Red for Negative, Green for Positive

**Rules method:**
```
If value > 0 → Font Color: Green (#27AE60)
If value < 0 → Font Color: Red (#E74C3C)
If value = 0 → Font Color: Gray (#95A5A6)
```

**DAX method:**
```dax
Variance Font Color = 
IF([Revenue Variance] >= 0, "#27AE60", "#E74C3C")
```

---

## 22.5 Data Bars

### What Are Data Bars?

Horizontal bars inside table/matrix cells that show the magnitude of values — like a mini bar chart.

### Configuration

1. Go to Conditional Formatting → **Data Bars**
2. Settings:
   - **Positive bar color:** (e.g., blue)
   - **Negative bar color:** (e.g., red)
   - **Show bar only:** On = hides the number, shows only the bar
   - **Minimum / Maximum:** Auto or custom values

### Best For
- Quick visual comparison of values across rows
- Revenue, quantity, or score columns
- When you want both the number AND a visual indicator

---

## 22.6 Icons (Icon Sets)

### What Are Icon Sets?

Small symbols displayed alongside or instead of values — used for status indicators.

### Available Icon Types

| Set | Icons | Use For |
|-----|-------|---------|
| **Flags** | 🚩 Red, Yellow, Green flags | Priority or urgency |
| **Traffic Lights** | 🔴🟡🟢 Circles | Performance status |
| **Signs** | ✖️△✔️ | Pass/Warn/Fail |
| **Arrows** | ▲▶▼ Up/Right/Down | Trend direction |
| **Shapes** | ◆●■ Diamond/Circle/Square | Custom status |
| **Ratings** | ★★★★★ Stars | Quality or rating |

### Configuration

1. Conditional Formatting → **Icons**
2. Choose Icon Layout: **Left of data** or **Right of data**
3. Set rules:
   ```
   If value >= 1.0 → ✔️ Green check (≥100% achievement)
   If value >= 0.9 → ⚠️ Yellow warning (90-99%)
   If value < 0.9 → ✖️ Red cross (<90%)
   ```
4. Option: **Show icon only** (hides the number)

### DAX-Driven Icons

For more control, use a DAX measure with Unicode characters:

```dax
Status Icon = 
VAR Achv = [Achievement %]
RETURN
SWITCH(
    TRUE(),
    Achv >= 1, "▲",
    Achv >= 0.9, "►",
    "▼"
)
```

Then apply Font Color conditional formatting to color the icon:
```dax
Status Icon Color = 
VAR Achv = [Achievement %]
RETURN
SWITCH(
    TRUE(),
    Achv >= 1, "#27AE60",
    Achv >= 0.9, "#F39C12",
    "#E74C3C"
)
```

---

## 22.7 Conditional Formatting on Charts

### Bar/Column Chart Colors

1. Select the bar/column chart
2. Format → **Data Colors** → **Advanced Controls** (fx icon)
3. Choose: **Gradient**, **Rules**, or **Field value**
4. Apply color based on the value of each bar

### Example: Color bars by performance
```dax
Bar Color = 
IF([Revenue YoY %] >= 0, "#27AE60", "#E74C3C")
```

Assign as Field value for Data Colors → bars turn green (growth) or red (decline).

### Card Conditional Formatting

1. Select a Card visual
2. Format → **Callout Value** → **Color** → **fx** (conditional formatting icon)
3. Apply rules: Green if above target, Red if below

---

## 22.8 Heat Map Pattern

### Building a Heat Map Matrix

1. Create a **Matrix:** Rows = Region, Columns = Month, Values = Revenue
2. Apply **Background Color** conditional formatting (Gradient):
   - Minimum: Light color (e.g., white or light blue)
   - Maximum: Dark color (e.g., dark blue or dark green)
3. Result: Cells with higher revenue are darker — patterns immediately visible

### Diverging Heat Map (Above/Below Average)

```dax
Revenue vs Avg = [Total Revenue] - [Avg Revenue All]

Heat Map Color = 
VAR Val = [Revenue vs Avg]
RETURN
SWITCH(
    TRUE(),
    Val > 20000, "#1E8449",
    Val > 0, "#82E0AA",
    Val > -20000, "#F5B7B1",
    "#CB4335"
)
```

---

## 22.9 Traffic Light Scorecard

### Complete Scorecard with Conditional Formatting

```
┌──────────┬──────────┬──────────┬──────────┬──────────┐
│ Region   │ Revenue  │ Target   │ Achv %   │ Status   │
├──────────┼──────────┼──────────┼──────────┼──────────┤
│ North    │ ₹12.5 Cr │ ₹12 Cr  │  104%    │   🟢     │
│ South    │ ₹10.2 Cr │ ₹11 Cr  │   93%    │   🟡     │
│ East     │ ₹8.1 Cr  │ ₹10 Cr  │   81%    │   🔴     │
│ West     │ ₹11.5 Cr │ ₹11 Cr  │  105%    │   🟢     │
└──────────┴──────────┴──────────┴──────────┴──────────┘
```

**Steps:**
1. Create a Matrix with Region, Revenue, Target, Achievement %
2. Apply **Icon** formatting on Achievement %: ✔️ ≥100%, ⚠️ 90-99%, ✖️ <90%
3. Apply **Background Color** on Achievement %: Green ≥100%, Yellow 90-99%, Red <90%
4. Apply **Data Bars** on Revenue column
5. Apply **Font Color** on Achievement %: Green positive, Red negative

---

## 🔧 Hands-On Activity: Conditional Formatting

**Duration:** 25 minutes

### Tasks

**Part 1 — Matrix Heat Map (8 min)**
1. Create a Matrix: Product Category (Rows) × Quarter (Columns) × Revenue (Values)
2. Apply **Background Color → Gradient**: White (min) → Dark Blue (max)
3. Verify: highest revenue cells are darkest

**Part 2 — Table with Data Bars and Icons (10 min)**
4. Create a Table: Region, Revenue, Profit, Margin %, YoY %
5. Apply **Data Bars** on Revenue column (blue bars)
6. Apply **Font Color** on YoY %: Green if ≥ 0, Red if < 0
7. Apply **Icons** on Margin %:
   - ✔️ if ≥ 20%
   - ⚠️ if ≥ 15%
   - ✖️ if < 15%

**Part 3 — DAX-Driven Formatting (7 min)**
8. Create a measure:
   ```dax
   Margin Color = IF([Gross Margin %] >= 0.2, "#27AE60", IF([Gross Margin %] >= 0.15, "#F39C12", "#E74C3C"))
   ```
9. Apply as **Field Value** background color on Margin % column
10. Test by filtering — colors should update dynamically
11. Save

---

## Session 22 — Key Takeaways

1. **Conditional Formatting** makes data patterns instantly visible — colors, bars, icons
2. **Three methods:** Gradient (continuous), Rules (discrete), Field Value (DAX-driven)
3. **Data Bars** = in-cell bar charts for magnitude comparison
4. **Icons** = status indicators (✔️⚠️✖️) for at-a-glance performance
5. **DAX-driven** formatting (Field Value) gives the most control and flexibility

---

## Preparation for Session 23
- Think about: In your organization, should all users see all data? Or should sales reps see only their region?
- Review: What is data security in a BI context?
- Consider: How would you restrict data access per user without creating separate reports?

---

*Session 22 of 30 | Module 5: Advanced Reporting*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
