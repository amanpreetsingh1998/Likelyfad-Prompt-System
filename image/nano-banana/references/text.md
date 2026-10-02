# Text and typography

> From the Nano Banana Pro Prompting Guide v2.0 (April 2026), kept as written. Part numbers refer to that guide; the skill maps each part to a file (see SKILL.md, "What to read, and when").

# Part 4 — Text and Typography

Text rendering is Pro's flagship capability upgrade. What used to be a universal weakness of image models is now a headline strength. This section replaces v1 Part 1.7 in full.

## 4.1 The non-negotiable rules

### Rule 1 — Wrap all desired text in quotes

Always. Every time. `"Happy Birthday"`, `"URBAN EXPLORER"`, `'3分钟搞定!'`, `"Inspired by Libre"`. Quotes signal "render this string verbatim" to the model. Unquoted text is treated as a general description of what the scene should contain, which leads to approximate spellings and invented words.

### Rule 2 — Specify the font descriptively

Font names work loosely ("Impact," "Century Gothic," "Brush Script") but descriptive language works more reliably. Recommended descriptors:

- **Weight** — thin, light, regular, medium, bold, heavy, extra-bold
- **Classification** — serif, sans-serif, slab serif, monospace, script, display
- **Character** — clean, geometric, humanist, condensed, expanded, rounded, stencil, distressed
- **Mood (rarely needed but sometimes useful)** — elegant, playful, industrial, retro, futuristic

**Example formulations that work:**
- "bold, white, geometric sans-serif, all caps"
- "flowing elegant brush script in cream"
- "heavy blocky condensed sans-serif, black with white outline"
- "thin minimalist serif, charcoal gray"

### Rule 3 — Specify placement spatially

"Top center," "bottom left," "centered above the subject," "vertical along the left edge," "overlaying the top third." Spatial language is more reliable than layout descriptors like "hero text" or "headline position."

### Rule 4 — Specify color explicitly

Pro doesn't infer text color from context well. State it: "bright red," "white with black drop shadow," "deep navy," "gold foil finish."

## 4.2 The text-first hack (Google-endorsed)

For any prompt where text accuracy is critical and the string is long, non-trivial, or contains unusual punctuation:

1. First, in a separate turn, have Gemini generate or verify the exact copy you want
2. Then ask for the image with that exact text wrapped in quotes

This reduces spelling errors on long strings significantly. It's how Google's DevRel team generates their own demo posters. Don't skip this step for anything longer than a tagline.

## 4.3 Multi-font hierarchy control

Pro can render three or more distinct fonts in a single image with correct hierarchy. The key is to label each text element explicitly.

**Canonical Google example (verbatim-worthy template):**

> A high-end, glossy commercial beauty shot of a sleek, minimalist nude-colored face moisturizer jar resting on a warm studio background. The lighting is soft and radiant. Next to the product, render three lines of text with the following exact styling:
>
> - For the top line, the word **"GLOW"** in a flowing, elegant Brush Script font.
> - For the middle line, the text **"10% OFF"** in a heavy, blocky Impact font.
> - For the bottom line, the text **"Your First Order"** in a thin, minimalist Century Gothic font.

Adapt this structure for any multi-font poster or ad.

## 4.4 Long-string text (now works)

Paragraph-length text renders cleanly in Pro where it failed in the original Nano Banana. The classic proof example — *"How much wood would a woodchuck chuck if a woodchuck could chuck wood"* rendered in wood chips — works. You can use Pro for:

- Full testimonial quotes on a background
- Pull-quote ad creative
- Product packaging with ingredient lists
- Event posters with venue details, dates, fine print
- Comic panels with speech bubbles

**Practical limit:** around 150–200 words in a single image, and the density affects legibility. For dense-text applications, use higher resolution (2K or 4K output — see Part 10).

## 4.5 Multilingual rendering (10+ languages)

Pro natively renders text in over ten languages including Korean, Arabic (right-to-left), Japanese (Kanji, Hiragana, Katakana), Chinese (Simplified and Traditional), Hebrew, Cyrillic, Devanagari (Hindi), Thai, Greek, and most European languages.

**Usage:**
- Prompt in English, specify target-language output: *"Render the tagline in Italian: 'Il profumo che cambia tutto'"*
- Or prompt natively in the target language
- Right-to-left languages (Arabic, Hebrew) are rendered with correct text direction

**For your dupe perfume project specifically:** this handles the German ("Riecht wie...") and Italian ("No. XXX - Ispirato alle note di...") storefront variants cleanly. One base creative can be text-translated for all four brands without re-shooting.

## 4.6 Translation inside existing images (new capability)

You can upload an existing image and ask Pro to translate the text inside it while preserving layout, font style, and positioning. This is genuinely new and valuable for multi-market ad production:

**Prompt pattern:**
> Translate all the text in this image from English to Italian, preserving the exact font style, size, positioning, and color. Keep everything else in the image unchanged.

**When this works:** clear, modern fonts on solid backgrounds. Layouts where text fits in defined regions.

**When this breaks:** heavily stylized text, text that follows a complex path or warp, text integrated into textures (e.g., embroidered or carved), and languages with very different character widths (long German words in a narrow English layout may overflow — verify output).

## 4.7 Text on complex surfaces

Pro can render text on non-flat surfaces with correct perspective and deformation:

- On a curved bottle label (follows cylinder geometry)
- On a wrinkled paper (follows folds)
- On a reflective surface (correct specular behavior)
- On fabric (follows drape)
- Engraved into wood or metal (correct depth shadows)
- As a neon sign (with glow and reflection)

For brand-exact product mockups, specify the surface geometry: "wrap the text around the cylinder of the bottle," "emboss the text into the matte leather," "render as neon tubing mounted on a brick wall."

## 4.8 What still fails in text rendering

Honest documentation, since production requires knowing the limits:

- **Small text under roughly 12px equivalent** — degrades into gibberish
- **Extreme stylization** (heavy warping, distressed effects layered on top of text) — sometimes breaks letterforms
- **Very specific typefaces by brand name** — "Helvetica Neue Bold 75" gets approximated; use descriptive language and verify
- **Cultural/idiomatic nuance in non-English text** — the letters render correctly, but occasionally the phrasing reads as direct translation rather than native idiom; always have a native speaker proof before shipping
- **Exact brand kerning** — kerning is approximately correct, not pixel-perfect. For logo-exact output, composite the logo in post

## 4.9 Quick-reference checklist for text-heavy work

- Every text string wrapped in quotes
- Font described (weight + classification + character)
- Placement specified spatially
- Color stated explicitly
- For multi-font: each line labeled separately
- For long strings: copy verified via text-first hack
- For multilingual: target language stated
- Output resolution sufficient for legibility (2K minimum for dense text)
- Post-pass plan for any brand-exact typography (logo comp in Photoshop if needed)

---

