# Session 10: Prompt Optimization
## Module 2 — Prompting Techniques
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 10 OF 30  │  Module 2, Session 5                          │
│  Topic: Prompt Optimization — Systematic Refinement for Consistent  │
│          High-Quality Output                                        │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Apply the Prompt Optimization Cycle to any underperforming prompt
2. Diagnose specific failure modes and apply targeted fixes
3. Use decomposition, output anchoring, negative instructions, and self-critique techniques
4. Build and maintain a versioned prompt library with quality metadata
5. Design a chain-prompting workflow for complex multi-output tasks
6. Complete the Module 2 assessment with a demonstrated optimization journey

---

## 10.1 What is Prompt Optimization?

**Prompt optimization** is the systematic, evidence-based process of improving a prompt to consistently produce high-quality, reliable outputs. It treats prompting like engineering — you test, measure, diagnose, and refine based on data, not guesswork.

The key shift in mindset:

```
AMATEUR APPROACH:              PROFESSIONAL APPROACH:
──────────────────             ──────────────────────────────────
Write a prompt                 Write a prompt → test multiple times
Accept the output              Evaluate against explicit success criteria
Try again if unsatisfied       Diagnose the specific failure mode
Hope for better results        Apply a targeted fix
                               Test again and compare
                               Document the winning version
```

---

## 10.2 The Prompt Optimization Cycle

```
┌───────────────────────────────────────────────────────────────┐
│                  PROMPT OPTIMIZATION CYCLE                    │
│                                                               │
│    ┌─────────┐                                                │
│    │  DESIGN │  Write initial prompt using CRAFT             │
│    └────┬────┘                                                │
│         │                                                     │
│         ▼                                                     │
│    ┌─────────┐                                                │
│    │  TEST   │  Run prompt 3–5 times to understand variance  │
│    └────┬────┘                                                │
│         │                                                     │
│         ▼                                                     │
│    ┌──────────┐                                               │
│    │ EVALUATE │  Score against success criteria              │
│    └────┬─────┘                                               │
│         │                                                     │
│         ▼                                                     │
│    ┌──────────┐                                               │
│    │ DIAGNOSE │  Identify the specific failure mode          │
│    └────┬─────┘                                               │
│         │                                                     │
│         ▼                                                     │
│    ┌────────┐                                                 │
│    │ REFINE │  Apply one targeted fix at a time              │
│    └────┬───┘                                                 │
│         │                                                     │
│         └──────────────────────────────────────► TEST AGAIN  │
└───────────────────────────────────────────────────────────────┘
```

### Step 1: Design

Use CRAFT to build your initial prompt. Don't optimize prematurely — write a solid first version, then improve it based on evidence.

### Step 2: Test

Run the same prompt **3–5 times** before drawing conclusions. Due to temperature-based randomness, a single run may not represent typical output. Look for:
- Consistency: Does the output format stay the same across runs?
- Quality: What's the average quality? What's the worst case?
- Variance: How much does the output change from run to run?

### Step 3: Evaluate

Score the output against your **success criteria** — which you should define BEFORE testing, not after.

**Defining success criteria:**
```
Task: Generate a weekly status report

Success criteria:
✓ Contains all 5 required sections (Completed, In Progress, Blockers, Next Week, Metrics)
✓ Every completed item states an outcome, not just an activity
✓ Blockers section specifies what help is needed
✓ Total length under 300 words
✓ Tone is professional and factual, not padded
✓ No section is missing even with minimal input notes
```

### Step 4: Diagnose

**Failure Mode → Root Cause → Fix Mapping:**

| Failure Mode Observed | Root Cause | Targeted Fix |
|----------------------|-----------|-------------|
| Output is too generic | Insufficient context | Add industry + role + specific situation |
| Wrong format (paragraphs instead of table) | No format instruction | Add explicit format spec with columns |
| Response too long | No length constraint | Add word count or section count limit |
| Missing key information | Task not specific enough | List required elements explicitly |
| Inconsistent results across runs | Prompt is ambiguous | Add examples (few-shot) or more constraints |
| Hallucinated facts | Over-reliance on AI knowledge | Instruct to only use provided information |
| Wrong tone (too casual for context) | No tone specification | Add: audience + tone description |
| Off-topic tangents | Task scope not bounded | Add negative instructions: "Do not discuss..." |
| First sentence is a boring opener | No opener instruction | Add: "Begin directly with [the insight / the action / the number]" |
| AI adds unsolicited caveats | Safety defaults | Add: "Provide direct recommendations without excessive caveats" |
| Repetitive vocabulary | Word repetition | Add: "Vary your vocabulary — avoid repeating the same key words" |
| No specific examples | Generic reasoning | Add: "Support each point with a specific, realistic example" |

### Step 5: Refine

**Critical rule:** Change **one variable at a time**. If you change three things simultaneously and the output improves, you won't know which change caused the improvement.

**Optimization variables (in order of typical impact):**
1. Task clarity (the action verb and deliverable)
2. Context specificity (industry, role, situation)
3. Format specification (structure, length, sections)
4. Constraints (scope, exclusions, inclusions)
5. Examples (zero-shot → one-shot → few-shot)
6. Persona (role definition depth)
7. CoT trigger (for reasoning tasks)

---

## 10.3 Optimization Techniques

### Technique 1: Decomposition

Break a complex single prompt into a sequence of focused, manageable prompts.

**Why it works:** Each sub-prompt gets the model's full attention. Complex multi-part prompts cause the model to spread attention thin, producing shallow outputs across all components.

**Example — Business Plan Generation:**

```
❌ Monolithic (shallow results for each section):
"Write a complete business plan for a fintech startup including: executive
summary, market analysis, competitive landscape, product description,
go-to-market strategy, team overview, and financial projections."

✅ Decomposed (deep results for each section):

Prompt 1 — Market Foundation:
"Research and analyze the Indian fintech market for [specific niche].
Cover: market size (₹), growth rate (CAGR), key segments, 3 major trends,
3 key challenges, regulatory environment. Source-flag statistics.
~400 words. Research report format."

Prompt 2 — Competitive Landscape (uses Prompt 1 output):
"Based on this market analysis: [paste output]
Map the competitive landscape. Identify: top 5 direct competitors,
2 indirect competitors, market gaps our product can fill.
Table format: Competitor | Segment | Strengths | Weaknesses | Our Opportunity"

Prompt 3 — Product Description (uses prior context):
"Given this market context: [paste]
Write the product description section of our business plan.
Cover: what it does, who it's for, key differentiators, core features (table),
and how it addresses the market gaps identified."

[Continue for each section...]
```

**Decomposition decision rule:**
- More than 3 distinct deliverables → decompose
- Any section requires different expertise/tone → decompose
- Quality of each component is business-critical → decompose
- Task would exceed ~800 tokens of output → decompose

---

### Technique 2: Output Anchoring

Provide a partial template that the AI fills in. This gives precise control over structure while letting the AI handle content.

**Template anchoring:**
```
"Complete the following product description by filling in all [BRACKETED SECTIONS]:

[PRODUCT NAME] is built for [TARGET USER DESCRIPTION] who struggle with [SPECIFIC PAIN POINT].
Unlike [COMPETITOR APPROACH], we [UNIQUE DIFFERENTIATOR].

Key benefits:
• [BENEFIT 1 — outcome-focused, not feature-focused]
• [BENEFIT 2 — outcome-focused, not feature-focused]
• [BENEFIT 3 — outcome-focused, not feature-focused]

[SOCIAL PROOF OR TRUST SIGNAL — 1 sentence]

[CTA — specific, low-friction, 1 sentence]

Product details:
- Category: [CATEGORY]
- Price: ₹[PRICE]
- Available: [AVAILABILITY/SHIPPING]"
```

**Why output anchoring is powerful:**
- Forces the AI to follow your exact structure
- Prevents the AI from reordering sections based on its judgment
- Ensures every required element is included
- Makes quality checking fast — you know exactly what to look for

**JSON anchoring for technical tasks:**
```python
"""
Extract information from the following text and fill in this JSON template.
Use null for any field not mentioned in the text. Do not infer or guess.

Template to fill:
{
    "company_name": null,
    "founded_year": null,
    "headquarters": null,
    "industry": null,
    "employees": null,
    "revenue_usd_millions": null,
    "key_products": [],
    "notable_clients": [],
    "recent_news": null
}

Text to extract from:
[paste text here]
"""
```

---

### Technique 3: Negative Instructions

Tell the AI what NOT to do. This technique is underused and highly effective.

**Why negative instructions work:** LLMs have default tendencies trained into them — safe hedging language, repetitive openers, passive voice, generic examples. Negative instructions override these defaults.

**Most valuable negative instructions by category:**

**Openers:**
```
"Do not begin with: 'Certainly!', 'Great question!', 'Of course!', 'Absolutely!'"
"Do not start with a definition of the topic"
"Do not begin with the phrase 'In today's world'"
"Do not open with a rhetorical question"
```

**Content:**
```
"Do not use vague, generic examples — every example must be industry-specific"
"Do not include implementation steps — this is a strategy document only"
"Do not recommend actions that require more than a 5-person team to execute"
"Do not use statistics unless you are highly confident they are accurate"
```

**Style:**
```
"Do not use passive voice"
"Do not use hedging language ('might,' 'could potentially,' 'perhaps')"
"Do not use the same sentence structure consecutively"
"Do not use jargon without definition"
"Do not use bullet points that begin with the same word"
```

**Length:**
```
"Do not pad — if you have said everything necessary, stop"
"Do not repeat points from the introduction in the conclusion"
"Do not add a summary section unless explicitly requested"
```

**Combined negative instruction block:**
```
"DO NOT:
- Open with agreement/affirmation ('Great!', 'Certainly!')
- Use passive voice
- Include vague advice ('consider focusing on your strengths')
- Start more than 2 consecutive bullets with the same word
- Add a conclusion that repeats the introduction
- Use the phrase 'It is important to note that'"
```

---

### Technique 4: Self-Critique Prompting

Ask the AI to critique and improve its own response. This creates a mini iteration loop within a single interaction.

**Pattern 1 — Critique then rewrite:**
```
"Write [DELIVERABLE].
Then immediately critique your own output for:
- [Criterion 1]
- [Criterion 2]
- [Criterion 3]
Then rewrite it addressing your own critiques."
```

**Pattern 2 — Score then improve:**
```
"Write a cover letter for this job application: [details]

After writing it, score it on each dimension (1–10):
- Relevance to the specific role
- Specificity (uses their company name, role title, their stated needs)
- Impact (quantified achievements)
- Differentiation (why this candidate vs. others)
- Tone (confident but not arrogant)

Then rewrite the letter to score 9+ on every dimension."
```

**Pattern 3 — Find the weakest part:**
```
"After you generate this analysis, identify the single weakest paragraph —
the one with the least evidence, most assumptions, or loosest reasoning.
Then rewrite only that paragraph to meet the standard of the rest."
```

**Programmatic self-critique (for API users):**

```python
def generate_with_self_critique(prompt: str, model: str = "gpt-4o") -> dict:
    """
    Generate content, then have the model critique and improve it.
    Returns original, critique, and improved version.
    """
    from openai import OpenAI
    client = OpenAI()
    
    # Step 1: Generate initial response
    initial_response = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": prompt}],
        temperature=0.7
    ).choices[0].message.content
    
    # Step 2: Critique
    critique_prompt = f"""
    You just generated this response:
    
    ---
    {initial_response}
    ---
    
    Critique it on these dimensions (score 1-10 each, then explain):
    1. Accuracy and specificity
    2. Actionability (can the reader act on this?)
    3. Clarity (no jargon, clear structure)
    4. Completeness (nothing important missing)
    5. Conciseness (no padding)
    
    End with: "Weakest element: [identify the single weakest part]"
    """
    
    critique = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": critique_prompt}],
        temperature=0.3
    ).choices[0].message.content
    
    # Step 3: Improved version
    improve_prompt = f"""
    Based on your critique:
    {critique}
    
    Rewrite the original response addressing ALL identified weaknesses.
    Maintain the strengths. Improve every dimension that scored below 8.
    """
    
    improved = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": improve_prompt}],
        temperature=0.7
    ).choices[0].message.content
    
    return {
        "original": initial_response,
        "critique": critique,
        "improved": improved
    }
```

---

### Technique 5: Chain Prompting

Use the output of one prompt as the input to the next, building complexity progressively.

```
Chain Structure:
Prompt 1 → Output 1 ──┐
                       ▼
              Prompt 2 + Output 1 → Output 2 ──┐
                                                ▼
                                   Prompt 3 + Output 2 → Final Output
```

**Real Chain Example — Content Marketing Pipeline:**

```
Chain Goal: Produce a complete, SEO-optimized blog post with social promotions.

PROMPT 1 — Research & Outline:
"Research the topic 'AI tools for small business owners in India in 2024'.
Identify: 5 key pain points of the audience | Top 5 tools with their use cases |
2 compelling statistics | 3 expert perspectives (simulate based on available knowledge).
Produce a detailed 8-section blog outline with H2 and H3 headings."

OUTPUT 1: [Detailed outline with 8 sections]

PROMPT 2 — Draft Sections 1–4 (takes Output 1 as input):
"Using this outline: [paste Output 1]
Write the full content for Sections 1–4 only.
Target: 150–200 words per section. Professional but conversational tone.
Include the statistics in Section 2. Use subheadings from the outline."

OUTPUT 2: [Sections 1–4 drafted]

PROMPT 3 — Draft Sections 5–8 (continues the draft):
"The blog post so far: [paste Output 1 + Output 2]
Write Sections 5–8 maintaining the same tone and style.
150–200 words per section. End with a strong CTA paragraph."

OUTPUT 3: [Complete draft]

PROMPT 4 — SEO Optimization:
"Full draft: [paste complete draft]
Target keyword: 'AI tools for small business India'
Optimize for SEO: Ensure keyword appears in H1, first paragraph, 2 H2s, and conclusion.
Suggest a meta title (under 60 chars) and meta description (under 155 chars).
Add internal link placeholders: [LINK: relevant page title] at 2 appropriate points."

OUTPUT 4: [SEO-optimized post]

PROMPT 5 — Social Media Promotions:
"Blog post: [paste Output 4]
Create promotional content for:
- LinkedIn: 250-word thought leadership post with 3 key insights
- Twitter thread: 7 tweets, each under 280 characters
- Instagram caption: 150 words + 10 hashtags
Each must drive clicks to the blog post."
```

---

## 10.4 Measuring Prompt Quality — The Scoring Rubric

Build a custom scoring rubric for your most important recurring prompts.

**Generic rubric template:**

| Criterion | Weight | Score (1–5) | Weighted Score |
|-----------|--------|------------|---------------|
| Accuracy (facts and claims are correct) | 30% | ___ | ___ |
| Completeness (all required elements present) | 25% | ___ | ___ |
| Format adherence (matches specified structure) | 20% | ___ | ___ |
| Tone appropriateness | 15% | ___ | ___ |
| Conciseness (no padding) | 10% | ___ | ___ |
| **Weighted Total** | 100% | — | **___/5.0** |

**Score interpretation:**
- 4.5–5.0: Production-ready — use as-is
- 3.5–4.4: Good — minor editing needed
- 2.5–3.4: Needs work — iterate before use
- Below 2.5: Rebuild the prompt

---

## 10.5 Building a Professional Prompt Library

A prompt library is a curated, versioned collection of your best prompts — organized so you can find, reuse, and improve them over time.

### Prompt Library Entry Schema

```
═══════════════════════════════════════════════════════════════
PROMPT ID:         [e.g., HR-001, MKT-003, FINANCE-007]
CATEGORY:          [HR / Marketing / Finance / Operations / etc.]
NAME:              [Descriptive short name]
VERSION:           [1.0, 1.1, 2.0...]
DATE UPDATED:      [YYYY-MM-DD]
AUTHOR:            [Your name]
STATUS:            [Active / Under Test / Deprecated]
═══════════════════════════════════════════════════════════════

PURPOSE:
[One paragraph describing what this prompt is for, when to use it,
and what problem it solves]

TECHNIQUE USED:
[Zero-shot / Few-shot / CoT / Persona / Chain / Combination]

SUCCESS RATE:
[e.g., "Produces usable output in ~90% of runs"]

KNOWN LIMITATIONS:
[When does this prompt fail or need manual adjustment?]

INPUT VARIABLES:
[LIST EACH VARIABLE IN [BRACKETS] WITH DESCRIPTION AND EXAMPLE]
- [PROJECT_NAME]: Name of the project. Example: "Project Phoenix"
- [WEEK_NUMBER]: Current week of project. Example: "Week 7 of 12"
- [NOTES]: Your raw notes for the week. Paste bullet points or sentences.

THE PROMPT:
───────────────────────────────────────────────────────────────
[Your complete, ready-to-use prompt here]
───────────────────────────────────────────────────────────────

EXAMPLE INPUT:
[Example values for each variable]

EXAMPLE OUTPUT:
[Paste the best output you've gotten from this prompt]

ITERATION HISTORY:
v1.0 [date]: Initial version
v1.1 [date]: Added negative instruction to avoid clichés
v2.0 [date]: Switched to few-shot after inconsistent tone in zero-shot
═══════════════════════════════════════════════════════════════
```

### Prompt Library Categories to Build

Start your library by building one entry for each of these high-value categories:

```
TIER 1 — BUILD FIRST (Highest daily value):
□ Email writing (professional request, follow-up, apology)
□ Document summary (any document → executive brief)
□ Meeting minutes (raw notes → structured minutes)
□ Weekly status report
□ Data interpretation (table/data → narrative insight)

TIER 2 — BUILD SECOND (High weekly value):
□ Job description writer
□ Presentation outline generator
□ Competitive analysis brief
□ Performance review feedback
□ Customer response template

TIER 3 — BUILD WHEN NEEDED (Situational):
□ Business proposal sections
□ Policy document drafts
□ Training content outlines
□ Vendor evaluation framework
□ Risk assessment template
```

---

## 10.6 Common Optimization Issues — Full Diagnostic Table

| Problem | Symptom | Root Cause | Fix |
|---------|---------|-----------|-----|
| Generic output | "Could apply to any company" | No industry/role context | Add: specific industry, company size, role |
| Wrong format | Paragraphs when you wanted bullets | No format instruction | Add: exact format specification |
| Too long | 1,000 words when 300 was needed | No length constraint | Add: word count or section count limit |
| Missing elements | Key section always absent | Not listed in task | List ALL required elements explicitly |
| Inconsistent format | Different structure each run | Ambiguous prompt | Add few-shot examples or output anchor |
| Hallucinated data | Made-up statistics, fake citations | AI fills gaps with invention | Add: "Only use information I provide. Do not invent data." |
| Wrong tone | Casual when formal needed | No tone/audience spec | Add: audience + tone + style rules |
| Off-topic content | Unwanted tangents | Scope not bounded | Add negative: "Do not discuss X, Y, Z" |
| Flat language | Boring, repetitive word choice | No style guidance | Add: "Use varied, vivid vocabulary. Avoid repetition." |
| No examples | Generic claims | Not instructed | Add: "Support each point with a specific example." |
| Over-hedged | Every claim qualified excessively | Safety defaults | Add: "Give direct recommendations. Minimize qualifications." |
| Opener problem | Starts with "Certainly!" or "Great!" | LLM courtesy training | Add: "Begin directly with [the content]. No opener." |

---

## Module 2 Assessment

### Knowledge Check

1. What is the Prompt Optimization Cycle and why is it important to change one variable at a time during refinement?
2. Explain the difference between decomposition and chain prompting.
3. Give 3 examples of negative instructions that would improve a business writing prompt.
4. What is output anchoring and when is it preferable to a standard format instruction?
5. Describe the self-critique prompting pattern and when you would use it.
6. What should a prompt library entry contain to be useful across time and team members?
7. A prompt for generating customer emails produces great results 60% of the time but poor results 40% of the time. What does this inconsistency indicate and what optimization technique would help most?
8. Compare the following two approaches to a complex task: (a) one large prompt covering all aspects vs. (b) a chain of focused prompts. What are the trade-offs?

---

### Practical Assessment — Module 2 Capstone

**Scenario:** You are a Marketing Manager at an ed-tech startup (online upskilling for working professionals). You need to build a prompt library with 3 entries that automate your most time-consuming content tasks.

**Task:** Build 3 complete prompt library entries for:

1. **Course Launch Email** — An email to subscribers announcing a new course with a launch offer
2. **Student Testimonial Enhancement** — Transform a short, raw student quote into a compelling 100-word testimonial
3. **LinkedIn Thought Leadership Post** — A post that uses a course insight to build the brand's thought leadership

**Each entry must include:**
- Full CRAFT-structured prompt with variables in [BRACKETS]
- Technique used (zero-shot, few-shot, CoT, persona, or combination)
- 3 targeted constraints
- Example input and expected output
- Iteration history (at least Version 1.0 and 1.1 — document one improvement you made)

**Scoring:**

| Criterion | Points |
|-----------|--------|
| All 3 prompts use appropriate techniques | 20 |
| CRAFT structure clearly applied | 15 |
| Variables are clearly marked and reusable | 15 |
| Output quality — are they production-ready? | 25 |
| Iteration documented with improvement rationale | 15 |
| Library format is complete and professional | 10 |
| **Total** | **100** |

---

## Module 2 Summary

| Session | Technique | The One Sentence |
|---------|-----------|-----------------|
| **Session 6** | Zero-Shot | Use when the task is standard and well-defined — instruction clarity is everything. |
| **Session 7** | Few-Shot | When you need custom formats, brand voice, or nuanced classification — show, don't just tell. |
| **Session 8** | Chain-of-Thought | For complex reasoning, math, and multi-step decisions — make the AI show its work. |
| **Session 9** | Persona | Stacked personas activate domain expertise and shape communication style with precision. |
| **Session 10** | Optimization | Test, diagnose, fix one variable at a time, document — treat prompts like professional assets. |

---

## Module 2 Technique Selection Guide

```
WHAT IS YOUR TASK?
        │
        ├─► Standard task (classify, summarize, translate, extract)
        │   └─► ZERO-SHOT: Focus on instruction clarity
        │
        ├─► Need a specific custom format or style
        │   └─► FEW-SHOT: Provide 2–5 examples
        │
        ├─► Complex reasoning, math, multi-factor decision
        │   └─► CHAIN-OF-THOUGHT: Add reasoning triggers
        │
        ├─► Need domain expertise or specific perspective
        │   └─► PERSONA PROMPTING: Stack role attributes
        │
        ├─► Inconsistent results across runs
        │   └─► OPTIMIZATION: Few-shot + output anchoring + constraints
        │
        ├─► Complex multi-part deliverable
        │   └─► DECOMPOSITION + CHAIN PROMPTING
        │
        └─► Quality is critical and output must be verified
            └─► SELF-CRITIQUE + HUMAN REVIEW
```

---

*Module 2 Complete → Proceed to Module 3: Academic & Professional Applications (Session 11)*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
