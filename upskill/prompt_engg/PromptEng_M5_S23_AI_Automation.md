# Session 23: AI Automation — Scaling AI Across Workflows
## Module 5 — Advanced Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 23 OF 30  │  Module 5, Session 3                          │
│  Topic: AI Automation — Scaling Prompts Across Systems & Workflows  │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Distinguish between manual prompting and automated AI workflows
2. Design automation-ready prompt templates with dynamic variables
3. Use no-code tools (Zapier, Make) to connect AI to business systems
4. Build Python-based batch processing workflows for high-volume tasks
5. Implement error handling and human-in-the-loop checkpoints in AI automations
6. Evaluate automation ROI and decide when to automate vs. keep manual

---

## 23.1 The Automation Mindset

Manual prompting and AI automation are not the same:

```
MANUAL PROMPTING:               AI AUTOMATION:
──────────────────              ────────────────────────────────────────
You write → AI responds         Trigger fires → AI processes → System acts
One at a time                   Hundreds or thousands in parallel
You paste the input             Data flows in programmatically
You read the output             Output goes directly to destination
You decide what to do           Rules decide what to do (with human gates)
Limited by your time            Limited only by API rate limits and cost
```

**The Automation Question:** Which of my recurring AI tasks happen more than 10 times per week? Those are candidates for automation.

### Automation Readiness Criteria

Before automating any AI task, check all boxes:

```
✓ The task is well-defined (same structure every time)
✓ The output quality from manual prompting is consistently high (>85%)
✓ The input data is structured and available programmatically
✓ The output can be validated before being acted upon
✓ The consequences of occasional errors are manageable
✓ A human spot-check process is in place
✓ You have approval from the appropriate stakeholders
```

---

## 23.2 Automation-Ready Prompt Design

To automate a prompt, it must be designed for dynamic variable injection — inputs arrive programmatically, not manually pasted.

### Anatomy of an Automation-Ready Prompt

```
SYSTEM PROMPT (static — defines AI role and rules):
"You are a {ROLE} for {COMPANY}. You produce {OUTPUT_TYPE}.
Rules: {STATIC_RULES}"

USER PROMPT (dynamic — variables replaced per run):
"Process the following {INPUT_TYPE}:

INPUT DATA:
{INPUT_VARIABLE}

REQUIRED OUTPUT FORMAT:
{OUTPUT_TEMPLATE}

CONSTRAINTS FOR THIS SPECIFIC RUN:
{DYNAMIC_CONSTRAINTS}"
```

### Example: Automated Support Ticket Classifier

**System Prompt (static):**
```
You are a support ticket classifier for CloudSync, a B2B project management platform.
Classify every ticket accurately and consistently.
Output ONLY valid JSON — no explanation, no preamble.
```

**User Prompt (dynamic per ticket):**
```
Classify this support ticket:

TICKET TEXT: {ticket_body}
CUSTOMER TIER: {customer_tier}
SUBMISSION CHANNEL: {channel}

Output this exact JSON structure:
{
  "category": "[Technical / Billing / Feature Request / Account / General]",
  "priority": "[P0 / P1 / P2 / P3]",
  "sentiment": "[Frustrated / Neutral / Positive]",
  "requires_human": [true / false],
  "reason_for_human": "[Brief reason if requires_human is true, else null]",
  "suggested_team": "[Engineering / Billing / Customer Success / Account Management]",
  "confidence": "[High / Medium / Low]"
}
```

---

## 23.3 No-Code Automation — Zapier and Make

### Zapier AI Automation Flow — Example

**Use Case:** Automatically draft a personalized response to every new support email.

```
ZAPIER FLOW DESIGN:

TRIGGER: New email arrives in support@company.com (Gmail trigger)
        ↓
STEP 1: Extract email fields
        — Sender name, subject, body
        ↓
STEP 2: OpenAI Action (ChatGPT / GPT-4)
        System message: [Your support persona system prompt]
        User message: "Draft a response to this support email:
        From: {sender_name}
        Subject: {subject}
        Body: {email_body}
        
        Use our support response framework.
        If this requires escalation, begin with: ESCALATION NEEDED:
        Otherwise begin with: DRAFT RESPONSE:"
        ↓
STEP 3: Conditional Filter
        IF response starts with "ESCALATION NEEDED:" →
            Create Jira ticket tagged URGENT + notify senior agent in Slack
        ELSE →
            Create draft reply in Gmail (not send — human reviews first)
        ↓
STEP 4: Slack notification to support agent
        "New support draft ready for {sender_name}.
        Category: [from AI output] | Review in Gmail drafts."
```

**Key design principle:** The automation creates a DRAFT — the human agent reviews and sends. This is the human-in-the-loop checkpoint for outbound communication.

---

### Make (Integromat) Automation — Content Calendar Execution

```
MAKE SCENARIO DESIGN:

TRIGGER: Google Sheets — new row added to content calendar
          (Columns: Date | Platform | Topic | Angle | Format | Status)
          Status = "Approved for AI Draft"
        ↓
STEP 1: Parse row fields
        — Extract: Platform, Topic, Angle, Format, Date
        ↓
STEP 2: Select prompt template based on Platform
        — LinkedIn → LinkedIn thought leadership prompt
        — Instagram → Instagram caption + hashtags prompt
        — Email → Newsletter section prompt
        ↓
STEP 3: OpenAI API call with selected prompt + variables injected
        ↓
STEP 4: Google Docs — Create new document with:
        — Title: [Platform] | [Date] | [Topic]
        — Content: AI-generated draft
        — Section: "Status: DRAFT — Needs human review"
        ↓
STEP 5: Update Google Sheets — Status → "Draft Ready"
        ↓
STEP 6: Email notification to content manager:
        "New AI draft ready for: [Topic] on [Platform] — [link to Google Doc]"
```

---

## 23.4 Python Batch Processing

For high-volume, systematic AI automation — processing hundreds or thousands of inputs.

### Batch Processor with Rate Limiting and Error Handling

```python
import time
import json
import csv
from pathlib import Path
from openai import OpenAI
from datetime import datetime


client = OpenAI()


def classify_support_ticket(ticket_text: str, customer_tier: str) -> dict:
    """
    Classify a single support ticket using the OpenAI API.

    Args:
        ticket_text: The raw text of the support ticket
        customer_tier: The customer's tier (Standard / Premium / Enterprise)

    Returns:
        Dictionary containing classification results, or error info.
    """
    system_prompt = """You are a support ticket classifier for CloudSync.
Classify accurately. Output ONLY valid JSON — no explanation."""

    user_prompt = f"""Classify this support ticket:

TICKET: {ticket_text}
CUSTOMER TIER: {customer_tier}

Output this exact JSON:
{{
  "category": "Technical|Billing|Feature Request|Account|General",
  "priority": "P0|P1|P2|P3",
  "sentiment": "Frustrated|Neutral|Positive",
  "requires_human": true|false,
  "suggested_team": "Engineering|Billing|Customer Success|Account Management",
  "confidence": "High|Medium|Low"
}}"""

    try:
        response = client.chat.completions.create(
            model="gpt-4o",
            messages=[
                {"role": "system", "content": system_prompt},
                {"role": "user", "content": user_prompt}
            ],
            temperature=0.1,       # Very low — classification should be deterministic
            max_tokens=200,
            response_format={"type": "json_object"}   # Force JSON output
        )

        result = json.loads(response.choices[0].message.content)
        result["status"] = "success"
        return result

    except json.JSONDecodeError as e:
        return {"status": "error", "error_type": "json_parse", "error": str(e)}
    except Exception as e:
        return {"status": "error", "error_type": "api_error", "error": str(e)}


def process_ticket_batch(
    input_csv: str,
    output_csv: str,
    requests_per_minute: int = 60
) -> dict:
    """
    Process a batch of support tickets from a CSV file.

    Args:
        input_csv: Path to CSV with columns: ticket_id, ticket_text, customer_tier
        output_csv: Path to write results CSV
        requests_per_minute: API rate limit to respect

    Returns:
        Summary statistics of the batch run.
    """
    delay_between_requests = 60.0 / requests_per_minute

    results = []
    stats = {
        "total": 0,
        "success": 0,
        "errors": 0,
        "requires_human": 0,
        "started_at": datetime.now().isoformat()
    }

    # Read input tickets
    tickets = []
    with open(input_csv, newline="", encoding="utf-8") as f:
        reader = csv.DictReader(f)
        tickets = list(reader)

    stats["total"] = len(tickets)
    print(f"Processing {stats['total']} tickets...")

    for i, ticket in enumerate(tickets):
        print(f"[{i+1}/{stats['total']}] Processing ticket {ticket.get('ticket_id', i)}")

        classification = classify_support_ticket(
            ticket_text=ticket["ticket_text"],
            customer_tier=ticket.get("customer_tier", "Standard")
        )

        # Merge original ticket data with classification
        row = {**ticket, **classification}
        results.append(row)

        # Update stats
        if classification["status"] == "success":
            stats["success"] += 1
            if classification.get("requires_human"):
                stats["requires_human"] += 1
        else:
            stats["errors"] += 1
            print(f"  ⚠️  Error on ticket {ticket.get('ticket_id')}: {classification.get('error')}")

        # Rate limiting — respect API limits
        if i < len(tickets) - 1:
            time.sleep(delay_between_requests)

    # Write output CSV
    if results:
        fieldnames = list(results[0].keys())
        with open(output_csv, "w", newline="", encoding="utf-8") as f:
            writer = csv.DictWriter(f, fieldnames=fieldnames)
            writer.writeheader()
            writer.writerows(results)

    stats["completed_at"] = datetime.now().isoformat()
    stats["success_rate"] = f"{stats['success']/stats['total']*100:.1f}%"

    print(f"\n{'='*50}")
    print(f"BATCH COMPLETE")
    print(f"Total: {stats['total']} | Success: {stats['success']} | Errors: {stats['errors']}")
    print(f"Requires human review: {stats['requires_human']}")
    print(f"Results written to: {output_csv}")

    return stats


# Human-in-the-loop: Review tickets flagged for human handling
def extract_human_review_queue(output_csv: str) -> list[dict]:
    """
    Extract tickets that need human review from batch output.

    Returns list of high-priority tickets for human agent queue.
    """
    human_queue = []

    with open(output_csv, newline="", encoding="utf-8") as f:
        reader = csv.DictReader(f)
        for row in reader:
            if row.get("requires_human") == "True" or row.get("priority") in ("P0", "P1"):
                human_queue.append({
                    "ticket_id": row["ticket_id"],
                    "priority": row.get("priority"),
                    "category": row.get("category"),
                    "suggested_team": row.get("suggested_team"),
                    "ticket_preview": row["ticket_text"][:100] + "..."
                })

    # Sort by priority (P0 first)
    priority_order = {"P0": 0, "P1": 1, "P2": 2, "P3": 3}
    human_queue.sort(key=lambda x: priority_order.get(x.get("priority", "P3"), 3))

    return human_queue


if __name__ == "__main__":
    # Example run
    stats = process_ticket_batch(
        input_csv="tickets.csv",
        output_csv="tickets_classified.csv",
        requests_per_minute=40   # Conservative limit for shared API plans
    )

    queue = extract_human_review_queue("tickets_classified.csv")
    print(f"\nHUMAN REVIEW QUEUE: {len(queue)} tickets need immediate attention")
    for item in queue[:5]:  # Show top 5
        print(f"  [{item['priority']}] {item['ticket_id']} — {item['category']}")
```

---

## 23.5 Human-in-the-Loop Design Patterns

Automation should never fully remove human oversight for consequential outputs. These patterns embed human judgment at the right points.

### Pattern 1: Draft-and-Review

```
AI generates → Human reviews → Human approves/edits → System sends/publishes

Use for: External communications, published content, financial outputs
When to skip human review: Very high volume, low-stakes outputs (internal notes)
```

### Pattern 2: Exception-Only Review

```
AI processes → Automated quality check →
  IF quality threshold met: automatically proceed
  IF below threshold OR flagged: route to human queue

Use for: High-volume classification, data enrichment, content generation at scale
```

### Pattern 3: Confidence-Gated Automation

```python
def route_by_confidence(classification: dict) -> str:
    """
    Route AI output based on confidence level.
    High confidence → automatic processing
    Low confidence → human review queue
    """
    confidence = classification.get("confidence", "Low")
    priority = classification.get("priority", "P3")

    # Always human-review: P0/P1 regardless of confidence
    if priority in ("P0", "P1"):
        return "human_queue_urgent"

    # High confidence, low stakes: auto-process
    if confidence == "High" and priority == "P3":
        return "auto_process"

    # Everything else: human review
    return "human_queue_standard"
```

### Pattern 4: Sampling-Based Quality Control

```
For every 100 auto-processed outputs, randomly sample 5 for human review.
If quality drops below 90% in any sample: pause automation and review.

This scales human oversight without reviewing every output.
```

---

## 23.6 Automation ROI Calculation

Before building an automation, calculate whether it's worth it.

```
ROI CALCULATION FRAMEWORK:

COSTS:
- Development time: [hours] × [developer rate]
- AI API costs per run: [tokens per run] × [price per token] × [runs per month]
- Maintenance time: [hours/month] × [rate]
- One-time tool/infrastructure costs
─────────────────────────────────────
TOTAL MONTHLY COST: [sum]

BENEFITS:
- Time saved per run: [minutes] × [runs per month] / 60 = hours saved/month
- Hours saved × [employee rate] = monthly labor saving
- Quality improvement benefit (if measurable): [estimate]
- Error reduction benefit (if measurable): [estimate]
─────────────────────────────────────
TOTAL MONTHLY BENEFIT: [sum]

MONTHLY ROI = (Benefit - Cost) / Cost × 100%
PAYBACK PERIOD = Development cost / Monthly net benefit
```

**Automation Threshold Rule:** Build the automation if:
- Payback period < 3 months, AND
- Monthly ROI > 200%, AND
- You will run this at least 50 times per month

---

## 23.7 Automation Governance

Automation at scale requires governance to prevent runaway errors and ensure accountability.

### Automation Governance Checklist

```
BEFORE DEPLOYING ANY AI AUTOMATION:

APPROVAL:
□ Stakeholder sign-off on automation scope and limits
□ Legal/compliance review for any customer-facing automation
□ Data privacy assessment (what data is being processed?)
□ IT security review for API key management

TESTING:
□ Tested on 50+ representative inputs before production
□ Edge cases identified and handled
□ Error rate acceptable (<5% for most use cases)
□ Human review sample confirms output quality

MONITORING:
□ Logging in place for all API calls and outputs
□ Alert system for error rate spikes
□ Weekly quality sampling by human reviewer
□ Monthly ROI measurement

DOCUMENTATION:
□ Prompt versions documented (what prompt is in production?)
□ Runbook: what to do when automation fails
□ Rollback plan: how to turn it off quickly if needed
□ Owner identified: who is responsible for this automation?

LIMITS:
□ Rate limits configured (no runaway API spending)
□ Cost alerts set (notify if monthly API spend exceeds threshold)
□ Output volume caps for first 30 days
```

---

## Hands-On Activities — Session 23

---

### Activity 23.1 — Automation-Ready Prompt Design

**Objective:** Convert a manual prompt into automation-ready form.

**Step 1:** Choose any prompt from your library that you run more than 10 times per week.

**Step 2:** Redesign it as an automation-ready prompt:
- Separate system prompt (static) from user prompt (dynamic)
- Replace all manual inputs with {VARIABLE} placeholders
- Add output format specification for structured parsing
- Add a confidence indicator or validation field

**Step 3:** Write the variable list: what data source would provide each variable? (Email inbox / CRM / spreadsheet / API / etc.)

---

### Activity 23.2 — ROI Calculation

**Objective:** Calculate the ROI of automating your chosen task.

Using the ROI framework from Section 23.6, calculate for your Activity 23.1 task:
- Current time cost (manual)
- Estimated API cost at scale
- Development time estimate
- Monthly benefit
- Payback period

**Decision:** Should this be automated? What threshold would make automation worthwhile if it isn't yet?

---

### Activity 23.3 — Batch Processor Simulation

**Objective:** Experience batch processing logic without full infrastructure.

**Step 1:** Create a small CSV with 5 test support tickets:

```csv
ticket_id,ticket_text,customer_tier
T001,"My account was charged twice last month",Standard
T002,"The app crashed and I lost all my work",Premium
T003,"How do I export my data to Excel?",Standard
T004,"Our entire team cannot log in since the update",Enterprise
T005,"Can you add dark mode to the app?",Standard
```

**Step 2:** Run the classify_support_ticket function prompt for each ticket individually (manually, using the prompt template in Section 23.2).

**Step 3:** Organize results as if they came from the batch processor: create the output table and identify which tickets would go to the human review queue.

---

### Activity 23.4 — Automation Design Document

**Objective:** Design a complete automation for a real business use case.

Choose one:
- Monthly report generation from raw data
- Job posting creation from a hiring brief
- Customer follow-up email from CRM data
- Content repurposing from blog post to social posts

Write a complete automation design document including:
- Trigger condition
- Step-by-step flow with tool/system for each step
- Human-in-the-loop checkpoint design
- Error handling approach
- Governance checklist items relevant to this automation
- ROI calculation

---

## Revision Questions — Session 23

1. What is the key difference between manual prompting and AI automation? What does the "Automation Readiness Criteria" checklist verify?
2. What makes a prompt "automation-ready"? Describe the structural differences from a manual prompt.
3. Describe the Zapier support email automation flow. Where is the human-in-the-loop checkpoint and why is it placed there?
4. What are the 4 human-in-the-loop design patterns? For which type of task is each most appropriate?
5. What is confidence-gated automation? How does it balance efficiency with quality control?
6. Describe the ROI calculation framework. What 3 conditions must be true before building an automation?
7. Name 5 items from the Automation Governance Checklist that you consider most critical. Justify each.
8. A marketing team wants to automate posting AI-generated content directly to their company LinkedIn without human review. What risks does this create and what would you recommend instead?

---

## Key Takeaways — Session 23

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 23 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Automate when: same task >10x/week, structured input, >85%      │
│    manual quality, manageable error consequences                     │
│                                                                      │
│  ✓ Automation-ready prompts: static system + dynamic user prompt   │
│    with {VARIABLE} placeholders and structured output format        │
│                                                                      │
│  ✓ Human-in-the-loop is mandatory for consequential outputs:        │
│    Draft-and-Review / Exception-only / Confidence-gated / Sampling │
│                                                                      │
│  ✓ ROI threshold: payback < 3 months, ROI > 200%, >50 runs/month  │
│                                                                      │
│  ✓ Governance before deployment: approval, testing, monitoring,    │
│    documentation, limits — all non-negotiable at scale             │
│                                                                      │
│  ✓ Never automate without an off switch: rate limits, cost alerts, │
│    and a documented rollback plan are essential safety controls     │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 23 Complete → Proceed to Session 24: Building a Professional Prompt Library*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
