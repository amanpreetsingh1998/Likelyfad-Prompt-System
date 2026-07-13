---
style: pixar-disney-3d
version: 1.0.0
updated: 2026-07-13
---

# Style — Pixar / Disney 3D (brand-agnostic)

Glossy, warm, feature-film 3D animation: rounded stylized characters, big expressive eyes, soft cinematic light. Works for **any brand** — the brand/product is a reference image + a script. This is Seedance's strongest animation mode (its smooth native motion suits it, so it drifts least).

## The style lives in the START FRAME, not the prompt
The Pixar look is set when the **image** is made (your image tool / the future front-half skill). In the *video* prompt you do **not** restate render tokens (subsurface scattering, global illumination, etc.) — the start frame already encodes them. The video prompt carries only **one short affirmative style anchor** to hold the look through motion.

## The style anchor (paste this — affirmative, no negatives)
> **Style:** 3D animated feature film, Pixar/Disney-style render — keep this exact animation render style, character design, and color palette consistent from the first frame to the last. Smooth, appealing, expressive animation.

That's it. No "no photoreal / no realism" — Seedance has no negative field and those backfire. If the image ever renders too realistic, fix it in the image step, not here.

## Motion cadence for this style
Pixar/Disney = **smooth, full, weighted 24fps** motion. Use anticipation before moves, follow-through on hair/cloth/ears, arcs, ease-in/ease-out, believable-but-snappy weight, and expressions pushed slightly larger than life. Avoid linear/robotic motion.

## Camera for this style
Smooth **virtual** camera — gentle dolly/push-in, slow orbit/arc, soft crane; shallow depth of field with creamy bokeh is a stylistic choice, not a realism tell. One eased move per scene beat; no jitter. For a **talking-head "animated creator"** look, keep the selfie *framing* (front-facing, subject upper-2/3, 9:16) but render it clean — not "iPhone handheld shake."

## Fill-in template
Fill the `[BRACKETS]`; keep the anchors as written. Reference roles → `models/seedance.md`; motion/voice craft → `chassis.md`.

```
References: Use @image1 as the first frame and the world. Use @image2 as the character — keep the same face, design, and outfit throughout. [Use @image3 as the product — preserve its label, shape, and colors exactly.]

Style: 3D animated feature film, Pixar/Disney-style render — keep this exact animation render style, character design, and color palette consistent from first frame to last. Smooth, appealing, expressive animation.

Format: vertical 9:16, [N] seconds, [talking-head / voiceover / product-world] animated ad.

Setup: [one line — who/what + the world]. Same character identity throughout.

[0–Xs] Scene 1: [action]. Camera: [one eased move]. Motion: [animation-principle beats — anticipation, follow-through, arcs, easing]. [For talking scenes: brows/eyes/hands/lean/head tied to words; head may move while speaking.] [She says: "[5–10 word line]" — accurate lip sync, natural pace, in [language].]

[X–Ys] Scene 2 (b-roll): [new scene carried by the same character/world in text — no new start frame]. Camera: [one eased move]. Motion: […].

[Y–15s] Scene 3: [payoff / hero shot]. Camera: [one eased move]. Motion: […].

Voice / Audio: [delivery mode — talking-head line / VO voice + line / ambient only]. Voice: [age/tone/energy + any per-word emphasis]. Ambient: [world sound]. [Music: only if the brief asks.]

Closing: keep the same character face, design, and outfit, and the same Pixar/Disney render style, consistent across every scene.
```

## Notes
- Default to one ≤15s multi-scene render (`chassis.md`); b-rolls are text-described, not separate start frames.
- Keep dialogue lines ≤10 words for clean lip-sync (`models/seedance.md`).
- Everything affirmative — no negative cue list in the video prompt.
