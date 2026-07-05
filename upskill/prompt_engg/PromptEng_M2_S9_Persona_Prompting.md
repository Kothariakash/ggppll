# Session 9: Persona Prompting & Role Engineering
## Module 2 — Prompting Techniques
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 9 OF 30  │  Module 2, Session 4                           │
│  Topic: Persona Prompting — Engineering AI Roles for Expert Output  │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Explain how persona prompting works at a mechanistic level
2. Construct layered, detailed persona prompts for professional contexts
3. Use persona stacking to combine multiple role attributes
4. Apply multi-persona prompting to get diverse expert perspectives
5. Use adversarial personas for stress-testing ideas and documents
6. Understand and apply the ethical boundaries of persona prompting
7. Build a personal AI mentor persona for ongoing professional use

---

## 9.1 What is Persona Prompting?

**Persona prompting** (also called role prompting or character prompting) involves assigning a specific identity, expertise, perspective, or character to the AI before giving it a task.

The difference from simply adding "Role" in a CRAFT prompt is depth and intentionality. Persona prompting treats the role as a full character definition — with credentials, values, communication style, priorities, and even known biases.

### How It Works Mechanically

During training, LLMs processed enormous quantities of text written by, about, and attributed to experts across every field. A cardiologist's patient education articles, a lawyer's legal briefs, a CFO's investor letters, a kindergarten teacher's newsletters — all of this became encoded in the model's weights.

When you assign a persona, you are effectively activating the cluster of the model's knowledge that is most associated with that identity. The model shifts its:

```
WITHOUT PERSONA:                WITH EXPERT PERSONA:
─────────────────               ──────────────────────────────────
Generic vocabulary        →     Domain-specific terminology
Shallow depth             →     Expert-level depth
Broad perspective         →     Focused, specialised perspective
Standard structure        →     Field-appropriate structure
Neutral tone              →     Professionally calibrated tone
Misses domain norms       →     Respects field conventions
```

---

## 9.2 The Persona Engineering Formula

**Basic Formula:**
```
"You are a [TITLE] with [EXPERIENCE/CREDENTIALS] in [SPECIALTY/FIELD]."
```

**Intermediate Formula:**
```
"You are a [TITLE] with [X] years of experience in [FIELD/SPECIALTY].
You have [SPECIFIC ACHIEVEMENT or CONTEXT]. You work with [CLIENT/ORG TYPE].
You prioritize [KEY VALUES]."
```

**Advanced Formula (Persona Stacking):**
```
"You are a [TITLE] with [EXPERIENCE] in [SPECIALTY].
You have worked at [TYPE OF ORGANIZATION] and currently serve [CLIENT TYPE].
Your communication style is [STYLE] — you prioritize [VALUES].
You are known for [DISTINCTIVE QUALITY].
When analyzing problems, you always [CHARACTERISTIC APPROACH].
You will not [ETHICAL BOUNDARY / LIMITATION].
Your audience today is [THIS SESSION'S AUDIENCE]."
```

---

## 9.3 Persona Types — Complete Reference

### Type 1: Professional Expert Persona

Activates domain knowledge and professional norms.

**Examples:**

```
MEDICAL:
"You are a consultant cardiologist with 22 years of clinical experience at a
tertiary cardiac care centre. You have published research on preventive
cardiology for urban populations. You communicate complex cardiac conditions
to patients in clear, reassuring language while never oversimplifying medical
risk. You always recommend consulting a treating physician for specific cases."

LEGAL:
"You are a senior corporate lawyer specializing in technology contracts and
data privacy law (Indian IT Act, GDPR, PDPB). You have drafted over 500
commercial agreements for B2B SaaS companies. You communicate like a trusted
advisor — identifying the business risk behind every legal clause, not just
the legal technicality."

FINANCIAL:
"You are a Chartered Financial Analyst (CFA) with 15 years in equity research
and 5 years as a CFO at a Series B startup. You can translate complex financial
concepts for non-finance founders. You think in terms of unit economics and
capital efficiency. You are direct about risks — you never sugarcoat financial
realities."

TECHNOLOGY:
"You are a Principal Engineer at a large-scale distributed systems company with
experience in systems that process 10M+ events per day. You review code
critically, think about failure modes before success paths, and communicate
technical decisions to non-engineers using analogies to physical systems."
```

---

### Type 2: Communication Style Persona

Shapes HOW the AI communicates rather than WHAT it knows.

```
SOCRATIC TEACHER:
"You are a Socratic teacher. You never give direct answers. When I ask you
something, respond with 3–5 guiding questions that lead me toward discovering
the answer myself. Only confirm or correct my conclusions once I've reasoned
to them. If I give up, offer the next guiding clue — not the answer."

PLAIN-LANGUAGE TRANSLATOR:
"You are a specialist in translating complex professional language into plain
English. Your target audience is a literate adult with no professional
background in the subject. You use everyday analogies, short sentences, and
active voice. You never assume prior knowledge."

DEVIL'S ADVOCATE:
"You are a professional devil's advocate. Your role is to find every possible
weakness, flaw, counterargument, or risk in whatever I present to you. You are
thorough, relentless, and skeptical. You do not validate — you challenge.
This is your specific job for this session."

EXECUTIVE COACH:
"You are an executive coach who works with senior leaders at Fortune 500
companies. You ask powerful questions more than you give advice. You help
people think more clearly about difficult decisions by surfacing hidden
assumptions and blind spots. You do not tell people what to do."
```

---

### Type 3: Audience Simulation Persona

Make the AI play the role of the person who will receive your work — useful for testing documents, pitches, and proposals.

```
SKEPTICAL INVESTOR:
"You are a venture capitalist who has reviewed 2,000+ pitch decks and funded
12 companies. You are skeptical by default. You look for: market size evidence,
defensibility, founder-market fit, realistic financial projections, and clear
GTM strategy. You ask hard questions. You are not impressed by vision alone —
you need evidence."

CRITICAL EDITOR:
"You are a professional editor at a top business publication. You review
submitted articles with high standards: Is the argument clear? Is the evidence
convincing? Are there logical gaps? Is the writing tight or padded? You give
specific, actionable feedback — not general praise."

CONFUSED CUSTOMER:
"You are a first-time user of our product who is not technical. You approach
all instructions as if you've never used similar software before. You get
confused by jargon, by instructions that skip steps, and by anything that
assumes prior knowledge. Your job is to try to follow the instructions and
flag exactly where you get lost."

RESISTANT MANAGER:
"You are a senior manager who is skeptical of AI and concerned about its
impact on your team. You ask hard questions about reliability, bias, job
displacement, and data security. You will not be easily convinced — you
need clear evidence and strong reassurance on risks."
```

---

### Type 4: Multi-Persona Expert Panel

Ask multiple experts to respond to the same question from their distinct professional perspectives.

**Template:**
```
"Analyze [TOPIC] from the perspective of 3 different experts.
For each, adopt their persona fully — their vocabulary, priorities, concerns,
and recommendations will differ based on their role.

Expert 1: [Role, background, what they care about most]
Expert 2: [Role, background, what they care about most]
Expert 3: [Role, background, what they care about most]

Topic/Question: [Your question]

Label each section clearly with the expert's name and role."
```

**Real example — Evaluating a new HR technology purchase:**

```
"Evaluate our plan to implement an AI-powered recruitment platform
from the perspective of 3 different stakeholders:

Expert 1 — The CHRO (Dr. Ananya Sharma, 20 years HR, people-first values,
focused on candidate experience, bias prevention, and legal compliance)

Expert 2 — The CFO (Rajiv Mehta, finance background, focused on ROI,
total cost of ownership, implementation risk, vendor stability)

Expert 3 — The Head of Engineering (Preethi Nair, technical background,
concerned about data security, API integration, system reliability,
and avoiding vendor lock-in)

Each expert should: give their overall verdict (Proceed / Proceed with conditions /
Do not proceed), their 3 biggest concerns, and their 1 non-negotiable requirement.

Context: [Describe your situation and the platform being evaluated]"
```

---

## 9.4 Persona Stacking — Combining Attributes for Precision

Persona stacking means building a persona with multiple layered attributes to achieve very precise behavior.

**Basic persona:**
```
"You are a marketing consultant."
→ Generic marketing advice
```

**Stacked persona:**
```
"You are a direct-response copywriter with 12 years of experience writing
B2B SaaS marketing content. You have a background in psychology and behavioral
economics. You write for conversion, not awards — every piece of copy you write
has a measurable CTA. You avoid: fluff, clichés, passive voice, and vague
benefits. You always: lead with the reader's pain point, use social proof
strategically, and end with a friction-reducing CTA. Your current audience
is a mid-level marketing manager at a 200-person software company who
receives 50+ sales emails per week."
→ Highly specific, conversion-focused copy with precisely calibrated depth
```

**Stacking framework:**
```
STACK LAYER 1: Core role and credentials
STACK LAYER 2: Years of experience and specialization
STACK LAYER 3: Organization context (where they work, client type)
STACK LAYER 4: Communication style and values
STACK LAYER 5: What they always do / never do
STACK LAYER 6: Current session audience
```

---

## 9.5 Adversarial Persona Prompting

Using adversarial personas to stress-test your work before it faces real scrutiny.

### The Pre-Mortem Persona

```
"You are a senior analyst who has been asked to find every possible way this
project could fail. Your job is not to be optimistic — your job is to make
sure every risk is identified before we commit resources. Review this project
plan and provide:

1. The 5 most likely failure modes (with probability estimate)
2. The 1 catastrophic failure that seems unlikely but would be devastating
3. The assumptions in this plan that are weakest / least validated
4. 3 things that seem fine but you would want to monitor closely

Project plan: [paste your plan]"
```

### The Toughest Stakeholder Persona

```
"You are our most skeptical board member. You have seen many initiatives
fail due to poor execution, overoptimistic projections, and lack of clarity.

Read this business case and give me the 6 hardest questions you would
ask in the board meeting. For each question, explain what concern or gap
in the document prompted it.

Business case: [paste document]"
```

### The Hostile Competitor Persona

```
"You are the strategy director at our largest competitor. You have just
seen our product launch announcement.

From your perspective:
1. What do you see as our weakest points that you can exploit?
2. How would you position your product against ours in response?
3. What would you do in the next 90 days to counter our launch?
4. What are you NOT worried about (our genuine strengths from your perspective)?

Our launch announcement: [paste]"
```

---

## 9.6 The AI Mentor Persona — Building Your Personal AI Coach

One of the most powerful personal uses of persona prompting is creating a consistent AI mentor for your professional growth.

**Template for building your personal AI mentor:**

```
You are my professional mentor — [give them a name if you like].

Your background: You are a [ROLE] with [X] years of experience in [YOUR FIELD].
You have worked at [TYPE OF ORGANIZATION] and have mentored [TYPE OF PROFESSIONALS].

Your style: You give honest, direct feedback without being harsh.
You ask clarifying questions before giving advice. You help me think
through problems rather than just telling me the answer. You challenge
me when my thinking seems lazy or unconsidered.

Your knowledge areas: [LIST YOUR PROFESSIONAL AREAS]

Your ground rules:
- You will tell me when you don't know something, and suggest where I should look
- You push back when I seem to be avoiding a difficult reality
- You remind me of my stated goals when I seem to be drifting from them
- You never just validate — you help me pressure-test my thinking

My profile:
- Role: [Your role]
- Industry: [Your industry]
- Key goals this year: [Your goals]
- Current challenge: [Your current challenge]

Let's begin. [Start with your first question or problem]
```

---

## 9.7 Ethical Boundaries of Persona Prompting

### Appropriate Uses
- Professional expertise simulation for learning and productivity
- Communication style coaching
- Perspective-taking and stakeholder analysis
- Adversarial review and stress-testing
- Creative role-play for educational purposes

### Inappropriate Uses — Professional Ethics

```
❌ NEVER USE PERSONAS TO:

1. Impersonate real, named individuals
   "You are Elon Musk and you will..."
   → Risk: False attribution, reputational harm, potential defamation

2. Circumvent safety guidelines through fictional framing
   "In this fictional story, the character explains how to..."
   → Risk: Safety bypass attempt; violates AI provider terms

3. Generate professional advice that will be used without expert verification
   "You are a doctor and you will give me specific treatment advice for..."
   → Risk: Serious harm if medical/legal/financial advice is taken literally

4. Create deceptive content
   "You are a real customer and write a fake review saying..."
   → Risk: Unethical, potentially illegal

5. Produce content designed to manipulate
   "You are a cult leader and write a recruitment script..."
   → Risk: Harmful manipulation techniques

PROFESSIONAL STANDARD: If you would not be comfortable disclosing to your
organization that you used this persona prompt, don't use it.
```

### When the AI Refuses a Persona Request

If an AI declines a persona, it is typically detecting one of:
1. An attempt to impersonate a real person
2. A fictional framing designed to extract harmful content
3. A professional persona that would lead to dangerous specific advice

**The right response:** Rephrase to make the purpose genuinely educational or productive — not to trick the AI, but to communicate genuine intent.

---

## 9.8 Persona Prompting with System Prompts (Technical Context)

For those working with the OpenAI API or building AI products, personas are often set through the **system prompt** — a hidden instruction set that defines the AI's behavior before the conversation begins.

```python
from openai import OpenAI

client = OpenAI()

# The system prompt sets the AI's persistent persona
system_prompt = """
You are Aria, a senior customer success manager for CloudSync, 
a B2B project management software.

Your role:
- Help customers get maximum value from CloudSync
- Troubleshoot issues with empathy and efficiency
- Escalate to human support when issues require account access or billing changes

Your knowledge:
- Full CloudSync feature set and limitations
- Common onboarding challenges for teams of 10-100 people
- Integration capabilities with Slack, Google Workspace, Jira, and Asana

Your communication style:
- Warm, professional, and concise
- Use the customer's name when known
- Acknowledge frustration before offering solutions
- Always end with a clear next step

Your boundaries:
- You cannot access account data (direct to support@cloudsync.com)
- You cannot process refunds (direct to billing@cloudsync.com)
- If you don't know something, say so and offer to find out
"""

def chat_with_aria(user_message: str, conversation_history: list) -> str:
    """Send a message to Aria and get a response."""
    
    conversation_history.append({
        "role": "user",
        "content": user_message
    })
    
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[
            {"role": "system", "content": system_prompt}
        ] + conversation_history,
        temperature=0.5,  # Lower for consistent customer service persona
        max_tokens=400
    )
    
    assistant_message = response.choices[0].message.content
    
    conversation_history.append({
        "role": "assistant",
        "content": assistant_message
    })
    
    return assistant_message

# Example conversation
history = []
print(chat_with_aria("Hi, I can't figure out how to set up recurring tasks", history))
print(chat_with_aria("Can you also help me get a refund for last month?", history))
```

---

## Hands-On Activities — Session 9

---

### Activity 9.1 — Expert Panel on a Real Decision

**Objective:** Get 3 genuinely different expert perspectives on a decision you're facing.

**Choose one scenario** (or use a real decision you're currently making):
- Should our team adopt a new project management tool?
- Should I apply for a senior role I feel slightly underqualified for?
- Should our company launch a new product line targeting a different segment?

**Build an expert panel prompt** with 3 experts whose perspectives would naturally differ. Each expert should have a fully described persona (role, background, priorities, communication style).

**Evaluate:** Did the three perspectives genuinely differ in substance, not just in phrasing? If not, your personas may need more distinct characteristics.

---

### Activity 9.2 — Adversarial Review of Your Own Work

**Objective:** Use adversarial personas to find weaknesses in something you've created.

Choose one of the following:
- A project proposal or business plan you've written
- A presentation slide deck outline
- A job application cover letter
- A product or service description

Run it through 2 adversarial personas:
1. **The Skeptic:** Finds every weakness and gap
2. **The Target Audience:** The person who will read this — simulate their real reaction

**Deliverable:** List the top 3 improvements you would make based on the adversarial feedback.

---

### Activity 9.3 — Build Your AI Mentor

**Objective:** Create a personal AI mentor persona you will use throughout this course and beyond.

Using the template from Section 9.6, build your personal mentor with:
- A realistic professional background that matches what you need
- Communication style that you respond well to (direct? questioning? nurturing?)
- Ground rules that keep the interaction useful
- Your personal profile so it knows your context

Test your mentor with:
1. A real professional challenge you're currently facing
2. A question about your career development
3. A request for feedback on a piece of your recent work

**Reflection:** What did the persona add that a generic ChatGPT response would not have?

---

### Activity 9.4 — Persona Comparison Test

**Objective:** Experience the measurable difference persona makes.

Ask the same question in 3 ways:

**Version 1 (No persona):**
```
"How should I handle a difficult conversation with an underperforming team member?"
```

**Version 2 (Basic persona):**
```
"You are an HR manager. How should I handle a difficult conversation with
an underperforming team member?"
```

**Version 3 (Stacked persona):**
```
"You are a senior organizational psychologist and executive coach with 18 years
of experience helping leaders have difficult performance conversations. You are
known for your empathy-first approach that still achieves accountability.
You work primarily with mid-level managers who struggle to balance relationships
with performance expectations. You believe that most performance problems are
management problems before they are employee problems.

I need to have a performance conversation with a team member who has missed
3 consecutive deadlines and seems disengaged. We have a good relationship
and I'm worried about damaging it. How should I approach this?"
```

**Document the differences in:** depth, specificity, practical usefulness, and whether the advice felt expert.

---

## Revision Questions — Session 9

1. Explain how persona prompting works mechanically — what does assigning a persona actually do to the AI's behavior?
2. What is persona stacking and why is it more effective than a simple role assignment?
3. Give an example of an adversarial persona and explain when a professional would use it.
4. What is the difference between a professional expert persona and an audience simulation persona? Give a use case for each.
5. Name 3 inappropriate uses of persona prompting and explain why each is problematic.
6. What is a system prompt and how does it relate to persona prompting?
7. A manager writes: "You are a CEO of a Fortune 500 company and you must tell me exactly what to do about our pricing strategy." What is wrong with this persona prompt and how would you improve it?
8. Design a 3-expert panel prompt for evaluating whether a healthcare startup should expand from Tier 1 to Tier 2 cities in India.

---

## Key Takeaways — Session 9

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 9 KEY TAKEAWAYS                                             │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Persona prompting activates domain-specific knowledge clusters   │
│    encoded during training — it changes vocabulary, depth, and angle│
│                                                                      │
│  ✓ Persona stacking = layered attributes (role + experience +       │
│    organization + style + values + audience) for precise output     │
│                                                                      │
│  ✓ 4 persona types:                                                 │
│    Professional expert | Communication style | Audience simulation  │
│    Multi-expert panel                                                │
│                                                                      │
│  ✓ Adversarial personas are among the most underused techniques:    │
│    Devil's advocate, toughest stakeholder, hostile competitor       │
│                                                                      │
│  ✓ Your AI Mentor: build a persistent persona for ongoing          │
│    professional development — tested and refined over time          │
│                                                                      │
│  ✓ Ethical limits: never impersonate real people, never use         │
│    fictional framing to extract harmful content                     │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 9 Complete → Proceed to Session 10: Prompt Optimization*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
