---
name: ai-ugc
description: Use this skill whenever the user wants realistic UGC-style video-ad prompts — talking-head / creator-style short vertical videos where a person speaks to camera (often holding a product) for TikTok, Reels, or Shorts. Trigger it when the user shares a script or hook plus reference images (a person and/or a product) and wants ready-to-paste AI video prompts. Currently targets Google Gemini Omni; the craft is model-agnostic.
version: 1.0.0
updated: 2026-06-16
---

# AI UGC — video-ad prompt skill

You turn a **script + reference images** into **ready-to-paste AI video prompts** for realistic UGC talking-head ads. Keep your own context lean — load the files below only when you reach the step that needs them.

## Workflow (in order)

1. **Understand the script** — the spoken line(s), the emotion, the beat. Long scripts get split into clips.
2. **Map the performance** — per line: facial micro-expressions, gestures, blinking, breathing, head/body motion, tied to specific words. → `references/chassis.md` (Performance section).
3. **Pick a duration bucket** — 4 / 6 / 8 / 10s — and size the dialogue to it. → word budgets in `references/models/gemini-omni.md`.
4. **Write the prompt on the chassis** — fill the variable slots; keep the locked sections verbatim. → `references/chassis.md` + the chosen `references/styles/<style>.md`.
5. **Deliver** — see Output format below.

## What to read, and when (don't load all of it)

- **Always, to write any prompt:** `references/chassis.md` — the section order, locked-vs-variable, the locked Voice block, performance craft.
- **For the current model's hard specs + fixes:** `references/models/gemini-omni.md` — durations, how references work, camera tokens, negatives, and a symptom→fix table. **(This is the swappable layer — when the model changes, only this file changes.)**
- **For the look:** `references/styles/realistic-ugc.md` (brand-agnostic; works for any brand).
- **For ready-to-paste patterns:** `examples/realistic-ugc.md`.
- **Never** load `docs/` — that's human background.

## Must-never rules

- Never reword the **locked Voice block** or any locked section — they exist to keep output consistent across clips.
- Never write **"locked-off / static / tripod"** for the camera — the model freezes the shot. Use handheld wording.
- Never say the background is **"consistent with"** a reference — instruct to **keep it exactly / use it as the first frame**, or the model reinvents it.
- Never exceed the duration's **word budget**; never add **on-screen text/captions** in the generation (captions are added in the edit).
- Don't put the model's name in structure or naming — the model is a swappable detail.

## Output format (every time)

1. A single fenced **code block containing only the prompt**.
2. Below it: **Duration:** (the chosen bucket) and **Assets to use, in order:** (the reference images; audio if any).
