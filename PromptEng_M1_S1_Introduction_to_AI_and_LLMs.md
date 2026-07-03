# Session 1: Introduction to Artificial Intelligence & Large Language Models
## Module 1 — Foundations of Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 1 OF 30  │  Module 1, Session 1                           │
│  Topic: Introduction to AI & Large Language Models                  │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Define Artificial Intelligence and explain how it differs from traditional programming
2. Describe the AI hierarchy: AI → Machine Learning → Deep Learning → LLMs
3. Explain what Large Language Models are and how they generate text
4. Identify what LLMs can and cannot do — and why
5. Name the major LLMs in use today and their key characteristics
6. Run your first AI prompt and critically observe the output

---

## 1.1 What is Artificial Intelligence?

### The Traditional Definition

**Artificial Intelligence (AI)** is the simulation of human intelligence processes by computer systems. These processes include:
- **Learning** — acquiring information and rules for using it
- **Reasoning** — using those rules to reach approximate or definite conclusions
- **Self-correction** — improving performance based on feedback

### Traditional Programming vs. AI

To understand AI, it helps to contrast it with how traditional software works:

| Aspect | Traditional Programming | Artificial Intelligence |
|--------|------------------------|------------------------|
| **Approach** | Programmer writes explicit rules | System learns rules from data |
| **Input** | Data + Rules → Output | Data + Output → Rules (training) |
| **Adaptability** | Fixed — can only do what programmer coded | Adaptive — improves with more data |
| **Example** | `if temperature > 100: send_alert()` | System learns when anomalies occur from historical data |
| **Handling new cases** | Fails or needs reprogramming | Can generalize to unseen situations |

**Analogy:** Teaching a child to recognize a cat.
- **Traditional programming:** You write: `if has_pointy_ears AND has_whiskers AND has_fur: it's_a_cat`
- **AI/ML:** You show the child 10,000 photos of cats and non-cats. They learn the pattern themselves.

---

### 1.2 The AI Hierarchy

AI is not one single technology. It is a family of related fields, each building on the previous:

```
┌─────────────────────────────────────────────────────────────────┐
│                    ARTIFICIAL INTELLIGENCE                       │
│  (Any technique that enables machines to mimic human behavior)  │
│                                                                  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                   MACHINE LEARNING                        │  │
│  │  (Systems that learn from data without explicit rules)    │  │
│  │                                                           │  │
│  │  ┌─────────────────────────────────────────────────────┐  │  │
│  │  │                 DEEP LEARNING                       │  │  │
│  │  │  (Neural networks with many layers — learns         │  │  │
│  │  │   complex patterns from large datasets)             │  │  │
│  │  │                                                     │  │  │
│  │  │  ┌───────────────────────────────────────────────┐  │  │  │
│  │  │  │         LARGE LANGUAGE MODELS (LLMs)          │  │  │  │
│  │  │  │  (Deep learning models trained specifically   │  │  │  │
│  │  │  │   on text to understand and generate language)│  │  │  │
│  │  │  └───────────────────────────────────────────────┘  │  │  │
│  │  └─────────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

**Layer 1 — Artificial Intelligence (broadest)**
- Includes rule-based systems, expert systems, search algorithms
- Any approach that makes machines appear intelligent

**Layer 2 — Machine Learning**
- Systems that improve automatically through experience
- Learn patterns from data, not from hand-coded rules
- Examples: spam filters, recommendation engines, fraud detection

**Layer 3 — Deep Learning**
- Subset of ML using artificial neural networks with many layers
- Requires large amounts of data and computing power
- Powers: image recognition, speech recognition, translation

**Layer 4 — Large Language Models (most specific)**
- Deep learning models specifically trained on text data
- Trained to predict, understand, and generate human language
- Examples: GPT-4, Claude, Gemini, Llama — what we use daily

---

### 1.3 A Brief History of AI

Understanding how we got here helps appreciate why LLMs work the way they do:

| Year | Milestone | Significance |
|------|-----------|-------------|
| **1950** | Alan Turing proposes the Turing Test | First formal definition of machine intelligence |
| **1956** | "Artificial Intelligence" coined at Dartmouth | Birth of AI as a field |
| **1966** | ELIZA — first chatbot at MIT | Early natural language processing |
| **1980s** | Expert Systems emerge | Rule-based AI for specific domains |
| **1997** | Deep Blue beats Kasparov at chess | AI surpasses humans in narrow domain |
| **2011** | IBM Watson wins Jeopardy | NLP milestone — AI understands natural language questions |
| **2012** | AlexNet wins ImageNet — Deep Learning revolution | Deep neural networks prove superior |
| **2017** | "Attention Is All You Need" paper published | Transformer architecture — the foundation of all modern LLMs |
| **2018** | BERT released by Google | Bidirectional language understanding |
| **2020** | GPT-3 released (175 billion parameters) | LLMs reach human-like text generation |
| **Nov 2022** | ChatGPT launches | AI becomes mainstream — 100M users in 2 months |
| **2023** | GPT-4, Claude, Gemini, Llama released | LLM race begins, rapid capability improvements |
| **2024** | GPT-4o, Claude 3.5, Gemini 1.5 | Multimodal AI, million-token contexts |

---

### 1.4 What are Large Language Models?

An **LLM (Large Language Model)** is a type of deep learning model trained on massive amounts of text data to understand, generate, translate, and reason about human language.

**The word "Large" has three meanings:**
1. **Large training data** — trained on hundreds of billions of words (the internet, books, code, Wikipedia)
2. **Large number of parameters** — billions to hundreds of billions of weights (internal values the model learned)
3. **Large compute** — requires thousands of specialized GPUs and months of training

### How an LLM Generates Text — Step by Step

When you send a message to ChatGPT, here is what actually happens:

```
YOUR MESSAGE
"Explain gravity to a child"
        │
        ▼
┌─────────────────────┐
│   TOKENIZATION      │  Your text is broken into tokens
│                     │  "Explain" "gravity" "to" "a" "child"
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│   EMBEDDING         │  Each token becomes a vector (list of numbers)
│                     │  "gravity" → [0.23, -0.87, 0.44, ...]
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│   TRANSFORMER       │  Attention mechanism weighs relationships
│   ATTENTION         │  "gravity" is strongly related to "explain"
│                     │  and "child" → changes how it responds
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│   NEXT TOKEN        │  Model predicts: "Gravity" is most likely
│   PREDICTION        │  next token (probability: 0.73)
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│   REPEAT            │  Predicts next token, then next, then next
│                     │  Until sentence / response is complete
└────────┬────────────┘
         │
         ▼
"Gravity is like an invisible force..."
```

**The key insight:** An LLM does NOT "think" or "know" things. It predicts the most statistically likely next word given everything it has seen. This is both its power (fluent, coherent text) and its limitation (it can confidently predict wrong answers).

---

### 1.5 The Transformer Architecture (Conceptual)

The 2017 paper *"Attention Is All You Need"* by Google researchers introduced the **Transformer** — the architecture that powers every major LLM today.

**The key innovation: Self-Attention**

Before Transformers, models read text word by word (left to right). The Transformer looks at ALL words simultaneously and weighs how much each word should "attend to" every other word.

**Example — Understanding pronouns:**

*"The trophy didn't fit in the suitcase because it was too large."*

What does "it" refer to? The trophy or the suitcase?

- Old models struggled with this
- The Transformer's attention mechanism lets "it" attend to "trophy" more strongly than "suitcase" based on the word "large" — getting the right answer

```python
# Conceptual illustration of attention (NOT actual code — simplified)
# For the word "it" in the sentence above:

attention_weights = {
    "The":       0.01,
    "trophy":    0.62,   # high attention — "it" refers to trophy
    "didn't":    0.02,
    "fit":       0.05,
    "suitcase":  0.12,
    "because":   0.03,
    "was":       0.04,
    "too":       0.04,
    "large":     0.07
}
# The model correctly resolves "it" → "trophy"
```

---

### 1.6 Major LLMs — Who Makes What

| Model | Organization | Key Strength | Context Window | Free Tier |
|-------|-------------|-------------|---------------|-----------|
| **GPT-4o** | OpenAI | General purpose, multimodal, coding | 128K tokens | Yes (limited) |
| **Claude 3.5 Sonnet** | Anthropic | Long documents, nuanced writing, safety | 200K tokens | Yes (limited) |
| **Gemini 1.5 Pro** | Google DeepMind | Google Workspace integration, 1M context | 1M tokens | Yes |
| **Llama 3.1** | Meta | Open-source, locally deployable | 128K tokens | Free (open source) |
| **Mistral Large** | Mistral AI | European, efficient, multilingual | 128K tokens | Via API |
| **Command R+** | Cohere | Enterprise search and RAG | 128K tokens | Via API |
| **Copilot** | Microsoft (GPT-4 powered) | Microsoft 365 integration | 128K tokens | Yes (M365 users) |

**Which should you use?**

```
Task                              → Best Model
─────────────────────────────────────────────────────
General writing & productivity    → ChatGPT (GPT-4o)
Very long documents (books, PDFs) → Claude 3.5 Sonnet
Google Docs / Gmail integration   → Gemini
Microsoft Word / Outlook / Teams  → Copilot
Code generation & debugging       → GPT-4o or Claude
Research with citations           → Perplexity AI (uses LLMs + search)
Privacy / local deployment        → Llama 3 (self-hosted)
```

---

### 1.7 What LLMs CAN Do

LLMs are remarkably capable across a wide range of language tasks:

**Content Generation:**
- Write blog posts, emails, reports, essays, stories, scripts
- Generate marketing copy, product descriptions, social media posts
- Draft legal documents, contracts, policies (with expert review)

**Comprehension & Analysis:**
- Summarize long documents in seconds
- Extract key information from dense text
- Identify themes, arguments, and sentiment
- Compare and contrast multiple documents

**Question Answering & Explanation:**
- Explain complex concepts at any level
- Answer domain-specific questions (medical, legal, technical)
- Teach topics using analogies, examples, and exercises

**Reasoning & Problem Solving:**
- Break down complex problems step by step
- Evaluate options and recommend solutions
- Debug logical errors in arguments or code

**Code:**
- Write, explain, debug, and optimize code in any language
- Convert code from one language to another
- Explain what a piece of code does in plain English

**Transformation:**
- Translate between languages
- Change tone (formal ↔ casual)
- Reformat data (text → table → JSON)
- Rewrite for different audiences

---

### 1.8 What LLMs CANNOT Do (and Why)

Understanding limitations is as important as knowing capabilities — especially for professional use:

**1. Real-Time Information Access**
- LLMs have a knowledge cutoff date (training data ends at a fixed point)
- GPT-4o cutoff: April 2024; Claude 3.5: early 2024
- They do NOT know about events after their cutoff
- **Fix:** Use tools that add web search (Perplexity, Copilot with web, ChatGPT with browsing)

**2. Guaranteed Factual Accuracy (Hallucination)**
- LLMs predict likely text — they don't "look things up"
- They can state false information confidently
- Particularly risky for: specific statistics, quotes, citations, recent events
- **Fix:** Always verify facts from AI against primary sources

```
Example of hallucination risk:
Prompt: "Who won the Nobel Prize in Literature in 2023?"
Risk: AI may confidently name the wrong person or fabricate details
Fix: Verify at nobelprize.org
```

**3. Private or Internal Data Access**
- The AI only knows what's in its training data or what you paste in the prompt
- It cannot access your company's internal systems, databases, or files
- **Fix:** Paste relevant text into the prompt (within context limits)

**4. Reliable Complex Mathematics**
- LLMs are language models, not calculators
- They can make arithmetic errors, especially with large or complex calculations
- **Fix:** Use AI for problem setup and interpretation; use Python/calculator for the actual math

```python
# What you should do for complex calculations:
# Ask AI to write the code, then run it yourself

prompt = """
Write Python code to calculate compound interest:
- Principal: $10,000
- Annual rate: 7.5%
- Compounded monthly
- Duration: 25 years
"""
# Then run the generated code — don't trust AI's mental arithmetic
```

**5. Understanding Images (Unless Multimodal)**
- Basic LLMs process text only
- GPT-4o, Claude 3, Gemini are multimodal — they CAN process images
- Older or smaller models cannot "see"

**6. Long-Term Memory**
- By default, each conversation starts fresh
- The model forgets everything from previous conversations
- **Fix:** Paste key context at the start of a new conversation, or use memory features where available

---

### 1.9 The Concept of Hallucination — In Depth

Hallucination is the most important LLM limitation to understand for professional use.

**What hallucination actually is:**

The model generates text by predicting the most probable next token. When asked about something it doesn't have reliable training data for, it still predicts a plausible-sounding continuation — because that's all it can do. It has no mechanism to say "I don't have data on this" and stop.

**Types of hallucination:**

| Type | Example | Risk Level |
|------|---------|-----------|
| **Factual errors** | Wrong dates, statistics, names | High |
| **Fabricated citations** | Made-up paper titles and authors that don't exist | Very High |
| **Confident speculation** | Presenting guesses as facts | High |
| **Outdated information** | Stating something as current that has changed | Medium |
| **False attribution** | Attributing quotes to wrong people | High |

**Real-world case study:**

In 2023, a US lawyer submitted a legal brief that cited 6 court cases — all fabricated by ChatGPT. The cases did not exist. The lawyer faced sanctions and the case became a landmark warning about AI hallucination in professional contexts.

**The Professional Rule:** Treat every AI factual claim as a hypothesis to be verified, not a fact to be trusted.

---

### 1.10 Key AI Concepts — Complete Glossary for Session 1

| Term | Definition | Example |
|------|-----------|---------|
| **Parameter** | A learned numerical weight inside a neural network. GPT-4 has ~1 trillion parameters | The settings a model adjusts during training |
| **Training** | Teaching the model by exposing it to data and adjusting parameters based on errors | Training GPT on billions of web pages |
| **Inference** | Using a trained model to generate responses | ChatGPT answering your question |
| **Hallucination** | AI generating false information confidently | Citing a book that doesn't exist |
| **Fine-tuning** | Further training a pre-trained model on specific data | Training GPT on medical textbooks for healthcare use |
| **Prompt** | The input text you give to an AI model | "Write a cover letter for a marketing role" |
| **Completion** | The output the model generates | The actual cover letter it writes |
| **Embedding** | A numerical vector representing the meaning of text | "king" → [0.4, -0.2, 0.7, ...] |
| **Token** | The smallest unit of text the model processes | "unbelievable" = 3 tokens |
| **Context window** | Max tokens the model can process at once | GPT-4o: 128K tokens |
| **Temperature** | Parameter controlling randomness of output | Low = predictable, High = creative |
| **Multimodal** | Able to process multiple types of input (text + images + audio) | GPT-4o can analyze images |

---

## Hands-On Activities — Session 1

---

### Activity 1.1 — Your First Prompt: The Audience Test

**Objective:** Understand how LLMs adapt to different audiences based on prompt instructions

**Steps:**
1. Open ChatGPT (chat.openai.com) or any LLM tool
2. In a new conversation, type **Prompt A** exactly:

```
What is Artificial Intelligence? Explain it to me like I am a 10-year-old.
```

3. Copy the response to a document
4. Start a **new conversation** (very important — fresh context)
5. Type **Prompt B** exactly:

```
What is Artificial Intelligence? Explain it to a postgraduate researcher
in computer science who is familiar with machine learning but new to LLMs.
```

6. Copy that response alongside Prompt A's response

**Analysis Questions:**
- How did vocabulary change between the two responses?
- Did the structure change (analogies vs. technical terms)?
- Which response was longer? Why do you think that is?
- What does this tell you about how the AI interprets your prompt?

**Key Insight:** The AI uses audience specification to select from its training data the appropriate register, vocabulary, and depth. This is why specifying your audience in prompts is one of the most powerful techniques you will learn.

---

### Activity 1.2 — Exploring LLM Limitations

**Objective:** Experience AI limitations firsthand to build healthy skepticism

**Part A — The Knowledge Cutoff Test**
```
What major AI announcements happened last week?
```
Observe: Does the AI answer confidently? Does it acknowledge uncertainty? Does it hallucinate events?

**Part B — The Arithmetic Test**

First, run this:
```
What is 2,847 × 9,341?
```
Then verify with a calculator. (Correct answer: 26,594,727)

Now run this more complex one:
```
If I invest $15,000 at 8.5% annual interest compounded monthly for 12 years,
what is the final value?
```
Verify with an online compound interest calculator.

**Part C — The Citation Test**
```
Give me 3 real, published academic papers about prompt engineering for
large language models, with full citations including author names, journal,
year, and DOI.
```
**Verification:** Take each citation and search Google Scholar. How many actually exist?

**Document your findings** in this table:

| Limitation Tested | Did AI handle it well? | What did it do wrong? | How would you verify? |
|------------------|----------------------|----------------------|----------------------|
| Knowledge cutoff | | | |
| Complex math | | | |
| Citation accuracy | | | |

---

### Activity 1.3 — Model Comparison

**Objective:** Experience how different LLMs respond to the same prompt

If you have access to multiple tools (ChatGPT + Gemini, or ChatGPT + Copilot), run this identical prompt in each:

```
You are a business consultant. A retail company is considering launching
an e-commerce platform. Give me the 5 most critical factors they should
evaluate before proceeding. Be specific and practical.
```

**Compare:**
- Which response was more structured?
- Which gave more practical, specific advice?
- Which was longer? Was longer better in this case?
- Did any model refuse or hedge excessively?

---

### Activity 1.4 — The Hallucination Trap

**Objective:** Experience hallucination firsthand in a controlled way

Run this prompt:
```
Tell me about the research paper "Leveraging Prompt Engineering for
Enterprise Knowledge Management" published in the Journal of AI
Applications in 2023. Who wrote it? What were the main findings?
```

*(This paper does not exist — it was made up for this exercise)*

**Observe:**
- Does the AI confess it cannot find this paper?
- Does it fabricate authors and findings?
- How confident does it sound?

This is the hallucination risk in action. It demonstrates why you should never use AI-generated citations in professional or academic work without independent verification.

---

## Deeper Dive — For Those Who Want More

### How the Transformer's Attention Works (Technical Detail)

For learners with a programming background, here is a simplified Python illustration of the attention concept:

```python
import numpy as np

# Simplified illustration of self-attention
# In reality, this involves learned weight matrices (Q, K, V)

def simple_attention(query, keys, values):
    """
    query: the current word we want to understand
    keys: all words in the sentence
    values: the information content of all words
    """
    # Compute similarity between query and all keys
    scores = np.dot(query, keys.T)
    
    # Convert scores to probabilities (softmax)
    attention_weights = np.exp(scores) / np.sum(np.exp(scores))
    
    # Weighted sum of values
    output = np.dot(attention_weights, values)
    
    return output, attention_weights

# Example: Sentence "The cat sat on the mat"
# Each word represented as a simple 3D vector (in reality: 1536+ dimensions)
words = ["The", "cat", "sat", "on", "the", "mat"]
vectors = np.random.randn(6, 3)  # simplified random vectors

# For the word "sat" (index 2), compute attention to all other words
query = vectors[2]  # "sat"
attention_output, weights = simple_attention(query, vectors, vectors)

print("Attention weights for 'sat':")
for word, weight in zip(words, weights):
    print(f"  {word}: {weight:.3f}")
```

**What this illustrates:**
- Every word attends to every other word
- Higher weight = more influence on meaning
- In a real transformer: "sat" would attend most to "cat" (the subject doing the sitting)

---

## Revision Questions — Session 1

1. In your own words, what is the difference between Machine Learning and a rule-based expert system?
2. What does the word "Large" in Large Language Model actually refer to?
3. Explain in one paragraph how an LLM generates a response to your question.
4. Name three things an LLM can do well and three things it cannot do reliably.
5. What is hallucination in the context of AI, and what is the professional risk it poses?
6. Why was the 2017 Transformer paper so important to the development of modern LLMs?
7. A colleague says "ChatGPT knows everything." How would you accurately correct this statement?
8. Which LLM would you choose for (a) processing a 300-page PDF and (b) generating emails in Microsoft Outlook? Why?

---

## Key Takeaways — Session 1

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 1 KEY TAKEAWAYS                                             │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ AI is an umbrella: AI → ML → Deep Learning → LLMs               │
│                                                                      │
│  ✓ LLMs predict the next token — they do NOT "know" or "think"     │
│                                                                      │
│  ✓ The Transformer (2017) is the architecture behind all modern LLMs│
│                                                                      │
│  ✓ LLMs excel at: text generation, summarization, reasoning,        │
│    translation, code, explanation                                    │
│                                                                      │
│  ✓ LLMs fail at: real-time info, guaranteed accuracy, private data, │
│    reliable complex math, permanent memory                           │
│                                                                      │
│  ✓ Hallucination = AI confidently generating false information      │
│    ALWAYS verify facts, statistics, and citations independently     │
│                                                                      │
│  ✓ Your prompt quality = your output quality                        │
│    This is the entire premise of prompt engineering                 │
└──────────────────────────────────────────────────────────────────────┘
```

---

## Further Reading

| Resource | What to Read | Why |
|----------|-------------|-----|
| "Attention Is All You Need" (Vaswani et al., 2017) | Abstract + Introduction | The paper that started everything |
| OpenAI Usage Policies | Full document | Understanding AI provider rules |
| Anthropic's Model Card for Claude | Key sections | How leading AI companies document capabilities/limits |
| learnprompting.org | Chapter 1 | Free resource aligned with this course |
| "Stochastic Parrots" (Bender et al., 2021) | Full paper | Academic critique of LLM limitations |

---

*Session 1 Complete → Proceed to Session 2: Tokens & Context Windows*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
