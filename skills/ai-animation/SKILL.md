---
name: ai-animation
description: Use this skill whenever the user wants animated short-form video prompts — animated ads or explainers for TikTok, Reels, or Shorts. Two distinct visual styles, never mixed: PIXAR/DISNEY 3D (glossy feature-film ads where a character tells a product story) and the DIRECT 3D EXPLAINER, also called the "Zack D" style (fast semi-realistic hard-cut explainers, a new visual fact every second, narration added in post). Also covers MUSIC from a finished song — beat-cut music videos (song + SRT timestamps, scenes hard-cut to the beat and lyrics, no lip-sync) and sung lip-sync (jingle ads, a character visibly singing). Trigger it when the user has a finished script, narration, or song plus already-made images and wants ready-to-paste AI video prompts. Targets ByteDance Seedance 2.0; the craft is model-agnostic.
version: 1.4.0
updated: 2026-09-09
---

# AI Animation — animated video prompt skill (ads + explainers)

You turn a **finished script or narration + already-made images (character, scene, product) + story context** into **ready-to-paste Seedance prompts** for animated ads and explainers. You write the *video* prompt only — the script, images, and characters are handed to you already done. Keep your own context lean — load the files below only when you reach the step that needs them.

## What you do (and don't)
- **Do:** absorb the whole story/script + the supplied assets, then write the Seedance prompt(s) for the scene(s)/line(s) the user wants — start to finish.
- **Don't:** plan the script, choose the marketing angle, generate images/characters, or compose music/vocals — those arrive already done (a separate front-half skill handles them; songs come finished, e.g. from Suno).

## Step 0 — pick the style path, and don't mix them
The two styles are **separate systems**, not variations. Each has its own look, camera, lighting, timing, and delivery layer. Load one path only; loading both blends them and the render comes out wrong.

| The user wants | Style file | Delivery layer | Example |
|---|---|---|---|
| Glossy feature-film animated ad, cute rounded characters, warm cinematic light | `references/styles/pixar-disney-3d.md` | none (or a music layer) | `examples/pixar-disney.md` |
| Fast explainer, semi-realistic characters, cyan voids, hard cuts every second, narration in post — **the "Zack D" style** | `references/styles/direct-3d-explainer.md` | `references/delivery/explainer.md` | `examples/direct-3d-explainer.md` |

If the user says *"Zack D"*, *"explainer"*, *"fact every second"*, *"cyan background"*, or *"cutaway/mechanism"* — that's the **direct 3D explainer** path. If they say *"Pixar"*, *"Disney"*, *"cartoon mascot"*, or *"cute character ad"* — that's the **Pixar** path. Ask when it's genuinely unclear; never blend.

## Workflow (in order)
1. **Absorb the full story** — the script, the characters, the product, the vibe, any context the user gives. Understand it before writing. **Ask up front whether anything must never appear** (attributes, body types, styles, moods) — if yes, that's the project's banned-vocabulary list. → `references/chassis.md` (Vocabulary discipline).
2. **Pick the shape — this depends on the style.** *Pixar path:* default to a single **≤15s multi-scene** generation (saves the video team time; Seedance carries one character across scenes without a fresh start frame each scene). *Explainer path:* **4–10s clips**, 5–7 beats each, assembled in the edit — never one long render. → `references/models/seedance.md`.
3. **Map the scenes & performance** — per scene/beat: action, camera, motion (animation principles), and — for talking scenes — dialogue tied to words. → `references/chassis.md`. **Explainer job?** `references/delivery/explainer.md` takes over timing — cuts land on **narration clauses**, a new visual fact every 0.8–1.8s. **Music job?** A full song + SRT (beat-cut video, no lip-sync) → `references/delivery/music-video.md` takes over timing. A character who must visibly sing → `references/delivery/singing.md`.
4. **Write on the chassis** — @-tag every asset with its role, add the affirmative style anchor, fill the scene beats + voice/audio block. → `references/chassis.md` + **the style file you picked at Step 0**. (Explainer path: also add the standing Background-rule and Lighting/colour lines.)
5. **Deliver** — see Output format.

## What to read, and when (don't load all of it)
- **Always, to write any prompt:** `references/chassis.md` — section order, the reference-tagging method, motion & performance craft, the voice/audio block.
- **For Seedance's hard specs + fixes:** `references/models/seedance.md` — durations, reference roles, the no-negative-field rule, symptom→fix. **(Swappable layer — when the model changes, only this file changes.)**
- **For the look — load exactly one (see Step 0):** `references/styles/pixar-disney-3d.md` *or* `references/styles/direct-3d-explainer.md`.
- **Only for explainer jobs (narrated, hard-cut, fact-per-second):** `references/delivery/explainer.md` — the new-fact cadence, the two visual modes, the narration clause map + beat manifest, the script-to-visual translation table, and the QC checklist.
- **Only for music-video jobs (a full song + SRT, no lip-sync):** `references/delivery/music-video.md` — the SRT-is-for-you reframe, the beat grid, the segment manifest + timestamp rebasing, silent-visuals default, hard-cut craft.
- **Only for sung lip-sync (a character visibly sings):** `references/delivery/singing.md` — the input contract, the transcript rule, the fidelity ladder (audio → black-screen video).
- **For ready-to-paste patterns:** `examples/pixar-disney.md` (spoken) · `examples/pixar-disney-music-video.md` (beat-cut song) · `examples/pixar-disney-singing.md` (sung) · `examples/direct-3d-explainer.md` (narrated explainer).
- **Never** load `docs/` — human background.

## Must-never rules
- **Let the image carry the look.** The start frame already IS the render. Do **not** paste a written "character bible" or a stack of render tokens — keep only the @-role tag, a one-line identity lock for what motion can break, and one affirmative style anchor. (Why → `references/models/seedance.md`.) **One deliberate exception:** the explainer style adds a standing **Background rule** and **Lighting/colour** line, because it hard-cuts to stripped locations and cyan voids no single start frame can carry.
- **@-tag every asset with its role** — this is the #1 thing that keeps characters/scenes consistent on Seedance. An untagged reference drifts.
- **Affirmative only — Seedance has no negative field.** Never write "no realism / no photoreal / no blur" in the video prompt; negated words backfire and add what you named. Say what you *do* want. (True negatives belong in the image step, not here.)
- **Stabilized, purposeful camera — never "iPhone handheld jitter."** One move per beat, always. The *pace* is set by the style, not here: Pixar wants smooth eased dolly/orbit/crane; the explainer wants quick pushes, snap reframes, and locked shots that point at the fact. Don't apply one style's camera doctrine to the other.
- **Keep the Voice/Audio block self-contained** — it's the seam the singing layer plugs into (`references/delivery/singing.md`). Music is optional per brief (never a hard-locked "no music").
- **Never ask the model to compose the singing.** The song arrives finished (like the images); the prompt lip-syncs to the supplied track — with the lyrics transcribed in the prompt, ≤14s per segment. (Why → `references/delivery/singing.md`.)
- **Never paste the SRT into a video prompt.** The SRT is input for the prompt-writer — you compute the segment windows and rebased timestamps from it; the model gets only local timestamped beats. (How → `references/delivery/music-video.md`.)
- **Story names never enter a prompt** — characters are referenced only as their @-tag ("the @image2 character"); names are conversation handles. With two+ characters, each gets its own identity lock + a "these are distinct characters" line. (→ `references/chassis.md`.)
- **Respect the banned list.** A concept the user banned (or a render already got wrong) never appears in the prompt in any form — not even negated; steer with richer positive description. (→ `references/chassis.md`.)
- **One owner per attribute, and never promise region-picking.** Each attribute has exactly one authoritative asset. An `@image` tag addresses the **whole** uploaded image — "the object in the left panel" is best-effort language, not a crop or mask. Describe the wanted object in words instead. (→ `references/models/seedance.md`.)
- **Audit every "left" and "right" before delivering a hand-critical shot** — mixed sides are the commonest cause of broken hands. Lock camera side, body side, and a visibly connected limb chain. (→ `references/models/seedance.md`.)
- **Never promise exact generated typography.** Prop text is unreliable; critical labels and captions are added in post. (→ `references/models/seedance.md`.)
- **Don't put the model's name in the structure** — Seedance is a swappable detail.

## Output format (every time)
1. A single fenced **code block containing only the prompt** — always the complete prompt, never a fragment or a "same as before, but…" diff.
2. Below it: **Duration:** (the chosen length) and **Assets to use, in order:** as numbered lines — `1 — @image_1 — <filename> (role)` — the tagged reference images; audio if any.
3. On multi-segment jobs (music videos): open with the "Locked:" ledger and close with the Notes block. → `references/delivery/music-video.md` (Per-segment delivery ritual).
4. On explainer jobs: add **generation mode**, **aspect ratio**, **the narration clause(s) this clip covers**, and a **risk note only when a known failure is likely**. → `references/delivery/explainer.md` (Delivery format).
