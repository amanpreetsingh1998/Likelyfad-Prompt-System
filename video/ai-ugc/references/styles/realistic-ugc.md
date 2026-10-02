---
style: realistic-ugc
version: 1.0.0
updated: 2026-06-16
---

# Style — Realistic UGC (brand-agnostic)

A real person filming themselves on a phone, talking to camera like a creator — candid, raw, slightly imperfect. Works for **any brand**; the brand/product is just a reference image + a script.

## What defines this style
- **Raw smartphone realism** — real iPhone look, visible skin texture/freckles, natural exposure; no beautify, HDR, color grade, or "cinematic polish."
- **Handheld selfie** — constant natural camera shake (never tripod-static).
- **Candid performance** — fast, conversational, alive; not announcer-like or overacted.
- **Authentic outdoor/indoor ambience** — real phone-mic sound; no studio/music/cinematic design.

## Fill-in template

Fill the `[BRACKETS]`; keep the rest as written. Compose this project's **Voice block** per `chassis.md` → Voice (fit it to the creator), and pull the camera/negative wording from `models/gemini-omni.md`.

```
Create a vertical 9:16 realistic UGC video, exactly [4/6/8/10] seconds, filmed as one continuous handheld iPhone selfie take with constant natural camera shake the whole time.

Quality / Fidelity Lock: Use the exact same lighting, texture, and iPhone image quality as @image1. Do not sharpen, smooth skin, or apply any beauty filter, HDR, color grade, or cinematic polish. Keep it raw and true to @image1 — natural daylight, realistic exposure, visible freckles and natural skin texture.

Reference / Identity: Use @image1 as the first frame and the exact scene, background, and framing. Use @charecterset as the identity reference — preserve [their exact face, hair, freckles, skin, age, build]. Use @[product] as the product — preserve its label, shape, and colors exactly; the label must never warp or distort. Keep them in the same [outfit] as @image1.

Scene: Keep the exact same background as @image1 — [describe only what's actually there]. Do not recreate or change the background; keep it identical and stable. Do not add people, roads, or pavement.

Camera: Handheld iPhone selfie held in their own hand — constant natural shake (small sway, drift, tiny bounces) the whole time; never tripod-static or locked-off. No zoom, pan, whip-pan, or cuts. Medium close-up, eye-level, matched to @image1, with the product on the same side of the frame as @image1.

Performance & Micro-Movement: [the per-line acting map — see chassis.md: blinking, breathing, brows, hands, lean, head, tied to specific words]. One hand holds the product the whole time with a relaxed, freely-moving wrist (never rigid); the other hand gestures.

Voice: [PASTE THIS PROJECT'S VOICE BLOCK — compose one to fit the creator per chassis.md "Voice", then reuse it verbatim across this creator's clips]

Dialogue: They speak directly to camera with accurate lip sync at a fast, natural, conversational TikTok pace, saying exactly: "[the line]"

Audio / Environment Sound: Realistic iPhone-recorded [setting] audio — [soft natural ambience, light breeze, faint birds, etc.]. Voice close and real to the phone mic, not studio-polished. Avoid traffic, indoor room tone, music, or cinematic sound design.

Style: Authentic TikTok/Reels UGC. Raw handheld smartphone selfie footage with natural camera shake. Natural skin texture with visible freckles. Slightly imperfect, candid realism.

Negative Constraints: No captions, no on-screen text, no logos other than the product label, no morphing, no warping, no extra or missing fingers. Do not mirror, flip, or horizontally reverse the shot — keep the same left-right layout as @image1. Do not recreate or change the background. Do not make the camera tripod-static — natural handheld shake must stay visible. Do not change the outfit, hair, skin, or the product.
```

## Notes
- Size the dialogue to the chosen bucket (`models/gemini-omni.md`).
- Before/after or B-roll visuals (e.g. "here's what it looked like before") are **added in the edit**, not generated in the talking-head clip — write only the lines they say to camera.
