# Session 18: AI for Finance & Data Analysis
## Module 4 — Business & Industry Applications
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 18 OF 30  │  Module 4, Session 3                          │
│  Topic: AI for Finance & Data Analysis                              │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Use AI to interpret financial data and generate narrative insights
2. Build financial analysis prompts for budgets, P&Ls, and variance reports
3. Generate Python and SQL code for data analysis tasks using AI
4. Create financial models and projections with AI-assisted frameworks
5. Use AI for business intelligence narrative reporting
6. Apply critical verification standards to all AI-generated financial content

---

## 18.1 AI's Role in Finance — The Critical Distinction

Finance is a domain where AI offers enormous value — and where errors have the most serious consequences. The critical distinction:

```
AI EXCELS AT:                         AI CANNOT REPLACE:
─────────────────────────────         ─────────────────────────────────────
Writing narrative around numbers      Performing verified complex calculations
Generating code to process data       Replacing a certified finance professional
Explaining financial concepts         Providing regulated financial advice
Structuring financial documents       Auditing or certifying financial statements
Generating multiple scenario names    Making judgment calls on materiality
Interpreting trends in plain English  Accessing your live financial systems
Generating SQL/Python for analysis    Guaranteeing numerical accuracy
```

**The Finance Rule:** Always verify every number independently. AI is a language model — it predicts likely text, not accurate arithmetic. Use AI for language, structure, and code generation; use Excel, Python, or a calculator for the actual numbers.

---

## 18.2 Financial Narrative Writing

The most immediate, low-risk, high-value AI use in finance is converting numbers into clear narrative — the written explanation of what the numbers mean.

### Monthly/Quarterly Business Review Narrative

```
You are a senior finance business partner who writes clear, insightful
financial commentary for senior business leaders.

Write the financial commentary section for our [PERIOD] business review.

The audience: [DESCRIBE — CEO / Board / Department Heads / Investors]
Their financial literacy: [High / Medium / Low]
Purpose of this commentary: [Inform / Justify / Recommend action]

Financial performance data (I will provide — verify these figures independently):
Revenue: [ACTUAL vs. PLAN vs. PRIOR PERIOD]
Gross Margin: [ACTUAL vs. PLAN]
Operating Expenses: [ACTUAL vs. PLAN, with major line items]
EBITDA: [ACTUAL vs. PLAN]
Cash Position: [IF RELEVANT]
Key variance drivers: [WHAT CAUSED THE VARIANCES — you decide, AI phrases]

Write commentary covering:
1. HEADLINE PERFORMANCE (1 sentence — on track / ahead / behind, and by how much)
2. REVENUE COMMENTARY (2–3 sentences — what drove the result, which segments/products)
3. MARGIN COMMENTARY (2 sentences — why margin moved, main drivers)
4. OPEX COMMENTARY (2 sentences — what drove spend, significant variances)
5. OUTLOOK (2 sentences — projection for remainder of period, key risks)

Rules:
- All figures I provide in the context — do NOT calculate or invent figures
- Use the figures exactly as I state them — do not round or adjust
- Flag any calculation you perform with [PLEASE VERIFY: calculation]
- Tone: Professional, factual, insightful — not a list of obvious numbers
Length: 250–350 words
```

---

### Variance Analysis Commentary

```
Write variance analysis commentary for the following budget vs. actual data.

Context:
Period: [MONTH/QUARTER]
Department: [DEPARTMENT NAME]
Currency: [INR / USD / etc.]

Variance data (provided by me — do not recalculate):
[Paste your variance table: Line Item | Budget | Actual | Variance | Variance %]

For each significant variance (>5% or material amount):
1. State the variance (amount and percentage — use my figures exactly)
2. Explain the most likely cause (I will confirm accuracy — you propose)
3. Classify as: Favorable / Unfavorable | Recurring / One-time | Controllable / Uncontrollable
4. Recommend action (if unfavorable and controllable): 1 specific action

Format: Table with narrative explanation below

After the table: Write a 3-sentence executive summary of the overall
variance position and the most important management action.
```

---

## 18.3 Financial Modeling Support

### Three-Statement Model Explanation

```
I am building a 3-statement financial model (P&L, Balance Sheet, Cash Flow).
Help me structure it correctly.

My business: [DESCRIBE — revenue model, cost structure, key metrics]
Planning horizon: [MONTHS / YEARS]
Purpose: [Internal planning / Investor deck / Bank loan / M&A]

For each statement, provide:
1. STRUCTURE — which line items to include, in what order
2. KEY DRIVERS — the main assumptions that drive each number
3. LINKAGES — how the statements connect to each other
4. VALIDATION CHECKS — formulas I can use to verify the model balances

Then explain:
- What the key model assumptions I should define first
- Where finance teams most commonly make errors in 3-statement models
- 5 sensitivity analyses I should run once the base case is built

Note: I will build all actual numbers — you are helping me structure the model
and think through the framework.
```

---

### Financial Projection Scenarios

```
Help me structure a scenario analysis for our [BUSINESS/PROJECT] financial projections.

Base case assumptions:
[List your key assumptions — revenue growth, margins, costs, etc.]

Generate:
1. BASE CASE — the realistic most likely scenario
2. BULL CASE — optimistic but plausible (justify each upside assumption)
3. BEAR CASE — conservative/downside (justify each downside assumption)
4. STRESS TEST — survival scenario (what does the business look like if
   the worst plausible combination of factors hits at once?)

For each scenario:
- Describe what would need to be true for this scenario to occur
- List the 3 key assumption changes from base case
- Describe what management actions would be appropriate in this scenario
- State the key risk factor that most determines which scenario we're in

Present as a scenario comparison framework (I will insert actual numbers).
```

---

## 18.4 AI-Generated Code for Financial Analysis

This section demonstrates how to use AI to generate Python and SQL code for financial analysis tasks — saving analysis time while ensuring accuracy through testable code.

### Python — Financial KPI Calculator

```
Write Python code to calculate and display key financial KPIs from raw data.

Input format: CSV with columns: date, revenue, cogs, opex, cash_in, cash_out
Output: Print a formatted financial dashboard showing:
- Gross Margin %
- Operating Margin %
- Net Burn Rate (monthly)
- Runway (months at current burn)
- MoM Revenue Growth %
- Revenue Run Rate (annualized)

Requirements:
- Handle missing values gracefully
- Round percentages to 1 decimal place
- Format currency values with comma separators
- Flag any negative margin or high burn rate with a warning
- Include docstrings and type hints
```

**Expected output from this prompt:**

```python
import pandas as pd
from pathlib import Path


def calculate_financial_kpis(csv_path: str) -> dict:
    """
    Calculate key financial KPIs from a revenue/cost CSV file.

    Args:
        csv_path: Path to CSV file with columns:
                  date, revenue, cogs, opex, cash_in, cash_out

    Returns:
        Dictionary of calculated KPIs with formatted values.

    Example:
        >>> kpis = calculate_financial_kpis("financials.csv")
        >>> print(kpis['gross_margin_pct'])
        '62.5%'
    """
    df = pd.read_csv(csv_path, parse_dates=['date'])
    df = df.dropna(subset=['revenue', 'cogs'])  # require core fields

    # Sort by date for growth calculations
    df = df.sort_values('date')

    # ── Core P&L Calculations ──────────────────────────────────────
    total_revenue = df['revenue'].sum()
    total_cogs = df['cogs'].sum()
    total_opex = df['opex'].fillna(0).sum()

    gross_profit = total_revenue - total_cogs
    operating_profit = gross_profit - total_opex

    gross_margin_pct = (gross_profit / total_revenue * 100) if total_revenue else 0
    operating_margin_pct = (operating_profit / total_revenue * 100) if total_revenue else 0

    # ── Cash / Burn Calculations ───────────────────────────────────
    df['net_cash'] = df['cash_in'].fillna(0) - df['cash_out'].fillna(0)
    monthly_burn = -df['net_cash'].mean()  # negative = burning cash
    current_cash = df['net_cash'].sum()
    runway_months = (current_cash / monthly_burn) if monthly_burn > 0 else float('inf')

    # ── Growth Calculations ────────────────────────────────────────
    if len(df) >= 2:
        latest_revenue = df['revenue'].iloc[-1]
        prev_revenue = df['revenue'].iloc[-2]
        mom_growth = ((latest_revenue - prev_revenue) / prev_revenue * 100) if prev_revenue else 0
    else:
        latest_revenue = df['revenue'].iloc[-1]
        mom_growth = None

    run_rate = latest_revenue * 12  # annualized from most recent month

    # ── Format and Return ──────────────────────────────────────────
    kpis = {
        'gross_margin_pct': f"{gross_margin_pct:.1f}%",
        'operating_margin_pct': f"{operating_margin_pct:.1f}%",
        'monthly_burn_inr': f"₹{monthly_burn:,.0f}",
        'runway_months': f"{runway_months:.1f} months" if runway_months != float('inf') else "Profitable",
        'mom_revenue_growth': f"{mom_growth:.1f}%" if mom_growth is not None else "N/A",
        'revenue_run_rate': f"₹{run_rate:,.0f}",
    }

    # ── Warnings ───────────────────────────────────────────────────
    warnings = []
    if gross_margin_pct < 30:
        warnings.append(f"⚠️  LOW GROSS MARGIN: {gross_margin_pct:.1f}% — review COGS drivers")
    if runway_months < 12:
        warnings.append(f"⚠️  SHORT RUNWAY: {runway_months:.1f} months — review burn rate urgently")
    if operating_margin_pct < 0:
        warnings.append(f"⚠️  OPERATING LOSS: margin is {operating_margin_pct:.1f}%")

    kpis['warnings'] = warnings
    return kpis


def print_dashboard(kpis: dict) -> None:
    """Print a formatted financial KPI dashboard."""
    print("\n" + "═" * 50)
    print("  FINANCIAL KPI DASHBOARD")
    print("═" * 50)
    print(f"  Gross Margin:          {kpis['gross_margin_pct']}")
    print(f"  Operating Margin:      {kpis['operating_margin_pct']}")
    print(f"  Monthly Burn:          {kpis['monthly_burn_inr']}")
    print(f"  Runway:                {kpis['runway_months']}")
    print(f"  MoM Revenue Growth:    {kpis['mom_revenue_growth']}")
    print(f"  Revenue Run Rate:      {kpis['revenue_run_rate']}")
    print("═" * 50)
    if kpis.get('warnings'):
        print("\n  ALERTS:")
        for w in kpis['warnings']:
            print(f"  {w}")
    print()


if __name__ == "__main__":
    kpis = calculate_financial_kpis("financials.csv")
    print_dashboard(kpis)
```

---

### SQL — Revenue Analysis Queries

```
Write SQL queries to analyze revenue data from a database with these tables:
- orders (order_id, customer_id, order_date, total_amount, status)
- customers (customer_id, signup_date, segment, region)
- products (product_id, category, unit_price)
- order_items (order_id, product_id, quantity, unit_price)

Generate queries for:
1. Monthly revenue trend (last 12 months)
2. Revenue by customer segment with YoY comparison
3. Top 10 products by revenue this quarter
4. Customer Lifetime Value by cohort (signup month)
5. Churn analysis: customers active 6+ months ago but not in last 90 days

For each query:
- Add comments explaining what it does
- Use CTEs (WITH clauses) for readability where appropriate
- Handle NULL values appropriately
- Include a sample output description
```

---

### Excel Formula Generation

```
Generate Excel formulas for the following financial analysis tasks.
My data layout: [DESCRIBE YOUR SPREADSHEET STRUCTURE]

Generate:
1. Formula to calculate gross margin % with error handling if revenue is zero
2. Formula to show variance vs. prior year as both amount and percentage
3. Conditional formatting rule to highlight cells where variance > 10%
4. VLOOKUP/INDEX-MATCH to pull budget figures from a separate Budget tab
5. Running total formula that accumulates month by month
6. Formula to calculate rolling 3-month average revenue

For each formula: the Excel formula + a plain English explanation of how it works.
```

---

## 18.5 Business Intelligence Reporting

### BI Report Narrative Template

```
Write the narrative commentary for a business intelligence dashboard.

Dashboard data (I provide — do not calculate):
[PASTE YOUR DATA: KPIs, trends, comparisons]

Report purpose: [WHAT DECISIONS DOES THIS REPORT SUPPORT?]
Primary audience: [WHO READS THIS?]
Reporting period: [PERIOD]

Write a BI report narrative with:

EXECUTIVE SUMMARY (3 sentences):
- Headline metric performance
- Most important positive development
- Most important concern or risk

PERFORMANCE HIGHLIGHTS (3 bullet points):
- Each must cite a specific metric from my data
- Each must explain the business implication, not just the number

KEY CONCERNS (2 bullet points):
- Most important negative trends or risks
- What action is recommended

FORWARD OUTLOOK (2 sentences):
- Expected trajectory based on current trends
- Key assumption this outlook depends on

Rules: All numbers from my data only. Flag any trend analysis with
[BASED ON DATA PROVIDED]. Do not project or forecast — just report.
```

---

### Board-Ready Financial Summary

```
You are a CFO preparing a board financial update. The board is composed
of [DESCRIBE — investors / independent directors / management].
Financial literacy of board members: [High / Mixed].

Convert the following financial data into a board-ready presentation narrative:
[PASTE YOUR DATA]

Board financial narrative structure:

SLIDE 1 — FINANCIAL HEADLINE:
"One sentence. The single most important financial fact this period.
Make it a complete, clear statement — not a vague overview."

SLIDE 2 — PERFORMANCE VS. PLAN:
Revenue: [Actual vs. Plan — narrative sentence with % variance]
Gross Margin: [Actual vs. Plan — why it moved]
EBITDA: [Actual vs. Plan — key drivers]
Cash: [Position + trend in 1 sentence]

SLIDE 3 — KEY RISKS AND OPPORTUNITIES:
Risk 1: [Name] | Impact [High/Medium/Low] | Mitigation [1 line]
Risk 2: [Name] | Impact [High/Medium/Low] | Mitigation [1 line]
Opportunity 1: [Name] | Potential [describe] | Action needed [1 line]

SLIDE 4 — OUTLOOK AND WHAT WE NEED FROM THE BOARD:
[2-sentence outlook] + [1 clear request for board decision or input]

All numbers: use exactly what I provide — do not recalculate.
```

---

## 18.6 Financial Concept Explanation

For non-finance audiences who need to understand financial reports:

```
Explain [FINANCIAL CONCEPT] for a [AUDIENCE] who has [BACKGROUND].

The concept: [SPECIFIC FINANCIAL TERM OR CONCEPT]
Why they need to understand it: [CONTEXT — what decision does it inform?]
Their background: [Non-finance professional / New manager / Entrepreneur etc.]

Explanation structure:
1. PLAIN ENGLISH DEFINITION (1–2 sentences — no jargon)
2. EVERYDAY ANALOGY (explain it using a non-finance comparison)
3. WHY IT MATTERS for their specific role/decision
4. EXAMPLE with numbers (simple, round numbers — not a real calculation)
5. THE KEY QUESTION they should ask when they see this metric
6. COMMON MISCONCEPTION about this concept (and the correction)

Tone: Patient but not condescending. Treat them as intelligent — just new to this.
```

---

## Hands-On Activities — Session 18

---

### Activity 18.1 — Financial Narrative Writing

**Objective:** Convert raw numbers into professional financial commentary.

**Step 1:** Use these sample figures (or your own real data):
- Revenue: ₹4.2 Cr actual vs. ₹3.8 Cr plan (+10.5%)
- Gross Margin: 58% actual vs. 62% planned (-4pp)
- OpEx: ₹1.8 Cr actual vs. ₹2.0 Cr plan (-10%)
- EBITDA: ₹0.6 Cr actual vs. ₹0.36 Cr plan (+67%)

**Step 2:** Run the Monthly Business Review Narrative prompt.

**Step 3:** Evaluate: Does the narrative add insight beyond stating the numbers? Does it explain the "so what"? Would you share this with your finance team or management?

---

### Activity 18.2 — Python KPI Calculator

**Objective:** Use AI to generate working financial analysis code.

**Step 1:** Run the Python KPI Calculator prompt.

**Step 2:** If you have Python installed (Google Colab is free and requires no installation):
- Create a sample CSV with 6 months of test data
- Run the generated code
- Verify the outputs match your manual calculations

**Step 3:** Ask AI to modify the code to add one new KPI of your choice (e.g., Customer Acquisition Cost, Average Revenue per User).

---

### Activity 18.3 — SQL Query Generation

**Objective:** Generate and evaluate SQL for business analysis.

**Step 1:** Run the SQL Revenue Analysis prompt.

**Step 2:** If you have database access, run the queries. If not:
- Evaluate the query logic conceptually
- Check: Are the JOINs correct? Are NULLs handled? Are date filters correct?
- Ask AI to add a 6th query: "Average order value by month for the last 12 months"

**Step 3:** Ask AI to explain one of the CTEs in plain English as if explaining to a non-technical business analyst.

---

### Activity 18.4 — Financial Concept Explainer

**Objective:** Use AI to explain finance to non-finance colleagues.

**Step 1:** Choose a financial concept that colleagues in your team often misunderstand:
- Working Capital
- Contribution Margin
- EBITDA
- Burn Rate
- Customer Lifetime Value

**Step 2:** Run the Financial Concept Explanation prompt.

**Step 3:** Share the output with a non-finance colleague and ask if it made the concept clear. What would they still want clarified?

---

## Revision Questions — Session 18

1. What is the most important rule for AI use in finance? Why?
2. Describe 5 high-value, lower-risk AI use cases in finance.
3. What is the purpose of financial narrative writing? How is it different from just presenting the numbers?
4. Why is AI better suited to generating financial analysis code than performing financial calculations directly?
5. What is a three-statement financial model and why does AI need your structure guidance before building one?
6. Describe what a scenario analysis framework contains. What are the 4 scenarios and what does each represent?
7. You receive AI-generated variance analysis commentary that includes figures. What must you do before sharing it?
8. A startup founder asks ChatGPT "What will our revenue be next year?" and uses the answer in an investor deck. What are the problems with this approach?

---

## Key Takeaways — Session 18

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 18 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Finance rule: AI for language and structure; calculators and     │
│    code for verified numbers — never trust AI arithmetic directly   │
│                                                                      │
│  ✓ Financial narrative: the highest-value, lowest-risk AI use —    │
│    converts numbers into decisions, not just reports                │
│                                                                      │
│  ✓ Code generation: Python + SQL for analysis is far more          │
│    reliable than asking AI to calculate directly                    │
│                                                                      │
│  ✓ Scenario planning: 4 scenarios (base / bull / bear / stress)    │
│    AI helps structure assumptions; you fill in the numbers          │
│                                                                      │
│  ✓ BI reporting: AI writes the "so what" — the insight and action  │
│    that goes beyond what the dashboard shows                        │
│                                                                      │
│  ✓ Always verify all figures in any AI-generated financial output  │
│    against your authoritative data source before distribution       │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 18 Complete → Proceed to Session 19: AI for Strategy & Business Development*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
