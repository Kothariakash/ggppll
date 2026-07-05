# Session 17: AI for Human Resources
## Module 4 — Business & Industry Applications
### Prompt Engineering Certification Program

---

```
┌─────────────────────────────────────────────────────────────────────┐
│  SESSION 17 OF 30  │  Module 4, Session 2                          │
│  Topic: AI for Human Resources — Recruitment, Performance & Culture │
│  Duration: 60–90 minutes                                            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of this session, you will be able to:
1. Use AI to write compelling, inclusive job descriptions
2. Generate structured interview frameworks for any role
3. Use AI to assist with performance reviews and feedback writing
4. Create HR policy documents and employee communications with AI
5. Apply ethical AI practices specific to HR and people management
6. Build an HR prompt library covering the full employee lifecycle

---

## 17.1 AI's Role in HR — Opportunity and Ethics

HR is a domain where AI offers significant productivity gains — and where the ethical stakes are equally significant. A poorly designed AI-assisted HR process can introduce bias, violate privacy, and damage employee trust.

**The Golden Rule for AI in HR:**
> AI assists human judgment — it never replaces it. Every AI-generated HR output must be reviewed, contextualized, and owned by an HR professional before use.

### High-Value, Lower-Risk AI Uses in HR

| Use Case | AI Role | Human Role |
|----------|---------|-----------|
| Job descriptions | Draft creation | Bias review + final approval |
| Interview questions | Framework generation | Selection + situational calibration |
| Performance review support | Language suggestions | Assessment judgment + context |
| HR policy drafts | Structure + language | Legal review + compliance check |
| Employee communications | First draft | Tone calibration + final approval |
| Onboarding materials | Content creation | Cultural accuracy check |

### High-Risk Uses to Approach with Extreme Caution

```
⚠️ NEVER use AI to:
- Make hiring decisions (AI output is an input to human judgment only)
- Evaluate employee performance scores autonomously
- Generate termination reasons without legal review
- Process employee personal data through consumer AI tools
- Screen resumes using AI without bias audit and human oversight
```

---

## 17.2 Job Descriptions — Complete Framework

### Job Description Generation Prompt

```
You are an experienced HR business partner known for writing job descriptions
that attract top talent through clarity, authenticity, and inclusion.

Role to fill: [JOB TITLE]
Department: [DEPARTMENT]
Company: [COMPANY NAME AND 2-SENTENCE DESCRIPTION]
Team size: [TEAM CONTEXT]
Why this role exists now: [STRATEGIC REASON — growth, replacement, new function]
Direct manager: [THEIR TITLE]
Key challenge this person will solve: [THE PRIMARY PROBLEM THEY WILL OWN]
Compensation range: [RANGE OR "Competitive / To be discussed"]

Write a complete job description with these sections:

1. ABOUT [COMPANY] (3 sentences — mission, culture, why it's a great place to work)

2. ABOUT THE ROLE (2 paragraphs — what makes this role unique and impactful;
   what success looks like in 12 months)

3. WHAT YOU'LL DO (6–8 bullet points — action verb-led, outcome-focused)

4. WHAT WE'RE LOOKING FOR
   Must Have (5 items): Essential qualifications
   Nice to Have (3 items): Differentiators

5. WHAT WE OFFER (5–7 items: salary range, benefits, growth, culture)

6. OUR COMMITMENT TO INCLUSION (2 sentences — genuine, not boilerplate)

Inclusion rules:
- No gendered language ("he/she" → "they"; remove masculine-coded adjectives
  like "aggressive," "dominant," "competitive" where not genuinely required)
- No age-coded language ("recent graduate" / "digital native")
- No unnecessary years-of-experience requirements if skills matter more
- Focus on what someone CAN DO, not what degree they have

Tone: Exciting opportunity, not a compliance form. Reads like we want them,
not like we're listing requirements to filter people out.
```

---

### Job Description Bias Audit Prompt

After generating any job description:

```
Audit the following job description for potential bias that could deter
qualified candidates from underrepresented groups.

Check for:
1. GENDER CODING — masculine-coded words (aggressive, dominant, competitive,
   ninja, rockstar) or feminine-coded words that may not attract all genders
2. AGE CODING — language that implies preference for younger or older candidates
3. CREDENTIAL BIAS — degree requirements where skills/experience could substitute
4. CULTURAL ASSUMPTIONS — jargon or references that assume a specific cultural background
5. DISABILITY EXCLUSION — language that implies physical requirements not relevant to role
6. SOCIOECONOMIC BIAS — unpaid internship requirements or "prestigious institution" language

For each issue found: flag the phrase → explain the potential impact →
suggest an inclusive alternative.

Job description: [paste]
```

---

## 17.3 Interview Frameworks

### Structured Interview Question Generator

```
Generate a structured interview framework for a [JOB TITLE] role at a
[COMPANY TYPE].

Key competencies required for this role (from job description):
[LIST 5–7 COMPETENCIES — e.g., stakeholder management, data analysis,
communication, problem-solving, leadership, etc.]

For each competency, generate:
- 1 BEHAVIORAL question (past experience: "Tell me about a time when...")
- 1 SITUATIONAL question (hypothetical: "Imagine you are...")
- PROBING FOLLOW-UPS: 2 questions to go deeper if the answer is vague
- GREEN FLAGS: What excellent answers typically include
- RED FLAGS: What concerning answers look like

ALSO GENERATE:
- 3 Culture fit questions (open-ended, non-leading)
- 2 Role-specific technical questions
- 2 Questions the CANDIDATE should ask (to assess quality of their preparation)
- 1 Closing question ("Is there anything we haven't covered...?")

Evaluation guide: How would you rate each answer on a 1–5 scale?
What distinguishes a 3 from a 5?
```

---

### Interview Scorecard Generator

```
Create an interview scorecard for evaluating candidates for [ROLE].

Format:
┌─────────────────────────────────────────────────────────────────┐
│ CANDIDATE: _________________ DATE: ________ INTERVIEWER: _____ │
├─────────────────────────────────────────────────────────────────┤
│ COMPETENCY RATINGS (1=Poor, 2=Below Exp, 3=Meets, 4=Exceeds,   │
│ 5=Exceptional)                                                  │
├──────────────────────────┬───────┬───────────────────────────── │
│ Competency               │ Score │ Evidence (specific examples) │
├──────────────────────────┼───────┼───────────────────────────── │
│ [Competency 1]           │  /5   │                              │
│ [Competency 2]           │  /5   │                              │
│ [etc.]                   │  /5   │                              │
├──────────────────────────┴───────┴───────────────────────────── │
│ OVERALL: Strong Hire / Hire / Maybe / No Hire                   │
│ REASONING: _________________________________________________    │
│ CONCERNS (if any): _________________________________________    │
└─────────────────────────────────────────────────────────────────┘

Generate this scorecard for a [ROLE] with these core competencies:
[LIST COMPETENCIES]

For each competency include: 2-sentence description of what it means
for this specific role."
```

---

## 17.4 Performance Reviews

### Performance Review Comment Generator

Performance review writing is one of the most dreaded HR tasks — AI helps you write specific, balanced, professional comments faster.

**Critical principle:** AI helps structure and phrase — but EVERY specific claim, achievement, and rating must come from your own knowledge of the employee.

```
You are an experienced HR business partner who coaches managers to write
clear, fair, and development-focused performance reviews.

I need to write a performance review comment for [EMPLOYEE NAME],
[THEIR ROLE], for the period [DATE RANGE].

Their actual performance information (what I know):
ACHIEVEMENTS: [List specific, factual achievements you observed]
STRENGTHS DEMONSTRATED: [Specific behaviors or skills that stood out]
AREAS FOR IMPROVEMENT: [Specific behaviors or gaps — be factual, not personal]
MISSED GOALS (if any): [What they committed to but didn't achieve — and context]
CONTEXT: [Any relevant circumstances — team changes, personal challenges, external factors]
RATING I AM GIVING: [Exceeds / Meets / Partially Meets / Does Not Meet Expectations]

Generate a performance review comment with:
1. OPENING (2 sentences): Overall assessment — consistent with the rating
2. STRENGTHS (2–3 bullets): Specific, evidence-based, behavior-focused
3. DEVELOPMENT AREAS (1–2 bullets): Constructive, future-focused, not character judgments
4. GOALS FOR NEXT PERIOD (2–3 SMART goals)
5. CLOSING (1 sentence): Forward-looking and motivating

Rules:
- Use specific examples I've provided — never invent examples
- Focus on behaviors and outcomes, not personality traits
- Use "SBI" language: Situation → Behavior → Impact
- No vague language: "great attitude" → "consistently supported teammates
  during deadline pressure by proactively sharing her expertise on [specific topic]"
- Development areas: always pair with a development path, not just a criticism
Length: 300–400 words
```

---

### 360-Degree Feedback Synthesis

```
I have received 360-degree feedback for [EMPLOYEE NAME] from [N] reviewers.
Here are the raw responses (anonymized): [PASTE ANONYMIZED FEEDBACK]

Synthesize this feedback into a structured development profile:

1. CONSISTENT STRENGTHS (themes that appeared across 3+ reviewers)
2. ISOLATED STRENGTHS (noted by 1–2 reviewers — still worth acknowledging)
3. CONSISTENT DEVELOPMENT AREAS (themes appearing across 3+ reviewers)
4. CONFLICTING FEEDBACK (areas where reviewers disagreed — note the tension)
5. BLIND SPOTS (potential gaps the employee may not be aware of)
6. DEVELOPMENT PRIORITIES (top 2 areas to focus on this year, with rationale)

Present this as a professional, balanced feedback summary I can share
with the employee. Anonymize and aggregate — never attribute specific
comments to specific reviewers.

Rules:
- Keep language constructive throughout
- Balance strengths and development areas proportionally
- Note context where feedback seems situational vs. consistent
```

---

## 17.5 HR Policy Documents

### Policy Draft Generator

```
Draft a [POLICY TYPE] policy for [COMPANY NAME], a [COMPANY DESCRIPTION].

Policy context:
- Why this policy is needed: [DESCRIBE THE SITUATION THAT PROMPTED IT]
- Key stakeholders: [WHO DOES THIS POLICY AFFECT?]
- Regulatory context: [ANY LAWS OR REGULATIONS THIS MUST ALIGN WITH]
- Company culture: [DESCRIBE — formal/flexible/startup/enterprise etc.]

Policy structure:
1. PURPOSE (2 sentences — why this policy exists)
2. SCOPE (who does this apply to? what situations?)
3. POLICY STATEMENT (core rules — numbered list, clear and unambiguous)
4. DEFINITIONS (any terms that need precise definition)
5. PROCESS / PROCEDURE (how to implement or follow this policy — step by step)
6. EMPLOYEE RESPONSIBILITIES
7. MANAGER RESPONSIBILITIES
8. CONSEQUENCES OF NON-COMPLIANCE
9. EXCEPTIONS (how to request and who approves)
10. REVIEW DATE (this policy will be reviewed by [DATE])
11. RELATED POLICIES

Tone: Professional and clear — employees must understand this without
a law degree. Avoid legalese where plain English works.

IMPORTANT: Flag [LEGAL REVIEW REQUIRED] next to any clause that involves
employment law, termination, discrimination, or benefits.
```

---

### Employee Communication Templates

**Offer Letter Opening:**
```
Write the opening section of an employment offer letter for:
Candidate: [NAME]
Role: [TITLE], [DEPARTMENT]
Start Date: [DATE]
Reporting to: [MANAGER TITLE]
Employment type: [Full-time / Part-time / Contract]

Opening (before the formal terms section):
- Warm congratulations that feel genuine, not formulaic
- Brief statement about what they bring and why we're excited
- 2-sentence preview of what they'll be working on
- Transition to formal terms with an inviting tone

Tone: Warm but professional. This is the first impression of their
employment experience — it should feel like a welcome, not a contract.
Under 150 words for this opening section.
```

**Onboarding Welcome Email:**
```
Write a welcome email for [EMPLOYEE NAME] joining as [ROLE] on [START DATE].

From: [MANAGER NAME], [MANAGER TITLE]
Company: [COMPANY NAME]

This email will be sent the day before they start. It should:
1. Express genuine excitement about them joining (specific — reference
   why we hired them, what we're looking forward to)
2. Set expectations for Day 1 (what to bring, where to go/login,
   who to look for, what time)
3. Preview Week 1 (3–4 things they can expect to experience)
4. Offer reassurance (it's okay to feel overwhelmed — here's how to reach out)
5. End with excitement, not formality

Tone: Warm team leader welcoming a new colleague.
Not HR department. Not generic.
Under 250 words.
```

**Difficult Announcement — Restructuring:**
```
Write a company-wide communication about an organizational restructuring.

Situation:
- What is changing: [DESCRIBE THE CHANGE]
- Effective date: [DATE]
- Who is affected: [WHICH TEAMS/ROLES]
- Reason for change: [BUSINESS RATIONALE — be honest but constructive]
- What support is available: [Severance / outplacement / transition support]
- What stays the same: [What employees can count on]

Communication principles for difficult news:
1. Lead with the news — don't make people read 3 paragraphs to find out
2. Acknowledge the human impact — don't be clinical
3. Explain the reason honestly — silence breeds speculation
4. State clearly what happens next and by when
5. Provide a channel for questions (named contact, not generic HR email)
6. End with genuine acknowledgment of the team, not hollow optimism

Tone: Authentic, empathetic, direct. Written by a human leader, not
a PR department. Under 400 words.
Flag [LEGAL REVIEW REQUIRED] before distribution.
```

---

## 17.6 Learning & Development Content

### Training Module Outline Generator

```
Design a training module for [COMPANY] employees on the topic of [TOPIC].

Audience: [WHO IS THIS FOR — role, experience level, prior knowledge]
Delivery format: [In-person / Virtual / Self-paced e-learning / Blended]
Duration: [TOTAL TIME]
Business need: [WHY IS THIS TRAINING NEEDED — what problem does it solve?]
Learning outcome: [What should participants be able to DO differently after?]

Module design:
1. LEARNING OBJECTIVES (3–5, starting with action verbs — measurable)
2. MODULE OUTLINE:
   For each section: title | duration | delivery method | key content | activity
3. KEY CONCEPTS to cover (prioritized by importance)
4. ENGAGEMENT ACTIVITIES (1 per 15 minutes of instruction)
5. KNOWLEDGE CHECKS (2–3 questions that test application, not recall)
6. ACTION COMMITMENT (what participants will do in the next 7 days)
7. RESOURCES TO SHARE (types of resources — you add the real links)

Design principle: Adult learning requires relevance, problem-solving,
and immediate application. Every 15 minutes needs an engagement moment.
```

---

## Hands-On Activities — Session 17

---

### Activity 17.1 — Job Description + Bias Audit

**Step 1:** Choose a real role from your organization (or use this scenario):
*"Data Analyst for a retail company in Mumbai, 3 years experience, reports to Head of Analytics."*

**Step 2:** Run the Job Description Generation Prompt.

**Step 3:** Run the Bias Audit Prompt on the output.

**Reflection:** How many bias flags were identified? Which surprised you? How did the inclusive alternatives change the language?

---

### Activity 17.2 — Interview Framework Build

**Objective:** Build a complete, ready-to-use interview framework.

Choose a role your team commonly hires for (or any role you know well).

Generate the full interview framework including:
- 5 competency-based question sets (behavioral + situational + probes)
- Green flags and red flags for each
- Scorecard format

**Test it:** Simulate conducting the interview with a colleague or by having AI play the role of a strong vs. weak candidate. Does the framework distinguish between them?

---

### Activity 17.3 — Performance Review Writing Practice

**Objective:** Practice writing specific, behavior-based performance review comments.

**Step 1:** Think of a real or fictional employee. Write bullet-point notes about their performance (3 strengths, 2 development areas, 1 key achievement).

**Step 2:** Run the Performance Review Comment Generator prompt.

**Step 3:** Evaluate: Are the comments specific (SBI format) or still vague? Is the development section constructive or just critical? Iterate once.

---

### Activity 17.4 — Policy Draft Exercise

**Choose one** and generate a full policy draft:
- Remote Work Policy for a hybrid-first organization
- AI Usage Policy for employees using AI tools at work
- Performance Improvement Plan (PIP) Process Policy

Run the Policy Draft Generator. Then flag every clause that needs legal review before actual implementation.

**Critical reflection:** Which sections would you NOT implement without legal counsel? What are the risks of using the draft without review?

---

## Revision Questions — Session 17

1. What is the golden rule for AI in HR and why is it important?
2. Name 5 appropriate AI uses in HR and 5 that require extreme caution.
3. What is gender coding in job descriptions and how does it affect hiring outcomes?
4. Describe the SBI format for performance review feedback. Give an example of a vague statement and its SBI-formatted equivalent.
5. What 8 sections should every HR policy document include?
6. Why must AI-generated interview questions be reviewed by a human before use?
7. Describe the principles for communicating difficult organizational news (restructuring, layoffs).
8. A manager wants to use AI to write their team's annual performance reviews entirely, then submit them. What concerns would you raise and what alternative approach would you recommend?

---

## Key Takeaways — Session 17

```
┌──────────────────────────────────────────────────────────────────────┐
│  SESSION 17 KEY TAKEAWAYS                                            │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ✓ AI in HR: assists human judgment, never replaces it              │
│    Every output reviewed by an HR professional before use           │
│                                                                      │
│  ✓ Job descriptions: inclusive language audit is mandatory —        │
│    gender, age, credential, cultural bias all detract talent        │
│                                                                      │
│  ✓ Interview frameworks: structured interviews reduce bias and      │
│    improve prediction accuracy vs. unstructured conversations       │
│                                                                      │
│  ✓ Performance reviews: SBI format (Situation → Behavior → Impact) │
│    AI provides language; all specific facts come from the manager   │
│                                                                      │
│  ✓ HR policies: always flag [LEGAL REVIEW REQUIRED] — AI generates │
│    structure and language; lawyers verify compliance                │
│                                                                      │
│  ✓ People communications: authentic, human tone matters most —     │
│    employees know the difference between genuine and templated      │
└──────────────────────────────────────────────────────────────────────┘
```

---

*Session 17 Complete → Proceed to Session 18: AI for Finance & Data Analysis*

---
*Prompt Engineering Certification Program | UpSkill Global Education Technologies Inc., Canada*
