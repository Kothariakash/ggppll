# Session 13: AI for Presentations — From Outline to Slide-Ready Content
## Module 3 — Academic & Professional Applications
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 13 OF 30  │  Module 3, Session 3                          │
│  Topic: AI for Presentations — Structure, Content & Speaker Notes   │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Use AI to structure a compelling presentation narrative arc
2. Generate slide-by-slide content with titles, bullets, and speaker notes
3. Create opening hooks, transitions, and closing calls to action with AI
4. Adapt presentation content for different audiences and time constraints
5. Use AI to transform existing documents into presentation structures
6. Build presentation templates for recurring use cases

---

## 13.1 The Presentation Challenge

Presentations fail for predictable reasons:
- **Too much text** on slides (reading the slide, not presenting)
- **No narrative arc** (a list of facts, not a story)
- **Wrong audience calibration** (wrong depth, wrong vocabulary)
- **Weak opening** (fails to capture attention in the first 60 seconds)
- **No clear call to action** (audience doesn't know what they should do)

AI, used correctly, addresses all of these — because a well-structured prompt forces you to think about audience, narrative, and purpose before generating a single slide.

---

## 13.2 The Presentation Structure Framework

Before generating any slide content, build the narrative architecture.

### Presentation Architecture Prompt

```
You are an executive presentation coach who has helped leaders at Fortune 500
companies deliver high-stakes presentations to boards, investors, and conference
audiences.

I need to design a [DURATION]-minute presentation for the following:

Audience: [Who they are, their role, what they care about, what they know]
Purpose: [What should the audience DO or BELIEVE after this presentation?]
Context: [Where is this being delivered? What is the setting? Formal/informal?]
Topic: [What are you presenting about?]
Key message: [If the audience remembers one thing, what should it be?]
Evidence I have: [List the strongest facts, data, or examples you have]

Design a complete presentation structure:
1. NARRATIVE ARC — Describe the story in 3–4 sentences (not the slides — the story)
2. SLIDE COUNT — Recommended number of slides for [DURATION] minutes
3. SLIDE MAP — List each slide with:
   - Slide #
   - Slide title (the "message headline" — not a topic label, but a complete statement)
   - Purpose (what does this slide accomplish in the narrative?)
   - Key content (3 words maximum — what visual/data goes here?)
   - Transition to next (how does this slide connect to the next one?)
4. OPENING (first 60 seconds) — recommended hook type with 1-sentence description
5. CLOSING — recommended structure for final 2 minutes
```

---

### The Message Headline Principle

Most presenters use topic labels as slide titles: "Market Analysis," "Financial Results," "Our Strategy." These tell the audience nothing — they are filing labels, not communication.

**Message headlines** are complete sentences that state the key takeaway of that slide:

| Topic Label (Weak) | Message Headline (Strong) |
|-------------------|--------------------------|
| Market Analysis | The Indian EdTech market is growing at 39% CAGR — and we are positioned in the fastest-growing segment |
| Q3 Financial Results | Q3 revenue grew 24% YoY, driven by our enterprise segment — on track for annual target |
| Competition | Our three main competitors have no presence in Tier 2 cities — our biggest opportunity |
| Our Strategy | One decision separates us from 40% revenue growth: expand to B2B before Q3 |
| Next Steps | Three actions this week will determine whether we hit our Q4 target |

**Slide title prompt:**
```
"I have a presentation slide about [TOPIC].
Convert this topic label into a message headline — a single complete sentence
that states the most important takeaway from this slide.
The audience is [AUDIENCE].
The key fact/data I'm presenting is: [DESCRIBE].

Give me 3 options ranging from:
Option 1: Factual (states the finding)
Option 2: Implication (states what the finding means)
Option 3: Action (states what should happen because of the finding)"
```

---

## 13.3 Slide-by-Slide Content Generation

Once the architecture is set, generate each slide's content individually.

### Standard Slide Content Prompt

```
Generate content for Slide [N] of my presentation.

Context:
- Presentation topic: [TOPIC]
- Total slides: [N]
- Audience: [AUDIENCE]
- This slide's position in narrative: [early context-setting / problem statement /
  evidence / solution / call to action / etc.]
- Previous slide summary: [What the slide before this covered]
- Next slide preview: [What comes after]

For this slide, generate:
SLIDE TITLE: [Message headline — complete sentence, max 12 words]
KEY VISUAL DESCRIPTION: [Describe what image, chart, or diagram would best
  illustrate this slide — no text-heavy designs]
BULLET POINTS: [Maximum 3 bullets. Each: max 8 words. Outcome-oriented.]
  • [Bullet 1]
  • [Bullet 2]
  • [Bullet 3]
SPEAKER NOTES: [What you would SAY — not read — about this slide.
  Full sentences. 3–4 sentences. Include the 1 thing the audience must
  remember from this slide.]
TRANSITION: [The sentence you would use to move to the next slide]

Slide content focus: [Describe what this slide covers]
```

---

### Opening Hook Slide — Types and Prompts

The first 60 seconds determine whether your audience is with you for the full presentation.

**Hook Type 1 — The Surprising Statistic:**
```
"Create an opening hook slide for a [DURATION] presentation about [TOPIC].

Hook type: Surprising statistic
Audience: [AUDIENCE]
The core message of my presentation: [MESSAGE]

Generate:
- A startling statistic that makes the audience sit up
  (flag if this is approximate — I will verify)
- The slide title as a provocative question
- 1-sentence setup before revealing the statistic
- 2-sentence bridge connecting the statistic to my presentation message
- Speaker note: what to say in the first 30 seconds"
```

**Hook Type 2 — The Provocative Question:**
```
"Open my presentation with a question that makes the audience reflect
on their own experience before I present my solution.

Topic: [TOPIC]
Audience: [AUDIENCE]
Core challenge I'm addressing: [THE PROBLEM]

Generate:
- 1 powerful rhetorical question (max 12 words)
- A short pause instruction for the speaker
- A 2-sentence follow-up that bridges to the presentation
- Slide title: the question itself
- Visual suggestion: what image would amplify this question?"
```

**Hook Type 3 — The Story Opening:**
```
"Write a 60-second story opening for my presentation.

The story should:
- Feature a real-seeming character facing the exact problem my presentation addresses
- Reach a turning point moment where the solution (my topic) becomes relevant
- End with a bridge line connecting the story to my presentation

Topic: [TOPIC]
Core problem I'm solving: [PROBLEM]
Audience: [DESCRIBE — they should see themselves in the story character]

Story format:
- Setting (1 sentence): when, where, who
- Problem moment (2 sentences): what went wrong
- Emotional stakes (1 sentence): what this meant for the character
- Resolution hint (1 sentence): what changed everything
- Bridge (1 sentence): 'In the next [X] minutes, I'll show you exactly how...'

Tone: Professional but human. This is real life, not a fairy tale."
```

---

## 13.4 Audience Adaptation

The same presentation content must be reshaped for different audiences.

### Audience Adaptation Prompt

```
I have a presentation on [TOPIC] that I have designed for [ORIGINAL AUDIENCE].
I now need to deliver it to [NEW AUDIENCE], who differ in these ways:
- Technical level: [Original level] → [New level]
- What they care most about: [Original priorities] → [New priorities]
- Likely objections: [List 2–3 things the new audience might push back on]
- Time available: [Original time] → [New time if different]

Adapt my presentation for the new audience by:
1. Recommending which slides to remove entirely (with reason)
2. Recommending which slides need significant content changes
3. Suggesting what NEW content or emphasis to add
4. Rewriting the opening hook for the new audience
5. Adapting the call to action for what THIS audience can actually decide

Original slides summary: [List each slide with its title and 1-sentence description]
```

### Time Constraint Adaptation

```
I need to cut my [ORIGINAL DURATION]-minute presentation to [NEW DURATION] minutes.

My slides:
[List all slides with their message headlines]

Recommend:
1. Which slides to cut entirely (with justification — what do we lose?)
2. Which slides to combine
3. Which slides are non-negotiable and must stay
4. How to restructure the opening and closing to work in the new time
5. Rewrite the slide map for the shorter version

Priority: preserve [CORE MESSAGE]. Everything else is negotiable."
```

---

## 13.5 Document to Presentation Transformation

### Report-to-Slides Prompt

```
Convert the following report into a [N]-slide presentation for [AUDIENCE].

Transformation rules:
- One key idea per slide — no information dumping
- Convert data tables into visual descriptions (describe what chart type to use)
- Convert report conclusions into action-oriented message headlines
- Reduce all body text to 3 bullets of max 8 words each
- Generate speaker notes for each slide (what to SAY, not read)
- The narrative must flow as a story, not as report sections

Presentation format:
Slide # | Message Headline | Bullets (3 max) | Visual Description |
Speaker Note (2–3 sentences) | Transition to next slide

Report: [paste full report]
```

---

## 13.6 Specific Presentation Types — Prompt Templates

### Investor Pitch (5 Minutes / 10 Slides)

```
You are a startup pitch coach who has helped companies raise $200M+.
You know what investors want to hear — and what kills deals in the first 2 minutes.

Design a 10-slide, 5-minute investor pitch for:
Company: [NAME]
Industry: [SECTOR]
Stage: [Pre-seed / Seed / Series A]
Problem solved: [1 sentence]
Solution: [1 sentence]
Traction: [Key metrics — revenue, users, growth rate, partnerships]
Ask: [Amount raising, what for, expected milestone]

Generate the 10-slide structure following this investor pitch framework:
1. Title — Company name + tagline + founder name
2. Problem — The pain, made vivid (a story or statistic)
3. Solution — What you do (demo/screenshot concept description)
4. Market — TAM / SAM / SOM with sourcing note
5. Business model — How you make money
6. Traction — Key metrics that prove this is working
7. Competition — Where you sit in the landscape (matrix)
8. Team — Why THIS team
9. Financials — 3-year projection + unit economics key metric
10. The Ask — Amount, use of funds, milestone this enables

For each slide: message headline + 3 bullets + speaker note + visual description.
Investor focus: What is the one question each slide answers in their mind?"
```

### Board Report Presentation

```
Design a board presentation on [TOPIC] for a [COMPANY TYPE] board of directors.

Board context:
- Board composition: [e.g., 8 members: 3 independent, 2 investor, 2 management, 1 chair]
- Meeting duration allotted: [TIME]
- Board's primary concerns: [e.g., financial performance, risk, strategic direction]
- Decision needed: [What must the board decide or approve?]

Board presentation principles:
- Lead with the recommendation or decision needed (boards don't like suspense)
- Every slide must earn its place — no background slides unless asked
- Anticipate the 3 hardest questions and address them preemptively
- Data must be board-level: trends, not operational detail

Generate:
1. Slide map (all slides with message headlines and purpose)
2. The recommended opening sentence (first words out of your mouth)
3. The 3 most likely board questions and suggested responses
4. Any slides that boards typically challenge — and how to strengthen them"
```

### Training / Workshop Presentation

```
Design a [DURATION]-minute training presentation on [TOPIC] for [AUDIENCE].

Training presentation rules (different from informational presentations):
- Every 10 minutes: engagement moment (question, activity, reflection, discussion)
- Learning objectives go on slide 2 — audience knows what they'll be able to DO
- Use "you will be able to..." framing for objectives, not "we will cover..."
- Include at least 2 knowledge check moments (not just Q&A at end)
- Close with an action commitment: what will they DO differently tomorrow?

Generate:
1. Learning objectives (3–5, all starting with action verbs)
2. Full slide map with engagement moments marked [ENGAGE]
3. 2 knowledge check questions with model answers
4. Closing action commitment slide content
5. Speaker notes for the most complex concept slide"
```

---

## 13.7 Speaker Notes — Making Them Actually Useful

Most speaker notes are either empty or are full text that the presenter reads word-for-word. Good speaker notes are a conversation script.

**Speaker Notes Generation Prompt:**

```
Write speaker notes for this slide that I will use as a conversation script — not text to read aloud.

Slide title: [TITLE]
Slide bullets: [PASTE BULLETS]
Audience: [AUDIENCE]
Time for this slide: [X seconds/minutes]

Speaker notes must include:
1. OPENING LINE — the exact sentence I'll say when this slide appears (conversational, not read)
2. KEY POINT ELABORATION — 1 sentence expanding each bullet with a real detail or example
3. DELIVERY NOTE — where to pause, where to emphasize, where to make eye contact with the room
4. BRIDGE — the transition sentence to the next slide
5. BACKUP DETAIL — 1 additional fact or example in case of questions (in italics)

Format: Conversational prose, as if you're coaching me on what to say.
Not formal. Not bullet points — actual sentences I would speak."
```

---

## 13.8 Handling Q&A with AI Preparation

Prepare for audience questions before you present.

```
I am presenting [TOPIC] to [AUDIENCE].
My key argument is: [YOUR MAIN MESSAGE]

Generate the 8 hardest questions this audience is likely to ask.

For each question:
- Question (word it as a skeptic would ask — challenging, not gentle)
- Why they're asking it (what underlying concern does this question reveal?)
- Recommended answer strategy (acknowledge the concern / reframe / provide data / defer to follow-up)
- Suggested response (2–3 sentences — confident, honest, not defensive)
- What NOT to say (the trap answer that would damage credibility)

Focus on questions that: challenge your data, question your assumptions,
compare you to alternatives, or probe implementation risks.
```

---

## Hands-On Activities — Session 13

---

### Activity 13.1 — Full Presentation Architecture

**Objective:** Build a complete presentation structure using AI.

**Task:** Design a 10-minute presentation you could actually give in the next month — at work, at a community event, for a job interview, or at a training.

**Step 1:** Run the Presentation Architecture Prompt.

**Step 2:** Evaluate the narrative arc — does it tell a story with a clear beginning (why this matters), middle (the content), and end (what to do)?

**Step 3:** Convert all slide titles from topic labels to message headlines using the Message Headline prompt for any that are still topic labels.

**Deliverable:** Complete slide map with 10 message headlines and speaker note summaries.

---

### Activity 13.2 — Three Opening Hooks

**Objective:** Practice generating and evaluating different hook types.

For the same presentation topic from Activity 13.1, generate all 3 hook types:
- Surprising Statistic
- Provocative Question
- Story Opening

**Evaluate each:**
- Which feels most authentic to your presenting style?
- Which would resonate most with your specific audience?
- Which is most appropriate for the setting (formal board vs. team meeting vs. conference)?

Choose one and refine it based on your evaluation.

---

### Activity 13.3 — Document-to-Presentation Transformation

**Objective:** Convert an existing document into a presentation structure.

**Step 1:** Take any existing document — a report you've written, a news article, a case study, or a blog post (500+ words).

**Step 2:** Run the Report-to-Slides prompt, targeting a 5-slide structure.

**Step 3:** Evaluate: Did the AI capture the core message? Were any important points lost? Did the narrative flow as a story?

**Step 4:** Make 2 rounds of iterations based on what was missing or wrong.

---

### Activity 13.4 — Q&A Preparation Drill

**Objective:** Use AI to prepare for challenging questions.

**Step 1:** Run the Q&A Preparation prompt for your presentation topic.

**Step 2:** Practice answering each question out loud using the suggested response as a starting point — but in your own words.

**Step 3:** Identify the 2 questions you feel least prepared for. For each, ask AI for a deeper preparation:

```
"I'm not confident answering this question: [QUESTION]
My concern is: [WHY IT'S HARD]
Help me prepare a thorough, honest answer that:
- Acknowledges the legitimate concern behind the question
- Provides the best answer I can honestly give
- Identifies what I would need to find out if I don't know
- Avoids defensive or evasive language"
```

---

## Revision Questions — Session 13

1. What is the difference between a topic label and a message headline? Why does this distinction matter for audience comprehension?
2. Describe 3 types of presentation opening hooks. For what kind of audience is each most effective?
3. You need to give the same presentation to two audiences: your technical team and the board of directors. Describe the specific changes AI would recommend and why.
4. What makes speaker notes useful? What is the most common mistake with speaker notes?
5. How many bullets should a slide have and why? What is the rule on bullet length?
6. You have a 60-page report that needs to become a 15-minute board presentation. Describe the AI-assisted process you would use to do this transformation.
7. Why is Q&A preparation an often-overlooked use of AI for presentations?
8. A sales manager says "I paste my data into ChatGPT and it gives me a full presentation." What is missing from this approach and what would you add?

---

## Key Takeaways — Session 13

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 13 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ Build narrative arc BEFORE generating slides — story first,      │
│    structure second, content third                                   │
│                                                                      │
│  ✓ Message headlines = complete sentences stating the takeaway      │
│    (not topic labels — "Market is growing fast" not "Market Analysis")│
│                                                                      │
│  ✓ 3 bullets max per slide, 8 words max per bullet                 │
│    Slides show what you say — they don't say it for you            │
│                                                                      │
│  ✓ Opening hook: first 60 seconds determine the audience's          │
│    engagement for the entire presentation                            │
│                                                                      │
│  ✓ Speaker notes should be conversation scripts, not read-aloud text│
│                                                                      │
│  ✓ Always prepare Q&A with AI — anticipate the hardest questions   │
│    and practice answers before you're in the room                   │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 13 Complete → Proceed to Session 14: AI for Email & Communication*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
