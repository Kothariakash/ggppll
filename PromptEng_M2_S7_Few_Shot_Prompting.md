# Session 7: Few-Shot Prompting
## Module 2 — Prompting Techniques
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 7 OF 30  │  Module 2, Session 2                           │
│  Topic: Few-Shot Prompting — Teaching AI by Example                 │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Explain what few-shot prompting is and how it differs from zero-shot
2. Design high-quality examples that teach the AI a pattern, format, or style
3. Apply one-shot, two-shot, and multi-shot prompting appropriately
4. Use few-shot prompting to establish brand voice and custom output formats
5. Identify and avoid the most common few-shot design mistakes
6. Build few-shot classifiers and extraction pipelines for real professional tasks

---

## 7.1 What is Few-Shot Prompting?

**Few-shot prompting** provides a small number of input-output examples (typically 2–8) that demonstrate exactly what kind of response you want. The model learns the pattern from your examples and applies it to new inputs.

```
ZERO-SHOT:
Instruction → New input → AI generates response using training knowledge

FEW-SHOT:
Instruction + [Example 1: input → output]
           + [Example 2: input → output]
           + [Example 3: input → output]
           + New input → AI generates response matching the demonstrated pattern
```

### Why Few-Shot Works

Every example you provide is interpreted as a demonstration of the "rule" the AI should apply. The model performs **in-context learning** — it temporarily learns from your examples within the conversation without any weight updates or fine-tuning.

This is a breakthrough capability of large language models: they can adapt their behavior based purely on patterns shown in the prompt.

### The Power Difference

| Scenario | Zero-Shot | Few-Shot |
|----------|-----------|---------|
| Standard sentiment analysis | Excellent — no examples needed | Not necessary |
| Your company's specific complaint categories | Poor — AI guesses | Excellent — examples define categories |
| Your brand's tone of voice | Poor — AI uses generic voice | Excellent — examples teach the voice |
| Unusual output format | Poor — AI invents a format | Excellent — example shows the exact format |
| Nuanced classification with edge cases | Inconsistent | Consistent — examples show edge case handling |

---

## 7.2 One-Shot Prompting

**One-shot** provides a single example — enough to establish a format or style when the task is relatively clear.

### When One-Shot is Sufficient
- The task itself is clear, but the output format is custom
- You need consistent phrasing or structure
- Token efficiency is important (more examples = more tokens)

### One-Shot Examples

**Example 1A — Customer Complaint to Support Ticket:**

```
Convert customer messages into structured support tickets.

EXAMPLE:
Customer message: "This is ridiculous! My order was supposed to arrive
3 days ago and nobody can tell me where it is! I need it for an event tomorrow!!!"

Support ticket:
TICKET-TYPE: Delivery Complaint
URGENCY: High
CUSTOMER-SENTIMENT: Frustrated
ISSUE: Order not delivered within expected timeframe; customer has a time-critical need
REQUIRED-ACTION: Locate shipment status immediately; provide update within 2 hours;
  escalate to logistics if status unknown
FOLLOW-UP: Confirm delivery or arrange emergency replacement before customer's event

Now convert this:
Customer message: "Your website keeps crashing every time I try to pay.
I've tried 3 times in the last hour and lost my cart twice. I really need to
place this order today for a gift."
```

**Example 1B — Raw Notes to Action Items:**

```
Convert raw meeting notes into clean, formatted action items.

EXAMPLE:
Raw notes: "priya will send the draft contract by end of day friday, also need
to follow up with legal team about the clause we discussed, rahul mentioned
he can have the financial model ready by next wednesday"

Action Items:
| # | Task | Owner | Deadline | Status |
|---|------|-------|----------|--------|
| 1 | Send draft contract | Priya | Friday EOD | Pending |
| 2 | Follow up with Legal on discussed clause | Meeting Lead | ASAP | Pending |
| 3 | Complete financial model | Rahul | Next Wednesday | Pending |

Now convert these notes:
"deepa needs to finalize the slide deck before tuesday's board meeting,
also someone should book the conference room for that day — 3 hours.
the ceo asked for the Q3 numbers to be added to slide 4"
```

---

## 7.3 Few-Shot Prompting — 2 to 5 Examples

More examples give the AI a richer pattern to learn from — especially for nuanced tasks.

### Few-Shot Structure Template

```
[Task instruction]

---EXAMPLE 1---
Input: [example input 1]
Output: [example output 1]

---EXAMPLE 2---
Input: [example input 2]
Output: [example output 2]

---EXAMPLE 3---
Input: [example input 3]
Output: [example output 3]

---YOUR TASK---
Input: [your actual input]
Output:
```

### Few-Shot Example 1 — Nuanced Sentiment with Context

```
Classify the following reviews. Consider the OVERALL sentiment,
even when mixed. Provide classification and a confidence score (1–5).

---EXAMPLE 1---
Review: "The hotel room was spotless and the staff were incredibly helpful.
However, the food at the restaurant was disappointing and overpriced."
Classification: Neutral (3/5 confidence)
Reasoning: Positive experience with room/staff balanced by negative dining
experience — neither dominates clearly.

---EXAMPLE 2---
Review: "Delivery was late by 4 days, but the product itself is absolutely
outstanding quality. Worth the wait in the end."
Classification: Mildly Positive (4/5 confidence)
Reasoning: Despite delivery frustration, the product satisfaction is the
lasting impression — ends on a strongly positive note.

---EXAMPLE 3---
Review: "The rep I spoke to was rude, put me on hold for 25 minutes, and
still didn't resolve my issue. The product is fine but I'm switching providers."
Classification: Strongly Negative (5/5 confidence)
Reasoning: Poor service experience leading to churn intent dominates despite
neutral product quality — a clear negative business outcome.

---YOUR TASK---
Review: "I've been using this software for 6 months. The features are great
and it saves me time every day, but the customer support takes 3–4 days to
respond and my last 2 tickets were never properly resolved."
Classification:
```

---

### Few-Shot Example 2 — Custom Output Format

**Scenario:** You need a consistent format for competitive analysis notes that doesn't exist as a standard format.

```
Convert competitor information into our standard Competitive Intelligence Brief format.

---EXAMPLE 1---
Raw info: "Salesforce is the market leader in CRM with 23% market share.
Their main product is their Sales Cloud, priced from $25/user/month.
Key strength: massive ecosystem and integrations. Main complaint from
customers: complex implementation and high total cost of ownership."

Competitive Intelligence Brief:
┌─────────────────────────────────────────────┐
│ COMPETITOR: Salesforce                       │
│ MARKET POSITION: Market Leader (#1)          │
│ MARKET SHARE: ~23%                           │
├─────────────────────────────────────────────┤
│ CORE PRODUCT: Sales Cloud                    │
│ PRICING: From $25/user/month                 │
├─────────────────────────────────────────────┤
│ STRENGTHS: Massive ecosystem; deep integrations│
│ WEAKNESSES: Complex implementation; high TCO │
├─────────────────────────────────────────────┤
│ OUR OPPORTUNITY: Target customers who find   │
│ Salesforce overly complex or expensive       │
└─────────────────────────────────────────────┘

---EXAMPLE 2---
Raw info: "HubSpot targets SMBs and startups. Free tier with limited features
available. Paid plans from $45/month. Very popular for inbound marketing
integration with CRM. Customers love the ease of use. Weakness: limited
customization compared to enterprise solutions."

Competitive Intelligence Brief:
┌─────────────────────────────────────────────┐
│ COMPETITOR: HubSpot                          │
│ MARKET POSITION: SMB/Startup Leader         │
│ MARKET SHARE: N/A in notes                  │
├─────────────────────────────────────────────┤
│ CORE PRODUCT: CRM + Marketing Hub           │
│ PRICING: Free tier; paid from $45/month      │
├─────────────────────────────────────────────┤
│ STRENGTHS: Ease of use; inbound marketing   │
│ WEAKNESSES: Limited customization for enterprises│
├─────────────────────────────────────────────┤
│ OUR OPPORTUNITY: Enterprise customers who   │
│ have outgrown HubSpot's capabilities        │
└─────────────────────────────────────────────┘

---YOUR TASK---
Raw info: "Zoho CRM is a strong player in the SMB market with aggressive pricing,
starting at $14/user/month. Part of the wider Zoho suite which is a major
selling point for businesses already using Zoho products. Often praised for
value for money but criticized for interface complexity and weaker third-party
integrations compared to Salesforce."
```

---

### Few-Shot Example 3 — Brand Voice Training

**Scenario:** Teach the AI your brand's specific writing style using real examples.

```
Write product descriptions in our brand voice.
Our brand is: direct, warm, no-fluff, sustainability-focused, confident.

---EXAMPLE 1---
Product: Organic Cotton T-Shirt
Description: "Soft as a second skin. Grown without pesticides. Worn with
intention. Our Organic Cotton T-Shirt isn't just a shirt — it's 200g of
proof that you don't have to compromise between comfort and conscience.
Machine wash. Tumble dry. Repeat."

---EXAMPLE 2---
Product: Bamboo Cutting Board
Description: "Harder than maple. Gentler on your knives. Grown without
irrigation or fertilizers. Your kitchen's new daily companion is also
one of the planet's fastest-renewable materials. It's not just a cutting
board. It's a better decision, twice a day."

---EXAMPLE 3---
Product: Recycled Glass Water Bottle
Description: "Made from glass that was already living its second life —
now living its third. BPA-free by nature, not by design. Keeps your water
at exactly the temperature you poured it. The planet put in the work.
We just gave it a handle."

---YOUR TASK---
Product: Recycled Denim Jacket
Key facts: Made from 100% post-consumer recycled denim. Equivalent of
3 pairs of jeans diverted from landfill per jacket. Available in 4 faded
colorways. Classic fit.
```

---

## 7.4 Designing High-Quality Examples

The quality of your few-shot examples is the most critical factor in few-shot prompting. Bad examples teach bad patterns.

### Principles for Excellent Examples

**Principle 1: Represent the Full Range**

Your examples should cover the variety of inputs you expect, not just easy cases.

```
Classification task — Good example set:
Example 1: Clear positive case
Example 2: Clear negative case
Example 3: An edge case (mixed, borderline)

Classification task — Bad example set:
Example 1: Easy positive
Example 2: Easy positive
Example 3: Easy positive
→ AI learns to classify everything as positive
```

**Principle 2: Perfect Consistency**

Every example must follow exactly the same format. Any variation teaches inconsistency.

```
❌ INCONSISTENT EXAMPLES:
Example 1 output: "Sentiment: Positive | Topic: Delivery"
Example 2 output: "POSITIVE sentiment. Issue = product quality"
Example 3 output: "negative"

✅ CONSISTENT EXAMPLES:
Example 1 output: "SENTIMENT: Positive | TOPIC: Delivery"
Example 2 output: "SENTIMENT: Negative | TOPIC: Product Quality"
Example 3 output: "SENTIMENT: Neutral | TOPIC: Price"
```

**Principle 3: Show Reasoning for Complex Classifications**

If the classification is nuanced, include a brief reasoning step in the example output. This teaches the model to reason before concluding.

```
Output format with reasoning:
"CLASSIFICATION: Mildly Negative
REASONING: Customer acknowledges product quality is fine but is ending
the relationship due to poor service — service failure dominates."
```

**Principle 4: Correctness Above Everything**

Every example output must be exactly what you want the AI to produce for that input. If your examples have errors, the AI will learn to make the same errors.

**Principle 5: Diversity of Phrasing**

If your real inputs will use varied language, your examples should too. Don't use artificially similar sentences.

```
❌ Examples too similar:
Input 1: "The product is great. I love it."
Input 2: "The item is wonderful. I really like it."
Input 3: "This product is excellent. I enjoy it."
→ AI learns only one pattern

✅ Diverse examples:
Input 1: "The product is great. I love it."
Input 2: "Terrible experience. Never again."
Input 3: "Works as expected, nothing special."
```

---

## 7.5 How Many Examples to Use

| Number of Examples | Name | When to Use |
|-------------------|------|------------|
| 0 | Zero-shot | Standard tasks; format not critical |
| 1 | One-shot | Format is the main concern; task is clear |
| 2–3 | Few-shot | Custom format + moderate nuance |
| 4–6 | Multi-shot | Complex nuanced classification; brand voice |
| 7+ | Extended few-shot | Very complex patterns (consider fine-tuning instead) |

**Diminishing returns:** After 5–6 good examples, adding more examples typically gives minimal improvement. The token cost may not be worth it.

**The sweet spot:** 3 diverse, well-crafted examples usually achieve 85–90% of what perfect few-shot can deliver.

---

## 7.6 Few-Shot for Code Tasks

Few-shot is highly effective for establishing code patterns — function signatures, docstring styles, test structures.

**Example — Establish coding style:**

```python
"""
Write Python functions in our team's standard style.

EXAMPLE 1:
Task: Function to validate email format

def validate_email(email: str) -> bool:
    """
    Check if the provided string is a valid email address.

    Args:
        email: The email string to validate.

    Returns:
        True if valid email format, False otherwise.

    Example:
        >>> validate_email("user@example.com")
        True
        >>> validate_email("not-an-email")
        False
    """
    import re
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))

EXAMPLE 2:
Task: Function to safely parse an integer from a string

def safe_parse_int(value: str, default: int = 0) -> int:
    """
    Safely parse an integer from a string, returning a default on failure.

    Args:
        value: The string to parse.
        default: Value to return if parsing fails. Defaults to 0.

    Returns:
        Parsed integer or the default value.

    Example:
        >>> safe_parse_int("42")
        42
        >>> safe_parse_int("not-a-number")
        0
        >>> safe_parse_int("not-a-number", default=-1)
        -1
    """
    try:
        return int(value)
    except (ValueError, TypeError):
        return default

YOUR TASK:
Task: Function to truncate a string to a maximum length, adding ellipsis if truncated
"""
```

---

## 7.7 Few-Shot vs. Fine-Tuning — When to Use Each

| Approach | Best When | Cost | Flexibility |
|----------|-----------|------|------------|
| **Few-shot** | You need consistent patterns for a moderate number of tasks; requirements change occasionally | Token cost per API call | High — change examples to change behavior |
| **Fine-tuning** | You need consistent behavior at very high volume (millions of calls); pattern is stable and well-defined | Training compute + storage | Low — changing behavior requires retraining |

**Rule of thumb:** Start with few-shot. Move to fine-tuning only when you are running the same pattern millions of times and the token cost of examples becomes significant.

---

## Hands-On Activities — Session 7

---

### Activity 7.1 — One-Shot Template Builder

**Objective:** Build a one-shot prompt for a recurring professional task.

**Task:** Choose any structured document you write regularly (weekly report bullet, meeting follow-up, client update, LinkedIn comment).

1. Write one perfect example of that document (your best real example)
2. Build a one-shot prompt using it as the example
3. Test it on a new scenario
4. Evaluate: Did the AI match the format, length, and tone of your example?

---

### Activity 7.2 — Brand Voice Training

**Objective:** Train an AI on a real brand's voice using few-shot examples.

1. Choose any brand you know well (your company, a company you admire, or a well-known consumer brand)
2. Find or write 3 real examples of their content (social posts, product copy, email headers)
3. Build a few-shot prompt using these examples
4. Ask the AI to generate:
   - A new social media post for an upcoming product launch
   - A 50-word product description for a new product
   - A customer email response

**Evaluate:** Show the outputs to someone familiar with the brand. Do they feel "on-brand"?

---

### Activity 7.3 — Zero-Shot vs. Few-Shot Comparison

**Objective:** Prove to yourself when few-shot adds significant value over zero-shot.

**Task:** Custom ticket priority classification

Your company's priority levels are:
- **P0 — Critical:** System is down; revenue impact or data loss occurring NOW
- **P1 — High:** Major feature broken; significant user impact; no workaround
- **P2 — Medium:** Feature degraded; workaround exists; affects many users
- **P3 — Low:** Minor issue; cosmetic; affects few users; workaround easy

**Step 1:** Run a ZERO-SHOT prompt:
```
"Classify the following support tickets as P0, P1, P2, or P3 based on severity."
[Paste 5 tickets]
```

**Step 2:** Build a FEW-SHOT prompt with one example per priority level showing how to classify.

**Step 3:** Run the same 5 tickets through the few-shot version.

**Compare:** Which was more accurate? Which was more consistent in format?

**Suggested test tickets:**
1. "App not loading for anyone — all users blocked since 10 AM"
2. "Export to PDF broken — users can use Excel export as workaround"
3. "Button label has typo on settings page"
4. "Dashboard charts show wrong date range for some users, some dates work fine"
5. "Our entire payment processing is down — no orders going through"

---

### Activity 7.4 — Few-Shot Classifier Construction

**Objective:** Build a production-ready few-shot classifier for a real business task.

**Scenario:** You manage content for an online education platform. User-submitted course reviews need to be tagged automatically.

Tags needed:
- `content_quality` — comments about course content, accuracy, depth
- `instructor` — comments about teaching style, explanation, engagement
- `platform` — comments about the website, app, technical issues
- `price_value` — comments about cost relative to value
- `support` — comments about customer service or technical support

Build a 5-example few-shot prompt (one per tag), then test with 8 new reviews. Format output as:
`Review # | Primary Tag | Secondary Tag (if any) | Confidence (High/Medium/Low)`

---

## Revision Questions — Session 7

1. What is in-context learning and how does few-shot prompting use it?
2. You need to teach an AI to write in your company's specific email style. Why is zero-shot insufficient and how would you use few-shot instead?
3. What are the 5 principles of designing high-quality few-shot examples?
4. Why might 3 diverse examples outperform 8 similar examples?
5. A colleague builds a few-shot classifier but notices the AI always chooses the category shown in Example 1. What is the likely cause and how would they fix it?
6. When does fine-tuning become preferable to few-shot prompting?
7. Describe how you would use few-shot prompting to establish a custom output format that doesn't follow any standard structure.
8. You are building a few-shot prompt for email tone classification. Write one example input-output pair that would demonstrate the "Passive-Aggressive" tone category.

---

## Key Takeaways — Session 7

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 7 KEY TAKEAWAYS                                             │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Few-shot = in-context learning from your examples                │
│    The model temporarily learns from your prompt, not retraining    │
│                                                                      │
│  ✓ One-shot: use when format is the main concern                    │
│    Few-shot (2–5): use for nuanced classification, brand voice      │
│    5+ examples: use for complex custom patterns                     │
│                                                                      │
│  ✓ Example quality matters more than example quantity               │
│    3 excellent examples > 8 mediocre ones                           │
│                                                                      │
│  ✓ Key design principles: representative, consistent, correct,      │
│    diverse phrasing, show reasoning for nuanced tasks               │
│                                                                      │
│  ✓ Killer use cases: brand voice, custom formats, nuanced           │
│    classification, consistent extraction patterns                   │
│                                                                      │
│  ✓ Fine-tuning is the next step only at massive scale —             │
│    start always with few-shot                                        │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 7 Complete → Proceed to Session 8: Chain-of-Thought Prompting*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
