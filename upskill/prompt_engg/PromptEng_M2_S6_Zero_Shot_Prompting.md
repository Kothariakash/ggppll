# Session 6: Zero-Shot Prompting
## Module 2 — Prompting Techniques
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 6 OF 30  │  Module 2, Session 1                           │
│  Topic: Zero-Shot Prompting — Getting Results Without Examples      │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Define zero-shot prompting and explain why it works
2. Identify when zero-shot is the right technique to use
3. Write effective zero-shot prompts for classification, extraction, summarization, and Q&A tasks
4. Improve zero-shot effectiveness using instruction clarity and structured formatting
5. Recognize when zero-shot is insufficient and another technique is needed
6. Build a zero-shot prompt template for your most frequent professional task

---

## 6.1 What is Zero-Shot Prompting?

**Zero-shot prompting** means asking an AI to perform a task without providing any examples of how to complete it. You rely entirely on the model's pre-existing knowledge — learned during training on billions of documents — to understand and execute the task.

The term comes from machine learning research:
- **Zero-shot**: no examples provided → AI uses general knowledge
- **One-shot**: one example provided → Session 7
- **Few-shot**: multiple examples provided → Session 7

### Why Zero-Shot Works

During training on massive datasets, LLMs encountered countless examples of nearly every common task: classification, summarization, translation, Q&A, formatting, and more. They learned what "good" output looks like for these tasks without needing examples in the prompt.

This makes zero-shot prompting both fast and surprisingly powerful for standard tasks.

```
ZERO-SHOT MENTAL MODEL:

Before LLMs, you had to "train" a classifier:
  "Here are 1,000 examples of spam emails and 1,000 legitimate emails.
   Learn to tell the difference." (supervised ML)

With an LLM zero-shot:
  "Classify this email as spam or legitimate."
  → The model already knows what spam looks like from training.
     No examples needed.
```

---

## 6.2 Zero-Shot Prompt Structure

```
[OPTIONAL ROLE] + [CLEAR TASK INSTRUCTION] + [INPUT DATA] + [OPTIONAL FORMAT SPEC]
```

The most important element is **instruction clarity**. Without examples to guide interpretation, your instructions must leave no room for ambiguity.

### The Clarity Spectrum

```
LEAST EFFECTIVE (Maximum ambiguity):
"Tell me about this text."
→ AI must guess: summarize? analyze? classify? What aspect?

LOW CLARITY:
"Is this email good or bad?"
→ Good in what sense? Tone? Grammar? Effectiveness?

MEDIUM CLARITY:
"Classify this email as professional or unprofessional."
→ Better — but what criteria define professional?

HIGH CLARITY:
"Classify this customer email as Professional, Neutral, or Unprofessional
based on: tone, grammar, clarity, and appropriateness for business context.
Output only the classification word, then a one-sentence justification."
→ Unambiguous task, clear criteria, defined output format
```

---

## 6.3 Zero-Shot Applications — Complete Examples

### Application 1: Classification

Classification is where zero-shot excels most. The model understands category definitions from training.

**Example 1A — Sentiment Classification:**

```
Classify the sentiment of the following customer review.
Output exactly: Positive, Negative, or Neutral.
Then provide a one-sentence justification.

Review: "The product quality is excellent and exactly as described,
but the delivery took 12 days instead of the promised 3–5 days."
```

**Expected output:**
```
Neutral.
The review expresses satisfaction with product quality but significant
disappointment with the delivery timeline, resulting in a mixed sentiment.
```

**Example 1B — Multi-Category Classification:**

```
Classify the following support ticket into exactly one category:
Technical Issue | Billing | Shipping | Product Quality | General Inquiry

Rules:
- Choose the category that best represents the PRIMARY issue
- If multiple issues exist, choose the most urgent one
- Output format: CATEGORY: [category] | REASON: [one sentence]

Ticket: "I can't log into my account since the update yesterday,
and I'm also being billed twice for this month's subscription."
```

**Expected output:**
```
CATEGORY: Technical Issue | REASON: Account access is blocking the user's
ability to use the service, making it more immediately urgent than the
billing issue, which can be corrected after access is restored.
```

**Example 1C — Batch Classification (efficient format):**

```
Classify each of the following items as Risk Level: Low, Medium, or High.
Context: We are evaluating risks in a software product launch.

Format: Number | Risk statement | Risk Level | Brief reason (max 10 words)

Items to classify:
1. One engineer who knows the entire codebase is leaving next month
2. The app has not been load-tested above 1,000 concurrent users
3. We have not yet finalized the app icon
4. Our payment gateway has a known intermittent error under high load
5. The marketing landing page copy is still being reviewed
```

---

### Application 2: Information Extraction

Zero-shot excels at pulling specific information from unstructured text.

**Example 2A — Entity Extraction:**

```
Extract the following information from the job posting below.
If a field is not mentioned, write "Not specified."

Fields to extract:
- Job Title
- Company Name
- Location
- Work Mode (On-site / Hybrid / Remote / Not specified)
- Required Experience (years)
- Salary Range
- Application Deadline

Job Posting:
"We are TalentBridge Solutions, a growing HR tech company based in Bengaluru.
We're looking for a Senior Product Manager to join our team. The role requires
5–8 years of product management experience in B2B SaaS. Work from our
Koramangala office 3 days per week. Compensation: ₹30–40 LPA + ESOP.
Applications accepted until March 31st."
```

**Example 2B — Contract Clause Extraction:**

```
Read the following contract clause and extract:
1. The obligation (who must do what)
2. The deadline or timeframe
3. The consequence of non-compliance
4. Any exceptions or conditions

Present as a structured list with bold labels.

Clause: "The Vendor shall deliver all contracted software modules to the
Client no later than 90 calendar days from the date of contract execution.
Failure to deliver within this period, unless caused by documented Force
Majeure events approved in writing by both parties, shall entitle the Client
to a penalty of 2% of the total contract value per week of delay, up to a
maximum of 20% of the total contract value."
```

**Example 2C — Key Point Extraction from Long Documents:**

```
Read the following meeting transcript excerpt and extract:
1. All DECISIONS made (numbered list)
2. All ACTION ITEMS (format: task | owner | deadline)
3. All OPEN QUESTIONS that were raised but not resolved

[Paste meeting transcript here]
```

---

### Application 3: Summarization

**Example 3A — Tiered Summarization:**

```
Summarize the following article at three levels:
Level 1 — Tweet (max 280 characters)
Level 2 — Executive summary (3 sentences)
Level 3 — Key points (5 bullet points)

Label each level clearly.

Article: [Paste article here]
```

**Example 3B — Audience-Specific Summary:**

```
Summarize the following research paper abstract for two different audiences:

Audience A: A non-technical business executive who needs to understand
the business implications only (2 paragraphs)

Audience B: A technical data scientist evaluating methodology and findings
(3 paragraphs, can use technical terms)

Label each summary with the audience name.

Abstract: [Paste abstract here]
```

**Example 3C — Comparative Document Summary:**

```
I have three vendor proposals for the same project. Summarize each proposal
in 3 bullet points covering: key offering, price, and standout differentiator.
Then provide a 2-sentence comparative conclusion.

Proposal 1: [text]
Proposal 2: [text]
Proposal 3: [text]
```

---

### Application 4: Translation and Transformation

**Example 4A — Tone Transformation:**

```
Rewrite the following email to change its tone from aggressive/emotional
to professional/constructive. Keep the core message and facts intact.
Do not add or remove information — only change the tone and language.

Original email:
"I'm absolutely furious about the constant delays on this project.
This is totally unacceptable and frankly unprofessional behavior.
If this isn't fixed by Friday, I'm escalating to your CEO."
```

**Example 4B — Jargon-to-Plain-English:**

```
Rewrite the following technical paragraph in plain English for a
non-technical business audience. No technical terms. If a concept
must be kept, use an everyday analogy. Max 100 words.

Technical text:
"The application leverages a microservices architecture deployed on
containerized infrastructure using Kubernetes orchestration. Each service
communicates asynchronously via a message broker, ensuring eventual
consistency across distributed data stores through event sourcing patterns."
```

**Example 4C — Format Transformation (Text to Table):**

```
Convert the following unstructured text into a structured table.
Columns: Employee Name | Department | Years of Service | Performance Rating | Promotion Recommended

Text:
"Arjun from Engineering has been with us for 6 years and consistently
receives Outstanding ratings — definitely recommend for promotion.
Priya in Marketing has 3 years here, rated as Meets Expectations.
No promotion yet. Rahul in Sales, 8 years, rated Outstanding — strong
promotion candidate. Deepa in HR, 2 years, Exceeds Expectations — worth
considering for promotion."
```

---

### Application 5: Question Answering

**Example 5A — Constrained Q&A:**

```
Answer the following question using ONLY the information provided in the
context below. If the answer is not in the context, say exactly:
"The provided context does not contain enough information to answer this question."
Do not use any outside knowledge.

Question: What is the company's return policy for digital products?

Context: [Paste your document/policy/FAQ here]
```

**Example 5B — Structured Q&A for Research:**

```
Answer the following questions about [TOPIC].
For each answer:
- Keep it under 3 sentences
- If uncertain, say "This is uncertain — verify at [type of source]"
- Do not speculate beyond what is well-established

Questions:
1. What year was [X] founded?
2. Who are the three main competitors of [X]?
3. What is [X]'s current market capitalization (approximate)?
4. What is [X]'s primary revenue model?
```

---

## 6.4 When Zero-Shot is the Right Choice

### Zero-Shot Strength Matrix

| Task Type | Zero-Shot Effectiveness | Why |
|-----------|------------------------|-----|
| Translation (common languages) | ★★★★★ Excellent | Massive training data for all major languages |
| Sentiment analysis | ★★★★★ Excellent | Well-defined, trained heavily |
| Summarization | ★★★★☆ Very Good | Clear, common task |
| Simple classification | ★★★★☆ Very Good | Standard categories |
| Factual Q&A (known topics) | ★★★★☆ Very Good | Knowledge from training |
| Format transformation | ★★★★☆ Very Good | Clear structural task |
| Custom classification | ★★★☆☆ Good | May need examples for nuanced categories |
| Brand voice writing | ★★☆☆☆ Limited | AI can't infer your specific style |
| Complex multi-step reasoning | ★★☆☆☆ Limited | Needs Chain-of-Thought (Session 8) |
| Specialized domain tasks | ★★☆☆☆ Limited | May need persona + examples |
| Novel/unusual output formats | ★☆☆☆☆ Poor | Needs examples to show the format |

### Decision Guide: Zero-Shot vs. Other Techniques

```
Is this a standard, well-defined task? (summarize, classify, translate)
→ YES: Use zero-shot. Focus on clarity.
→ NO: Consider few-shot (Session 7)

Does the output need to match a very specific format or style?
→ YES: Use few-shot — show an example
→ NO: Zero-shot with format spec is sufficient

Does the task require multi-step reasoning?
→ YES: Use Chain-of-Thought (Session 8)
→ NO: Zero-shot or few-shot

Do you need the AI to adopt a very specific expert perspective?
→ YES: Add Persona Prompting (Session 9) to your zero-shot

Is accuracy in complex calculations critical?
→ YES: Use CoT + ask to show work; verify independently
```

---

## 6.5 Advanced Zero-Shot Techniques

### Technique 1: Instruction-Anchored Zero-Shot

Add an instruction that anchors the AI's behavior before the task:

```
You will be given customer feedback. Your job is ONLY to identify the primary
complaint — do not suggest solutions, do not comment on the tone, do not
evaluate the customer's validity. Output only the primary complaint in
one sentence, starting with the subject: "The customer is unhappy about..."

Feedback: [paste here]
```

### Technique 2: Output-Format-Led Zero-Shot

Show the output structure before the input — the AI fills in the template:

```
Analyze the following business problem and fill in this template:

PROBLEM SUMMARY: [1 sentence]
ROOT CAUSE: [most likely cause in 1–2 sentences]
IMPACT: [business impact, 1 sentence]
RECOMMENDED ACTION: [1 specific action]
RISK IF NO ACTION: [1 sentence]

Business problem: [describe the problem here]
```

### Technique 3: Step-Directed Zero-Shot

Tell the AI the exact steps to follow without providing examples:

```
Process the following job application using these exact steps:
Step 1: Extract the candidate's name, role applied for, and years of experience
Step 2: List the top 3 technical skills mentioned
Step 3: Identify any gaps against this requirement: [job requirements]
Step 4: Give a screening recommendation: PROCEED / HOLD / REJECT with one-sentence reasoning

Application text: [paste here]
```

### Technique 4: Negative-Instruction Zero-Shot

Prevent common AI tendencies by explicitly prohibiting them:

```
Summarize this article in 5 bullet points.
Rules:
- Do NOT start any bullet with "The article discusses" or "The author mentions"
- Do NOT include transitional phrases between bullets
- Each bullet must be a standalone, self-contained insight
- No bullet longer than 20 words
- Start each bullet with the key insight word in bold

Article: [paste here]
```

---

## 6.6 Zero-Shot for Common Professional Tasks — Quick Reference

```
EMAIL SUBJECT LINES:
"Generate 5 email subject line options for: [email description].
Each subject line: under 50 characters. Styles: curiosity / urgency /
benefit-led / question / direct. Label each style."

MEETING AGENDAS:
"Create a meeting agenda for: [meeting topic].
Duration: [X] minutes. Attendees: [roles].
Format: Time | Agenda Item | Owner | Goal
Include: 5-minute buffer for late starts, 5-minute actions close."

PROFESSIONAL BIO:
"Write a professional bio for: [name], [role], [company], [background highlights].
Three versions: 50 words (Twitter bio) | 100 words (website) | 200 words (conference speaker).
Third person. Active voice. End with a personal detail that humanizes the bio."

PERFORMANCE REVIEW COMMENTS:
"Write a professional performance review comment for an employee who [achievements].
Include: 1 specific strength with evidence, 1 development area with constructive framing,
1 SMART goal for next period. 150 words. Balanced, specific, encouraging."

DATA INTERPRETATION:
"Interpret the following data and provide: key trend (1 sentence), biggest concern
(1 sentence), most positive finding (1 sentence), recommended action (1 sentence).
Data: [paste data or table]"
```

---

## Hands-On Activities — Session 6

---

### Activity 6.1 — Zero-Shot Classification Pipeline

**Objective:** Build a zero-shot prompt that classifies all 5 customer reviews simultaneously.

**Step 1:** Write a single zero-shot prompt that:
- Classifies sentiment as: Strongly Positive / Mildly Positive / Neutral / Mildly Negative / Strongly Negative
- Identifies the primary topic: Product Quality / Delivery / Customer Service / Price / Other
- Gives a follow-up action recommendation for each

**Step 2:** Test with these 5 reviews:

```
Review 1: "Absolutely amazing product! Exceeded all my expectations.
Will tell everyone I know about this."

Review 2: "It arrived 3 days late but the item itself is okay, I guess.
Customer support was responsive when I asked about the delay."

Review 3: "Completely wrong item sent. This is the second time this has
happened. I am cancelling my subscription."

Review 4: "Works as advertised. Nothing exceptional, nothing bad.
Would buy again if I needed it."

Review 5: "The product is fine but ₹3,500 for this seems overpriced
compared to similar items I've seen elsewhere."
```

**Format your output as a table:**

| Review | Sentiment | Primary Topic | Recommended Action |
|--------|-----------|-------------|-------------------|
| 1 | | | |
| ... | | | |

---

### Activity 6.2 — Zero-Shot Extraction Template

**Objective:** Build a reusable zero-shot extraction prompt for job postings.

Create a prompt that extracts from any job posting:
- Job title
- Company name and brief description
- Location and work mode
- Required experience
- Required skills (must-have + nice-to-have separated)
- Compensation (if mentioned)
- Application deadline (if mentioned)
- 3 "green flags" about the role (why a candidate would want it)
- 1 "watch out" if anything seems concerning

Test your prompt on a real job posting from LinkedIn or Naukri.

---

### Activity 6.3 — Instruction Clarity Comparison

**Objective:** Experience how instruction clarity transforms zero-shot results.

Run these 4 versions of the same prompt and compare outputs:

**Version 1 (Minimal):**
```
"Analyze this business."
[Paste a short description of any business — real or fictional]
```

**Version 2 (Task specified):**
```
"Analyze the strengths and weaknesses of this business."
[Same business description]
```

**Version 3 (Task + Format):**
```
"Analyze the strengths and weaknesses of this business.
Format as a table: Category | Strength | Weakness | Implication"
[Same business description]
```

**Version 4 (Full CRAFT + structured zero-shot):**
```
"You are a business consultant specializing in SME growth strategy.
Analyze the following business for: market positioning, operational
strengths, key risks, and growth opportunities.

Format as 4 sections with these exact headers:
MARKET POSITIONING: (2–3 sentences)
OPERATIONAL STRENGTHS: (3 bullet points)
KEY RISKS: (3 bullet points, each with risk level: High/Medium/Low)
GROWTH OPPORTUNITIES: (3 bullet points, each with timeframe: Short/Medium/Long term)

Business description: [paste here]"
```

Document how quality improved at each step. Which single change had the biggest impact?

---

### Activity 6.4 — Build Your Zero-Shot Template

**Objective:** Create a reusable zero-shot template for your most frequent professional task.

Think of the one task you do most frequently that involves reading, writing, or analyzing text.

Build a zero-shot template for it with:
- Clear instruction anchoring
- Defined output format
- At least 3 constraints
- Variable placeholders in [BRACKETS]

Run it with real data. Iterate once. Save it to your prompt library.

---

## Revision Questions — Session 6

1. What does "zero-shot" mean in the context of LLM prompting? Why does it work without examples?
2. What is the single most important factor that determines zero-shot effectiveness?
3. A colleague says "I asked ChatGPT to classify these emails and the results were inconsistent." What is the most likely cause and what would you recommend?
4. Name 3 tasks where zero-shot works excellently and 3 where it is insufficient. Explain why for each.
5. What is the difference between "output-format-led zero-shot" and standard zero-shot? When would you use the output-format-led approach?
6. You need to extract 8 specific fields from 200 unstructured customer records. Design the zero-shot extraction prompt structure you would use.
7. Why do negative instructions ("do not start bullets with X") improve zero-shot output quality?
8. Describe the decision process you would use to decide whether to use zero-shot or switch to a different technique.

---

## Key Takeaways — Session 6

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 6 KEY TAKEAWAYS                                             │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Zero-shot = no examples; relies on model's training knowledge    │
│                                                                      │
│  ✓ Instruction clarity is the #1 determinant of zero-shot quality   │
│                                                                      │
│  ✓ Zero-shot excels at: classification, extraction, summarization,  │
│    translation, format transformation                                │
│                                                                      │
│  ✓ Zero-shot is insufficient for: custom styles, complex reasoning, │
│    unusual output formats, specialized niche tasks                   │
│                                                                      │
│  ✓ Advanced techniques: instruction-anchored, output-format-led,    │
│    step-directed, negative-instruction zero-shot                     │
│                                                                      │
│  ✓ Decision rule: Standard task + clear instruction = zero-shot     │
│    Custom format/style needed = move to few-shot (Session 7)        │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 6 Complete → Proceed to Session 7: Few-Shot Prompting*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
