# Session 27: Capstone — Building Your AI Solution
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 6 — CAPSTONE PROJECT                                                 │
│  SESSION 27 of 30  |  1 Hour  |  10% Theory + 90% Hands-On                 │
│                                                                              │
│  "You have defined the problem. You have designed the solution.             │
│   This session, you build it. Every prompt written, every step mapped,     │
│   every tool configured — done today."                                       │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 27, you will be able to:

- Implement every step of your designed AI pipeline using the right tools
- Write all key prompts to production-ready CRAFT standard
- Configure your AI assistant or automation workflow end-to-end
- Generate working demonstration outputs for testing in Session 28
- Apply the Prompt Quality Rubric to self-evaluate each prompt before using it
- Document your solution for reproducibility and presentation

---

## 1. The Build Mindset

### 1.1 From Design to Implementation

```
SESSION 26 OUTPUT:
  ✓ Problem Definition Canvas (completed)
  ✓ Problem Statement (written and refined)
  ✓ Solution Design Document (all 8 elements)
  ✓ Pipeline Map (step-by-step)
  ✓ Key Prompts identified (names and purposes)

SESSION 27 GOAL:
  Transform every element of your design into a working, demonstrable solution.
  By the end of this session:
  ✓ Every prompt written, tested, and meeting quality standard
  ✓ Every tool configured and connected
  ✓ At least 3 working sample outputs produced
  ✓ Build documentation completed
```

### 1.2 The Build Priority Order

Not all parts of your solution are equal. Build in this order:

```
PRIORITY 1 — THE CORE PROMPT (most important):
  The one prompt that does the most critical work in your pipeline.
  This is the heart of your solution. Build it first, refine it most.

PRIORITY 2 — THE INPUT/OUTPUT CHAIN:
  Whatever comes before and after the core prompt the full pipeline flow.
  Build so a user can go from raw input to final output end-to-end.

PRIORITY 3 — SUPPORTING PROMPTS:
  Validation, quality-checking, formatting, or ancillary prompts.
  Important but secondary to the core.

PRIORITY 4 — AUTOMATION AND INTEGRATION:
  If your solution includes Zapier workflows or Custom GPT configuration
  these come after the prompt logic is proven to work manually.

PRIORITY 5 — POLISH:
  Formatting, user instructions, templates for end users.
  Add last, after functionality is confirmed.
```

---

## 2. The Production-Ready Prompt Standard

### 2.1 What "Production-Ready" Means

A production-ready prompt is one that:

```
PRODUCTION-READY PROMPT CHECKLIST:

☐ CRAFT COMPLETE: Context, Role, Action, Format, Tone — all specified
☐ PLACEHOLDERS CLEAR: Every variable clearly marked as [PLACEHOLDER]
   in square brackets user knows exactly what to replace
☐ OUTPUT ANCHORED: Format is explicitly specified (bullet list / table /
   paragraphs / numbered steps) — AI knows the exact structure to produce
☐ CONSTRAINTS INCLUDED: Length, exclusions, rules for edge cases
☐ TESTED: Has produced at least 3 consistent, quality outputs
☐ VERSIONED: Labeled with a version number (v1.0)
☐ DOCUMENTED: Purpose, use case, variables, and expected output noted
```

### 2.2 The Full CRAFT Prompt Build Template

Use this template to write every prompt in your solution:

```
[PROMPT ID: Your Library ID]
[PURPOSE: What this prompt does — 1 sentence]
[VERSION: v1.0]
[VARIABLES: List all [PLACEHOLDERS] and what they represent]

---PROMPT START---

[CONTEXT — 1–3 sentences setting up the situation]
You are [ROLE — specific expert persona].
[Your task/situation context: who you're helping, what has happened]

[ROLE — stated explicitly]
Your expertise includes: [RELEVANT EXPERTISE — specific and credible]

[ACTION — crystal clear instruction]
Your task is to [SPECIFIC TASK — verb-led, unambiguous]:
[If multi-part — number each part]
1. [FIRST SPECIFIC DELIVERABLE]
2. [SECOND SPECIFIC DELIVERABLE]
3. [THIRD SPECIFIC DELIVERABLE]

[FORMAT — explicit structure]
Format your response as:
[SECTION 1 TITLE]: [What goes here — length guidance]
[SECTION 2 TITLE]: [What goes here — length guidance]
[SECTION 3 TITLE]: [What goes here — length guidance]

[TONE — specific and measurable]
Tone: [TONE DESCRIPTION].
Do NOT use: [SPECIFIC PHRASES OR STYLES TO AVOID].

[CONSTRAINTS — guardrails and rules]
Additional constraints:
- [CONSTRAINT 1]
- [CONSTRAINT 2]
- [CONSTRAINT 3]
- Flag any gaps as [DATA NEEDED] rather than inventing information.

[USER INPUT SECTION]
---INPUT---
[VARIABLE 1]: [PLACEHOLDER]
[VARIABLE 2]: [PLACEHOLDER]
[VARIABLE 3]: [PLACEHOLDER]
---END INPUT---

---PROMPT END---
```

---

## 3. Building by Capstone Category

### 3.1 Category A — AI Productivity System

**Core build tasks:**
```
BUILD TASK 1 — Map your workflow:
  Document the complete workflow (what the user does vs. what AI does).
  Create a step-by-step user guide: how do they use this system daily?

BUILD TASK 2 — Core Prompts:
  Write each production-ready prompt in the workflow.
  For recurring prompts: add [PLACEHOLDERS] for the parts that change each use.
  Target: minimum 5 fully developed prompts.

BUILD TASK 3 — Prompt Library Document:
  Organize all prompts in a structured document:
  - Category / name / version / use case / full prompt text / sample output
  
BUILD TASK 4 — Test Runs:
  Run each prompt with 3 different realistic inputs.
  Document the best output for each as your sample output.

BUILD TASK 5 — User Instructions:
  Write a 1-page "Quick Start Guide" for a new user of your system.
  They should be able to use it without any explanation from you.
```

### 3.2 Category B — AI Business Solution

**Core build tasks:**
```
BUILD TASK 1 — Core Solution Prompt:
  The primary prompt that solves the business problem.
  This is the most important output of Session 27.
  Build it to the full CRAFT production-ready standard.
  Test with at least 5 realistic inputs from your problem domain.

BUILD TASK 2 — Supporting Prompts:
  Input validation prompt (checks if user input is complete and specific)
  Quality audit prompt (reviews the output and flags weaknesses)
  Edge case prompt (handles the 2–3 most common exceptions)

BUILD TASK 3 — Sample Outputs:
  Run your solution on 3 real or realistic example inputs.
  These are your demonstration materials for Session 30.

BUILD TASK 4 — Comparison:
  For the same 3 inputs, document what the current manual process produces.
  Side-by-side: Current approach vs. AI-assisted approach.
  This is your ROI evidence for the final presentation.

BUILD TASK 5 — User Documentation:
  Brief user guide for your target user:
  When to use this, what to input, what to expect, when to override AI.
```

### 3.3 Category C — AI Assistant / Chatbot

**Core build tasks:**
```
BUILD TASK 1 — System Prompt (full production version):
  Complete system prompt using the template from Session 23.
  Must include: Identity, Persona, Capabilities, Knowledge,
  Limits (guardrails), Escalation, Opening Message.

BUILD TASK 2 — Knowledge Base:
  Collect and upload all required documents.
  For Custom GPT: Upload files directly.
  Organize your knowledge with clear, specific document names.

BUILD TASK 3 — Configure the Custom GPT:
  Set up the GPT with your system prompt, knowledge, and capabilities.
  Test the opening message — does it make users feel welcome and clear?

BUILD TASK 4 — Core Q&A Testing:
  Generate 20 test questions (15 in-scope, 5 out-of-scope).
  Run all 20. Document responses. Identify failures.

BUILD TASK 5 — Refinement Round 1:
  Based on testing, identify the top 3 prompt failures.
  Diagnose root cause: wrong guardrail, missing knowledge, unclear scope?
  Update system prompt to address each failure.
  Re-test the 3 failed questions.
```

### 3.4 Category D — AI Creative / Multimedia System

**Core build tasks:**
```
BUILD TASK 1 — Brand/Style Foundation:
  Create the Brand Voice Card or Style Guide for your system.
  This anchors all content generation in the pipeline.

BUILD TASK 2 — Complete Pipeline Implementation:
  Execute every step of your PIPES pipeline map.
  For each step: write the prompt, test it, document the output.
  Save one quality output from each step as demonstration material.

BUILD TASK 3 — Content Set Production:
  Produce a complete set of sample outputs using your pipeline.
  For a content system: a full content set for one campaign or week.
  For a multimedia pipeline: a completed piece (video, article + image + social).

BUILD TASK 4 — Tool Configuration:
  Any automation (Zapier), any Custom GPT, any tool settings —
  configured and tested.

BUILD TASK 5 — Quality Comparison:
  Compare your pipeline output to what the same work would produce:
  (a) without AI, (b) with basic AI prompting without the pipeline.
  Document the difference this is your presentation evidence.
```

---

## 4. The Prompt Quality Rubric — Self-Evaluation

Before finalizing any prompt, score it against this rubric:

```
PROMPT QUALITY RUBRIC (from Session 10):

1. CONTEXT (0–5):
   0 = No context at all
   3 = Some context (tool, topic)
   5 = Full professional context (role, situation, audience, purpose)

2. SPECIFICITY OF ACTION (0–5):
   0 = Vague verb ("write something about...")
   3 = Clear action but general
   5 = Precise, measurable deliverable with specific sub-tasks

3. FORMAT SPECIFICATION (0–5):
   0 = No format guidance
   3 = General format requested
   5 = Explicit structure with section titles and length guidance

4. TONE AND VOICE (0–5):
   0 = No tone guidance
   3 = General tone ("professional")
   5 = Specific tone + "do not use X" constraints + voice model

5. CONSTRAINTS AND GUARDRAILS (0–5):
   0 = No constraints
   3 = Some limits (word count)
   5 = Data-handling rules, edge case instructions, quality guardrails

6. TESTABILITY (0–5):
   0 = Output is subjective — no way to know if it's good
   3 = Output could be partially evaluated
   5 = Clear success criteria built into the prompt or verifiable against
       the problem's success metrics

TOTAL: /30
  26–30: Production-ready — deploy
  20–25: Good — minor improvements before deployment
  14–19: Needs work — rewrite 1–2 sections before deployment
  Below 14: Major revision needed
```

---

## 5. Build Documentation Template

Every prompt and pipeline step must be documented for the presentation:

```
BUILD DOCUMENTATION — [PROJECT NAME]
──────────────────────────────────────────────────────────────────

PROJECT OVERVIEW:
  Problem solved: [1 sentence]
  Category: [A/B/C/D]
  Primary AI tool(s): [LIST]
  Total prompts built: [NUMBER]

PROMPT REGISTER:
  ID    | Name                | Purpose              | Quality Score | Version
  ───────────────────────────────────────────────────────────────────────────
  P-001 | [Name]              | [Purpose]            | [X/30]        | v1.0
  P-002 | [Name]              | [Purpose]            | [X/30]        | v1.0
  [etc.]

PIPELINE IMPLEMENTATION STATUS:
  Step | Tool           | Status        | Notes
  ──────────────────────────────────────────────────────────────
  1    | [TOOL]         | ✅ Complete   | [Any notes]
  2    | [TOOL]         | ✅ Complete   | [Any notes]
  3    | [TOOL]         | 🟡 In Progress | [Blocker if any]
  [etc.]

SAMPLE OUTPUTS PRODUCED:
  Output 1: [Brief description — what was input, what was output]
  Output 2: [Brief description]
  Output 3: [Brief description]

RESPONSIBLE AI COMPLIANCE:
  ☐ No PII used in any prompt or test
  ☐ Human review checkpoint built into workflow
  ☐ Data privacy risk assessed and mitigated
  ☐ Scope and limitations documented for users

KNOWN LIMITATIONS:
  1. [Limitation 1 and why it exists]
  2. [Limitation 2 and why it exists]

BUILD TIME:
  Session 27 actual hours spent: [X hours]
```

---

## 6. Common Build-Session Pitfalls and Fixes

```
PITFALL 1: STARTING WITH POLISH INSTEAD OF FUNCTION
  "I spent 30 minutes formatting my prompt library before testing the prompts."
  FIX: Always test function first. Format later. A beautiful broken prompt
  is worse than an ugly working one.

PITFALL 2: OVER-ENGINEERING THE FIRST VERSION
  "I tried to build 12 prompts instead of 5 core ones."
  FIX: Build the MVP. Your Session 26 design specified the MVP scope.
  Every additional feature is scope creep. Test what you have first.

PITFALL 3: NOT TESTING WITH REALISTIC INPUTS
  "I tested with perfect, clean inputs. It works great."
  FIX: Always test with messy, incomplete, or ambiguous inputs.
  Your real users will provide these. The prompt must handle them.

PITFALL 4: IGNORING THE QUALITY RUBRIC
  "I wrote the prompt, it seemed fine, I moved on."
  FIX: Score every production prompt against the rubric before finalizing.
  This catches problems before testing and saves rework in Session 28.

PITFALL 5: FORGETTING THE HUMAN CHECKPOINT
  "My automation runs end-to-end automatically — no human review."
  FIX: Add at least one human review step before any final output reaches
  an end user. Even if it's just "save as draft for review."

PITFALL 6: NO DOCUMENTATION
  "I'll remember how it works."
  FIX: Use the Build Documentation Template. During the Session 30
  presentation, you will need to explain every decision. You need the record.
```

---

## 7. Worked Example: Building Tanvir's Performance Review Assistant

Continuing the example from Session 26:

### 7.1 The Core Prompt — Built to Production Standard

```
[PROMPT ID: PRF-001]
[PURPOSE: Generate structured performance review narrative from manager's bullet notes]
[VERSION: v1.0]
[VARIABLES: [EMPLOYEE_ROLE], [PERFORMANCE_RATING], [OBSERVATION_BULLETS]]

---PROMPT START---

You are an experienced HR Business Partner at a technology company
who is helping a line manager write a structured, specific, and
developmental quarterly performance review.

Your expertise includes: translating observational notes into professional
performance language, applying SMART goal frameworks, and writing reviews
that are both honest and developmental in tone.

Your task is to convert the manager's raw observation bullets into a
formal performance review narrative with four sections:

1. OVERALL PERFORMANCE SUMMARY (2–3 sentences):
   State the performance level clearly, using the rating provided.
   Do not use vague language. Reference the role expectations briefly.

2. KEY STRENGTHS — 2 specific examples:
   For each strength:
   - Name the competency or behavior (specific, not generic)
   - Reference one example from the manager's notes
   - State the business impact of this strength

3. DEVELOPMENT AREAS — 1–2 areas:
   For each:
   - Name the specific gap (not "communication" — be precise)
   - Reference one example from the notes
   - Frame developmentally: "An area for growth is..."
   - Suggest one concrete development action

4. GOALS FOR NEXT QUARTER — 2 SMART goals:
   Specific, Measurable, Achievable, Relevant, Time-bound.
   Directly address development areas where possible.

Format: Professional prose. Active voice. 
Do not use bullet points — write in paragraphs.
Each section on a new line with the section title in CAPS.

Tone: Honest, specific, forward-looking, professional.
Do NOT use: "good team player," "meets expectations," "hardworking,"
or any other phrase that is not grounded in a specific observable example.

Additional constraints:
- Do not add examples, achievements, or claims not present in my notes
- Flag any observation too vague to work with as [CLARIFY: ...]
- This is a draft for the manager to review — flag anything requiring
  the manager's judgment as [MANAGER REVIEW: ...]
- Keep to 350–450 words total

---INPUT---
EMPLOYEE ROLE: [EMPLOYEE_ROLE]
PERFORMANCE RATING: [PERFORMANCE_RATING]
  (Options: Exceptional / Exceeds Expectations / Meets Expectations /
   Partially Meets / Does Not Meet)
OBSERVATION BULLETS: 
[OBSERVATION_BULLETS]
---END INPUT---

---PROMPT END---
```

**Quality Rubric Score: 29/30** (deduction: could add more tone specificity)

### 7.2 Sample Output — Testing the Prompt

**Test Input:**
```
EMPLOYEE ROLE: Senior Software Engineer
PERFORMANCE RATING: Exceeds Expectations
OBSERVATION BULLETS:
- Led the API migration project — delivered 3 weeks early, zero production incidents
- Mentored 2 junior devs — both passed their first code reviews independently
- Missed 2 sprint planning sessions without notice in Q2 (addressed in 1:1)
- Proactively documented the new authentication module (saved team onboarding time)
- Communication with product team could be clearer sometimes misaligned on requirements
- Reduced API response time by 40% through caching optimization (flagged by CTO)
```

**AI Output (excerpt):**
```
OVERALL PERFORMANCE SUMMARY
This quarter, [Employee Name] has delivered at a level that meaningfully
exceeds the expectations of a Senior Software Engineer. Their contributions
spanned technical delivery, team development, and proactive quality improvement,
with particularly standout performance in the API migration project.

KEY STRENGTHS
The most significant strength demonstrated this quarter was technical ownership
and delivery discipline. Leading the API migration project, [Employee Name]
not only delivered three weeks ahead of schedule but did so with zero production
incidents a result that reflects exceptional planning, testing rigour, and
cross-team coordination. This project outcome directly reduced the risk of
service disruption and was recognized at the CTO level as a model delivery.

The second strength worth highlighting is a commitment to team capability
development...
[MANAGER REVIEW: Continue with mentoring example and documentation contribution]
```

**Assessment:** Output is specific, grounded in the provided examples, correctly flagged sections needing manager judgment, and maintained professional tone throughout. Ready for Session 28 quality testing.

---

## 8. Hands-On Lab 27: The Build Session

**Duration:** 50 minutes (full session hands-on)  
**Objective:** Produce a working, demonstrable AI solution

---

### Build Checklist (track your progress):

```
PRE-BUILD (5 min):
  ☐ Reviewed my Solution Design Document from Session 26
  ☐ Identified my Build Priority Order (core prompt first)
  ☐ Opened all required tools (ChatGPT, Zapier, Gamma, etc.)

CORE PROMPT BUILD (15 min):
  ☐ Written to full CRAFT production-ready standard
  ☐ All [PLACEHOLDERS] clearly marked
  ☐ Scored on Quality Rubric — score: ___/30
  ☐ Tested with 3 realistic inputs

SUPPORTING PROMPTS (15 min):
  ☐ Prompt 2: [NAME] — built and tested
  ☐ Prompt 3: [NAME] — built and tested
  ☐ Prompt 4: [NAME] — built and tested (if applicable)

PIPELINE / CONFIGURATION (10 min):
  ☐ Custom GPT configured (if Category C)
  ☐ Zapier Zap built and tested (if Category A/B with automation)
  ☐ Full pipeline run end-to-end with one complete input

SAMPLE OUTPUTS (5 min):
  ☐ 3 sample outputs produced and saved
  ☐ Best output identified as primary demo material

DOCUMENTATION (5 min):
  ☐ Build Documentation Template completed
  ☐ Prompt Register filled for all prompts
  ☐ Limitations section completed honestly
```

---

### Lab Evaluation Rubric

| Deliverable | Marks |
|-------------|-------|
| Core prompt written to CRAFT standard + Quality Rubric score shown | 10 |
| 2+ supporting prompts written and tested | 6 |
| 3 sample outputs produced | 6 |
| Build Documentation Template completed | 3 |
| **Total** | **25** |

---

## 9. Interview Questions — Session 27

**Q1:** *"How do you ensure the quality of prompts you build for professional use?"*

**Strong Answer:**
"I apply a 6-dimension quality rubric to every production prompt before deploying it scoring context, specificity of action, format specification, tone and voice, constraints and guardrails, and testability, on a scale of 1–5 each. A score below 20 out of 30 means the prompt needs revision before use. Beyond the rubric, I test every prompt with at least three realistic inputs including imperfect or ambiguous inputs that real users would actually provide, not just clean test cases. I document each prompt with its purpose, version, variables, expected output, and quality score, so anyone on my team can understand and use it without needing me to explain it. The documentation also makes it easy to iterate when a prompt underperforms in production, I can quickly identify which dimension to improve."

---

## 10. Revision Questions — Session 27

1. What is the 5-step Build Priority Order? Why should the core prompt be built first?
2. What are the 6 elements of a production-ready prompt checklist?
3. What is the full CRAFT Prompt Build Template? What are its 6 sections?
4. What is the Prompt Quality Rubric? Describe each of the 6 dimensions and what a score of 5 looks like.
5. What are the build tasks for Category B (AI Business Solution)?
6. What are the 6 common build-session pitfalls? For each, describe the fix.
7. In Tanvir's core prompt (PRF-001), identify the Context, Role, Action, Format, Tone, and Constraints elements.
8. What is the Build Documentation Template? What 7 sections does it contain?

---

## 11. Key Terminology — Session 27

| Term | Definition |
|------|-----------|
| **Production-Ready Prompt** | A prompt that meets all quality standards and is ready for real-world deployment |
| **Prompt Register** | A documentation record of all prompts in a solution with their purpose, version, and quality score |
| **Build Priority Order** | The sequence for implementing a solution: core prompt first, then supporting prompts, then automation and polish |
| **Output Anchoring** | Specifying the exact format structure an AI must follow in its response |
| **Placeholder** | A marked variable in a prompt template (in [SQUARE BRACKETS]) that the user replaces with specific information |
| **Sample Output** | A tested, high-quality example of a prompt's output used as demonstration material |
| **MVP Scope** | The minimum viable set of features to build and test in the available time |
| **Build Documentation** | A complete record of what was built, how it works, its limitations, and testing results |

---

## 12. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 27 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  Build priority: Core prompt → Input/output chain → Supporting prompts   │
│     → Automation → Polish                                                    │
│  ✓  Production-ready checklist: CRAFT complete, placeholders, output        │
│     anchored, constraints, tested, versioned, documented                    │
│  ✓  Quality Rubric: 6 dimensions, score /30, deploy at 26+                 │
│  ✓  Test with messy inputs — real users never give clean input              │
│  ✓  Document everything: Build template, prompt register, sample outputs    │
│  ✓  6 pitfalls: polish first, over-engineering, clean inputs, skip rubric,  │
│     no human checkpoint, no documentation                                    │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 28 — Capstone: Quality Assurance & Testing                        │
│  (Systematic testing of your solution, identifying and resolving failures, │
│   responsible AI audit, and producing your final demonstration materials)  │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 27 Complete | Next: Session 28 — Capstone: Quality Assurance & Testing*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
