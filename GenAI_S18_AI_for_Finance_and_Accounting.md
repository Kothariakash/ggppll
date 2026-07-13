# Session 18: AI for Finance & Accounting
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 4 — BUSINESS APPLICATIONS                                            │
│  SESSION 18 of 30  |  1 Hour  |  30% Theory + 70% Hands-On                 │
│                                                                              │
│  "AI does not replace financial judgment. It removes the hours spent        │
│   on the writing, formatting, and explaining that surround that judgment."  │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 18, you will be able to:

- Use AI to write financial narratives, variance analyses, and management commentary
- Generate Excel formulas, Python scripts, and SQL queries for financial analysis
- Use AI to explain complex financial concepts to non-financial stakeholders
- Create financial model documentation and assumption logs
- Apply responsible AI standards specifically to financial contexts
- Understand the critical distinction between AI-assisted writing and AI-generated numbers

---

## 1. The Critical Distinction in Finance AI

### 1.1 What AI Does Safely in Finance vs. What Requires Your Numbers

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  THE MOST IMPORTANT RULE IN FINANCE AI                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  AI IS SAFE FOR:                   AI IS RISKY FOR:                         │
│  ✓ Writing narrative around        ✗ Generating financial numbers           │
│    numbers YOU provide               (high hallucination risk)              │
│  ✓ Generating code/formulas        ✗ Interpreting data it cannot see        │
│    (verify before use)             ✗ Making investment recommendations      │
│  ✓ Explaining concepts             ✗ Providing regulatory compliance advice │
│  ✓ Structuring documents           ✗ Auditing financial statements          │
│  ✓ Summarizing reports             ✗ Any number it generates without a      │
│  ✓ Creating templates                source = VERIFY BEFORE USE             │
│                                                                              │
│  RULE: Finance professionals PROVIDE the numbers.                           │
│         AI WRITES ABOUT the numbers.                                         │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

**The hallucination risk in finance is especially high** because AI produces confident-sounding numbers. A hallucinated revenue figure or margin percentage in a financial document can have serious professional and legal consequences. Always: Your data → AI narrative. Never: AI data → your report.

---

## 2. Financial Narrative Writing

### 2.1 The Management Commentary / Business Review

The monthly management commentary explaining what happened financially and why is one of the most time-consuming tasks in finance. AI excels at this.

**Step 1: Provide your numbers (you do this)**
```
YOUR DATA INPUT (never generate this with AI):
  Revenue: ₹42.5 Crore (Budget: ₹45.0 Crore, Prior Year: ₹38.2 Crore)
  Gross Margin: 34.2% (Budget: 36.0%, Prior Year: 32.8%)
  EBITDA: ₹6.8 Crore (Budget: ₹7.2 Crore, Prior Year: ₹5.6 Crore)
  Key driver of revenue miss: Lower-than-expected retail channel volume
  Key driver of margin improvement vs. PY: Raw material cost reduction
  Key risk in next quarter: [YOU SPECIFY]
```

**Step 2: AI writes the narrative**
```
PROMPT:
You are a Chief Financial Officer writing a monthly management commentary
for the Board of Directors. Translate these financial results into a clear,
insightful narrative that explains performance and drives decisions.

FINANCIAL DATA (All numbers I am providing do not generate any numbers):
[PASTE YOUR NUMBERS AND CONTEXT]

Write a management commentary with these sections:

REVENUE PERFORMANCE:
  - State actual vs. budget vs. prior year (use the numbers I gave you)
  - Explain the key driver of any variance (use my explanation)
  - Assess: is this a structural or one-time variance?

MARGIN ANALYSIS:
  - Gross margin performance vs. budget and prior year
  - Key factor driving the change (from my data)
  - Implication for full-year margin outlook

EBITDA:
  - Actual vs. budget vs. prior year
  - Bridge: what drove the difference

OUTLOOK:
  - 1–2 sentences on key risks and opportunities ahead
  - Management's priority focus for next 30 days

Tone: Board-level authority. Direct, number-specific, no hedging.
Do not add any numbers I have not provided. Flag any gap as [DATA NEEDED].
Under 400 words.
```

---

### 2.2 Variance Analysis Narrative

For deep dives into specific variances:

```
PROMPT:
Write a variance analysis narrative for this line item.

Line item: [e.g., Marketing Expenditure]
Actual: [X]
Budget: [Y]
Variance: [Z — favorable or unfavorable]
Variance %: [%]
Key reasons for variance (from your knowledge):
  1. [REASON 1]
  2. [REASON 2]
  3. [REASON 3 if applicable]

Write:
1. HEADLINE: One sentence stating the variance and direction
   (Favorable/Unfavorable) with the exact numbers
2. EXPLANATION: 2–3 sentences explaining the reasons in priority order
3. ASSESSMENT: Is this temporary or structural? What is the implication
   for the full-year forecast?
4. ACTION: What management action (if any) is required or already planned?

Tone: Precise, factual, accountable. Finance professional speaking to audit committee.
Do not generate any numbers beyond what I have provided.
Under 150 words.
```

---

### 2.3 The Board Pack Executive Summary

```
PROMPT:
You are the CFO summarizing this month's financial pack for the Board.

Here are the key financial metrics and management commentary I have prepared:
[PASTE YOUR PREPARED COMMENTARY AND KEY NUMBERS]

Write a 1-page Board Pack Executive Summary:

Structure:
1. HEADLINE (1 sentence): Overall performance status this period
2. FINANCIAL PERFORMANCE (3–4 bullets): Revenue, margin, EBITDA vs. budget/PY
3. BUSINESS DRIVERS (2 bullets): Key factors explaining performance
4. RISKS AND OPPORTUNITIES (2 bullets): What to watch in the next 90 days
5. BOARD FOCUS ITEMS (2 bullets): What needs Board attention or decision

Rules:
- Every number from my data do not invent any figures
- Business-language, not accounting language
- Lead with the conclusion in every bullet (assertion format)
- Under 300 words
- Format: suitable for the first page of a Board pack
```

---

## 3. AI for Financial Formulas and Code

### 3.1 Excel Formula Generator

One of the most practical immediate uses of AI generating complex Excel formulas on demand:

```
PROMPT:
Generate an Excel formula for the following task:

I have a spreadsheet with:
Column A: Date (format: DD/MM/YYYY)
Column B: Product category (text: "Electronics", "Clothing", "Home")
Column C: Sales amount (number)
Column D: Region (text: "North", "South", "East", "West")

I want to calculate in cell F2:
The total sales amount where:
- Product category is "Electronics" AND
- Region is "North" AND
- Date is within Q3 2024 (July 1 – September 30, 2024)

Provide:
1. The Excel formula
2. A plain-English explanation of how it works
3. Any assumptions I should verify (e.g., date format)
4. An alternative approach if this formula is too complex for my Excel version
```

**Example complex formulas AI handles well:**
- XLOOKUP / VLOOKUP with error handling
- Dynamic arrays (FILTER, SORT, UNIQUE)
- Financial functions (NPV, IRR, XIRR, PMT)
- Date range calculations with SUMPRODUCT
- Conditional formatting formulas
- Power Query M code explanations

### 3.2 Python Financial Analysis Script

```
PROMPT:
Write a Python script to perform the following financial analysis task:

Task: [DESCRIBE WHAT YOU NEED TO DO]
Data available: [DESCRIBE YOUR DATA columns, format, size]
Desired output: [WHAT SHOULD THE SCRIPT PRODUCE]

Requirements:
- Use pandas for data manipulation
- Use matplotlib or plotly for any visualization
- Include comments explaining each major step
- Include error handling for common data issues (missing values, wrong types)
- Provide a function structure (not just procedural code)
- At the end: print a summary of the key findings in plain English

After the code, provide:
1. A list of libraries to install (pip install commands)
2. The one most common error a user might encounter and how to fix it
3. How to adapt this script for [A COMMON VARIATION OF THE TASK]
```

**Practical Python tasks for finance:**
```python
# Examples of high-value finance Python prompts:

"Write a Python script to calculate rolling 12-month revenue growth
from a CSV file with columns: Date, Revenue. Plot the result."

"Write a Python script to categorize bank transactions from a CSV by
merchant type using keyword matching. Output a pivot table by category."

"Write a Python script to calculate employee cost as % of revenue
from two CSV files: headcount.csv and financials.csv.
Join on month and produce a monthly trend chart."

"Write a Python function to calculate IRR given a list of cash flows.
Include validation that the cash flow sequence changes sign at least once."
```

### 3.3 SQL Query Generator for Finance

```
PROMPT:
Write a SQL query for the following financial analysis:

Database context:
  Table: transactions
  Columns: transaction_id, date, account_code, department, amount, currency, description
  
  Table: accounts
  Columns: account_code, account_name, account_type (Revenue/Expense/Asset/Liability)

Query I need:
  Monthly P&L by department for the current financial year (April 2024 – March 2025)
  Showing: Revenue, Cost of Sales, Gross Profit, Operating Expenses, EBITDA
  Grouped by: Month, Department
  Sorted by: Month ascending, Department alphabetically

Requirements:
  - Handle multi-currency by assuming all amounts are in INR (already converted)
  - Exclude inter-company transactions (account codes starting with '9')
  - Flag negative revenue as unusual (add a column: revenue_flag)
  - Database: PostgreSQL syntax

Provide:
1. The complete SQL query
2. Explanation of any complex joins or window functions used
3. How to add a YoY comparison column to this query
```

---

## 4. Explaining Financial Concepts to Non-Financial Audiences

### 4.1 The "Translate Finance" Prompt

One of the most valuable uses of AI in finance: bridging the gap between financial professionals and business leaders without financial training.

```
PROMPT:
You are a CFO who is excellent at explaining financial concepts to non-financial
audiences without dumbing them down.

Explain [FINANCIAL CONCEPT] to [AUDIENCE e.g., a marketing team, new employees,
a board member with no finance background].

Requirements:
- Use an everyday analogy to build intuition first
- Explain what it is in plain English (no jargon)
- Explain why it matters for business decisions
- Give one specific business example of this concept in action
- End with: "The key question to ask yourself about this is: [PRACTICAL QUESTION]"

Do not use: accounting jargon, technical formulas in the explanation section,
or assume prior financial knowledge.
Under 200 words.
```

**Examples of concepts to explain this way:**

| Concept | Non-Financial Audience |
|---------|----------------------|
| Working capital | Sales team |
| Cash conversion cycle | Operations managers |
| Contribution margin | Product managers |
| EBITDA | New hires |
| IRR | Department heads proposing capital investment |
| Burn rate | Non-finance startup team |
| Variance analysis | Marketing managers |
| Accounts receivable aging | Business development team |

### 4.2 The Financial Model Assumption Documenter

When building financial models, AI helps document assumptions clearly:

```
PROMPT:
I have built a financial model with these assumptions:
[LIST YOUR MODEL ASSUMPTIONS AS BULLET POINTS]

Write a model assumption log for this financial model:

For each assumption, document:
ASSUMPTION: [The assumption stated clearly]
BASIS: [Why this assumption was chosen market data, management judgment, historical trend]
SENSITIVITY: HIGH / MEDIUM / LOW how much does the output change if this is wrong?
RISK: If this assumption proves incorrect, the effect would be: [DESCRIBE]
SOURCE: [Where this data came from flag as [VERIFY] if not confirmed]

Format as a table.
After the table, write a 2-sentence "Model Limitations" statement for the front page.
```

---

## 5. Financial Reporting Automation

### 5.1 Automated Monthly Report Template

Build once, reuse every month with updated numbers:

```
PROMPT (TEMPLATE save in your prompt library):

[MONTHLY MANAGEMENT REPORT TEMPLATE ID: FIN-001]

You are the CFO of [COMPANY TYPE]. Write the monthly management report commentary 
for [MONTH YEAR].

All numbers below are final and verified use them exactly as provided:

INCOME STATEMENT HIGHLIGHTS:
  Revenue: Actual [___] | Budget [___] | Prior Year [___]
  Variance vs Budget: [___] ([___]%) — [Favorable/Unfavorable]
  Gross Profit: Actual [___] | Budget [___] | Prior Year [___]
  Gross Margin %: Actual [___]% | Budget [___]% | Prior Year [___]%
  EBITDA: Actual [___] | Budget [___] | Prior Year [___]

KEY BUSINESS DRIVERS:
  Revenue variance explained by: [YOUR EXPLANATION]
  Margin movement explained by: [YOUR EXPLANATION]
  
BALANCE SHEET HIGHLIGHTS:
  Cash position: [___] (vs [___] last month)
  Debtors: [___] (DSO: [___] days vs target [___] days)
  Creditors: [___] (DPO: [___] days)

OUTLOOK:
  Next month revenue forecast: [___]
  Key risk: [YOUR TEXT]
  Key opportunity: [YOUR TEXT]

Write a 350-word management commentary using the structure:
(1) Performance Summary | (2) Revenue Analysis | (3) Margin Analysis | 
(4) Cash and Working Capital | (5) Outlook

Board-level tone. Specific. No numbers beyond what I provided.
```

---

## 6. Real-World Example: JP Morgan's AI in Finance

**Company:** JPMorgan Chase global financial services firm, $4+ trillion in assets

**The COIN Platform (Contract Intelligence):**
JPMorgan built an AI platform called COIN (Contract Intelligence) to analyze commercial loan agreements.

```
TRADITIONAL PROCESS:
  Legal and finance teams manually reviewed:
  - 12,000 commercial credit agreements per year
  - Each review: ~360,000 hours of lawyer/analyst time annually
  - Common errors: missed clauses, inconsistent interpretation

AI-POWERED PROCESS:
  COIN analyzes each contract in seconds:
  - Extracts key clauses, terms, and obligations
  - Flags unusual or non-standard provisions
  - Generates structured summary for human review
  
  Human role: Review AI summary, verify flagged items, make decisions
```

**Results:**
- 360,000 hours of annual work → completed in seconds by AI
- Error rate: reduced (AI does not miss clauses due to fatigue)
- Lawyer/analyst time: redirected to complex judgment work
- Cost savings: estimated $150M+ annually

**Beyond COIN:**
JPMorgan has deployed AI for:
- Natural language search across 40,000 research documents (DocuSign)
- Automated trading signal generation
- Anti-money laundering pattern detection
- Fraud detection with 99.8% accuracy

**The key learning for finance professionals:** AI at JPMorgan does not make financial decisions. It processes and structures information so human experts can make better decisions faster.

---

## 7. Hands-On Lab 18: Financial Document Production

**Objective:** Produce 3 financial documents using AI with accurate data inputs  
**Duration:** 25 minutes  
**Tool:** ChatGPT

*Use fictional or sample data throughout never real company financial data in public AI tools.*

---

### Task 1: Write a Variance Analysis Narrative (8 minutes)

Create fictional financial data:
- Line item: Sales & Marketing Expenses
- Actual: ₹8.5 Crore
- Budget: ₹7.2 Crore
- Prior Year: ₹6.8 Crore
- Unfavorable variance of ₹1.3 Crore (18%)
- Reason: Digital advertising campaign launched in Month 2 + 3 new hires

Use the Variance Analysis Narrative prompt. Evaluate: Is it specific? Does it only use your numbers?

---

### Task 2: Generate an Excel Formula (7 minutes)

Describe a financial calculation you actually need (or use this example):

"I have a table with: Column A = Month, Column B = Product Line, Column C = Revenue.
I want: Total revenue for 'Product Line A' for Q2 (April, May, June) only."

Use the Excel Formula Generator prompt. Then verify: does the formula logic make sense?

---

### Task 3: Explain a Financial Concept (5 minutes)

Choose one:
- EBITDA (for a new marketing hire joining your company)
- Contribution margin (for a product manager)
- Cash conversion cycle (for an operations manager)

Use the "Translate Finance" prompt. Evaluate: Would a non-finance person understand this? Is the analogy helpful?

---

### Task 4: Python Starter Script (5 minutes)

Prompt ChatGPT: "Write a Python function that calculates CAGR (Compound Annual Growth Rate) given a starting value, ending value, and number of years. Include a docstring, example usage, and validation."

Review: Does the formula look correct? (CAGR = (End/Start)^(1/years) - 1)

---

### Lab Evaluation Rubric

| Task | Marks |
|------|-------|
| Task 1: Variance narrative uses provided data only + evaluated | 3 |
| Task 2: Excel formula generated + logic verified | 3 |
| Task 3: Concept explanation + evaluation written | 2 |
| Task 4: Python CAGR function generated + formula verified | 2 |
| **Total** | **10** |

---

## 8. Interview Questions — Session 18

**Q1:** *"How do you use AI in your finance work, and what limits do you apply?"*

**Strong Answer:**
"The fundamental rule in finance AI is that I provide the numbers and AI writes about them never the reverse. AI excels at financial narrative writing: I paste in my verified actuals vs. budget vs. prior year, explain the key drivers, and AI produces a management commentary that would take me 2 hours to write in 5 minutes. I use AI heavily for formula and code generation Excel formulas, Python data manipulation scripts, SQL queries which I then verify before relying on. For explaining financial concepts to non-financial stakeholders, AI is invaluable for finding plain-language analogies that resonate. The firm limits: no real financial data in public AI tools, no AI-generated numbers in financial reports without verification, and no AI involvement in audit conclusions or regulatory filings."

---

## 9. Revision Questions — Session 18

1. What is the single most important rule for AI use in finance? Why is it especially important?
2. What is a variance analysis narrative and what 4 elements should it contain?
3. Give 3 examples of Excel functions where AI assistance is particularly valuable.
4. How would you use AI to write a Board Pack Executive Summary? What data must you provide?
5. Why is explaining financial concepts to non-financial stakeholders a high-value AI use case?
6. What is an assumption log in a financial model? What does AI help document?
7. Describe JPMorgan's COIN platform what did it do, what were the results, and what did humans still do?
8. List 5 specific things AI should NEVER do in a finance context, and explain the risk each poses.

---

## 10. Key Terminology — Session 18

| Term | Definition |
|------|-----------|
| **Management Commentary** | Narrative explanation of financial results for management/board the "story behind the numbers" |
| **Variance Analysis** | Examination of the difference between actual and budgeted financial performance |
| **Board Pack** | Monthly/quarterly financial reporting package prepared for the Board of Directors |
| **EBITDA** | Earnings Before Interest, Taxes, Depreciation and Amortization a measure of operating profitability |
| **Financial Narrative** | Written explanation of financial data designed for decision-making audiences |
| **Assumption Log** | Documentation of the key assumptions underlying a financial model |
| **DSO / DPO** | Days Sales Outstanding / Days Payable Outstanding working capital efficiency metrics |
| **CAGR** | Compound Annual Growth Rate the annualized growth rate of an investment over a period |
| **COIN (JPMorgan)** | Contract Intelligence AI platform that analyzes commercial loan agreements |

---

## 11. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 18 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  Golden Rule: YOU provide numbers → AI writes narrative                  │
│  ✓  Never: AI generates financial numbers for a report                      │
│  ✓  Financial narrative: management commentary, variance analysis, board pack│
│  ✓  Formulas/code: Excel, Python, SQL generate and verify before use     │
│  ✓  Concept translation: AI bridges finance to non-finance audiences        │
│  ✓  Assumption logs: document every model assumption with AI assistance     │
│  ✓  No real financial data in public AI tools (confidentiality)             │
│  ✓  JPMorgan COIN: 360,000 human hours → seconds. Human still decides.     │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 19 — AI for Customer Support                                       │
│  (Empathy-first response frameworks, chatbot design, knowledge base        │
│   creation, quality evaluation, and responsible AI in customer-facing       │
│   contexts)                                                                  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 18 Complete | Next: Session 19 — AI for Customer Support*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
