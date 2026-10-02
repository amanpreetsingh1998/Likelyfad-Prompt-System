# Identity, character consistency and reference roles

> From the Nano Banana Pro Prompting Guide v2.0 (April 2026), kept as written. Part numbers refer to that guide; the skill maps each part to a file (see SKILL.md, "What to read, and when").

## House rules for character sheets (Likelyfad, added 2026-10-02)
- **Full character shown in the video → a 5-view FULL-BODY sheet** (front, 3/4 front, profile, 3/4 back, back), 16:9, one canvas, neutral seamless background, no text.
- **Only chest-up shown (a talking model framed from the stomach up) → a 3-view sheet** is enough.
- **Building a cast from a script, a Pixar / high-fidelity / realistic / UGC character, or a before/after transformation** → use `image/character-casting/` instead. It carries the casting theory (unique, recognisable, age-true people) and the transformation workflow.
- **Transformation edits are the one exception to "preservation contracts" below.** For a weight-loss or before/after stage, a blanket "keep everything the same" lock suppresses the change. Follow the character-casting transition rules.

# Part 5 — Identity and Character Consistency

This section expands v1 Part 1.3 and Part 2.45 significantly. Character consistency is central to AI-influencer production, and Pro's new capabilities change the workflow meaningfully.

## 5.1 The 14-reference-image ceiling

Pro accepts up to 14 input images, distributed approximately as:
- 6 high-fidelity object/product reference slots
- 5 human identity/face reference slots
- 3 environmental, style, or auxiliary slots

**Community-validated sweet spot: 3–5 references total.** More references than this introduces noise and inconsistency rather than improving output. The model can't reconcile six different angles of the same face as well as it can reconcile three.

**When to use more vs. fewer:**
- Simple product shot: 1 reference (the product)
- Product in a styled scene: 2–3 references (product + environment mood + optional style anchor)
- Identity-locked influencer shot: 1 character sheet + 1 outfit reference = 2 refs
- Complex composite (two people + location + style): 4–5 refs, with clear role assignment (see Part 6)

## 5.2 The character sheet trick

**The problem v1 didn't solve:** uploading front, 3/4, and side views of the same person as three separate images makes the model reconcile three "people" and produces blended results.

**The solution the community discovered:** generate a single reference image containing all views on one canvas. Upload that one image.

**Workflow:**
1. In an initial session, generate your character once: "a 28-year-old woman with shoulder-length auburn hair, freckles, green eyes, wearing a neutral gray crew neck. Studio lighting, neutral gray background."
2. Then ask: "Now show the same woman in a character sheet layout: front view center, 3/4 left view on the left, 3/4 right view on the right, profile left on the far left, profile right on the far right. All five views on a single image, neutral gray background, consistent lighting."
3. Save that image. This is your canonical character reference.
4. For every future session, upload this one image and reference it: "Use the character in the attached reference. Place her in [new scene]."

This produces dramatically more consistent identity across sessions than any other technique.

## 5.3 Session-based memory vs. character sheet

These are two different tools for two different jobs:

- **Session memory** (Part 1.5) — for consistent identity within a single production session, across multiple turns. Free. Degrades after 15–20 turns.
- **Character sheet** (Part 5.2) — for consistent identity across sessions, across days, across team members. Durable. Always requires re-uploading.

Use both together for ongoing AI-influencer production: character sheet to seed each session, session memory to iterate within it.

## 5.4 Preservation-contract phrasing (the language that actually works)

Specific phrasing matters a lot for identity preservation. Community testing has validated these formulations:

**Strong (use these):**
- *"Maintain the exact [logo placement / colorway / facial features] of the reference."*
- *"Keep the person's facial features exactly the same as Image 1."*
- *"Preserve the character's identity: bone structure, skin tone, hair color, eye color, facial proportions."*
- *"Identity-lock to Image A."*

**Weak (avoid):**
- *"Use this as reference."* — too vague
- *"Similar to the reference."* — invites drift
- *"Inspired by the reference."* — explicitly permits drift
- *"Don't change the face."* — buried in prose, gets deprioritized

**Why this matters:** v1 correctly identified that identity preservation has to be high-priority. v2 adds the specific phrasing that the community has stress-tested.

## 5.5 Face-lock negatives (narrow use)

Despite negatives being largely deprecated (Part 8), there is one scenario where they still earn their place: identity-lock insurance for production AI-influencer work.

The Sider.ai character-consistency cheat sheet validates this negative list for faces:

> Avoid: age change, face warp, asymmetrical eyes, extra fingers, logo distortion, text artifacts, blended faces, identity drift.

Use this block only when identity fidelity is critical and only as a narrow insurance policy alongside explicit positive preservation contracts. Don't use it as a general prompting layer.

## 5.6 Age, gender, expression stability

**Age drift** is a common failure — the model tends to age subjects 5–10 years across edits. Mitigate by restating age in preservation: *"Preserve age: late 20s."*

**Gender presentation** — similar drift. Restate: *"Preserve gender presentation: woman."*

**Expression control under identity lock** — you can change expression without breaking identity: *"Preserve facial features. Change expression from neutral to warm smile, eyes slightly crinkled."*

## 5.7 Multi-character scenes

For two or more characters, give each their own paragraph. Assign explicit positions.

**Example:**

```
Character A (left side of frame): 28-year-old woman, shoulder-length auburn hair, wearing cream linen button-down.
Character B (right side of frame): 32-year-old man, short dark brown hair, five o'clock shadow, wearing navy crew neck.
Action: Seated at a café table, laughing, looking at each other.
Composition: Medium shot, both characters in frame, 16:9.
```

Never say "two people" — always assign distinct descriptions. Pro's reasoning layer handles distinct characters well if you separate them clearly.

## 5.8 Reflections, screens, mirrors

Identity appearing in a mirror, a TV screen, or a reflection is a specific failure zone. Pro sometimes renders a different face in the reflection than in the primary subject.

**Mitigation:**
- Explicit constraint: *"The reflection in the mirror must show the same person, identical facial features."*
- For critical work, post-composite the reflection separately

## 5.9 Stylization without identity loss

You can stylize a character (anime, oil painting, watercolor, line drawing) while preserving identity markers if you're explicit:

*"Render the person from the reference in a watercolor style. Preserve: face shape, hair color, freckle pattern, eye color. Style: soft watercolor, visible brush strokes, paper texture."*

The preserve list holds the identity while style free-parameters (linework, color palette, medium) change.

---

# Part 6 — Multi-Image Compositing and Reference Roles

## 6.1 The mandatory role-declaration rule

When you provide multiple reference images, assign each one a role. The model interprets unlabeled references as competing influences and produces blended, low-fidelity output.

**Canonical role assignment language (Google-official):**

> Use **Image A for the character's pose**, **Image B for the art style**, and **Image C for the background environment**.

This explicit pattern outperforms everything else the community has tested.

## 6.2 Valid role types

- **Identity** — whose face/body
- **Pose** — what position
- **Style** — aesthetic / medium / rendering
- **Environment** — setting
- **Outfit/garment** — what they wear
- **Product** — what appears in the scene
- **Lighting** — light mood/direction reference
- **Color palette** — tonal reference
- **Composition** — framing/layout reference

## 6.3 Single-source authority rule

Each attribute belongs to exactly one reference. If both Image A and Image B show a face, the model has to pick one — and it will pick silently. Prevent this with explicit authority: *"Identity comes from Image A. Image B is style only — ignore the face in Image B."*

## 6.4 Virtual try-on / garment swap formula

The canonical Google formula for garment try-on:

> Combine these images into one cinematic image in 16:9 format and change the dress on the mannequin to the dress in the image.

For more control:

```
Reference roles: Image 1 = person (identity + pose), Image 2 = garment to apply.
Action: Dress the person from Image 1 in the garment from Image 2.
Preserve: face, pose, background of Image 1. Preserve the exact fabric, cut, and color of the garment from Image 2.
Context: e-commerce product shot for a DTC fashion brand.
```

## 6.5 Sketch-to-final-ad

Pro handles sketch-to-render well, which is genuinely underused for storyboarding ads:

```
Reference roles: Image 1 = napkin sketch (composition and structure), Image 2 = fabric swatch (texture and material), Image 3 = brand mood board (color palette).
Task: Transform Image 1 into a high-fidelity photographic render of a chair, using the fabric from Image 2 and the color palette from Image 3.
Composition: studio product shot, 4:5 vertical.
Lighting: soft three-point softbox, neutral gray seamless.
```

This collapses what was a three-step pipeline (sketch → 3D render → photo comp) into one prompt.

## 6.6 Before/after / scene continuity

For demonstrating product or space transformations, Pro is strong at coherent before/after pairs:

```
Task: Generate two images as a before/after pair.
Before: a cluttered, poorly-lit apartment living room, muted colors, harsh overhead light, disorganized furniture.
After: the same room after a renovation. Preserve: room dimensions, window placement, door placement, architectural features. Change: bright natural light, minimalist Scandinavian furniture, neutral palette, clean staging.
Composition: matching wide shot from the same angle, 16:9 landscape.
```

## 6.7 2D↔3D translation (underused)

One of Pro's strongest capabilities is 2D-to-3D translation and vice versa:

- Floor plan → photorealistic interior render
- Manga/illustration → 3D figurine
- Product sketch → studio product render
- Meme/flat graphic → 3D sculptural version
- Architectural elevation → photographic exterior

For your ad-creative use case, the high-value applications are: sketch-to-final for storyboarding, product-sketch-to-render for prototype visualization, and mood-board-to-ad-frame for pitch decks.

## 6.8 Multi-image negative constraints

When combining references, the model sometimes leaks unwanted elements from a reference into the output. Specify what not to carry over:

*"Ignore the background of Image 1. Ignore the color palette of Image 2. Ignore any text visible in Image 3."*

This is the one legitimate remaining use of negative language — scoped reference exclusion, not general "no cats, no clutter" lists.

---

