# Session 21: Multi-Step AI Workflows
## Module 5 — Advanced Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 21 OF 30  │  Module 5, Session 1                          │
│  Topic: Multi-Step AI Workflows — Chaining Prompts for Complex Tasks│
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Design multi-step prompt chains for complex professional tasks
2. Apply the pipeline architecture: sequential, parallel, and conditional chains
3. Use context injection to carry information between prompt steps
4. Build a content production pipeline from brief to published asset
5. Design a research-to-report pipeline with quality gates
6. Implement error handling and quality checks within prompt chains

---

## 21.1 Why Multi-Step Workflows?

Single prompts have fundamental limitations for complex tasks:

```
PROBLEM WITH SINGLE COMPLEX PROMPTS:
─────────────────────────────────────────────────────
1. ATTENTION DILUTION: When asked to do 8 things at once, the model
   allocates limited attention across all 8. Each gets ~12% of focus.
   Result: shallow output across all dimensions.

2. CONTEXT OVERFLOW: Complex outputs require a full context window.
   If the prompt is long, less room remains for generation quality.

3. UNVERIFIABLE STEPS: You can't catch errors in intermediate steps
   because you never see them — only the final output.

4. NO COURSE CORRECTION: If step 3 of a 10-step process is wrong,
   you've wasted all 10 steps. With a pipeline, you catch it at step 3.

SOLUTION: PROMPT CHAINS
─────────────────────────────────────────────────────
Each prompt does one thing well. Output of step N becomes input to step N+1.
You see, verify, and approve each step before proceeding.
Quality compounds across steps rather than averaging down.
```

---

## 21.2 Chain Architecture Types

### Type 1: Sequential Chain

Each step feeds directly into the next. The classic pipeline.

```
Input → [Step 1] → Output 1 → [Step 2] → Output 2 → [Step 3] → Final Output
```

**Best for:** Linear processes where each step builds on the previous (research → outline → draft → polish).

### Type 2: Parallel Chain

Multiple prompts run independently on the same input, then results are synthesized.

```
         ┌──[Step 1A: Expert A perspective]──┐
Input ───┤──[Step 1B: Expert B perspective]──├──[Synthesis Step]──→ Output
         └──[Step 1C: Expert C perspective]──┘
```

**Best for:** Multi-perspective analysis, A/B variation generation, cross-domain evaluation.

### Type 3: Conditional Chain

The next step depends on the output of the previous step.

```
Input → [Step 1: Classify] → IF Category A → [Step 2A]
                           → IF Category B → [Step 2B]
                           → IF Category C → [Step 2C]
```

**Best for:** Triage systems, adaptive content generation, support ticket routing.

### Type 4: Recursive / Iterative Chain

A prompt loop that refines output until a quality threshold is met.

```
Input → [Generate] → [Evaluate Quality] → IF below threshold → [Refine] → [Evaluate]
                                         → IF above threshold → Output
```

**Best for:** High-quality content generation, prompt optimization, code refinement.

---

## 21.3 The Content Production Pipeline

A complete example of a sequential chain for professional content production.

**Goal:** Transform a rough idea into a published-ready LinkedIn article.

---

**STEP 1 — Idea Validation and Expansion**

```
You are a content strategist who evaluates LinkedIn article ideas for engagement potential.

My rough idea: [DESCRIBE IN 2–3 SENTENCES]
My audience: [WHO FOLLOWS ME / WHO I WANT TO REACH]
My purpose: [THOUGHT LEADERSHIP / LEAD GENERATION / COMMUNITY BUILDING]

Evaluate and expand this idea:
1. ANGLE ASSESSMENT: Is this angle original? What would make it more distinctive?
2. AUDIENCE FIT: Will this resonate with my described audience? Why/why not?
3. REFINED THESIS: Rewrite my idea as a sharp, specific thesis statement (1 sentence)
4. HOOK OPTIONS: 3 opening hook options (one statistic, one story, one contrarian claim)
5. GO / REFINE / DISCARD: Recommendation with rationale

Output this evaluation before I proceed to the next step.
```

**STEP 2 — Structured Outline** *(uses Step 1 output)*

```
Based on this validated idea and thesis:
Thesis: [PASTE STEP 1 REFINED THESIS]
Selected hook: [PASTE CHOSEN HOOK FROM STEP 1]

Build a detailed outline for a 1,000-word LinkedIn article:
- Title (2 options: one curiosity-driven, one benefit-driven)
- Introduction structure (hook → context → thesis → promise)
- 4–5 main sections with H2 titles (each as a complete, compelling statement)
- For each section: 2–3 bullet points of the specific content to include
- Conclusion structure (synthesis → insight → call to engagement)

The outline should create narrative momentum — each section should
make the reader want to read the next one.
```

**STEP 3 — First Draft: Sections 1 & 2** *(uses Step 2 outline)*

```
Write sections 1 and 2 of my LinkedIn article using this outline:
[PASTE STEP 2 OUTLINE]

Rules:
- First person ("I") voice throughout
- Short paragraphs: 2–3 sentences maximum
- Every claim supported by a specific example, statistic, or anecdote
- No buzzwords: "game-changer," "synergy," "leverage," "disruption"
- Active voice only
- Target: 200–250 words for these two sections combined
```

**STEP 4 — First Draft: Sections 3, 4 & Conclusion** *(continues)*

```
Continue writing my LinkedIn article. Here is what's been written:
[PASTE TITLE + INTRO + SECTIONS 1 & 2]

Now write sections 3, 4, and the conclusion following the same outline.
Maintain identical tone, paragraph length, and style.
Conclusion: synthesize the key insight → memorable closing line → engagement CTA
(CTA should be a specific question that invites comments — not "What do you think?")

Target: 300–350 words for sections 3, 4, and conclusion.
```

**STEP 5 — Self-Critique and Polish** *(full draft)*

```
Here is my complete LinkedIn article draft:
[PASTE FULL DRAFT]

Critique and improve it:

CRITIQUE (score each 1–10):
- Hook strength: does it stop the scroll?
- Thesis clarity: is the core argument crystal clear?
- Evidence quality: are claims supported specifically?
- Flow: does each section lead naturally to the next?
- Voice consistency: does it sound like one person throughout?
- Ending: does the conclusion leave a memorable impression?

IMPROVEMENTS:
- Rewrite the weakest paragraph (lowest score)
- Suggest 2 places where a specific example could replace a general claim
- Propose a stronger final sentence for the CTA

METADATA:
- Suggested LinkedIn hashtags (5)
- Optimal publishing day/time recommendation with rationale
```

---

## 21.4 The Research-to-Report Pipeline

**Goal:** Transform raw notes and sources into a polished client-ready report.

```
STEP 1: Source Processing
For each source, run: [Source Summarization Prompt from Session 11]
Output: Structured summaries (one per source)

STEP 2: Synthesis
Run: [Multi-source synthesis prompt]
Input: All source summaries
Output: Thematic synthesis with consensus, conflicts, gaps

STEP 3: Report Structure
"Based on this synthesis: [paste]
And this brief: [client objective + audience + deliverable format]
Generate a complete report outline with section titles (as message headlines),
purpose of each section, recommended length, and key content points."

STEP 4: Section Drafting
For each section (run separately):
"Write [SECTION TITLE] of this report.
Context: [executive summary so far + relevant synthesis points]
Target: [word count]
Format: [structure for this section]"

STEP 5: Executive Summary
"Based on the complete report: [paste all sections]
Write the executive summary (last written, first read):
[Executive summary prompt from Session 12]"

STEP 6: Final Consistency Polish
"Review this complete report for:
Consistency of tense, terminology, tone, and formatting.
List all inconsistencies with location and correction."

STEP 7: Client Deliverable Formatting
"Convert the polished report into an executive brief
[Executive brief template from Session 12]
And generate: 5 LinkedIn post ideas based on key report insights."
```

---

## 21.5 Context Injection — Carrying Information Between Steps

The key technical skill in multi-step workflows: what to carry forward and how.

### What to Carry Forward

```
ALWAYS carry forward:
✓ The core brief / objective (so every step stays aligned)
✓ Key constraints (audience, tone, word count, format)
✓ Key terms and definitions (consistency across steps)
✓ The output of the immediately preceding step

CARRY FORWARD SELECTIVELY:
~ Earlier steps: include summary or the specific relevant portion
~ Long outputs: paste the key section, not the full text
~ Established decisions: a brief "previously decided: X" note

DO NOT carry forward:
✗ Everything from every previous step (context window pollution)
✗ Failed drafts or rejected options
✗ Meta-commentary about the process
```

### Context Injection Template

```
CONTEXT BRIEF (carry at top of every step):
──────────────────────────────────────────
Project: [ONE-LINE DESCRIPTION]
Audience: [WHO THIS IS FOR]
Purpose: [WHAT IT MUST ACHIEVE]
Key constraints: [TONE / LENGTH / FORMAT / MUST-INCLUDE]
Previously decided: [KEY DECISIONS ALREADY MADE]
──────────────────────────────────────────

PREVIOUS STEP OUTPUT (relevant portion):
[PASTE RELEVANT OUTPUT]

CURRENT STEP TASK:
[THIS STEP'S SPECIFIC TASK]
```

---

## 21.6 Quality Gates in Pipelines

A quality gate is a checkpoint where you evaluate output before proceeding. Without gates, errors compound across steps.

### Quality Gate Prompt Template

```
Before I proceed to [NEXT STEP], evaluate the output of [CURRENT STEP]:

Output to evaluate: [PASTE OUTPUT]

Quality gate criteria for this step:
☐ Criterion 1: [SPECIFIC, BINARY — PASS or FAIL]
☐ Criterion 2: [SPECIFIC, BINARY — PASS or FAIL]
☐ Criterion 3: [SPECIFIC, BINARY — PASS or FAIL]
☐ Criterion 4: [SPECIFIC, BINARY — PASS or FAIL]

For any FAIL:
- State what was expected
- State what was produced
- Recommend the specific fix
- Indicate if this is a minor revision or requires restarting the step

Overall gate decision: PROCEED / REVISE / RESTART
```

### When to Place Quality Gates

| Step Type | Gate Needed? | What to Check |
|-----------|-------------|--------------|
| Research synthesis | YES — always | Accuracy, no hallucinated citations |
| Strategic framework | YES | Specificity, not generic statements |
| First draft (any) | YES — light | Structure, tone, completeness |
| Subsequent drafts | OPTIONAL | Improvement from previous version |
| Final polish | YES — thorough | All quality dimensions |
| Code generation | YES — always | Logic, edge cases, runs without error |

---

## 21.7 Programmatic Pipeline (Python)

For teams building systematic AI workflows programmatically:

```python
from openai import OpenAI
from typing import Callable

client = OpenAI()


class PromptPipeline:
    """
    A sequential prompt pipeline that carries context between steps
    and supports quality gate evaluation.

    Example usage:
        pipeline = PromptPipeline(model="gpt-4o")
        pipeline.add_step("ideation", ideation_prompt)
        pipeline.add_step("outline", outline_prompt, gate=outline_gate_fn)
        pipeline.add_step("draft", draft_prompt)
        result = pipeline.run(initial_input="Write about AI in healthcare")
    """

    def __init__(self, model: str = "gpt-4o", temperature: float = 0.7):
        self.model = model
        self.temperature = temperature
        self.steps: list[dict] = []
        self.outputs: dict[str, str] = {}
        self.context_brief: str = ""

    def set_context_brief(self, brief: str) -> None:
        """Set a persistent context brief injected at every step."""
        self.context_brief = brief

    def add_step(
        self,
        step_name: str,
        prompt_template: str,
        gate: Callable[[str], tuple[bool, str]] | None = None,
        temperature: float | None = None
    ) -> None:
        """
        Add a step to the pipeline.

        Args:
            step_name: Unique identifier for this step
            prompt_template: Prompt text with {previous_output} placeholder
            gate: Optional quality gate function returning (passed: bool, feedback: str)
            temperature: Override temperature for this step
        """
        self.steps.append({
            "name": step_name,
            "prompt_template": prompt_template,
            "gate": gate,
            "temperature": temperature or self.temperature
        })

    def _run_step(self, prompt: str, temperature: float) -> str:
        """Execute a single prompt and return the response."""
        response = client.chat.completions.create(
            model=self.model,
            messages=[{"role": "user", "content": prompt}],
            temperature=temperature
        )
        return response.choices[0].message.content

    def run(self, initial_input: str, max_gate_retries: int = 2) -> dict:
        """
        Execute the full pipeline.

        Args:
            initial_input: The starting input for step 1
            max_gate_retries: How many times to retry a failed quality gate

        Returns:
            Dictionary of all step outputs
        """
        current_input = initial_input

        for step in self.steps:
            print(f"\n{'='*50}")
            print(f"STEP: {step['name']}")
            print(f"{'='*50}")

            # Build prompt with context brief and previous output
            prompt = f"{self.context_brief}\n\n{step['prompt_template']}".format(
                previous_output=current_input
            )

            retries = 0
            while True:
                output = self._run_step(prompt, step["temperature"])
                print(f"Output preview: {output[:200]}...")

                # Run quality gate if defined
                if step["gate"]:
                    passed, feedback = step["gate"](output)
                    if passed:
                        print(f"✅ Quality gate PASSED")
                        break
                    elif retries < max_gate_retries:
                        print(f"⚠️  Quality gate FAILED: {feedback}")
                        print(f"Retrying... ({retries + 1}/{max_gate_retries})")
                        prompt += f"\n\nPREVIOUS ATTEMPT FEEDBACK: {feedback}\nPlease address this in your revised output."
                        retries += 1
                    else:
                        print(f"❌ Quality gate failed after {max_gate_retries} retries. Proceeding with best output.")
                        break
                else:
                    break  # No gate — always proceed

            self.outputs[step["name"]] = output
            current_input = output

        return self.outputs


# ── Example Gate Function ──────────────────────────────────────────────────
def check_has_sections(output: str) -> tuple[bool, str]:
    """
    Simple quality gate: check that the output has at least 3 sections
    indicated by numbered points or headers.
    """
    has_sections = (
        output.count("\n\n") >= 3 or
        any(f"{i}." in output for i in range(1, 6))
    )
    if has_sections:
        return True, "Structure check passed"
    return False, "Output appears to lack clear sections. Add numbered sections or clear paragraph breaks."


# ── Example Pipeline Usage ────────────────────────────────────────────────
if __name__ == "__main__":
    pipeline = PromptPipeline(model="gpt-4o", temperature=0.7)

    pipeline.set_context_brief(
        "PROJECT: Blog post for a B2B SaaS marketing audience.\n"
        "AUDIENCE: Marketing managers at 50-200 person tech companies.\n"
        "TONE: Professional but conversational. First person. No buzzwords."
    )

    pipeline.add_step(
        "ideation",
        "Generate 3 unique angles for a blog post on this topic: {previous_output}\n"
        "For each angle: thesis (1 sentence) + hook (1 sentence) + why it's original."
    )

    pipeline.add_step(
        "outline",
        "Using the best angle from: {previous_output}\n"
        "Write a detailed 6-section outline with message headline titles.",
        gate=check_has_sections
    )

    pipeline.add_step(
        "draft",
        "Write the full blog post from this outline: {previous_output}\n"
        "Target 800 words. Follow the established tone exactly.",
        temperature=0.8
    )

    results = pipeline.run("AI tools for B2B marketing teams")
    print("\n\nFINAL OUTPUT:")
    print(results["draft"])
```

---

## Hands-On Activities — Session 21

---

### Activity 21.1 — Run the Content Production Pipeline

**Objective:** Experience a full 5-step sequential chain.

**Step 1:** Choose a topic you know well and have a genuine opinion on.

**Step 2:** Run all 5 steps of the Content Production Pipeline (Section 21.3) in sequence.

**Step 3:** After each step, evaluate: Is this output good enough to feed into the next step? If not, revise before continuing.

**Deliverable:** A complete, polished 1,000-word LinkedIn article produced through the pipeline.

**Reflection:** At which step did quality improve the most? Which step was the most critical to get right?

---

### Activity 21.2 — Design a Custom Pipeline

**Objective:** Build a multi-step pipeline for a recurring task in your role.

Think of any complex task you repeat regularly. Design a pipeline for it with:
- 4–6 steps
- Step name and purpose for each
- What gets carried forward from each step
- A quality gate for at least 2 steps (what you check and what constitutes a pass)

Write this as a reference document you could actually use.

---

### Activity 21.3 — Parallel Chain Analysis

**Objective:** Experience the multi-perspective power of parallel chains.

Choose a strategic question facing your organization (or use: "Should a mid-size Indian IT services company expand into the US market?").

Run 3 simultaneous prompts, each with a different expert persona:
- CFO perspective (financial risk and return)
- Chief Strategy Officer perspective (market positioning and competitive dynamics)
- CHRO perspective (talent and organizational readiness)

Then run a synthesis step:
```
"Given these three expert perspectives: [paste all three]
Synthesize into a unified recommendation that weighs all three viewpoints.
Where perspectives conflict, acknowledge the tension and recommend how to resolve it."
```

---

### Activity 21.4 — Quality Gate Practice

**Objective:** Build quality gate checkpoints for a pipeline.

For the pipeline you designed in Activity 21.2, build a detailed quality gate for each identified checkpoint:
- 4–5 binary pass/fail criteria per gate
- Specific failure response (what to do if it fails)
- Maximum retries before accepting and moving on

---

## Revision Questions — Session 21

1. What are the 4 limitations of single complex prompts that multi-step pipelines solve?
2. Describe the 4 chain architecture types. Give a professional use case for each.
3. What is context injection and why is it the most important skill in pipeline design?
4. What should always be carried forward between steps? What should never be carried forward?
5. What is a quality gate? Describe where in a content pipeline you would place gates and what each would check.
6. What is the difference between a sequential and a conditional chain? Give an example of when conditional branching is valuable.
7. Describe the Content Production Pipeline. What does each of the 5 steps accomplish?
8. A colleague complains that their AI pipeline produces great results in step 1 but the final output is poor. What are the most likely causes and what would you diagnose first?

---

## Key Takeaways — Session 21

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 21 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Multi-step chains solve attention dilution, error compounding,  │
│    and unverifiable intermediate steps                              │
│                                                                      │
│  ✓ 4 chain types: Sequential | Parallel | Conditional | Iterative  │
│    Match the architecture to the task structure                     │
│                                                                      │
│  ✓ Context injection: carry project brief + constraints + previous  │
│    step output at every step — trim aggressively                    │
│                                                                      │
│  ✓ Quality gates are mandatory for professional pipelines —         │
│    PASS/FAIL criteria at each critical step                         │
│                                                                      │
│  ✓ The Content Production Pipeline: 5 steps from idea to published │
│    LinkedIn article — each step earns the right to the next         │
│                                                                      │
│  ✓ Programmatic pipelines (Python) scale multi-step workflows       │
│    across hundreds of inputs with consistent quality control        │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 21 Complete → Proceed to Session 22: Advanced Prompt Frameworks*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
