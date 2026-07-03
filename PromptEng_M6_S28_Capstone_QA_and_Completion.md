# Session 28: Capstone Build Phase 2 — Complete System & Quality Assurance
## Module 6 — Capstone Project & Certification
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 28 OF 30  │  Module 6, Session 3                          │
│  Topic: Capstone Build Phase 2 — Complete System, QA & Impact Data  │
│  Duration: 90–120 minutes (extended build session)                  │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Complete the remaining 5+ prompt library entries to reach the 10-entry minimum
2. Finalize your automation design with full governance documentation
3. Conduct a comprehensive responsible AI assessment of your complete system
4. Apply the quality evaluation rubric across all outputs and document results
5. Measure and document after-state metrics for your impact comparison
6. Compile the full deliverables package ready for presentation

---

## 28.1 Building Prompts 6–10: The Advanced Layer

Session 27 built the foundational prompts. Session 28 builds the advanced layer — prompts that handle edge cases, complex variations, and team-scale use.

### Advanced Prompt Types to Add in Session 28

```
AFTER YOUR CORE PROMPTS WORK — BUILD THESE:

1. EDGE CASE HANDLER
   A prompt variant for the hardest or most unusual inputs your system will face.
   Example: The report-writing prompt for a report with contradictory data sources.

2. AUDIENCE ADAPTATION PROMPT
   Takes core output from your pipeline and adapts it for a different audience.
   Example: Technical report → Executive brief → Client summary.

3. BATCH / TEMPLATE VARIANT
   The automation-ready version of your best prompt with full variable placeholders.
   Example: The email template version of your core email prompt.

4. QUALITY IMPROVEMENT PROMPT
   Takes any output from your system and critiques + improves it.
   "Given this [OUTPUT], improve it by addressing [specific weakness]."

5. CHAIN CONNECTOR PROMPT
   The synthesis step — takes outputs from multiple prompts and combines them.
   Example: Combines research brief + competitor analysis + market data
   into a unified strategic recommendation.
```

---

## 28.2 Automation Design — Complete Documentation

In Session 27 you designed your pipeline. In Session 28, complete the automation documentation so it could be handed to a developer or implemented in a no-code tool.

### Full Automation Specification

```
════════════════════════════════════════════════════════════════════════
AUTOMATION SPECIFICATION — [AUTOMATION NAME]
════════════════════════════════════════════════════════════════════════

OVERVIEW:
Purpose: [What this automation accomplishes]
Trigger: [What initiates this automation — manual, scheduled, event-based]
Frequency: [How often it runs]
Owner: [Who is responsible for this automation]
Current status: [Designed / Prototyped / Production-ready]

INPUTS:
Data source: [Where input data comes from]
Input format: [CSV / JSON / email / form / database query / manual paste]
Required fields: [List each required variable with format and example]
Optional fields: [List optional variables and defaults if not provided]

STEPS:
Step 1: [Name]
  Tool/method: [OpenAI API / ChatGPT manual / Zapier / Make / Python]
  Prompt ID: [Library ID of the prompt used]
  Input variables: [Which variables enter this step]
  Output: [What this step produces — format and expected length]
  Quality gate: [YES — criteria] / [NO]
  Error handling: [What happens if this step fails]

Step 2–N: [Repeat for each step]

OUTPUTS:
Destination: [Where output goes — email / doc / spreadsheet / database / etc.]
Format: [Exact format of final output]
Human review required: [YES — who reviews, what they check] / [NO]

API/TOOL REQUIREMENTS:
AI model: [GPT-4o / Claude / Gemini / other]
API parameters: temperature=[X] | max_tokens=[N] | response_format=[JSON/text]
Other tools: [Zapier / Make / Python / Excel / etc.]
Estimated cost per run: [Token estimate × current pricing]
Estimated cost per month: [Runs/month × cost per run]

GOVERNANCE:
Privacy compliance: [What data privacy measures are in place]
Human oversight checkpoint: [Where and how humans review outputs]
Audit log: [How outputs are logged for review]
Off-switch: [How to disable this automation immediately if needed]
Review schedule: [When to reassess this automation]

ROLLOUT PLAN:
Phase 1 (first 2 weeks): [Manual testing on 10% of volume]
Phase 2 (weeks 3–4): [Semi-automated with full human review]
Phase 3 (month 2+): [Full automation with sampling review]

TEST CASES:
Test 1 (typical): Input: [describe] | Expected output: [describe]
Test 2 (edge case): Input: [describe] | Expected output: [describe]
Test 3 (failure case): Input: [describe] | Expected behavior: [describe]
════════════════════════════════════════════════════════════════════════
```

---

## 28.3 Responsible AI Assessment — Full Audit

Every capstone project must include a documented Responsible AI Assessment. This is worth 10 points in the assessment rubric.

### Capstone Responsible AI Assessment

```
════════════════════════════════════════════════════════════════════════
RESPONSIBLE AI ASSESSMENT
Project: [Your capstone project name]
Assessor: [Your name]
Date: [Date]
════════════════════════════════════════════════════════════════════════

SECTION 1: FAIRNESS AND BIAS
─────────────────────────────────────────────────────────────────────
Task: Run the Bias Audit Prompt (Session 25) on 3 representative outputs
from your system. Document findings below.

Output 1 — [Describe what this output was]:
Bias audit result: [PASS / CONCERNS FOUND]
Concerns identified: [List any bias flags]
Action taken: [How you addressed each concern in the prompt]

Output 2 — [Describe]:
[Repeat]

Output 3 — [Describe]:
[Repeat]

Overall bias risk level: [Low / Medium / High]
Bias guardrails added to prompts: [List specific guardrails added]

SECTION 2: DATA PRIVACY
─────────────────────────────────────────────────────────────────────
Data processed by this system:
□ Personal data of any kind: YES / NO
  If YES: What data? → Anonymization approach used: ________
□ Customer or client data: YES / NO
  If YES: Compliance measure: ________
□ Employee personal data: YES / NO
  If YES: Compliance measure: ________
□ Confidential business data: YES / NO
  If YES: Handling approach: ________
□ Data subject to regulations (GDPR, HIPAA, etc.): YES / NO
  If YES: Regulations applicable and compliance measures: ________

AI tool used: [ChatGPT / Claude / Copilot / other]
Data retention policy of this tool: [What does the provider retain?]
Steps taken to minimize data exposure: [List specific steps]

SECTION 3: TRANSPARENCY AND DISCLOSURE
─────────────────────────────────────────────────────────────────────
Who will receive AI-generated outputs from this system?
[Internal team / External clients / Both / End customers]

Disclosure approach:
□ Recipients will be informed that AI assisted in producing outputs
□ All AI outputs reviewed by a qualified professional before use
□ AI cannot be cited as a source in any output document
□ Any regulated outputs (legal, medical, financial) reviewed by licensed professional

Disclosure statement (if needed): [The specific statement you will use
when disclosing AI assistance to relevant stakeholders]

SECTION 4: ACCOUNTABILITY
─────────────────────────────────────────────────────────────────────
Who is accountable for outputs from this system?
[Name, role]

Human review process:
Every output is reviewed by: [Who]
Review checklist for reviewers: [List 3–5 things reviewers check]

Escalation path if AI output is clearly wrong:
[What process do you follow to correct and prevent recurrence?]

SECTION 5: RISK SUMMARY
─────────────────────────────────────────────────────────────────────
Overall responsible AI risk level: [Low / Medium / High]
Justification: [2–3 sentences]

Top 2 residual risks accepted:
Risk 1: [Describe] | Accepted because: [Reason]
Risk 2: [Describe] | Accepted because: [Reason]

Final sign-off:
I confirm this system has been assessed for responsible AI compliance
and all identified risks have been addressed or consciously accepted.
Signed: _________________ Date: _________
════════════════════════════════════════════════════════════════════════
```

---

## 28.4 Quality Evaluation — Scoring All Outputs

Use this master quality evaluation process to score your complete capstone system.

### Master Quality Evaluation Protocol

```
Run the Quality Evaluation for each of your 10 prompt library entries:

For each prompt, generate 3 outputs using different inputs.
Score each on your domain-appropriate rubric (1–5 per criterion).
Calculate: Average score across 3 runs.

QUALITY SUMMARY TABLE:
| Prompt ID | Name | Run 1 | Run 2 | Run 3 | Average | Pass? (≥3.0) |
|-----------|------|-------|-------|-------|---------|-------------|
| PROMPT-001| [name]| X/5 | X/5 | X/5 | X.X/5 | YES/NO |
[Continue for all 10 prompts]

SYSTEM QUALITY SCORE: Average of all prompts = X.X/5
(Target for certification: ≥ 3.5/5 system average)

FOR PROMPTS BELOW 3.0:
Document the specific failure mode and your diagnosis.
Attempt one more iteration (v2.0) to address the root cause.
If still below 3.0 after iteration: document the limitation honestly
and explain what would be needed to improve it further.
```

### Domain Quality Rubrics

**For Writing/Communication Outputs:**
```
Rate 1–5 on each criterion:
1. Accuracy (factually correct and complete)
2. Clarity (easy to understand without re-reading)
3. Tone (appropriate for the audience and purpose)
4. Structure (logically organized, flows well)
5. Conciseness (no unnecessary words or padding)
6. Actionability (reader knows what to do next)
Average: __/5
```

**For Analysis Outputs:**
```
Rate 1–5 on each criterion:
1. Completeness (covers all relevant aspects)
2. Specificity (concrete, not generic)
3. Evidence quality (claims supported by specific data/examples)
4. Insight depth (goes beyond obvious observations)
5. Actionability (clear "so what" and "now what")
Average: __/5
```

**For Presentation/Content Outputs:**
```
Rate 1–5 on each criterion:
1. Hook strength (would this stop the audience?)
2. Structure clarity (easy to follow narrative)
3. Message quality (memorable, specific takeaways)
4. Audience fit (right level, right tone)
5. Visual potential (could this be designed well?)
Average: __/5
```

---

## 28.5 After-State Measurement

Now that your system is built and tested, measure the after-state for each task you baselined in Session 27.

### After-State Data Collection

```
AFTER-STATE MEASUREMENT TABLE:

For each task:
Task: [Name]
Before time per run: [From Session 27 baseline]
After time per run: [Time NOW using your AI system]
Time savings per run: [Before - After]
Time savings per week: [Savings per run × frequency]

Before quality score (1–5): [From Session 27 baseline]
After quality score (1–5): [Evaluated against same rubric]
Quality delta: [After - Before]

Before capability: [Could you do this at all before? How well?]
After capability: [New tasks now enabled that were not feasible before]
```

### Impact Summary — For Presentation

```
Help me write the impact summary section for my capstone presentation.

Here is my before/after data:
[PASTE YOUR COMPLETE BEFORE/AFTER TABLE]

Generate:
1. HEADLINE IMPACT STATEMENT (1 sentence — the most compelling number)
2. IMPACT VISUALIZATION:
   - Weekly time savings: [hours] → equivalent to [describe in human terms]
   - Monthly time savings: [hours]
   - Annual time savings at this rate: [hours / working days]
3. QUALITY IMPROVEMENT NARRATIVE:
   - Where quality improved most significantly (which tasks)
   - What was enabled that wasn't possible before (new capabilities)
4. ROI STATEMENT:
   If I valued my time at [HOURLY RATE], this system saves approximately
   [₹ / $ amount] per month in labor value.
5. CONFIDENT CLAIM (what I can now say with evidence):
   "[Specific, credible claim about impact — grounded in your data]"
```

---

## 28.6 Library Completion — Final 10+ Entries

### Library Completeness Check

Run this audit before declaring your library complete:

```
PROMPT LIBRARY COMPLETENESS AUDIT

Total entries: _______ (minimum: 10 Active entries)
Entries by technique:
  Zero-shot: _______
  Few-shot: _______
  Chain-of-Thought: _______
  Persona: _______
  Multi-step chain: _______
  Advanced (RAG/ToT/ReAct): _______

Technique coverage check:
□ At least 3 different techniques represented
□ At least 1 multi-step pipeline (minimum 4 steps)
□ At least 1 advanced framework (beyond CRAFT + basic techniques)

Documentation completeness:
□ All entries have complete metadata (no empty required fields)
□ All entries have at least 1 tested example input and output
□ All entries have iteration history (minimum v1.0 → v1.1)
□ Library Index updated and accurate
□ Governance document completed

Quality threshold:
□ Average quality score across all prompts ≥ 3.5/5
□ No Active prompt below 3.0/5 without documented explanation

STATUS: COMPLETE / NEEDS WORK
Items to address before Session 29: [LIST]
```

---

## 28.7 Session 28 Deliverables

```
BY END OF SESSION 28, COMPILE:

□ Prompt Library — 10+ complete entries (library standard)
□ Library Index — Updated with all entries
□ Pipeline Design Document — Finalized
□ Automation Specification — Complete
□ Responsible AI Assessment — All 5 sections completed
□ Quality Evaluation Summary Table — All prompts scored
□ Before/After Impact Data — Complete table
□ Impact Summary — Ready for presentation
□ Deliverables Package — All documents organized and named consistently
```

---

## Hands-On Activities — Session 28

---

### Activity 28.1 — Build Prompts 6–10

Using the advanced layer prompt types (Section 28.1), build your remaining 5+ prompts. Follow the same 5-step Build Protocol from Session 27 for each.

Do not skip the test-and-iterate steps. Every prompt needs at minimum a v1.0 and v1.1.

---

### Activity 28.2 — Complete the Automation Specification

Fill in the full Automation Specification document (Section 28.2) for your primary automated workflow. If you are in Track A (Personal Productivity), this is your daily planning or end-of-day capture automation. If Track B/C/D, this is your core production pipeline.

---

### Activity 28.3 — Full Responsible AI Assessment

Complete all 5 sections of the Responsible AI Assessment (Section 28.3). Do not rush through it. The bias audit requires actually running the audit prompt on 3 of your outputs.

If the audit reveals any concerns: fix the prompt (add guardrail), re-test, and document the fix.

---

### Activity 28.4 — After-State Measurement

Time yourself running each of the tasks from your baseline using your AI system. Record the after-state data. Calculate savings.

Run the Impact Summary prompt (Section 28.5) to prepare your impact narrative for the presentation.

---

### Activity 28.5 — Library Completeness Audit

Run the Library Completeness Check (Section 28.6). Address every item flagged as incomplete before moving to Session 29.

---

## Key Takeaways — Session 28

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 28 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ 5 advanced prompt types complete the library: edge case handler, │
│    audience adapter, batch template, quality improver, chain connector│
│                                                                      │
│  ✓ Automation Specification: complete enough for a developer or     │
│    no-code tool to implement without asking you questions           │
│                                                                      │
│  ✓ Responsible AI Assessment: 5 sections, signed — this is your    │
│    professional accountability document for this system             │
│                                                                      │
│  ✓ After-state measurement: only meaningful when compared to a      │
│    documented before-state — both are required for impact claim     │
│                                                                      │
│  ✓ System Quality Score ≥ 3.5/5 average across all prompts        │
│    Iterate any prompt below 3.0 before declaring it Active          │
│                                                                      │
│  ✓ Session 28 exit: all deliverables compiled and organized —      │
│    Session 29 is presentation building, not content building        │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 28 Complete → Proceed to Session 29: Capstone Presentation Preparation*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
