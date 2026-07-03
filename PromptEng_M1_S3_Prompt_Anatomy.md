# Session 3: Prompt Anatomy — The Structure of an Effective Prompt
## Module 1 — Foundations of Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 3 OF 30  │  Module 1, Session 3                           │
│  Topic: Prompt Anatomy — Five Components of a High-Quality Prompt   │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Define the five structural components of an effective prompt
2. Distinguish between weak (unstructured) and strong (structured) prompts
3. Identify which component is missing when an AI response falls short
4. Construct complete, structured prompts for a variety of real-world scenarios
5. Classify prompts by type (instructional, analytical, creative, transformational)
6. Diagnose prompt failures and apply targeted fixes

---

## 3.1 What is a Prompt?

A **prompt** is any input you provide to an AI model to elicit a response. It can be as simple as a single question or as complex as a multi-paragraph document with instructions, examples, context, and constraints.

The most important principle in prompt engineering:

> **The quality of your prompt is the primary determinant of the quality of the AI's response.**

Two people using identical AI tools can get vastly different results — not because of the tool, but because of how they communicate with it.

---

## 3.2 The Five Components of Prompt Anatomy

A well-constructed prompt contains up to five components. You don't always need all five — but knowing each one allows you to identify what's missing when a response falls short.

```
┌──────────────────────────────────────────────────────────────────┐
│              THE FIVE COMPONENTS OF A PROMPT                     │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│   1. ROLE / PERSONA    — Who should the AI be?                   │
│   2. CONTEXT           — What's the situation/background?        │
│   3. TASK              — What should the AI do?                  │
│   4. FORMAT            — How should the output look?             │
│   5. CONSTRAINTS       — What are the rules and limits?          │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

### Component 1: Role / Persona

**What it is:** Instructions telling the AI what identity, expertise, or perspective to adopt.

**Why it matters:** Assigning a role activates the model's training associated with that identity — shaping vocabulary, depth, priorities, and communication style.

**Examples by profession:**

| Role Instruction | Effect on Response |
|-----------------|-------------------|
| "You are a cardiologist..." | Uses medical terminology, references clinical guidelines |
| "You are a kindergarten teacher..." | Uses simple language, analogies, encouraging tone |
| "You are a management consultant at McKinsey..." | Structured frameworks, business language, data-driven |
| "You are a skeptical editor..." | Critical eye, identifies weaknesses, questions assumptions |
| "You are a startup founder with 3 failed ventures..." | Practical, risk-aware, experience-grounded |

**Without a role:**
```
Prompt: "What should I do about my low sales figures?"
Response: Generic advice — could apply to any business
```

**With a role:**
```
Prompt: "You are a B2B sales director with 15 years of experience in
SaaS companies. What should I do about my low sales figures?"
Response: Specific to B2B SaaS context — CRM hygiene, pipeline review,
ICP refinement, sales cycle analysis
```

**Role Template:**
```
You are a [JOB TITLE] with [YEARS/TYPE] of experience in [FIELD/SPECIALTY].
You work with [TYPE OF CLIENTS/ORGANIZATION].
You prioritize [KEY VALUES/APPROACH].
```

---

### Component 2: Context

**What it is:** Background information, situation details, or relevant facts that the AI needs to give a relevant, tailored response.

**Why it matters:** Without context, the AI gives general answers. With context, it gives answers specific to YOUR situation.

**Levels of context:**

**Level 0 — No context:**
```
"How do I increase employee engagement?"
→ Generic HR advice applicable to any company
```

**Level 1 — Basic context:**
```
"I am an HR manager at a 200-person tech startup. How do I increase employee engagement?"
→ More relevant — considers startup culture and tech worker expectations
```

**Level 2 — Rich context:**
```
"I am an HR manager at a 200-person B2B SaaS startup in Bengaluru.
Our team is 80% engineers, ages 24–35. We shifted to fully remote in 2022.
Our latest engagement survey showed: work-life balance (3.2/5) and
recognition (2.8/5) as the lowest-scoring areas. Budget for initiatives: ₹5 lakh.
How do I increase employee engagement?"
→ Highly specific, actionable advice targeting the exact problem areas
```

**Types of context to provide:**

| Context Type | Examples |
|-------------|---------|
| **Who you are** | Role, industry, experience level |
| **Who the audience is** | Age, expertise level, relationship to you |
| **What the situation is** | Problem, current state, history |
| **What constraints exist** | Budget, timeline, resources, approvals needed |
| **What has been tried** | Previous attempts and outcomes |
| **What you have access to** | Tools, data, people, systems |

---

### Component 3: Task / Instruction

**What it is:** The specific action you want the AI to perform. This is the most critical component — without it, nothing else matters.

**Why it matters:** The more precisely you define the task, the more precisely the AI executes it.

**The power of action verbs:**

Weak tasks use vague verbs. Strong tasks use specific action verbs:

| Weak Verb | Strong Alternative | Difference in Output |
|-----------|-------------------|---------------------|
| Help me with... | Write / Analyze / Summarize / Evaluate | Clear direction |
| Talk about... | Explain / Compare / Argue / Critique | Defines the angle |
| Do something about... | Rewrite / Fix / Improve / Optimize | Defines the action |
| Give me info on... | List / Research / Outline / Extract | Defines structure |

**Master list of task action verbs:**

```
GENERATION:   Write, Draft, Create, Generate, Compose, Produce
ANALYSIS:     Analyze, Evaluate, Assess, Critique, Review, Audit
TRANSFORMATION: Rewrite, Translate, Convert, Simplify, Expand, Condense
EXTRACTION:   Summarize, Extract, Identify, List, Find, Locate
COMPARISON:   Compare, Contrast, Differentiate, Benchmark, Rank
EXPLANATION:  Explain, Describe, Define, Illustrate, Clarify, Teach
REASONING:    Argue, Defend, Debate, Challenge, Hypothesize, Predict
ORGANIZATION: Outline, Structure, Categorize, Prioritize, Plan, Map
```

**Single task vs. multi-task (common mistake):**

```
❌ Multi-task in one prompt (reduces quality):
"Analyze my business idea, write a business plan, create financial projections,
and suggest marketing strategies."

✅ Sequential single tasks (much better):
Prompt 1: "Analyze this business idea for market fit and competitive advantage."
Prompt 2: "Based on that analysis, create a business plan outline."
Prompt 3: "Now develop the Financial Projections section."
Prompt 4: "Develop a marketing strategy based on the plan."
```

---

### Component 4: Format

**What it is:** Instructions specifying how you want the output structured, organized, and presented.

**Why it matters:** Without format instructions, the AI defaults to prose paragraphs — which may not be useful for your actual purpose.

**Complete Format Vocabulary:**

```
TEXT STRUCTURE:
• Bullet points (unordered list)
• Numbered list (ordered/sequential)
• Paragraph form (specify: 2 paragraphs / short paragraphs / long-form)
• Headers and subheadings (specify: H2 / H3 levels)
• Outline format (I. A. 1. style)

DATA PRESENTATION:
• Table (specify: columns and rows)
• Comparison matrix
• Timeline format
• Pros and cons table
• Decision matrix

DOCUMENT FORMATS:
• Email (subject line + greeting + body + closing)
• Report (executive summary + sections + conclusion)
• Slide outline (slide number + title + 3 bullets + speaker note)
• Script (speaker + dialogue format)
• FAQ (Q: ... A: ...)

TECHNICAL FORMATS:
• JSON structure
• XML
• CSV (comma-separated values)
• Markdown
• Code (specify language: Python, SQL, JavaScript, etc.)

LENGTH SPECIFICATIONS:
• Word count: "in exactly 250 words"
• Sentence count: "in 3 sentences"
• Paragraph count: "in 2 short paragraphs"
• Section count: "covering 5 main points"
• Time-based: "for a 2-minute read"
```

**Powerful format example:**

```
Task: "Compare three cloud providers for a small business."

Without format:
→ 3 paragraphs of text about each, mixed together, hard to compare

With format:
"Present as a comparison table with these columns:
Provider | Cost (monthly for 100GB) | Key Strength | Key Weakness |
Best For | Ease of Use (1-5)"
→ Immediately scannable, directly useful
```

**JSON format for technical use:**

```
Prompt: "Extract the following information from this job posting and
return it as JSON:
- job_title (string)
- company_name (string)
- required_experience_years (integer)
- required_skills (array of strings)
- salary_range (string, null if not mentioned)
- location (string)
- remote_status (enum: 'on-site', 'hybrid', 'remote', 'unspecified')

Job posting: [paste job posting here]"

Expected output:
{
  "job_title": "Senior Data Analyst",
  "company_name": "FinTech Solutions Pvt Ltd",
  "required_experience_years": 5,
  "required_skills": ["Python", "SQL", "Tableau", "Power BI"],
  "salary_range": "₹18-25 LPA",
  "location": "Bengaluru",
  "remote_status": "hybrid"
}
```

---

### Component 5: Constraints

**What it is:** Boundaries, rules, limitations, inclusions, and exclusions that govern the response.

**Why it matters:** Constraints paradoxically improve quality by narrowing the AI's creative space to the most useful range.

**Types of constraints:**

**Length constraints:**
```
"Under 100 words"
"Exactly 5 bullet points"
"No more than 3 paragraphs"
"Between 400 and 500 words"
```

**Scope constraints:**
```
"Focus only on the financial implications, not operational"
"Only consider options available in India"
"Limit advice to what can be done with a team of 3"
```

**Exclusion constraints (negative instructions):**
```
"Do not use technical jargon"
"Avoid mentioning competitor brands by name"
"Do not include implementation steps — only strategy"
"Do not use clichés like 'think outside the box'"
```

**Inclusion requirements:**
```
"Must include at least one real-world example"
"Include a specific statistic for each point"
"Each point must have an action step"
```

**Audience constraints:**
```
"Write for someone with no finance background"
"Assume the reader is a CEO with limited time"
"The audience is skeptical — address objections proactively"
```

**Style constraints:**
```
"Use active voice throughout"
"Write in second person ('you' language)"
"Match the tone of this example: [sample]"
"No emojis"
```

---

## 3.3 Putting All Five Components Together

### Anatomy Dissection — Before and After

**Weak prompt:**
```
"Help me with a presentation about sustainability."
```

**Analysis of what's missing:**
- ❌ Role: Who is giving this advice? Generic output.
- ❌ Context: What kind of presentation? For whom? How long?
- ✅ Task: Present (create a presentation) — but vague
- ❌ Format: No structure specified
- ❌ Constraints: No length, no depth, no topic boundaries

**Expected output:** A vague, generic presentation outline about sustainability that could fit anyone, anywhere, for any purpose.

---

**Strong prompt:**
```
You are an experienced sustainability consultant who has worked with Fortune 500
companies on ESG reporting.

Context: I am the Head of Corporate Affairs at a 3,000-employee manufacturing
company in Pune. I need to present our 2024 sustainability initiatives to the
Board of Directors (10 people, non-technical, focused on business outcomes).

Task: Create a complete 10-slide presentation outline for a 20-minute board
presentation on our sustainability progress and 2025 roadmap.

Format: For each slide provide:
Slide # | Slide Title | 3 key content points | Suggested visual | Speaker note (2 sentences)

Constraints:
- Frame everything in terms of business value and risk reduction, not environmental idealism
- Include specific metrics where possible (use placeholders like [X%] if actual data needed)
- Slide 1 must be an executive summary with the single most important takeaway
- Last slide must be a clear call-to-action for the board
- No slide should be text-heavy — aim for visual-first design
```

**Expected output:** A board-ready, professionally structured 10-slide outline tailored to a manufacturing company's ESG context, framed for business-focused non-technical executives.

---

## 3.4 Types of Prompts

Different tasks call for different prompt types. Recognizing the type helps you structure the task component correctly.

| Prompt Type | Definition | Task Verb Examples | Best For |
|-------------|-----------|-------------------|---------|
| **Instructional** | Direct command to produce output | Write, Draft, Create, Generate | Documents, emails, content |
| **Analytical** | Request evaluation or breakdown | Analyze, Evaluate, Assess, Critique | Data, decisions, plans |
| **Question-based** | Seek information or explanation | Explain, Describe, What is, How does | Learning, research |
| **Transformational** | Convert existing content | Rewrite, Translate, Summarize, Improve | Editing, localization |
| **Generative-Creative** | Open-ended creation | Invent, Imagine, Design, Brainstorm | Ideas, fiction, concepts |
| **Conversational** | Ongoing dialogue | Let's discuss, I think... do you agree? | Exploration, debate |
| **Comparative** | Contrast multiple options | Compare, Contrast, Which is better | Decisions, trade-offs |
| **Procedural** | Step-by-step guidance | How do I, Walk me through, Steps to | Tutorials, processes |

---

## 3.5 Diagnosing Prompt Failures

When an AI response isn't what you wanted, use this diagnostic:

```
PROMPT FAILURE DIAGNOSTIC CHECKLIST

Response problem: "Too generic / could apply to anyone"
→ Missing: CONTEXT — add your specific situation

Response problem: "Wrong format (got paragraphs, wanted bullets)"
→ Missing: FORMAT — specify exact structure required

Response problem: "Doesn't sound expert enough / too basic"
→ Missing: ROLE — assign expert persona with credentials

Response problem: "Covered too much, not focused on what I needed"
→ Missing: CONSTRAINTS — add scope limitations and exclusions

Response problem: "I asked for X but got Y"
→ Weak: TASK — use more specific action verb and explicit task description

Response problem: "Too long / too short"
→ Missing: LENGTH CONSTRAINT — specify word count or bullet count

Response problem: "Doesn't account for my specific situation"
→ Missing: CONTEXT — add industry, role, organization details

Response problem: "Wrong tone (too formal / too casual)"
→ Add to CONSTRAINTS: tone descriptor + audience specification
```

---

## 3.6 Worked Examples — Full Prompt Anatomy

### Example 1: Business Email

**Scenario:** You need to ask a client for a 2-week extension on a project deadline.

**Anatomy:**
```
ROLE: You are a professional project manager who communicates with clarity and confidence.

CONTEXT: I am the project lead at an IT consulting firm. Our client is a large bank
(conservative, formal culture). We promised delivery of a data migration project by
November 30th. Due to unexpected API changes on the client's own system, we need 2
more weeks (to December 14th). This is our 3rd project together.

TASK: Write a professional email requesting a deadline extension.

FORMAT: Standard business email format — Subject line, greeting, 3 paragraphs (reason,
impact, solution), clear ask, professional closing.

CONSTRAINTS:
- Under 200 words
- Do not make excuses — present it as a quality decision
- Acknowledge the client's business impact briefly
- End with a specific proposed new deadline
- Professional but warm tone — we have an established relationship
```

**Full Prompt:**
```
You are a professional project manager who communicates with clarity and confidence.

I am the project lead at an IT consulting firm. Our client is a large bank with a
conservative, formal culture. We promised delivery of a data migration project by
November 30th. Due to unexpected API changes on the client's own system (not our
fault, but ours to solve), we need 2 more weeks (new deadline: December 14th).
This is our 3rd successful project together — we have a good relationship.

Write a professional email requesting a 2-week deadline extension.

Format: Business email — Subject line, greeting, 3 short paragraphs (situation,
impact of rushing, proposed solution), clear ask, professional closing.

Constraints: Under 200 words. Do not frame it as an excuse — present it as ensuring
quality. Acknowledge their time briefly. End with the specific new proposed date.
Tone: Professional but warm, reflecting an established working relationship.
```

---

### Example 2: Data Extraction in JSON

**Scenario:** You want to extract structured data from unstructured product descriptions.

```
You are a data extraction specialist who outputs clean, structured JSON.

Context: I am building a product database from raw web-scraped descriptions.
Each description is unstructured text containing product information.

Task: Extract product attributes from the description below and return
as a JSON object.

Format: JSON with these exact fields:
{
  "product_name": string,
  "brand": string,
  "price_inr": number or null,
  "category": string,
  "key_features": array of strings (max 5),
  "materials": array of strings,
  "target_audience": string,
  "warranty_months": number or null
}

Constraints:
- If a field is not mentioned, use null (never guess or infer)
- key_features must be actual product benefits, not marketing fluff
- All strings in English regardless of source language
- Return ONLY the JSON — no explanation, no markdown, no commentary

Product description to extract from:
"Introducing the UrbanGo Pro X Running Shoes by NovaTrek — priced at just
₹4,999! These lightweight trainers feature air-mesh upper construction and
dual-density EVA foam midsoles for maximum comfort. Perfect for daily runners
and fitness enthusiasts. Built with recycled polyester and natural rubber.
Our 6-month manufacturer warranty gives you peace of mind."
```

**Expected output:**
```json
{
  "product_name": "UrbanGo Pro X Running Shoes",
  "brand": "NovaTrek",
  "price_inr": 4999,
  "category": "Running Shoes",
  "key_features": [
    "Lightweight design",
    "Air-mesh upper construction",
    "Dual-density EVA foam midsoles",
    "Maximum comfort"
  ],
  "materials": ["Recycled polyester", "Natural rubber", "EVA foam"],
  "target_audience": "Daily runners and fitness enthusiasts",
  "warranty_months": 6
}
```

---

### Example 3: Educational Content

**Scenario:** Explaining a concept to a specific audience.

```
You are a high school chemistry teacher known for making abstract concepts
tangible through everyday examples.

Context: My students are 16-year-olds with no prior chemistry background.
We just finished a unit on states of matter. Next lesson introduces chemical
bonding. Many students struggle with abstract atomic concepts.

Task: Explain the concept of ionic bonding to my students.

Format:
1. Start with a relatable everyday analogy (2-3 sentences)
2. The scientific explanation using the analogy as a bridge (1 paragraph)
3. A real-world example of an ionic compound they know (table salt — NaCl)
4. A simple diagram using ASCII art to show electron transfer
5. A "Remember It" memory trick (1 sentence)
6. Two practice questions with answers

Constraints:
- No jargon without explanation
- Avoid equations — this is a conceptual introduction
- Maximum 400 words total
- Use an enthusiastic, encouraging tone
```

---

## Hands-On Activities — Session 3

---

### Activity 3.1 — Anatomy Dissection

For each of the following prompts, identify which of the 5 components are PRESENT and which are MISSING. Then rate the prompt's likely quality (1–5 stars).

**Prompt A:**
```
"Summarize this article."
```

| Component | Present? | Missing? |
|-----------|---------|--------|
| Role | | |
| Context | | |
| Task | | |
| Format | | |
| Constraints | | |
Predicted quality: ★☆☆☆☆ to ★★★★★ (circle one)

---

**Prompt B:**
```
"You are a financial advisor. I am a 28-year-old software engineer earning
₹20 LPA with ₹3 lakh in savings and no investments yet. I want to start
investing for retirement and a home purchase in 7 years. Create a monthly
investment plan for me. Present it as a table with columns: Investment Type,
Monthly Amount, Expected Annual Return, Purpose. Limit to 5 investment types.
Avoid overly technical jargon — I am new to investing."
```

| Component | Present? | Missing? |
|-----------|---------|--------|
| Role | | |
| Context | | |
| Task | | |
| Format | | |
| Constraints | | |
Predicted quality: ★☆☆☆☆ to ★★★★★ (circle one)

---

### Activity 3.2 — Prompt Reconstruction

Take this weak prompt and reconstruct it with all five components:

**Weak prompt:** *"Write about remote work."*

Fill in each component deliberately:
```
ROLE: _______________________________________________
CONTEXT: _______________________________________________
TASK: _______________________________________________
FORMAT: _______________________________________________
CONSTRAINTS: _______________________________________________
```

Write your complete reconstructed prompt:
```
[Your full prompt here]
```

Run both the weak prompt and your reconstructed prompt in ChatGPT. Screenshot both responses and write a 3-sentence reflection on the difference.

---

### Activity 3.3 — Real-World Prompt Build

Choose ONE real task you need to complete this week (at work, study, or life). Build a complete 5-component prompt for it.

**My task:** _______________________________________

```
Complete Prompt:
[Write your full prompt here]
```

Run it, evaluate the response, and identify which component you would strengthen for the next iteration.

---

### Activity 3.4 — Format Exploration

Take this single task and run it 5 times with different format specifications:

**Task:** "Give me information about the benefits of regular exercise."

**Run 1:** No format specified (observe default)
**Run 2:** "Format as 5 bullet points"
**Run 3:** "Format as a table: Benefit | Explanation | Timeframe to see results"
**Run 4:** "Format as a Q&A — 5 questions and answers"
**Run 5:** "Format as a timeline: Week 1, Month 1, Month 3, Month 6, Year 1"

**Reflection:** Which format was most useful for which purpose? What does this tell you about choosing formats based on end use?

---

## Revision Questions — Session 3

1. What are the five components of prompt anatomy? Define each in one sentence.
2. Why does assigning a role to the AI improve the quality of the response?
3. A colleague gives the prompt "Tell me about marketing strategies." Which components are missing and what should they add?
4. What is the difference between an instructional prompt and an analytical prompt?
5. Give an example of a format constraint and explain when you would use it.
6. Give three examples of exclusion constraints (what NOT to do) and explain when each is useful.
7. You run a prompt and get a response that is technically correct but uses advanced jargon your audience won't understand. Which component was missing or insufficient?
8. Why is it better to break a complex task into multiple single-task prompts rather than putting everything in one prompt?

---

## Key Takeaways — Session 3

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 3 KEY TAKEAWAYS                                             │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ 5 components: Role | Context | Task | Format | Constraints       │
│                                                                      │
│  ✓ Role activates domain-appropriate vocabulary and depth           │
│                                                                      │
│  ✓ Context makes generic advice specific to YOUR situation          │
│                                                                      │
│  ✓ Task precision: use strong action verbs — never "help me with"   │
│                                                                      │
│  ✓ Format = the shape of the output — always specify it             │
│                                                                      │
│  ✓ Constraints improve quality by narrowing the AI's scope          │
│    Negative instructions ("do not...") are highly effective         │
│                                                                      │
│  ✓ Prompt failure diagnostic: if response is wrong,                 │
│    identify which component is weak and fix it specifically         │
│                                                                      │
│  ✓ For complex tasks: one prompt per task, not everything at once   │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 3 Complete → Proceed to Session 4: Prompt Best Practices*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
