# Session 20: AI for Data Analysis
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 4 — BUSINESS APPLICATIONS                                            │
│  SESSION 20 of 30  |  1 Hour  |  30% Theory + 70% Hands-On                 │
│                                                                              │
│  "Data tells you what happened. AI helps you understand why,                │
│   and communicate it to people who need to act on it."                      │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 20, you will be able to:

- Use ChatGPT Code Interpreter (Advanced Data Analysis) for data exploration
- Generate Python, SQL, and Excel analysis code on demand
- Interpret and communicate data insights to non-technical audiences
- Build data storytelling narratives from raw analysis outputs
- Apply AI to dashboard design briefs and KPI framework creation
- Understand the limits of AI in statistical analysis and data science

---

## 1. AI's Role in Data Work

### 1.1 The Data Skills Gap in Business

```
REALITY IN MOST ORGANIZATIONS:
  ▸ Most business decisions require data analysis
  ▸ Only ~15–20% of business professionals can write SQL or Python
  ▸ Business analysts spend ~40% of time on data wrangling (not insight)
  ▸ Data scientists spend ~60% of time on data cleaning and prep
  ▸ ~70% of data projects fail to deliver actionable insights to decision-makers

THE AI BRIDGE:
  ✓ Non-technical users can now generate analysis code in natural language
  ✓ Data analysts can automate repetitive wrangling with AI-generated scripts
  ✓ Insights can be translated from jargon to business narrative automatically
  ✓ Any professional can build an analysis in Excel using AI-generated formulas
  ✓ Data scientists can focus on complex modeling while AI handles boilerplate
```

### 1.2 The Three Modes of AI Data Work

```
MODE 1 — AI AS ANALYST (ChatGPT Code Interpreter):
  Upload your data file → ask questions in plain English →
  AI writes code, runs it, shows charts → You interpret and act
  Best for: exploratory analysis, quick insights, non-coders

MODE 2 — AI AS CODE GENERATOR (ChatGPT/Claude):
  Describe the analysis → AI generates Python/SQL/Excel code →
  You copy, run, and verify in your own environment
  Best for: analysts who need code fast, repeatable scripts, automation

MODE 3 — AI AS TRANSLATOR (ChatGPT/Claude/Gemini):
  Paste analysis outputs → AI writes the business narrative →
  You verify and refine
  Best for: communicating data to non-technical audiences, reports, slides
```

---

## 2. ChatGPT Code Interpreter — Advanced Data Analysis

### 2.1 What it Does

ChatGPT's "Advanced Data Analysis" (Code Interpreter) feature allows you to:
- Upload CSV, Excel, or other data files directly into the chat
- Ask questions in plain English
- ChatGPT writes Python code, executes it in a sandboxed environment, and shows you the results including charts and visualizations

**Access:** ChatGPT Plus (paid) → "Advanced Data Analysis" mode

### 2.2 The Data Exploration Workflow

**Step 1: Upload and Orient**
```
PROMPT (after uploading your data file):
"I've uploaded a dataset. First:
1. Describe the structure: number of rows, columns, column names and data types
2. Show me the first 5 rows
3. Identify any obvious data quality issues (missing values, wrong types, outliers)
4. Tell me what questions this data is well-suited to answer"
```

**Step 2: Exploratory Analysis**
```
PROMPT:
"Now perform an exploratory analysis:
1. Summary statistics for all numerical columns (mean, median, min, max, std)
2. Distribution of [KEY CATEGORICAL COLUMN] show as a bar chart
3. Trend of [KEY METRIC] over time show as a line chart
4. Correlation between [COLUMN A] and [COLUMN B] show as a scatter plot
5. Top 10 [ENTITY — customers / products / regions] by [METRIC]

For each chart: add a title, clear axis labels, and a 1-sentence interpretation."
```

**Step 3: Specific Business Question**
```
PROMPT:
"Answer this specific business question using the data:
[YOUR SPECIFIC QUESTION e.g., 'Which product category has the highest
customer return rate and what is the trend over the last 6 months?']

Show:
1. The relevant data subset
2. The calculation/analysis
3. A visualization if helpful
4. A plain-English summary of the finding
5. What further analysis would strengthen this finding"
```

**Step 4: Data Cleaning**
```
PROMPT:
"Clean this dataset for analysis:
1. Remove duplicate rows (show count of duplicates removed)
2. Handle missing values in [COLUMN]: [fill with median / drop rows / flag]
3. Convert [COLUMN] from [current format] to [desired format]
4. Create a new column: [DESCRIPTION OF DERIVED COLUMN]
5. Export the cleaned dataset as a CSV

Show me a before/after comparison of the data quality metrics."
```

---

## 3. AI as Code Generator — Python, SQL, Excel

### 3.1 Python Data Analysis Scripts

**Template for any pandas analysis:**
```
PROMPT:
Write a Python script for this data analysis task.

Dataset: [DESCRIBE YOUR DATA — columns, format, approximate size]
Task: [DESCRIBE WHAT YOU WANT TO ANALYZE]
Output required: [TABLE / CHART / BOTH / EXPORTED FILE]

Requirements:
- Use pandas for data manipulation
- Use matplotlib and/or seaborn for visualization
- Include a function structure (not just procedural code)
- Add comments explaining each major step
- Include: data loading, cleaning check, analysis, visualization, export
- Print a human-readable summary of key findings at the end

Python version: 3.10+
After the code, provide:
1. pip install commands for all libraries needed
2. One line explanation of the most complex part of the code
3. How to adapt this for [COMMON VARIATION]
```

**High-value Python analysis templates to request:**

```python
# 1. SALES TREND ANALYSIS
"Write a Python script to analyze monthly sales trends from a CSV with
columns: date, product_id, product_name, category, quantity, revenue, region.
Show: monthly revenue trend, top 5 products by revenue, regional breakdown.
Export: summary statistics CSV and 3 charts as PNG files."

# 2. CUSTOMER COHORT ANALYSIS
"Write a Python script to perform customer cohort analysis from transaction data.
CSV columns: customer_id, transaction_date, transaction_amount.
Calculate: monthly cohort retention rates. Output: cohort heatmap."

# 3. CHURN PREDICTION FEATURES
"Write a Python script to calculate churn risk features for each customer.
CSV columns: customer_id, signup_date, last_purchase_date, total_orders, 
total_spend, support_tickets.
Create features: days_since_last_purchase, avg_order_value, order_frequency.
Flag customers as HIGH/MEDIUM/LOW churn risk based on recency."

# 4. MARKET BASKET ANALYSIS
"Write a Python script to find which products are frequently purchased together.
CSV columns: order_id, product_name.
Use: Apriori algorithm (mlxtend library).
Output: top 20 product association rules by confidence."
```

### 3.2 SQL for Data Analysis

**SQL Analysis Generator Template:**
```
PROMPT:
Write SQL queries for the following data analysis tasks.

Database: [PostgreSQL / MySQL / BigQuery / Snowflake / SQL Server]
Schema context:
  Table: [TABLE NAME]
  Columns: [LIST COLUMNS WITH TYPES]
  [Add more tables if joins are needed]

Queries needed:
1. [ANALYSIS TASK 1]
2. [ANALYSIS TASK 2]
3. [ANALYSIS TASK 3]

For each query:
- Write the complete SQL
- Add inline comments explaining complex parts
- Note the expected output structure
- Suggest an index that would improve performance (if applicable)

After all queries, write one "master query" that combines the key metrics
into a single result set suitable for a dashboard or reporting tool.
```

**High-value SQL patterns for finance/ops:**
```sql
-- 1. RUNNING TOTAL / CUMULATIVE SUM
"Write a SQL query showing monthly revenue with a running total YTD
and the % of annual target achieved each month."

-- 2. PERIOD-OVER-PERIOD COMPARISON
"Write a SQL query comparing revenue this month vs same month last year
and vs previous month, with % change for each comparison."

-- 3. CUSTOMER RFM ANALYSIS (Recency, Frequency, Monetary)
"Write a SQL query to calculate RFM scores for all customers.
Segment them into: Champions, Loyal, At Risk, Lost."

-- 4. ROLLING AVERAGE
"Write a SQL query showing 3-month and 6-month rolling average sales
for each product category."

-- 5. RANK AND TOP-N
"Write a SQL query showing the top 3 salespeople by revenue in each region
for each quarter, using window functions."
```

### 3.3 Excel Advanced Formula Generation

```
PROMPT:
Generate Excel formulas for the following analysis tasks.
My Excel version: [Excel 365 / Excel 2019 / Google Sheets]

Dataset structure:
  Sheet name: [SHEET NAME]
  Headers in row 1: [LIST COLUMN HEADERS]
  Data starts in row 2

Formulas needed:
1. [FORMULA TASK 1]
2. [FORMULA TASK 2]
3. [FORMULA TASK 3]

For each formula:
- Write the complete formula syntax
- Explain in plain English how it works
- Note any array-formula requirements (Ctrl+Shift+Enter)
- Provide a simpler alternative if the formula is complex

Also suggest: which of these analyses would benefit from a Pivot Table
instead, and describe the Pivot Table setup.
```

---

## 4. Data Storytelling — Translating Insights to Business Narrative

### 4.1 The Data Narrative Framework

Raw analysis output is not a business insight. The insight comes from interpreting what the data means in context and communicating it in a way that drives action.

```
RAW ANALYSIS OUTPUT:
  "Revenue in Q3: ₹42.5 Cr. Budget: ₹45.0 Cr. Variance: -₹2.5 Cr (-5.6%).
   Product category A: -12%. Category B: +8%. Region South: -18%."

DATA NARRATIVE (what decision-makers need):
  "Q3 revenue missed budget by 5.6% driven entirely by performance in
   South region and Category A, which together account for 85% of the shortfall.
   Category B and all other regions are tracking ahead of plan.
   The implication: this is a concentrated geographic and product issue,
   not a broad market problem. A focused intervention in South region distribution
   and Category A promotion strategy could recover the gap in Q4."
```

### 4.2 The Data Narrative Prompt

```
PROMPT:
You are a Business Intelligence Director who translates data into business stories
for non-analytical audiences.

Here is the output of my data analysis:
[PASTE YOUR ANALYSIS OUTPUT — numbers, table, or chart description]

Context:
  Audience: [WHO WILL READ THIS — role, decision-making power]
  Business question this analysis answers: [THE QUESTION]
  Decision to be made based on this: [WHAT DECISION THIS INFORMS]

Write a data narrative using this structure:

THE HEADLINE (1 sentence):
  State the single most important finding as an assertion.
  Not "Q3 revenue was ₹42.5 Cr" but what it MEANS.

THE STORY (2–3 sentences):
  What does the data show? What pattern or trend is most significant?
  Compare to context: prior period, target, industry benchmark.

THE "SO WHAT" (1–2 sentences):
  What does this mean for the business? What is at stake?

THE RECOMMENDATION (1 sentence):
  What specific action does this analysis point to?

THE CAVEAT (1 sentence, if applicable):
  What limitation of this data should the audience know?

Rules:
- Translate numbers into implications: not "revenue declined 12%" but
  "at this rate, we will miss our annual target by [amount]"
- Avoid jargon: no "statistically significant," "p-value," "heteroscedasticity"
- Under 200 words total
```

### 4.3 The "Explain This Chart" Prompt

```
PROMPT:
I have a chart showing [DESCRIBE THE CHART — type, axes, data it shows].

Key observations from the chart:
1. [OBSERVATION 1]
2. [OBSERVATION 2]
3. [OBSERVATION 3 if applicable]

Write a 3-sentence chart annotation / talking point:
- Sentence 1: What the chart shows (the finding)
- Sentence 2: Why this is significant (the so-what)
- Sentence 3: What action or question this raises

Audience: [Non-technical executive / Technical analyst / External client]
Tone: [Executive briefing / Analytical report / Board presentation]
```

---

## 5. KPI Framework Design with AI

### 5.1 KPI Framework Generator

```
PROMPT:
You are a Strategy and Analytics consultant designing a KPI framework.

Design a comprehensive KPI framework for:
Function / Department: [SALES / MARKETING / OPERATIONS / HR / FINANCE]
Company type: [DESCRIBE — size, industry, stage]
Strategic priorities: [LIST 3–4 PRIORITIES FOR THIS PERIOD]

For each strategic priority, generate 2–3 KPIs:

KPI NAME: [Clear, measurable name]
DEFINITION: [Exactly how it is calculated formula if applicable]
DATA SOURCE: [Where this data lives system, table, process]
MEASUREMENT FREQUENCY: [Daily / Weekly / Monthly / Quarterly]
TARGET: [Describe how the target should be set not a specific number]
RAG STATUS: [Describe Green / Amber / Red threshold logic]
OWNER: [Role responsible for this KPI]
WHY IT MATTERS: [1 sentence — business impact of this metric]
LEADING OR LAGGING: [Indicate which]

After the KPI table, provide:
- 1 "vanity metric" to avoid for each priority (and why)
- Recommended dashboard layout grouping these KPIs
```

### 5.2 Dashboard Design Brief

```
PROMPT:
Write a dashboard design brief for a [TYPE] dashboard.

Purpose: [Who will use this, for what decisions, how frequently]
Data sources: [List the systems or tables that will feed this dashboard]
Key questions this dashboard must answer: [LIST 3–5 QUESTIONS]

For each key question, specify:
VISUALIZATION TYPE: [Bar chart / Line chart / KPI card / Table / Heatmap / Gauge]
METRIC SHOWN: [What exactly is being measured]
DIMENSIONS / FILTERS: [How users will filter the data by time, region, product]
BENCHMARK REFERENCE: [What to compare against target, prior period, industry]

Layout recommendation:
- Top row: [3–4 headline KPI cards — the numbers at a glance]
- Middle: [Primary trend charts]
- Bottom: [Detail table or breakdown charts]

Tool recommendation: [Power BI / Tableau / Google Looker Studio / Excel / Metabase]
Justify the recommendation based on the stated data sources and audience.
```

---

## 6. Real-World Example: Netflix's Data-Driven Content Decisions

**Company:** Netflix — streaming platform, 260+ million subscribers globally

**How Netflix Uses AI + Data Analysis:**

```
THE CHALLENGE:
  Netflix produces hundreds of original shows annually.
  Content investment decisions ($15–200M per show) need data-backed justification.
  Traditional metrics (viewer numbers) are not sufficient to predict success.

AI + DATA ANALYTICS IN PRACTICE:

  1. CONTENT RECOMMENDATION ENGINE:
     AI analyzes 200+ signals per user (watch time, pauses, rewatches,
     search behavior, device, time of day) to predict what content
     each user will watch next.
     Business value: 75% of viewer activity is AI-recommended content.

  2. CONTENT INVESTMENT DECISIONS:
     Data teams analyze: genre performance by region, optimal episode length,
     optimal season length, release timing, thumbnail A/B tests (millions/day)
     AI models: predict expected viewership before greenlight

  3. DATA STORYTELLING FOR LEADERSHIP:
     Analytics team translates complex model outputs into business narratives
     for content leadership who are not data scientists.
     "This show's viewership in first 28 days indicates a 68% probability
     of renewal-worthy performance" → becomes a business decision framework.

  4. AI-ASSISTED ANALYSIS:
     Data analysts use AI to write boilerplate analysis code (pandas, SQL),
     accelerating the time from data question to insight by 40–60%.
```

**The lesson for this session:** Netflix's data success is NOT just about having great data or great algorithms. It is about the humans who can ask the right questions, interpret the outputs, and translate them into business decisions. That translation work data → narrative → decision is exactly what this session has equipped you to do.

---

## 7. Responsible AI in Data Analysis

### 7.1 Critical Limitations to Know

```
AI LIMITATIONS IN DATA ANALYSIS:

1. AI CANNOT SEE YOUR DATA UNLESS YOU SHARE IT
   (In non-Code Interpreter mode, you must describe or paste the data)

2. AI CAN MAKE ARITHMETIC ERRORS
   Verify every number AI produces through independent calculation

3. AI CANNOT HANDLE VERY LARGE DATASETS IN CONTEXT WINDOW
   For large datasets, Code Interpreter is better than text prompts

4. AI DOES NOT KNOW YOUR BUSINESS CONTEXT
   "Revenue declined" is not necessarily bad — AI cannot know your seasonality

5. AI CORRELATION ≠ CAUSATION UNDERSTANDING
   AI may identify correlations but cannot determine business causality

6. AI GENERATED CODE MAY HAVE BUGS
   Always test code on a sample before running on full dataset

7. CONFIDENTIAL DATA PROTECTION
   Never upload confidential company data to public AI tools (ChatGPT, Claude)
   Use enterprise versions (Azure OpenAI, Copilot Enterprise) for sensitive data
```

### 7.2 The Data Analysis Verification Protocol

```
Before using any AI-generated analysis professionally:

☐ VERIFY NUMBERS: Spot-check 3–5 calculations independently
☐ VERIFY CODE: Run on sample data first; review logic before full run
☐ VERIFY INTERPRETATION: Does the narrative match what the data actually shows?
☐ VERIFY COMPLETENESS: What did AI NOT analyze that you should?
☐ VERIFY CONTEXT: Have you told AI about seasonality, industry norms, prior events?
☐ DATA PRIVACY: Was any personally identifiable data included? Remove it.
☐ ATTRIBUTION: If sharing, note that AI assisted in the analysis
```

---

## 8. Hands-On Lab 20: Data Analysis Sprint

**Objective:** Perform a data analysis workflow using AI from question to narrative  
**Duration:** 25 minutes  
**Tool:** ChatGPT (Code Interpreter preferred for Task 1)

---

### Task 1: Data Exploration with Code Interpreter (10 minutes)

**Option A (with Code Interpreter):**
Download a free sample dataset (e.g., from Kaggle or use a CSV of public data e.g., India state-wise population data, or a public sales dataset). Upload to ChatGPT Code Interpreter. Use the 4-step exploration workflow (Orient → Explore → Specific Question → Clean).

**Option B (without Code Interpreter):**
Use this fictional dataset description:
```
Sales data: 12 months, 4 product categories (Electronics, Clothing, Home, Food),
5 regions (North, South, East, West, Central), Monthly revenue and units sold.

Key facts:
  Total annual revenue: ₹180 Crore
  Electronics: 45% of revenue, declining 8% in last quarter
  Clothing: 25% of revenue, growing 15% YoY
  South region: 30% below target across all categories
  December spike: 40% above average monthly revenue
```

Ask ChatGPT: "Based on this dataset description, what are the 3 most important business questions I should investigate? For each question, tell me what analysis to run and what chart to use."

---

### Task 2: Generate Analysis Code (7 minutes)

Choose ONE:
- **Python:** Write a pandas script that calculates monthly revenue growth rate from a CSV with columns: Month, Category, Revenue
- **SQL:** Write a query showing top 3 products by revenue in each region for the last quarter
- **Excel:** Generate formulas to calculate: (1) quarter-to-date total, (2) % vs same quarter last year, (3) rank among all products

Use the appropriate code generator prompt. Review the output does the logic look correct?

---

### Task 3: Data Narrative (8 minutes)

Using the fictional data from Task 1 (Option B), use the Data Narrative Prompt to write a business narrative.

Your analysis findings:
- Electronics is declining; Clothing is the growth story
- South region is the main drag on performance
- December seasonality is extreme plan accordingly

Write a 150-word narrative for a CEO who needs to make Q4 resource allocation decisions.

---

### Lab Evaluation Rubric

| Task | Marks |
|------|-------|
| Task 1: 3 business questions + analysis approach identified | 3 |
| Task 2: Analysis code generated + logic review written | 4 |
| Task 3: 150-word data narrative with all 5 elements | 3 |
| **Total** | **10** |

---

## 9. Module 4 Review — What You Can Now Do

```
MODULE 4: BUSINESS APPLICATIONS — CAPABILITY SUMMARY

SESSION 16 ✓ AI for Marketing
  → Brand Voice Card, social media at scale, 4-step SEO blog workflow
  → Ad copy A/B variations, email sequences, content repurposing

SESSION 17 ✓ AI for Human Resources
  → Inclusive JDs + bias audit, structured interview frameworks
  → Performance review narratives, 360 synthesis, onboarding plans
  → Responsible AI in HR: no PII, no auto-screening, legal review

SESSION 18 ✓ AI for Finance & Accounting
  → Financial narrative, variance analysis, board pack commentary
  → Excel formulas, Python scripts, SQL queries for finance
  → Concept translation, assumption documentation

SESSION 19 ✓ AI for Customer Support
  → HEARD framework, 8 response types, template library
  → FAQ and knowledge base creation, chatbot design

SESSION 20 ✓ AI for Data Analysis
  → Code Interpreter workflow, Python/SQL/Excel code generation
  → Data narrative framework, KPI design, dashboard briefs
  → Responsible data AI: verification protocol, confidentiality
```

---

## 10. Interview Questions — Session 20

**Q1:** *"How do you use AI for data analysis in a business context?"*

**Strong Answer:**
"I use AI in three ways for data work. First, for code generation I describe the analysis I need in plain English and AI writes the Python, SQL, or Excel formula. I then verify the logic, test on sample data, and run it. This eliminates 70–80% of the time I'd spend writing boilerplate. Second, for Code Interpreter exploratory analysis I upload a dataset and ask business questions in plain language. AI writes and executes the Python code, shows me charts, and I focus on interpreting the findings. Third, for data narrative writing I take my analysis outputs and use a structured prompt to convert them into a business narrative with headline, story, so-what, recommendation, and caveat. This bridges the gap between the analysis and the decision-maker. The key discipline: verify every number AI produces before using it professionally, and never upload confidential data to public AI tools."

---

## 11. Revision Questions — Session 20

1. What are the three modes of AI data work? Describe each with an example use case.
2. What are the 4 steps of the Code Interpreter data exploration workflow?
3. What is the Data Narrative Framework? What are the 5 elements and what does each accomplish?
4. Write a prompt to generate a Python script for monthly sales trend analysis from a CSV file.
5. What SQL pattern would you use for period-over-period comparison? What window functions are typically involved?
6. What is a KPI framework? What 8 attributes should every KPI have in the framework?
7. List 7 limitations of AI in data analysis. For each, what is the corresponding safeguard?
8. How did Netflix use AI and data analysis to improve content investment decisions? What is the lesson for analysts?

---

## 12. Key Terminology — Session 20

| Term | Definition |
|------|-----------|
| **Code Interpreter** | ChatGPT's Advanced Data Analysis feature that uploads, runs code, and shows results |
| **Exploratory Data Analysis (EDA)** | Initial investigation of a dataset to discover patterns, anomalies, and structure |
| **Data Narrative** | A written story translating analysis outputs into business-relevant insight |
| **KPI Framework** | A structured set of key performance indicators aligned to strategic priorities |
| **Dashboard Design Brief** | A specification document defining what a dashboard must show and for whom |
| **Cohort Analysis** | Grouping customers by a shared characteristic (sign-up month) and tracking behavior over time |
| **RFM Analysis** | Recency, Frequency, Monetary a customer segmentation framework |
| **Window Function (SQL)** | SQL functions that perform calculations across related rows (RANK, LAG, RUNNING SUM) |
| **Data Wrangling** | The process of cleaning, transforming, and structuring raw data for analysis |

---

## 13. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 20 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  3 modes: AI as Analyst (Code Interpreter), Code Generator, Translator  │
│  ✓  Code Interpreter: Orient → Explore → Specific Q → Clean                │
│  ✓  Code generation: Python / SQL / Excel — describe task, verify output    │
│  ✓  Data Narrative: Headline → Story → So What → Recommendation → Caveat   │
│  ✓  KPI Framework: 8 attributes per KPI including owner and RAG logic       │
│  ✓  7 limitations: verify all numbers, test code, protect confidential data │
│  ✓  Netflix: AI handles recommendation + prediction; humans ask questions   │
│     and translate insights to decisions                                      │
│                                                                              │
├──────────────────────────────────────────────────────────────────────────────┤
│  MODULE 4 COMPLETE — YOU CAN NOW USE AI FOR:                                 │
│  ✓ Marketing content at scale (brand voice, social, blog, ad copy)          │
│  ✓ HR documents (JDs, interviews, reviews, onboarding, policy)              │
│  ✓ Finance narratives, formulas, code, concept translation                  │
│  ✓ Customer support (HEARD, templates, FAQs, chatbot design)                │
│  ✓ Data analysis (exploration, code, narrative, KPIs, dashboards)           │
├──────────────────────────────────────────────────────────────────────────────┤
│  NEXT MODULE:                                                                │
│  Module 5 — Creative AI & Automation (Sessions 21–25)                       │
│  "AI for image generation, video/audio, building AI assistants,            │
│   workflow automation, and advanced prompt pipelines"                        │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 20 Complete | Module 4 Complete | Next: Session 21 — AI Image Generation*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
