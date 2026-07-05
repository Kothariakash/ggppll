# Session 20: AI for Customer Support
## Module 4 — Business & Industry Applications
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 20 OF 30  │  Module 4, Session 5                          │
│  Topic: AI for Customer Support — Responses, Workflows & Chatbots   │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Use AI to draft empathetic, effective customer support responses
2. Build response templates for common support scenarios
3. Design a tiered escalation prompt system for support teams
4. Create FAQ content and knowledge base articles with AI
5. Design a basic AI chatbot persona for customer-facing support
6. Apply quality evaluation frameworks to AI-generated support content

---

## 20.1 AI in Customer Support — The Opportunity

Customer support is one of the highest-volume, most repetitive writing tasks in any business. AI can assist with:

```
HIGH AUTOMATION POTENTIAL:               REQUIRES HUMAN JUDGMENT:
──────────────────────────────           ──────────────────────────────────────
Standard inquiry responses               Complex complaints with legal implications
FAQ content generation                   Escalated customer situations
Knowledge base articles                  VIP customer handling
Response tone improvement                Refund / compensation decisions
Ticket categorization and routing        Crisis communication
Agent response drafting                  Situations involving safety or urgency
First-draft responses for review         Account security and identity verification
```

**The Customer Support AI Rule:** AI drafts and assists — trained human agents make final judgment calls on escalated issues, compensation, and anything that could create legal or reputational risk.

---

## 20.2 Customer Support Response Types

### The Empathy-First Response Framework

Every customer support response must follow this structure:

```
1. ACKNOWLEDGE — Validate the customer's experience (not just their request)
2. EMPATHIZE — Show genuine understanding of the impact
3. TAKE OWNERSHIP — Accept responsibility (even if the cause isn't entirely yours)
4. RESOLVE — State what you will do (specific, with timeline)
5. PREVENT — What will stop this from happening again (if applicable)
6. OFFER MORE — Invite further questions; close warmly
```

### Response Type 1: Standard Inquiry Response

```
Write a customer support response to the following inquiry.

Customer tier: [Standard / Premium / Enterprise]
Inquiry type: [Product question / Feature request / How-to / Policy question]
Customer's message: [PASTE THE CUSTOMER'S MESSAGE]

Response requirements:
- Directly answer their question in the first paragraph
- If multiple questions: answer each in numbered order
- Provide the relevant information clearly and simply
- End with an offer to help further

Tone: Helpful, warm, professional. Not overly formal. First-name basis if name known.
Length: Under 150 words (they want the answer, not a document).
Do not: Use "Please be advised", "As per our records", or corporate jargon.
Do not: Make promises we cannot keep or cite policies inaccurately.
```

---

### Response Type 2: Complaint / Frustrated Customer

```
Write a customer support response to an unhappy customer.

Customer's complaint: [PASTE MESSAGE]
What actually happened: [YOUR VERSION OF EVENTS — honest]
What we CAN offer: [What resolution options are available?]
What we CANNOT offer: [Honest constraints — don't overpromise]
Customer's tier and history: [NEW / LOYAL / VIP / AT-RISK OF CHURN]

Response structure (mandatory):
1. ACKNOWLEDGE: First sentence — validate their frustration specifically
   (mirror what they said, not generic "I understand your frustration")
2. EMPATHIZE: Show you understand the IMPACT, not just the event
3. EXPLAIN: Brief, factual explanation (1–2 sentences — not excuses)
4. RESOLVE: What we will do — specific action + timeline
5. COMPENSATE (if applicable): What we're offering as goodwill
6. CLOSE: Invite them to reach back; warm, genuine closing

Critical rules:
- NEVER start with "I apologize for any inconvenience" — it's meaningless
- NEVER use passive voice in the resolution ("Your refund will be processed")
  → Use active: "I will process your refund by [date]"
- Acknowledge the specific thing they complained about, not a generic complaint
- If a loyal customer: acknowledge loyalty explicitly (brief, genuine)

Tone: Empathetic, accountable, solution-focused. Human, not scripted.
```

---

### Response Type 3: Cannot-Help / Policy-Limit Response

```
Write a customer support response declining a request while maintaining goodwill.

Customer's request: [PASTE]
Why we cannot fulfill it: [POLICY / TECHNICAL LIMITATION / TIMING]
What we CAN offer as an alternative: [ANY PARTIAL SOLUTION OR WORKAROUND]

Decline response rules:
1. Lead with empathy, not the refusal
2. Explain WHY briefly — customers respect honest reasons more than "policy says no"
3. State what you CAN do (not just what you can't)
4. Offer an alternative path where possible
5. Close with genuine goodwill — not a formulaic "Thank you for your understanding"

What NOT to do:
- "I'm afraid we're unable to..." → Just say "We can't, because..."
- "Our policy states that..." → "To ensure fairness for all customers, we..."
- "Thank you for your understanding" → Only say this if they might not understand
- Apologizing excessively for a reasonable policy

Tone: Direct, kind, honest. They should leave feeling respected even if disappointed.
```

---

### Response Type 4: Escalation Acknowledgment

```
Write an escalation acknowledgment response.

Context:
Customer's issue: [DESCRIBE — what has gone wrong, how many times it's happened]
Previous attempts: [WHAT RESOLUTION WAS ALREADY TRIED AND FAILED]
Escalating to: [WHICH TEAM OR LEVEL]
Timeline for resolution: [REALISTIC TIMEFRAME]

Escalation acknowledgment must:
1. Open by acknowledging this is unacceptable and that you understand why they're escalating
2. Take clear ownership — don't blame the previous agent or "the system"
3. Give the customer a NAMED CONTACT (or at minimum a specific team/reference number)
4. State explicitly what will happen and by WHEN
5. Give them a direct channel to follow up (specific — not "contact us")
6. Optional: goodwill gesture for significant issues

Tone: Senior-level accountability. The customer should feel this is being taken seriously.
```

---

## 20.3 Building a Support Response Template Library

### Template Library Structure for Support Teams

```
TEMPLATE ID: SUP-[CATEGORY]-[NUMBER]
CATEGORY: [BILLING / TECHNICAL / DELIVERY / PRODUCT / RETURNS / ACCOUNT]
SCENARIO: [Specific situation this template handles]
TRIGGER: [Keywords or conditions that activate this template]
CUSTOMER TIER: [All / Standard only / Premium+ only]
LAST REVIEWED: [DATE — templates need quarterly review]

TEMPLATE:
─────────────────────────────────────────────────────────────
[COMPLETE RESPONSE TEXT WITH VARIABLES IN {CURLY BRACKETS}]
─────────────────────────────────────────────────────────────

VARIABLES:
{CUSTOMER_NAME} — customer's first name
{ORDER_NUMBER} — their reference number
{DATE} — specific date or timeframe
{AGENT_NAME} — responding agent's name

TONE GUIDANCE:
[Brief note on how to calibrate for different emotional levels]

DO NOT USE WHEN:
[Conditions where this template is inappropriate]

ESCALATION TRIGGER:
[If customer responds with X, escalate immediately]
```

---

### Generating a Support Template Library

```
Generate a customer support response template library for a [TYPE OF BUSINESS].

Business: [DESCRIBE — what you sell, who your customers are]
Support channels: [Email / Chat / Phone script / Social media DM]
Most common support scenarios: [LIST 8–10]

For each scenario, create a response template that:
1. Has a clear template ID and category
2. Contains the full response with {VARIABLE} placeholders
3. Has a 1-sentence tone note
4. Includes an escalation trigger line
5. Is under 200 words (email) or under 80 words (chat/social)

Scenarios to cover:
1. Order delayed beyond expected delivery date
2. Wrong item received
3. Refund request (within policy)
4. Refund request (outside policy)
5. Technical issue — app not working
6. Account access problem / login issue
7. Billing error / double charge
8. Product quality complaint
9. Request for feature that doesn't exist
10. Cancellation request

Tone across all templates: [BRAND VOICE — describe: warm / professional / friendly / formal]
```

---

## 20.4 FAQ and Knowledge Base Creation

### FAQ Generation Prompt

```
Generate a comprehensive FAQ section for [PRODUCT/SERVICE/TOPIC].

Target audience: [WHO WILL READ THIS — new customers / existing users / technical buyers]
Format: Question + Answer, organized by category

Categories to cover:
1. Getting Started (4–5 questions)
2. Account & Billing (4–5 questions)
3. Product Features (5–6 questions)
4. Troubleshooting (4–5 questions)
5. Policies (3–4 questions)

For each FAQ entry:
- Question: Written as a customer would actually ask it (conversational, not formal)
- Answer: Clear, direct, under 100 words
- If multi-step: numbered list format
- If policy-related: include the "why" briefly

SEO principle: Write questions the way customers search, not the way we think about them.
Example: NOT "What is the cancellation protocol?" → "How do I cancel my subscription?"

After the FAQ, generate: 5 related questions we should add in the next version
(questions customers are likely asking that we haven't answered yet).

Context for FAQ: [DESCRIBE YOUR PRODUCT/SERVICE AND KEY POLICIES]
```

---

### Knowledge Base Article Generator

```
Write a knowledge base article on: [TOPIC]

Article type: [How-to / Troubleshooting / Concept explanation / Policy]
Product/feature involved: [DESCRIBE]
Target reader: [Self-service customer / Support agent / Both]
Technical level: [Non-technical / Intermediate / Technical]

Knowledge base article structure:

TITLE: [Action-oriented, searchable — "How to [do X]" or "Why [X] happens"]
DESCRIPTION (under article title): 2 sentences — what this article covers + who it's for

OVERVIEW: 1 paragraph — brief explanation of what this feature/topic is

[FOR HOW-TO]:
PREREQUISITES: What the reader needs before starting (software, account level, etc.)
STEPS:
  Step 1: [Clear action verb + what to do]
  Screenshot placeholder: [describe what screenshot should show]
  Step 2: [Next action]
  ...
EXPECTED RESULT: What happens when steps are completed successfully

[FOR TROUBLESHOOTING]:
SYMPTOMS: Bullet list of what the user experiences
COMMON CAUSES: 3–4 most frequent reasons for this issue
SOLUTIONS (try in this order):
  Solution 1: [Most common fix — step by step]
  Solution 2: [Next option]
  If these don't work: [Escalation path]

RELATED ARTICLES: [List 3 suggested related topics]
LAST UPDATED: [DATE PLACEHOLDER]
HELPFUL? YES / NO / FEEDBACK LINK
```

---

## 20.5 AI Chatbot Persona Design

For organizations building AI-powered customer-facing chatbots using LLM APIs.

### Chatbot Persona and System Prompt

```python
"""
Building a customer support chatbot for [COMPANY] using the OpenAI API.

The system prompt defines the chatbot's behavior, persona, and boundaries.
"""

CHATBOT_SYSTEM_PROMPT = """
You are Aria, the virtual customer support assistant for CloudShop India,
an e-commerce platform specializing in electronics and home appliances.

YOUR PERSONA:
- Friendly, helpful, and patient — like a knowledgeable store associate
- Professional but not stiff — you use natural, conversational language
- Honest about what you can and cannot help with
- You refer to the customer by their first name once you know it

YOUR KNOWLEDGE:
- Full product catalog descriptions and specifications
- Shipping policies: standard (5–7 days), express (1–2 days), free above ₹999
- Return policy: 30 days for most products, 7 days for large appliances
- Warranty handling: 1-year manufacturer warranty on all electronics
- Common troubleshooting steps for top 20 products

YOUR LIMITATIONS (be honest — don't guess or invent):
- You cannot access live order tracking (direct to track.cloudshop.in)
- You cannot process refunds (direct to support@cloudshop.in with subject REFUND)
- You cannot access account payment information
- You cannot make exceptions to policies (escalate to human agent)
- Your product knowledge extends to items listed before [CUTOFF DATE]

RESPONSE RULES:
- Answer the question first, then offer additional help
- Keep responses under 100 words unless a detailed how-to is genuinely needed
- Never say "I cannot help with that" without offering an alternative path
- If uncertain: say "I want to make sure I give you accurate information —
  let me connect you with a specialist for this." Then provide escalation path.
- For complaints: acknowledge the issue empathetically before offering a solution
- For escalation triggers (refund disputes, safety issues, legal threats):
  immediately route to human agent without attempting to resolve

ESCALATION TRIGGERS (route immediately to human):
- Customer mentions legal action, consumer forum, or media
- Customer reports safety hazard with a product
- Customer expresses extreme distress or mentions personal hardship
- Refund of ₹5,000+ that has been previously denied
- Any issue a customer says has occurred more than twice

Escalation response: "I completely understand, and I want to make sure
this is handled with the care it deserves. Let me connect you right now
with [name], our Customer Resolution Specialist. They will be with you
within [timeframe]. Your reference number is [REF]. Is there anything
else I can help with in the meantime?"
"""


def create_support_chatbot(customer_message: str, conversation_history: list) -> str:
    """
    Create a customer support response using the chatbot persona.
    
    Args:
        customer_message: The latest message from the customer
        conversation_history: List of previous messages in the conversation
    
    Returns:
        The chatbot's response string
    """
    from openai import OpenAI
    client = OpenAI()
    
    # Add customer message to history
    conversation_history.append({
        "role": "user",
        "content": customer_message
    })
    
    # Build the full messages array
    messages = [
        {"role": "system", "content": CHATBOT_SYSTEM_PROMPT}
    ] + conversation_history
    
    response = client.chat.completions.create(
        model="gpt-4o",
        messages=messages,
        temperature=0.4,   # Lower temperature for consistent, reliable support responses
        max_tokens=300     # Keep responses concise for chat format
    )
    
    assistant_response = response.choices[0].message.content
    
    # Add response to history for context in next turn
    conversation_history.append({
        "role": "assistant",
        "content": assistant_response
    })
    
    return assistant_response


# Example usage
if __name__ == "__main__":
    history = []
    
    # Simulate a support conversation
    queries = [
        "Hi, my order hasn't arrived yet and it's been 10 days.",
        "My order number is CS-847291. I chose standard shipping.",
        "Can I get a refund if it doesn't arrive by tomorrow?"
    ]
    
    for query in queries:
        print(f"\nCustomer: {query}")
        response = create_support_chatbot(query, history)
        print(f"Aria: {response}")
```

---

## 20.6 Quality Evaluation for Support Responses

### Response Quality Rubric

```
Evaluate the following customer support response against these criteria.
Score each 1–5 and provide one specific improvement per criterion below 4.

CUSTOMER MESSAGE: [paste customer's message]
SUPPORT RESPONSE: [paste the support response]

Evaluation criteria:

1. EMPATHY (Does the response acknowledge the customer's feelings/experience?)
   1 = No empathy | 3 = Generic acknowledgment | 5 = Specific, genuine empathy

2. ACCURACY (Is the information provided correct and complete?)
   1 = Wrong/incomplete | 3 = Mostly correct | 5 = Fully accurate and complete

3. RESOLUTION (Does the response solve or clearly advance the issue?)
   1 = No resolution offered | 3 = Partial resolution | 5 = Clear, complete resolution

4. TONE (Is the tone appropriate for the customer's emotional state?)
   1 = Wrong tone | 3 = Adequate | 5 = Perfectly calibrated to situation

5. CLARITY (Is the response easy to understand? No jargon?)
   1 = Confusing | 3 = Mostly clear | 5 = Crystal clear, no ambiguity

6. CONCISENESS (Is it appropriately brief — no padding?)
   1 = Way too long | 3 = Acceptable length | 5 = Perfect length for the situation

7. NEXT STEP (Is there a clear next step or call to action?)
   1 = No next step | 3 = Vague next step | 5 = Specific, easy next step

OVERALL SCORE: [total / 35]
MOST IMPORTANT IMPROVEMENT: [single highest-impact change]
REWRITTEN VERSION: [Provide improved version if score below 28/35]
```

---

## 20.7 Support Metrics and AI Impact

### Building a Support Analytics Dashboard (Prompt)

```
Help me design a customer support analytics dashboard for [TEAM SIZE] agents
handling [VOLUME] tickets per [PERIOD].

Key metrics to track (generate definitions and formulas for each):
1. First Response Time (FRT)
2. First Contact Resolution Rate (FCR)
3. Customer Satisfaction Score (CSAT)
4. Average Handle Time (AHT)
5. Ticket Volume by Category
6. Escalation Rate
7. Agent Utilization Rate
8. AI Assist Usage Rate (% of responses using AI drafts)

For each metric:
- Definition (plain English)
- Formula (how to calculate)
- Industry benchmark (flag for verification)
- Target for our team
- What to do if this metric is trending negatively

Also generate: 3 leading indicators that predict customer churn
before it shows up in CSAT scores.
```

---

## Module 4 Summary

| Session | Topic | The One Sentence |
|---------|-------|-----------------|
| **Session 16** | Marketing & Content | Brand voice is the foundation — establish it once, include it in every content prompt. |
| **Session 17** | HR | AI assists human judgment in HR — it never replaces it; every output needs professional review. |
| **Session 18** | Finance & Data | AI for language and code; calculators and auditors for verified numbers. |
| **Session 19** | Strategy & BizDev | AI builds the thinking infrastructure; human judgment makes the actual strategic decision. |
| **Session 20** | Customer Support | Empathy-first responses with clear resolution and next steps — AI drafts, humans approve escalations. |

---

## Hands-On Activities — Session 20

---

### Activity 20.1 — Response Type Practice

Write AI-assisted responses for all 4 response types:

**Scenario 1 (Complaint):**
"I ordered a laptop 2 weeks ago, paid for express shipping, and it still hasn't arrived. I called 3 times and got different answers each time. This is completely unacceptable."

**Scenario 2 (Cannot Help):**
"I'd like a refund on the software I downloaded 45 days ago. I know your policy says 30 days but I really didn't use it much."

**Scenario 3 (Standard Inquiry):**
"Does your premium plan include API access and if so, what are the rate limits?"

**Scenario 4 (Escalation):**
"I have spoken to 4 agents, nothing has been resolved, and I am now going to post this on social media and contact the consumer forum."

For each: run the appropriate prompt, then score the output using the Quality Rubric (Section 20.6).

---

### Activity 20.2 — FAQ Generation

**Objective:** Build a real FAQ for a product or service you know.

Choose: your company's product, a product you use, or invent a simple product.

Run the FAQ Generation prompt. Then evaluate:
- Are the questions written the way a customer would actually ask?
- Are the answers under 100 words?
- Does the FAQ cover the real scenarios or the "official" scenarios?
- What 5 additional questions should be added?

---

### Activity 20.3 — Chatbot Persona Design

**Objective:** Design a customer support chatbot persona for your organization.

Fill in the chatbot system prompt template (Section 20.5) for a real or hypothetical business.

Key design decisions you must make:
- What can the bot handle autonomously vs. what escalates?
- What are the escalation triggers?
- What is the escalation path and response?
- What is the persona's name and voice?

**Test it:** Use your system prompt with ChatGPT. Play the role of different types of customers (easy inquiry, frustrated customer, escalation scenario). Does the bot handle each appropriately?

---

### Activity 20.4 — Quality Rubric Audit

**Objective:** Evaluate 3 real customer support responses you've received.

Find 3 emails or chat transcripts from customer support interactions you've had (any company).

Run the Quality Evaluation Rubric on each.

**Analysis:**
- What was the average score across the 3 responses?
- Which criterion is most commonly weak?
- What would you teach a support team to improve based on this analysis?

---

## Revision Questions — Session 20

1. What is the Empathy-First Response Framework? List the 6 elements in order.
2. Why should support responses never start with "I apologize for any inconvenience"?
3. What 5 elements must a support template library entry contain to be genuinely useful?
4. Describe the difference between a FAQ article and a knowledge base article. What is each designed to accomplish?
5. Name 5 escalation triggers that should route immediately to a human agent, bypassing the AI chatbot.
6. What is the temperature setting you would use for a customer support chatbot and why?
7. A customer says "I'm going to post about this on Twitter and contact a consumer forum." How should a well-designed AI chatbot respond?
8. Describe the 7 criteria in the support response quality rubric. For a response scoring below 28/35, what is the recommended action?

---

## Key Takeaways — Session 20

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 20 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Empathy-first always: Acknowledge → Empathize → Own → Resolve   │
│    → Prevent → Offer more                                           │
│                                                                      │
│  ✓ 4 response types: Inquiry | Complaint | Decline | Escalation    │
│    Each has a distinct structure — match the structure to the type  │
│                                                                      │
│  ✓ Templates accelerate without sacrificing quality —               │
│    variables ensure personalization within a consistent structure   │
│                                                                      │
│  ✓ Chatbot design: define boundaries before capabilities —          │
│    what it escalates is more important than what it handles         │
│                                                                      │
│  ✓ Escalation triggers are non-negotiable: legal threats, safety   │
│    hazards, extreme distress — always route to humans               │
│                                                                      │
│  ✓ Quality rubric: 7 criteria, score out of 35 — use it to train  │
│    agents and to audit AI-generated draft responses                 │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Module 4 Complete → Proceed to Module 5: Advanced Prompt Engineering (Session 21)*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
