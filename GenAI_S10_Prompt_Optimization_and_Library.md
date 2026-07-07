# Session 10: Prompt Optimization & Building Your Professional Prompt Library
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 2 — PROMPT ENGINEERING                                               │
│  SESSION 10 of 30  |  1 Hour  |  30% Theory + 70% Hands-On                 │
│                                                                              │
│  "A prompt used once is a one-time gain. A prompt saved, refined,           │
│   and shared is a compounding organizational asset."                         │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 10, you will be able to:

- Apply a structured optimization cycle to improve any underperforming prompt
- Use output anchoring, negative instructions, and decomposition to fix common failures
- Score prompts objectively using a quality rubric
- Design a personal prompt library with proper metadata and versioning
- Structure a team prompt library for collaborative use
- Complete the Module 2 capstone: a 10-prompt personal library

---

## 1. The Prompt Optimization Cycle

### 1.1 Why Prompts Need Iteration

First-draft prompts rarely produce optimal outputs — just like first-draft documents. The professional value comes from a disciplined optimization cycle: test, evaluate, diagnose, refine, repeat.

```
THE PROMPT OPTIMIZATION CYCLE
─────────────────────────────────────────────────────
      ┌─────────────────────────────────────────┐
      │                                         │
      ▼                                         │
   DESIGN                                       │
   (Write the prompt using CRAFT)               │
      │                                         │
      ▼                                         │
   TEST                                         │
   (Run 2–3 times to see typical output range)  │
      │                                         │
      ▼                                         │
   EVALUATE                                     │
   (Score against output quality criteria)      │
      │                                         │
      ├── PASS (score ≥ 8/10) ──► SAVE TO LIBRARY
      │                                         │
      ▼                                         │
   DIAGNOSE                                     │
   (Identify what specifically failed)          │
      │                                         │
      ▼                                         │
   REFINE                                       │
   (Apply targeted fix to the failing element)  │
      │                                         │
      └─────────────────────────────────────────┘
```

**Critical rule:** Change **one element at a time** when refining. If you change multiple elements simultaneously, you cannot isolate what improved the output.

---

### 1.2 The Diagnosis Framework — What Went Wrong?

Before you can fix a prompt, you must identify the correct failure mode:

| Symptom | Root Cause | Fix |
|---------|-----------|-----|
| Output is too generic | No Role or weak Context | Add specific engineered persona + rich context |
| Output is too long | No length constraint | Add "under X words" or "maximum 3 paragraphs" |
| Output is too short | No depth instruction | Add "comprehensive" / "include reasoning" / "minimum 3 examples" |
| Wrong format | No Format specified | Add explicit format instruction (bullets, table, email, etc.) |
| Wrong tone | No Tone specified | Add specific tone descriptor + example phrase |
| Missing key information | No inclusion constraints | Add "Must include [specific element]" |
| Includes unwanted content | No exclusion constraints | Add "Do not include [X]" or "Avoid [Y]" |
| Inconsistent across runs | Too open-ended | Add temperature-reducing constraints; be more specific |
| Good structure but wrong depth | Role too junior | Upgrade to more senior or specialized persona |
| Misses the point | Ambiguous Action verb | Replace with precise, specific action instruction |

---

## 2. Advanced Optimization Techniques

### 2.1 Output Anchoring — Show the Structure You Expect

Instead of just describing format, show the exact output structure you want using a template or skeleton.

**Without Output Anchoring:**
```
Write a competitive analysis of our top 3 competitors.
Format: Table with pros and cons.
```
→ AI creates its own table structure, which may not match what you need.

**With Output Anchoring:**
```
Write a competitive analysis of our top 3 competitors.
Use exactly this structure:

| Competitor | Core Strength | Core Weakness | Our Advantage | Our Risk |
|------------|--------------|---------------|---------------|----------|
| [Name 1]   |              |               |               |          |
| [Name 2]   |              |               |               |          |
| [Name 3]   |              |               |               |          |

After the table, write 2–3 sentences of strategic implication.
```
→ AI fills in your exact structure. No reformatting needed.

**Output Anchoring Examples:**

```
EXAMPLE 1 — Email anchoring:
Subject: [Subject line here]

Dear [Name],

[Opening paragraph — 1–2 sentences, warm but professional]

[Body — main message in 2–3 sentences]

[Action step — what you want them to do]

[Closing — 1 sentence]

Best regards,
[Your name]

---

EXAMPLE 2 — Report section anchoring:
## [Section Title]
**Key Finding:** [1 sentence — the single most important insight]
**Supporting Evidence:** [2–3 bullet points with data/examples]
**Business Implication:** [1–2 sentences — what this means for decisions]
**Recommended Action:** [1 specific action with timeline]

---

EXAMPLE 3 — JSON output anchoring (for technical/automation use):
Return the analysis in this exact JSON format:
{
  "sentiment": "positive|negative|neutral",
  "confidence": 0.0-1.0,
  "key_topics": ["topic1", "topic2"],
  "action_required": true|false,
  "priority": "high|medium|low"
}
```

---

### 2.2 Negative Instructions — Telling AI What NOT to Do

Negative instructions are one of the most underused but highly effective optimization techniques. They prevent AI from defaulting to patterns it learned from its training data.

**Common Negative Instructions and When to Use Them:**

```
CONTENT NEGATIVES:
"Do not include a disclaimer at the end."
"Do not begin with a definition of [topic]."
"Do not mention competitors by name."
"Do not include any information not supported by the data I provided."
"Avoid using statistics — I will add them myself."

STYLE NEGATIVES:
"Do not use passive voice."
"Do not use these clichés: 'in today's fast-paced world', 'leverage',
 'synergy', 'game-changing', 'paradigm shift', 'deep dive'."
"Do not start any sentence with 'It is important to note that'."
"Do not use bullet points — use flowing paragraphs only."
"Do not use exclamation marks in a formal document."

FORMAT NEGATIVES:
"Do not add a title or heading — start directly with the content."
"Do not add a summary section at the end."
"Do not number the paragraphs."

LENGTH NEGATIVES:
"Do not exceed 150 words."
"Do not write more than 3 bullet points per section."
"Do not pad the response — if you have nothing useful to add, stop."
```

**The Negative Instruction Rule:** Every time AI consistently produces something unwanted that you keep removing manually, add a negative instruction. Convert manual editing into prompt intelligence.

---

### 2.3 Progressive Refinement — The Layered Approach

Start simple and add specificity based on what falls short — rather than writing a 500-word prompt on the first attempt.

```
ITERATION 1 (Base prompt):
"Write a project status update email."

→ Too generic. Missing: audience, project context, tone.

ITERATION 2 (Add Role + Context):
"You are a Project Manager. Write a project status update email for
the Bangalore office renovation project that is 2 weeks behind schedule."

→ Better, but tone feels corporate. Format not ideal.

ITERATION 3 (Add Format + Tone):
"You are a Project Manager. Write a project status update email for
the Bangalore office renovation project that is 2 weeks behind schedule.

Format: Subject line + 3 paragraphs (status, cause, mitigation plan)
Tone: Transparent and confident. Not defensive. Under 180 words."

→ Good. But it starts with 'I wanted to update you...' which is weak.

ITERATION 4 (Add negative instruction):
"...Do not begin with 'I wanted to update you' or any similar passive
opener. Start with the project status directly."

→ Final output: sharp, well-structured, usable professional email.
```

**Document each iteration** — this becomes your prompt development history and helps you build better first-draft prompts next time.

---

### 2.4 Self-Instruction Refinement

Ask the AI to help you improve your own prompt before running the actual task:

```
STEP 1 — Submit your prompt to AI for review:
"I am about to use this prompt. Before I run it, review it and tell me:
1. What is unclear or ambiguous in my prompt?
2. What important information am I missing?
3. What would make this prompt produce significantly better output?
Do not run the prompt yet — just critique it."

[Paste your prompt here]

STEP 2 — Revise based on feedback.
STEP 3 — Run the improved prompt.
```

This meta-technique — using AI to improve your AI instructions — is one of the highest-leverage optimization habits.

---

## 3. The Prompt Quality Scoring Rubric

Use this rubric consistently to evaluate and compare prompt versions:

### 3.1 Output Quality Dimensions

| Dimension | 1 — Poor | 3 — Acceptable | 5 — Excellent |
|-----------|---------|---------------|--------------|
| **Relevance** | Misses the point; off-topic | Mostly relevant, some drift | Precisely on-point for the task |
| **Accuracy** | Contains errors or hallucinations | Mostly accurate; 1–2 issues | Factually sound; verifiable |
| **Format** | Wrong structure; needs reformatting | Approximately right format | Exactly the requested format |
| **Tone** | Wrong register for context | Mostly appropriate | Perfectly calibrated |
| **Usability** | Complete rewrite needed | Moderate editing needed | Minor edits; ready to use |
| **Depth** | Superficial; generic | Reasonable depth | Expert-level depth and specificity |

**Scoring:** Sum all 6 dimensions (max 30 points)
- 25–30: Publish-ready prompt — save to library as-is
- 18–24: Good prompt — save with note of what to watch for
- 12–17: Needs refinement — identify 2–3 specific improvements
- Below 12: Significant rewrite needed — diagnose root cause

---

## 4. Building Your Professional Prompt Library

### 4.1 Why a Prompt Library is a Career Asset

```
WITHOUT A LIBRARY:
  Every task → start from scratch
  Inconsistent quality across uses
  Institutional knowledge lives only in your head
  When you leave a role, the prompts leave with you

WITH A LIBRARY:
  Every task → start from a tested, refined template
  Consistent quality regardless of who uses it
  Institutional AI knowledge is documented and shareable
  Onboarding new team members: share the library, not just instructions
```

A well-built prompt library is increasingly a professional portfolio artifact — demonstrating both AI literacy and systematic thinking.

---

### 4.2 Prompt Library Entry Structure

Every prompt in your library should have this metadata:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  PROMPT LIBRARY ENTRY                                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│  ID:            [Unique identifier — e.g., MKT-001, HR-003, FIN-007]       │
│  NAME:          [Clear, descriptive name]                                   │
│  CATEGORY:      [Marketing / HR / Finance / Operations / Communication]     │
│  PURPOSE:       [What task does this prompt accomplish?]                    │
│  BEST MODEL:    [ChatGPT / Claude / Gemini — which works best?]             │
│  VERSION:       [v1.0, v1.1, v2.0 — track improvements]                   │
│  LAST TESTED:   [Date]                                                      │
│  QUALITY SCORE: [X/30 from the rubric]                                     │
│  TAGS:          [email, client, apology, B2B, senior-audience]             │
├─────────────────────────────────────────────────────────────────────────────┤
│  PROMPT TEXT:                                                               │
│  [Full prompt text here — copy-paste ready]                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│  VARIABLES:     [Placeholders to customize — [CLIENT NAME], [INDUSTRY]]    │
│  SAMPLE OUTPUT: [One example of the output this prompt produces]           │
│  NOTES:         [Known limitations, ideal use case, what to watch for]     │
│  AUTHOR:        [Who created/refined this prompt]                           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 4.3 Prompt Library Categories

Organize your library by function for easy navigation:

```
PERSONAL PROMPT LIBRARY STRUCTURE:
├── 01_Communication/
│   ├── Email_Requests/
│   ├── Email_Followup/
│   ├── Email_Difficult_Conversations/
│   ├── Meeting_Agendas/
│   └── Presentation_Decks/
├── 02_Analysis/
│   ├── Market_Research/
│   ├── Competitor_Analysis/
│   ├── Financial_Analysis/
│   └── Risk_Assessment/
├── 03_Content_Creation/
│   ├── LinkedIn_Posts/
│   ├── Blog_Articles/
│   ├── Social_Media/
│   └── Reports_Documents/
├── 04_HR_People/
│   ├── Job_Descriptions/
│   ├── Interview_Questions/
│   ├── Performance_Reviews/
│   └── Policy_Documents/
└── 05_Learning_Research/
    ├── Concept_Explanation/
    ├── Literature_Summary/
    └── Study_Aids/
```

---

### 4.4 Versioning and Improvement Discipline

Track prompt versions like software versions:

```
VERSION HISTORY EXAMPLE:

Prompt: Client Proposal Email Generator
────────────────────────────────────────────────────────────────

v1.0 (Jan 5, 2025) — Initial version. Score: 22/30
  Issue: Tone was too salesy. Missing client-specific context.

v1.1 (Jan 8, 2025) — Added audience context + tone constraint. Score: 26/30
  Change: Added "Tone: consultative, not salesy. We are solving their
  problem, not selling our product."
  Issue: Output still started with "I hope this email finds you well."

v1.2 (Jan 10, 2025) — Added negative instruction. Score: 29/30
  Change: Added "Do not use 'I hope this email finds you well' or similar
  openers. Start with value or context directly."
  Status: APPROVED FOR LIBRARY — stable, high quality.

v2.0 (Planned): Add few-shot examples from best actual client emails.
```

---

## 5. Sample Professional Prompt Library — 10 Production-Ready Prompts

These 10 prompts cover the most common professional tasks. Each is ready to use and can be customized:

---

**PROMPT 1 — Executive Email: Project Status Update**
```
[ID: COM-001 | Category: Communication | Model: Any]

You are a professional Project Manager known for clear, transparent communication.

Write a project status update email with these details:
Project: [PROJECT NAME]
Current status: [ON TRACK / AT RISK / DELAYED]
Key milestone: [MILESTONE] — [STATUS]
If delayed: Reason: [CAUSE] | Recovery plan: [PLAN]
Audience: [Your manager / The client / The project team]

Format:
Subject: [Status emoji] [Project] Status Update — [Date]
Body: 3 paragraphs — (1) status summary, (2) current situation/action, (3) next milestone + date

Tone: Transparent, professional, confident. Not defensive.
Do not use: "I wanted to update you," "Just checking in," or passive openers.
Under 180 words.
```

---

**PROMPT 2 — Difficult Conversation Email**
```
[ID: COM-002 | Category: Communication | Model: Any]

You are a senior professional experienced in navigating difficult conversations.

Write an email for this situation: [DESCRIBE THE DIFFICULT SITUATION]
My goal: [WHAT OUTCOME DO YOU WANT?]
My relationship with the recipient: [DESCRIBE THE RELATIONSHIP]

Requirements:
- Lead with empathy, not defensiveness
- Be direct about the issue without being accusatory
- Propose a concrete solution or next step
- Leave the door open for their perspective

Tone: Firm but respectful. Emotionally intelligent.
Do not use: blame language, passive aggression, or corporate non-speak.
Under 200 words.
```

---

**PROMPT 3 — LinkedIn Thought Leadership Post**
```
[ID: CON-001 | Category: Content | Model: ChatGPT/Claude]

You are a thought leader in [INDUSTRY/DOMAIN] who writes insightful
LinkedIn posts that generate engagement from [TARGET AUDIENCE].

Write a LinkedIn post about: [TOPIC]
My key insight or perspective: [YOUR UNIQUE ANGLE]
My professional experience that makes me credible here: [1 SENTENCE]

Structure:
Line 1: Hook — a bold statement, surprising fact, or counterintuitive claim
Lines 2–4: Develop the insight with 1 concrete example or story
Lines 5–7: 3–4 short bullet takeaways
Final line: Question to invite comments

Tone: Conversational, confident, genuine. NOT corporate or self-promotional.
Do not use: "Excited to share," "Humbled to announce," hashtag soup.
Line breaks between each section. Under 250 words total.
```

---

**PROMPT 4 — Competitor Analysis (Structured)**
```
[ID: ANA-001 | Category: Analysis | Model: Claude/ChatGPT]

You are a Senior Strategy Analyst with deep knowledge of [INDUSTRY].

Provide a structured analysis of [COMPETITOR NAME] as a competitor
for [YOUR COMPANY TYPE / VALUE PROPOSITION].

Use exactly this structure:

| Dimension | Analysis |
|-----------|---------|
| Core Product/Service | |
| Target Customer | |
| Key Competitive Advantages | |
| Known Weaknesses or Gaps | |
| Recent Strategic Moves | |
| Our Biggest Competitive Threat from Them | |
| Our Strongest Advantage vs. Them | |

After the table: 2–3 sentences on the strategic implication for us.

Sources: Note if any information is uncertain or requires verification.
```

---

**PROMPT 5 — Meeting Summary & Action Items**
```
[ID: COM-003 | Category: Communication | Model: Any]

Convert these meeting notes into a professional meeting summary.

Meeting: [MEETING TITLE]
Date: [DATE]
Attendees: [LIST]

Notes: [PASTE RAW NOTES HERE]

Output format:
## Meeting Summary: [Title] — [Date]

**Decisions Made:**
- [Decision 1]
- [Decision 2]

**Action Items:**
| Task | Owner | Deadline |
|------|-------|----------|
|      |       |          |

**Next Meeting:** [Date/Topic if mentioned]

Tone: Concise and professional. Use exactly the format above.
Do not add information that was not in the notes.
```

---

**PROMPT 6 — Job Description Generator**
```
[ID: HR-001 | Category: HR | Model: Any]

You are an experienced Talent Acquisition specialist who writes
inclusive, compelling job descriptions that attract top candidates.

Write a job description for: [JOB TITLE]
Department: [DEPARTMENT]
Level: [Junior / Mid / Senior / Manager / Director]
Key responsibilities: [LIST 3–5 KEY RESPONSIBILITIES]
Must-have qualifications: [LIST 3–4 MUST-HAVES]
Company culture notes: [2–3 words or a short phrase]

Structure:
1. Role headline (1 sentence — what makes this role exciting)
2. About the role (2–3 sentences — impact, team, growth)
3. What you'll do (5–7 bullets — responsibilities)
4. What we're looking for (4–5 bullets — requirements)
5. Why join us (3 bullets — culture/benefits)

Tone: Inclusive, energetic, human. Avoid masculine-coded language.
Avoid: "rockstar," "ninja," "hustle culture," "fast-paced environment."
```

---

**PROMPT 7 — Executive Summary Generator**
```
[ID: ANA-002 | Category: Analysis | Model: Claude/ChatGPT]

You are a senior business writer who specializes in executive summaries
for C-suite audiences who read under time pressure.

Write an executive summary of this document/findings:
[PASTE CONTENT OR DESCRIBE FINDINGS HERE]

Structure:
**Situation:** [1 sentence — what is the context?]
**Finding:** [1–2 sentences — the single most important insight]
**Implication:** [1 sentence — what does this mean for the business?]
**Recommendation:** [1 sentence — what should happen next?]

Tone: Authoritative, direct. No qualifications or hedging.
Rule: If it can be removed without losing information, remove it.
Maximum 100 words total.
```

---

**PROMPT 8 — Customer Complaint Response**
```
[ID: CS-001 | Category: Customer Service | Model: Any]

You are a Senior Customer Service Manager committed to turning
unhappy customers into loyal advocates.

Write a response to this customer complaint:
[PASTE COMPLAINT HERE]

Our response policy:
- Acknowledge and empathize first (never defend immediately)
- Take ownership — do not blame third parties
- Offer a specific solution or next step
- Invite continued dialogue

Tone: Warm, genuine, professional. Human, not scripted.
Do not use: "We apologize for any inconvenience," "We value your
feedback," or any phrase that sounds like a template.
Under 150 words. Personal and specific to their exact complaint.
```

---

**PROMPT 9 — Performance Review Comment Generator**
```
[ID: HR-002 | Category: HR | Model: Any]

You are an experienced manager skilled at writing performance review
comments that are specific, fair, and developmental.

Write a performance review comment for:
Employee context: [ROLE, LEVEL, TENURE]
Rating: [Exceeds / Meets / Partially Meets / Does Not Meet Expectations]
Key achievement this period: [SPECIFIC ACHIEVEMENT]
Key development area: [SPECIFIC AREA]
Goal for next period: [SPECIFIC GOAL]

Structure:
1. Opening statement of performance summary (1 sentence)
2. Key strength with specific example (2 sentences)
3. Development area with constructive framing (2 sentences — not critical)
4. Forward-looking goal (1 sentence)

Tone: Specific, fair, professional, development-focused.
Do not use vague phrases like "good team player" or "needs improvement."
Be specific — what exactly did they do, and what exactly should change?
Under 150 words.
```

---

**PROMPT 10 — Data Insight Narrative**
```
[ID: ANA-003 | Category: Analysis | Model: ChatGPT/Claude]

You are a Business Intelligence Analyst who translates raw data
into clear narratives for non-technical business audiences.

Here is the data: [PASTE DATA OR DESCRIBE KEY NUMBERS]

Write a data narrative that:
1. States the single most important trend or finding (1 sentence)
2. Explains the key drivers behind it (2–3 bullets)
3. Identifies one risk or concern hidden in the data (1 sentence)
4. Recommends one specific management action (1 sentence)

Tone: Clear, direct, business language. No statistics jargon.
Translate: percentages into implications, not just numbers.
Example of what I mean: Not "Revenue grew 12%." But "Revenue grew 12%
— faster than the previous quarter's 8% and significantly ahead of
the industry average of 7%, suggesting market share gain."
Under 200 words.
```

---

## 6. Module 2 Capstone: Build Your 10-Prompt Library

### 6.1 The Capstone Task

Build a personal 10-prompt library using the full metadata structure. Your library must:

**Minimum requirements:**
- 10 prompts covering at least 3 different functional categories
- Full metadata for each (ID, Name, Category, Purpose, Model, Version, Score)
- At least 3 prompts that went through minimum 2 iterations (show version history)
- At least 2 prompts with few-shot examples embedded
- At least 1 prompt that uses chain-of-thought technique
- At least 1 prompt with output anchoring

**Deliverable format:** A structured document (Word/PDF/Notion) or shared Google Doc

---

### 6.2 Hands-On Lab 10: Library Sprint

**Objective:** Build the first 5 prompts of your library in class  
**Duration:** 25 minutes

---

**Step 1 (5 min): Plan your library**

Choose 5 tasks from your real professional or academic life. For each:
- What is the task?
- How often do you do it?
- What category does it belong to?
- What would "excellent" output look like?

---

**Step 2 (15 min): Build 5 prompts**

For each task, write a complete CRAFT prompt using the metadata structure:

| Field | Your Entry |
|-------|-----------|
| ID | |
| Name | |
| Category | |
| Purpose | |
| Model | |
| Version | v1.0 |
| Prompt Text | |
| Variables | |
| Notes | |

Run each prompt in ChatGPT and score it on the quality rubric (out of 30).

---

**Step 3 (5 min): Optimize your lowest-scoring prompt**

Identify the lowest-scoring of your 5 prompts. Apply 1–2 targeted fixes. Run it again. Record the new score as v1.1.

---

### Lab Evaluation Rubric

| Deliverable | Marks |
|-------------|-------|
| 5 prompts written with full metadata | 5 |
| All 5 tested and scored on quality rubric | 2 |
| One prompt optimized (v1.0 → v1.1) with improvement documented | 3 |
| **Total** | **10** |

---

## 7. Module 2 Final Assessment Preparation

### 7.1 The 5 Highest-Leverage Prompt Engineering Skills

Ranked by professional impact:

```
1. CRAFT Framework application           → Eliminates generic outputs
2. Output anchoring                      → Eliminates reformatting work
3. Few-shot examples                     → Enables brand voice replication
4. Chain-of-thought                      → Enables complex analysis
5. Negative instructions                 → Eliminates manual cleanup
```

### 7.2 Module 2 Key Concepts Flashcard Review

| Concept | One-Line Definition |
|---------|-------------------|
| CRAFT | Context, Role, Action, Format, Tone, Constraints — the 6 prompt components |
| Zero-shot | Prompt with no examples; AI infers from training |
| Few-shot | Prompt with 2–8 examples establishing the output pattern |
| Chain-of-Thought | Instructing AI to reason step-by-step before concluding |
| Self-critique | Prompting AI to review and challenge its own output |
| Output anchoring | Providing a template/skeleton that AI fills in |
| Negative instructions | Explicitly telling AI what NOT to produce |
| Prompt decomposition | Breaking complex tasks into sequential focused prompts |
| Persona engineering | Building a precise expert identity with title, experience, style |
| Prompt library | Curated collection of tested, versioned, production-ready prompts |

---

## 8. Interview Questions — Session 10

**Q1:** *"How do you systematically improve a prompt that isn't working?"*

**Strong Answer:**
"I use a structured optimization cycle: test the prompt 2–3 times to understand typical output range, then evaluate each dimension — relevance, accuracy, format, tone, usability, depth. I diagnose the specific failure mode rather than changing everything at once. Common fixes are targeted: if the output is too generic, I add a richer persona; if the format is wrong, I add output anchoring; if it consistently includes unwanted content, I add negative instructions. I change one element at a time so I can isolate what improved the output. I then version and document the improvement — v1.0 to v1.1 — so I build a history of what works for each task type."

**Q2:** *"What is a prompt library and why would a company invest in building one?"*

**Strong Answer:**
"A prompt library is a curated, versioned, metadata-rich collection of tested prompts organized by task type. Companies invest in building one for three reasons. First, quality: team members use proven, optimized prompts rather than reinventing from scratch each time — reducing variance and raising the floor of AI output quality. Second, efficiency: when an analyst can start a competitive analysis from a tested template rather than drafting from zero, hours become minutes. Third, institutional knowledge: the library captures the team's AI expertise in a portable, shareable form. When a senior person leaves, their prompt expertise stays in the library. A prompt library is increasingly a standard component of a team's operational playbook."

---

## 9. Revision Questions — Session 10

1. Describe the Prompt Optimization Cycle. What are its 5 stages?
2. What is the "one element at a time" rule in prompt optimization, and why does it matter?
3. What is output anchoring? Give a concrete example of when it prevents rework.
4. List 5 specific negative instructions you could add to a prompt. For each, explain what problem it solves.
5. What is the "self-instruction refinement" technique? Walk through the 3 steps.
6. What metadata fields should every prompt library entry include?
7. What is version control in a prompt library context? Why does it matter?
8. Score this prompt: "You are a financial analyst at a PE firm. Write a 1-page investment memo for this startup [attached financials]. Format: Situation / Opportunity / Risk / Recommendation. Under 400 words. Do not use 'synergies' or vague ROI claims — quantify everything." (Use the 6-dimension rubric.)

---

## 10. Key Terminology — Session 10

| Term | Definition |
|------|-----------|
| **Prompt Optimization Cycle** | Design → Test → Evaluate → Diagnose → Refine → Repeat |
| **Output Anchoring** | Providing an exact template or skeleton structure for AI to fill in |
| **Negative Instructions** | Explicit constraints telling AI what NOT to include or do |
| **Progressive Refinement** | Iteratively improving a prompt by adding specificity based on what fails |
| **Self-Instruction Refinement** | Using AI to critique and improve your prompt before running the actual task |
| **Quality Rubric** | Structured scoring framework to objectively evaluate AI output (6 dimensions) |
| **Prompt Library** | Curated collection of tested, versioned, production-ready prompts with metadata |
| **Prompt Metadata** | Structured information about a prompt: ID, category, purpose, version, score, notes |
| **Version Control (prompts)** | Tracking iterations of a prompt (v1.0 → v1.1 → v2.0) with change notes |
| **Production-Ready Prompt** | A prompt that consistently scores ≥25/30 and is cleared for regular use |

---

## 11. Summary and Module 2 Close

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 10 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  Optimization = test → evaluate → diagnose → fix ONE thing → repeat     │
│  ✓  Output anchoring: give AI the skeleton to fill in → no reformatting    │
│  ✓  Negative instructions: every manual edit → convert to prompt rule       │
│  ✓  Self-instruction: ask AI to critique your prompt before running it      │
│  ✓  Score every prompt on 6 dimensions (30-point rubric)                    │
│  ✓  Library = prompts + metadata + version history + sample outputs        │
│  ✓  A prompt used once = one-time gain. A library = compounding asset.     │
│                                                                              │
├──────────────────────────────────────────────────────────────────────────────┤
│  MODULE 2 COMPLETE — YOU NOW KNOW:                                           │
│  ✓ CRAFT Framework for professional prompt construction                     │
│  ✓ Zero-shot, one-shot, few-shot — when and how to use each                │
│  ✓ Chain-of-thought for complex reasoning and analysis                      │
│  ✓ Persona engineering for expert-level outputs                             │
│  ✓ Optimization cycle, output anchoring, negative instructions              │
│  ✓ Building a personal and team prompt library                              │
├──────────────────────────────────────────────────────────────────────────────┤
│  NEXT MODULE:                                                                │
│  Module 3 — AI for Productivity (Sessions 11–15)                            │
│  "Applying your prompt skills to real professional tasks:                   │
│   email, reports, presentations, research, and building a personal         │
│   AI productivity system"                                                   │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 10 Complete | Module 2 Complete | Next: Session 11 — AI for Professional Email & Communication*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
