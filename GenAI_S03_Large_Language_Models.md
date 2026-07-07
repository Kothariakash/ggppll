# Session 3: Large Language Models — The Brain Behind AI Tools
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 1 — AI FOUNDATIONS                                                   │
│  SESSION 3 of 30  |  1 Hour  |  50% Theory + 50% Hands-On                  │
│                                                                              │
│  "Knowing how the engine works makes you a better driver.                   │
│   Knowing how LLMs work makes you a better AI user."                        │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 3, you will be able to:

- Define a Large Language Model (LLM) and explain what makes it "large"
- Describe how an LLM generates responses using token prediction
- Explain tokens, context windows, and temperature with practical examples
- Compare the major LLMs (GPT-4o, Claude, Gemini, Copilot, Llama) and their strengths
- Select the appropriate LLM for a given professional task
- Understand why the same prompt can produce different outputs at different times

---

## 1. What is a Large Language Model?

### 1.1 The Definition

> A **Large Language Model (LLM)** is an AI system trained on massive amounts of text data that can understand, generate, and manipulate human language with remarkable fluency and accuracy.

"**Large**" refers to two dimensions simultaneously:

```
┌─────────────────────────────────────────────────────────────────────┐
│  DIMENSION 1: Training Data Size                                    │
│  ─────────────────────────────                                      │
│  GPT-3 (2020)  → ~570 GB of text  ≈  1,000,000 books              │
│  GPT-4 (2023)  → Estimated 10–13 trillion tokens                   │
│  Claude 3      → Multimodal — text, images, code combined           │
│  Gemini 1.5    → 1 million token context; text + audio + video     │
│                                                                     │
│  Comparison: All books in the Library of Congress ≈ 17 million     │
│  GPT-4 training data >> Library of Congress read 100+ times        │
├─────────────────────────────────────────────────────────────────────┤
│  DIMENSION 2: Model Size (Parameters)                               │
│  ────────────────────────────────────                               │
│  GPT-2 (2019)  →   1.5 Billion parameters                          │
│  GPT-3 (2020)  → 175 Billion parameters                            │
│  GPT-4 (2023)  → Estimated 1 Trillion+ parameters                  │
│  Human brain   → ~100 Trillion neural connections                   │
│                                                                     │
│  Parameters = the mathematical "weights" the model adjusts         │
│  during training to learn patterns. More parameters =              │
│  more nuanced pattern-recognition capability.                       │
└─────────────────────────────────────────────────────────────────────┘
```

---

### 1.2 How an LLM Generates a Response — Step by Step

The core mechanism is deceptively simple but enormously powerful at scale:

**The LLM's fundamental task: predict the next most likely token.**

```
Step 1: You type a prompt
────────────────────────
"Write a subject line for an apology email about a delayed shipment"

Step 2: LLM converts your text to tokens
─────────────────────────────────────────
["Write", " a", " subject", " line", " for", " an", " apology",
 " email", " about", " a", " delayed", " shipment"]

Step 3: LLM processes ALL tokens simultaneously (Transformer)
──────────────────────────────────────────────────────────────
Understands: Task=write, Type=subject line, Context=apology, 
             Reason=delay, Medium=email

Step 4: LLM generates the first output token
──────────────────────────────────────────────
Probabilities calculated:
  "Apology" → 28%   ← selected
  "Update"  → 19%
  "Re:"     → 15%
  "Notice"  → 12%
  
Output so far: "Apology"

Step 5: Using "Apology" as new context, generates next token
──────────────────────────────────────────────────────────────
  ":"        → 31%   ← selected
  "Regarding"→ 22%
  "for"      → 18%

Output so far: "Apology:"

Step 6: Continues until response is complete
──────────────────────────────────────────────
Final output: "Apology: Delay in Your Recent Shipment — We're On It"
```

**Key insight:** The LLM does not "know" the answer and retrieve it. It **constructs** the answer word by word, each token influenced by everything that came before. This is why:
- Output quality improves with more detailed prompts (more context = better token predictions)
- The same prompt can give slightly different outputs each time
- Temperature setting changes how "bold" each token selection is

---

## 2. The Three Critical Technical Concepts

### 2.1 Tokens — The Currency of LLMs

**Definition:** A token is the basic unit of text that an LLM processes. Tokens are NOT the same as words — they are subword chunks the model learned during training.

```
TOKENIZATION EXAMPLES:
─────────────────────
"Hello"           = 1 token
"Hello, world!"   = 4 tokens  ["Hello", ",", " world", "!"]
"Unbelievable"    = 3 tokens  ["Un", "believ", "able"]
"ChatGPT"         = 2 tokens  ["Chat", "GPT"]
"I am happy."     = 4 tokens  ["I", " am", " happy", "."]
"artificial"      = 2 tokens  ["art", "ificial"]
"entrepreneurship"= 4 tokens  ["entre", "pren", "eur", "ship"]

Rule of thumb:
  1 token ≈ 0.75 words
  100 tokens ≈ 75 words ≈ a short paragraph
  1,000 tokens ≈ 750 words ≈ a 1.5-page document
  4,096 tokens ≈ 3,000 words ≈ a 6-page document
```

**Why tokens matter practically:**

| Reason | Practical Impact |
|--------|----------------|
| **Pricing** | AI APIs charge per token — knowing token counts helps estimate cost |
| **Context limits** | Every model has a maximum token budget for input + output |
| **Response length** | Setting `max_tokens=500` limits how long the AI response can be |
| **Efficiency** | Concise prompts use fewer tokens and often get better results |

**Token counting example for budget planning:**

```
Your prompt: 150 words → ~200 tokens
Expected response: 500 words → ~667 tokens
Total per query: ~867 tokens

GPT-4o pricing (as of 2024):
  Input:  $0.005 per 1,000 tokens
  Output: $0.015 per 1,000 tokens

Cost per query:
  Input:  200 tokens × $0.005/1K = $0.001
  Output: 667 tokens × $0.015/1K = $0.010
  Total:  ~$0.011 per query (~1 rupee equivalent)

For a business processing 10,000 queries/day:
  Daily cost: ~$110 | Monthly: ~$3,300
```

---

### 2.2 Context Window — The LLM's Working Memory

> The **context window** is the total amount of text the LLM can "see" and process at one time — including your entire conversation history, any documents you uploaded, and the response it is generating.

**A simple analogy:**
Think of the context window as the LLM's short-term memory. Everything inside the window is crystal clear. Anything outside the window is completely invisible.

```
WHAT FITS INSIDE THE CONTEXT WINDOW:
  ┌──────────────────────────────────────────────────────────┐
  │  Your system instructions (if any)                       │
  │  + All previous messages in the conversation             │
  │  + Any documents you uploaded                            │
  │  + Your current prompt                                   │
  │  + The response being generated                          │
  │  ─────────────────────────────────────────────────────   │
  │  Total must stay within the model's context limit        │
  └──────────────────────────────────────────────────────────┘
```

**Context window comparison across major models:**

| Model | Context Window | Equivalent Pages | Best For |
|-------|---------------|-----------------|---------|
| **GPT-4o** | 128,000 tokens | ~320 pages | Most professional tasks |
| **Claude 3.5 Sonnet** | 200,000 tokens | ~500 pages | Long contracts, reports |
| **Gemini 1.5 Pro** | 1,000,000 tokens | ~2,500 pages | Very long documents |
| **Gemini 1.5 Flash** | 1,000,000 tokens | ~2,500 pages | Fast, large-volume tasks |
| **GPT-3.5 Turbo** | 16,385 tokens | ~41 pages | Simple, short tasks |
| **Llama 3.1 405B** | 128,000 tokens | ~320 pages | Open-source deployment |

**Practical implications of context window size:**

```
Small context (16K tokens):
  ✓ Quick email drafts
  ✓ Short summaries
  ✓ Simple Q&A
  ✗ Cannot process a full business plan at once
  ✗ Long conversations may "forget" early context

Large context (200K tokens):
  ✓ Upload and analyze a 300-page annual report
  ✓ Process an entire legal contract
  ✓ Long multi-turn project conversations
  ✓ Analyze multiple documents simultaneously
```

**What happens when you exceed the context window:**

When a conversation gets very long, older messages "fall out" of the context window. The AI literally cannot "remember" what was said earlier. This explains why AI seems to "forget" things in very long conversations — it is not forgetting; it is losing earlier messages from its working memory.

---

### 2.3 Temperature — Controlling Creativity vs. Precision

> **Temperature** is a numerical setting that controls how random or creative the LLM's token selections are. It ranges from 0.0 to 2.0.

**How temperature works mechanically:**

At each token generation step, the LLM calculates probabilities for all possible next tokens. Temperature adjusts whether the AI always picks the highest-probability token (low temperature) or sometimes picks lower-probability, more surprising tokens (high temperature).

```
EXAMPLE: Completing "The best way to solve this problem is to..."

Temperature 0.0 (Deterministic):
  Probabilities: "analyze" (45%), "break" (22%), "identify" (18%)
  → Always picks "analyze" (highest probability)
  → Same answer every single time

Temperature 0.7 (Balanced):
  Sometimes picks "analyze" (most likely)
  Sometimes picks "break" (second most likely)
  Sometimes picks "identify" (third most likely)
  → Varied but still professional answers

Temperature 1.5 (Creative):
  Might pick "reimagine" (5% probability)
  Might pick "destroy" (2% probability)
  → Surprising, creative, sometimes unexpected answers
```

**Temperature decision guide:**

```
┌────────────────┬────────────────┬──────────────────────────────────┐
│  Temperature   │  Behavior      │  Best For                         │
├────────────────┼────────────────┼──────────────────────────────────┤
│  0.0           │  Deterministic │  Data extraction, factual Q&A,   │
│                │  Consistent    │  JSON output, code that must work │
├────────────────┼────────────────┼──────────────────────────────────┤
│  0.3           │  Reliable      │  Business writing, reports,       │
│                │  Professional  │  analysis, summaries              │
├────────────────┼────────────────┼──────────────────────────────────┤
│  0.7 (default) │  Balanced      │  Most general tasks, emails,      │
│                │                │  explanations, drafts             │
├────────────────┼────────────────┼──────────────────────────────────┤
│  1.0–1.2       │  Creative      │  Brainstorming, ideation,         │
│                │  Varied        │  taglines, story concepts         │
├────────────────┼────────────────┼──────────────────────────────────┤
│  1.5–2.0       │  Highly varied │  Experimental creative writing,   │
│                │  Unpredictable │  poetry, avant-garde concepts     │
└────────────────┴────────────────┴──────────────────────────────────┘
```

> 💡 **Practical Tip:** In ChatGPT's free interface, you cannot set temperature directly — the model uses a default (~0.7). In API access (for developers) and some advanced tools, you can set it precisely. Understanding temperature helps you write better prompts that achieve the same effect — e.g., adding "Be creative and surprising" effectively increases temperature; "Be precise and consistent" effectively decreases it.

---

## 3. Major LLMs Compared

### 3.1 The Landscape of Leading LLMs (2024)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                    MAJOR LLMs COMPARISON                                 │
├────────────────┬────────────┬────────────────┬─────────────┬────────────┤
│  Model         │  Creator   │  Context       │  Free Tier  │  Best For  │
├────────────────┼────────────┼────────────────┼─────────────┼────────────┤
│  GPT-4o        │  OpenAI    │  128K tokens   │  Yes(limited│  General   │
│                │            │                │  )          │  tasks,    │
│                │            │                │             │  coding,   │
│                │            │                │             │  analysis  │
├────────────────┼────────────┼────────────────┼─────────────┼────────────┤
│  Claude 3.5    │  Anthropic │  200K tokens   │  Yes        │  Long docs,│
│  Sonnet        │            │                │  (claude.ai)│  nuanced   │
│                │            │                │             │  writing   │
├────────────────┼────────────┼────────────────┼─────────────┼────────────┤
│  Gemini 1.5    │  Google    │  1M tokens     │  Yes        │  Google    │
│  Pro           │            │                │             │  Workspace,│
│                │            │                │             │  multimodal│
├────────────────┼────────────┼────────────────┼─────────────┼────────────┤
│  Microsoft     │  Microsoft │  128K tokens   │  Yes        │  Microsoft │
│  Copilot       │  (OpenAI)  │  + web access  │             │  365,      │
│                │            │                │             │  live web  │
├────────────────┼────────────┼────────────────┼─────────────┼────────────┤
│  Llama 3.1     │  Meta      │  128K tokens   │  Free       │  Private   │
│  405B          │            │                │  (open src) │  deployment│
├────────────────┼────────────┼────────────────┼─────────────┼────────────┤
│  Perplexity    │  Perplexity│  N/A (search)  │  Yes        │  Research  │
│  AI            │            │  + live web    │             │  with      │
│                │            │                │             │  citations │
└────────────────┴────────────┴────────────────┴─────────────┴────────────┘
```

---

### 3.2 Which LLM to Choose for Which Task

This is a practical decision framework you will use throughout your career:

```
TASK                                    RECOMMENDED LLM(S)
─────────────────────────────────────── ────────────────────────────────────
General writing (emails, reports)     → ChatGPT (GPT-4o) or Copilot
Drafting in Word/Outlook/Teams        → Microsoft Copilot
Analyzing a Google Doc or Gmail       → Google Gemini
Summarizing a 200-page contract       → Claude 3.5 (longest context)
Research with source citations        → Perplexity AI
Coding and debugging                  → ChatGPT or GitHub Copilot
Current news or real-time data        → Copilot or Perplexity (live web)
Private/confidential company data     → Llama 3 (runs locally, no cloud)
Multimodal (image + text analysis)    → GPT-4o or Gemini 1.5 Pro
Analyzing a YouTube video             → Gemini (paste YouTube URL)
Long academic paper analysis          → Claude 3.5 (200K context)
Creating a presentation from notes    → Gamma.app (uses GPT-4)
```

**Decision framework — three questions:**

```
Question 1: Does this task involve live/current information?
  YES → Use Copilot or Perplexity (web access)
  NO  → Continue to Question 2

Question 2: How long is the document I'm processing?
  <50 pages  → Any major LLM works
  50-300 pages → GPT-4o or Claude 3.5
  300+ pages   → Claude 3.5 (200K) or Gemini 1.5 Pro (1M)

Question 3: Where does this data live / what tools do I use?
  Google Workspace → Gemini
  Microsoft 365   → Copilot
  Standalone use  → ChatGPT (GPT-4o)
  Must be private → Llama 3 (local deployment)
```

---

## 4. Real-World Example: LLM Selection in a Law Firm

**Scenario:** A corporate law firm has four different tasks today. Which LLM should each lawyer use?

| Lawyer | Task | Optimal LLM | Reason |
|--------|------|-------------|--------|
| Priya | Summarize a 400-page merger agreement | Claude 3.5 | 200K context fits the entire document |
| Rahul | Draft a reply email in Outlook | Microsoft Copilot | Integrates directly into Outlook |
| Ananya | Research current court rulings on IP law | Perplexity AI | Live web with citations |
| Vikram | Analyze proprietary client strategy documents | Llama 3 (local) | Data never leaves the firm's servers |

**The mistake to avoid:** Using a single LLM for all tasks. Just as you would use different tools for different tasks (Excel for data, Word for documents, Outlook for email), you should select the right LLM for each specific need.

---

## 5. Industry Case Study: LLMs in Legal Services — Allen & Overy

**Company:** Allen & Overy — one of the world's largest law firms, operating in 40+ countries

**The Problem:**  
Lawyers at Allen & Overy were spending 60–80% of their time on:
- Reading and extracting key clauses from lengthy contracts (500–1,000 pages)
- Researching relevant case law across multiple jurisdictions
- Generating first drafts of standard legal documents (NDAs, employment contracts, terms of service)
- Translating legal documents for international matters

This work was expensive (senior partner time), slow, and limited capacity for higher-value strategic work.

**The AI Solution — Harvey (built on GPT-4):**

```
WHAT HARVEY DOES:
─────────────────
Contract Review:
  ✓ Reads an entire 800-page contract in seconds
  ✓ Extracts key clauses (termination, liability, payment, IP)
  ✓ Flags unusual or high-risk clauses with explanations
  ✓ Compares against standard firm templates

Legal Research:
  ✓ Searches case law databases
  ✓ Summarizes relevant precedents
  ✓ Identifies jurisdictional differences

Document Generation:
  ✓ Generates first drafts of standard documents
  ✓ Customizes based on matter-specific instructions
  ✓ All output reviewed and signed by qualified lawyers
```

**Results:**
- Contract review time reduced by **80%** (from 6 hours to ~70 minutes)
- Lawyers now handle **3x more client matters** with the same team size
- Document drafting time reduced from **3 days to 3 hours** for standard agreements
- Zero job losses — lawyers redirected to higher-value strategic and advisory work
- Allen & Overy rolled out Harvey to **3,500+ lawyers** globally

**The governance model (critical lesson):**
```
AI produces draft → Junior associate reviews → Senior partner approves → Client receives
```
AI is **never** the final signatory. A qualified lawyer reviews every AI output before it reaches the client. This is the model for responsible AI in high-stakes professional contexts.

---

## 6. Hands-On Lab 3: LLM Comparison Test

**Objective:** Experience firsthand how different LLMs respond to the same professional prompt  
**Duration:** 25 minutes  
**Tools:** chat.openai.com | claude.ai | gemini.google.com | copilot.microsoft.com

---

### The Test Prompt

Give this **exact same prompt** to all four platforms (or minimum three):

```
You are a Business Analyst at a mid-sized retail company.

The CEO has asked you to analyze why sales dropped 18% in Q3 compared
to Q2 of the same year.

Provide:
1. The top 5 most likely reasons for the sales decline (specific to retail)
2. For each reason: one specific data source or metric that would confirm it
3. A prioritized action plan with 3 immediate steps (within 30 days)

Format your response as:
- A brief executive summary (2 sentences)
- A numbered list of 5 reasons with their data sources
- A numbered action plan

Keep total response under 400 words. Use professional business language.
```

---

### Comparison Evaluation Matrix

After running the prompt on each platform, complete this matrix:

| Evaluation Criterion | ChatGPT | Claude | Gemini | Copilot |
|---------------------|---------|--------|--------|---------|
| **Followed the format exactly?** (exec summary + 5 reasons + action plan) | Y/N | Y/N | Y/N | Y/N |
| **Specificity** — were reasons specific to retail (not generic)? | /5 | /5 | /5 | /5 |
| **Data sources** — did each reason include a concrete data source? | /5 | /5 | /5 | /5 |
| **Action plan quality** — are actions specific and actionable in 30 days? | /5 | /5 | /5 | /5 |
| **Word count** — stayed under 400 words? | Y/N | Y/N | Y/N | Y/N |
| **Business language quality** | /5 | /5 | /5 | /5 |
| **Overall preference** | /5 | /5 | /5 | /5 |
| **TOTAL** | /30 | /30 | /30 | /30 |

---

### Post-Lab Discussion Questions

Answer these individually (written) or discuss in pairs:

1. Which LLM followed the format instructions most precisely?
2. Which LLM gave the most **specific** retail-relevant reasons (not generic business advice)?
3. Were the outputs meaningfully different, or similar in substance with different wording?
4. Based on this test, which LLM would you recommend for a business analyst preparing executive briefings? Why?
5. Did any LLM add information beyond what was asked (positively or negatively)?

---

### Lab Evaluation Rubric

| Deliverable | Marks |
|-------------|-------|
| Screenshots from minimum 3 platforms | 3 |
| Comparison matrix completed for all criteria | 4 |
| Post-lab discussion answers (4/5 minimum) | 3 |
| **Total** | **10** |

---

## 7. Mini Exercise: Token and Context Window Calculations

Solve these practical problems:

**Problem 1:**
You need to analyze a 250-page business report. Assuming 300 words per page, approximately how many tokens is the document? Which LLMs can process it in a single context window?

```
Calculation:
  250 pages × 300 words/page = 75,000 words
  75,000 words ÷ 0.75 words/token = 100,000 tokens

  Can handle it:
  ✓ GPT-4o (128K limit) — just fits
  ✓ Claude 3.5 (200K limit) — comfortably fits
  ✓ Gemini 1.5 Pro (1M limit) — easily fits
  ✗ GPT-3.5 (16K limit) — cannot; must be summarized in chunks
```

**Problem 2:**
You are building a customer service chatbot that processes ~200 customer messages per hour, each message averages 50 tokens (input) and the AI response averages 150 tokens (output). Using GPT-4o at $0.005/1K input tokens and $0.015/1K output tokens, what is the estimated daily cost?

```
Per message cost:
  Input:  50 tokens  × $0.005/1K = $0.00025
  Output: 150 tokens × $0.015/1K = $0.00225
  Per message total: $0.0025

Daily messages: 200/hour × 24 hours = 4,800 messages
Daily cost: 4,800 × $0.0025 = $12.00/day
Monthly cost: $12 × 30 = $360/month
```

---

## 8. Interview Questions — Session 3

**Q1:** *"What is a Large Language Model? How is it different from a regular search engine?"*

**Strong Answer:**
"A Large Language Model is an AI system trained on massive text datasets to understand and generate human language. Unlike a search engine, which retrieves existing web pages that match your query, an LLM generates new, original text based on patterns learned during training. A search engine answers 'what documents contain this information?' An LLM answers 'what response would be most appropriate given this context?' The output of an LLM is always freshly generated — not retrieved from a database."

**Q2:** *"What is a context window and how would you work within its limits on a real project?"*

**Strong Answer:**
"The context window is the maximum amount of text an LLM can process in one interaction — including the conversation history and any uploaded documents. For example, GPT-4o has a 128,000 token context, which is roughly 320 pages of text. When working with documents longer than this, I would either choose a model with a larger context (Claude 3.5 at 200K or Gemini at 1M tokens), or use a chunking strategy — breaking the document into sections, processing each separately, and synthesizing the results. For ongoing projects, I would also periodically summarize the conversation to preserve key context without hitting the limit."

**Q3:** *"When would you choose Claude over ChatGPT, and vice versa?"*

**Strong Answer:**
"I would choose Claude 3.5 for tasks requiring very long context — like analyzing a full annual report or a lengthy legal contract — because its 200K token window is larger than GPT-4o's 128K. Claude also tends to produce nuanced, well-structured long-form writing. I would choose GPT-4o for general versatility, coding tasks, image generation (via DALL-E), and broad everyday use. For current information or web-cited research, I would use Perplexity AI or Microsoft Copilot. The right choice depends on the specific task requirements."

---

## 9. Revision Questions — Session 3

1. What do the two dimensions of "large" in Large Language Model refer to?
2. Walk through the step-by-step process of how an LLM generates a response token by token.
3. How many tokens is approximately equivalent to 1,000 words of text?
4. Define context window. What happens to a conversation when you exceed the context window?
5. What is temperature in LLMs? Give a specific example of when you would use temperature 0.0 versus temperature 1.0.
6. Compare GPT-4o and Claude 3.5 on context window size. Which would you use to analyze a 400-page contract and why?
7. Why does Microsoft Copilot have an advantage over standard ChatGPT for researching current events?
8. What does it mean for an LLM to be "open source" (like Llama 3)? What is the primary business advantage?

---

## 10. Key Terminology — Session 3

| Term | Definition |
|------|-----------|
| **Large Language Model (LLM)** | AI system trained on massive text to understand and generate language |
| **Token** | The basic unit of text an LLM processes (~0.75 words per token) |
| **Context Window** | Maximum tokens an LLM can process in one interaction (conversation + documents + response) |
| **Temperature** | Setting controlling randomness of LLM output (0.0=deterministic, 2.0=highly creative) |
| **Parameters** | Mathematical weights in a neural network learned during training |
| **Inference** | Running a trained model to generate a new response (vs. training) |
| **Tokenization** | The process of converting text into tokens for LLM processing |
| **Knowledge Cutoff** | The date after which an LLM has no training data (no awareness of later events) |
| **Multimodal** | An LLM that can process multiple input types (text + images + audio + video) |
| **Open Source LLM** | An LLM whose weights are publicly released (e.g., Llama 3) and can be run locally |

---

## 11. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 3 SUMMARY — WHAT TO REMEMBER                                        │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  LLM = AI trained on massive text to generate language token-by-token    │
│  ✓  "Large" = large training data + large number of parameters              │
│  ✓  Token ≈ 0.75 words; 1,000 tokens ≈ 750 words ≈ 1.5 pages               │
│  ✓  Context window = LLM's working memory; bigger = process longer docs     │
│  ✓  Temperature: 0.0 = precise/consistent; 1.0+ = creative/varied           │
│  ✓  Choose LLM based on: content length, integration needs, web access      │
│  ✓  Claude 3.5 = longest context (200K); Gemini = 1M tokens                │
│  ✓  Copilot + Perplexity = live web access; ChatGPT = knowledge cutoff     │
│  ✓  Allen & Overy: 80% reduction in contract review time using LLMs         │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 4 — AI Tools Landscape: ChatGPT, Copilot, Gemini & More            │
│  (Hands-on platform exploration, the PACE evaluation framework,              │
│   and building your personalized AI toolkit)                                 │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 3 Complete | Next: Session 4 — AI Tools Landscape: ChatGPT, Copilot, Gemini & More*  
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
