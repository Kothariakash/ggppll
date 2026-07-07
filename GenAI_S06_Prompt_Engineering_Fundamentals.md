# Session 6: Prompt Engineering Fundamentals & The CRAFT Framework
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 2 — PROMPT ENGINEERING                                               │
│  SESSION 6 of 30  |  1 Hour  |  40% Theory + 60% Hands-On                  │
│                                                                              │
│  "The AI didn't change. The prompt changed. That's the entire lesson."      │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 6, you will be able to:

- Define prompt engineering and articulate its professional value
- Apply all 6 components of the CRAFT framework to any task
- Diagnose why a weak prompt produces poor output
- Transform any vague request into a professional-grade prompt
- Write prompts that produce immediately usable professional outputs
- Score and improve prompts using a structured quality rubric

---

## 1. What is Prompt Engineering?

### 1.1 The Core Definition

> **Prompt Engineering** is the practice of designing, structuring, and refining the instructions you give an AI model to consistently produce accurate, relevant, and high-quality outputs.

The same AI tool given two different prompts for the same task can produce results that are either completely generic and unusable — or polished, specific, and ready to use. The difference is **entirely** in how you communicate with the AI.

Prompt engineering is not about "hacking" AI or finding tricks. It is about applying clear communication principles — the same skills that make a good manager, writer, or consultant — to instruct an AI system.

---

### 1.2 The Proof: Same AI, Completely Different Results

This single comparison demonstrates the entire value of this module:

**Weak Prompt:**
```
Write about marketing.
```

**Output:** A 200-word generic definition of marketing. No specificity. Not usable.

---

**Professional Prompt (CRAFT Framework Applied):**
```
You are a Senior Marketing Strategist with 15 years of B2B SaaS experience.

Write a 300-word thought leadership article introduction for LinkedIn
targeting CMOs of mid-sized technology companies (500–2,000 employees).

Topic: "Why traditional lead generation is failing in 2024 and what
high-performing marketing teams are doing instead."

Structure:
- Hook: A surprising statistic or bold claim in the first sentence
- Problem: 2 sentences establishing the pain point CMOs feel
- Bridge: 1 sentence hinting at the solution direction
- Question: End with an open question that invites comments

Tone: Authoritative but conversational. No corporate jargon.
Do not start with "In today's world" or "In this article."
```

**Output:** A polished, publish-ready LinkedIn introduction that would take a skilled writer 45 minutes to produce independently. Ready with minor edits.

**The AI did not change. The prompt changed.**

---

### 1.3 Why Prompt Engineering is a Valuable Professional Skill

| Without Prompt Engineering | With Prompt Engineering |
|---------------------------|------------------------|
| Generic outputs needing complete rewrites | Specific outputs needing minor edits |
| 3–5 revision cycles per task | 1–2 revision cycles |
| AI as an unreliable assistant | AI as a consistent co-worker |
| 30–40% time saving | 70–85% time saving |
| "AI doesn't really work for my tasks" | "AI handles my first drafts entirely" |

**The Economic Value:**

```
If a professional earns ₹15,00,000/year and works 250 days:
  Daily value of time = ₹6,000/day

With effective prompting, saving 2 hours/day:
  Annual value saved = 2 hrs × 250 days × ₹750/hr = ₹3,75,000/year

At the organizational level (100-person team):
  Annual value = ₹3.75 Crore in reclaimed productive time
```

---

## 2. The CRAFT Framework — 6 Components of Every Great Prompt

CRAFT is the master framework for professional prompt engineering. Every element improves output quality. Together, they transform AI from a vague assistant into a precise professional tool.

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                        THE CRAFT FRAMEWORK                                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  C — CONTEXT      Background information the AI needs to understand          │
│                   your specific situation and requirements                   │
│                                                                              │
│  R — ROLE         The expert identity or persona you want the AI to adopt   │
│                   to frame its knowledge and perspective                     │
│                                                                              │
│  A — ACTION       The specific, concrete task you want completed:            │
│                   Write / Analyze / Summarize / Compare / Create...          │
│                                                                              │
│  F — FORMAT       How the output should be structured:                       │
│                   Bullet points / Table / Email / Report / Code block...     │
│                                                                              │
│  T — TONE         The voice and style of the output:                         │
│                   Formal / Friendly / Technical / Persuasive / Empathetic... │
│                                                                              │
│  [+] CONSTRAINTS  Limits and boundaries:                                     │
│                   Under 200 words / No jargon / Must include X / Avoid Y    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

### 2.1 C — Context: Background That Changes Everything

Context is the information the AI needs about **your specific situation** that it cannot guess from the action alone.

**Without Context:**
```
Write a meeting agenda.
```
AI guesses: What meeting? Who attends? What decisions need to be made?
Output: A generic meeting agenda template. Unusable.

**With Rich Context:**
```
Context: I am a Product Manager at a fintech startup.
We are having a 45-minute sprint planning meeting with 6 engineers
and 2 designers. We need to prioritize 12 features for our Q1 release.
Our main constraint is 3 engineers are unavailable for 2 weeks in January.
```
Output: A specific, structured sprint planning agenda with time allocations, prioritization frameworks, and a slot to discuss the January capacity constraint.

**Context includes:**
- Who you are (your role, level, industry)
- Who the audience is (their background, expertise, concerns)
- What situation prompted this task
- What constraints or constraints exist
- What has already been tried or decided
- What the output will be used for

---

### 2.2 R — Role: Unlocking Expert-Level Knowledge

Assigning a role shifts the AI's "perspective" and activates domain-specific knowledge, vocabulary, and reasoning patterns relevant to that expert.

**The Difference Role Makes:**

| Same Task | Without Role | With Role |
|-----------|-------------|-----------|
| Explain compound interest | Generic textbook definition | Financial advisor explaining to a first-time investor |
| Review this contract clause | Surface-level comments | Senior corporate lawyer flagging legal risks |
| Improve this presentation | Generic design tips | McKinsey consultant restructuring for executive clarity |
| Analyze this marketing data | Basic observations | CMO identifying strategic implications for board reporting |

**Role Formulas That Work:**

```
Formula 1: Expert + Experience
"You are a [job title] with [X years] of experience in [specific domain]."

Example: "You are a Chief Financial Officer with 20 years of experience
in manufacturing companies with annual revenue of $50M–$500M."

Formula 2: Expert + Audience Awareness
"You are a [expert] speaking to [specific audience]."

Example: "You are a cybersecurity expert explaining risks to
a non-technical board of directors."

Formula 3: Expert + Style Model
"You are a [expert] who writes in the style of [reference]."

Example: "You are a business writer who writes in the concise,
evidence-based style of Harvard Business Review articles."
```

---

### 2.3 A — Action: The Precise Task Instruction

The Action is the most important element — it tells AI exactly what to do. Vague actions produce vague results.

**Action Verb Precision:**

| Vague Action | What AI Does | Precise Action | What AI Does |
|-------------|-------------|---------------|-------------|
| "Write about X" | Generates an overview | "Write a 500-word persuasive argument for X" | Writes specifically persuasive content |
| "Help with email" | Offers generic tips | "Draft a follow-up email that re-engages a client who went silent after receiving our proposal" | Writes that specific email |
| "Analyze this" | Surface-level comments | "Identify the 3 biggest risks and quantify their potential financial impact" | Focused risk analysis |
| "Improve this" | Minor edits | "Rewrite this to be 40% shorter while preserving all key arguments" | Targeted compression |

**Action + Specificity Ladder:**

```
Level 1 (Weak):     "Write an email"
Level 2:            "Write a professional email"
Level 3:            "Write a professional email requesting a meeting"
Level 4:            "Write a professional email requesting a 30-minute
                    meeting with the Head of Operations"
Level 5 (Strong):   "Write a professional email requesting a 30-minute
                    meeting with the Head of Operations to discuss
                    Q3 supply chain bottlenecks. I am the Logistics
                    Manager. Propose 3 specific time slots next week.
                    Subject line included. Under 120 words."
```

---

### 2.4 F — Format: Structuring the Output

Format tells the AI exactly how to present the output. AI will match whatever format you specify — tables, bullet points, numbered lists, code blocks, email format, report structure, JSON, Markdown.

**Format Options and When to Use Each:**

| Format | Best For | Example Instruction |
|--------|---------|---------------------|
| **Bullet points** | Scannable lists, options, tips | "Present as bullet points, max 10 words each" |
| **Numbered list** | Sequential steps, ranked items | "Number each step in order of priority" |
| **Table** | Comparisons, data, side-by-side options | "Present in a table with columns: Option, Pros, Cons, Cost" |
| **Email format** | Professional communications | "Format as a business email with subject line, greeting, body, sign-off" |
| **Report structure** | Formal documents | "Use headings: Executive Summary, Analysis, Recommendations, Next Steps" |
| **Code block** | Programming, scripts, formulas | "Present the code in a Python code block with comments" |
| **Slide outline** | Presentations | "Format as slide-by-slide: Slide title, 3 bullet points per slide" |
| **FAQ format** | Knowledge base, support content | "Format as Q&A pairs: bold the question, plain text the answer" |

**Format + Length Instruction Example:**
```
Format your response as:
1. Executive Summary (2 sentences max)
2. Key Findings (bullet points, max 5 items)
3. Recommendations (numbered list, 3 items)
4. Risk Considerations (1 short paragraph)
Total response: under 350 words.
```

---

### 2.5 T — Tone: The Voice of the Output

Tone determines how the output sounds — its emotional register, formality level, and personality. Mismatched tone is one of the most common reasons AI outputs feel "off."

**The Tone Spectrum:**

```
FORMAL ◄────────────────────────────────────► INFORMAL
  Legal brief  |  Business report  |  Email  |  Slack message  |  Tweet

AUTHORITATIVE ◄─────────────────────────────► EMPATHETIC
  Policy document  |  Analysis  |  Customer complaint response

TECHNICAL ◄─────────────────────────────────► PLAIN LANGUAGE
  Developer docs  |  Internal memo  |  C-suite summary  |  Public explainer
```

**Tone Descriptors with Examples:**

| Tone | When to Use | Example Instruction |
|------|------------|---------------------|
| **Professional and formal** | Board reports, legal docs, official correspondence | "Write in a professional, formal tone suitable for executive review" |
| **Warm and empathetic** | Customer apologies, HR communications, support responses | "Write with warmth and genuine empathy. Acknowledge the customer's frustration first." |
| **Confident and persuasive** | Proposals, pitches, sales content | "Write confidently. Use active voice. Make a clear, compelling case." |
| **Clear and simple** | Public communications, non-expert audiences | "Write in plain English. No jargon. Use short sentences. Explain any technical terms." |
| **Conversational and engaging** | Social media, blog posts, newsletters | "Write conversationally, as if talking to a smart friend. Friendly but professional." |
| **Urgent and direct** | Escalation emails, risk alerts, crisis comms | "Be direct and urgent. Get to the critical point in the first sentence." |

---

### 2.6 Constraints: Setting the Boundaries

Constraints prevent AI from drifting into generic territory, going on too long, or including things you specifically don't want.

**Types of Constraints:**

```
LENGTH CONSTRAINTS:
  "Under 150 words"
  "Exactly 5 bullet points"
  "Maximum 3 paragraphs"
  "One sentence per point"

INCLUSION CONSTRAINTS:
  "Must mention our 15-year track record"
  "Include at least one specific statistic"
  "Reference the CRAFT framework"

EXCLUSION CONSTRAINTS:
  "Do not use the word 'leverage'"
  "No bullet points — use flowing paragraphs"
  "Do not include pricing information"
  "Avoid clichés like 'in today's fast-paced world'"

AUDIENCE CONSTRAINTS:
  "Assume the reader has no technical background"
  "Written for a senior executive with 5 seconds to read it"
  "For a non-English-speaking audience — use simple vocabulary"

STRUCTURAL CONSTRAINTS:
  "Start with a question"
  "End with a specific call to action"
  "Each paragraph must have a topic sentence"
```

---

## 3. Building a CRAFT Prompt — Step by Step

### 3.1 The Prompt Assembly Process

Here is a real business scenario built into a CRAFT prompt, component by component:

**Scenario:** You are a Marketing Manager. Your company is launching a new project management app targeting small business owners. You need to write an email to your email subscriber list announcing the launch.

```
STEP 1 — Start with ACTION (what do you need?):
  Write a launch announcement email

STEP 2 — Add ROLE (who should write it?):
  You are an expert email copywriter specializing in SaaS product launches.

STEP 3 — Add CONTEXT (what do they need to know?):
  Product: "FlowDesk" — a project management app for small businesses (1–20 employees)
  Audience: Existing email subscribers who signed up for early access
  USP: 50% cheaper than competitors, 5-minute setup, mobile-first
  Launch date: Monday, January 20th
  Offer: First 100 sign-ups get 3 months free

STEP 4 — Add FORMAT (how should it look?):
  Format: Professional email with:
  - Subject line (A/B test: give 2 options)
  - Preview text
  - Email body: greeting, value statement, 3 key benefits (bullets), CTA button text
  - PS line

STEP 5 — Add TONE (how should it sound?):
  Tone: Excited but professional. Conversational. Not salesy or pushy.

STEP 6 — Add CONSTRAINTS (what to avoid/include?):
  - Under 250 words total
  - CTA button text: under 5 words
  - Do not use "revolutionary" or "game-changing"
  - Must mention the January 20th launch date
```

**Final Assembled CRAFT Prompt:**

```
You are an expert email copywriter specializing in SaaS product launches.

Write a launch announcement email for "FlowDesk" — a project management
app for small businesses (1–20 employees) with these unique advantages:
  - 50% cheaper than Monday.com or Asana
  - 5-minute setup (no training required)
  - Mobile-first design for teams that work on the go

The email goes to subscribers who signed up for early access. They have
been waiting for this moment — treat them as VIPs who get first access.

Launch date: Monday, January 20th
Offer: First 100 customers get 3 months completely free

Format:
  - 2 subject line options (A/B test)
  - Preview text (max 90 characters)
  - Body: warm greeting + value statement + 3 benefits as bullets + CTA
  - PS line with urgency

Tone: Genuinely excited but professional. Conversational, not salesy.
Do not use the words "revolutionary" or "game-changing."
Total under 250 words. CTA button text: maximum 5 words.
```

---

## 4. Prompt Quality Scoring — The CRAFT Rubric

Use this rubric to evaluate any prompt before sending it:

| Component | 0 — Missing | 1 — Partial | 2 — Strong |
|-----------|------------|------------|-----------|
| **Context** | No background given | Some context but vague | Rich, specific context |
| **Role** | No role assigned | Generic role ("expert") | Specific expert with domain |
| **Action** | Vague ("write about") | General action | Precise action + specifics |
| **Format** | No format specified | Format mentioned | Full format with structure |
| **Tone** | No tone specified | One-word tone | Specific tone + examples |
| **Constraints** | No constraints | One constraint | Multiple clear constraints |

**Score interpretation:**
- 0–4: Weak prompt — rewrite before sending
- 5–8: Moderate prompt — add missing elements
- 9–12: Strong prompt — ready to use

**Practice:** Score the following prompt:
```
Write a summary of the meeting for the team.
```
*Score: 0 (Context) + 0 (Role) + 1 (Action) + 0 (Format) + 0 (Tone) + 0 (Constraints) = 1/12 — Rewrite.*

---

## 5. Common Prompt Mistakes — And How to Fix Them

### Mistake 1: The Vague Request

```
WEAK:   "Write something about our new product."
FIXED:  "Write a 200-word product description for [Product Name] targeting
         [audience]. Highlight [top 3 benefits]. Tone: [specify]."
```

### Mistake 2: The Missing Audience

```
WEAK:   "Explain machine learning."
FIXED:  "Explain machine learning to a CFO with no technical background.
         Use a financial analogy. Under 100 words."
```

### Mistake 3: The Wrong Tone Assumption

```
WEAK:   "Write a response to this angry customer email."
FIXED:  "You are a senior customer service manager. Write a response to
         this angry customer email. Lead with genuine empathy.
         Acknowledge the specific issue. Offer a concrete solution.
         Do not be defensive. Professional but warm."
```

### Mistake 4: Overloading a Single Prompt

```
WEAK:   "Write a full marketing strategy, social media posts for a month,
         email campaign, blog posts, and a press release for our launch."
FIXED:  Break into separate prompts per deliverable. Start with:
         "Write the overall marketing strategy first."
         Then follow with specific deliverables in sequence.
```

### Mistake 5: No Constraints → Runaway Output

```
WEAK:   "Write a business plan."
         → AI writes 3,000 words of generic content.

FIXED:  "Write a 1-page business plan outline with these sections:
         [list]. Maximum 500 words. Use bullet points under each section."
```

---

## 6. Real-World Example: CRAFT in Action at a Consulting Firm

**Scenario:** Ananya, a junior consultant at a management consulting firm, needs to prepare a one-page situation analysis for a client meeting in 90 minutes.

**Without CRAFT — her old approach:**
- Types: "Analyze the Indian retail sector"
- Gets a 5-paragraph Wikipedia-style overview
- Spends 45 minutes rewriting it to match the client's context
- Still not quite right — wrong focus, wrong tone

**With CRAFT — her new approach:**

```
You are a McKinsey Associate with deep expertise in Indian retail and
consumer goods.

Write a one-page situation analysis of the Indian organized retail sector
for a board presentation to the leadership of a mid-size fashion retail
chain (₹500 Crore revenue, 120 stores, primarily tier-2 cities).

Focus on:
1. Current market dynamics (3 key trends affecting fashion retail specifically)
2. Competitive pressures (both offline and D2C online)
3. Consumer behavior shifts post-COVID
4. 2 strategic implications relevant to a tier-2 city retail chain

Format: Executive-style prose with 4 clearly labeled sections.
Tone: Authoritative, concise, C-suite appropriate. No jargon.
Length: 400 words maximum. This is a one-pager, not a full report.
Do not include generic market size statistics. Focus on strategic insights.
```

**Result:** A focused, context-specific analysis in the right format and tone. Ananya reviews and refines it in 15 minutes rather than 45.

---

## 7. Hands-On Lab 6: Building CRAFT Prompts

**Objective:** Transform weak prompts into professional CRAFT prompts and compare outputs  
**Duration:** 25 minutes  
**Tool:** ChatGPT or any LLM

---

### Exercise A: Diagnose and Upgrade (10 minutes)

For each weak prompt below, identify what CRAFT elements are missing, then rewrite it as a full CRAFT prompt. Test both in ChatGPT and compare the outputs.

**Weak Prompt 1:**
```
Write a job posting.
```
Missing elements: _______________________________
Your CRAFT prompt: _______________________________

**Weak Prompt 2:**
```
Give me some ideas for a presentation.
```
Missing elements: _______________________________
Your CRAFT prompt: _______________________________

**Weak Prompt 3:**
```
Respond to this customer complaint: "Your product broke after one week."
```
Missing elements: _______________________________
Your CRAFT prompt: _______________________________

---

### Exercise B: CRAFT Prompt from Scratch (10 minutes)

Choose ONE of these scenarios and write a complete CRAFT prompt. Then run it in ChatGPT and evaluate the output using the scoring rubric.

**Scenario Options:**
1. You are a Financial Analyst preparing a quarterly performance email for your manager
2. You are an HR Manager writing a policy update about the company's new remote work guidelines
3. You are a Sales Executive drafting a follow-up proposal to a client who expressed interest but went quiet
4. You are a startup founder writing your first fundraising pitch paragraph for an investor email

**Your CRAFT Prompt:**

```
Role:        ___________________________________________
Context:     ___________________________________________
Action:      ___________________________________________
Format:      ___________________________________________
Tone:        ___________________________________________
Constraints: ___________________________________________
```

**Output Quality Self-Assessment:**

| Criterion | Score /5 | Notes |
|-----------|---------|-------|
| Would I use this output professionally? | | |
| Did the role make a noticeable difference? | | |
| Was the format followed exactly? | | |
| Did the tone match what you specified? | | |

---

### Exercise C: Constraints Experiment (5 minutes)

Take any prompt you wrote in Exercise B. Run it 3 times with different constraint sets:

- **Version 1:** No constraints (baseline)
- **Version 2:** Add: "Under 100 words. No bullet points. One flowing paragraph."
- **Version 3:** Add: "Under 100 words. Use exactly 3 bullet points. End with a question."

**Observe:** How dramatically does changing constraints change the output?

---

### Lab Evaluation Rubric

| Task | Marks |
|------|-------|
| Exercise A: 3 weak prompts diagnosed and upgraded correctly | 4 |
| Exercise B: CRAFT prompt complete + output screenshot | 4 |
| Exercise C: 3 constraint versions compared with observation note | 2 |
| **Total** | **10** |

---

## 8. Interview Questions — Session 6

**Q1:** *"What is prompt engineering and why does it matter professionally?"*

**Strong Answer:**
"Prompt engineering is the practice of structuring AI instructions to consistently produce high-quality, specific, and immediately usable outputs. It matters professionally because the same AI tool can produce completely different quality outputs depending on how it is instructed — from generic, unusable text to polished, professional content. A professional who can prompt effectively can reduce their time on routine writing tasks by 70–80%, produce better first drafts, and get consistent results at scale. I use the CRAFT framework — Context, Role, Action, Format, Tone, and Constraints — as my standard approach."

**Q2:** *"Walk me through how you would write a prompt for a complex professional task."*

**Strong Answer:**
"I use the CRAFT framework. First, I identify the Role — what expert perspective will produce the best output. Then I add Context — the specific background the AI needs about my situation, audience, and constraints. I define the Action precisely — not 'write about X' but 'write a 300-word persuasive introduction for X audience.' I specify Format — table, bullets, email structure, report sections. I set the Tone — formal, empathetic, conversational. Finally, I add Constraints — word limits, what to include, what to avoid. I test the output, then refine the prompt based on what fell short."

---

## 9. Revision Questions — Session 6

1. What does CRAFT stand for? Explain what each component does and why it improves output quality.
2. Take this prompt: "Summarize this article." Score it on the CRAFT rubric and rewrite it with all 6 elements.
3. What is the difference between Format and Constraints in the CRAFT framework?
4. Why does assigning a Role to the AI produce better outputs than not assigning one?
5. Give an example of a situation where the wrong Tone would make an AI output professionally unusable even if the content was accurate.
6. What is the "Action Specificity Ladder"? Give 5 levels for the task "write an email."
7. Why should you avoid overloading a single prompt with too many tasks?
8. Score this prompt on the CRAFT rubric (0–12): "You are a marketing expert. Write 5 Instagram captions for a luxury watch brand targeting men aged 30–50. Each caption: 2 sentences + 3 relevant hashtags. Tone: sophisticated and aspirational. No emojis."

---

## 10. Key Terminology — Session 6

| Term | Definition |
|------|-----------|
| **Prompt Engineering** | The practice of designing AI instructions to produce consistent, high-quality outputs |
| **CRAFT Framework** | Context, Role, Action, Format, Tone, Constraints — the 6 components of a professional prompt |
| **Context** | Background information the AI needs to understand your specific situation |
| **Role** | The expert identity assigned to the AI to activate domain-specific knowledge |
| **Action** | The specific, precise task instruction given to the AI |
| **Format** | The structural presentation style of the output (bullets, table, email, report, etc.) |
| **Tone** | The voice, style, and emotional register of the output |
| **Constraints** | Specific limits, inclusions, or exclusions that bound the output |
| **System Prompt** | Instructions given to AI before the user conversation begins (used in API/enterprise deployments) |
| **Prompt Iteration** | The process of testing, evaluating, and refining a prompt to improve output quality |

---

## 11. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 6 SUMMARY — WHAT TO REMEMBER                                        │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  Prompt engineering = professional communication skill applied to AI     │
│  ✓  CRAFT: Context | Role | Action | Format | Tone | Constraints            │
│  ✓  The AI doesn't change — the prompt changes. Weak in = weak out.        │
│  ✓  Role shifts AI perspective → unlocks expert-level knowledge             │
│  ✓  Action must be specific: not "write about" but "write a 300-word X     │
│     for Y audience doing Z task"                                             │
│  ✓  Constraints prevent runaway generic output                              │
│  ✓  Score your prompts before sending: 0–4 rewrite, 9–12 ready to use      │
│  ✓  The most common mistake: missing context and missing constraints        │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 7 — Zero-Shot, One-Shot & Few-Shot Prompting                       │
│  (How to give AI examples to dramatically improve output quality            │
│   for classification, formatting, and domain-specific tasks)                │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 6 Complete | Next: Session 7 — Zero-Shot, One-Shot & Few-Shot Prompting*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
