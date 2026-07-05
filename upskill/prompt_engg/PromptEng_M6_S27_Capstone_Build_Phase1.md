# Session 27: Capstone Build Phase 1 — Foundation Prompts & Core Pipeline
## Module 6 — Capstone Project & Certification
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 27 OF 30  │  Module 6, Session 2                          │
│  Topic: Capstone Build Phase 1 — Core Prompts & Pipeline Design     │
│  Duration: 90–120 minutes (extended build session)                  │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Build the first 5 prompt library entries for your capstone project
2. Design and test your core multi-step pipeline
3. Establish baseline measurements for your chosen metrics
4. Apply quality gate evaluation to your first outputs
5. Use iteration discipline to move from v1.0 to v1.1+ on your core prompts
6. Identify and resolve the first round of prompt failures

---

## 27.1 The Build Phase Mindset

Session 27 is where the capstone moves from planning to production. The mindset shift required:

```
FROM PLANNING MODE:              TO BUILD MODE:
─────────────────────────────    ────────────────────────────────────────
Thinking about what to build     Actually building
Designing the ideal solution     Shipping a working v1.0
Avoiding the first failure       Expecting the first failure — and learning
Waiting for clarity              Starting with the best available information
Optimizing before testing        Testing before optimizing

BUILD MANTRA: "Make it work, then make it better."
A tested v1.0 that works 70% of the time is more valuable
than a perfect design that hasn't been tested at all.
```

---

## 27.2 Baseline Measurement — Before You Build

Before writing a single prompt, establish your baseline measurements. You cannot prove impact without a "before" state.

### Baseline Data Collection Prompt

```
Help me establish measurable baseline metrics for my capstone project.

My project: [DESCRIBE YOUR CAPSTONE — what problem, what solution]
Tasks I will be improving with AI:
[LIST EACH TASK YOU PLAN TO IMPROVE]

For each task, help me design a baseline measurement:
1. TASK NAME: [Specific task]
   Current approach: How do I do this now? (manually, with what tools?)
   Time measurement: How long does it currently take? (per instance)
   Quality measurement: How do I currently rate the quality? (1–5 scale or %)
   Frequency: How often do I do this? (per day/week/month)
   Total current time cost: [time per instance × frequency = weekly hours]

2. TASK NAME: [...]
   [Repeat for each task]

BASELINE SUMMARY TABLE:
| Task | Time Per Run (now) | Quality (now) | Frequency | Weekly Hours |
[Generate this table from the task data above]

TOTAL BASELINE: [Sum of weekly hours spent on all tasks identified]

For each task, also identify:
- What would a "high quality" output look like? (Define the standard)
- What would a "low quality" output look like? (Define the floor)
This will be used for the After comparison in Session 28.
```

---

## 27.3 The First 5 Prompts — Build Standards

### Prompt Build Sequence

For a systematic capstone, build prompts in this priority sequence:

```
PRIORITY ORDER FOR FIRST 5 PROMPTS:

1. CORE TASK PROMPT — The single most important, highest-frequency task
   (This prompt alone should deliver most of your time savings)

2. PIPELINE STEP 1 — The first step of your core multi-step pipeline
   (Build incrementally — get step 1 working before building step 2)

3. PIPELINE STEP 2 — The second step of your core pipeline

4. SUPPORTING TASK PROMPT — Second most important task prompt

5. QUALITY EVALUATION PROMPT — The rubric/critique prompt for your domain
   (You need this to evaluate everything else you build)
```

### Build Protocol for Each Prompt

For every prompt you build in the capstone, follow this 5-step protocol:

```
STEP 1 — DESIGN (5 minutes)
Answer these questions BEFORE writing:
- What technique am I using? (Zero-shot / Few-shot / CoT / Persona / Chain)
- What framework? (CRAFT / ReAct / ToT / RAG / Skeleton)
- What is the exact output format I need?
- What are the top 3 failure modes to guard against?

STEP 2 — WRITE v1.0 (10 minutes)
Write the complete prompt using the full template.
Include all CRAFT elements: Role, Context, Task, Format, Tone, Constraints.

STEP 3 — TEST v1.0 (10 minutes)
Run the prompt on 3 different inputs:
- A typical/expected input
- A complex or edge-case input
- A minimal/sparse input (least information)
Score each output: 1–5 on your quality rubric.

STEP 4 — DIAGNOSE AND ITERATE (10 minutes)
Identify the single most important failure mode from your 3 tests.
Make ONE change to address it. Document what changed and why.
This is v1.1.

STEP 5 — DOCUMENT (10 minutes)
Complete the full library entry standard.
Include the best output example from your tests.
Record your iteration history: v1.0 → v1.1 with the specific change.
```

---

## 27.4 Core Pipeline Design and Testing

### The Pipeline Design Document

Before coding or prompting the pipeline, write this design document:

```
PIPELINE DESIGN DOCUMENT

PIPELINE NAME: [Descriptive name]
PIPELINE PURPOSE: [What problem does this pipeline solve end-to-end?]
INPUT: [What does the user/system provide at the start?]
OUTPUT: [What is the final deliverable?]

STEP MAP:
───────────────────────────────────────────────────────────────────
Step # | Name | Input | Prompt Technique | Output | Quality Gate?
───────────────────────────────────────────────────────────────────
1      | [Name] | [What enters this step] | [Technique] | [Output type] | YES/NO
2      | [Name] | [Step 1 output + ?] | [Technique] | [Output type] | YES/NO
3      | [Name] | [Step 2 output + ?] | [Technique] | [Output type] | YES/NO
4      | [Name] | [Step 3 output + ?] | [Technique] | [Output type] | YES/NO

QUALITY GATES:
After Step [N]: Check for [specific criteria — binary pass/fail]
If FAIL: [specific corrective action]

CONTEXT BRIEF (carried at every step):
[What information will you include at the top of every step prompt?]

FAILURE MODES TO DESIGN AGAINST:
[List 3 things that most commonly break this type of pipeline]

ESTIMATED TIME SAVINGS vs. MANUAL:
[Time per run manually] → [Time per run with pipeline] = [Savings per run]
At [frequency], this saves [X hours per week/month]
```

---

## 27.5 Pipeline Step Templates by Capstone Track

### Track A — AI Productivity System Pipeline Example

**Pipeline: Weekly Review and Forward Planning**

```
STEP 1 — WEEKLY CAPTURE
Prompt: "Process my raw week-end notes into structured categories.
Input: [paste notes]
Output: COMPLETED | CREATED ACTIONS | DECISIONS MADE | WAITING FOR | INSIGHTS"

STEP 2 — ACCOMPLISHMENT SYNTHESIS
Input: [Step 1 COMPLETED section]
Prompt: "Convert these completed items into 3–5 professional achievement
bullets suitable for a weekly status report. Focus on outcomes, not activities."

STEP 3 — NEXT WEEK PLANNING
Input: [Step 1 CREATED ACTIONS + any carry-forward]
Prompt: "Prioritize this action list for next week using these criteria:
[your specific criteria]. Output a ranked daily plan with time estimates."

STEP 4 — STAKEHOLDER UPDATE
Input: [Step 2 achievements + Step 3 top priorities]
Prompt: "Draft my weekly stakeholder update email:
- 3 achievements this week
- 3 priorities for next week
- 1 item needing stakeholder input or decision
Under 200 words. Professional but conversational tone."
```

---

### Track B — Business Function Pipeline Example

**Pipeline: Customer Insight to Action Report**

```
STEP 1 — RAW FEEDBACK PROCESSING
Input: [Customer feedback, NPS comments, support tickets]
Prompt: "Categorize and quantify themes in this customer feedback.
Output: Theme | Frequency | Sentiment | Representative Quote | Urgency"

STEP 2 — INSIGHT EXTRACTION
Input: [Step 1 theme table]
Prompt: "Identify the 3 most actionable insights from this feedback analysis.
For each: insight | evidence | business impact | root cause hypothesis"

STEP 3 — RECOMMENDATION GENERATION
Input: [Step 2 insights]
Prompt: "Generate specific, implementable recommendations for each insight.
Format: Recommendation | Owner (function) | Effort | Impact | Timeline"

STEP 4 — EXECUTIVE BRIEF
Input: [Step 1–3 outputs]
Prompt: "Write an executive customer insight brief:
HEADLINE: Most important finding in 1 sentence
INSIGHTS: 3 findings with evidence
RECOMMENDATIONS: Top 3 actions
METRICS TO WATCH: 2 leading indicators
Under 300 words. Board-ready language."
```

---

### Track C — Content System Pipeline Example

**Pipeline: Idea to Multi-Platform Content**

```
STEP 1 — IDEA VALIDATION AND ANGLE
Input: [Content idea / topic]
Prompt: "Evaluate this content idea for my audience [DESCRIBE].
Output: Best angle | Hook options (3) | Platform fit | GO/REFINE/DISCARD"

STEP 2 — CORNERSTONE CONTENT DRAFT
Input: [Validated angle + best hook]
Prompt: "Write a 1,000-word blog post with SEO structure.
Keyword: [keyword]. Audience: [describe]. [Full blog post prompt]"

STEP 3 — REPURPOSING PACKAGE
Input: [Step 2 blog post]
Prompt: "Repurpose this into:
- LinkedIn post (250 words)
- Twitter thread (8 tweets)
- Email newsletter section (150 words)
- Instagram carousel (10 slides — title + 2 lines each)"

STEP 4 — PERFORMANCE PREDICTION AND CTA OPTIMIZATION
Input: [All Step 3 content]
Prompt: "For each platform version:
- Suggest the A/B variant for the opening hook
- Recommend optimal CTA
- Identify the highest-risk quality issue in this piece"
```

---

### Track D — Learning System Pipeline Example

**Pipeline: Topic to Complete Lesson**

```
STEP 1 — LEARNING OBJECTIVE DESIGN
Input: [Topic / concept to teach]
Prompt: "Design learning objectives for a 60-minute lesson on [topic].
Audience: [describe]. Format: 3–5 objectives using Bloom's taxonomy verbs."

STEP 2 — LESSON CONTENT GENERATION
Input: [Step 1 objectives]
Prompt: "Generate lesson content outline with:
- Concept explanation (plain language)
- 2 concrete examples (real-world application)
- Common misconception and correction
- Summary framework (mnemonic or visual concept)"

STEP 3 — ASSESSMENT CREATION
Input: [Step 2 content]
Prompt: "Create 5 assessment questions from this lesson:
2 MCQ (knowledge check), 2 scenario questions (application),
1 reflection question. Include model answers."

STEP 4 — FACILITATION GUIDE
Input: [Step 1 objectives + Step 2 content + Step 3 assessments]
Prompt: "Write a facilitator guide for this lesson:
- Suggested timing for each section
- Engagement activity for the 30-minute mark
- Common learner questions and suggested responses
- How to adapt if the group is ahead / behind schedule"
```

---

## 27.6 Quality Gate — End of Session 27

Before ending Session 27, run this quality gate on everything built:

```
CAPSTONE BUILD QUALITY GATE — SESSION 27

For each of my 5 completed prompts, answer:

COMPLETENESS:
□ Full documentation standard completed? (all metadata fields)
□ Example input and output documented?
□ Iteration history shows at least v1.0 → v1.1?
□ "Do Not Use When" section completed?

QUALITY:
□ Prompt tested on 3+ different inputs?
□ Average quality score across tests: ___/5 (minimum: 3/5 to proceed)
□ Failure modes identified and addressed?

PIPELINE:
□ Pipeline Design Document completed?
□ All steps tested end-to-end at least once?
□ At least one quality gate defined and tested?
□ Context brief defined and consistently applied?

BASELINE:
□ Baseline measurements documented for all target tasks?
□ Before-state quality scores recorded?

If ANY answer is NO: Address before starting Session 28.
Session 28 builds ON this foundation — weak foundations compound.
```

---

## Hands-On Activities — Session 27

---

### Activity 27.1 — Baseline Data Collection

Run the Baseline Data Collection Prompt on your chosen capstone tasks. Spend time on this — it is your evidence base for the impact claim in your final presentation.

Time yourself doing each task manually (or estimate carefully from past experience). Record everything in your baseline table.

---

### Activity 27.2 — Build Prompt 1: Your Core Task

Follow the 5-step Build Protocol (Section 27.3) for your most important prompt.

Do not move to Prompt 2 until Prompt 1 has been tested on 3 inputs and iterated at least once.

---

### Activity 27.3 — Build Prompts 2 & 3: Pipeline Steps 1 and 2

Build the first two steps of your core pipeline following the Pipeline Design Document.

Test steps 1 and 2 in sequence — does the output of step 1 work as input for step 2? If not, what context is missing?

---

### Activity 27.4 — Build Prompts 4 & 5

Build your supporting task prompt and your quality evaluation prompt.

Test the quality evaluation prompt on outputs from Prompts 1–3. Does the rubric catch the right quality issues?

---

### Activity 27.5 — Run the Session 27 Quality Gate

Complete the quality gate checklist before closing this session. Address every NO before moving to Session 28.

---

## Session 27 Deliverable Checklist

```
BY END OF SESSION 27:
□ Baseline measurements documented (table format)
□ 5 prompt library entries — complete documentation standard
□ Pipeline Design Document completed
□ All 5 prompts tested on 3+ inputs each
□ Iteration history showing at least v1.0 → v1.1 for each prompt
□ Session 27 Quality Gate passed (all checkboxes YES)
□ Clear plan for Session 28 (which 5 prompts to build next)
```

---

## Key Takeaways — Session 27

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 27 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Baseline before building — without a "before" measurement,      │
│    impact cannot be proven; collect it first                        │
│                                                                      │
│  ✓ Build protocol: Design → Write v1.0 → Test 3 inputs →           │
│    Diagnose one failure → Iterate to v1.1 → Document               │
│                                                                      │
│  ✓ Priority sequence: Core task → Pipeline steps → Supporting →    │
│    Quality evaluation prompt (you need this to evaluate everything) │
│                                                                      │
│  ✓ Pipeline Design Document before pipeline prompts — architecture │
│    decisions made in writing, not discovered mid-build             │
│                                                                      │
│  ✓ Session 27 Quality Gate is mandatory — weak foundations in      │
│    Session 27 become compounding problems in Session 28            │
│                                                                      │
│  ✓ "Make it work, then make it better" — a tested 70% solution    │
│    beats an untested perfect design every time                     │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 27 Complete → Proceed to Session 28: Capstone Build Phase 2 & Quality Assurance*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
