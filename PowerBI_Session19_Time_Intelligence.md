# Session 19 — Time Intelligence in DAX
## Module 4: DAX Fundamentals | Professional Power BI Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Build YTD, QTD, MoM, YoY, and Running Total Measures

---

## Learning Objectives
By the end of this session, you will be able to:
1. Understand the requirements for Time Intelligence (Date table, Mark as Date Table)
2. Create Year-to-Date (YTD), Quarter-to-Date (QTD), Month-to-Date (MTD) measures
3. Build Period-over-Period comparisons (MoM, QoQ, YoY)
4. Calculate Running Totals and Moving Averages
5. Use DATEADD, SAMEPERIODLASTYEAR, PARALLELPERIOD

---

## 19.1 Prerequisites for Time Intelligence

### Three Requirements

1. **A dedicated Date Table** — one row per day, no gaps
2. **Mark as Date Table** — Modeling tab → Mark as Date Table
3. **Active relationship** between Date table and Fact table on the date column

### Verifying Your Date Table

```dax
// Date table should have been created in Session 8:
DateTable = 
ADDCOLUMNS(
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Quarter", "Q" & QUARTER([Date]),
    "QuarterNumber", QUARTER([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "MonthNumber", MONTH([Date]),
    "MonthYear", FORMAT([Date], "MMM YYYY"),
    "WeekNumber", WEEKNUM([Date]),
    "DayOfWeek", FORMAT([Date], "DDDD"),
    "DayOfWeekNumber", WEEKDAY([Date], 2),
    "IsWeekend", IF(WEEKDAY([Date], 2) >= 6, TRUE(), FALSE())
)
```

### Marking as Date Table
1. Select the Date table in the Fields pane
2. **Table Tools** tab → **Mark as Date Table**
3. Select the Date column as the date column
4. Power BI validates: continuous dates, unique values, no blanks

> **If you skip this step:** Time Intelligence functions will produce incorrect or no results.

---

## 19.2 Year-to-Date (YTD), Quarter-to-Date (QTD), Month-to-Date (MTD)

### What are X-to-Date Calculations?

| Function | Meaning | Example (if today = March 15, 2024) |
|----------|---------|--------------------------------------|
| **YTD** | January 1 to current date in the year | Jan 1 → Mar 15 revenue |
| **QTD** | First day of current quarter to current date | Jan 1 → Mar 15 (Q1) |
| **MTD** | First day of current month to current date | Mar 1 → Mar 15 |

### DAX Functions

```dax
// Year-to-Date Revenue
Revenue YTD = TOTALYTD(SUM(Sales[Revenue]), DateTable[Date])

// Quarter-to-Date Revenue
Revenue QTD = TOTALQTD(SUM(Sales[Revenue]), DateTable[Date])

// Month-to-Date Revenue
Revenue MTD = TOTALMTD(SUM(Sales[Revenue]), DateTable[Date])
```

### Alternative Using CALCULATE + DATESYTD

```dax
Revenue YTD = 
CALCULATE(
    SUM(Sales[Revenue]),
    DATESYTD(DateTable[Date])
)
```

| Function | Filter Modification |
|----------|-------------------|
| `DATESYTD(date_column)` | Expands filter to start of year through current date |
| `DATESQTD(date_column)` | Expands filter to start of quarter through current date |
| `DATESMTD(date_column)` | Expands filter to start of month through current date |

### Fiscal Year YTD

If your fiscal year starts in April:

```dax
Revenue FY YTD = TOTALYTD(SUM(Sales[Revenue]), DateTable[Date], "3/31")
```

- Third argument: fiscal year end date ("3/31" = fiscal year April–March)

---

## 19.3 Period-over-Period Comparisons

### Same Period Last Year (SPLY)

```dax
Revenue Last Year = 
CALCULATE(
    SUM(Sales[Revenue]),
    SAMEPERIODLASTYEAR(DateTable[Date])
)
```

- If current context is March 2024 → returns March 2023 revenue
- If current context is Q2 2024 → returns Q2 2023 revenue
- Works with any date granularity (day, month, quarter, year)

### Year-over-Year (YoY) Change

```dax
Revenue YoY Change = [Total Revenue] - [Revenue Last Year]

Revenue YoY % = 
DIVIDE(
    [Total Revenue] - [Revenue Last Year],
    [Revenue Last Year],
    0
)
```

### YTD Last Year

```dax
Revenue YTD LY = 
CALCULATE(
    SUM(Sales[Revenue]),
    DATESYTD(SAMEPERIODLASTYEAR(DateTable[Date]))
)

// YTD Growth %
YTD Growth % = DIVIDE([Revenue YTD] - [Revenue YTD LY], [Revenue YTD LY], 0)
```

---

## 19.4 DATEADD — Flexible Period Shifts

### Syntax

```dax
DATEADD(date_column, number_of_intervals, interval)
```

### Intervals: DAY, MONTH, QUARTER, YEAR

### Examples

```dax
// Revenue — Previous Month
Revenue Prev Month = 
CALCULATE(SUM(Sales[Revenue]), DATEADD(DateTable[Date], -1, MONTH))

// Revenue — Previous Quarter
Revenue Prev Quarter = 
CALCULATE(SUM(Sales[Revenue]), DATEADD(DateTable[Date], -1, QUARTER))

// Revenue — Previous Year (same as SAMEPERIODLASTYEAR)
Revenue Prev Year = 
CALCULATE(SUM(Sales[Revenue]), DATEADD(DateTable[Date], -1, YEAR))

// Revenue — 2 Years Ago
Revenue 2 Years Ago = 
CALCULATE(SUM(Sales[Revenue]), DATEADD(DateTable[Date], -2, YEAR))

// Revenue — Next Month (forecast comparison)
Revenue Next Month = 
CALCULATE(SUM(Sales[Revenue]), DATEADD(DateTable[Date], 1, MONTH))
```

### Month-over-Month (MoM) Change

```dax
Revenue MoM Change = [Total Revenue] - [Revenue Prev Month]

Revenue MoM % = 
DIVIDE(
    [Total Revenue] - [Revenue Prev Month],
    [Revenue Prev Month],
    0
)
```

### Quarter-over-Quarter (QoQ) Change

```dax
Revenue QoQ Change = [Total Revenue] - [Revenue Prev Quarter]

Revenue QoQ % = 
DIVIDE(
    [Total Revenue] - [Revenue Prev Quarter],
    [Revenue Prev Quarter],
    0
)
```

---

## 19.5 PARALLELPERIOD

### Syntax

```dax
PARALLELPERIOD(date_column, number_of_intervals, interval)
```

### Difference from DATEADD

| Function | Behavior |
|----------|----------|
| **DATEADD** | Shifts the EXACT date range (e.g., Mar 1–15 → Feb 1–15) |
| **PARALLELPERIOD** | Shifts to the FULL parallel period (e.g., if in March → returns ALL of February) |

### Example

```dax
// Full previous month revenue (regardless of which day you're viewing)
Revenue Full Prev Month = 
CALCULATE(SUM(Sales[Revenue]), PARALLELPERIOD(DateTable[Date], -1, MONTH))

// Full previous year revenue
Revenue Full Prev Year = 
CALCULATE(SUM(Sales[Revenue]), PARALLELPERIOD(DateTable[Date], -1, YEAR))
```

### When to Use Which

| Scenario | Use |
|----------|-----|
| Compare same date range shifted back | **DATEADD** |
| Compare full previous period | **PARALLELPERIOD** |
| Compare same period last year | **SAMEPERIODLASTYEAR** |
| X-to-Date calculations | **TOTALYTD / DATESYTD** |

---

## 19.6 Running Total (Cumulative Sum)

### Running Total by Date

```dax
Revenue Running Total = 
CALCULATE(
    SUM(Sales[Revenue]),
    FILTER(
        ALL(DateTable[Date]),
        DateTable[Date] <= MAX(DateTable[Date])
    )
)
```

### How It Works

| Month | Revenue | Running Total |
|-------|---------|---------------|
| Jan | 50,000 | 50,000 |
| Feb | 48,000 | 98,000 |
| Mar | 52,000 | 150,000 |
| Apr | 55,000 | 205,000 |

### Running Total Within Year (Resets Each Year)

```dax
Revenue Running Total YTD = 
CALCULATE(
    SUM(Sales[Revenue]),
    FILTER(
        ALL(DateTable),
        DateTable[Date] <= MAX(DateTable[Date]) &&
        DateTable[Year] = MAX(DateTable[Year])
    )
)
```

---

## 19.7 Moving Average

### 3-Month Moving Average

```dax
Revenue 3M Avg = 
AVERAGEX(
    DATESINPERIOD(DateTable[Date], MAX(DateTable[Date]), -3, MONTH),
    CALCULATE(SUM(Sales[Revenue]))
)
```

### 12-Month Moving Average

```dax
Revenue 12M Avg = 
AVERAGEX(
    DATESINPERIOD(DateTable[Date], MAX(DateTable[Date]), -12, MONTH),
    CALCULATE(SUM(Sales[Revenue]))
)
```

### How Moving Average Works

| Month | Revenue | 3M Moving Avg |
|-------|---------|--------------|
| Jan | 50,000 | 50,000 (only 1 month) |
| Feb | 48,000 | 49,000 (avg of Jan+Feb) |
| Mar | 52,000 | 50,000 (avg of Jan+Feb+Mar) |
| Apr | 55,000 | 51,667 (avg of Feb+Mar+Apr) |
| May | 62,000 | 56,333 (avg of Mar+Apr+May) |

---

## 19.8 Time Intelligence Functions Reference

| Function | Purpose |
|----------|---------|
| `TOTALYTD(expr, date)` | Year-to-Date |
| `TOTALQTD(expr, date)` | Quarter-to-Date |
| `TOTALMTD(expr, date)` | Month-to-Date |
| `DATESYTD(date)` | Returns dates from year start to current |
| `DATESQTD(date)` | Returns dates from quarter start to current |
| `DATESMTD(date)` | Returns dates from month start to current |
| `SAMEPERIODLASTYEAR(date)` | Same dates, previous year |
| `DATEADD(date, n, interval)` | Shift dates by n intervals |
| `PARALLELPERIOD(date, n, interval)` | Full parallel period shifted |
| `DATESINPERIOD(date, end, n, interval)` | Returns n periods of dates ending at end date |
| `PREVIOUSMONTH(date)` | Dates of previous month |
| `PREVIOUSQUARTER(date)` | Dates of previous quarter |
| `PREVIOUSYEAR(date)` | Dates of previous year |
| `NEXTMONTH(date)` | Dates of next month |
| `FIRSTDATE(date)` | First date in context |
| `LASTDATE(date)` | Last date in context |
| `STARTOFMONTH(date)` | First day of month in context |
| `ENDOFMONTH(date)` | Last day of month in context |
| `STARTOFQUARTER(date)` | First day of quarter |
| `ENDOFQUARTER(date)` | Last day of quarter |
| `STARTOFYEAR(date)` | First day of year |
| `ENDOFYEAR(date)` | Last day of year |
| `OPENINGBALANCEMONTH(expr, date)` | Value at start of month |
| `CLOSINGBALANCEMONTH(expr, date)` | Value at end of month |

---

## 🔧 Hands-On Activity: Build Time Intelligence Measures

**Duration:** 25 minutes

### Pre-Check
- [ ] Date table exists with continuous dates
- [ ] Date table is marked as Date Table
- [ ] Relationship: DateTable[Date] → Sales[OrderDate] (1:Many, Active)

### Tasks

**Year-to-Date:**
1. `Revenue YTD = TOTALYTD(SUM(Sales[Revenue]), DateTable[Date])`

**Period Comparisons:**
2. `Revenue LY = CALCULATE(SUM(Sales[Revenue]), SAMEPERIODLASTYEAR(DateTable[Date]))`
3. `Revenue YoY % = DIVIDE([Total Revenue] - [Revenue LY], [Revenue LY], 0)`
4. `Revenue Prev Month = CALCULATE(SUM(Sales[Revenue]), DATEADD(DateTable[Date], -1, MONTH))`
5. `Revenue MoM % = DIVIDE([Total Revenue] - [Revenue Prev Month], [Revenue Prev Month], 0)`

**Running Total:**
6. `Revenue Running = CALCULATE(SUM(Sales[Revenue]), FILTER(ALL(DateTable[Date]), DateTable[Date] <= MAX(DateTable[Date])))`

**Moving Average:**
7. `Revenue 3M Avg = AVERAGEX(DATESINPERIOD(DateTable[Date], MAX(DateTable[Date]), -3, MONTH), CALCULATE(SUM(Sales[Revenue])))`

### Verification
- Create a **Line Chart:** Month (X-axis) + Revenue + Revenue LY (two lines) → verify LY line lags by 12 months
- Create a **Matrix:** Month (Rows) × Revenue, Revenue YTD, Revenue LY, YoY % (Values)
- Add a **Line Chart** with Revenue + 3M Moving Average → verify the smoothing effect
- Format YoY % and MoM % as Percentage with 1 decimal place
- Save

---

## Session 19 — Key Takeaways

1. **Three prerequisites:** Date table + Mark as Date Table + Active relationship
2. **TOTALYTD/QTD/MTD** for cumulative period calculations
3. **SAMEPERIODLASTYEAR** for same-period-last-year comparisons
4. **DATEADD** for flexible period shifts (days, months, quarters, years)
5. **Running totals** use CALCULATE + FILTER on ALL dates up to current
6. **Moving averages** smooth trends — use DATESINPERIOD + AVERAGEX

---

## Preparation for Session 20
- Review all measures created so far
- Think about: What KPIs does your organization track monthly/quarterly/yearly?
- Consider: How would you build a Profit & Loss statement in Power BI?

---

*Session 19 of 30 | Module 4: DAX Fundamentals*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
