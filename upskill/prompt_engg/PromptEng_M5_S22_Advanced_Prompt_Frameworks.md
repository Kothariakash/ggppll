# Session 22: Advanced Prompt Frameworks
## Module 5 — Advanced Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 22 OF 30  │  Module 5, Session 2                          │
│  Topic: Advanced Prompt Frameworks — Beyond CRAFT                   │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Apply 6 advanced prompt frameworks beyond CRAFT for specialized tasks
2. Use the Tree of Thought framework for complex multi-path reasoning
3. Apply Retrieval-Augmented Generation (RAG) principles in manual workflows
4. Use the ReAct framework for iterative reasoning and action
5. Build meta-prompts that generate and improve other prompts
6. Select the right framework for each task type using a decision matrix

---

## 22.1 The Framework Landscape

As prompt engineering matures, researchers and practitioners have developed specialized frameworks that outperform general-purpose prompting for specific task types:

```
FRAMEWORK          BEST FOR                          KEY MECHANISM
─────────────────  ───────────────────────────────   ──────────────────────────
CRAFT              All professional tasks            Structured 5-element prompt
Chain-of-Thought   Reasoning and math                Show step-by-step thinking
Tree of Thought    Complex decisions with options    Explore multiple paths
ReAct              Iterative tasks with feedback     Reason → Act → Observe loop
RAG Principles     Knowledge-grounded responses      Ground in provided sources
APE                Prompt generation                 AI writes and optimizes prompts
Skeleton-of-Thought Long structured documents        Outline first, fill in parallel
Metacognitive       Self-aware reasoning             AI monitors its own thinking
```

---

## 22.2 Tree of Thought (ToT)

**What it is:** Instead of one linear reasoning chain, Tree of Thought explores multiple possible reasoning paths simultaneously — like a decision tree — then selects the most promising path.

**Introduced by:** Yao et al., 2023 — demonstrated significant improvements over CoT on complex planning, creative writing, and game-solving tasks.

### Why ToT Outperforms CoT

```
CHAIN-OF-THOUGHT:
Problem → Step 1 → Step 2 → Step 3 → Answer
         (If Step 1 direction is wrong, all subsequent steps compound the error)

TREE OF THOUGHT:
                    ┌─ Path A: Step 1a → Step 2a → Evaluate → [PRUNED]
Problem → Branch ───┤
                    ├─ Path B: Step 1b → Step 2b → Evaluate → [SELECTED]
                    │
                    └─ Path C: Step 1c → Step 2c → Evaluate → [PRUNED]
                    
Best path continues → Final Answer
(Wrong paths are pruned early; best path gets full focus)
```

### ToT Prompt Template

```
Solve the following problem using Tree of Thought reasoning.

Problem: [DESCRIBE THE PROBLEM]

Step 1 — BRANCH: Generate 3 distinct approaches or solution paths.
For each path: Name it, describe the core logic in 2 sentences, and identify
its key assumption.
  Path A: [Name and logic]
  Path B: [Name and logic]
  Path C: [Name and logic]

Step 2 — EVALUATE: Score each path on:
- Feasibility (how likely it is to work): 1–5
- Completeness (does it fully address the problem): 1–5
- Risk (what could go wrong): 1–5 (5 = lowest risk)
Present as a score table.

Step 3 — SELECT: Choose the path with the highest total score.
Justify the selection in 2 sentences.

Step 4 — DEVELOP: Follow the selected path to its full solution.
Show each sub-step and its output.

Step 5 — VERIFY: Check the solution against the original problem.
Does it fully resolve the problem? If not, what adjustment is needed?
```

### ToT Applied — Strategic Decision Example

```
Use Tree of Thought to decide how [COMPANY] should respond to a
new competitor who has entered our market with 30% lower pricing.

Step 1 — BRANCH: Three distinct strategic response paths:
Path A: Price Match — meet their price across our product line
Path B: Differentiation — double down on premium value and service
Path C: Segment Retreat — cede price-sensitive customers, focus on enterprise

Step 2 — EVALUATE each path on:
- Short-term revenue impact
- Long-term brand/margin impact
- Operational feasibility
- Customer retention probability
Score each 1–5, total out of 20.

Step 3 — SELECT the highest-scoring path with rationale.

Step 4 — DEVELOP: Build a 90-day implementation plan for the selected path,
including: key actions, resources needed, success metrics, and trigger points
that would cause us to reconsider.

Step 5 — VERIFY: What is the one scenario where this strategy fails?
How would we detect it early and what's the contingency?

Company context: [DESCRIBE YOUR COMPANY, MARKET POSITION, AND RESOURCES]
```

---

## 22.3 ReAct Framework (Reason + Act)

**What it is:** The ReAct (Reasoning + Acting) framework alternates between reasoning about what to do next and taking an action — then observing the result — in an iterative loop. Originally designed for AI agents with tool access, it applies equally to manual research and complex problem-solving.

```
ReAct Loop:
Thought: What do I know? What should I do next?
    ↓
Action: Take the next step (research, calculate, draft, test)
    ↓
Observation: What did the action reveal? Does this change my plan?
    ↓
Thought: Given this observation, what's next?
    ↓
(Repeat until task complete)
```

### ReAct Prompt — Research and Analysis Task

```
Use ReAct reasoning to investigate the following question.
For each cycle, explicitly state: Thought → Action → Observation.
Continue until you reach a well-supported conclusion.

Question: [YOUR RESEARCH OR ANALYSIS QUESTION]

Available information: [ANY CONTEXT OR DATA YOU CAN PROVIDE]

Begin the ReAct loop:

THOUGHT 1: What do I already know about this question? What is the most
important thing I need to find out first?

ACTION 1: [Describe what you would look up, calculate, or investigate]
(If the information is in my context: use it. If not: state what source
type would provide it and what it likely contains based on general knowledge,
clearly flagged as estimated.)

OBSERVATION 1: [What does the action reveal?]

THOUGHT 2: Given what I just learned, what should I investigate next?
Does this change my initial assumptions?

ACTION 2: [Next investigation]

OBSERVATION 2: [What this reveals]

[Continue for 4–6 cycles]

FINAL CONCLUSION:
Based on my Thought-Action-Observation sequence:
- Main finding: [1–2 sentences]
- Confidence level: [High / Medium / Low] and why
- What I would still need to verify independently
```

### ReAct Applied — Business Problem Diagnosis

```
Apply ReAct reasoning to diagnose the following business problem.
Work through the diagnostic process step by step.

Problem: Our customer churn rate increased from 4% to 7% MoM in the last quarter.
Revenue impact: approximately ₹40 lakh/month in lost recurring revenue.

Available data:
- Churn is highest in our SMB segment (under 50 users)
- Enterprise segment churn is unchanged
- Net Promoter Score dropped from 42 to 31 in the same period
- We launched a major product update 4 months ago
- Two competitors reduced pricing by 15% and 20% respectively 3 months ago
- Customer support ticket volume increased 35% in the same quarter
- Agent-reported most common complaint: "product is slower than it used to be"

THOUGHT 1: What are the most likely causes based on this data?
ACTION 1: Analyze which data points are most correlated with churn increase
OBSERVATION 1: [What does the pattern suggest?]

THOUGHT 2: Which cause should I investigate first and what evidence would confirm it?
[Continue ReAct cycles until root cause is identified]

FINAL DIAGNOSIS:
- Root cause (most likely)
- Supporting evidence from the data
- Recommended first 3 actions this week
- What additional data would confirm the diagnosis
```

---

## 22.4 Retrieval-Augmented Generation (RAG) Principles

**What it is:** RAG is an architecture where an AI retrieves relevant information from a knowledge base before generating its response — ensuring answers are grounded in real, current, verified data rather than training knowledge.

In practice for prompt engineers (without building a full RAG system), you apply the core principle manually:

**RAG Principle:** Provide the relevant context/documents IN the prompt → instruct the AI to use ONLY that context → get grounded, verifiable responses.

### Manual RAG Prompt Pattern

```
You are a [ROLE] answering questions based only on the provided source material.

CRITICAL RULES:
- Answer ONLY using information from the SOURCE MATERIAL below
- If the answer is not in the source material, say: "The provided documents
  do not contain this information."
- Do not use your general knowledge — only the sources
- Cite the source (e.g., "According to Section 2 of the Policy Document...")
  for every factual claim
- If sources conflict, note the conflict and state both positions

SOURCE MATERIAL:
─────────────────────────────────────────────
[PASTE YOUR DOCUMENTS HERE]
Document 1: [Title] — [Content]
Document 2: [Title] — [Content]
─────────────────────────────────────────────

QUESTION: [YOUR QUESTION]
```

### RAG for Internal Knowledge Base Q&A

```
You are the AI assistant for [COMPANY NAME]. Answer employee questions
using only the following company policies and documentation.

SOURCE DOCUMENTS:
[HR Policy Manual excerpts]
[Employee Handbook sections]
[Benefits Documentation]
[IT Security Policy]

Rules:
1. Ground every answer in the specific policy document
2. Quote the exact policy language when precision matters
3. If a question falls outside the provided documents:
   "This question is outside our documented policies. Please contact
   HR directly at [contact] for guidance on [topic]."
4. Never interpret or extend policy — only state what's documented
5. If policy has changed recently and you're uncertain, say so

Employee question: [PASTE QUESTION]
```

### RAG for Competitive Intelligence

```
Analyze the following competitor earnings call transcript and press releases.
Answer my questions using ONLY information from these provided documents.
Do not add any information from your general knowledge about this company.

SOURCE 1 — Q3 Earnings Call Transcript: [PASTE]
SOURCE 2 — Recent Press Release: [PASTE]
SOURCE 3 — Annual Report Excerpt: [PASTE]

Answer the following questions, citing your source for each answer:
1. What was their stated revenue for the most recent quarter?
2. Which product lines are growing and which are declining?
3. What strategic initiatives did management mention for next year?
4. What risks did management acknowledge?
5. What did management NOT discuss that competitors typically do?
```

---

## 22.5 Automatic Prompt Engineering (APE) — Meta-Prompts

**What it is:** Using AI to generate, evaluate, and optimize prompts — rather than writing them yourself. The AI becomes a prompt engineer.

### Meta-Prompt: Generate Better Prompts

```
You are an expert prompt engineer who specializes in writing prompts
that produce consistent, high-quality outputs from large language models.

I need a prompt for the following task:
Task: [DESCRIBE WHAT THE PROMPT SHOULD ACCOMPLISH]
Input: [WHAT DATA/CONTENT WILL BE PROVIDED TO THIS PROMPT]
Output: [WHAT THE IDEAL OUTPUT LOOKS LIKE — describe in detail]
Use case: [WHO WILL USE THIS — professional context]
Failure modes to avoid: [WHAT COMMONLY GOES WRONG WITH THIS TYPE OF TASK]

Generate 3 versions of this prompt:
VERSION A: Zero-shot approach (instruction only)
VERSION B: Few-shot approach (instruction + 1 example)
VERSION C: Chain-of-thought approach (instruction + reasoning steps)

For each version:
- The complete, ready-to-use prompt (with variable placeholders in [BRACKETS])
- Why this approach is appropriate
- Expected quality and consistency level
- When this version might fail

Then recommend which version to use first and why.
```

### Meta-Prompt: Improve an Existing Prompt

```
You are a senior prompt engineer reviewing and improving a draft prompt.

DRAFT PROMPT TO IMPROVE:
[PASTE YOUR CURRENT PROMPT]

PROBLEM WITH CURRENT PROMPT:
[DESCRIBE WHAT'S GOING WRONG — wrong format / inconsistent / wrong tone / etc.]

DESIRED OUTCOME:
[DESCRIBE WHAT PERFECT OUTPUT LOOKS LIKE]

Analyze and improve this prompt:

DIAGNOSIS:
1. What is causing the identified problem? (Root cause, not symptoms)
2. What elements of the prompt are working well? (Keep these)
3. What elements are causing the problem? (Change these)

IMPROVED PROMPT:
[Provide the rewritten prompt — complete and ready to use]

WHAT CHANGED AND WHY:
[For each change: original → revised and the specific reason]

PREDICTED IMPROVEMENT:
How confident are you this solves the stated problem? (High / Medium / Low)
What residual risk remains?

TEST CASE:
Provide a test input and expected output to validate this improved prompt.
```

### Meta-Prompt: Prompt Stress Testing

```
You are a quality assurance expert for AI prompts. Your job is to
find every way this prompt could fail before it goes into production.

PROMPT TO STRESS TEST:
[PASTE YOUR PROMPT]

Stress test this prompt across these dimensions:

1. AMBIGUITY TEST: Find every phrase in this prompt that could be
   interpreted in more than one way. For each: state the two interpretations
   and which one the AI is more likely to take.

2. EDGE CASE TEST: What inputs would break this prompt or produce
   unexpected outputs? Describe 3 edge cases.

3. ADVERSARIAL TEST: How could a user (intentionally or accidentally)
   get the AI to produce outputs that don't meet the intended goal?

4. OMISSION TEST: What important information or instruction is missing
   that a professional would assume but an AI might not?

5. OVER-CONSTRAINT TEST: Are any constraints so strict they'll prevent
   the AI from producing a good output? Which constraints should be loosened?

6. UNDER-CONSTRAINT TEST: Are any important guardrails missing that could
   let the AI produce inappropriate or off-brand output?

After the stress test: Provide the improved, hardened prompt that addresses
all identified vulnerabilities.
```

---

## 22.6 Skeleton-of-Thought Framework

**What it is:** For long, structured documents, first generate a skeleton (headings and brief content summaries), then fill each section in focused, parallel prompts. This is more efficient than sequential drafting for large documents.

```
STEP 1 — SKELETON GENERATION:
"Generate a skeleton outline for a [DOCUMENT TYPE] on [TOPIC].
For each section: heading | 3-word content summary | word count target | key point to make
Produce the full skeleton before any content is written."

STEP 2 — PARALLEL SECTION FILLING:
(Run simultaneously for each section)
"Fill in Section [N] of this document: [Section heading]
Content summary from skeleton: [paste summary]
Word count target: [N] words
Context: The full skeleton is: [paste skeleton]
Maintain consistent tone with: [paste adjacent sections already written]"

STEP 3 — INTEGRATION:
"I have filled in all sections of this [DOCUMENT TYPE].
Review the complete document for: flow, consistency, transitions.
Suggest and rewrite any transition sentences that feel abrupt."
```

---

## 22.7 Framework Selection Matrix

| Task Type | Primary Framework | Secondary Framework | Avoid |
|-----------|------------------|--------------------|----|
| Complex decisions with multiple paths | Tree of Thought | Chain-of-Thought | Zero-shot |
| Iterative diagnosis / investigation | ReAct | Chain-of-Thought | One-shot |
| Grounded Q&A on documents | RAG Principles | Chain-of-Thought | Zero-shot (hallucination risk) |
| Prompt writing and improvement | APE (Meta-prompting) | — | Random iteration |
| Large structured documents | Skeleton-of-Thought | Sequential chain | Single monolithic prompt |
| Standard professional tasks | CRAFT | Few-shot | Over-engineering |
| Math and logical reasoning | Chain-of-Thought | Self-Consistency | Zero-shot |
| Brand voice and custom formats | Few-shot | CRAFT + examples | Zero-shot |
| Strategic planning | Tree of Thought + Persona | CRAFT + CoT | Zero-shot |

---

## Hands-On Activities — Session 22

---

### Activity 22.1 — Tree of Thought Decision

**Objective:** Apply ToT to a real decision you're facing.

Choose any genuine decision: career move, business investment, process change, personal choice.

Run the full ToT prompt (5 steps). Evaluate:
- Did exploring 3 paths reveal an option you hadn't seriously considered?
- Was the evaluation step helpful or did you already know which path was best?
- Did Step 5 (verification/failure scenario) change your confidence in the selected path?

---

### Activity 22.2 — ReAct Business Diagnosis

**Objective:** Use ReAct to systematically diagnose a real or hypothetical business problem.

**Option A:** Use the churn diagnosis example from Section 22.3 as-is.

**Option B:** Use a real problem from your organization (anonymize as needed):
- A metric that moved unexpectedly
- A project that is underperforming
- A process that isn't working

Run at least 5 Thought-Action-Observation cycles. Did the iterative process help you reach a more grounded conclusion than you would have in one step?

---

### Activity 22.3 — Manual RAG Q&A System

**Objective:** Build a manually grounded knowledge base Q&A prompt.

**Step 1:** Choose a document you work with regularly (a policy, a product spec, a research report, a set of guidelines).

**Step 2:** Paste the document (or key sections) into the Manual RAG Prompt Pattern.

**Step 3:** Ask 5 questions — some answerable from the document, some not.

**Evaluate:** Did the AI correctly answer from the document? Did it correctly identify questions it couldn't answer from the provided sources? Did it hallucinate any answers?

---

### Activity 22.4 — APE: Improve Your Worst Prompt

**Objective:** Use meta-prompting to fix a prompt that isn't working well.

**Step 1:** Identify a prompt in your library that consistently underperforms.

**Step 2:** Run the Meta-Prompt: Improve an Existing Prompt (Section 22.5).

**Step 3:** Run the Meta-Prompt: Stress Test the improved version.

**Step 4:** Test the final improved prompt 3 times and score against your success criteria.

**Document:** What changed between the original and final version? What was the root cause of the original failure?

---

## Revision Questions — Session 22

1. What is Tree of Thought and how does it differ from Chain-of-Thought? Give a scenario where ToT would outperform CoT.
2. Describe the ReAct loop. What are the 3 elements of each cycle?
3. What is the core principle of RAG? How does a prompt engineer apply it without building a technical RAG system?
4. What is Automatic Prompt Engineering (APE)? What are the 3 meta-prompt types described in this session?
5. What is Skeleton-of-Thought and when is it preferable to sequential drafting?
6. A colleague's AI keeps hallucinating facts when answering questions about company policy. Which framework would you recommend and how would you implement it?
7. You need to make a complex strategic decision with several viable approaches and significant uncertainty. Which framework is most appropriate and why?
8. Describe the Prompt Stress Testing process. What 6 dimensions does it evaluate?

---

## Key Takeaways — Session 22

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 22 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Tree of Thought: 3 paths → evaluate → select → develop → verify │
│    Best for complex decisions with multiple viable approaches        │
│                                                                      │
│  ✓ ReAct: Thought → Action → Observation loop — iterative diagnosis │
│    Best for investigation, diagnosis, research with feedback         │
│                                                                      │
│  ✓ RAG principle: paste your sources → instruct to use only them   │
│    Eliminates hallucination for document-grounded Q&A               │
│                                                                      │
│  ✓ APE (meta-prompting): use AI to write and improve your prompts  │
│    Stress-testing before production saves rework downstream          │
│                                                                      │
│  ✓ Skeleton-of-Thought: outline first → fill sections in parallel  │
│    Most efficient approach for long, complex structured documents    │
│                                                                      │
│  ✓ Framework selection: match the task structure to the framework  │
│    Over-engineering simple tasks is as costly as under-engineering  │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 22 Complete → Proceed to Session 23: AI Automation*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
