# Session 26: Capstone — Problem Definition & Solution Design
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 6 — CAPSTONE PROJECT                                                 │
│  SESSION 26 of 30  |  1 Hour  |  20% Theory + 80% Hands-On                 │
│                                                                              │
│  "Every great AI solution starts with a clearly defined problem.            │
│   The work you do in this session determines the quality of everything      │
│   that follows."                                                             │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 26, you will be able to:

- Select and clearly articulate a real-world problem worth solving with AI
- Apply the Problem Definition Canvas to diagnose a business problem precisely
- Design an AI-based solution with defined scope, tools, and success metrics
- Write a compelling Problem Statement and Solution Hypothesis
- Produce a complete Capstone Project Brief that guides Sessions 27–30
- Understand the evaluation criteria for the final capstone submission

---

## 1. The Capstone Project Overview

### 1.1 What the Capstone Is

The capstone project is the culminating work of the certification program. Over Sessions 26–30, you will:

```
SESSION 26: Define your problem and design your solution
SESSION 27: Build the actual AI solution (prompts, tools, pipeline)
SESSION 28: Test, evaluate, and refine your solution
SESSION 29: Prepare your presentation deck and delivery
SESSION 30: Present your solution and receive certification

THE DELIVERABLE:
  A real, working AI solution that:
  ✓ Addresses a genuine business or professional problem
  ✓ Uses AI tools and techniques from this course
  ✓ Has been tested and refined
  ✓ Can be demonstrated live
  ✓ Includes a 10-minute professional presentation

THE STANDARD:
  "Could you show this to your manager, a client, or an employer
   and have them immediately understand its value?"
```

### 1.2 Capstone Project Options

Choose ONE category for your capstone:

```
CATEGORY A — AI PRODUCTIVITY SYSTEM:
  Build a personal or team AI workflow that measurably improves productivity
  in a specific professional context.
  Example: A complete AI-powered content creation system for a startup,
  a weekly reporting automation for a business team, or a personal
  research-to-writing pipeline.

CATEGORY B — AI BUSINESS SOLUTION:
  Apply AI to a specific business function (marketing, HR, finance,
  customer support, operations) to solve a real problem.
  Example: An AI-powered customer support response system,
  an AI-assisted recruitment workflow, or a financial narrative generator.

CATEGORY C — AI ASSISTANT / CHATBOT:
  Design and build a Custom GPT or chatbot for a specific use case,
  complete with system prompt, knowledge base, and testing documentation.
  Example: A policy FAQ assistant, a product recommendation assistant,
  or a learning support chatbot.

CATEGORY D — AI CREATIVE / MULTIMEDIA SYSTEM:
  Build a multi-tool content production pipeline producing professional
  multimedia output for a specific audience and purpose.
  Example: A complete social media production system, an e-learning
  module creation pipeline, or a branded content generation system.
```

---

## 2. The Problem Definition Canvas

Before designing any solution, the problem must be precisely defined. A vague problem leads to a vague solution.

### 2.1 The Canvas — 8 Elements

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  PROBLEM DEFINITION CANVAS                                                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  1. WHO HAS THIS PROBLEM?                                                    │
│     Describe the person/role experiencing this problem.                     │
│     Be specific: not "marketing teams" but "a solo marketing manager        │
│     at a 50-person B2B SaaS company with no design support"                 │
│                                                                              │
│  2. WHAT IS THE PROBLEM?                                                     │
│     Describe the current situation in 2–3 sentences.                        │
│     Include: what they do today, what is painful about it, frequency.       │
│                                                                              │
│  3. WHAT IS THE IMPACT?                                                      │
│     Quantify if possible: time lost, cost, quality impact,                  │
│     opportunity cost, stress.                                                │
│                                                                              │
│  4. WHAT CAUSES THE PROBLEM?                                                 │
│     Root cause analysis: WHY does this problem exist?                       │
│     (Not symptoms — the underlying reason)                                  │
│                                                                              │
│  5. WHAT HAS BEEN TRIED?                                                     │
│     Current or past attempts to solve this. Why did they fail or            │
│     why are they insufficient?                                               │
│                                                                              │
│  6. WHAT DOES "SOLVED" LOOK LIKE?                                            │
│     Describe the ideal future state. What would the person experience       │
│     if this problem were fully resolved?                                     │
│                                                                              │
│  7. WHAT ARE THE CONSTRAINTS?                                                │
│     Budget, tools available, technical skills, time, data privacy,          │
│     stakeholder requirements.                                                │
│                                                                              │
│  8. HOW WILL WE MEASURE SUCCESS?                                             │
│     2–3 specific, measurable success metrics.                               │
│     Not "it saves time" — but "reduces report writing from 3 hours           │
│     to 45 minutes (75% reduction), verified by time tracking"               │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### 2.2 Worked Example — Problem Definition Canvas

**Student profile:** Tanvir, HR Business Partner at a 300-person technology company

```
PROBLEM DEFINITION CANVAS — FILLED EXAMPLE:

1. WHO HAS THIS PROBLEM?
   HR Business Partners and people managers at mid-sized technology companies
   (300–1,000 employees). Specifically: managers who conduct quarterly performance
   reviews for 6–10 direct reports and lack structured support in writing them.

2. WHAT IS THE PROBLEM?
   Each quarter, managers must write performance review narratives for all direct
   reports. Most managers spend 3–5 hours per review cycle writing vague,
   generic comments ("good team player," "meets expectations") because they lack
   a structured process and the time to write thoughtful, specific feedback.
   HR spends additional time coaching managers to improve their review quality.

3. WHAT IS THE IMPACT?
   - Each manager: 24–40 hours/year on performance reviews
   - Review quality: 60% rated "needs improvement" in last HR audit
   - HR rework: 8 hours/review cycle coaching poor-quality reviews
   - Employee dissatisfaction: 42% say feedback is too vague to act on
   - Business impact: poor feedback → slower professional development

4. WHAT CAUSES THE PROBLEM?
   Root cause: Managers lack a structured prompting framework that converts
   their observational notes into specific, developmental review language.
   They have the observations but not the writing skill or time.

5. WHAT HAS BEEN TRIED?
   - Manager training on performance feedback (limited impact — forgotten quickly)
   - Review templates with prompts (partially helpful, but still blank-page problem)
   - HR coaching reviews (scales poorly — HR is a bottleneck)

6. WHAT DOES "SOLVED" LOOK LIKE?
   A manager can: take 5 bullet notes about an employee's performance →
   paste into an AI tool → receive a structured, specific, development-focused
   review narrative → edit lightly for personal voice → submit in 20 minutes.
   Quality audits show 80%+ meet the "good" standard without HR rework.

7. CONSTRAINTS?
   - Only publicly available AI tools (no enterprise IT deployment for now)
   - No employee names or sensitive data in public AI tools (privacy)
   - Must work within ChatGPT Free or Plus (no coding required)
   - Managers are non-technical — must be easy to use

8. SUCCESS METRICS:
   - Review writing time per employee: 45 min → 15 min (67% reduction)
   - % reviews meeting quality standard without HR rework: 42% → 75%
   - Manager satisfaction with the tool: 4+/5 in post-pilot survey
```

---

## 3. Writing the Problem Statement

The Problem Statement is a crisp, compelling articulation of the problem — precise enough to drive solution design.

### 3.1 The Problem Statement Formula

```
[WHO] currently [DOES WHAT] which [TAKES/COSTS/CAUSES WHAT].
This happens because [ROOT CAUSE].
The business impact is [QUANTIFIED IMPACT].
A successful solution would [DESCRIBE THE DESIRED OUTCOME].
```

**Example (from Tanvir's canvas):**
```
HR managers at mid-sized technology companies currently write quarterly
performance reviews manually from scratch, which takes 3–5 hours per
employee and produces vague, unhelpful feedback 60% of the time.
This happens because managers lack a structured framework to convert
observational notes into specific developmental language.
The business impact is 30–40 hours/manager/year in low-value writing work,
42% of employees rating feedback as too vague to act on, and an 8-hour
HR coaching burden per review cycle.
A successful solution would allow a manager to convert 5 observation
bullets into a draft review narrative in under 15 minutes, meeting
the quality standard without HR rework.
```

---

## 4. The Solution Design

### 4.1 The AI Solution Design Framework

Once the problem is precisely defined, design the solution systematically:

```
SOLUTION DESIGN DOCUMENT:

1. SOLUTION CONCEPT (1 paragraph):
   Describe what you are building. The reader should understand
   what it is, who uses it, and how, in 3–4 sentences.

2. AI TOOLS REQUIRED:
   List the tools your solution will use, and why each was chosen.

3. PIPELINE / WORKFLOW MAP:
   Map the steps from user input to final output.
   Use the pipeline map template from Session 25.

4. KEY PROMPTS (list — build in Session 27):
   What prompts will you develop? Name and describe each.

5. RESPONSIBLE AI CONSIDERATIONS:
   Data privacy, bias risks, human review requirements,
   transparency with users.

6. MVP SCOPE (what is IN the solution for this capstone):
   What will you build in Sessions 27–28?
   What is explicitly OUT OF SCOPE for now?

7. SUCCESS METRICS:
   How will you know it works? (From Problem Definition Canvas #8)

8. TIMELINE:
   Session 27: Build [LIST WHAT YOU'LL BUILD]
   Session 28: Test [LIST WHAT YOU'LL TEST]
   Session 29: Present [PRESENTATION PREP TASKS]
```

### 4.2 Worked Example — Solution Design

**Tanvir's Solution Design:**

```
1. SOLUTION CONCEPT:
   A Performance Review AI Assistant — a Custom GPT that transforms a manager's
   bullet-note observations about an employee into a structured, specific,
   development-focused performance review narrative. The manager inputs:
   employee role, performance rating, and 5–8 bullet observations. The GPT
   outputs a complete review narrative with 4 sections: Overall Performance
   Summary, Key Strengths (with examples), Development Areas, and SMART Goals.

2. AI TOOLS REQUIRED:
   Primary: ChatGPT Custom GPT (free to deploy, no-code, accessible on any device)
   Supporting: ChatGPT for prompt development and testing
   Alternative (if needed): Prompt template in Google Docs for managers
   without ChatGPT Plus

3. PIPELINE MAP:
   INPUT: Manager's bullet notes (role, rating, 5–8 observations)
   ↓
   STEP 1 (Custom GPT): Validates input completeness
   ↓
   STEP 2 (Custom GPT): Generates 4-section review narrative
   ↓
   STEP 3 (Custom GPT): Flags any vague language for human to improve
   ↓
   HUMAN CHECKPOINT: Manager reviews, personalizes, submits
   ↓
   OUTPUT: Final review ready for submission

4. KEY PROMPTS:
   - Core review generation prompt (main prompt — detailed CRAFT)
   - Input validation prompt (checks if observations are specific enough)
   - Vague language audit prompt (flags generic phrases for revision)
   - SMART goal generator prompt (for development section)

5. RESPONSIBLE AI CONSIDERATIONS:
   - Manager inputs must be anonymized (no real employee names)
   - All outputs are drafts — manager owns final review
   - No AI-generated ratings — only human-assigned ratings fed in
   - System prompt will include: "This is a drafting assistant. The manager
     is responsible for all performance judgments."

6. MVP SCOPE:
   IN: Core review generator + input validation + vague language audit
   OUT: CRM integration, automated distribution, multi-language support

7. SUCCESS METRICS:
   - Writing time: 45 min → 15 min (test with 3 sample reviews)
   - Quality: Evaluate 5 AI-generated reviews against quality rubric
   - Usability: 3 manager testers complete without instructions

8. TIMELINE:
   Session 27: Build core GPT system prompt + 3 key prompts + test samples
   Session 28: Test with 5 scenarios, run quality audit, refine
   Session 29: Build 10-slide presentation deck + speaker notes
```

---

## 5. Capstone Evaluation Criteria

### 5.1 How the Capstone Will Be Evaluated

```
CAPSTONE EVALUATION RUBRIC (Sessions 26–30):

SESSION 26 — Problem Definition & Solution Design (20 points):
  ☐ Problem Definition Canvas: all 8 elements completed with specificity (8 pts)
  ☐ Problem Statement: follows the formula, quantified, precise (4 pts)
  ☐ Solution Design: all 8 elements, MVP scope clearly defined (8 pts)

SESSION 27 — Building the Solution (25 points):
  ☐ All prompts written to CRAFT standard (10 pts)
  ☐ Pipeline/workflow fully implemented (8 pts)
  ☐ AI tools correctly selected and configured (7 pts)

SESSION 28 — Quality Assurance (20 points):
  ☐ Testing documentation: 5+ test scenarios run (8 pts)
  ☐ Quality issues identified and resolved (6 pts)
  ☐ Responsible AI checklist completed (6 pts)

SESSION 29 — Presentation Preparation (10 points):
  ☐ 10-slide presentation deck complete (5 pts)
  ☐ Speaker notes for all slides (3 pts)
  ☐ 5 tough Q&As prepared with answers (2 pts)

SESSION 30 — Final Presentation (25 points):
  ☐ Clarity: Is the problem and solution clearly communicated? (8 pts)
  ☐ Demonstration: Is the solution shown working live? (7 pts)
  ☐ Impact: Is the business value clearly articulated? (5 pts)
  ☐ Q&A: Are questions answered confidently? (5 pts)

TOTAL: 100 points
PASS THRESHOLD: 70 points
DISTINCTION: 85+ points
```

---

## 6. AI Tools to Help You Define Your Problem

### 6.1 Using AI to Improve Your Problem Definition

AI can help you sharpen your problem definition before you finalize it:

**Prompt 1 — Problem Sharpener:**
```
PROMPT:
I am defining a problem for an AI solution capstone project.
Here is my current problem description: [PASTE YOUR DRAFT PROBLEM]

Act as a demanding consultant and challenge my problem definition:
1. Is this problem specific enough? If not, what's missing?
2. Is the root cause identified, or am I describing symptoms?
3. Is the impact quantified? If not, how could I estimate it?
4. Who exactly experiences this — am I too broad or too narrow?
5. Is this genuinely solvable with AI tools available to a non-developer?

Then rewrite my Problem Statement using the formula:
[WHO] currently [DOES WHAT] which [TAKES/COSTS/CAUSES WHAT].
This happens because [ROOT CAUSE].
The business impact is [QUANTIFIED IMPACT].
A successful solution would [DESIRED OUTCOME].
```

**Prompt 2 — Solution Feasibility Check:**
```
PROMPT:
I am proposing this AI solution for a professional certification capstone:
[DESCRIBE YOUR SOLUTION CONCEPT]

Act as a skeptical evaluator and assess:
1. Is this genuinely feasible with the AI tools described?
2. What is the most likely failure mode of this solution?
3. What responsible AI risks should I address?
4. What is the minimum viable version I should build?
5. What success metrics would actually demonstrate this works?

Be constructive but honest about weaknesses in the design.
```

---

## 7. Common Problem Selection Mistakes to Avoid

```
MISTAKE 1: TOO BROAD
  Bad: "AI for marketing"
  Good: "An AI prompt system that generates one week of Instagram captions
        for a fashion D2C brand in under 30 minutes"

MISTAKE 2: TOO NARROW / TOO TRIVIAL
  Bad: "An AI prompt to write thank-you emails"
  Good: "A complete customer response template library covering 12 ticket
        types, with a quality scoring system"

MISTAKE 3: PROBLEM DOESN'T EXIST YET
  Bad: "A solution for a problem I imagined" (no real evidence)
  Good: A problem you have directly experienced or observed in your
        professional/academic life

MISTAKE 4: SOLUTION LOOKING FOR A PROBLEM
  Bad: "I want to use Zapier, so I'll build something with Zapier"
  Good: Start with the real problem → choose tools that best solve it

MISTAKE 5: IGNORING RESPONSIBLE AI
  Bad: Designing a solution that inputs personal/confidential data
       into public AI tools
  Good: Design the data handling as carefully as the technical solution

MISTAKE 6: NO MEASURABLE OUTCOME
  Bad: "The solution will save time" (how much? how do you know?)
  Good: "The solution will reduce email drafting time from 15 minutes
        to 3 minutes per email, verified by self-reported time tracking"
```

---

## 8. Hands-On Lab 26: Capstone Kickoff

**Objective:** Complete your Problem Definition Canvas and Solution Design Document  
**Duration:** 30 minutes (extended for capstone kickoff)

---

### Task 1: Choose Your Category and Problem (5 minutes)

Select one of the four capstone categories (A, B, C, or D).

Identify a real problem from your professional, academic, or entrepreneurial experience. The problem must:
- Be real (you have observed or experienced it)
- Be solvable with AI tools covered in this course
- Have a measurable outcome
- Not require you to input real personal data into public AI tools

---

### Task 2: Complete the Problem Definition Canvas (10 minutes)

Fill in all 8 elements of the Problem Definition Canvas with specificity.

Use the AI Problem Sharpener prompt to challenge and improve your draft if needed.

---

### Task 3: Write Your Problem Statement (5 minutes)

Write a 4-sentence Problem Statement using the formula.

Have a classmate or the AI evaluate it: Is it specific? Quantified? Clear?

---

### Task 4: Draft Your Solution Design (10 minutes)

Complete all 8 elements of the Solution Design Document.

Focus especially on:
- Your pipeline map (even if rough at this stage)
- Your MVP scope (what is realistically buildable in Session 27)
- Your success metrics (how will you prove it works in Session 28)

---

### Lab Evaluation Rubric

| Deliverable | Marks |
|-------------|-------|
| Problem Definition Canvas — all 8 elements completed | 8 |
| Problem Statement — follows formula, quantified, precise | 4 |
| Solution Design — all 8 elements, MVP scope defined | 8 |
| **Total** | **20** |

*(Note: This lab is worth double marks as the foundation for the entire capstone)*

---

## 9. Interview Questions — Session 26

**Q1:** *"Tell me about an AI project you've worked on. How did you define the problem?"*

**Strong Answer:**
"I used a structured Problem Definition Canvas before designing anything. The canvas has 8 elements: who has the problem, what it is, the quantified impact, the root cause, what's been tried, what success looks like, constraints, and success metrics. The key insight this process gave me was the root cause — I discovered that the problem I was solving wasn't the one the person *said* they had, but a deeper underlying issue. Once I had a precise problem statement using the formula — [who] currently [does what] which [costs/causes what] because [root cause], and a successful solution would [outcome] — I could design a solution that actually addressed the root cause rather than the surface symptom. My solution design then mapped the pipeline, identified the right AI tools for each step, and defined an MVP scope I could build and test in two sessions."

---

## 10. Revision Questions — Session 26

1. What are the 4 capstone categories? Give an example project for each.
2. What are the 8 elements of the Problem Definition Canvas? Why is each necessary?
3. Write the Problem Statement Formula. Give a fictional example using it.
4. What are the 8 elements of the Solution Design Document?
5. What is MVP Scope and why is it important to define it explicitly?
6. What are the 6 common problem selection mistakes? Give a "bad" and "good" example for each.
7. What is the Capstone Evaluation Rubric? How many total points and what is the pass threshold?
8. How can AI itself help you improve your problem definition? What two prompts were provided?

---

## 11. Key Terminology — Session 26

| Term | Definition |
|------|-----------|
| **Problem Definition Canvas** | An 8-element structured tool for precisely diagnosing a business problem before designing a solution |
| **Problem Statement** | A concise, formulaic articulation of a problem including who, what, impact, root cause, and desired outcome |
| **Solution Design Document** | An 8-element planning document for an AI solution including tools, pipeline, prompts, and success metrics |
| **MVP (Minimum Viable Product)** | The simplest version of a solution that can be built and tested to validate the core concept |
| **Root Cause** | The underlying reason a problem exists — distinct from its symptoms |
| **Success Metrics** | Specific, measurable criteria used to determine whether a solution has solved the problem |
| **Capstone Project** | The final integrative project for the certification program — a real AI solution designed, built, tested, and presented |

---

## 12. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 26 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  4 capstone categories: Productivity, Business Solution, AI Assistant,   │
│     Creative/Multimedia System                                               │
│  ✓  Problem Definition Canvas: 8 elements — start here before any design    │
│  ✓  Problem Statement formula: WHO + DOES WHAT + COSTS + ROOT CAUSE +       │
│     DESIRED OUTCOME (4 sentences)                                            │
│  ✓  Solution Design: 8 elements including pipeline map and MVP scope        │
│  ✓  6 mistakes: too broad, too trivial, imaginary problem, solution-first,  │
│     no responsible AI, no metrics                                            │
│  ✓  Evaluation: 100 points, 70 = pass, 85 = distinction                    │
│  ✓  Lab 26 deliverables: Canvas (8 pts) + Statement (4 pts) + Design (8 pts)│
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 27 — Capstone: Building Your AI Solution                           │
│  (Implement your pipeline, write all production-ready prompts,             │
│   configure your tools, and produce working demonstration outputs)          │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 26 Complete | Next: Session 27 — Capstone: Building Your AI Solution*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
