# Session 2: Tokens & Context Windows
## Module 1 — Foundations of Prompt Engineering
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 2 OF 30  │  Module 1, Session 2                           │
│  Topic: Tokens, Context Windows & Generation Parameters             │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Explain what tokens are and how LLMs use them to process text
2. Calculate approximate token counts for any piece of text
3. Describe the context window and why it acts as the model's "working memory"
4. Explain what happens when a context window is exceeded
5. Understand generation parameters: Temperature, Top-P, Max Tokens, Frequency Penalty
6. Make practical decisions about context management in long AI conversations

---

## 2.1 What is a Token?

A **token** is the fundamental unit of text that an LLM processes. The model never sees raw characters or complete words — it sees tokens, which are chunks of text determined by a process called **tokenization**.

Tokenization splits text into pieces that balance:
- Computational efficiency (not too many tiny pieces)
- Semantic meaning (not losing word structure)
- Coverage of rare words (can build uncommon words from common sub-parts)

### How Tokenization Works — Examples

```
Word              Tokens          Count
──────────────────────────────────────────
"cat"           → ["cat"]              1
"cats"          → ["cats"]             1
"running"       → ["running"]          1
"unbelievable"  → ["un","believ","able"] 3
"ChatGPT"       → ["Chat","G","PT"]    3
"2024"          → ["2024"]             1
","             → [","]                1
" Hello"        → [" Hello"]           1  (space is part of the token)
```

**Key Rules of Thumb:**

| Approximation | Value |
|--------------|-------|
| 1 token | ≈ 4 characters of English |
| 1 token | ≈ 0.75 words |
| 100 tokens | ≈ 75 words |
| 1,000 tokens | ≈ 750 words |
| 1 page of text | ≈ 500–700 tokens |
| 1 average email | ≈ 100–200 tokens |
| 1 short blog post (500 words) | ≈ 650–700 tokens |
| This entire session document | ≈ 2,500–3,000 tokens |

### Why Different Words Have Different Token Counts

```python
# Token count examples (using tiktoken — OpenAI's tokenization library)
# pip install tiktoken

import tiktoken

encoder = tiktoken.encoding_for_model("gpt-4o")

examples = [
    "Hello",                  # common English word → 1 token
    "Serendipity",            # longer word → 2 tokens
    "Electroencephalography", # technical term → 5+ tokens
    "नमस्ते",                 # Hindi — non-Latin script → more tokens
    "🎉",                     # emoji → 1-3 tokens
    "2024-01-15",             # date → 4 tokens
    "https://openai.com",     # URL → multiple tokens
]

for text in examples:
    tokens = encoder.encode(text)
    print(f"'{text}' → {len(tokens)} token(s): {tokens}")
```

**Critical Insight:** Non-English languages generally use MORE tokens per word than English because the tokenizer was trained primarily on English text. This means the same sentence in Hindi or Arabic costs more tokens than in English — a practical cost consideration when using AI at scale.

---

## 2.2 Why Tokens Matter for Prompt Engineers

### 1. Cost (API Usage)

When calling AI APIs programmatically, you pay per token:

| Model | Input Price | Output Price |
|-------|------------|-------------|
| GPT-4o | $5 / 1M tokens | $15 / 1M tokens |
| GPT-4o mini | $0.15 / 1M tokens | $0.60 / 1M tokens |
| Claude 3.5 Sonnet | $3 / 1M tokens | $15 / 1M tokens |
| Gemini 1.5 Pro | $3.50 / 1M tokens | $10.50 / 1M tokens |

**Practical example:**
- 1,000 API calls per day, each with 500 input + 200 output tokens
- GPT-4o cost: (700,000 input × $5/1M) + (200,000 output × $15/1M)
- = $3.50 + $3.00 = **$6.50/day → ~$197/month**

For a business processing thousands of documents, token efficiency becomes a significant cost factor.

### 2. Context Limits

Every model has a maximum token limit. If your conversation + prompt + response would exceed this, the model either:
- **Truncates** early content (forgets it)
- **Refuses** to process (returns an error)

### 3. Response Length

When you leave no guidance on length, the model decides. Knowing tokens helps you specify precise lengths:

```
"Summarize this in 50 words"       → ~67 tokens of output
"Write a 500-word blog post"       → ~667 tokens of output
"Keep your response under 3 sentences" → clearer constraint
```

---

## 2.3 The Context Window — The Model's Working Memory

The **context window** is the maximum number of tokens an LLM can process in a single interaction — this includes BOTH your input (prompt + conversation history) AND the model's output (its response).

Think of it as a **whiteboard of fixed size**. Everything written on it (your messages, its responses, any documents you paste) uses up space. When the whiteboard is full, the oldest content starts getting erased.

### Context Window Sizes

| Model | Context Window | ≈ Word Count | Equivalent to |
|-------|---------------|-------------|--------------|
| GPT-3.5 Turbo | 16,385 tokens | ~12,000 words | A short novella |
| GPT-4o | 128,000 tokens | ~96,000 words | A 350-page book |
| Claude 3.5 Sonnet | 200,000 tokens | ~150,000 words | A 550-page book |
| Gemini 1.5 Pro | 1,000,000 tokens | ~750,000 words | A 2,700-page book |
| Gemini 1.5 Ultra | 2,000,000 tokens | ~1,500,000 words | Multiple encyclopedias |

### What Goes Into the Context Window

```
┌─────────────────────────────────────────────────────────────┐
│                    CONTEXT WINDOW                           │
│                  (e.g., 128,000 tokens)                     │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  SYSTEM PROMPT (optional)                           │   │
│  │  "You are a helpful assistant..."  (200 tokens)     │   │
│  ├─────────────────────────────────────────────────────┤   │
│  │  USER MESSAGE 1                                     │   │
│  │  "Explain quantum computing..."    (50 tokens)      │   │
│  ├─────────────────────────────────────────────────────┤   │
│  │  ASSISTANT RESPONSE 1                               │   │
│  │  "Quantum computing uses..."       (400 tokens)     │   │
│  ├─────────────────────────────────────────────────────┤   │
│  │  USER MESSAGE 2                                     │   │
│  │  "Now explain its business uses..."  (30 tokens)    │   │
│  ├─────────────────────────────────────────────────────┤   │
│  │  ASSISTANT RESPONSE 2                               │   │
│  │  "Businesses are using quantum..."  (350 tokens)    │   │
│  ├─────────────────────────────────────────────────────┤   │
│  │  ... (More turns of conversation) ...               │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  Total used: 1,030 tokens | Remaining: 126,970 tokens      │
└─────────────────────────────────────────────────────────────┘
```

### What Happens When Context Is Exceeded?

For consumer chatbots (ChatGPT, Claude.ai):
- The interface silently drops the oldest messages from the context
- The model "forgets" earlier parts of the conversation
- You may notice responses that ignore or contradict earlier instructions

For API usage:
- You receive an error: `context_length_exceeded`
- Your application must handle this by summarizing or trimming the context

**Example of context loss in practice:**

```
Message 1: "My name is Priya and I work in healthcare IT."
[...20 more messages about a technical topic...]
Message 22: "Now, with that background about my work, which approach fits my industry?"

PROBLEM: If messages 1-3 fell out of the context window, the model no longer
knows Priya is in healthcare IT and will give a generic answer.
```

---

## 2.4 Input Tokens vs Output Tokens

These are always tracked separately:

| Type | What it includes | Typical cost |
|------|-----------------|-------------|
| **Input tokens** | Your prompt + full conversation history | Cheaper |
| **Output tokens** | Text the model generates as response | More expensive (2-3x) |

**Why output costs more:** Generating each output token requires a full forward pass through the entire model. Input tokens can be processed more efficiently in parallel.

**Prompt engineering implication:** For cost-sensitive applications, shorter prompts that still achieve the same result are more efficient. This is why concise, well-structured prompts are professionally valuable.

---

## 2.5 Generation Parameters — Controlling How the Model Responds

Beyond your prompt text, several parameters control HOW the model generates its response. Understanding these helps you get more consistent, appropriate outputs.

### Parameter 1: Temperature

**Temperature** controls the randomness and creativity of the model's output.

Technically: Temperature scales the probability distribution of the next token. Low temperature = high confidence winner takes all. High temperature = the model picks from more options, including less likely ones.

```
Temperature = 0.0 (Deterministic)
─────────────────────────────────────────────────────
The model always picks the single highest-probability next token.
Every run of the same prompt gives the same (or very similar) result.

Use for: Factual Q&A, code generation, data extraction,
          classification, structured data output.

Example prompt: "What is the capital of France?"
Temperature 0 output: "Paris." (every time, identical)


Temperature = 0.7 (Balanced — most common default)
─────────────────────────────────────────────────────
Good balance of coherence and variety.
Each run may vary slightly in word choice and structure.

Use for: Professional writing, emails, reports, explanations.

Example: Business email drafting, blog post writing


Temperature = 1.5–2.0 (High creativity)
─────────────────────────────────────────────────────
The model picks from many possible tokens, including unlikely ones.
Output is highly varied, sometimes surprising, occasionally incoherent.

Use for: Creative fiction, brainstorming, poetry,
          generating unusual ideas.

Caution: Higher temperatures increase hallucination risk.
```

**Visual representation:**

```
Next word after "The cat sat on the..."

Probability distribution:
"mat"    ████████████████████████  0.75
"floor"  ████████                  0.12
"chair"  ████                      0.08
"table"  ██                        0.03
"roof"   █                         0.02

Temperature = 0:   Always picks "mat"
Temperature = 0.7: Usually "mat", sometimes "floor" or "chair"
Temperature = 2.0: Could pick any of these, "roof" becomes likely too
```

### Parameter 2: Max Tokens

Sets a hard limit on how many tokens the model can generate in its response.

```
"max_tokens": 100   → Very short response (~75 words)
"max_tokens": 500   → Short response (~375 words)
"max_tokens": 2000  → Medium response (~1,500 words)
"max_tokens": 4096  → Long response (~3,000 words)
```

**Important:** The model won't pad to fill this limit — it stops when it's done. Max tokens is a ceiling, not a target.

### Parameter 3: Top-P (Nucleus Sampling)

An alternative to temperature for controlling diversity. Instead of adjusting the full probability distribution, it limits the model to the smallest set of tokens whose combined probability adds up to P.

```
Top-P = 0.1: Only consider tokens making up top 10% of probability mass
             → Very conservative, predictable output

Top-P = 0.9: Consider tokens making up top 90% of probability mass
             → Moderate creativity (common default alongside temperature)

Top-P = 1.0: Consider all tokens
             → Full probability distribution
```

**Best practice:** Use EITHER temperature OR top-P, not both adjusted simultaneously (in most cases).

### Parameter 4: Frequency Penalty

Reduces the likelihood of the model repeating the same words or phrases it has already used.

```
Frequency Penalty = 0:    No penalty for repetition (default)
Frequency Penalty = 0.5:  Moderate reduction in word repetition
Frequency Penalty = 2.0:  Strong penalty — output uses very diverse vocabulary
```

**Use case:** When you notice the model repeating phrases like "It is important to note that..." or "Furthermore, it should be mentioned..." — increase frequency penalty.

### Parameter 5: Presence Penalty

Similar to frequency penalty, but applies a flat penalty to any word that has appeared at all (rather than scaling with how often it appeared). Encourages new topics/concepts.

### Quick Reference — Parameter Settings by Use Case

| Use Case | Temperature | Top-P | Max Tokens | Notes |
|----------|------------|-------|------------|-------|
| Code generation | 0.0–0.2 | 0.1 | 1000–4000 | Deterministic accuracy needed |
| Factual Q&A | 0.0–0.3 | 0.1 | 200–500 | Prevent creative "facts" |
| Business writing | 0.5–0.7 | 0.9 | 500–1500 | Natural but professional |
| Email drafting | 0.5–0.7 | 0.9 | 200–400 | Consistent quality |
| Creative writing | 0.8–1.2 | 0.95 | 1000–4000 | Allow variety |
| Brainstorming | 1.0–1.5 | 1.0 | 500–1000 | Diverse ideas valued |

---

## 2.6 Practical Context Management Strategies

When working with long documents or conversations, use these strategies:

### Strategy 1: Summarization Injection

Instead of pasting an entire conversation history, summarize what's been decided:

```
❌ Inefficient (pastes 5,000 tokens of history):
[Entire previous conversation pasted here]
Based on all of the above, what should we do next?

✅ Efficient (100-token summary injection):
Context: We have decided to target the B2B market, focus on SMEs,
price at ₹5,000/month, and launch in Q3. Key constraint: 3-person team.
Given this, what should our go-to-market strategy be?
```

### Strategy 2: Chunking Long Documents

For very long documents (contracts, research papers, reports):

```
Step 1 prompt:
"Read the following Section 1 of a contract and identify any unusual clauses.
Focus only on clauses related to payment terms and liability.
[Section 1 of 5 — paste here]"

Step 2 prompt:
"From Section 1, you identified: [key findings].
Now read Section 2 and identify the same. [Section 2 — paste here]"

Step 3:
"Here are findings from all 5 sections: [compiled findings].
Summarize the 3 highest-risk clauses in the full contract."
```

### Strategy 3: Progressive Summarization

Ask the AI to summarize its own previous responses:

```
"Summarize the key decisions and facts from our conversation so far
in 5 bullet points. I will use this as context for the next phase."
```

Then start a new conversation with those 5 bullets as your opening context.

### Strategy 4: Front-Loading Critical Information

The model pays more attention to information at the START of the context (primacy effect) and the END (recency effect). Place the most important context and instructions at the beginning, not buried in the middle.

```
✅ Good structure:
[Critical instructions at the top]
[Background information in the middle]
[Specific task and format at the end — restated from top]

❌ Avoid:
[Long background]
[Critical instruction buried at paragraph 7 of 10]
[Task at the end]
```

---

## 2.7 Token Counting — Practical Tools

### Using OpenAI's Tokenizer (Web Tool)

1. Visit: **https://platform.openai.com/tokenizer**
2. Paste any text
3. See how many tokens it uses and how it's broken up (color-coded)

### Using tiktoken in Python

```python
import tiktoken

def count_tokens(text: str, model: str = "gpt-4o") -> int:
    """Count the number of tokens in a string for a given model."""
    encoder = tiktoken.encoding_for_model(model)
    tokens = encoder.encode(text)
    return len(tokens)

def estimate_cost(prompt: str, response: str, model: str = "gpt-4o") -> dict:
    """
    Estimate the API cost of a prompt-response pair.
    Prices as of 2024 — check openai.com for current pricing.
    """
    pricing = {
        "gpt-4o": {"input": 5.00, "output": 15.00},        # per 1M tokens
        "gpt-4o-mini": {"input": 0.15, "output": 0.60},
        "gpt-3.5-turbo": {"input": 0.50, "output": 1.50},
    }
    
    input_tokens = count_tokens(prompt, model)
    output_tokens = count_tokens(response, model)
    
    if model in pricing:
        input_cost = (input_tokens / 1_000_000) * pricing[model]["input"]
        output_cost = (output_tokens / 1_000_000) * pricing[model]["output"]
        total_cost = input_cost + output_cost
    else:
        input_cost = output_cost = total_cost = 0
    
    return {
        "model": model,
        "input_tokens": input_tokens,
        "output_tokens": output_tokens,
        "total_tokens": input_tokens + output_tokens,
        "estimated_cost_usd": round(total_cost, 6)
    }

# Example usage
sample_prompt = "Explain the concept of compound interest with an example."
sample_response = "Compound interest is interest calculated on both the principal and the previously accumulated interest. For example, if you invest ₹10,000 at 10% annual compound interest, after year 1 you have ₹11,000. In year 2, you earn 10% on ₹11,000 (not just ₹10,000), giving you ₹12,100. This snowball effect makes compound interest powerful for long-term savings."

result = estimate_cost(sample_prompt, sample_response)
print(f"Input tokens: {result['input_tokens']}")
print(f"Output tokens: {result['output_tokens']}")
print(f"Estimated cost: ${result['estimated_cost_usd']}")
```

---

## Hands-On Activities — Session 2

---

### Activity 2.1 — Tokenizer Exploration

**Objective:** Develop an intuitive feel for token counts

1. Go to **https://platform.openai.com/tokenizer**
2. Test each of the following and record the token count:

| Text to Test | Your Token Count | Notes |
|-------------|-----------------|-------|
| Your full name | | |
| "Hello, how are you today?" | | |
| "Electroencephalography and pneumonoultramicroscopicsilicovolcanoconiosis" | | |
| A 200-word paragraph of your choice | | |
| The same paragraph translated to Hindi/Tamil/another language | | |
| A URL: https://www.example.com/some/long/path?query=test | | |
| 10 numbers: 1, 2, 3... 10 | | |
| The number 1000000000 | | |

**Discussion Questions:**
- Were any results surprising?
- How did the non-English text compare to English in token count?
- What are the implications for businesses building multilingual AI apps?

---

### Activity 2.2 — Context Window Experiment

**Objective:** Observe the context window limitation in practice

**Setup:**
1. Open ChatGPT (or any LLM)
2. In message 1, state: *"Remember this code for later: ALPHA-9923-ZEBRA"*
3. Have a long, genuine conversation about a different topic (10–15 exchanges minimum — discuss any topic at length)
4. After the long conversation, ask: *"What was the secret code I gave you at the start?"*

**Observe:**
- Did the model remember the code?
- If not, at what point in the conversation did it likely "forget"?
- How does this change how you would structure a long AI-assisted work session?

**Alternative approach for long-context models (Claude, Gemini):** Try the same experiment but with a piece of text buried in the middle of a very long document. Models often recall text from the start and end better than the middle ("lost in the middle" effect).

---

### Activity 2.3 — Temperature Effects

**Objective:** Experience how temperature changes output character

Use the ChatGPT API playground (platform.openai.com/playground) or equivalent, where you can control temperature.

Run this prompt three times, each with a different temperature:

```
Write an opening sentence for a thriller novel set in Mumbai.
```

| Temperature | Your Output | Your Observations |
|------------|------------|------------------|
| 0.0 | | |
| 0.7 | | |
| 1.5 | | |

**If you don't have API access**, describe to ChatGPT what you want:
```
Give me 3 very different opening sentences for a thriller novel set in Mumbai.
Make each one distinctly different in style, tone, and imagery — as if written
by 3 completely different authors.
```

---

### Activity 2.4 — Practical Context Management

**Objective:** Practice the summarization injection technique

**Scenario:** You've just had a 30-minute ChatGPT conversation planning a new product launch. Instead of continuing in that same conversation (which is getting long), you want to start fresh.

1. Ask the AI to create a context summary:
```
Summarize the key decisions, facts, constraints, and open questions from
our conversation so far. Format as:
- Key decisions made: (bullet list)
- Established facts/constraints: (bullet list)
- Open questions to resolve: (bullet list)
Maximum 200 words.
```

2. Start a new conversation
3. Paste the summary as your first message:
```
Context for this conversation:
[Paste the summary]

Given this context, let's now focus on [next topic].
```

**Reflection:** How does this approach compare to simply continuing the old conversation? What are the trade-offs?

---

## Revision Questions — Session 2

1. What is a token and how is it different from a word?
2. Approximately how many words does a 1,000-token limit correspond to?
3. A user pastes a 5,000-word PDF into ChatGPT. Approximately how many tokens is that?
4. What is the context window and what happens when it is exceeded?
5. Explain the difference between input tokens and output tokens. Why are output tokens more expensive in API pricing?
6. What does setting temperature = 0 mean for an LLM's output?
7. When building a customer service chatbot that must give accurate, consistent answers about return policies, what temperature setting would you recommend? Why?
8. You are processing a 200-page legal contract using an LLM. What strategies would you use to work within context limits?

---

## Key Takeaways — Session 2

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 2 KEY TAKEAWAYS                                             │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Tokens are the unit of LLM processing: ~0.75 words per token     │
│                                                                      │
│  ✓ Non-English text uses more tokens per word than English           │
│                                                                      │
│  ✓ Context window = model's working memory (input + output together) │
│    When exceeded → model forgets oldest content                      │
│                                                                      │
│  ✓ Temperature: 0 = deterministic | 0.7 = balanced | 1.5+ = creative│
│    Match temperature to task type                                    │
│                                                                      │
│  ✓ Max tokens = output length ceiling, not target                    │
│                                                                      │
│  ✓ Context management strategies:                                    │
│    → Summarization injection                                         │
│    → Document chunking                                               │
│    → Front-loading critical information                              │
│                                                                      │
│  ✓ For APIs: token count directly = cost. Efficiency matters at scale│
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 2 Complete → Proceed to Session 3: Prompt Anatomy*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
