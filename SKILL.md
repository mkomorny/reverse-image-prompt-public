---
name: reverse-image-prompt
description: Analyzes an uploaded image and generates an exhaustive, reconstruction-grade reverse prompt — so detailed that feeding it to any AI image generator (Midjourney, DALL·E, Stable Diffusion, Flux, Firefly, etc.) reproduces the image as closely as possible. Use when the user uploads an image and asks for a "reverse prompt", "image prompt", "recreate this image", "what prompt made this", "prompt this image", or similar. Also triggers when the user wants to extract a usable AI prompt from a photo, artwork, screenshot, or render.
---

# Reverse Image Prompt

Analyze the uploaded image and produce a reconstruction-grade prompt that another AI image model can use to reproduce it.

## Workflow

### 1. Deep Visual Analysis

Before writing a single word of the prompt, mentally scan the image across all dimensions. Read `references/prompt-dimensions.md` — it contains the full taxonomy of every dimension to analyze. Work through every section systematically.

### 2. Internal Confidence Audit

After scanning, rate each dimension 1–5 on how confidently you can describe it. Dimensions rated 3 or below need extra care: be more specific and use hedging phrases like "appears to be" or "reminiscent of" only when uncertain — never drop the dimension entirely.

### 3. Build the Reconstruction Prompt

Output the final prompt as a **single continuous block of comma-separated descriptors** (no bullet points, no section headers in the output) followed by a **structured breakdown section** below it.

#### Output Format

```
## Reconstruction Prompt

[Full prompt text — dense, comma-separated, ordered from macro to micro. ~200–500 words.]

---

## Prompt Breakdown

### Medium & Style
...
### Subject
...
### Composition & Framing
...
### Lighting
...
### Color & Tone
...
### Texture & Detail
...
### Atmosphere & Mood
...
### Technical / Model Tags
...
```

### 4. Prompt Ordering (Macro → Micro)

Structure the prompt in this order for maximum generator compatibility:

1. **Medium/style opener** — `digital art`, `oil painting`, `photograph`, `3D render`, etc.
2. **Subject core** — what is it, who/what is the main subject
3. **Subject details** — pose, expression, clothing, features
4. **Environment/setting** — where, what surrounds the subject
5. **Composition** — framing, angle, depth, rule-of-thirds placement
6. **Lighting** — source, quality, direction, shadows, highlights
7. **Color palette** — dominant hues, saturation, temperature
8. **Texture & detail level** — surface qualities, material rendering
9. **Atmosphere & mood** — emotional tone, weather, time of day
10. **Technical/model tags** — aspect ratio, quality boosters, style references

### 5. Platform Variants (optional)

If the user asks for platform-specific prompts, output variants optimized for each:

- **Midjourney**: include `--ar`, `--style`, `--v` flags; use `::` weighting for key subjects
- **Stable Diffusion / Flux**: separate positive and negative prompts; include CFG guidance (e.g., `CFG 7`)
- **DALL·E**: natural language style; avoid unsupported syntax
- **Firefly**: descriptive, brand-safe phrasing

If the user does not specify a platform, produce a **universal prompt** compatible with any generator.

### 6. Quality Rules

- **Never truncate** — a missing detail is a missed reproduction opportunity
- **Use artist/style references** only when clearly identifiable (e.g., "in the style of Moebius", "painterly like Alphonse Mucha")
- **Quantify everything possible**: angles in degrees, color as hex or named values, sizes as relative proportions
- **Preserve negatives**: if something is notably *absent* (no people, no text, monochromatic), state it
- **Capture what makes it unique**: the one detail that separates this image from a generic version of itself
