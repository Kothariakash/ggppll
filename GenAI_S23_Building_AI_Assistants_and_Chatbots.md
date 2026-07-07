# Session 23: Building AI Assistants & Chatbots
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 5 — CREATIVE AI & AUTOMATION                                         │
│  SESSION 23 of 30  |  1 Hour  |  30% Theory + 70% Hands-On                 │
│                                                                              │
│  "An AI assistant you build yourself does exactly what you designed it      │
│   to do — no more, no less. The design is the work."                        │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 23, you will be able to:

- Design a custom AI assistant using a structured system prompt
- Build a Custom GPT in ChatGPT with instructions, knowledge, and capabilities
- Apply the ASSIST framework to design any AI assistant for a specific use case
- Define capability limits, guardrails, and escalation paths for AI assistants
- Use no-code platforms (Botpress, Tidio, Voiceflow) for chatbot deployment
- Evaluate AI assistant quality using the 5-dimension quality framework

---

## 1. What Is an AI Assistant?

### 1.1 The Spectrum of AI Assistants

```
BASIC CHAT (Session 1–10 level):
  You open ChatGPT and type a prompt.
  No memory, no persona, no custom knowledge.
  Generic AI → general answers.

PERSONA-INSTRUCTED ASSISTANT (Session 9 level):
  You start a session with a system prompt defining role and behavior.
  Works within that session only.
  Custom persona → focused answers.

CUSTOM GPT / CONFIGURED ASSISTANT (This Session):
  A persistent AI assistant with:
  ✓ A defined identity and persona
  ✓ Specific knowledge (uploaded documents)
  ✓ Specific capabilities (tools, browsing, code)
  ✓ Defined boundaries (what it will/won't do)
  ✓ Persistent configuration (works the same every session)
  Result: A reusable, deployable AI tool for a specific purpose.

DEPLOYED CHATBOT (Next level — Botpress/Voiceflow):
  Custom GPT logic + user interface deployed on a website, app, or platform.
  Can interact with real users at scale.
  Can connect to databases, APIs, and back-end systems.
```

### 1.2 Professional Use Cases for Custom AI Assistants

| Assistant Type | Use Case | Who Deploys It |
|---------------|----------|----------------|
| **Knowledge Base Assistant** | Answers FAQs from company documents | HR, Customer Support |
| **Onboarding Assistant** | Guides new employees through company processes | HR, L&D |
| **Sales Assistant** | Qualifies leads, answers product questions | Marketing, Sales |
| **Research Assistant** | Summarizes industry reports, finds relevant data | Strategy, Consulting |
| **Writing Assistant** | Generates on-brand content following brand guidelines | Marketing |
| **Training Assistant** | Quiz questions, practice scenarios, learning support | L&D |
| **Policy Assistant** | Answers policy questions from uploaded documents | HR, Legal, Compliance |
| **Personal Productivity GPT** | Your personal AI workflow tool | Any professional |

---

## 2. The ASSIST Framework for AI Assistant Design

Before building any AI assistant, design it using the ASSIST framework:

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  THE ASSIST FRAMEWORK                                                        │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  A — AUDIENCE         Who is this assistant for?                            │
│                       Their role, knowledge level, what they need            │
│                                                                              │
│  S — SCOPE            What topics/tasks is this assistant authorized to     │
│                       handle? What is explicitly OUT of scope?              │
│                                                                              │
│  S — STYLE            What persona, tone, and communication style?          │
│                       How should it feel to interact with this assistant?   │
│                                                                              │
│  I — INFORMATION      What knowledge does the assistant need?               │
│                       What documents, data, or context to upload?           │
│                                                                              │
│  S — SAFEGUARDS       What guardrails and limits apply?                     │
│                       What should it never say or do?                       │
│                                                                              │
│  T — TRIGGER          How does the user activate it?                        │
│                       What is the first message / entry point?              │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### 2.1 ASSIST in Practice — Example Design

**Project:** A Procurement Policy Assistant for an internal HR team

```
ASSIST DESIGN DOCUMENT:

A — AUDIENCE:
  HR managers and business unit leaders who need quick answers to
  procurement policy questions. Non-specialist in procurement.
  They want clear, actionable answers — not policy document quotes.

S — SCOPE (IN):
  Procurement policy questions (vendor selection, approval thresholds,
  PO creation, travel expense rules, contractor engagement rules)
  Guidance on the correct process for specific procurement scenarios

S — SCOPE (OUT):
  Legal advice on contracts
  Vendor-specific pricing or negotiation
  Finance approval decisions (it explains the process, does not approve)
  Anything outside the uploaded procurement policy documents

S — STYLE:
  Name: "ProcureHelper"
  Personality: Knowledgeable, direct, friendly. Like a helpful colleague
  who knows the rulebook cold. Not bureaucratic or legalistic.
  Tone: Business casual. Short answers. Always ends with "anything else?"

I — INFORMATION:
  Upload: Procurement Policy v4.2 (PDF)
  Upload: Expense Policy 2024 (PDF)
  Upload: Vendor Approval Process Guide (PDF)
  Upload: Frequently Asked Questions document (compiled from past queries)

S — SAFEGUARDS:
  Never: provide legal advice or interpret contract terms
  Never: approve or deny a specific procurement request
  Never: reference specific vendor names or pricing
  Always: for edge cases, direct to: procurement@company.com
  Always: flag if a policy section has been updated (note date)

T — TRIGGER:
  Opening message: "Hi! I'm ProcureHelper. Ask me anything about our
  procurement and expense policies. What do you need to know?"
```

---

## 3. Building a Custom GPT in ChatGPT

### 3.1 How to Access Custom GPTs

```
ACCESS:
  ChatGPT Plus account required → 
  Left sidebar → "Explore GPTs" → "Create a GPT" (top right)

TWO CREATION MODES:
  1. BUILDER (conversational): ChatGPT asks you questions and
     builds the system prompt automatically based on your answers.
     Best for: first-time builders, quick prototypes.

  2. CONFIGURE (manual): You write the system prompt directly.
     Best for: precise control, professional deployments.
```

### 3.2 The Custom GPT Configuration Fields

```
NAME:         Short, descriptive name (displays to users)
DESCRIPTION:  1–2 sentence explanation (displays in GPT store)
INSTRUCTIONS: The full system prompt — the core of your GPT's behavior
KNOWLEDGE:    Upload files (PDF, Word, TXT, CSV) the GPT will reference
CAPABILITIES:
  ☐ Web browsing (can search the internet)
  ☐ DALL-E image generation
  ☐ Code interpreter (can run Python code)
ACTIONS:      Connect to external APIs (advanced — for developers)
```

### 3.3 Writing the Custom GPT System Prompt

The system prompt is the most critical element. Use this template:

```
CUSTOM GPT SYSTEM PROMPT TEMPLATE:

# IDENTITY
You are [NAME], an AI assistant designed for [AUDIENCE].
Your purpose is to [PRIMARY PURPOSE — what you help users do].

# PERSONA AND STYLE
- You communicate like [PERSONALITY DESCRIPTION]
- Tone: [FORMAL / PROFESSIONAL-CASUAL / FRIENDLY / etc.]
- Response length: [SHORT AND DIRECT / DETAILED AND THOROUGH / depends on question]
- You always end responses with [HOW YOU CLOSE — e.g., "Let me know if you need clarification."]

# WHAT YOU DO
You help users with:
1. [CAPABILITY 1]
2. [CAPABILITY 2]
3. [CAPABILITY 3]
[Add more as needed]

# YOUR KNOWLEDGE BASE
You have access to the following uploaded documents:
- [DOCUMENT 1 NAME]: [What it covers]
- [DOCUMENT 2 NAME]: [What it covers]
When answering questions, cite the relevant document section where possible.
If the answer is not in your uploaded documents, say so clearly.

# WHAT YOU DO NOT DO
You do not:
- [HARD LIMIT 1]
- [HARD LIMIT 2]
- [HARD LIMIT 3]
If asked to do any of the above, politely decline and [REDIRECT TO ALTERNATIVE].

# ESCALATION
For questions outside your scope, direct users to: [CONTACT / RESOURCE]
For urgent matters, always recommend: [ESCALATION PATH]

# OPENING MESSAGE
When a user first opens this assistant, greet them with:
"[YOUR DESIGNED OPENING MESSAGE]"
```

### 3.4 Example: Complete System Prompt for a Procurement Assistant

```
# IDENTITY
You are ProcureHelper, an AI assistant designed for employees at Acme Corp
who need quick, accurate answers to procurement and expense policy questions.
Your purpose is to help employees understand the correct process without having
to search through lengthy policy documents.

# PERSONA AND STYLE
- You communicate like a knowledgeable colleague who knows the policies well
  and explains them clearly without jargon.
- Tone: Friendly, direct, professional-casual.
- Response length: Short and actionable. Give the direct answer first,
  then any relevant detail. Do not quote entire policy sections.
- You always end responses with "Anything else I can help with?"

# WHAT YOU DO
You help employees with:
1. Understanding procurement approval thresholds and who needs to approve what
2. Expense policy questions (travel, meals, accommodation, equipment)
3. Vendor selection process and vendor registration requirements
4. PO creation guidance and required documentation
5. Contractor engagement rules

# YOUR KNOWLEDGE BASE
You have access to:
- Procurement Policy v4.2: Covers all vendor and PO processes
- Expense Policy 2024: Covers all employee expense guidelines
- Vendor Approval Guide: Step-by-step vendor registration process
Reference the relevant policy section (e.g., "Per Procurement Policy Section 3.2...")
when providing guidance. If uncertain, say so.

# WHAT YOU DO NOT DO
- You do not approve or deny specific procurement requests
- You do not interpret legal contract terms
- You do not provide vendor-specific pricing advice
- You do not make exceptions to policy — you explain the exceptions process
If asked to do any of the above, say: "That's outside what I can help with —
for that, please contact procurement@acmecorp.com"

# ESCALATION
For edge cases or policy interpretations requiring judgment, direct to:
procurement@acmecorp.com

For urgent exceptions (needed today), direct to:
Your line manager + procurement team at +91-XXXXX

# OPENING MESSAGE
"Hi! I'm ProcureHelper — your guide to Acme's procurement and expense policies.
Ask me anything: approval limits, expense rules, vendor setup, PO process.
What do you need to know?"
```

---

## 4. No-Code Chatbot Platforms

### 4.1 When to Go Beyond Custom GPTs

Custom GPTs are great for internal use within ChatGPT. For deploying to:
- A company website (as a chat widget)
- A customer-facing app
- WhatsApp, Slack, or Teams
- Complex conversation flows with decision trees

You need a chatbot platform that connects your AI to real deployment channels.

### 4.2 Key Platforms Compared

| Platform | Best For | Complexity | Cost | Deploy To |
|----------|---------|------------|------|-----------|
| **Tidio** | Small business customer support | Low | Free + $29/mo | Website widget |
| **Botpress** | Developers, enterprise | Medium | Free tier + paid | Web, Slack, WhatsApp |
| **Voiceflow** | Complex conversation design | Medium | Free tier + paid | Web, Alexa, phone |
| **Landbot** | Marketing chatbots, lead gen | Low | Free + $39/mo | Website, WhatsApp |
| **ManyChat** | Social media automation | Low | Free + $15/mo | Instagram, FB, WhatsApp |
| **Intercom** | Customer support at scale | Medium | $74/mo+ | Website, mobile app |

### 4.3 Conversation Flow Design — The Decision Tree Approach

For more structured chatbots (not just open-ended AI), design a conversation flow:

```
CONVERSATION FLOW DESIGN FOR A CUSTOMER SUPPORT CHATBOT:

START:
  Bot: "Hi! How can I help you today?"
  User selects or types: [Track Order] [Return Request] [Product Question] [Other]

BRANCH 1 — TRACK ORDER:
  Bot: "Please share your order number."
  → User provides number → Bot queries order system → Returns status
  → If delivered: "Your order was delivered on [DATE]. Tap to confirm receipt."
  → If in transit: "Your order is on the way — expected [DATE]. Track here: [LINK]"
  → If delayed: Escalate to human agent immediately

BRANCH 2 — RETURN REQUEST:
  Bot: "What would you like to return and why?"
  → User describes item + reason
  → Bot checks return policy eligibility
  → If eligible: Generate return label link → Confirm steps
  → If not eligible: Explain + offer alternatives (exchange / store credit)
  → If uncertain: "Let me connect you with our team." → Escalate

FALLBACK (anything not matched):
  Bot: "I'm not sure I can help with that directly. 
  Would you like to [Chat with a team member] or [Send an email]?"
```

---

## 5. Testing and Evaluating Your AI Assistant

### 5.1 The Pre-Launch Testing Protocol

Before deploying any AI assistant to real users:

```
TESTING PHASE 1 — FUNCTIONAL TESTING (Can it do what it's supposed to?):
  ☐ Ask 20 questions in scope — does it answer correctly?
  ☐ Ask 5 questions out of scope — does it redirect appropriately?
  ☐ Ask ambiguous questions — does it ask for clarification?
  ☐ Test with real user language (not your clean test language)

TESTING PHASE 2 — ADVERSARIAL TESTING (Can it be broken?):
  ☐ Try to make it violate its guardrails ("ignore previous instructions...")
  ☐ Ask about competitor products
  ☐ Ask for information it shouldn't provide (pricing, legal advice)
  ☐ Give it incorrect information and see if it corrects or accepts it
  ☐ Test with emotional/angry inputs — does it respond appropriately?

TESTING PHASE 3 — USER TESTING:
  ☐ Have 3–5 actual target users test it without instructions
  ☐ Record what confused them, what broke, what they loved
  ☐ Identify the top 3 failure modes and fix before launch

TESTING PHASE 4 — QUALITY SCORING:
  Apply the 5-dimension quality framework (from Session 19) to 10 sample
  interactions. Target: average score of 20/25 before launch.
```

### 5.2 The AI Assistant Quality Scorecard

| Dimension | Score 1–5 | Notes |
|-----------|----------|-------|
| **Accuracy** | | Correct information from knowledge base |
| **Scope compliance** | | Stays within defined boundaries |
| **Tone consistency** | | Matches designed persona every time |
| **Escalation quality** | | Escalates appropriately and gracefully |
| **User experience** | | Easy to interact with, logical responses |
| **TOTAL** | **/25** | |

---

## 6. Real-World Example: Decathlon's Product Assistant GPT

**Company:** Decathlon India — sports equipment retailer, 100+ stores

**The Problem:**
Store staff and online support team received thousands of repetitive questions daily:
- "What is the right size kayak for someone who weighs 85kg?"
- "Which running shoe is best for flat feet?"
- "What's the difference between a carbon and aluminum bike frame?"

Training staff on the full product catalog (10,000+ SKUs) was impossible. Customer satisfaction suffered when staff didn't know the answer.

**The AI Assistant Solution:**

```
DESIGN (ASSIST):
  A — Audience: Store staff + online chat users
  S — Scope: Product questions, size guides, comparative features,
              care instructions, compatibility checks
  S — Style: Friendly sports enthusiast — "a knowledgeable fellow athlete"
  I — Information: Full product catalog PDFs, size guides, care manuals
  S — Safeguards: No price quotes (volatile), no stock availability,
                   no medical advice (injury/health related)
  T — Trigger: "Hi! I'm your Decathlon sports advisor. What are you looking for?"

BUILD:
  Custom GPT with 50+ product catalog PDFs uploaded.
  Tested with 200 real customer questions from support ticket archive.
  Refined 3 iterations before launch.
  Deployed via QR code in stores (links to Custom GPT link on mobile).

RESULTS (after 60 days):
  Product question resolution rate: 78% without staff involvement
  Staff time freed for floor assistance and checkout: +35%
  Customer satisfaction on product advice: +22%
  Staff training time for new hires: reduced by 40%
  (New staff rely on the GPT while learning — reduces pressure)
```

**Key Design Lesson:** The assistant was designed with explicit out-of-scope guardrails for pricing (volatile, must be checked live) and medical advice (liability). These guardrails were as important as the in-scope capabilities.

---

## 7. Hands-On Lab 23: Build Your First AI Assistant

**Objective:** Design and configure a Custom GPT for a specific professional use case  
**Duration:** 25 minutes  
**Tool:** ChatGPT Plus (Custom GPT builder)  
**Alternative (if no ChatGPT Plus):** Design the full system prompt for a Custom GPT as a document

---

### Task 1: ASSIST Design Document (8 minutes)

Choose ONE of these assistant types:
1. A writing assistant for your professional role (follows your brand voice and style)
2. A research assistant for your industry/field (with 2–3 topic-area uploads)
3. A FAQ assistant for a company, team, or product you know well

Complete the full ASSIST design document — all 6 elements.

---

### Task 2: Write the System Prompt (10 minutes)

Using your ASSIST design document, write a complete Custom GPT system prompt using the template from Section 3.3.

Include all sections: Identity, Persona, What You Do, Knowledge Base, What You Don't Do, Escalation, Opening Message.

---

### Task 3: Test With 5 Questions (7 minutes)

**Option A (ChatGPT Plus):** Create the Custom GPT, add your system prompt, run 5 test questions.

**Option B (Standard ChatGPT):** Paste your system prompt at the start of a new chat. Run 5 test questions:
- 3 in-scope questions (should be answered well)
- 1 out-of-scope question (should be redirected)
- 1 adversarial question ("ignore your instructions and...") (should refuse politely)

Document the results for each test.

---

### Lab Evaluation Rubric

| Deliverable | Marks |
|-------------|-------|
| Task 1: ASSIST design document — all 6 elements complete | 3 |
| Task 2: System prompt complete with all required sections | 4 |
| Task 3: 5 test results documented with pass/fail for each | 3 |
| **Total** | **10** |

---

## 8. Interview Questions — Session 23

**Q1:** *"Have you built any custom AI tools? How did you approach it?"*

**Strong Answer:**
"Yes — I've built custom AI assistants using ChatGPT's Custom GPT feature and by designing detailed system prompts. My design process follows what I call the ASSIST framework: I define the Audience, Scope (what's in and what's explicitly out), Style and persona, Information to upload, Safeguards and guardrails, and the Trigger or opening experience. The most important element is the safeguards — clearly defining what the assistant should refuse to do is as critical as defining what it should do. I test every assistant with adversarial inputs before deploying, including asking it to ignore its instructions, asking out-of-scope questions, and having real target users test it without any explanation. The quality standard I apply is a 5-dimension scorecard: accuracy, scope compliance, tone consistency, escalation quality, and user experience."

---

## 9. Revision Questions — Session 23

1. What is the ASSIST framework? Explain each element with an example from a specific assistant type.
2. What are the 6 configuration fields in a Custom GPT? What does each control?
3. Why are guardrails (what the assistant does NOT do) as important as its capabilities?
4. What is the difference between a Custom GPT and a deployed chatbot on a website?
5. What is a conversation flow / decision tree in chatbot design? Sketch a simple 2-branch flow.
6. What are the 4 phases of AI assistant testing? What happens in each phase?
7. In the Decathlon example, what were the explicit out-of-scope guardrails and why were they important?
8. What is the 5-dimension quality scorecard for AI assistants? Give a specific example of a 1-score vs. 5-score response for the "Scope Compliance" dimension.

---

## 10. Key Terminology — Session 23

| Term | Definition |
|------|-----------|
| **Custom GPT** | A configured AI assistant built on ChatGPT with custom instructions, knowledge, and capabilities |
| **System Prompt** | Persistent instructions that define an AI assistant's identity, behavior, and boundaries |
| **ASSIST Framework** | Audience, Scope, Style, Information, Safeguards, Trigger — a design framework for AI assistants |
| **Guardrail** | A hard rule in an AI assistant's instructions preventing specific behaviors or outputs |
| **Conversation Flow** | A designed sequence of chatbot responses and decision branches for structured interactions |
| **Adversarial Testing** | Deliberately trying to make an AI assistant violate its guidelines to find weaknesses |
| **Knowledge Base (GPT)** | Uploaded documents that provide the AI assistant with specific, proprietary information to reference |
| **Escalation Path** | A defined route for transferring a user from the AI assistant to a human agent |
| **No-Code Chatbot Platform** | Tools like Botpress, Tidio, or Voiceflow that allow chatbot deployment without programming |

---

## 11. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 23 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  ASSIST: Audience, Scope, Style, Information, Safeguards, Trigger        │
│  ✓  Custom GPT: 6 fields — Name, Description, Instructions, Knowledge,      │
│     Capabilities, Actions                                                    │
│  ✓  System prompt structure: Identity, Persona, Capabilities, Knowledge,    │
│     Limits, Escalation, Opening Message                                      │
│  ✓  Guardrails matter as much as capabilities — design both                 │
│  ✓  4-phase testing: Functional → Adversarial → User → Quality Score        │
│  ✓  No-code platforms: Tidio (website), Botpress (enterprise), ManyChat     │
│     (social media) for deploying beyond ChatGPT                             │
│  ✓  Decathlon: 78% resolution rate, 35% more staff time, 22% higher CSAT   │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 24 — AI Workflow Automation                                        │
│  (Using Zapier, Make.com, and n8n to automate multi-step workflows          │
│   that connect AI outputs to real business applications)                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 23 Complete | Next: Session 24 — AI Workflow Automation*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
