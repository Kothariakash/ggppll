# Session 5: The CRAFT Framework — Putting It All Together
## Module 1 — Foundations of Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 5 OF 30  │  Module 1, Session 5                           │
│  Topic: CRAFT Framework, Prompt Quality Assessment & Module Capstone│
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Apply the CRAFT framework as a complete prompt-building system
2. Evaluate any prompt using a 5-dimension quality scoring rubric
3. Identify and fix the 5 most common prompt anti-patterns
4. Build a personal reusable template for any professional use case
5. Apply CRAFT to three different professional domains from a single framework
6. Complete the Module 1 capstone assessment

---

## 5.1 The CRAFT Framework

CRAFT is a memorable, practical framework that consolidates everything from Sessions 1–4 into a single system you can apply to any prompt — in any professional context.

```
┌──────────────────────────────────────────────────────────────────┐
│                     THE CRAFT FRAMEWORK                          │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│   C — CONTEXT      What is the background and situation?        │
│   R — ROLE         Who should the AI be?                        │
│   A — ACTION       What specific task should the AI perform?    │
│   F — FORMAT       How should the output be structured?         │
│   T — TONE         What style and voice is appropriate?         │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

Note the relationship to the 5-component anatomy from Session 3:

| Session 3 Component | CRAFT Equivalent |
|--------------------|-----------------|
| Role/Persona | R — Role |
| Context | C — Context |
| Task/Instruction | A — Action |
| Format | F — Format |
| Constraints | Embedded across T (Tone) and A (Action) |

CRAFT adds **Tone** as an explicit, named component — because in professional contexts, tone is often the most frequently neglected dimension.

---

## 5.2 CRAFT — Component Deep Dive

### C — Context

Context answers: *What is the situation? What background does the AI need?*

**Context should include (as relevant):**
- Who you are (role, company, industry)
- Who the audience is (their background, expertise, relationship to you)
- What problem you're solving or what goal you're achieving
- What constraints or circumstances exist in your situation
- What has been tried or decided already
- What data, documents, or information is relevant (paste it in)

**Context richness scale:**

```
Level 1 (Weak):   "I run a business."
Level 2:          "I run a small HR consulting firm."
Level 3:          "I run a 5-person HR consulting firm in Chennai serving mid-sized
                   manufacturing companies (200-500 employees)."
Level 4 (Strong): "I run a 5-person HR consulting firm in Chennai. We work with
                   mid-sized manufacturing companies (200-500 employees) on
                   compliance, recruitment, and training. Our main challenge is
                   that clients view HR as a cost center, not a value driver.
                   We recently won 2 new clients in the automotive sector."
```

Level 4 context will produce dramatically more tailored advice than Level 1.

---

### R — Role

Role answers: *What expertise, identity, and perspective should the AI adopt?*

**Role formula:**
```
"You are a [TITLE] with [CREDENTIALS/EXPERIENCE] who specializes in [AREA].
You [CHARACTERISTIC APPROACH/VALUE]. You communicate with [STYLE]."
```

**Role by use case:**

| Use Case | Effective Role |
|----------|---------------|
| Technical writing | "You are a senior technical writer who specializes in making complex systems understandable to non-technical business users." |
| Legal review | "You are a corporate lawyer with 20 years of experience in commercial contracts. You are known for identifying hidden risks that non-lawyers miss." |
| Marketing | "You are a direct-response copywriter with 10 years of experience writing for B2B SaaS companies. You prioritize clarity over cleverness." |
| Training design | "You are an instructional designer who builds learning experiences for adult professionals. You follow principles of spaced repetition and active recall." |
| Financial analysis | "You are a CFO with experience in both startups and large enterprises. You communicate financial insights to non-finance stakeholders without dumbing it down." |

**What NOT to do with Role:**
```
❌ "You are Albert Einstein" → Impersonating a real person
❌ "You are God" → Absurd personas produce poor results
❌ "You are a very smart assistant" → Vague, doesn't activate domain knowledge
✅ "You are a neurologist who specializes in patient education" → Specific and useful
```

---

### A — Action

Action answers: *What exactly should the AI do?*

**The A in CRAFT = Task + specific action verb + explicit deliverable**

```
WEAK ACTION:
"Help me with my project proposal."

STRONG ACTION:
"Write the Executive Summary section of a project proposal.
Cover: project objective (2 sentences), key benefits (3 bullet points),
budget summary (1 sentence), and timeline (1 sentence).
This is the first section the reader will see — make it compelling."
```

**Multi-step action with numbered instructions:**

When the task involves a specific sequence, number the steps:

```
"Complete the following actions in order:
1. Read the meeting notes below and extract all decisions made
2. For each decision, identify: who owns it, what the deadline is, and any dependencies
3. List any items discussed but NOT decided — these are open questions
4. Format the output as structured meeting minutes

Meeting notes: [paste here]"
```

---

### F — Format

Format answers: *What is the shape and structure of the output?*

**The Format specification should always answer:**
- What is the overall structure? (document type)
- What are the sections/parts?
- What is the expected length?
- Are there any visual or structural elements (tables, code blocks, headings)?

**Format specification levels:**

```
Level 1 (Minimal):
"As bullet points."

Level 2 (Structured):
"As a numbered list of 5 points, each with a bold title."

Level 3 (Complete):
"Structure as:
 - Headline (bold, 1 sentence — the single most important takeaway)
 - Summary (3 sentences — situation, finding, recommendation)
 - Key Points (5 bullet points, each starting with a bold keyword)
 - Call to Action (1 sentence — specific next step)
 Total length: 200–250 words."

Level 4 (Technical):
"Return as JSON conforming to this schema:
{
  'headline': string (max 10 words),
  'summary': string (max 50 words),
  'key_points': array of objects [{'keyword': string, 'explanation': string}],
  'call_to_action': string (max 20 words)
}"
```

---

### T — Tone

Tone answers: *What voice, style, and register is appropriate for this context?*

**Tone is the most commonly forgotten component** — and often the reason a technically correct response still "feels wrong."

**Tone specification system:**

```
PRIMARY TONE (the overall feel):
formal | professional | conversational | academic | casual |
technical | approachable | authoritative | empathetic | urgent

SECONDARY MODIFIER (the angle):
concise | detailed | inspiring | analytical | persuasive |
encouraging | neutral | critical | nurturing | direct

AUDIENCE CALIBRATION:
"appropriate for a [audience] who [has/wants/knows/fears X]"

STYLE RULES:
"Use active voice" | "Avoid jargon" | "Short sentences (under 15 words)"
"Second person ('you')" | "No hedging language" | "Evidence-first"
```

**Tone combination examples:**

```
Board presentation: "Formal, authoritative, data-led. No fluff."

Team email after a setback: "Empathetic but forward-looking. Acknowledge
the difficulty briefly, then pivot to what's next."

Sales email: "Professional but conversational. Confident without being
pushy. Use 'you' language — focus on the reader's outcome, not our product."

Customer complaint response: "Empathetic first, then practical. Validate
their frustration before offering a solution."

Internal training material: "Conversational and encouraging. Use examples.
Avoid anything that sounds like a policy document."
```

---

## 5.3 CRAFT in Action — Complete Worked Examples

### Worked Example 1: Strategic Business Email

**Scenario:** You are a startup founder requesting a partnership meeting with a large corporate.

```
C (Context):
"I am the founder of DataSync, an AI-powered data integration startup
(2 years old, 15 customers, Series A in progress, ₹8 Cr ARR).
I want to request a partnership exploration meeting with TechCorp India,
a ₹2,000 Cr enterprise software company. My contact is their Head of
Partnerships, whom I met briefly at a conference 3 months ago."

R (Role):
"You are an experienced startup founder who is skilled at writing
partnership outreach emails that are confident, peer-level, and focused
on mutual value — not sounding like a vendor asking for a favor."

A (Action):
"Write a cold outreach email requesting a 30-minute partnership
exploration call."

F (Format):
"Email format:
 - Subject line (creates curiosity, max 8 words)
 - Opener (1 sentence — reference our brief meeting)
 - Value hook (2–3 sentences — why this is worth their time)
 - Specific ask (1 sentence — 30 min call, give 2 date options)
 - Closing (1 line)
 Maximum 150 words total (body only, excluding subject)"

T (Tone):
"Peer-level and confident, not supplicant. Professional but not stiff.
Focus on their potential gain, not our need. No buzzwords."
```

**Full CRAFT prompt:**
```
You are an experienced startup founder skilled at writing partnership
outreach emails that are confident, peer-level, and focused on mutual value.

Context: I am the founder of DataSync, an AI-powered data integration startup
(₹8 Cr ARR, Series A in progress). I want a partnership exploration meeting with
the Head of Partnerships at TechCorp India — someone I met briefly 3 months ago
at the FinTech Summit.

Write a cold outreach email requesting a 30-minute partnership call.

Format: Subject line (curiosity, max 8 words) | 1-line opener referencing
our meeting | 2–3 sentence value hook (why this matters to them) |
1-sentence specific ask with 2 date options | 1-line close.
Body under 150 words.

Tone: Peer-level confidence. Professional but not stiff. Their potential gain
first, our need last. No buzzwords or "synergy" language.
```

---

### Worked Example 2: HR Job Description

```
C (Context):
"Our company, Freshfarm Technologies, is a 180-person agri-tech startup
in Hyderabad. We are hiring a Head of Marketing — our first marketing hire
at the senior leadership level. The company culture is fast-paced, data-driven,
and mission-driven (sustainable agriculture). Current team: 3 junior marketers
and 2 interns. Budget: ₹35–50 LPA."

R (Role):
"You are an experienced HR business partner who writes job descriptions that
attract top talent. You know how to write descriptions that excite candidates
(not just list requirements), use inclusive language, and reflect genuine
company culture."

A (Action):
"Write a complete job description for the Head of Marketing role."

F (Format):
"Sections (in order):
 1. About Freshfarm Technologies (3 sentences — mission, growth, culture)
 2. About This Role (2 paragraphs — what makes this role unique and impactful)
 3. What You Will Do (6 bullet points, action verb-led)
 4. What We're Looking For (Must Have: 5 items | Nice to Have: 3 items)
 5. Compensation & Benefits (include placeholder: ₹35–50 LPA + equity)
 6. Inclusion Statement (2 sentences)"

T (Tone):
"Authentic and mission-driven. Exciting — reads like an opportunity,
not a compliance form. Avoids corporate HR clichés ('fast-paced environment',
'wearing many hats', 'rockstar'). Gender-neutral language throughout."
```

---

### Worked Example 3: Technical Code Generation

```
C (Context):
"I am building a Python API for a content moderation system. I need a
function that checks whether a given text contains any of a provided list
of prohibited keywords. The function will be called thousands of times per
minute, so performance matters. Prohibited keywords are case-insensitive
and may appear as substrings within words (e.g., 'hate' in 'hateful')."

R (Role):
"You are a senior Python backend developer with expertise in performance
optimization. You write production-ready code with proper error handling,
documentation, and testing."

A (Action):
"Write a Python function called 'contains_prohibited_content' that checks
whether input text contains any prohibited keywords."

F (Format):
"Python code block containing:
 - Function with type hints
 - Docstring (purpose, parameters, returns, raises, example)
 - Input validation (empty string, None, invalid types)
 - The core implementation (optimized for speed)
 - Unit tests using pytest (5 test cases: empty input, no match, exact match,
   substring match, case-insensitive match)"

T (Tone):
"Clean, professional Python code following PEP 8 style.
Inline comments only where logic is non-obvious. No unnecessary verbosity."
```

**Expected output:**

```python
import re
from typing import List, Optional
import pytest


def contains_prohibited_content(
    text: str,
    prohibited_keywords: List[str]
) -> tuple[bool, Optional[str]]:
    """
    Check whether a text contains any prohibited keywords (case-insensitive,
    substring match).

    Args:
        text: The input text to check. Must be a non-None string.
        prohibited_keywords: List of prohibited keyword strings.

    Returns:
        A tuple of (is_prohibited: bool, matched_keyword: str | None).
        Returns (True, matched_keyword) on first match found.
        Returns (False, None) if no prohibited content detected.

    Raises:
        TypeError: If text is not a string or prohibited_keywords is not a list.
        ValueError: If prohibited_keywords contains non-string elements.

    Example:
        >>> result = contains_prohibited_content("I hate this", ["hate", "violence"])
        >>> print(result)
        (True, 'hate')
    """
    # Input validation
    if not isinstance(text, str):
        raise TypeError(f"text must be a string, got {type(text).__name__}")
    if not isinstance(prohibited_keywords, list):
        raise TypeError(f"prohibited_keywords must be a list, got {type(prohibited_keywords).__name__}")
    if not all(isinstance(kw, str) for kw in prohibited_keywords):
        raise ValueError("All prohibited_keywords must be strings")

    if not text or not prohibited_keywords:
        return False, None

    # Pre-compile regex patterns once for performance (substring, case-insensitive)
    text_lower = text.lower()
    for keyword in prohibited_keywords:
        if keyword.lower() in text_lower:
            return True, keyword

    return False, None


# ─── Unit Tests ───────────────────────────────────────────────────────────────

class TestContainsProhibitedContent:

    def test_empty_text_returns_false(self):
        result = contains_prohibited_content("", ["hate"])
        assert result == (False, None)

    def test_no_match_returns_false(self):
        result = contains_prohibited_content("Have a wonderful day!", ["hate", "violence"])
        assert result == (False, None)

    def test_exact_match_detected(self):
        is_prohibited, keyword = contains_prohibited_content("hate is wrong", ["hate"])
        assert is_prohibited is True
        assert keyword == "hate"

    def test_substring_match_detected(self):
        # 'hate' should be found inside 'hateful'
        is_prohibited, keyword = contains_prohibited_content("This is hateful content", ["hate"])
        assert is_prohibited is True
        assert keyword == "hate"

    def test_case_insensitive_match(self):
        is_prohibited, keyword = contains_prohibited_content("HATE this product", ["hate"])
        assert is_prohibited is True
        assert keyword == "hate"
```

---

## 5.4 The Prompt Quality Scoring Rubric

Use this rubric to score any prompt before submitting, or to evaluate why a response fell short.

| Dimension | 1 — Poor | 3 — Adequate | 5 — Excellent | Score |
|-----------|----------|-------------|---------------|-------|
| **Clarity** | Ambiguous — multiple interpretations possible | One clear reading, minor ambiguity | Unambiguous — zero room for misinterpretation | /5 |
| **Specificity** | Generic — applies to any situation | Some specifics — industry or role mentioned | Highly specific — company, audience, data, constraints all present | /5 |
| **Context** | No background provided | Basic who/what provided | Full situation, audience, constraints, and history provided | /5 |
| **Structure** | No format specified | Basic format (e.g., "bullet points") | Complete format spec: structure + length + each component defined | /5 |
| **Constraints** | No rules or boundaries | 1–2 basic constraints | 4+ targeted constraints covering scope, tone, length, exclusions | /5 |
| **TOTAL** | | | | /25 |

**Interpretation:**
- 20–25: Professional-grade prompt. Submit with confidence.
- 14–19: Good prompt. Identify lowest-scoring dimension and improve before submitting.
- 8–13: Needs significant work. Likely to produce generic output.
- 5–7: Weak prompt. Rebuild using CRAFT before submitting.

---

## 5.5 Common Prompt Anti-Patterns

These are the most frequently observed patterns in poor prompts. Learn to recognize and correct them.

### Anti-Pattern 1: The Open Abyss

```
❌ "Tell me everything about blockchain."
Problem: No scope, no audience, no format — AI will generate 2,000 words of generic content.
✅ Fix: "Explain the 3 core concepts behind blockchain that a bank executive needs to
understand when evaluating a DeFi investment. Use analogies to traditional banking.
Under 300 words."
```

### Anti-Pattern 2: The Assumption Prompt

```
❌ "Continue the report."
Problem: AI has no idea what report, what section, what style, or what comes next.
✅ Fix: "[Paste report so far]
Continue this report by writing the Risk Analysis section.
Match the tone and structure of the sections above.
Cover: 4 key risks, each with probability, impact, and mitigation. Table format."
```

### Anti-Pattern 3: The Wish Upon a Star

```
❌ "Make my business successful."
Problem: Impossibly broad. AI cannot "make" anything — it generates text.
✅ Fix: "I run a tutoring business struggling with lead generation.
Recommend 5 specific, low-cost digital marketing tactics for getting
more student inquiries. Each tactic: name, how to implement, expected cost,
expected outcome. Table format."
```

### Anti-Pattern 4: The Ambiguous Pronoun

```
❌ "Sarah told Priya that she had made a mistake in the report."
Problem: "She" refers to Sarah or Priya? AI may guess wrong.
✅ Fix: Always use full names and explicit references. "Sarah told Priya that Priya
had made a mistake in the report."
```

### Anti-Pattern 5: The Overloaded Prompt

```
❌ "Analyze my business, write a plan, create financials, design a marketing
strategy, write social media content, and suggest investors to approach."

Problem: 6 distinct tasks in one prompt — AI will do all of them shallowly.
✅ Fix: Create 6 separate prompts. Run them sequentially, using each output as
context for the next.
```

---

## 5.6 CRAFT Quick-Reference Card

```
┌──────────────────────────────────────────────────────────────────────────┐
│  CRAFT QUICK-REFERENCE CARD                                              │
│  Print this. Keep it open while prompting.                               │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  C — CONTEXT    │ Who am I? Who is the audience? What's the situation?  │
│                 │ What data/constraints exist? What has been tried?     │
├─────────────────┼────────────────────────────────────────────────────────┤
│  R — ROLE       │ "You are a [TITLE] with [X years] of [SPECIALTY].    │
│                 │ You prioritize [VALUES]. You communicate with [STYLE]"│
├─────────────────┼────────────────────────────────────────────────────────┤
│  A — ACTION     │ Strong action verb + specific deliverable             │
│                 │ Write / Analyze / Extract / Compare / Evaluate...     │
├─────────────────┼────────────────────────────────────────────────────────┤
│  F — FORMAT     │ Overall structure: email / table / report / list...   │
│                 │ Sections + length + visual elements + technical format│
├─────────────────┼────────────────────────────────────────────────────────┤
│  T — TONE       │ Primary: formal/conversational/empathetic/urgent...   │
│                 │ Modifier: concise/inspiring/direct/evidence-first...  │
│                 │ Style rules: active voice / no jargon / second person │
├─────────────────┼────────────────────────────────────────────────────────┤
│  CONSTRAINTS    │ Embedded in A, F, T — but list separately:           │
│  (bonus layer)  │ Word count | Scope limits | Exclusions | Must-include │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## 5.7 Building Prompt Templates with CRAFT

CRAFT is most powerful when used as a template structure. Here are three ready-to-use CRAFT templates:

### Template 1: Professional Email

```
C: I am a [ROLE] at [COMPANY TYPE]. My recipient is [RECIPIENT ROLE] at [RELATIONSHIP].
   The situation: [2-sentence description of what happened and why this email is needed].

R: You are a professional business communicator who writes clear, persuasive emails
   that achieve their goal while maintaining a positive professional relationship.

A: Write a [REQUEST/FOLLOW-UP/APOLOGY/ANNOUNCEMENT] email.

F: Email format — Subject line | Greeting | [3 paragraphs: situation, key message,
   next step] | Professional closing. Under [WORD COUNT] words.

T: [Formal/Professional/Warm]. Active voice. No clichés.
   Audience expectation: [brief note on recipient's style/culture].
```

### Template 2: Research Overview

```
C: I am researching [TOPIC] for [PURPOSE]. My audience is [AUDIENCE].
   I have [SOME/NO/INTERMEDIATE] background in this area.
   Key aspect I most need to understand: [SPECIFIC FOCUS].

R: You are a senior research analyst who specializes in synthesizing complex
   information into clear, actionable insights for [AUDIENCE TYPE].

A: Create a structured research overview on [TOPIC].

F: Structure:
   1. Definition & Background (2 paragraphs)
   2. Current State (bullet points with approximate figures — flag for verification)
   3. Key Trends (3–5 bullet points with brief explanations)
   4. Key Challenges (3–4 bullet points)
   5. Implications for [MY CONTEXT] (2–3 specific, actionable insights)
   Total: 500–700 words.

T: Research report tone — authoritative and evidence-referenced.
   Flag any statistics with [VERIFY] if uncertain of accuracy.
   Avoid jargon specific to [FIELD] without explanation.
```

### Template 3: Data Extraction (Technical)

```
C: I have [TYPE OF DOCUMENT] containing unstructured [TYPE OF DATA].
   I need to extract specific fields for [PURPOSE/DOWNSTREAM USE].

R: You are a precise data extraction specialist who outputs clean,
   structured data. You never guess — you use null for missing values.

A: Extract the following fields from the document below: [LIST FIELDS].

F: Return as JSON conforming to this exact schema:
   {
     "[field_name]": [type],
     "[field_name]": [type] (null if not present)
   }
   Return ONLY the JSON. No commentary, no markdown code fences.

T: Precise and literal. Never infer or assume. If a value could be
   interpreted multiple ways, use the more conservative interpretation.

[PASTE DOCUMENT HERE]
```

---

## Hands-On Activities — Session 5

---

### Activity 5.1 — CRAFT Framework Practice (3 Scenarios)

Apply the full CRAFT framework to all three scenarios. Write complete prompts, run them, and evaluate the outputs.

**Scenario A — Teacher Creating a Quiz:**
```
You are a teacher who needs to create a 10-question multiple-choice quiz for
your students on the topic of climate change. Students are in Class 10 (CBSE).
Build a CRAFT prompt and run it.
```

Fill in:
- C: ____________________
- R: ____________________
- A: ____________________
- F: ____________________
- T: ____________________

**Scenario B — Job Seeker Improving LinkedIn Summary:**
```
You have 5 years of experience as a data analyst in retail banking and
are transitioning to a fintech startup. Your LinkedIn summary is weak
and generic. Build a CRAFT prompt to rewrite it.
```

**Scenario C — Small Business Owner Needing Social Media Ideas:**
```
You run a home bakery in Pune selling artisanal cakes and desserts.
You want content ideas for the next 2 weeks across Instagram and WhatsApp.
Build a CRAFT prompt for this.
```

---

### Activity 5.2 — Prompt Scoring Lab

Score these two prompts using the 5-dimension rubric (each out of 5, total /25):

**Prompt A:**
```
"Summarize this document and make it better."
```

**Prompt B:**
```
"You are a senior business consultant who specializes in executive communication.

Context: I am a VP of Operations presenting a 1,200-word operational review
to our Board of Directors. The board (8 people, mixed business/finance backgrounds)
will read this as a pre-read before a 45-minute board meeting.

Action: Rewrite the following operational review to be board-ready.

Format: Structure as:
- Headline (1 bold sentence: the single most important operational takeaway)
- Executive Summary (3 sentences: situation, key change, recommendation)
- Key Metrics (table: Metric | Current | Target | Gap | Trend)
- 3 Strategic Issues (each: issue name, 2-sentence description, proposed action)
- Decision Required (1 clear sentence — what the board must decide)
Maximum 500 words.

Tone: Executive — authoritative, data-led, no padding. Every word earns its place.
Active voice throughout. No operational jargon — translate to business language.

[PASTE DOCUMENT HERE]"
```

| Dimension | Prompt A Score | Prompt B Score |
|-----------|---------------|---------------|
| Clarity | /5 | /5 |
| Specificity | /5 | /5 |
| Context | /5 | /5 |
| Structure | /5 | /5 |
| Constraints | /5 | /5 |
| **Total** | **/25** | **/25** |

---

### Activity 5.3 — Module 1 Capstone Challenge

**Task:** Create a single, professional-grade CRAFT prompt for a real problem you currently face at work, study, or in your professional development.

**Requirements:**
Your prompt must:
1. Use all 5 CRAFT components explicitly
2. Include at least 4 constraints (scope, length, exclusion, inclusion)
3. Specify a detailed output format
4. Be tested in an AI tool with at least 2 iterations

**Submission includes:**
- Your CRAFT prompt (Version 1)
- The AI response (Version 1)
- Your iteration prompt (what you changed and why)
- The AI response (Version 2)
- A written reflection (150 words): What worked? What still needed improvement? What would you change in a Version 3?

**Scoring rubric:**

| Criterion | Points |
|-----------|--------|
| All 5 CRAFT components clearly present | 20 |
| At least 4 constraints included | 15 |
| Detailed format specification | 15 |
| Evidence of genuine iteration (Version 2 is measurably better) | 20 |
| Written reflection — specific and insightful | 15 |
| Output quality — is V2 genuinely usable professionally? | 15 |
| **Total** | **100** |

---

## Module 1 Assessment — Knowledge Check

**Part A — Short Answer (2–3 sentences each)**

1. Explain the difference between an LLM and a traditional search engine. What does each do when you ask them a question?

2. What is a token? Give an example of a word that is 1 token and a word that is 3 or more tokens.

3. A user's ChatGPT conversation is getting very long. They notice the AI seems to "forget" things they said earlier. What is happening technically, and what should they do?

4. What is hallucination in LLMs? Give a professional scenario where hallucination could cause a serious problem.

5. Explain the difference between temperature = 0 and temperature = 1.5. Give a use case where each setting is appropriate.

**Part B — Prompt Evaluation**

Read the following prompt and:
a) Identify which CRAFT components are present and which are missing
b) Score it using the 5-dimension rubric
c) Rewrite it as a complete CRAFT-structured prompt

**Prompt to evaluate:**
```
"Write something about digital transformation for my company."
```

**Part C — Practical Assessment**

*Scenario:* You are an HR professional who needs to create a job description for a Data Analyst role at a mid-sized retail company in Mumbai.

Write a complete CRAFT prompt that would generate a professional, compelling job description. Run it, evaluate the output against the rubric, and refine it once.

Submit both versions of the prompt and the final job description.

---

## Module 1 Summary

| Session | Core Topic | The One Sentence You Must Remember |
|---------|-----------|-----------------------------------|
| **Session 1** | AI & LLMs | LLMs predict the most likely next token — they don't "know" or "think" — verify everything important. |
| **Session 2** | Tokens & Context | The context window is the model's working memory — manage it intentionally in long conversations. |
| **Session 3** | Prompt Anatomy | Every great prompt has Role, Context, Task, Format, and Constraints — identify what's missing when outputs disappoint. |
| **Session 4** | Best Practices | First output = first draft; always iterate at least once and verify facts before professional use. |
| **Session 5** | CRAFT Framework | CRAFT (Context, Role, Action, Format, Tone) is the professional system for building any prompt from scratch. |

---

## Further Reading — Module 1

| Resource | Topic | Access |
|----------|-------|--------|
| OpenAI Prompt Engineering Guide | Official best practices | platform.openai.com/docs/guides/prompt-engineering |
| Anthropic Prompt Library | 50+ real prompt examples | docs.anthropic.com/en/prompt-library |
| learnprompting.org | Free comprehensive course aligned with this module | Free |
| OpenAI Tokenizer | Interactive token counting tool | platform.openai.com/tokenizer |
| "Prompt Engineering Guide" by DAIR.AI | Technical reference | promptingguide.ai |

---

*Module 1 Complete → Proceed to Module 2: Prompting Techniques (Session 6: Zero-Shot Prompting)*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
