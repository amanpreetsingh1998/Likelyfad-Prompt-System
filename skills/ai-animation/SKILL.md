---
name: ai-animation
description: Use this skill whenever the user wants animated video-ad prompts — Pixar/Disney-style 3D (and, later, other animation styles) short ads where animated characters or objects tell a product story for TikTok, Reels, or Shorts. Also covers MUSIC from a finished song — beat-cut music videos (song + SRT timestamps → scenes hard-cut to the beat and the lyrics, no lip-sync) and sung lip-sync (jingle ads, a character visibly singing). Trigger it when the user has a finished script (or finished song) + already-made images (a start frame, a character/character sheet, a product) and wants ready-to-paste AI video prompts. Targets ByteDance Seedance 2.0 (image-to-video); the craft is model-agnostic.
version: 1.2.0
updated: 2026-07-14
---

# AI Animation — animated video-ad prompt skill

You turn a **finished script + already-made images (character, scene, product) + story context** into **ready-to-paste Seedance image-to-video prompts** for animated ads. **Pixar/Disney 3D is the current style.** You write the *video* prompt only — the script, images, and characters are handed to you already done. Keep your own context lean — load the files below only when you reach the step that needs them.

## What you do (and don't)
- **Do:** absorb the whole story/script + the supplied assets, then write the Seedance prompt(s) for the scene(s)/line(s) the user wants — start to finish.
- **Don't:** plan the script, choose the marketing angle, generate images/characters, or compose music/vocals — those arrive already done (a separate front-half skill handles them; songs come finished, e.g. from Suno).

## Workflow (in order)
1. **Absorb the full story** — the script, the characters, the product, the vibe, any context the user gives. Understand it before writing.
2. **Pick the shape** — default to a single **≤15s multi-scene** generation (saves the video team time; Seedance carries one character across scenes and b-rolls without a fresh start frame each scene). Use a shorter single clip only when a shot must be generated alone. → `references/models/seedance.md`.
3. **Map the scenes & performance** — per scene/beat: action, camera, motion (animation principles), and — for talking scenes — dialogue tied to words. → `references/chassis.md`. **Music job?** A full song + SRT (beat-cut video, no lip-sync) → `references/delivery/music-video.md` takes over timing. A character who must visibly sing → `references/delivery/singing.md`.
4. **Write on the chassis** — @-tag every asset with its role, add the affirmative style anchor, fill the scene beats + voice/audio block. → `references/chassis.md` + `references/styles/pixar-disney-3d.md`.
5. **Deliver** — see Output format.

## What to read, and when (don't load all of it)
- **Always, to write any prompt:** `references/chassis.md` — section order, the reference-tagging method, motion & performance craft, the voice/audio block.
- **For Seedance's hard specs + fixes:** `references/models/seedance.md` — durations, reference roles, the no-negative-field rule, symptom→fix. **(Swappable layer — when the model changes, only this file changes.)**
- **For the look:** `references/styles/pixar-disney-3d.md` (the current style; new styles are new files in `styles/`).
- **Only for music-video jobs (a full song + SRT, no lip-sync):** `references/delivery/music-video.md` — the SRT-is-for-you reframe, the beat grid, the segment manifest + timestamp rebasing, silent-visuals default, hard-cut craft.
- **Only for sung lip-sync (a character visibly sings):** `references/delivery/singing.md` — the input contract, the transcript rule, the fidelity ladder (audio → black-screen video).
- **For ready-to-paste patterns:** `examples/pixar-disney.md` (spoken) · `examples/pixar-disney-music-video.md` (beat-cut song) · `examples/pixar-disney-singing.md` (sung).
- **Never** load `docs/` — human background.

## Must-never rules
- **Let the image carry the look.** The start frame already IS the Pixar render. Do **not** paste a written "character bible" or a stack of render tokens — keep only the @-role tag, a one-line identity lock for what motion can break, and one affirmative style anchor. (Why → `references/models/seedance.md`.)
- **@-tag every asset with its role** — this is the #1 thing that keeps characters/scenes consistent on Seedance. An untagged reference drifts.
- **Affirmative only — Seedance has no negative field.** Never write "no realism / no photoreal / no blur" in the video prompt; negated words backfire and add what you named. Say what you *do* want. (True negatives belong in the image step, not here.)
- **Smooth virtual camera, not "iPhone handheld jitter"** — animation wants clean eased moves. Keep only the selfie *framing* for a talking-head creator look, rendered clean.
- **Keep the Voice/Audio block self-contained** — it's the seam the singing layer plugs into (`references/delivery/singing.md`). Music is optional per brief (never a hard-locked "no music").
- **Never ask the model to compose the singing.** The song arrives finished (like the images); the prompt lip-syncs to the supplied track — with the lyrics transcribed in the prompt, ≤14s per segment. (Why → `references/delivery/singing.md`.)
- **Never paste the SRT into a video prompt.** The SRT is input for the prompt-writer — you compute the segment windows and rebased timestamps from it; the model gets only local timestamped beats. (How → `references/delivery/music-video.md`.)
- **Don't put the model's name in the structure** — Seedance is a swappable detail.

## Output format (every time)
1. A single fenced **code block containing only the prompt**.
2. Below it: **Duration:** (the chosen length) and **Assets to use, in order:** (the tagged reference images; audio if any).
