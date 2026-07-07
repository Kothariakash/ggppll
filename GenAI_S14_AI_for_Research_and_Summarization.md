# Session 14: AI for Research & Summarization
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 3 — AI FOR PRODUCTIVITY                                              │
│  SESSION 14 of 30  |  1 Hour  |  30% Theory + 70% Hands-On                 │
│                                                                              │
│  "Research used to mean spending hours finding information.                  │
│   AI shifts your time to the harder and more valuable work:                 │
│   judging, connecting, and applying what you find."                         │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 14, you will be able to:

- Design a structured AI-assisted research workflow for any professional task
- Use Perplexity AI for cited, current-information research
- Summarize long documents, articles, and reports with precision
- Synthesize information from multiple sources into a unified analysis
- Apply the SIFT framework to evaluate AI-generated research content
- Perform comparative analysis and literature review using AI

---

## 1. The Research Transformation

### 1.1 How AI Changes Research Work

```
TRADITIONAL RESEARCH WORKFLOW:
  Define question → Search Google/databases → Open 20+ tabs
  → Read and take notes (hours) → Organize notes → Synthesize
  → Write summary → Identify gaps → Search again
  Total: 4–8 hours for a thorough research task

AI-ASSISTED WORKFLOW:
  Define question → AI orients you (10 min) → AI summarizes sources
  → You verify key claims (20 min) → AI synthesizes findings
  → You add judgment and implications (20 min)
  Total: 50–90 minutes for comparable depth

  CRITICAL: The quality of the research depends on you verifying
  AI outputs against primary sources — especially statistics,
  citations, and specific claims.
```

### 1.2 What AI Does Best in Research

| Research Task | AI Strength | AI Limitation | Human Role |
|--------------|------------|--------------|------------|
| Background orientation | Excellent | May be outdated | Verify with current sources |
| Long document summarization | Excellent | May miss nuance | Read key sections yourself |
| Comparative analysis | Good | May miss recent examples | Add current examples |
| Citation finding | RISKY | High hallucination risk | Always verify citations |
| Synthesis across sources | Good | Cannot read new paywalled papers | Provide sources to AI |
| Identifying research gaps | Good | Depends on training data | Supplement with expert knowledge |

---

## 2. The Research Orientation Prompt

### 2.1 Starting Any Research Topic

Use this as your first prompt for any new research area:

```
PROMPT:
I am beginning research on: [TOPIC]
My purpose: [WHY I AM RESEARCHING THIS — professional context]
My background knowledge: [BEGINNER / INTERMEDIATE / EXPERT]
Time available: [X hours for research]

Give me a research orientation that includes:
1. The 3–5 most important sub-topics I need to understand within this field
2. The key debates or controversies in this area (where experts disagree)
3. The 3 most important organizations or experts who are authoritative on this topic
4. Common misconceptions I should be aware of
5. The 3 most valuable search terms or databases for this topic
6. What you are NOT able to reliably tell me about this topic (your limitations)

This is a map, not a full answer. I want to know where to look.
```

### 2.2 Topic Deepening — The "Explain Like" Spectrum

Once you have orientation, deepen your understanding:

```
LEVEL 1 — For non-expert audience:
"Explain [TOPIC] to someone with no background in this field.
Use an everyday analogy. Under 200 words."

LEVEL 2 — For business professional:
"Explain [TOPIC] to a business professional who needs to understand
it well enough to make decisions about it, but not implement it.
Focus on: what it is, how it works, and business implications."

LEVEL 3 — For expert engagement:
"Explain the current state of debate on [TOPIC] among experts.
What are the strongest competing viewpoints?
What evidence supports each side?
What would it take to resolve the debate?"
```

---

## 3. Document Summarization — Precision Techniques

### 3.1 The Layered Summarization Approach

Different summaries serve different purposes. AI can generate each layer:

```
LAYER 1 — HEADLINE SUMMARY (30 words):
"Summarize this document in one sentence (under 30 words).
Capture: what it's about, the key finding, and who it's for."

LAYER 2 — EXECUTIVE SUMMARY (150 words):
"Write a 150-word executive summary. Include:
(1) Purpose of the document, (2) 3 key findings, 
(3) Main recommendation or conclusion, (4) Who should act on this."

LAYER 3 — DETAILED SUMMARY (500 words):
"Write a 500-word detailed summary preserving:
- All quantitative findings
- All specific recommendations
- Key methodology points
- Notable limitations or caveats
Use the same section headings as the original document."

LAYER 4 — EXTRACTION PROMPT:
"Extract from this document:
1. All statistics and numerical claims (with context)
2. All named recommendations
3. All definitions given for key terms
4. All limitations explicitly acknowledged by the authors
Present each as a numbered list."
```

### 3.2 The "Annotated Summary" Prompt

For academic papers, research reports, or complex technical documents:

```
PROMPT:
Read this document and create an annotated summary.

For each major section:
SECTION: [Section title]
SUMMARY: [2–3 sentence summary of this section]
KEY CLAIM: [The most important assertion made in this section]
EVIDENCE: [What evidence or data is provided to support it]
LIMITATION: [Any weakness, gap, or caveat in this section]
MY NOTE: [Leave blank — I'll fill this in myself]

After all sections:
OVERALL ASSESSMENT:
- Strongest argument made:
- Biggest gap or weakness:
- Most actionable finding for my purpose: [STATE YOUR PURPOSE]

DOCUMENT:
[PASTE DOCUMENT HERE]
```

---

## 4. Multi-Source Synthesis

### 4.1 Synthesizing Across Multiple Documents

When you have read multiple sources on a topic, use AI to create a unified synthesis:

```
PROMPT:
I have studied multiple sources on [TOPIC]. Here are summaries of the key points 
from each source:

SOURCE 1: [Name/Title]
Key points: [BULLET LIST]

SOURCE 2: [Name/Title]
Key points: [BULLET LIST]

SOURCE 3: [Name/Title]
Key points: [BULLET LIST]

Please synthesize these sources by:
1. POINTS OF AGREEMENT: Where do all (or most) sources agree?
2. POINTS OF DIVERGENCE: Where do sources contradict or disagree?
3. UNIQUE INSIGHTS: What does each source contribute that the others don't?
4. SYNTHESIS STATEMENT: A 3-sentence paragraph that integrates the most
   important insights across all sources into a coherent position.
5. RESEARCH GAP: What question is NOT answered by any of these sources?

Do not make up information not present in my summaries.
If sources don't address something, say so explicitly.
```

### 4.2 The Comparative Analysis Prompt

When you need to compare approaches, models, frameworks, or options:

```
PROMPT:
Compare these [NUMBER] approaches to [TOPIC]:
[LIST APPROACHES / OPTIONS / FRAMEWORKS]

Create a structured comparison covering:
1. A brief description of each approach (2–3 sentences)
2. A comparison table with these dimensions:
   | Approach | Core Principle | Best For | Key Limitation | Real-World Example |
3. Recommended approach for my context: [DESCRIBE YOUR CONTEXT]
   Justify the recommendation with specific reasons.

Note: If any comparison point is uncertain or contested, indicate
this clearly rather than presenting it as fact.
```

---

## 5. Research with Perplexity AI — Cited, Current Information

### 5.1 Why Perplexity for Research

```
ChatGPT (standard):
  ✓ Great for explanation and synthesis
  ✗ Knowledge cutoff — no current information
  ✗ No source citations in responses

Perplexity AI (perplexity.ai):
  ✓ Searches the live web for every query
  ✓ Provides numbered source citations for every claim
  ✓ Can focus search by domain type (academic, news, etc.)
  ✓ "Pro Search" mode reasons through complex research questions
  ✓ Ideal for: current events, recent data, statistics, citations
```

### 5.2 Effective Perplexity Prompts

**For Current Data:**
```
What is the current [STATISTIC/METRIC] for [TOPIC] in [GEOGRAPHY/INDUSTRY]?
Provide the most recent data available and cite the source.
```

**For Recent Developments:**
```
What are the most significant developments in [TOPIC] in the last 6 months?
Focus on: [SPECIFIC ASPECT]. Cite your sources.
```

**For Research Citations:**
```
I need credible sources on [TOPIC] for [PURPOSE — academic paper / business report / presentation].
Find 5 high-quality sources published in the last 2 years.
For each: title, author/organization, date, URL, and 2-sentence summary.
```

**For Fact Verification:**
```
Verify this claim: "[CLAIM YOU WANT TO CHECK]"
Is this accurate? What do credible sources say?
Cite your sources.
```

### 5.3 Using Perplexity + ChatGPT Together

The most powerful research workflow combines both tools:

```
STEP 1 — PERPLEXITY (Current facts with citations):
"What is the current state of [TOPIC]? Give me the 5 most important
recent developments with citations."

STEP 2 — VERIFY & SAVE (Human step):
Click through to verify the 2–3 most important claims.
Save the source links.

STEP 3 — CHATGPT (Deep synthesis and drafting):
"Using these verified facts: [PASTE PERPLEXITY FINDINGS]
Plus this background context: [PASTE ANY ADDITIONAL NOTES]
Write a comprehensive analysis of [TOPIC] for [PURPOSE]."

Result: Current, cited facts + deep analytical synthesis
```

---

## 6. The SIFT Framework — Evaluating AI Research Output

Every claim from AI research needs evaluation. Use SIFT:

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SIFT FRAMEWORK FOR EVALUATING AI RESEARCH                                   │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  S — STOP                                                                    │
│      Before accepting any claim, pause.                                     │
│      Ask: "Am I accepting this because it sounds credible, or because       │
│      I've actually verified it?"                                             │
│                                                                              │
│  I — INVESTIGATE THE SOURCE                                                  │
│      Who is the original source of this claim?                              │
│      Is the organization or author credible in this field?                  │
│      Was the research peer-reviewed?                                        │
│                                                                              │
│  F — FIND BETTER COVERAGE                                                    │
│      Is this the only source making this claim?                             │
│      Does independent corroboration exist?                                  │
│      Are there contradicting sources?                                        │
│                                                                              │
│  T — TRACE CLAIMS TO THEIR ORIGINAL CONTEXT                                 │
│      Often AI summarizes claims out of context.                             │
│      Find the original source and verify the claim                          │
│      was not misrepresented, exaggerated, or taken out of context.          │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

**High-Risk Signals in AI Research Output:**
```
⚠️  "Studies show that..." (which studies? what year? what sample size?)
⚠️  "According to experts..." (which experts? in what context?)
⚠️  Specific percentages without a source (e.g., "73% of companies...")
⚠️  Quotations attributed to real people (always verify the actual quote)
⚠️  Recent statistics (may be outdated due to knowledge cutoff)
⚠️  Very precise numbers (e.g., "$47.3 billion market size") — suspiciously precise
```

---

## 7. Specialized Research Prompts

### 7.1 Competitive Intelligence Research

```
PROMPT:
You are a competitive intelligence analyst. Research [COMPETITOR/INDUSTRY].

Provide structured competitive intelligence on [COMPANY/MARKET]:

1. COMPANY OVERVIEW (3–4 sentences: what they do, who they serve, scale)
2. KNOWN STRENGTHS (3 specific competitive advantages with evidence)
3. KNOWN WEAKNESSES (3 specific vulnerabilities with evidence)
4. RECENT STRATEGIC MOVES (product launches, acquisitions, partnerships — last 12 months)
5. MARKET POSITIONING (how they position vs. alternatives)
6. CUSTOMER PERCEPTION (what customers publicly say — review themes)
7. WHAT WE SHOULD WATCH (1–2 emerging threats or opportunities they represent)

For each point: indicate if this is CONFIRMED (public source) or INFERRED (logical assumption)
Note: I will verify all specific claims before using them professionally.
```

### 7.2 Academic / Literature Review Support

```
PROMPT:
I am writing a literature review on [TOPIC] for [PURPOSE — MBA thesis / research paper / report].

Based on your training knowledge, help me map the academic landscape:
1. The 3–5 most influential theoretical frameworks in this field
2. Key scholars or researchers known for their work in this area
3. The major debates or schools of thought
4. Evolution of thinking on this topic over time (key paradigm shifts)
5. Suggested search terms for Google Scholar, PubMed, or JSTOR

IMPORTANT: I will use this as a starting map only. I will independently
verify all sources and find actual papers for citation. Do not generate
fake citations. Flag anything you are uncertain about.
```

### 7.3 Industry and Market Research

```
PROMPT:
You are a market research analyst. Provide a market overview for:
Industry: [INDUSTRY]
Geography: [COUNTRY/REGION]
Purpose: [WHY I NEED THIS — investment decision / market entry / competitive analysis]

Cover:
1. MARKET SIZE AND GROWTH (estimate order of magnitude — note uncertainty)
2. KEY PLAYERS (top 5 with brief description of their positioning)
3. KEY TRENDS (3–4 macro trends shaping this market)
4. REGULATORY ENVIRONMENT (major regulations affecting the industry)
5. COMPETITIVE DYNAMICS (how intense is competition, what does it compete on?)
6. DISRUPTION RISKS (what could reshape this industry in 5 years?)

For each section: distinguish between widely accepted facts vs. your analysis.
Flag every statistic as [VERIFY — current figure may differ].
```

---

## 8. Real-World Example: AI Research at a Management Consulting Firm

**Scenario:** A management consulting team (3 consultants) receives a new engagement: a 6-week project to advise a pharmaceutical company on entering the Indian generic drugs market. The team must become domain experts in 2 weeks.

**Traditional Approach (without AI):**
- Each consultant reads 15–20 industry reports (2–3 days per report)
- Team divides up sub-topics, takes notes independently
- Team meeting to align understanding (3 hours)
- Junior consultant writes background section (2 days)
- Total: 2 full weeks

**AI-Assisted Approach:**

```
WEEK 1, DAY 1 (2 hours total):
  ─────────────────────────────────────────────────────────────────
  Prompt 1 (Perplexity): Current state of Indian generic pharma market
  → Current facts + sources in 5 minutes
  
  Prompt 2 (ChatGPT): Research orientation on Indian pharma market
  → Sub-topics map, key debates, key players, search terms
  
  Prompt 3 (Claude): Upload and summarize 3 key industry reports 
  → 100-page reports → 500-word summaries in 10 minutes each
  
  Prompt 4 (ChatGPT): Synthesize the 3 summaries
  → Unified synthesis, points of agreement/divergence, gaps
  
  Prompt 5 (ChatGPT): Competitive analysis of top 5 players
  → Structured comparison table in 5 minutes

  Result: Team has research-ready knowledge in 2 hours
  that would have taken 2 weeks traditionally
```

**Outcomes:**
- Background section written in 4 hours vs. 2 days
- Research quality: comparable; team spent freed time on primary interviews
- Client interviews started on Day 3 instead of Day 14
- More time on synthesis and recommendations → higher-value deliverable

---

## 9. Hands-On Lab 14: Research Sprint

**Objective:** Complete a structured research task using AI from orientation to synthesis  
**Duration:** 25 minutes  
**Tools:** Perplexity AI + ChatGPT/Claude

---

### Step 1: Choose a Research Topic (2 minutes)

Choose a topic relevant to your professional goals. Examples:
- AI adoption in Indian banking
- Sustainable packaging trends in FMCG
- Remote work productivity research
- EdTech market in Southeast Asia
- EV charging infrastructure in India

---

### Step 2: Research Orientation (5 minutes)

Use ChatGPT with the Research Orientation Prompt.
Record:
- The 5 sub-topics the AI identified
- The 2 most interesting debates in the field
- The 3 most important sources or experts mentioned
- 1 thing AI flagged as uncertain or beyond its knowledge

---

### Step 3: Current Facts with Citations (5 minutes)

Use Perplexity AI: "What are the 5 most important recent developments in [YOUR TOPIC]? Cite sources."
Record:
- 3 specific facts with source URLs
- Click through to verify 1 fact against its source — was the AI accurate?

---

### Step 4: Document Summarization (8 minutes)

Find one document related to your topic (news article, report, Wikipedia page).
Paste it into ChatGPT using the Annotated Summary Prompt.
Record:
- The key claim from the most important section
- The biggest limitation or gap the AI identified
- Whether the AI's summary accurately represents the original

---

### Step 5: Synthesis (5 minutes)

Combine your findings from Steps 2, 3, and 4. Use the Multi-Source Synthesis Prompt.
Generate a 200-word synthesis that you could use in a business presentation.

---

### Lab Evaluation Rubric

| Deliverable | Marks |
|-------------|-------|
| Step 2: Research orientation screenshot + 4 records | 2 |
| Step 3: 3 cited facts + fact verification result | 3 |
| Step 4: Annotated summary + accuracy assessment | 2 |
| Step 5: 200-word synthesis produced | 3 |
| **Total** | **10** |

---

## 10. Interview Questions — Session 14

**Q1:** *"How would you use AI to conduct research for a business report?"*

**Strong Answer:**
"I use a three-tool workflow. First, I use ChatGPT for research orientation — it maps the sub-topics, debates, key players, and limitations of the field in 10 minutes, giving me a research map rather than diving in blind. Second, for current facts and citations, I use Perplexity AI because it searches the live web and cites sources — I then verify the most important claims against the original sources. Third, I use Claude for summarizing long documents, because its 200K context window handles full reports at once. I synthesize across sources using ChatGPT's multi-source synthesis prompt. Throughout, I apply the SIFT framework to evaluate every claim — especially statistics, specific percentages, and any quantitative finding — before including it in professional work."

---

## 11. Revision Questions — Session 14

1. What is the SIFT framework? Explain each letter with a practical research example.
2. Why is Perplexity AI better than ChatGPT for finding current statistics with citations?
3. What is the "layered summarization approach"? Describe the 4 layers and when each is useful.
4. What is the Multi-Source Synthesis Prompt designed to produce? What are its 5 outputs?
5. List 5 "high-risk signals" in AI research output that should trigger verification.
6. Describe the two-tool (Perplexity + ChatGPT) research workflow. Why is combining both more powerful than either alone?
7. In the consulting firm example, how did AI change the team's research timeline? What did the freed time allow them to do?
8. Why should you never use AI-generated citations without verification? What specifically can go wrong?

---

## 12. Key Terminology — Session 14

| Term | Definition |
|------|-----------|
| **Research Orientation** | A map of a topic's sub-topics, debates, and key sources — not a full answer |
| **Layered Summarization** | Producing summaries at different depths (30 words → 150 → 500) for different uses |
| **Multi-Source Synthesis** | Combining findings from multiple sources into a coherent unified analysis |
| **SIFT Framework** | Stop, Investigate the source, Find better coverage, Trace to original context |
| **Perplexity AI** | Web-connected AI research tool that cites sources for every claim |
| **Annotated Summary** | A summary that includes assessment of each section's key claim, evidence, and limitation |
| **Comparative Analysis** | A structured comparison of multiple approaches, options, or frameworks |
| **Literature Review** | A survey of existing research and scholarship on a topic |
| **Citation Hallucination** | AI generating fake but realistic-looking academic citations |

---

## 13. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 14 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  AI research workflow: Orientation → Current facts (Perplexity) →        │
│     Document summarization → Synthesis → Human judgment layer               │
│  ✓  Perplexity for current facts + citations; ChatGPT for deep synthesis    │
│  ✓  4 summarization layers: 30 words / 150 words / 500 words / extraction   │
│  ✓  Multi-source synthesis: agreement, divergence, unique insights, gaps     │
│  ✓  SIFT: Stop, Investigate source, Find coverage, Trace to original        │
│  ✓  High-risk signals: vague "studies show," specific % without source,     │
│     quotes from real people, recent statistics                               │
│  ✓  NEVER use AI-generated citations without verification                   │
│  ✓  Consulting example: 2 weeks of research → 2 hours with AI workflow      │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 15 — Building Your Personal AI Productivity System                 │
│  (Designing your personal AI workflow, measuring impact, building           │
│   habits that compound, and your 30-day AI adoption plan)                   │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 14 Complete | Next: Session 15 — Building Your Personal AI Productivity System*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
