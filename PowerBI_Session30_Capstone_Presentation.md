# Session 30 — Capstone Presentation & Certification
## Module 6: Power BI Service & Capstone | Professional Power BI Certification
### Duration: 1 Hour | Type: Presentation + Review | Final Session

---

## Learning Objectives
By the end of this session, you will be able to:
1. Present a complete BI solution confidently to stakeholders
2. Demonstrate the end-to-end Power BI workflow live
3. Articulate business insights derived from your dashboard
4. Answer questions about data model, DAX, and design decisions
5. Receive feedback and identify areas for continued learning

---

## 30.1 Presentation Structure

### Recommended Flow (5–10 minutes)

| Section | Duration | Content |
|---------|----------|---------|
| **1. Business Context** | 1 min | What problem does this dashboard solve? Who is the audience? |
| **2. Data & Model** | 1–2 min | Data sources, Power Query steps, Star Schema overview |
| **3. DAX Highlights** | 1 min | Key measures: Time Intelligence, KPIs, CALCULATE usage |
| **4. Live Demo** | 3–4 min | Walk through dashboard pages, demo interactivity |
| **5. Key Insights** | 1 min | 2–3 business insights discovered from the data |
| **6. Recommendations** | 30 sec | What action should the business take based on these insights? |
| **Q&A** | 2–3 min | Answer evaluator/audience questions |

---

## 30.2 Presentation Script Template

### Section 1: Business Context

```
"The [Company/Department] needs to understand [business problem].
Currently, decisions are made using [spreadsheets / gut feeling / delayed reports].

This dashboard provides [VP of Sales / Regional Managers / Operations Team]
with real-time visibility into [Revenue, Profitability, Customer Trends].

The key question this dashboard answers is:
'[State the core business question]'"
```

### Section 2: Data & Model

```
"I connected to [2-3] data sources:
- [Sales transactions from Excel — 10,000 rows]
- [Product catalog from CSV — 200 products]
- [Date table generated with DAX CALENDARAUTO]

In Power Query, I:
- Cleaned [X issues: nulls, wrong types, duplicates]
- Applied [Y transformations: unpivot, merge, rename]

The data model follows a Star Schema:
- Fact table: Sales (transactions)
- Dimensions: Products, Customers, Regions, Date
- All relationships are One-to-Many with single cross-filter direction"
```

### Section 3: DAX Highlights

```
"I created [X] DAX measures including:
- Core KPIs: Revenue, Profit, Margin %, Order Count
- Time Intelligence: YTD, Year-over-Year, Month-over-Month
- Advanced: Revenue % of Total using CALCULATE with ALL
- Conditional formatting measures for the scorecard

For example, the YoY measure uses SAMEPERIODLASTYEAR
to compare current performance against the prior year,
and the result dynamically changes based on slicer selections."
```

### Section 4: Live Demo

**Demo Checklist — show each of these:**

| # | Demo Action | What It Shows |
|---|------------|---------------|
| 1 | Open Page 1 — point out KPI cards | Information hierarchy |
| 2 | Click a slicer value (Region) | Cross-filtering across all visuals |
| 3 | Click a bar in the chart | Visual interactions |
| 4 | Toggle Chart ↔ Table (Bookmark) | Bookmark functionality |
| 5 | Right-click a category → Drill through | Drill-through navigation |
| 6 | Click Back button | Navigation |
| 7 | Hover over a data point | Custom tooltip page |
| 8 | Point out conditional formatting | Color-coded matrix/table |
| 9 | Click Reset button | Bookmark-based filter reset |
| 10 | Show Model View briefly | Star Schema structure |
| 11 | Switch to Power BI Service | Published report + Dashboard |
| 12 | (Optional) Show RLS — View as Roles | Security filtering |

### Section 5: Key Insights

```
"From this analysis, three key insights emerged:

1. [Revenue grew 12% YoY, primarily driven by the Electronics
   category which accounts for 35% of total revenue]

2. [The West region is underperforming by 15% against target,
   while North and South exceed targets by 5-8%]

3. [Top 5 products contribute 60% of revenue — high concentration
   risk if any of these products face supply issues]"
```

### Section 6: Recommendations

```
"Based on these insights, I recommend:

1. [Investigate West region — possible staffing, pricing, or
   market issues need attention]

2. [Diversify product portfolio — reduce dependency on top 5]

3. [Expand the Monday promotion nationally — it drove 35%
   higher sales in the pilot regions]"
```

---

## 30.3 Answering Q&A Questions

### Common Evaluator Questions and How to Answer

| Question | How to Answer |
|----------|--------------|
| "Why did you choose this chart type?" | "A bar chart is ideal for comparing categories. I avoided a pie chart because there are more than 5 categories." |
| "How does your measure respond to filters?" | "This is an explicit measure with filter context. When a slicer is applied, CALCULATE adjusts the evaluation context." |
| "What happens if the data source changes?" | "Power Query steps are recorded. On refresh, the same cleaning pipeline runs automatically on new data." |
| "How do you ensure data security?" | "I implemented RLS with [static/dynamic] roles. Regional managers see only their region's data." |
| "Can this be automated?" | "Yes — scheduled refresh runs up to 8x/day on Pro. Data gateway connects on-premises sources." |
| "What would you add with more time?" | "I would add [forecasting, more drill-through pages, mobile layout, alerts, subscriptions]." |
| "How did you validate the data?" | "I compared grand totals against the source file, checked for nulls in key columns, and tested RLS filtering." |
| "Why Star Schema?" | "Power BI's VertiPaq engine is optimized for Star Schema. It gives the best performance, simplest DAX, and cleanest filter flow." |

---

## 30.4 Presentation Best Practices

### Do's

| Practice | Why |
|----------|-----|
| **Start with the business problem** | Audience cares about "why" before "how" |
| **Show, don't tell** | Live demo > screenshots > bullet points |
| **Keep it under 10 minutes** | Respect the audience's time |
| **Prepare for failures** | Have screenshots or a backup PDF in case of connectivity issues |
| **Practice once** | Time yourself, catch awkward transitions |
| **Make eye contact** | Look at the audience, not the screen |
| **End with a clear recommendation** | "Here's what the data tells us we should do" |

### Don'ts

| Avoid | Why |
|-------|-----|
| **Don't read from slides** | You built this — speak naturally |
| **Don't explain every DAX formula** | Show 1–2 key measures; the code is in the file |
| **Don't apologize for what's missing** | Focus on what you built |
| **Don't demo everything** | Pick 3–4 best features to demonstrate |
| **Don't rush the insights** | This is the most valuable part — give it time |
| **Don't use jargon without context** | Say "Year-over-Year growth" not "SAMEPERIODLASTYEAR" |

---

## 30.5 Peer Review Feedback Form

### For Audience Members / Evaluators

| Criterion | Score (1-5) | Comments |
|-----------|------------|----------|
| **Business problem clearly defined** | | |
| **Data model is well-structured (Star Schema)** | | |
| **DAX measures are appropriate and correct** | | |
| **Dashboard design is clean and professional** | | |
| **Interactivity works (slicers, drill-through)** | | |
| **Advanced features demonstrated (Bookmarks, RLS, Conditional Formatting)** | | |
| **Insights are meaningful and actionable** | | |
| **Presentation was clear and within time limit** | | |
| **Questions answered confidently** | | |
| **Overall impression** | | |

**Total Score: ___ / 50**

**Strengths:**

**Areas for Improvement:**

---

## 30.6 Course Completion — Skills Summary

### What You Can Now Do

| Module | Skills Acquired |
|--------|----------------|
| **Module 1: BI Fundamentals** | Connect to 150+ data sources, import Excel/CSV/Web, clean data in Power Query |
| **Module 2: Data Modeling** | Build Star Schema, create relationships, Date tables, validate data |
| **Module 3: Visualization** | Charts, Maps, Cards, KPIs, Slicers, Drill-through, Dashboard design |
| **Module 4: DAX** | Calculated columns, Measures, CALCULATE, Time Intelligence, Business KPIs |
| **Module 5: Advanced Reporting** | Bookmarks, Conditional Formatting, RLS, Design principles, Executive dashboards |
| **Module 6: Service & Capstone** | Publish, Workspaces, Apps, Sharing, Alerts, Subscriptions, End-to-end project |

### Power BI Skill Matrix

```
Beginner ─────────────────────────── Advanced
│                                          │
│  Sessions 1-5:   ████████░░  Data Import │
│  Sessions 6-10:  ████████░░  Modeling    │
│  Sessions 11-15: ████████░░  Visuals     │
│  Sessions 16-20: ████████░░  DAX         │
│  Sessions 21-25: ████████░░  Advanced    │
│  Sessions 26-30: ████████░░  Service     │
│                                          │
│  You are here: ──────────────► Certified │
```

---

## 30.7 Continued Learning Path

### Immediate Next Steps

| Step | Action | Resource |
|------|--------|----------|
| 1 | **Practice daily** | Build dashboards for personal or work projects |
| 2 | **Get PL-300 certified** | Microsoft Certified: Power BI Data Analyst Associate |
| 3 | **Join the community** | community.powerbi.com — forums, challenges, samples |
| 4 | **Follow updates** | Power BI Blog (blog.powerbi.com) — monthly feature updates |
| 5 | **Explore advanced topics** | See below |

### Advanced Topics to Explore

| Topic | Description |
|-------|-------------|
| **Advanced DAX** | CALCULATE deep dive, virtual tables, context transition |
| **Performance Optimization** | DAX Studio, VertiPaq Analyzer, query reduction |
| **Dataflows** | Reusable Power Query in the cloud |
| **Paginated Reports** | Pixel-perfect, print-ready reports with Report Builder |
| **Power BI Embedded** | Embed reports in custom applications |
| **Power BI REST API** | Automate refresh, manage content programmatically |
| **Composite Models** | Mix Import + DirectQuery in one model |
| **AI Visuals** | Key Influencers, Decomposition Tree, Q&A, Smart Narratives |
| **Microsoft Fabric** | Unified analytics: lakehouse + data warehouse + BI |
| **Power BI Copilot** | AI-generated DAX, visuals, and narratives |

### PL-300 Certification Exam Topics

| Domain | Weight | Key Topics |
|--------|--------|-----------|
| **Prepare the Data (25-30%)** | Power Query, data sources, profiling, cleaning |
| **Model the Data (25-30%)** | Star Schema, relationships, DAX, calculated tables |
| **Visualize and Analyze (25-30%)** | Charts, formatting, drill-through, AI visuals, analytics |
| **Deploy and Maintain (15-20%)** | Workspaces, RLS, refresh, Apps, performance |

---

## 30.8 Course Feedback

### Reflection Questions

1. What was the most valuable skill you learned in this course?
2. Which session was the most challenging? How did you overcome it?
3. How will you apply Power BI in your current role?
4. What additional topics would you like to learn?
5. Would you recommend this course to a colleague? Why?

---

## 🔧 Session Activity: Capstone Presentations

**Duration:** Full session

### Schedule

| Time | Activity |
|------|----------|
| 0:00–0:05 | Introduction and presentation order |
| 0:05–0:45 | **Student presentations** (5–10 min each + Q&A) |
| 0:45–0:55 | **Peer feedback** and evaluator scoring |
| 0:55–1:00 | **Course wrap-up**, certificate information, next steps |

### Presentation Order

Each participant presents their capstone:
1. Open your dashboard in Power BI Service (or Desktop as backup)
2. Follow the presentation structure (Section 30.2)
3. Demo key features live
4. Share insights and recommendations
5. Answer 2–3 questions from evaluators/peers

### After Presentations

- Submit your `.pbix` file and documentation
- Complete the course feedback form
- Receive your **Professional Power BI Certification** from UpSkill Global Education Technologies Inc.

---

## Session 30 — Key Takeaways

1. **Present the story, not the tool** — business problem → insights → recommendations
2. **Live demo** is more impactful than screenshots — show slicers, drill-through, toggles
3. **Prepare for questions** — know your DAX, model design, and design decisions
4. **Practice once** — timing, flow, and transitions matter
5. **This is the beginning** — Power BI skills grow with practice and real-world application

---

## Module 6 Complete — Summary

| Session | Topic | Key Skill |
|---------|-------|-----------|
| 26 | Publishing Reports | Publish to Service, create dashboards, scheduled refresh |
| 27 | Workspace Management | Workspaces, roles, Apps, shared datasets, governance |
| 28 | Sharing & Collaboration | Share links, alerts, subscriptions, Teams/SharePoint embed |
| 29 | Capstone Build | End-to-end BI solution with all skills integrated |
| 30 | Capstone Presentation | Present, demo, insights, Q&A, certification |

---

## Full Course Summary — 30 Sessions

| Module | Sessions | Topic | Focus |
|--------|----------|-------|-------|
| **1** | 1–5 | BI Fundamentals | Data import, Power Query, types, interface |
| **2** | 6–10 | Data Modeling | Star Schema, relationships, validation |
| **3** | 11–15 | Visualization | Charts, maps, KPIs, slicers, dashboard design |
| **4** | 16–20 | DAX Fundamentals | Columns, measures, CALCULATE, time intelligence |
| **5** | 21–25 | Advanced Reporting | Bookmarks, conditional formatting, RLS, executive dashboard |
| **6** | 26–30 | Service & Capstone | Publish, share, collaborate, capstone project |

---

## Congratulations!

You have completed the **Professional Power BI Certification Course** — 30 sessions covering the complete Power BI workflow from data import to published, secured, interactive dashboards.

**Your next step:** Apply these skills to a real business problem. The best way to learn Power BI is to build something that matters.

---

*Session 30 of 30 | Module 6: Power BI Service & Capstone*
*Professional Power BI Certification — UpSkill Global Education Technologies Inc., Canada*
