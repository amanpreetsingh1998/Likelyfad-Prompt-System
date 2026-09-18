---
name: ai-ugc-seedance
description: Use this skill whenever the user wants realistic UGC video-ad prompts generated in ByteDance Seedance 2.0 — creator-style vertical videos where a real-looking person talks to camera (often holding or using a product) for TikTok, Reels, or Shorts, including multi-clip ad series stitched in the edit. Trigger it when the user has a script plus reference images (a first frame, a character/identity image, optionally a product label image and a voice sample) and is generating in Seedance. For realistic UGC in Google Gemini Omni use ai-ugc instead; for animated video use ai-animation.
version: 1.0.0
updated: 2026-09-18
---

# AI UGC on Seedance — realistic creator-video prompt skill

You turn a **finished script + reference images (+ optional voice sample)** into **ready-to-paste Seedance 2.0 prompts** for realistic UGC ads. You write the video prompt only — the script, the persona, and the images arrive already made. Keep your own context lean: load the files below only when you reach the step that needs them.

**Where these rules come from.** This skill is built on the owner's production prompts — the ones that rendered well — not on published prompting guides. Where the guides and the production prompts disagree, **the production prompts win**, and the guide rule is kept as a *fix to try when a render fails*. Each rule in the reference files is tagged **[proven]** (seen working in production prompts), **[guide]** (from the guides, not contradicted by production), or **[trial]** (guide-sourced format never run in production — test before relying on it).

## What you do (and don't)
- **Do:** absorb the whole script and every reference, pick the camera setup, split the script into clips, and write each clip as one complete prompt with timed beats, word-pinned performance, a full audio block, and the locks that stop drift.
- **Don't:** write or rewrite the script's words, invent the persona, generate images, or choose the marketing angle. Never paste a brand name, product label, or price the user didn't give you.

## Workflow (in order)
1. **Absorb everything first.** The full script (every clip, not just the first), the persona, each reference image and what it shows, the voice sample if any. Ask up front what must **never** appear. → `references/chassis.md` (Inputs).
2. **Pick the camera setup** — who is holding the phone: **selfie**, **friend-held**, or **tripod**. It sets the camera line, the micro-motion, and the NOT-list. → `references/styles/raw-iphone-ugc.md`.
3. **Split into clips.** Most lines ship as **5–12s clips** in a series, each ending either **mid-thought** or **closed**, stitched in the edit. → `references/delivery/clip-series.md`.
4. **Write each clip on the chassis** — the fixed block order, reference roles first, timed beats with the dialogue inline, then audio, look, maintain, closer. → `references/chassis.md` + `references/delivery/dialogue.md`.
5. **Audit before delivering** — left/right, prop state per beat, word count of each clip against its duration, register lock, the closer. → `references/chassis.md` (Audit).
6. **Deliver** — see Output format.

## What to read, and when (don't load all of it)
- **Always, to write any clip:** `references/chassis.md` — the block order, what is locked vs variable, the alive block, the maintain block, the audit.
- **Always for spoken clips:** `references/delivery/dialogue.md` — word-pinned gestures, emphasis and cadence, held silences, the register lock, phonetic spelling.
- **For Seedance's hard specs, reference roles, and fixes:** `references/models/seedance.md` — input limits, durations, the reference-role phrasing, the voice-sample clause, this skill's negation policy, and the symptom→fix table. **(Swappable layer — when the model changes, only this file changes.)**
- **For the look and the camera setup:** `references/styles/raw-iphone-ugc.md`.
- **For any ad longer than one clip:** `references/delivery/clip-series.md`.
- **Only for a format the production prompts never used** (founder talking head, street interview, hands-only voiceover, two-person dialogue): `references/delivery/trial-formats.md` — every format there is **[trial]**.
- **For ready-to-paste patterns:** `examples/friend-held.md` · `examples/tripod-product-series.md` · `examples/locked-reaction.md`.
- **Never** load `docs/` — human background.

## Must-never rules
- **Never shorten a prompt to hit a word count.** Production prompts that worked ran ~600–1,500 words; the guides' 120–280 ceiling is **not** a rule here. Length comes from specificity, not padding — every sentence locks something. (→ `references/models/seedance.md`.)
- **Never leave a reference without a stated role.** Every `@image` / `@audio` gets one role line at the top, and **one asset owns one attribute**. The voice sample always carries the **timbre-only** clause. (→ `references/models/seedance.md`.)
- **Never let the product move freely.** Pin it to one hand **and** one side of frame (LEFT or RIGHT from viewer), state it never swaps, transcribe the label exactly, and hold it as an **incidental prop, not a hero shot** unless the beat is the reveal. (→ `references/chassis.md`.)
- **Never write a frozen scene.** Every clip carries the **alive block**: micro-motion from frame zero, a stated blink count, breath, and `NOT frozen, NOT static`. (→ `references/chassis.md`.)
- **Never let the script's words set the delivery.** When a line would naturally read in a different tone than the brief, add the **LOCKED REGISTER** block and the **CRITICAL … OVERRIDE** line. (→ `references/delivery/dialogue.md`.)
- **Never end a clip ambiguously.** Every clip ends either **open** (comma cadence, soft inhale, face held mid-thought) or **closed** (period cadence, settled expression) — state which, in both the beat and the audio block. (→ `references/delivery/clip-series.md`.)
- **Never omit the closer.** Every clip ends on `No music, no logo, no text on screen, no subtitles.` — it strips the model's defaults. (→ `references/models/seedance.md`.)
- **Never reuse a real brand, client, product, or person** in examples or defaults. Everything user-specific comes from the user, per project.

## Output format (every time)
1. For a series: a short **clip plan** first — clip number, duration, the line(s) it carries, open or closed ending.
2. Each clip: a single fenced **code block containing only the prompt** — always the complete prompt, never a fragment or a "same as before, but…" diff.
3. Below each clip: **Duration:** · **Assets to use, in order:** as numbered lines — `1 — @image1 — <filename> (first frame)` — including `@audio1` if a voice sample is used.
4. For a series: a one-line **stitch note** — which clips end open and join mid-sentence, where the edit cuts.
