# Session 4: Prompt Best Practices — Writing Prompts That Work
## Module 1 — Foundations of Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 4 OF 30  │  Module 1, Session 4                           │
│  Topic: Prompt Best Practices — 10 Principles for Professional Use  │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Apply 10 proven best practices to any prompt you write
2. Distinguish between strong and weak prompts across multiple task types
3. Use iterative prompting to refine AI outputs through follow-up
4. Apply constraint-based prompting to improve precision
5. Verify AI outputs critically using a structured evaluation checklist
6. Identify and fix the most common prompting mistakes professionals make

---

## 4.1 Why Best Practices Matter

Knowing the five components of a prompt (Session 3) is necessary — but not sufficient. Best practices are the professional-level habits that separate prompt engineers who consistently get great results from those who get inconsistent, mediocre ones.

Think of it like cooking: knowing the ingredients (components) is different from knowing how to cook (best practices). Both are needed.

---

## Best Practice 1: Be Specific and Clear

**The Rule:** Every word of ambiguity in your prompt becomes a decision the AI makes on your behalf — often not the decision you wanted.

**The Test:** Read your prompt and ask: *"Could this instruction be interpreted in two different ways?"* If yes, make it more specific.

**Weak vs. Strong Examples:**

| Weak | Strong | What changed |
|------|-------|-------------|
| "Write a cover letter" | "Write a cover letter for a Senior Product Manager role at a B2B SaaS startup, from a candidate with 6 years of PM experience in e-commerce" | Who, what role, what background |
| "Explain machine learning" | "Explain machine learning in plain English to a non-technical HR director who needs to evaluate AI vendors" | Audience + purpose + depth level |
| "Give me ideas" | "Give me 10 low-cost (under ₹5,000/each) team-building activity ideas for a remote team of 12 people spread across India, that can be done virtually over 90 minutes" | Count + budget + context + format + constraint |
| "Make this better" | "Improve the clarity and professional tone of this email. Remove passive voice. Shorten it to under 120 words. Keep the core message intact." | Specific improvements + length + preservation rule |

**The specificity checklist:**
```
Before submitting, ask:
□ Who is the audience?
□ What is the exact output I need?
□ What scope/topic constraints apply?
□ What format do I want the output in?
□ What length is appropriate?
□ What tone/style is needed?
□ What should NOT be included?
```

---

## Best Practice 2: Use Strong Action Verbs

**The Rule:** Your task instruction must start with a verb that unambiguously describes what you want the AI to do.

**The Problem:** Vague openers like "Can you...", "Help me...", "Talk about...", "Do something with..." do not tell the AI what kind of response to generate.

**Master Action Verb Reference:**

```
DOCUMENT GENERATION:
Write      → Produce complete text from scratch
Draft      → Create a first version (implies editing to follow)
Compose    → Write in a considered, structured way
Generate   → Produce multiple items or options
Produce    → Create a complete, usable output

ANALYSIS:
Analyze    → Break down into components and examine each
Evaluate   → Assess quality, merit, or suitability
Critique   → Identify weaknesses and areas for improvement
Audit      → Systematically check against criteria
Assess     → Determine value, risk, or fit

TRANSFORMATION:
Rewrite    → Change the way something is expressed
Translate  → Convert between languages or styles
Simplify   → Reduce complexity
Expand     → Add depth and detail to existing content
Condense   → Reduce length while preserving meaning
Convert    → Change format or structure

INFORMATION:
Summarize  → Distill to key points
Extract    → Pull specific information from text
Identify   → Find and name specific elements
List       → Enumerate items
Find       → Locate specific information within given text

REASONING:
Compare    → Show similarities and differences systematically
Contrast   → Highlight differences specifically
Recommend  → Advise on the best option with reasoning
Argue      → Make a case for a position
Predict    → Forecast likely outcomes with justification

ORGANIZATION:
Outline    → Create hierarchical structure
Prioritize → Rank by importance with reasoning
Categorize → Group items by type or criteria
Map        → Show relationships between elements
```

**Example — Same task, different verbs:**

```
"Discuss remote work."          → Vague, AI decides what to discuss
"Summarize remote work trends." → Concise overview of key trends
"Analyze remote work impacts."  → Structured breakdown of effects
"Compare remote vs. on-site."   → Head-to-head comparison
"Argue for remote work."        → Persuasive one-sided case
"Critique remote work policies."→ Identifies weaknesses in policies
```

Each verb produces a fundamentally different type of output from the same topic.

---

## Best Practice 3: Specify Output Format Explicitly

**The Rule:** Never leave format to chance. Always tell the AI the exact structure you want.

**Why the AI defaults to paragraphs:** Without format instructions, LLMs default to continuous prose — the format most common in their training data. This is rarely the most useful format for professional tasks.

**Format specification patterns:**

```
TABLES:
"Present as a table with columns: [Col1] | [Col2] | [Col3] | [Col4]"
"Format as a comparison matrix. Rows: [items]. Columns: [criteria]."

LISTS:
"List as 5 numbered items"
"Use bullet points, one per line, starting with a bold key term"
"Format as a numbered list. Each item: bold title, then 2-sentence explanation"

DOCUMENTS:
"Structure as: Executive Summary (100 words) | Key Findings (5 bullets) |
Recommendations (3 numbered points) | Next Steps (deadline + owner)"

EMAILS:
"Email format: Subject line | Greeting | 3 paragraphs | Closing | Signature"

SLIDE OUTLINES:
"For each slide: Slide # | Title | 3 bullet points | Speaker note (1 sentence)"

JSON:
"Return ONLY valid JSON. Schema: {'field1': type, 'field2': type, ...}"

CODE:
"Write as a Python function with:
 - Docstring explaining purpose, parameters, and return value
 - Input validation
 - Inline comments for complex logic
 - Example usage in the docstring"
```

**Powerful format for professional reports:**

```
"Structure this report as follows:
1. Executive Summary (3 sentences — problem, finding, recommendation)
2. Background (1 paragraph — context and why this matters)
3. Key Findings (3–5 bullet points, each starting with a bold insight)
4. Analysis (2–3 paragraphs — explanation and evidence)
5. Recommendations (numbered list — specific and actionable)
6. Next Steps (table: Action | Owner | Deadline | Success Metric)"
```

---

## Best Practice 4: Specify Tone and Audience

**The Rule:** The same information must be communicated differently for different audiences. Always specify who you are writing for and what tone to use.

**Tone vocabulary:**

| Tone | When to Use | Key Characteristics |
|------|------------|-------------------|
| **Formal/Professional** | Business reports, legal, executive comms | Precise, impersonal, structured |
| **Conversational** | Blog posts, social media, newsletters | Informal, direct, "you" language |
| **Authoritative** | Expert opinions, guidance, instruction | Confident, fact-based, decisive |
| **Empathetic** | Customer service, HR, sensitive topics | Warm, validating, supportive |
| **Persuasive** | Sales copy, proposals, pitches | Benefit-led, action-oriented |
| **Educational** | Training content, explainers | Clear, layered, example-rich |
| **Urgent** | Crisis comms, alerts, deadlines | Direct, short sentences, action-first |
| **Inspiring** | Leadership speeches, campaigns | Emotional, vivid, motivational |

**Audience-tone matching examples:**

```
SAME MESSAGE: "We need to reduce the software development team's headcount by 20%"

To the Board (formal, data-driven):
"Present the business case for a 20% reduction in software development headcount,
including cost savings, productivity impacts, and risk mitigation strategies."

To HR Manager (collaborative, process-focused):
"Draft guidelines for HR on how to handle the restructuring process for a 20%
team reduction, focusing on legal compliance, employee communication, and timeline."

To Affected Team (empathetic, transparent):
"Write a team communication about a planned 20% headcount reduction, acknowledging
the difficulty, explaining the business reason clearly, and outlining what
support will be provided to affected employees."
```

---

## Best Practice 5: Use Constraints Strategically

**The Rule:** Constraints are not restrictions — they are precision tools that dramatically improve output quality by narrowing the solution space.

**Counter-intuitive truth:** A tighter prompt almost always produces better output than a loose one, because the AI has less room to make poor decisions.

**Constraint types and their effects:**

**Word/length constraints:**
```
"In exactly 3 sentences"     → Forces concision and prioritization
"Between 250–300 words"      → Specific target prevents padding or cutting short
"Under 50 words"             → Tests what truly matters (excellent for headlines/summaries)
```

**Scope constraints:**
```
"Only consider options available in India"
"Focus exclusively on the marketing implications, not technical"
"Limit analysis to the period 2020–2024"
"Only include factors that can be influenced by our team"
```

**Negative / exclusion constraints:**
```
"Do not use the phrase 'It is important to note'"
"Avoid generic advice — every point must be specific to retail banking"
"Do not begin any bullet with 'The'"
"No platitudes or motivational language"
"Do not recommend tools that cost more than ₹10,000/month"
```

**Inclusion requirements:**
```
"Include at least one statistic per point (use [STATISTIC NEEDED] if you don't have one)"
"Each recommendation must include: rationale + risk + expected outcome"
"Include a real company example for each strategy"
```

**Quality constraints:**
```
"Avoid clichés"
"Use active voice throughout"
"All sentences under 20 words"
"Avoid starting consecutive sentences with the same word"
```

---

## Best Practice 6: Provide Examples When Needed (Preview of Few-Shot)

**The Rule:** When you need a specific format, style, or output type that's hard to describe in words — show it.

**The principle:** One good example is worth 100 words of description.

**Example — Writing in a specific style:**
```
"Write product descriptions in this style:

EXAMPLE: 'The Kinetic Pro Desk Chair isn't just furniture — it's where your
best thinking happens. Lumbar support that adapts to you. Breathable mesh
that keeps you cool. An armrest that meets your elbow, not the other way around.
For the 8 hours you actually work.'

Now write a similar description for: A standing desk converter for home offices
that adjusts from sitting to standing in 3 seconds."
```

**Example — Custom classification:**
```
"Classify each support ticket by urgency and category.

Example:
Ticket: 'App keeps crashing when I try to upload files. Losing work!'
Classification: URGENCY: High | CATEGORY: Bug | ACTION: Escalate to Engineering

Ticket: 'How do I change my notification settings?'
Classification: URGENCY: Low | CATEGORY: Feature Question | ACTION: Send Help Article

Now classify these:
Ticket 1: 'I was charged twice for last month. This is unacceptable.'
Ticket 2: 'Love the new dashboard design!'
Ticket 3: 'Cannot log in since the update yesterday. Team of 10 blocked.'"
```

---

## Best Practice 7: Iterative Prompting — Treat It as a Conversation

**The Rule:** Never expect the first response to be final. Great AI outputs are the result of guided iteration.

**The Iteration Mindset:**

```
TRADITIONAL MINDSET:      ONE PROMPT → ONE FINAL OUTPUT
PROFESSIONAL MINDSET:     INITIAL PROMPT → EVALUATE → REFINE → EVALUATE → REFINE
```

**Structured iteration workflow:**

```
ROUND 1: Write your initial structured prompt
         ↓
         Evaluate response:
         ✓ What is good? (keep)
         ✗ What is wrong? (fix)
         ? What is missing? (add)
         ↓
ROUND 2: Follow-up prompt addressing specific issues:
         "The structure is good. Now:
          - Shorten the introduction to 2 sentences
          - Add a specific Indian retail example to point 3
          - Make the tone more confident — remove hedging phrases
          - Add a table for the comparison in section 4"
         ↓
ROUND 3: Final refinement prompt:
         "Almost perfect. Final changes:
          - Change 'It should be noted that' to direct statements
          - The conclusion needs a stronger call to action
          - Standardize the formatting so all bullet points match"
```

**Iteration command vocabulary:**

```
SHORTEN:    "Reduce the [section] to [length]. Keep only essential points."
EXPAND:     "Expand [section/point] with more detail and a specific example."
REFORMAT:   "Convert [paragraphs] into [bullet points / table / numbered list]."
ADJUST TONE: "Rewrite in a [warmer/more formal/less jargon-heavy] tone."
ADD:        "Add [a statistic/an example/a caveat/a section on X] after [location]."
REMOVE:     "Remove [repetitions/clichés/the second paragraph/jargon]."
REORDER:    "Move [point X] before [point Y] — it's more logical that way."
REPLACE:    "Replace [phrase/section] with [alternative approach/better example]."
STRENGTHEN: "The [recommendation/argument/conclusion] is weak — make it more specific."
```

**Real iteration example:**

```
INITIAL PROMPT:
"Write a LinkedIn post about the importance of data literacy in business."

ROUND 1 OUTPUT: A generic 300-word post with no hook and vague points.

ROUND 2 ITERATION:
"Good structure. Now improve it:
 - Start with a specific, counterintuitive statistic as the hook
 - Replace the generic points with 3 concrete business scenarios
 - Add a provocative question at the end to drive comments
 - Shorten to 200 words maximum
 - This is for a technology consulting audience, not general"

ROUND 3 ITERATION:
"Much better. Two final changes:
 - The opening statistic needs a source year (add '2024' if recent)
 - The closing question should mention AI specifically — that's what this
   audience cares about most"
```

---

## Best Practice 8: Break Complex Tasks into Steps

**The Rule:** One complex multi-part prompt almost always produces worse results than several focused single-task prompts.

**Why:** When given many tasks simultaneously, the AI often:
- Gives less depth to each
- Misses some tasks entirely
- Produces rushed or generic sub-sections
- Loses track of the overall goal

**The Sequential Decomposition Pattern:**

```
❌ MONOLITHIC PROMPT:
"Analyze my startup idea, write a full business plan, create 3-year
financial projections, develop a go-to-market strategy, and suggest
what team I should hire first."

✅ DECOMPOSED WORKFLOW:

Step 1: "Analyze this startup idea for market fit, competitive advantage,
and key risks. Be brutally honest. [Idea description]"

Step 2: "Using this analysis [paste], create a business plan outline
with section summaries. Focus on sections investors care about most."

Step 3: "Based on the market analysis [paste], create 3-year financial
projections as a table: Year | Revenue | Costs | EBITDA | Key Assumptions"

Step 4: "Given the business plan [paste], develop a go-to-market strategy
for Year 1. Focus on the first 90 days — what to do, in what order."

Step 5: "For the GTM strategy [paste], recommend the first 3 hires.
For each: Role | Why first | Ideal background | Approximate CTC"
```

**When to decompose:**
- Task has more than 3 distinct deliverables
- Different sections require different expertise or tone
- Quality of each component is critical
- The full output would exceed 1,000 tokens

---

## Best Practice 9: Verify and Validate All AI Outputs

**The Rule:** AI outputs are first drafts, not final facts. Every professional must apply a verification layer before acting on or sharing AI-generated content.

**The Verification Hierarchy:**

```
TIER 1 — ALWAYS VERIFY (Never trust AI alone):
• Specific statistics and numbers
• Named citations and references
• Medical, legal, financial advice
• Current events and recent developments
• Claims about specific companies or people

TIER 2 — OFTEN VERIFY (Check if accuracy matters):
• Technical procedures and instructions
• Industry regulations and compliance
• Specific dates and timelines
• Claims about software/tools (may be outdated)

TIER 3 — SPOT CHECK (Verify a sample):
• Writing style and tone consistency
• Logical flow and structure
• Completeness relative to your brief

TIER 4 — AI JUDGMENT TRUSTED (Generally fine):
• Creative and stylistic choices
• Structural suggestions
• Brainstorming and idea generation
```

**Verification prompts — asking AI to check itself:**

```
"Review the response you just gave. Flag any claims that:
 - You are less than 90% confident are accurate
 - Involve specific statistics or numbers
 - Relate to events after your training cutoff
 - Would benefit from citing a primary source
Mark each flag with [VERIFY]."
```

```
"List any factual claims in your previous response where someone
should independently verify accuracy before using this professionally."
```

**The Professional Standard:** Before sending any AI-assisted document to a client, manager, or external stakeholder, every factual claim should be verified and every calculation independently checked.

---

## Best Practice 10: Build Reusable Prompt Templates

**The Rule:** If you write the same type of prompt more than twice, build a template. A prompt library is a professional asset.

**Anatomy of a reusable template:**

```
TEMPLATE NAME: Weekly Status Report
USE CASE: Every Monday morning status update to my manager
VARIABLES: [PROJECT_NAME], [WEEK_NUMBER], [TEAM_NAME]

PROMPT:
─────────────────────────────────────────────────────────────
You are a project manager writing a crisp, professional status report.

Project: [PROJECT_NAME] | Week: [WEEK_NUMBER] | Team: [TEAM_NAME]

Based on the following notes from this week:
[PASTE YOUR NOTES HERE]

Write a weekly status report in this format:
1. HEADLINE STATUS: One sentence — on track / at risk / blocked
2. COMPLETED THIS WEEK: 3–5 bullet points (specific, measurable outcomes)
3. IN PROGRESS: Current work with % completion where possible
4. BLOCKERS: Issues needing manager action (or "None")
5. NEXT WEEK: Priority actions (3–5 bullets)
6. METRICS: [any KPIs relevant to this project]

Constraints:
- Under 300 words total
- Every completed item should state the outcome, not just the activity
- Blockers section: state the blocker AND the help needed
- Tone: professional, concise, factual — no padding
─────────────────────────────────────────────────────────────
SUCCESS RATE: Tested ✓ | Works with: ChatGPT, Claude, Gemini
NOTES: Works best when you paste raw notes — even bullet points or
       incomplete sentences work fine as input
```

**Template library categories to build:**

```
COMMUNICATION TEMPLATES:
□ Professional email (request / follow-up / apology / announcement)
□ Meeting invitation with agenda
□ Performance feedback (positive / constructive)
□ Client proposal summary

ANALYSIS TEMPLATES:
□ SWOT analysis
□ Competitor comparison table
□ Data interpretation summary
□ Root cause analysis

CONTENT TEMPLATES:
□ LinkedIn post (thought leadership)
□ Blog post outline + introduction
□ Newsletter section
□ Training module outline

PROFESSIONAL TEMPLATES:
□ Job description
□ Meeting minutes
□ Project status report
□ Lesson learned / retrospective
```

---

## 4.2 The 10 Most Common Prompting Mistakes

| Mistake | Example | Fix |
|---------|---------|-----|
| **1. Too vague** | "Help me write something about AI" | Specify type, audience, length, purpose |
| **2. No format** | Forgetting to specify structure | Always add format to every prompt |
| **3. Multiple tasks** | "Write, translate, and summarize this" | One task per prompt |
| **4. No context** | "Write a business proposal" | Add: who it's for, what product, what goal |
| **5. Trusting everything** | Using AI stats without checking | Verify Tier 1 claims always |
| **6. Never iterating** | Accepting first output as final | Always iterate at least once |
| **7. No length control** | Getting 2,000 words when you need 200 | Specify word count explicitly |
| **8. Wrong tone default** | Getting formal when you need casual | Always specify tone + audience |
| **9. Pasting confidential data** | Sending client PII to ChatGPT | Anonymize or use enterprise tools |
| **10. Not saving good prompts** | Rebuilding the same prompt weekly | Build and maintain a prompt library |

---

## Hands-On Activities — Session 4

---

### Activity 4.1 — Best Practice Application Challenge

Start with this weak prompt:
```
"Help me write an email."
```

Apply each best practice one at a time, observing how the response improves at each step:

**Round 1 — Add specificity:**
```
"Write a professional email to a client requesting a 1-week extension
on our project deadline."
```
→ Observe: Better, but missing context and format.

**Round 2 — Add role + context:**
```
"You are a project manager at an IT consulting firm. Our client is
a healthcare company. We need 1 more week on a data dashboard project.
Write the extension request email."
```

**Round 3 — Add format + constraints:**
```
"You are a project manager at an IT consulting firm. Our client is a
healthcare company (formal culture). We need 1 more week on a data
dashboard project due to API integration complexity.
Write the extension request email.
Format: Subject line + 3 paragraphs (situation, impact of rushing,
proposed new date) + professional closing.
Constraints: Under 150 words. Frame it as a quality decision, not an
excuse. Do not use passive voice. The new proposed date: December 21st."
```

**Document each output:** Paste Round 1, 2, and 3 outputs side by side. Write a 3-sentence reflection on how the output changed at each step.

---

### Activity 4.2 — Iterative Refinement Practice

**Starting prompt:**
```
"Explain the importance of data privacy to a non-technical business audience."
```

**Step 1:** Run the prompt. Evaluate it against these criteria:
- Is there a compelling opening hook? (Yes/No)
- Are there specific real-world examples? (Yes/No)
- Is the length appropriate for a busy executive? (Yes/No)
- Is there a clear "so what" for their business? (Yes/No)

**Step 2:** Write an iteration prompt addressing every "No" above:
```
"Good start. Now improve:
 - [Add iteration instructions based on your evaluation]"
```

**Step 3:** Run one more iteration to polish.

**Deliverable:** Submit 3 prompt versions + 3 responses + a reflection on what changed.

---

### Activity 4.3 — Build Your First Template

Think of a writing task you do repeatedly (weekly report, team update, client email, meeting agenda, etc.).

Build a complete reusable template for it:
```
TEMPLATE NAME: _______________________
USE CASE: ____________________________
VARIABLES (in [BRACKETS]): ___________

FULL PROMPT:
[Write your complete template here]

TEST: Run it with real data. Does it produce a usable output on the first run?
SUCCESS? Yes / No. If No: what needs to change?
```

---

### Activity 4.4 — Verification Exercise

Generate this content with AI:
```
"Give me 5 compelling statistics about the impact of AI on workplace
productivity, with the source and year for each."
```

Then:
1. Try to independently verify each statistic using Google or a reputable source
2. Mark each as: ✅ Verified | ⚠️ Approximate | ❌ Cannot verify/Incorrect
3. Write a 3-sentence reflection on what this exercise reveals about trusting AI-generated statistics in professional documents

---

## Revision Questions — Session 4

1. Why is specificity the most important single best practice in prompt engineering?
2. What is the difference between using "help me with" vs. using a specific action verb like "analyze"?
3. Why do constraints improve rather than limit AI output quality?
4. Describe the iterative prompting workflow in 4 steps.
5. Name 5 types of AI outputs that must always be independently verified before professional use.
6. Why is it a best practice to break complex tasks into multiple focused prompts?
7. What makes a prompt reusable as a template? What elements must it contain?
8. A colleague says "I just ask AI to tell me if it's confident in its own answer." Why is this not sufficient verification? What should they do instead?

---

## Key Takeaways — Session 4

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 4 KEY TAKEAWAYS — 10 BEST PRACTICES                        │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  1. Specificity   — Eliminate every ambiguity before submitting     │
│  2. Action verbs  — Tell AI exactly WHAT to do, not "help me"       │
│  3. Format        — Always specify the output structure             │
│  4. Tone/Audience — Match communication style to the reader         │
│  5. Constraints   — Rules improve quality by narrowing scope        │
│  6. Examples      — Show, don't just tell (preview of few-shot)     │
│  7. Iterate       — First output is a draft, not a final product    │
│  8. Decompose     — One task per prompt for complex work            │
│  9. Verify        — Always check facts, stats, citations            │
│ 10. Templates     — Reuse what works; build a prompt library        │
│                                                                      │
│  Top mistake to avoid: accepting the first AI output as final       │
│  Professional habit: always run at least one iteration              │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 4 Complete → Proceed to Session 5: The CRAFT Framework*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
