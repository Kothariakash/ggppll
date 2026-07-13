# Session 21: AI Image Generation
## Professional Generative AI Applications Certification
#### UpSkill Global Education Technologies Inc., Canada

---

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  MODULE 5 — CREATIVE AI & AUTOMATION                                         │
│  SESSION 21 of 30  |  1 Hour  |  35% Theory + 65% Hands-On                 │
│                                                                              │
│  "A professional doesn't need to be a designer to create design-quality     │
│   visuals. They need to know how to describe what they want."                │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Learning Objectives

By the end of Session 21, you will be able to:

- Explain how AI image generation works (diffusion models, text-to-image)
- Write effective image prompts using the VACS framework
- Use DALL-E 3, Midjourney, and Adobe Firefly for professional use cases
- Apply negative prompting and style references to control output quality
- Apply copyright, IP, and ethical guidelines to AI-generated images
- Use AI image generation for 6 practical business applications

---

## 1. How AI Image Generation Works

### 1.1 The Technology Behind the Magic

AI image generators use a technology called **diffusion models**. Unlike text AI (which predicts the next word), image AI starts with random noise and progressively "de-noises" it guided by the text prompt until a coherent image emerges.

```
HOW DIFFUSION MODELS WORK:

Step 1: ENCODE THE PROMPT
  "A professional woman in a modern office, natural light, smiling"
  → AI converts text to mathematical vectors (embeddings)

Step 2: START WITH NOISE
  AI begins with a completely random image (pure visual noise)

Step 3: PROGRESSIVE DE-NOISING (50–100 steps)
  Step 1:  Blurry, barely distinguishable shapes
  Step 25: Rough forms — clearly an indoor scene with a figure
  Step 50: Clear image — recognizable person in office environment
  Step 100: Final polished image matching prompt description

Step 4: UPSCALING (in high-quality models)
  Final image sharpened and upscaled to full resolution
```

### 1.2 Key AI Image Generation Terms

| Term | Definition |
|------|-----------|
| **Text-to-Image** | Generating an image from a text description |
| **Image-to-Image** | Transforming an existing image based on a text prompt |
| **Inpainting** | Editing a specific region of an image using AI |
| **Outpainting** | Extending an image beyond its original boundaries |
| **Style Transfer** | Applying the visual style of a reference image to new content |
| **Seed** | A number that determines the starting noise — same seed = reproducible result |
| **Steps** | Number of de-noising iterations more steps = higher quality (up to a limit) |
| **CFG Scale** | How closely the AI follows the prompt vs. being creative (Classifier-Free Guidance) |
| **Negative Prompt** | Words describing what you do NOT want in the image |

---

## 2. Leading AI Image Tools

### 2.1 Tool Comparison

| Tool | Best For | Quality | Cost | Access |
|------|---------|---------|------|--------|
| **DALL-E 3** (OpenAI) | Business use, content-safe, natural images | Excellent | Included in ChatGPT+ / API | chat.openai.com |
| **Midjourney** | Artistic, photorealistic, high-detail | Best-in-class | $10–$120/mo | Discord + web |
| **Adobe Firefly** | Commercial use, brand assets, licensed safe | Very Good | Adobe CC subscription | firefly.adobe.com |
| **Stable Diffusion** | Custom, local, fine-tuned models | Variable | Free (open source) | Local or Replicate |
| **Canva AI** | Quick marketing assets | Good | Free tier + Canva Pro | canva.com |
| **Ideogram** | Text in images (logos, quotes) | Good for text | Free tier | ideogram.ai |
| **Leonardo.ai** | Product photography, game assets | Very Good | Free tier | leonardo.ai |

### 2.2 Choosing the Right Tool for Your Use Case

```
USE CASE → RECOMMENDED TOOL:

Marketing visuals and social media:
  → Canva AI (easy, brand-consistent) or DALL-E 3 (high quality)

Product photography and e-commerce:
  → Leonardo.ai or Midjourney (photorealistic quality)

Brand-safe commercial assets:
  → Adobe Firefly (trained on licensed content — commercial use safe)

Artistic and editorial visuals:
  → Midjourney (unmatched artistic quality)

Presentations and documents:
  → DALL-E 3 in ChatGPT (fastest workflow)

Images containing text (logos, infographics):
  → Ideogram (best AI text rendering)

Technical diagrams and UI mockups:
  → DALL-E 3 + Canva editing
```

---

## 3. The VACS Image Prompting Framework

### 3.1 The Framework

Great image prompts work differently from text prompts — they are more descriptive and visual. VACS covers the four dimensions of a strong image prompt:

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  THE VACS IMAGE PROMPTING FRAMEWORK                                          │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  V — VISUAL SUBJECT    What is in the image? Who/what is the main focus?    │
│                        Be specific: not "a person" but "a South Asian       │
│                        woman in her 30s, wearing a navy blazer"             │
│                                                                              │
│  A — ATMOSPHERE        Mood, lighting, time of day, color palette           │
│                        "warm golden hour lighting," "cool blue tones,"      │
│                        "moody and cinematic," "bright and airy"             │
│                                                                              │
│  C — COMPOSITION       Camera angle, framing, perspective, depth            │
│                        "close-up portrait," "wide establishing shot,"       │
│                        "bird's eye view," "shallow depth of field"          │
│                                                                              │
│  S — STYLE             Visual style, art movement, rendering quality         │
│                        "photorealistic," "flat illustration," "watercolor," │
│                        "corporate photography," "cinematic film still"      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### 3.2 Applying VACS — Before and After

**Weak Prompt:**
```
A businesswoman in an office
```
*Result: Generic stock photo aesthetic — could be any tool, any company, forgettable.*

**VACS Prompt:**
```
[V] A South Asian woman in her early 30s, wearing a navy blazer over a white shirt,
sitting at a minimalist white desk with a laptop, looking confident and focused.

[A] Warm natural light from a large window to her left, creating soft shadows.
Clean, modern aesthetic. Muted color palette: white, grey, navy accents.

[C] Three-quarter angle, medium shot, slight bokeh background to focus on subject.
The background shows a blurred open-plan modern office.

[S] High-quality corporate photography. Photorealistic. DSLR quality.
Similar to LinkedIn professional photography or McKinsey annual report imagery.
```
*Result: A polished, brand-appropriate professional image — stock-photo quality.*

---

### 3.3 Style Reference Keywords

**Photography styles:**
```
• Corporate photography / editorial photography
• Documentary / reportage style
• Fashion photography
• Product photography on white background
• Lifestyle photography (natural, candid feel)
• Architectural photography (clean, geometric)
• Macro photography (extreme close-up detail)
```

**Art and illustration styles:**
```
• Flat illustration / flat design (clean vectors, no shadows)
• Isometric illustration (3D geometric style popular in tech)
• Watercolor illustration (soft, flowing, hand-crafted feel)
• Line art (clean black lines, minimal or no fill)
• Infographic illustration
• Hand-drawn sketch style
• Minimalist icon design
```

**Cinematic and editorial styles:**
```
• Cinematic film still (wide aspect ratio, dramatic lighting)
• Magazine editorial (high contrast, sophisticated)
• Advertising campaign visual (perfect lighting, intentional composition)
• Concept art (slightly fantastical, detailed environment)
```

---

## 4. Negative Prompting

### 4.1 What Negative Prompts Do

Negative prompts tell the AI what to EXCLUDE from the image. They are essential for avoiding the common AI image problems:

```
COMMON AI IMAGE PROBLEMS + NEGATIVE PROMPTS TO FIX THEM:

Problem: Extra fingers, distorted hands
Negative: "deformed hands, extra fingers, mutated hands, poorly drawn hands"

Problem: Unrealistic text in image
Negative: "text, watermark, labels, writing, typography, letters"

Problem: Blurry or low quality
Negative: "blurry, out of focus, low quality, low resolution, pixelated, grainy"

Problem: Stock photo clichés
Negative: "stock photo, overused, cheesy, fake smile, unnatural pose"

Problem: Distracting backgrounds
Negative: "cluttered background, busy background, distracting elements"

Problem: Wrong lighting
Negative: "harsh shadows, overexposed, underexposed, unnatural lighting"

Problem: Cartoon-like when you want realism
Negative: "cartoon, anime, illustration, drawing, painting"
```

### 4.2 The Standard Negative Prompt Template

For most professional uses, start with this baseline negative prompt:

```
STANDARD NEGATIVE PROMPT (copy-paste for professional images):

Negative: blurry, low quality, pixelated, distorted, deformed, extra limbs,
extra fingers, poorly drawn face, bad anatomy, watermark, text, logo,
signature, overexposed, underexposed, grainy, noise, artifacts, flat,
uninteresting composition, stock photo cliché, fake smile, unnatural pose
```

---

## 5. Professional Business Applications

### 5.1 Marketing and Social Media Visuals

```
PROMPT TEMPLATE — Social Media Hero Image:

[V] [PRODUCT / SERVICE / CONCEPT] shown in a lifestyle context.
[DESCRIBE WHO IS USING IT OR THE SETTING]

[A] [MOOD — warm and inviting / bright and energetic / calm and minimal]
Color palette: [YOUR BRAND COLORS OR AESTHETIC]

[C] [FRAMING — square crop for Instagram / 16:9 for LinkedIn / portrait for Stories]
[COMPOSITION NOTES]

[S] Professional lifestyle photography. Brand campaign quality.
Suitable for [PLATFORM] advertising.

Negative: text, watermark, logos, blurry, low quality, cheesy stock photo aesthetic
```

**Example — for a healthy food brand:**
```
A young Indian woman (late 20s) holding a bowl of colorful salad with quinoa,
chickpeas, and roasted vegetables. She is standing in a bright modern kitchen,
laughing naturally, not posed.

Warm morning light from window. Clean white kitchen background.
Colors: greens, yellows, oranges of the food against white.

Medium shot, slightly from the side. Shallow depth of field on the food.

High-quality lifestyle photography. Editorial quality.
Think: Instagram food brand campaign.

Negative: text, watermark, artificial lighting, fake smile, cluttered background,
low quality, blurry, cheesy stock photo
```

### 5.2 Presentation Backgrounds and Icons

```
PROMPT TEMPLATE — Presentation Background:

Abstract [THEME — data / growth / connection / innovation / sustainability] concept.
[COLOR PALETTE matching brand e.g., "blues and whites with subtle gradients"]
Minimal, clean design no text, no recognizable objects.
Suitable as a PowerPoint or Keynote slide background.
Resolution: high quality, sharp edges.
Style: modern corporate graphic design, flat and geometric.

Negative: text, words, letters, numbers, people, faces, cluttered, busy, low quality
```

```
PROMPT TEMPLATE — Custom Icon Set:

Set of 6 flat design icons representing: [LIST YOUR CONCEPTS]
Style: modern flat vector illustration, consistent line weight.
Color: [YOUR BRAND COLOR] monochrome or [2-TONE SCHEME].
Background: white / transparent.
Each icon simple enough to read at 32px.

Negative: 3D effects, shadows, gradients, inconsistent style, text
```

### 5.3 Product Visualization

```
PROMPT TEMPLATE — Product Photography:

[PRODUCT NAME AND DESCRIPTION] on [BACKGROUND — white studio / lifestyle context].
[SPECIFIC PRODUCT DETAILS — color, material, key features visible]

Studio product photography setup: softbox lighting, pure white background.
Product centered, sharp focus, slight shadow beneath for depth.
Professional e-commerce photography quality.
No props unless: [SPECIFY ANY PROPS]

Negative: background clutter, blurry, shadows on white, text, watermark,
poor lighting, distorted product shape
```

### 5.4 Team / People Imagery for Documents

```
PROMPT TEMPLATE — Professional Diversity Images:

[DESCRIPTION OF SCENE — team meeting, professional at work, collaboration]

Diversity considerations: [DESCRIBE DIVERSITY — gender, ethnicity, age range]
Clothing: [PROFESSIONAL STANDARD — formal / business casual / industry-specific]
Setting: [MODERN OFFICE / OUTDOOR / SPECIFIC INDUSTRY SETTING]

[ATMOSPHERE — natural light / bright and collaborative / serious and focused]
[COMPOSITION — group shot / individual portrait / in-action candid]

Corporate photography. Authentic, not staged-looking.
Suitable for company website, annual report, recruitment materials.

Negative: fake poses, staged smiles, homogeneous group, old-fashioned office,
text, watermark, low quality, stock photo clichés
```

---

## 6. Copyright, IP, and Ethical Considerations

### 6.1 Copyright in AI-Generated Images

```
CURRENT LEGAL LANDSCAPE (2024):

IN MOST JURISDICTIONS:
  ✓ AI-generated images are not automatically copyrighted
    (because there is no human author)
  ✓ The human who writes the prompt may claim some rights
    (this varies by jurisdiction and is still being tested in courts)
  ✓ Images generated with Adobe Firefly are commercially safe
    (trained on licensed Adobe Stock content)

RISKS TO UNDERSTAND:
  ⚠ Some AI tools (Midjourney, early Stable Diffusion) were trained on
    web-scraped images without explicit licenses ongoing legal debate
  ⚠ Generating images "in the style of a living artist" is legally grey
    and ethically questionable
  ⚠ DALL-E 3 has content policies that prevent generating images that
    reproduce recognizable copyrighted characters or artwork

SAFEST APPROACH FOR COMMERCIAL USE:
  → Use Adobe Firefly (licensed training data, commercial use explicitly safe)
  → Use DALL-E 3 (OpenAI's commercial use terms cover API and ChatGPT outputs)
  → Avoid: asking for "in the style of [specific living artist]"
  → Avoid: generating recognizable brand logos, characters, or trademarked imagery
```

### 6.2 Ethical Guidelines for AI Images

```
ABSOLUTE LIMITS (never generate):
  ✗ Realistic images of real, identifiable people without consent
  ✗ Deepfake-style images that could be mistaken for real photographs
  ✗ Images designed to deceive (fake news, false events)
  ✗ Images that perpetuate harmful stereotypes about any group
  ✗ Any content involving minors in inappropriate contexts

PROFESSIONAL RESPONSIBILITY:
  ✓ Label AI-generated images in contexts where the audience would assume
    real photography (journalism, product listings, professional profiles)
  ✓ Consider representation: AI default outputs often reflect Western,
    non-diverse aesthetics actively prompt for diversity
  ✓ Do not use AI images to replace photographers without considering
    the economic impact on creative professionals
```

### 6.3 Representation in AI Images

One of the most important professional considerations: AI image generators have biases in their default outputs certain genders, ethnicities, ages, and body types appear more frequently without explicit prompting.

**Actively prompt for representation:**
```
Instead of: "a doctor in a hospital"
Write: "a female South Asian doctor in her 40s in a modern hospital"

Instead of: "a team meeting"
Write: "a diverse team of 5 professionals (mixed gender, ethnicity, age 25–55)
in a collaborative meeting. Not all are wearing suits business casual."

Instead of: "a CEO"
Write: "a Black male CEO in his 50s, confident and well-dressed,
in a modern corner office"
```

---

## 7. Real-World Example: Canva and DALL-E 3 at Marketing Scale

**Company:** A 12-person D2C health and wellness brand (₹15 Crore annual revenue)

**The Challenge:**
The brand needed 200+ unique images per year for:
- Product photography (seasonal variations)
- Social media content (Instagram, Pinterest, Facebook)
- Email marketing headers
- Blog post hero images
- Website banners

Traditional approach: ₹3–5 Lakhs/year on photography + design freelancers. 2-week lead time per shoot.

**The AI Implementation:**

```
TOOL STACK:
  DALL-E 3 (via ChatGPT+): Campaign concepts and hero images
  Canva AI: Quick social media variations and templates
  Adobe Firefly: Commercial-use-safe product lifestyle images

WORKFLOW:
  1. Content brief (15 min): Describe campaign, mood, product, audience
  2. DALL-E 3 generation (10 min): 3–5 hero image variations
  3. Human selection + Canva edit (20 min): Pick best, add text, resize
  4. Batch generation (30 min): Canva AI generates 20+ social variations
  5. Approval and scheduling (15 min): Review, minor edits, schedule

TOTAL TIME: 90 minutes for a full campaign set (vs. 2-week photography process)
```

**Results:**
- Photography + design spend: ₹3.5 Lakhs → ₹60K/year (Canva Pro + ChatGPT+)
- Lead time: 2 weeks → 2 hours
- Content volume: 200 → 600+ images/year
- Social media engagement: +28% (more fresh content = higher algorithmic reach)
- Brand consistency: improved (AI follows the same style prompt every time)

**What changed for the design team:**
The one in-house designer stopped spending time on routine asset creation and moved to: brand strategy, campaign concept development, higher-level creative direction, and overseeing AI-generated batches. Role became more strategic, not eliminated.

---

## 8. Hands-On Lab 21: Image Generation Practical

**Objective:** Generate professional-quality images for 3 business use cases  
**Duration:** 25 minutes  
**Tools:** DALL-E 3 (via ChatGPT+) or Adobe Firefly (free at firefly.adobe.com)

---

### Task 1: Professional Person / Team Image (8 minutes)

Create an image for a company website "About Us" or "Team" page.

Build a VACS prompt:
- V: Describe a professional person or small team (include diversity specifics)
- A: Warm, natural, authentic atmosphere
- C: Medium shot, slightly candid composition
- S: Corporate lifestyle photography, website quality

Generate the image. Evaluate:
- Does it feel authentic or staged?
- Is the diversity you specified represented?
- Would you use this professionally?

---

### Task 2: Marketing Visual (8 minutes)

Choose a product, service, or concept relevant to your interests or career.

Build a VACS prompt for a social media hero image:
- V: The product/service in a lifestyle context
- A: Mood matching your target audience's aspiration
- C: Appropriate for your chosen platform (Instagram square / LinkedIn landscape)
- S: High-quality marketing photography

Also include: Standard Negative Prompt template.

Generate 2–3 variations (change the atmosphere or composition slightly each time). Which is most effective and why?

---

### Task 3: Presentation Background or Icon (9 minutes)

**Option A:** Create an abstract presentation background for a slide deck on [TOPIC OF YOUR CHOICE].
Use the Presentation Background prompt template.

**Option B:** Create a set of 4 icons representing key concepts from your work or studies.
Use the Custom Icon Set prompt template.

Evaluate: Would this fit into a professional document you'd present to a manager or client?

---

### Lab Evaluation Rubric

| Deliverable | Marks |
|-------------|-------|
| Task 1: VACS prompt written + image generated + 3-point evaluation | 3 |
| Task 2: VACS prompt with negative prompting + 2 variations + comparison | 4 |
| Task 3: Background or icon set generated + professional use assessment | 3 |
| **Total** | **10** |

---

## 9. Interview Questions — Session 21

**Q1:** *"How would you use AI image generation in a professional context?"*

**Strong Answer:**
"I use AI image generation for three main professional purposes. First, marketing and social media visuals using DALL-E 3 or Canva AI with carefully written VACS prompts (Visual subject, Atmosphere, Composition, Style) that specify exactly the mood, framing, and style I want. Second, presentation assets custom backgrounds and icons that are consistent with a brand's visual identity, generated in minutes rather than sourced from stock libraries. Third, product visualization lifestyle images showing products in realistic contexts. I always include negative prompts to avoid common AI image problems like distorted faces or generic stock photo aesthetics. For commercial use, I use Adobe Firefly specifically because it's trained on licensed content. I apply representation principles actively explicitly describing diverse subjects rather than relying on AI defaults."

---

## 10. Revision Questions — Session 21

1. How do diffusion models generate images? Describe the 4 steps in the process.
2. What does VACS stand for in image prompting? Give an example of each component for a corporate team meeting image.
3. What is a negative prompt and why is it important? Give 5 specific negative prompt terms and the problems they prevent.
4. Compare DALL-E 3, Midjourney, and Adobe Firefly. Which would you choose for commercial brand assets and why?
5. What are the current copyright implications of AI-generated images? What is the safest approach for commercial use?
6. What are 5 absolute ethical limits in AI image generation?
7. Why must representation be actively prompted in AI images rather than relying on defaults?
8. In the D2C brand case study, what happened to the designer's role after AI image generation was introduced? What does this tell us about AI's impact on creative jobs?

---

## 11. Key Terminology — Session 21

| Term | Definition |
|------|-----------|
| **Diffusion Model** | An AI architecture that generates images by progressively removing noise from a random starting point |
| **Text-to-Image** | Generating an image from a natural language description |
| **VACS Framework** | Visual subject, Atmosphere, Composition, Style a framework for image prompt writing |
| **Negative Prompt** | Text describing what should be EXCLUDED from the generated image |
| **Seed** | A numerical value that determines the starting noise state same seed produces reproducible results |
| **Inpainting** | AI-powered editing of a specific region within an existing image |
| **Style Reference** | A description or example image used to guide the visual style of AI output |
| **Adobe Firefly** | Adobe's AI image generation tool trained on licensed content safe for commercial use |
| **CFG Scale** | Classifier-Free Guidance controls how closely AI follows the prompt vs. creative freedom |

---

## 12. Summary

```
┌──────────────────────────────────────────────────────────────────────────────┐
│  SESSION 21 SUMMARY — WHAT TO REMEMBER                                       │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ✓  Diffusion models: noise → de-noising → polished image (50–100 steps)   │
│  ✓  VACS: Visual subject + Atmosphere + Composition + Style                 │
│  ✓  Negative prompts: essential for controlling quality and avoiding        │
│     common AI artifacts (hands, blurriness, stock clichés)                  │
│  ✓  Tool choice: Firefly for commercial safety; Midjourney for art quality; │
│     DALL-E 3 for speed and integration; Canva AI for marketing workflows   │
│  ✓  Copyright: Firefly is safest for commercial; avoid artist names         │
│  ✓  Ethics: no real people, no deepfakes, label AI images when needed       │
│  ✓  Representation: always explicitly prompt for diversity                  │
│  ✓  D2C brand: ₹3.5L → ₹60K/year; 2 weeks → 2 hours; 3x more content     │
│                                                                              │
│  NEXT SESSION:                                                               │
│  Session 22 — AI for Video, Audio & Multimedia                              │
│  (AI video generation, voiceovers, podcast editing, background music,      │
│   and building multimedia content workflows)                                 │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

*Session 21 Complete | Next: Session 22 — AI for Video, Audio & Multimedia*
*Professional Generative AI Applications Certification | UpSkill Global Education Technologies Inc., Canada*
