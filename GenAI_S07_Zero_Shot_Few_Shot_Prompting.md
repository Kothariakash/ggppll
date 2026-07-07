# Session 7: Zero-Shot, One-Shot & Few-Shot Prompting
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 2 — PROMPT ENGINEERING                                               │
│  SESSION 7 of 30  |  1 Hour  |  40% Theory + 60% Hands-On                  │
│                                                                              │
│  "Show, don't just tell. Examples are the most powerful instruction         │
│   you can give an AI model."                                                 │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 7, you will be able to:

- Define zero-shot, one-shot, and few-shot prompting and explain when to use each
- Design high-quality examples that guide AI toward your desired output
- Apply few-shot prompting to classification, formatting, and tone-matching tasks
- Understand why examples outperform instructions for style and format replication
- Build reusable prompt templates with embedded examples
- Diagnose when a zero-shot prompt is failing and upgrade it to few-shot

---

## 1. The Three Prompting Approaches

### 1.1 The Core Concept

The terms "zero-shot," "one-shot," and "few-shot" describe **how many examples you provide in your prompt** to guide the AI's output.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                                                                              │
│  ZERO-SHOT:  No examples given. Just the instruction.                       │
│              "Write a product tagline for a running shoe brand."            │
│                                                                              │
│  ONE-SHOT:   One example given to show the pattern.                         │
│              "Example: Nike Air Max → 'Just Do It'                          │
│               Now write a tagline for a running shoe brand called Strideo." │
│                                                                              │
│  FEW-SHOT:   Multiple examples (2–8) given to firmly establish the pattern. │
│              "Here are 3 examples of our tagline style:                     │
│               [example 1] | [example 2] | [example 3]                      │
│               Now write a tagline for Strideo in the same style."           │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

The key insight: **examples communicate requirements that instructions alone cannot fully capture** — especially for style, tone, format, and domain-specific conventions.

---

### 1.2 Zero-Shot Prompting

**Definition:** Providing the AI with only instructions, no examples. The AI relies entirely on its training data to infer the correct approach.

**When Zero-Shot Works Well:**

```
✓ General tasks the AI has seen many times in training
  "Summarize this paragraph in 2 sentences."
  "Translate this text to Spanish."
  "List 5 benefits of remote work."

✓ Standard formats (emails, reports, lists)
  "Write a professional apology email."
  "Create a table comparing these 3 options."

✓ Factual Q&A with clear answers
  "What is the difference between gross margin and net margin?"

✓ Simple transformations
  "Convert this paragraph from passive to active voice."
```

**When Zero-Shot Struggles:**

```
✗ Highly specific style or tone you want replicated
  "Write in my brand voice" — AI doesn't know your brand voice

✗ Domain-specific formats it hasn't seen often
  "Write an SOP in our company's internal format"

✗ Classification tasks where your categories are non-standard
  "Classify these support tickets by our internal priority system"

✗ Tasks requiring specific output structure unique to your organization
```

**Zero-Shot Example — Business Use:**

```
PROMPT:
Write a one-paragraph executive summary of the following findings:
[paste your findings here]

Executive summary should:
- Lead with the most important insight
- Include one key number or statistic
- End with the primary recommendation
- Be under 80 words

RESULT: Works well for standard summary tasks.
```

---

### 1.3 One-Shot Prompting

**Definition:** Providing exactly one example alongside your instruction. The example demonstrates the pattern you want replicated.

**The Power of One Good Example:**

Without example (zero-shot):
```
PROMPT: Write a product review response for negative feedback.

OUTPUT: Generic, formal corporate response that sounds defensive.
```

With one example (one-shot):
```
PROMPT:
Write a response to a negative product review. 

Here is an example of the style and tone we use:

EXAMPLE:
Customer review: "The delivery took 2 weeks and the packaging was damaged."
Our response: "Hi Priya! We're so sorry about your experience — that's
absolutely not the standard we hold ourselves to. We've already flagged
this with our logistics team. We'd love to make this right: can you DM us
your order number? A full replacement is on its way once we confirm.
Thank you for giving us a chance to fix this."

Now write a response to this review:
Customer review: "The product quality is much worse than the photos suggested."

OUTPUT: AI closely matches the warm, empathetic, action-oriented style 
of the example — far better than the zero-shot generic response.
```

**One-Shot is ideal for:**
- Tone and style matching
- Format replication
- When you have one strong example from past work
- When zero-shot is producing something close but not quite right

---

### 1.4 Few-Shot Prompting

**Definition:** Providing 2–8 carefully chosen examples that collectively establish a clear, consistent pattern the AI should follow.

**Why More Examples Work Better:**

```
1 example: AI learns one pattern but may not generalize well
3 examples: AI identifies the pattern confidently
5+ examples: AI has very high pattern confidence; output highly consistent
```

**The Classic Few-Shot Structure:**

```
[INSTRUCTION]

EXAMPLES:

Input: [example input 1]
Output: [example output 1]

Input: [example input 2]
Output: [example output 2]

Input: [example input 3]
Output: [example output 3]

Now complete this:
Input: [your actual input]
Output:
```

---

## 2. Designing High-Quality Examples

The quality of your examples determines the quality of the output. Poorly chosen examples mislead the AI; excellent examples produce consistent, usable results.

### 2.1 The 5 Principles of Good Few-Shot Examples

**Principle 1: Variety — Cover Different Cases**
```
BAD (too similar):
  Example 1: Positive review → "Thank you for the kind words!"
  Example 2: Positive review → "We're so glad you loved it!"
  Example 3: Positive review → "Wonderful feedback, thank you!"

GOOD (varied inputs):
  Example 1: Positive review → warm appreciation response
  Example 2: Neutral/mixed review → acknowledge + invite conversation
  Example 3: Negative review → empathize + resolve + offer solution
```

**Principle 2: Consistency — Same Pattern Throughout**
```
BAD (inconsistent tone):
  Example 1 response: "Dear valued customer, we sincerely apologize..."
  Example 2 response: "Hey! So sorry about that, let's fix it asap :)"

The AI will average out the mixed signals and produce something inconsistent.

GOOD: Every example uses the same tone, structure, and formality level.
```

**Principle 3: Length Calibration — Examples Match Desired Length**
```
If you want 50-word responses: your examples should be ~50 words
If you want single-line outputs: your examples should be single lines
If you want multi-paragraph: your examples should be multi-paragraph

AI calibrates output length based on example length.
```

**Principle 4: Representative — Examples Cover the Real Use Cases**
```
If your actual inputs are angry customer emails,
your examples should be angry customer emails — not polite ones.

Match your examples to the actual inputs you will feed in.
```

**Principle 5: Correct — Examples Must Be Your Best Work**
```
AI learns from your examples EXACTLY.
If your examples contain errors, jargon, or weak writing,
the AI will replicate those flaws.

Your examples = your quality standard.
```

---

### 2.2 Few-Shot for Classification Tasks

Classification is one of the most powerful few-shot applications in business — categorizing customer feedback, tagging support tickets, sorting leads, grading responses.

**Example: Customer Feedback Classification**

```
PROMPT:
Classify each customer comment into one of these categories:
PRODUCT_QUALITY | DELIVERY | CUSTOMER_SERVICE | PRICING | OTHER

EXAMPLES:

Comment: "The stitching came apart after 2 washes."
Category: PRODUCT_QUALITY

Comment: "It took 3 weeks to arrive and the tracking never updated."
Category: DELIVERY

Comment: "The agent I spoke to was rude and unhelpful."
Category: CUSTOMER_SERVICE

Comment: "Love the product but ₹2,500 feels steep for what it is."
Category: PRICING

Comment: "I ordered red but received blue."
Category: OTHER

Now classify these:
Comment: "The zipper broke on the first use."
Category:

Comment: "Your website kept crashing when I tried to checkout."
Category:

Comment: "Great quality but I wish there were more size options."
Category:
```

**Why few-shot works here:** The examples precisely define what each category means in your context — which generic zero-shot classification cannot know.

---

### 2.3 Few-Shot for Tone and Style Replication

One of the most valuable professional applications — making AI write in your brand voice, your personal writing style, or a specific communication register.

**Example: Replicating a Company's Email Tone**

```
PROMPT:
Write customer emails in the style and tone shown in these examples.
Our brand voice is: warm, direct, helpful, never formal or stiff.

EXAMPLE 1:
Situation: Customer asks about return policy
Our response: "Hey! Great question. Our return window is 30 days from
delivery — no questions asked, no receipts needed. Just reach out and
we'll send you a prepaid label. Simple as that."

EXAMPLE 2:
Situation: Customer reports a delayed order
Our response: "Oh no, that's not okay and we completely understand your
frustration. We've tracked down your order — it's stuck at the Mumbai
hub and should reach you by Thursday. If it doesn't, reply here and
we'll make it right, guaranteed."

EXAMPLE 3:
Situation: Customer asks if a product is available in blue
Our response: "Yes! Blue just came back in stock this week — and it's
looking amazing. Here's the direct link: [link]. Grab it fast, it tends
to sell out over weekends!"

Now write a response to:
Situation: Customer asks about the difference between the Standard and
Premium subscription plans.
```

---

### 2.4 Few-Shot for Structured Data Extraction

AI can extract structured information from unstructured text — a powerful automation use case.

**Example: Extracting Meeting Action Items**

```
PROMPT:
Extract action items from meeting notes. Format each as:
TASK | OWNER | DEADLINE

EXAMPLES:

Meeting notes: "Priya will send the updated proposal to the client
by end of this week. Rahul needs to set up the demo environment before
the Friday call. We agreed that Ananya would follow up with legal
about the contract terms — she said she'd have an update by next Tuesday."

Extracted:
TASK: Send updated proposal to client | OWNER: Priya | DEADLINE: End of week
TASK: Set up demo environment | OWNER: Rahul | DEADLINE: Before Friday call
TASK: Follow up with legal on contract terms | OWNER: Ananya | DEADLINE: Next Tuesday

---

Meeting notes: "The design team (led by Vikram) will finalize mockups
by March 15. Marketing should review and provide feedback within 3 days
of receiving them. Dev sprint planning is Zara's responsibility —
she'll share the sprint board by Monday morning."

Extracted:
TASK: Finalize UI mockups | OWNER: Vikram (Design team) | DEADLINE: March 15
TASK: Review mockups and provide feedback | OWNER: Marketing team | DEADLINE: 3 days after receipt
TASK: Share sprint board | OWNER: Zara | DEADLINE: Monday morning

---

Now extract from:
Meeting notes: "CFO Meera will present the budget variance analysis to
the board by the 20th. IT needs to complete the server migration before
the quarter end. The compliance team — specifically Dev — must submit
the regulatory filing by April 5th, no exceptions."
```

---

## 3. Choosing Between Zero-Shot, One-Shot, and Few-Shot

### 3.1 The Decision Framework

```
START: What type of output do I need?
         │
         ├─► Standard format (email, summary, list)?
         │     → Start with ZERO-SHOT (CRAFT prompt)
         │     → If output is close but style is off → upgrade to ONE-SHOT
         │
         ├─► Specific style, tone, or brand voice?
         │     → Start with ONE-SHOT (one strong example)
         │     → If still inconsistent → upgrade to FEW-SHOT (3–5 examples)
         │
         ├─► Classification or labeling task?
         │     → Always use FEW-SHOT (minimum 2 examples per category)
         │
         ├─► Structured data extraction?
         │     → FEW-SHOT with exact format examples
         │
         └─► Complex reasoning or analysis?
               → Zero-shot with detailed CRAFT prompt
               → If still weak → chain-of-thought (Session 8)
```

### 3.2 Comparison Table

| Criterion | Zero-Shot | One-Shot | Few-Shot |
|-----------|-----------|----------|----------|
| **When to use** | Standard tasks | Style matching | Classification, tone replication |
| **Example count** | 0 | 1 | 2–8 |
| **Best for** | General tasks | Incremental improvement | Consistent pattern enforcement |
| **Effort to set up** | Low | Medium | Higher (but reusable) |
| **Output consistency** | Variable | Better | High |
| **Prompt length** | Short | Medium | Longer |

---

## 4. Building Reusable Few-Shot Templates

### 4.1 The Template Approach

The real ROI of few-shot prompting comes from building templates you reuse. Write the examples once, save the template, and use it repeatedly with different inputs.

**Template Structure:**

```
[TEMPLATE NAME: Customer Review Response]
[LAST UPDATED: January 2025]
[SUITABLE FOR: Customer service team, e-commerce]

INSTRUCTIONS:
You are our customer service specialist. Write responses to customer reviews
in our brand voice: warm, empathetic, action-oriented, never defensive.
Always: acknowledge → empathize → offer solution → invite further contact.

EXAMPLES:
[Example 1 input] → [Example 1 output]
[Example 2 input] → [Example 2 output]
[Example 3 input] → [Example 3 output]

TEMPLATE INPUT (replace with actual review):
Customer review: [PASTE REVIEW HERE]
Our response:
```

---

### 4.2 Few-Shot Template: Sales Email Follow-Up

```
TEMPLATE: Sales Follow-Up Email Generator
PURPOSE: Re-engage leads who have gone quiet after a proposal or demo

BRAND VOICE: Professional, warm, value-focused. Never pushy. 
Show genuine interest in their success, not just the sale.

EXAMPLES:

Context: Lead went quiet 10 days after receiving proposal for HR software
Follow-up: "Hi Rahul, hope this week is treating you well. I wanted to
check in on the proposal — I know decisions like this involve several
stakeholders and timelines can shift. We recently helped a company similar
to yours cut their HR admin time by 40%. Happy to jump on a 15-minute call
to address any questions or adjust the proposal if priorities have changed.
No pressure — just here to help. — Anita"

---

Context: Lead went quiet 2 weeks after a product demo for marketing platform
Follow-up: "Hi Priya, it's been a couple of weeks since we walked through
the platform together. I remember you mentioned content approval workflows
were a big pain point — we just released a new feature specifically for
that. Would love to show you. If the timing isn't right, just say the word
and I'll circle back when it works better for you. Best, Rohan"

---

Now generate a follow-up for:
Context: [PASTE CONTEXT HERE — what was offered, how long ago, any known concern]
Follow-up:
```

---

## 5. Real-World Example: Few-Shot at a Customer Analytics Company

**Company:** An e-commerce analytics startup (200 employees)

**Problem:** Customer success managers (CSMs) were spending 2–3 hours per week writing personalized account health summaries for their clients. Each summary needed to:
- Match the company's established report format
- Reference specific metrics from the client's account
- Use a confident, advisory tone
- Highlight risks and opportunities

**Zero-shot attempt:** Generic, didn't follow format, required complete rewriting.

**Solution — Few-Shot Template:**

The team's best CSM wrote 5 excellent account summaries. These became the few-shot examples in a template. The team could now:
- Paste the client's metrics into the template
- Run in ChatGPT
- Get an 80% draft in 3 minutes
- Edit in 10 minutes (vs. 2–3 hours)

**Result:**
- Time per summary: 2.5 hours → 15 minutes (90% reduction)
- 8 CSMs × 5 clients × 15 min = 10 hours/week (vs. 100 hours previously)
- Quality became more consistent than pure human drafts

---

## 6. Hands-On Lab 7: Zero-Shot vs. Few-Shot Comparison

**Objective:** Experience firsthand how examples transform output quality  
**Duration:** 25 minutes  
**Tool:** ChatGPT

---

### Exercise A: The Classification Challenge (10 minutes)

**Part 1 — Zero-Shot Attempt:**
```
Classify these support tickets by priority: HIGH, MEDIUM, or LOW.

Ticket 1: "I can't log into my account at all."
Ticket 2: "Can you add a dark mode to the app?"
Ticket 3: "The invoice from last month has the wrong company name."
Ticket 4: "The export function is a bit slow sometimes."
Ticket 5: "I've been charged twice for my subscription this month."
```

Record the AI's classifications.

**Part 2 — Few-Shot Upgrade:**
```
Classify support tickets as HIGH, MEDIUM, or LOW priority.
Use these examples to understand our priority standards:

Ticket: "I cannot access my account and have a client demo in 1 hour." → HIGH
Ticket: "My password reset email is going to spam." → HIGH
Ticket: "The mobile app crashes occasionally when uploading images." → MEDIUM
Ticket: "The date filter in reports doesn't remember my last setting." → MEDIUM
Ticket: "It would be nice to have keyboard shortcuts." → LOW
Ticket: "The loading animation is a bit slow on older devices." → LOW

Now classify:
Ticket 1: "I can't log into my account at all." →
Ticket 2: "Can you add a dark mode to the app?" →
Ticket 3: "The invoice from last month has the wrong company name." →
Ticket 4: "The export function is a bit slow sometimes." →
Ticket 5: "I've been charged twice for my subscription this month." →
```

**Compare:** Did few-shot change any classifications? Were the few-shot results more aligned with what a real support manager would decide?

---

### Exercise B: Style Replication (10 minutes)

Find 2–3 examples of your own professional writing (emails, reports, messages). These become your few-shot examples.

Build a prompt:
```
Write in the exact style and tone of these examples:

EXAMPLE 1:
[Paste a real email or message you wrote]

EXAMPLE 2:
[Paste another real email or message]

Now write: [new task that matches the context of your examples]
```

**Evaluate:** Does the output sound like YOU? What did it get right? What is still off?

---

### Exercise C: Build a Reusable Template (5 minutes)

Based on a task you do repeatedly (weekly reports, client updates, social posts, meeting summaries), build a reusable few-shot template:

```
TEMPLATE NAME: _______________________________
TASK: _______________________________
EXAMPLES: (write 2–3 real examples)
  Input: _____ → Output: _____
  Input: _____ → Output: _____
TEMPLATE INPUT: [PASTE YOUR CONTENT HERE]
```

Save this template — you will use it in Session 10 (Prompt Library).

---

### Lab Evaluation Rubric

| Task | Marks |
|------|-------|
| Exercise A: Both prompts run; classification comparison documented | 3 |
| Exercise B: Style replication attempt + evaluation written | 4 |
| Exercise C: Reusable template built and saved | 3 |
| **Total** | **10** |

---

## 7. Mini Exercise: Identify the Shot Type

For each prompt below, identify whether it is zero-shot, one-shot, or few-shot:

| Prompt | Shot Type |
|--------|-----------|
| "Summarize this email in 3 bullet points." | |
| "Translate: 'Good morning' → 'Buenos días'. Now translate: 'How are you?'" | |
| "Classify: angry → NEGATIVE, delighted → POSITIVE, confusing → NEUTRAL. Now classify: 'This product is decent but the price is too high.'" | |
| "Write a tweet about our product launch." | |
| "Format 1: Q: What is AI? A: AI is... Format 2: Q: What is ML? A: ML is... Now answer: Q: What is NLP?" | |

**Answers:** 1. Zero-shot | 2. One-shot | 3. Few-shot | 4. Zero-shot | 5. Few-shot

---

## 8. Interview Questions — Session 7

**Q1:** *"What is few-shot prompting and when would you use it?"*

**Strong Answer:**
"Few-shot prompting means providing the AI with 2–8 carefully chosen examples alongside your instruction, so it learns the exact pattern you want replicated. I use it when zero-shot prompting produces outputs that are close but not quite right — particularly for style and tone matching, classification tasks with custom categories, and structured data extraction. The examples communicate requirements that instructions alone often cannot capture. For instance, if I want AI to write in my company's specific brand voice, one or two examples of our best past communications are more effective than any written description of our tone."

**Q2:** *"How do you design good few-shot examples?"*

**Strong Answer:**
"Five principles: First, variety — examples should cover different scenarios, not just the easiest case. Second, consistency — all examples must use the same tone, format, and style that I want in the output. Third, length calibration — example outputs should match the target length I want. Fourth, representation — examples should resemble the actual inputs I'll be processing. Fifth, quality — the examples must be my best work, because AI learns and replicates exactly what I show it. Weak examples produce weak outputs."

---

## 9. Revision Questions — Session 7

1. Define zero-shot, one-shot, and few-shot prompting. What distinguishes each?
2. Give a professional example where few-shot dramatically outperforms zero-shot.
3. What are the 5 principles of designing good few-shot examples? Why does each matter?
4. For which types of tasks should you always use few-shot rather than zero-shot?
5. What is the risk of using poorly written examples in a few-shot prompt?
6. How many examples are typically sufficient for a classification task with 4 categories?
7. What is a "reusable few-shot template" and what is its business value?
8. Why does providing 5 examples generally produce more consistent output than providing 1?

---

## 10. Key Terminology — Session 7

| Term | Definition |
|------|-----------|
| **Zero-Shot Prompting** | Providing only instructions with no examples; AI infers from training |
| **One-Shot Prompting** | Providing one example alongside the instruction to establish the pattern |
| **Few-Shot Prompting** | Providing 2–8 examples to firmly establish a pattern the AI should follow |
| **In-Context Learning** | The mechanism by which LLMs learn from examples within the prompt itself |
| **Pattern Recognition (prompting)** | AI's ability to identify the structure/style of examples and extend it |
| **Classification Prompt** | A prompt that instructs AI to categorize inputs into predefined categories |
| **Style Replication** | Using examples to make AI write in a specific voice or format |
| **Template (prompt)** | A reusable prompt structure with placeholders for variable inputs |

---

## 11. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 7 SUMMARY — WHAT TO REMEMBER                                        │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  Zero-shot: instruction only — works for standard, common tasks          │
│  ✓  One-shot: one example — best for style matching and tone calibration    │
│  ✓  Few-shot: 2–8 examples — best for classification, brand voice,          │
│     structured extraction, consistent formatting                             │
│  ✓  Examples > instructions for style, tone, and format requirements        │
│  ✓  5 Principles: Variety, Consistency, Length calibration,                 │
│     Representation, Quality                                                  │
│  ✓  Build reusable few-shot templates for repeated tasks                    │
│  ✓  Your examples ARE your quality standard — make them your best work      │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 8 — Chain-of-Thought & Advanced Prompting Techniques               │
│  (How to make AI reason through complex problems step by step,              │
│   and advanced techniques: self-critique, decomposition, structured         │
│   reasoning for business analysis)                                           │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 7 Complete | Next: Session 8 — Chain-of-Thought & Advanced Prompting*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
