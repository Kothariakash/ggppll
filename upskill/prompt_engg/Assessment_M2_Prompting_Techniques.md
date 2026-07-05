# Module 2 Assessment — Prompting Techniques
## Sessions 6–10 | Assignment Questions, MCQs & Answer Key
### Prompt Engineering Certification Program

---

> **Instructions for Students**
> - Part A: MCQ — 25 questions, 1 mark each (25 marks)
> - Part B: Short Answer Assignments — 10 questions, 2 marks each (20 marks)
> - Part C: Long Answer / Practical Assignments — 5 questions, variable marks (30 marks)
> - **Total: 75 marks | Pass: 53 marks (70%)**

---

# PART A — MULTIPLE CHOICE QUESTIONS (25 Marks)

---

**Q1.** Zero-shot prompting means:

- A) Using zero examples in the prompt and relying on the model's pre-trained knowledge
- B) Setting the temperature parameter to zero
- C) Using zero context in the prompt
- D) Running the prompt zero times before sending it to the API

---

**Q2.** Which of the following is a correctly designed few-shot example pair?

- A) Input: "Question: What is AI?" Output: "AI is a complex field."
- B) Input: "Classify: The product arrived damaged." Output: "Negative"
- C) Input: "Summarize this." Output: "Sure, here is a summary."
- D) Input: "Write an email." Output: "Email written."

---

**Q3.** In few-shot prompting, what is the MOST important quality of the examples you provide?

- A) They should be very long to give the model more to learn from
- B) They should be representative, correctly formatted, and consistently follow the pattern you want
- C) They should always include at least one example of failure
- D) They must be from the exact same industry as the target task

---

**Q4.** The phrase "Let's think step by step" is associated with which prompting technique?

- A) Zero-shot prompting
- B) Few-shot prompting
- C) Zero-shot Chain-of-Thought prompting
- D) Persona prompting

---

**Q5.** Chain-of-Thought (CoT) prompting primarily improves AI performance on:

- A) Creative writing tasks
- B) Simple factual recall questions
- C) Tasks requiring multi-step reasoning, logic, and calculation
- D) Formatting and layout tasks

---

**Q6.** Which describes the "Self-Consistency" technique in Chain-of-Thought prompting?

- A) The AI checks its own grammar before responding
- B) Generating multiple reasoning chains and selecting the most common answer across them
- C) Instructing the AI to be consistent with its persona across the conversation
- D) Running the same prompt twice and comparing outputs

---

**Q7.** What is the primary purpose of "Persona Prompting"?

- A) To make the AI's outputs longer and more detailed
- B) To assign the AI a specific identity or expertise that shapes the tone, vocabulary, and depth of its response
- C) To prevent the AI from using its own knowledge
- D) To make the AI respond in a different language

---

**Q8.** A "Persona Stack" in advanced persona prompting means:

- A) Running multiple prompts in sequence
- B) Combining multiple roles or attributes into a single, nuanced persona
- C) Stacking examples on top of each other in the few-shot format
- D) Using a stack data structure to organize prompts

---

**Q9.** Which of the following is the correct Prompt Optimization Cycle?

- A) Write → Submit → Accept → Archive
- B) Design → Test → Evaluate → Diagnose → Refine
- C) Brainstorm → Draft → Publish → Review
- D) Input → Output → Retry → Accept

---

**Q10.** "Output Anchoring" in prompt optimization means:

- A) Pinning a prompt to the top of the prompt library
- B) Fixing the output format by showing the AI the first word or structure of the expected output
- C) Anchoring the prompt to a specific API parameter
- D) Adding a constraint that prevents the output from changing between runs

---

**Q11.** When should you use Chain-of-Thought prompting instead of a simple instruction?

- A) Always — CoT always produces better results
- B) Only for math problems
- C) When the task requires multiple reasoning steps, where intermediate logic affects the final answer
- D) When you want shorter, faster responses

---

**Q12.** A few-shot prompt for sentiment classification should include examples that:

- A) Are all positive examples so the AI learns the positive class first
- B) Cover all target classes (positive, negative, neutral) with balanced representation
- C) Are from the same source as the input text
- D) Use formal academic language regardless of the target domain

---

**Q13.** What is "Prompt Decomposition" in the context of optimization?

- A) Breaking apart a poorly written prompt into its components for diagnosis
- B) Splitting a complex task into smaller, focused sub-prompts that can be chained
- C) Removing unnecessary words from a prompt to save tokens
- D) Decomposing the prompt into its CRAFT components for audit

---

**Q14.** An "Adversarial Persona" in prompt engineering is used for:

- A) Making the AI argue against the user's position
- B) Having the AI adopt a critical or opposing viewpoint to stress-test an idea
- C) Creating a persona that bypasses AI safety guidelines
- D) Training the AI to be more aggressive in tone

---

**Q15.** Which of the following is a "Negative Instruction" that improves prompt precision?

- A) "You are a negative person."
- B) "Do not begin your response with 'Certainly!' or 'Of course!'"
- C) "Do not answer this question."
- D) "Negative sentiment should be classified as 0."

---

**Q16.** What does "in-context learning" mean in the context of few-shot prompting?

- A) The model learns from examples provided within the prompt itself, without updating model weights
- B) The model is retrained with new data during the conversation
- C) The model learns from the context window across multiple conversations
- D) In-context learning is another term for fine-tuning

---

**Q17.** A "Self-Critique" prompt asks the AI to:

- A) Write a negative review of its own product
- B) Evaluate and improve its own previously generated output using a defined quality rubric
- C) Rate the quality of the user's prompt
- D) Check for grammar and spelling errors only

---

**Q18.** You are prompting an AI to write a performance review comment. Which persona would be most appropriate?

- A) "You are a creative fiction writer."
- B) "You are an experienced HR business partner with 12 years of writing performance feedback."
- C) "You are a data scientist specializing in NLP."
- D) "You are an 18th-century philosopher."

---

**Q19.** The "Scoring Rubric" technique in Prompt Optimization involves:

- A) Giving the prompt a score before submitting it
- B) Providing explicit, weighted evaluation criteria in the prompt so the AI self-evaluates its output before presenting it
- C) Scoring each token in the output for quality
- D) Applying API pricing calculations to the prompt

---

**Q20.** Few-shot prompting is particularly valuable compared to zero-shot when:

- A) The task is simple and well-known
- B) The desired output format or style is unusual or highly specific and hard to describe in words
- C) The model has been fine-tuned on similar data
- D) You want to minimize the number of tokens used

---

**Q21.** "Chain Prompting" (as an optimization technique) refers to:

- A) Using blockchain technology with AI
- B) Passing the output of one prompt as the input to the next in a deliberate sequence
- C) Chaining together multiple LLM models
- D) Connecting prompts to external databases

---

**Q22.** Which of the following correctly describes "Few-Shot CoT" (Chain-of-Thought)?

- A) Providing a few examples where each example shows the reasoning steps, not just the final answer
- B) Using a short chain-of-thought with only two reasoning steps
- C) A few-shot prompt with chain structure but no reasoning shown
- D) Combining few-shot examples with temperature = 0

---

**Q23.** What is the primary risk of using too many few-shot examples?

- A) The AI becomes confused and ignores all examples
- B) Consuming excessive context window space, leaving less room for the actual input and output
- C) The AI memorizes the examples and cannot generalize
- D) The API will reject prompts with more than 5 examples

---

**Q24.** A student uses the same generic persona ("You are an expert") across all prompts. What is wrong with this?

- A) Nothing — "expert" is sufficient for any task
- B) "Expert" is a vague role that provides no domain calibration, leaving the AI to guess what kind of expert is needed
- C) The word "expert" triggers safety filters in most models
- D) Personas should never be used in professional prompts

---

**Q25.** Which statement about Prompt Optimization is MOST accurate?

- A) A prompt that works well once should be archived and never changed
- B) The best prompts are discovered by luck through random experimentation
- C) Prompt optimization is a systematic cycle of design, test, diagnose, and refine — with each iteration targeting a specific diagnosed failure
- D) Optimization is only needed when using the API, not when using ChatGPT directly

---

# PART A — ANSWER KEY WITH EXPLANATIONS

---

**Q1. Answer: A**
*Explanation:* Zero-shot prompting provides no examples — the model must rely entirely on its pre-training to understand and perform the task. It works well for common, well-understood tasks. The "zero" refers to the number of examples (shots), not to the temperature (B) or any other parameter.

---

**Q2. Answer: B**
*Explanation:* A good few-shot example pair shows a clear, complete input and a specific, correct output that demonstrates exactly the pattern you want. "The product arrived damaged" → "Negative" is a clean sentiment classification example: concrete input, unambiguous output, no filler. Options A, C, and D all have vague or unhelpful outputs that don't demonstrate a learnable pattern.

---

**Q3. Answer: B**
*Explanation:* The quality of few-shot examples is more important than the quantity. Examples must be representative (reflect real inputs the model will face), correctly formatted (show the exact output format you want), and consistently follow the same pattern (so the model can extract the rule). A single high-quality example often outperforms five mediocre ones.

---

**Q4. Answer: C**
*Explanation:* "Let's think step by step" is the canonical zero-shot Chain-of-Thought trigger phrase identified by Kojima et al. (2022). It instructs the model to generate a reasoning chain before giving the final answer, without requiring any example reasoning chains in the prompt (which would make it few-shot CoT).

---

**Q5. Answer: C**
*Explanation:* CoT is specifically designed for tasks where the correct answer depends on correctly executing multiple intermediate reasoning steps — math word problems, logical inference, multi-condition classification, process debugging. For simple factual recall (B), a direct answer is faster. For creative writing (A), CoT adds unnecessary rigidity. CoT does not assist with formatting (D).

---

**Q6. Answer: B**
*Explanation:* Self-Consistency (Wang et al., 2022) improves on basic CoT by generating multiple independent reasoning paths (at higher temperature) and then selecting the most frequently occurring final answer across those paths. This mirrors how humans check their work — if 4 of 5 reasoning approaches lead to the same answer, that answer is more likely correct.

---

**Q7. Answer: B**
*Explanation:* Persona prompting assigns the AI a specific identity — which calibrates its vocabulary, assumed expertise level, communication style, and perspective. "You are a senior tax attorney" produces dramatically different output than "you are an expert" for the same tax question. Persona prompting does not prevent the model from using its knowledge (C) — it shapes HOW that knowledge is expressed.

---

**Q8. Answer: B**
*Explanation:* A Persona Stack combines multiple complementary attributes into a single, nuanced persona. Example: "You are a former management consultant with 10 years of experience, now a startup CEO who writes for a non-technical LinkedIn audience and values direct, jargon-free communication." Each attribute adds a different layer of calibration that a single-attribute persona cannot achieve.

---

**Q9. Answer: B**
*Explanation:* The Prompt Optimization Cycle is: **Design** (write the initial prompt) → **Test** (run on representative inputs) → **Evaluate** (score outputs against quality criteria) → **Diagnose** (identify the root cause of failures — not just symptoms) → **Refine** (make one targeted change). This is a systematic discipline, not random iteration.

---

**Q10. Answer: B**
*Explanation:* Output Anchoring provides the beginning of the expected output structure within the prompt itself — for example: "Begin your response with: | Feature | Benefit | Evidence |" or "Start your answer with: 'The three key risks are:'". This anchors the model's generation to your desired format from the first token, preventing it from defaulting to a different structure.

---

**Q11. Answer: C**
*Explanation:* CoT is most valuable when the task has a multi-step reasoning structure — where getting step 2 wrong because step 1 was skipped is the primary failure mode. For simple tasks (A), CoT adds overhead with no benefit. For pure factual recall (B), the answer either exists in training data or doesn't — reasoning steps don't help. For formatting tasks (D), a Format specification is more effective than a reasoning chain.

---

**Q12. Answer: B**
*Explanation:* In classification tasks, few-shot examples must cover all classes the model will encounter — otherwise the model has only seen one class in context and will over-predict it. Balanced representation (at least one example per class, ideally proportional to class frequency) ensures the model understands the full classification space. Imbalanced examples (A) introduce systematic bias.

---

**Q13. Answer: B**
*Explanation:* Prompt Decomposition (as an optimization technique) means breaking a complex, multi-dimensional task into a sequence of simpler, focused sub-prompts. Instead of one prompt that asks for research, analysis, recommendation, and formatting simultaneously, you create four prompts — each doing one thing well — and chain the outputs. Option A describes a different process (failure diagnosis).

---

**Q14. Answer: B**
*Explanation:* An adversarial persona is a legitimate, powerful technique for stress-testing ideas, plans, or arguments. By asking the AI to adopt the role of a "skeptical investor," a "rival company," or a "devil's advocate," you get rigorous pushback that reveals weaknesses before they matter. It is not about bypassing safety guidelines (C) or making the AI aggressive (D).

---

**Q15. Answer: B**
*Explanation:* "Do not begin your response with 'Certainly!' or 'Of course!'" is a precision negative instruction targeting a specific, common AI output behavior. Negative instructions are most effective when: the AI has a strong default you want to override, AND you can specifically name what to avoid. Generic negatives ("don't be bad") are ineffective; specific negatives ("don't use the words X, Y, Z") work precisely.

---

**Q16. Answer: A**
*Explanation:* In-context learning is what makes few-shot prompting possible: by providing examples within the prompt, the model adjusts its behavior for the current task without any weight updates (no retraining). This is entirely different from fine-tuning (D), which does update model weights. Each new conversation starts fresh — no learning persists across conversations (C).

---

**Q17. Answer: B**
*Explanation:* A self-critique prompt asks the AI to evaluate its own output — "Rate the above response on accuracy, clarity, and completeness (1–5 each). Then rewrite it addressing any score below 4." This recursive quality check often catches issues the first pass missed. It's one of the most effective single-step quality improvements available to a prompt engineer.

---

**Q18. Answer: B**
*Explanation:* For performance review writing, "experienced HR business partner with 12 years of writing performance feedback" provides three critical calibrations: domain (HR), role (business partner — not just admin), and experience level (12 years — calibrates sophistication). The other personas (A, C, D) provide no relevant domain calibration for this task.

---

**Q19. Answer: B**
*Explanation:* The Scoring Rubric technique embeds explicit evaluation criteria directly in the prompt: "Before presenting your final output, evaluate it against these criteria: [accuracy: 1–5, clarity: 1–5, completeness: 1–5]. If any score is below 4, revise and re-score before presenting." This transforms the AI from a passive generator to an active quality controller of its own output.

---

**Q20. Answer: B**
*Explanation:* Few-shot is most valuable when the desired output format or style is unusual, highly specific, or difficult to describe purely in words — showing is more efficient than describing. If you want output in a very particular JSON structure, a specific prose style, or domain-specific language that the AI doesn't naturally default to, one or two examples communicate the pattern instantly.

---

**Q21. Answer: B**
*Explanation:* Chain Prompting (as an optimization technique, distinct from the Session 21 pipeline concept) is the practice of passing output from one prompt as structured input to the next. Each prompt in the chain has a focused, single responsibility. The output of "Extract all action items" becomes the input to "Prioritize these action items by urgency" — each step is clean and verifiable.

---

**Q22. Answer: A**
*Explanation:* Few-Shot CoT provides examples where each example shows not just the final answer but the complete reasoning chain that leads to it. This teaches the model both the answer pattern AND the reasoning pattern simultaneously. Contrast with zero-shot CoT ("Let's think step by step") which triggers reasoning without showing examples of how to reason.

---

**Q23. Answer: B**
*Explanation:* Context window is a finite resource shared between prompt and response. Each few-shot example consumes tokens — 3–5 high-quality examples is typically optimal for most tasks. Adding 15–20 examples may push useful context (the actual input) out of the window, or leave insufficient space for a thorough response. Quality over quantity always applies to few-shot selection.

---

**Q24. Answer: B**
*Explanation:* "Expert" without domain specification is a near-empty instruction. Expert in what? At what level? For what audience? The model has no calibration to apply. A specific persona ("senior tax attorney specializing in corporate restructuring") carries domain vocabulary, assumed expertise level, communication register, and perspective — none of which "expert" alone provides. This is one of the most common, easily-fixed persona errors.

---

**Q25. Answer: C**
*Explanation:* Prompt optimization is a disciplined, systematic process — not luck (B) or a one-time event (A). The key word is "diagnosed": every refinement should target a specific identified failure mode (wrong tone → add tone specification; too generic → add context). Random changes hoping for improvement are not optimization — they are iteration without learning.

---

---

# PART B — SHORT ANSWER ASSIGNMENTS (20 Marks)

---

**B1.** Explain the difference between zero-shot and few-shot prompting. When would you choose each? *(2 marks)*

**Answer:**
Zero-shot prompting provides no examples — the AI performs the task relying entirely on its training knowledge. Few-shot prompting provides 1–5 input/output examples that demonstrate the desired pattern before the actual input. Choose zero-shot when: the task is well-understood (summarization, translation, standard formatting) and the model's default behavior matches your need. Choose few-shot when: the output format is unusual or highly specific, you need consistent style or terminology not easily described in words, or the task involves a domain-specific pattern the model hasn't seen frequently. The core trade-off is token efficiency (zero-shot) vs. pattern precision (few-shot).

*Marking: 1 mark for accurate definitions of both. 1 mark for practical selection criteria.*

---

**B2.** Write a zero-shot CoT prompt for this problem: "A company has 120 employees. 30% work remotely. Of the remote workers, 40% are in the engineering department. How many remote engineers are there?" *(2 marks)*

**Answer:**
```
A company has 120 employees. 30% work remotely. Of the remote workers, 40% are
in the engineering department. How many remote engineers are there?

Let's think through this step by step before giving the final answer.
```

*Expected reasoning chain the AI should produce:*
- Step 1: Remote workers = 30% of 120 = 0.30 × 120 = 36 remote workers
- Step 2: Remote engineers = 40% of 36 = 0.40 × 36 = 14.4 ≈ 14 remote engineers (rounding to whole people)
- Answer: 14 remote engineers

The trigger phrase "Let's think through this step by step" activates zero-shot CoT reasoning, making the model show its work rather than attempting to compute the answer in a single jump (which introduces arithmetic errors for multi-step problems).

*Marking: 1 mark for the correctly structured CoT prompt. 1 mark for brief explanation of why CoT helps here.*

---

**B3.** Design two few-shot examples for a prompt that classifies customer support tickets into: Technical / Billing / Feature Request / General. *(2 marks)*

**Answer:**
```
Classify the following customer support ticket into one of:
Technical | Billing | Feature Request | General

Examples:
Input: "The app crashes every time I try to upload a file larger than 10MB."
Output: Technical

Input: "I was charged twice for my subscription this month. Please refund the duplicate."
Output: Billing

Input: "It would be really useful if I could export my data to CSV format."
Output: Feature Request

Now classify this ticket:
Input: "{new_ticket_text}"
Output:
```

The examples cover 3 of 4 classes. A fourth example covering "General" (e.g., "How do I find my account number?") should also be added for complete class coverage. Each example is minimal, unambiguous, and follows the exact Input/Output format the model should reproduce.

*Marking: 1 mark for correctly formatted examples with Input/Output structure. 1 mark for demonstrating class variety and noting the completeness principle.*

---

**B4.** Your colleague says Chain-of-Thought prompting always makes outputs better. Describe TWO situations where CoT would NOT improve output. *(2 marks)*

**Answer:**
(1) **Simple factual recall:** "What is the capital of France?" — Adding "Let's think step by step" adds tokens and delay without improving the answer. The model either knows it's Paris or doesn't; a reasoning chain doesn't help. (2) **Creative writing:** "Write a poem about the ocean." Forcing step-by-step reasoning on a creative task introduces analytical rigidity that actually constrains the quality and spontaneity of creative output — the opposite of what's needed. CoT is specifically a tool for multi-step reasoning tasks where intermediate steps affect the correctness of the final answer. Applying it universally wastes tokens and can degrade quality for tasks that don't need it.

*Marking: 1 mark per valid scenario with explanation.*

---

**B5.** What is the risk of using only one few-shot example in a sentiment classification prompt? How would you address it? *(2 marks)*

**Answer:**
A single example teaches the model only one class — it cannot learn the full classification space from one data point. If the only example is "Positive," the model may over-predict Positive for ambiguous inputs because it has no context for what Negative or Neutral looks like in this domain. Additionally, one example may introduce pattern bias: if the example uses formal language, the model may associate the classification with formality rather than content. Fix: include at least one high-quality example per class (minimum 3 for 3-class problems), ensuring examples vary in length, style, and phrasing to prevent pattern memorization on surface features rather than the underlying classification logic.

*Marking: 1 mark for identifying the class imbalance/single class risk. 1 mark for the fix with rationale.*

---

**B6.** Write a Persona Prompt for an AI that will help a finance team write executive-level variance commentary for monthly financial reports. *(2 marks)*

**Answer:**
```
You are a senior FP&A (Financial Planning & Analysis) Manager with 15 years of
experience in management reporting for publicly traded companies. You specialize
in translating financial variance data into clear, concise executive commentary
that connects numbers to business drivers and strategic implications.

Your communication style:
- Lead with the "so what" before explaining the numbers
- Use business language, not accounting jargon ("revenue grew" not "top-line increased")
- Every variance has a driver — name it specifically, not generically
- Keep commentary under 60 words per variance unless complexity demands more
- Never say "favorable" or "unfavorable" — say what actually happened and why it matters

You are writing for a CFO and board of directors who read hundreds of these per quarter
and want insight, not a recitation of the numbers they already have in the table above.
```

*Marking: 1 mark for specific role with domain and experience. 1 mark for detailed communication style guidance that shapes output quality.*

---

**B7.** Describe the "One Change at a Time" rule for prompt optimization. Why is it critical? Give an example of what goes wrong when you violate it. *(2 marks)*

**Answer:**
The "One Change at a Time" rule states that when iterating on a prompt, you should change exactly ONE element per iteration — then test to see if quality improved, declined, or stayed the same. This is critical because it establishes causality: if you change three elements simultaneously and quality improves, you cannot know which change caused the improvement. If quality drops, you cannot identify the cause. You lose the ability to learn from your own iterations. Example violation: A prompt produces outputs that are too generic and too long. A prompt engineer simultaneously adds more context, shortens the task description, and adds a word count constraint. Quality improves — but they don't know if it was the context, the shorter task, or the word limit. The next time they face a similar problem, they must guess again. With one change at a time, each iteration is an experiment that teaches a reusable lesson.

*Marking: 1 mark for clear rule definition and why it matters. 1 mark for a concrete violation example.*

---

**B8.** What is the difference between a "Prompt Library" and a folder of saved prompts? What makes a prompt library professional-grade? *(2 marks)*

**Answer:**
A folder of saved prompts is an unorganized collection of text files — no metadata, no categorization, no version history, no documented performance. A professional-grade prompt library is a governed, documented asset with: (1) unique IDs and consistent naming, (2) full metadata (technique, version, success rate, last reviewed, author), (3) tested examples with quality scores, (4) iteration history showing what changed and why, (5) a navigable index so any team member can find the right prompt in under 30 seconds, and (6) governance rules for adding, modifying, and retiring entries. The difference is between "a collection of things that worked once" and "institutional knowledge that compounds in value over time."

*Marking: 1 mark for clear distinction. 1 mark for listing key professional-grade characteristics.*

---

**B9.** Explain "Self-Consistency" in Chain-of-Thought prompting. Why does it work? *(2 marks)*

**Answer:**
Self-Consistency generates multiple independent reasoning paths for the same problem (typically at temperature 0.5–0.8 to introduce variation) and then takes a majority vote across the final answers from each path. It works because: different reasoning chains make different errors, but correct reasoning chains tend to converge on the same answer. If 7 of 10 reasoning chains reach answer "₹42,000" through different routes, that answer has much stronger reliability than a single chain reaching the same conclusion. It's mathematically similar to ensemble methods in machine learning — diversity of approach reduces systematic error. Self-Consistency is particularly effective for math, logic, and constrained reasoning where there is one objectively correct answer.

*Marking: 1 mark for accurate definition of the mechanism. 1 mark for why it works (diversity → error reduction).*

---

**B10.** Write a Self-Critique prompt for the following task: evaluating AI-generated marketing copy. *(2 marks)*

**Answer:**
```
You have just generated the following marketing copy:
[AI OUTPUT TO EVALUATE]

Before presenting this as your final output, evaluate it against these criteria:

SELF-CRITIQUE:
1. CLARITY (1–5): Is the core message clear in the first sentence?
2. AUDIENCE FIT (1–5): Does the language match a [TARGET AUDIENCE] reader?
3. SPECIFICITY (1–5): Are claims specific (numbers, features) or generic ("best-in-class")?
4. CALL TO ACTION (1–5): Is the CTA specific and compelling?
5. BRAND VOICE (1–5): Does this match [BRAND VOICE DESCRIPTION]?

For any criterion scored below 4:
- State the specific problem
- Rewrite that element to address it
- Re-score

Present your FINAL REVISED VERSION only (not the drafts).
```

*Marking: 1 mark for a correctly structured self-critique prompt with rubric criteria. 1 mark for the revision instruction closing the loop.*

---

---

# PART C — LONG ANSWER / PRACTICAL ASSIGNMENTS (30 Marks)

---

**C1.** *(6 marks)* Design a complete few-shot prompt for classifying business emails into five categories: Action Required / FYI Only / Meeting Request / Approval Needed / Spam. Include one example per category. Explain your example selection choices.

**Answer:**

```
You are an executive assistant AI trained to classify incoming business emails
accurately so that the recipient can triage their inbox by priority.

Classify each email into exactly one of these categories:
Action Required | FYI Only | Meeting Request | Approval Needed | Spam

Rules:
- Choose the MOST specific category that applies
- If an email could be Action Required OR Approval Needed, choose Approval Needed
- Base classification on the email content, not the sender

EXAMPLES:

Input: "Hi Sarah, Please review the attached vendor contract and send me
your redlines by Friday. Legal needs it finalized before the board meeting."
Output: Action Required

Input: "Team, Just a heads-up that the office will be closed on October 2nd
for the national holiday. No action needed."
Output: FYI Only

Input: "Could we find 30 minutes this week to discuss the Q4 planning timeline?
I'm free Tuesday afternoon or Thursday morning."
Output: Meeting Request

Input: "Attached is the revised marketing budget for Q4. Please approve so we
can proceed with vendor bookings. Deadline: end of week."
Output: Approval Needed

Input: "Congratulations! You've been selected for our exclusive offer. Click here
to claim your prize."
Output: Spam

Now classify this email:
Input: "{email_text}"
Output:
```

**Explanation of Example Selection:**

- **Action Required:** Selected an email with a clear deliverable (redlines), a responsible party (Sarah), and a deadline (Friday) — all the markers that distinguish action from FYI.
- **FYI Only:** Explicitly includes "No action needed" to teach the model the key distinguishing phrase. The example reflects a realistic office communication pattern.
- **Meeting Request:** Deliberately made it informal ("could we find") rather than formal calendar language, to show the model this category includes informal meeting asks — not just calendar invites.
- **Approval Needed:** Distinguished from Action Required by including explicit approval language ("Please approve") and a business consequence (vendor bookings) — teaching the boundary between the two most easily confused categories.
- **Spam:** Uses clear spam markers (unsolicited prize, click-here CTA) without being too extreme — teaching the model the pattern without using an example so obvious it doesn't generalize.

*Marking: 3 marks for complete, well-structured prompt with all 5 examples. 3 marks for thoughtful explanation of selection choices — specifically addressing boundary cases between similar categories.*

---

**C2.** *(6 marks)* A product manager needs to evaluate 3 proposed feature names for a new mobile app. Design a complete Chain-of-Thought prompt that evaluates each name against 4 criteria: memorability, brand fit, clarity, and competitive differentiation. Show the expected reasoning structure.

**Answer:**

**Prompt:**
```
You are a brand strategist with 12 years of experience naming consumer mobile apps.

Evaluate the following three proposed names for a new personal finance app
that helps young professionals (24–35) track spending and build savings habits.
The brand values are: simple, trustworthy, modern, and empowering (not scary).

PROPOSED NAMES: "Vault", "Candor", "Leafy"

Evaluate each name step by step against these four criteria:
1. MEMORABILITY: Is it easy to remember, pronounce, and spell after one hearing?
2. BRAND FIT: Does it align with the brand values (simple, trustworthy, modern, empowering)?
3. CLARITY: Does it clearly communicate the app's purpose (personal finance, saving)?
4. COMPETITIVE DIFFERENTIATION: Does it stand out from common finance app names?
   (Reference names to differentiate from: Mint, Wallet, Monefy, Spendee, YNAB)

For EACH NAME:
Step 1 — Evaluate Memorability: [reasoning] → Score: /5
Step 2 — Evaluate Brand Fit: [reasoning] → Score: /5
Step 3 — Evaluate Clarity: [reasoning] → Score: /5
Step 4 — Evaluate Competitive Differentiation: [reasoning] → Score: /5
Step 5 — Total Score: /20
Step 6 — Key Strength: [the one strongest attribute of this name]
Step 7 — Key Risk: [the one biggest weakness or concern]

After evaluating all three names:
FINAL RECOMMENDATION: Which name to proceed with and why (2–3 sentences).
RUNNER-UP: Second choice with brief rationale.
REJECT: Which name to eliminate first and the primary reason.
```

**Expected Reasoning Structure (for "Vault"):**

- Step 1 (Memorability): "Vault" is a single syllable, easy to spell, no ambiguous pronunciation. High recall probability. → Score: 5/5
- Step 2 (Brand Fit): "Vault" evokes security and protection (trustworthy ✓), but also heaviness and restriction — potentially at odds with "empowering" and "modern." May skew toward fear-based rather than growth-based associations. → Score: 3/5
- Step 3 (Clarity): Strong association with money storage, but less with spending tracking or habit-building — the key use cases. → Score: 3/5
- Step 4 (Differentiation): No major competitor uses "Vault" as primary name. Strong differentiation from the "green" and "wallet" metaphor names. → Score: 4/5
- Total: 15/20 | Key Strength: Maximum memorability | Key Risk: Brand tone skews conservative/restrictive

*Marking: 3 marks for a complete, correctly structured CoT prompt with all required elements. 3 marks for showing what the expected reasoning chain would look like — demonstrating understanding of how CoT structures multi-criteria evaluation.*

---

**C3.** *(6 marks)* You are a prompt engineer building a support ticket auto-response system. Design the complete persona (system prompt) for the AI, including: role, capabilities, limitations, escalation triggers, and tone guidelines. Then explain why each element of the persona is necessary.

**Answer:**

**System Prompt:**
```
You are Aria, the AI-powered customer support assistant for FinTrack, a personal
finance app for young professionals.

YOUR ROLE:
You are the first-line support responder. You handle routine inquiries, guide users
through common issues, and ensure every customer feels heard and helped — quickly.

YOUR CAPABILITIES (handle independently):
- Explain all app features and how to use them
- Walk users through account setup, linking bank accounts, and troubleshooting
  common sync errors
- Explain subscription plans, billing cycles, and how to update payment methods
- Guide users through password reset and account recovery standard process
- Answer questions about data privacy using the provided privacy policy

YOUR LIMITATIONS (be honest — do not attempt to resolve these):
- You cannot access live account data, balances, or transaction history
- You cannot process refunds — escalate all refund requests to the billing team
- You cannot verify identity for account security issues — escalate to security team
- You do not know about app updates released after [KNOWLEDGE CUTOFF DATE]

ESCALATION TRIGGERS (transfer to human agent immediately):
- Customer explicitly requests to speak with a human
- Customer mentions legal action, regulatory complaint, or media coverage
- Customer reports fraudulent transactions or unauthorized account access
- Customer expresses serious personal distress unrelated to the app
- The same issue has been reported by the customer more than twice

ESCALATION RESPONSE TEMPLATE:
"I completely understand, and I want to make sure this gets the attention it
deserves. I'm connecting you right now with a specialist from our [TEAM] team.
They'll be with you within [TIMEFRAME]. Your reference number is [REF]. Is there
anything else I can help with while you wait?"

TONE GUIDELINES:
- Warm, helpful, and patient — like a knowledgeable friend
- First-name basis once the customer's name is known
- Short responses (under 80 words for chat, under 150 for email)
- Acknowledge the customer's feeling before solving the problem
- Never say "I understand your frustration" — it sounds scripted; show understanding specifically
- Never start with "Certainly!" or "Of course!" — go directly to helping
```

**Explanation of Each Element:**

- **Role clarity:** Establishes what the AI is and what its purpose is — preventing it from trying to be a financial advisor or general assistant.
- **Capabilities list:** Explicitly defines what the AI CAN handle autonomously — limits hallucinated improvisation on unknown topics.
- **Limitations list:** This is the most critical element. Without explicit limitations, the AI will attempt to help with everything (including things it cannot actually do), creating false promises and legal risk.
- **Escalation triggers:** Defines exactly WHEN the AI must stop trying to solve the problem — protects the company from AI handling situations that require human judgment, legal awareness, or emotional intelligence.
- **Escalation template:** Gives the AI exact language for the handoff — ensuring the escalation itself doesn't create a negative experience.
- **Tone guidelines:** Specific enough to shape actual output behavior ("under 80 words" is measurable; "never say 'Certainly'" targets a specific undesired behavior).

*Marking: 3 marks for complete, professional system prompt covering all 5 required elements. 3 marks for insightful explanation of each element's necessity.*

---

**C4.** *(6 marks)* Build a complete Prompt Optimization Case Study. Start with a weak prompt, show 3 iterations with a specific diagnosis and change at each step, and produce a final optimized version. Include quality scores at each stage.

**Answer:**

**Task:** Generate a LinkedIn post announcing a company's new office opening in Bangalore.

---

**ITERATION 1 — v1.0 (Starting Prompt):**
```
Write a LinkedIn post about our new office in Bangalore.
```

**Output:** "We are excited to announce the opening of our new office in Bangalore! This is a significant milestone for our company as we continue to grow and expand our presence in India. We look forward to serving our customers better and creating new opportunities for our team. Stay tuned for more updates! #Bangalore #Growth #NewOffice"

**Quality Score:** 2/5
**Diagnosis:** Generic to the point of being meaningless. Could be any company. No specific details, no human interest, no call to action. The output mirrors the vagueness of the prompt.

---

**ITERATION 2 — v1.1 (Added Context):**
```
Write a LinkedIn post about our new office in Bangalore.

Context: Our company is Finaxis, a 6-year-old B2B fintech company based in Mumbai.
The Bangalore office is our first expansion outside Mumbai. It will house 45
employees — primarily engineering and product teams. Opening date: November 15, 2024.
CEO is Priya Mehta.
```

**Output:** "We're thrilled to announce that Finaxis is expanding! On November 15th, we open our Bangalore office — our first step beyond Mumbai in 6 years of building fintech solutions. The new space will be home to 45 engineers and product thinkers driving our next chapter. This is more than an office opening — it's a statement about where we're headed. Welcome to the team, Bangalore! #Finaxis #Bangalore #Fintech #Growth"

**Quality Score:** 3.5/5
**Improvement:** Specific details make this recognizably Finaxis. The emotional note ("6 years of building") adds human interest.
**Remaining diagnosis:** Still lacks a call to action and doesn't leverage the CEO's voice, which would increase engagement on LinkedIn. Tone is still corporate rather than authentic.

---

**ITERATION 3 — v1.2 (Added Persona + Tone):**
```
Write a LinkedIn post about our new office in Bangalore.

Context: [same as v1.1]
Persona: Written in the voice of CEO Priya Mehta — direct, warm, and unscripted.
She is proud of this milestone but doesn't use corporate language.

Tone: Conversational, first person ("I"), genuine. Not a press release. Not "thrilled."
Max 200 words. End with a question that invites comments.
Do not use: "thrilled," "excited," "milestone," "solutions," or passive voice.
```

**Output:** "Six years ago, Finaxis was four people in a Mumbai co-working space arguing about the best way to fix small business lending in India.

Today, we're opening our Bangalore office — 45 people, our first engineering hub outside Mumbai, and the team that will build what comes next for us.

I won't pretend this was the plan from day one. It happened because the right people showed up, believed in what we were doing, and pushed us further than we thought we'd go.

To our Bangalore team: you picked this company at an interesting time. I think you'll look back and say it was the right call.

If you're in Bangalore and want to see what we're building — or you know someone who should be part of this team — drop a comment or a DM.

#Finaxis #Bangalore #Fintech #IndiaBuilds"

**Quality Score:** 4.8/5
**What changed:** Persona created authentic voice. Negative instructions eliminated corporate defaults. The question ending drives engagement.

---

**Optimization Summary:**

| Version | Change Made | Quality |
|---------|------------|---------|
| v1.0 | No elements — raw topic only | 2/5 |
| v1.1 | Added specific Context | 3.5/5 |
| v1.2 | Added Persona + Tone + Negative Instructions | 4.8/5 |

**Key Learning:** The most impactful single change was the persona (CEO voice) combined with negative instructions ("not 'thrilled'") — because the AI's defaults for corporate announcements are heavily trained on generic PR language. Overriding those defaults requires explicit persona + explicit prohibition.

*Marking: 2 marks for showing 3 distinct, correctly diagnosed iterations. 2 marks for quality scores that track real improvement. 2 marks for the summary learning — identifying which change had the most impact and why.*

---

**C5.** *(6 marks)* Explain the concept of "Prompt Decomposition" with a detailed example. Take a complex task, show the single-prompt version (and why it fails), then show the decomposed version with 4 steps. Explain what each step achieves that the single prompt cannot.

**Answer:**

**Complex Task:** "Analyze our Q3 customer churn data and write a board-ready presentation on what's causing churn, what we should do about it, and what metrics to track going forward."

---

**Single Prompt Attempt:**
```
You are a business analyst. Analyze our Q3 customer churn data, identify root
causes, recommend 3 strategic actions, and write board-ready slides for the
full presentation.

[Data: 500 rows of customer data pasted here]
```

**Why it fails:**
- The prompt asks for 4 different cognitive tasks simultaneously: data analysis, root cause identification, strategy development, AND presentation writing
- Each task requires different depth, structure, and quality gate — merging them means each gets ~25% of the model's attention
- The data context competes with the output context for the same context window
- There is no point to verify intermediate analysis before it drives the strategy
- Errors in data interpretation (step 1) silently propagate into strategy (step 3) and presentation (step 4) — by the time you see the problem, it's embedded in the final output

---

**Decomposed Version — 4 Steps:**

**Step 1 — Data Interpretation:**
```
You are a data analyst. Here is Q3 churn data: [DATA]
Task: Identify the top 5 patterns in this churn data. For each pattern:
- What segment churns most?
- What time pattern (when in the customer lifecycle)?
- What product/feature usage is correlated with churn?
Output: Numbered list. No recommendations yet — only what the data shows.
```
*Achieves:* Pure data-driven pattern extraction without contamination from strategic assumptions. Human can verify these patterns before they drive any recommendations.

**Step 2 — Root Cause Hypothesis:**
```
Based on these churn patterns: [Step 1 output]
And this additional context: [business context — recent product changes, pricing
changes, competitive events]
Task: For each pattern, generate the 2 most plausible root cause hypotheses.
Distinguish between: [Hypothesis] and [Evidence strength: Strong/Moderate/Weak]
Output: Table — Pattern | Hypothesis | Evidence Strength
```
*Achieves:* Separates pattern observation (what) from causal reasoning (why) — these are different cognitive tasks. Labeling evidence strength enables human judgment about which causes are confirmed vs. assumed.

**Step 3 — Strategic Recommendations:**
```
Given these validated root causes: [Step 2 output — human curated]
Task: Recommend 3 specific, implementable actions to reduce churn.
For each action: What to do | Owner function | Expected impact | Timeline | Cost level
Prioritize by: highest impact relative to implementation effort.
Format: Decision-ready table.
```
*Achieves:* Recommendations are grounded in the validated root causes, not invented from generic best practices. The human-curated Step 2 output means bad hypotheses don't drive bad strategy.

**Step 4 — Board Slide Content:**
```
Based on this analysis: [Steps 1–3 summaries]
Task: Write 4 board slides on our Q3 churn situation.
Slide 1: The headline — what the board needs to know in 1 sentence
Slide 2: Root causes — 3 bullets, each a complete finding with evidence
Slide 3: Our response — 3 recommended actions with owner and timeline
Slide 4: Going forward — 3 metrics the board should track quarterly
Format: Message headlines (complete sentences). Max 3 bullets per slide.
```
*Achieves:* Presentation writing happens AFTER analysis is validated — not simultaneously. The input to this step is already curated, validated intelligence, not raw data.

**What Decomposition Achieves That Single Prompts Cannot:**
- Verification at each step before errors propagate
- Each step gets full attention (not 25% of a multi-task prompt)
- Human judgment inserted at the critical transitions (data → hypothesis, hypothesis → strategy)
- Easier to identify which step fails if output quality is poor
- Each step's output is a standalone deliverable that has independent value

*Marking: 2 marks for clearly explaining why the single prompt fails. 2 marks for 4 well-structured, distinct decomposed steps. 2 marks for articulating what each step achieves that the single prompt cannot.*

---

---

# MODULE 2 ASSESSMENT SUMMARY

| Part | Questions | Marks | Pass Mark |
|------|-----------|-------|-----------|
| A — MCQ | 25 | 25 | 18/25 |
| B — Short Answer | 10 | 20 | 14/20 |
| C — Long Answer | 5 | 30 | 21/30 |
| **Total** | **40** | **75** | **53/75** |

**Sessions Covered:**
- Session 6: Zero-Shot Prompting
- Session 7: Few-Shot Prompting
- Session 8: Chain-of-Thought Prompting
- Session 9: Persona Prompting & Role Engineering
- Session 10: Prompt Optimization

---

*Prompt Engineering Certification Program | Assessment Bank | Module 2*
*UpSkill Global Education Technologies Inc., Canada*
