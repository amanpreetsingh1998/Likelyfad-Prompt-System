# Changelog

All notable changes to this system are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/). Each skill also carries its own `version:` in its `SKILL.md` front-matter; releases are git-tagged as `<skill>@<version>` (e.g. `ai-ugc@1.0.0`).

## [Unreleased]

## ai-animation@1.4.0 — 2026-09-09
Adds the **direct 3D explainer** style (the "Zack D" style) as a **second, separate style path** inside `ai-animation` — not a variant of Pixar/Disney 3D, and not related to the song or music layers. Ported from a production-calibrated external style guide (v2.0, 2026-09-02) that was itself adapted from this skill and refined on observed render failures.
### Added
- **New style** (`styles/direct-3d-explainer.md`): semi-realistic game-engine-like characters, cyan-void explainer space or locations built from 3–5 primitives, bright flat phone-readable lighting, a **colour-ownership table** (colour explains function, not decoration), material rules, and this style's camera menu (quick push, snap reframe, locked when the mechanism evolves). Includes a Pixar-vs-explainer delta table and a "writer-notes are never prompt text" guard.
- **New delivery layer** (`delivery/explainer.md`): the **new-fact cadence** (a readable visual fact every 0.8–1.8s, and the insight that a fact is not always a cut), the two visual modes (narrative reenactment vs. explanatory demonstration), the **input contract**, the narration **clause map → beat manifest → rebase → assembly** workflow, the **script-to-visual translation table**, narration-in-post audio, a QC checklist, and a symptom→fix table.
- **Worked example** (`examples/direct-3d-explainer.md`, flagged v1 — test & calibrate): a 24s narrated explainer as three 8s clips, demonstrating both visual modes, the beat manifest, and the two standing lines this style adds.
- **Step 0 style router** in `SKILL.md` — a decision table plus trigger vocabulary so the Pixar and explainer paths are never blended or co-loaded.
### Changed
- **Model layer** (`models/seedance.md`) gained style-agnostic craft hoisted out of the guide, which improves Pixar work too: **one owner per attribute**; the **multi-panel/collage limitation** (an `@image` tag addresses the whole image, never a region — never promise region-picking); final-frame reuse nuance; **motion safeguards** (exact repeated-action counts, cloth and flexible geometry staging, particle/field distribution); the **anatomy and handedness protocol** (camera side, body side, limb chain, grip, active finger, resting hand); expanded **text and label** craft; a **mature/sensitive context** checklist; and nine new symptom→fix rows.
- **Chassis** (`chassis.md`): motion and camera craft is now explicitly **style-scoped** (the animation-principle doctrine is Pixar's, not universal — only "stabilized, purposeful, one move per beat" is universal); added one-owner-per-attribute, the narrated-explainer delivery mode, a mature-context section, and a note that the explainer style legitimately adds Background-rule and Lighting/colour lines to the prompt.
- **`SKILL.md`** description widened from ads-only to ads **and** explainers, with "Zack D" as trigger vocabulary; camera must-never rescoped per style; new must-nevers for attribute ownership, left/right auditing, and not promising generated typography; explainer fields added to the output format.
- Repo plumbing updated: `AGENTS.md`, `CLAUDE.md`, and the plugin marketplace manifest.
### Notes
- Provenance is handled deliberately: the file is named for the **format**, not the creator, and the style file carries the source guide's disclaimer — apply the observable grammar, never copy any channel's name, branding, voice, characters, or individual scenes.

## ai-animation@1.3.0 — 2026-07-23
Calibration from the first real music-video production run (prompt-side; playback validation pending).
### Changed
- **Cut pacing inverted** (`delivery/music-video.md`): a **per-shot ceiling (~1.5s, no lingering)** replaces the old cuts-per-segment cap — 10+ cuts per segment is normal; long lyric lines are covered in multiple angles of the same action, never held. Each segment pre-declares a two-half **split fallback**, fired only if the render smears.
- **Timing authority**: SRT lyric timestamps are the **master clock** (cuts land where words land); the beat grid is secondary. Ceiling violations are repaired by **subdividing the shot in place** — downstream lyric-locked timestamps never move.
- **Fast edit ≠ fast characters**: the Format line now splits editing energy (fast punchy hard cuts) from character motion (calm, believable, slightly slow-motion) — omitting the split makes characters frantic.
- **Per-shot anchors**: every shot line opens with its thread's grade token and closes with exactly one `Camera:` move; grades double as story-thread markers (one locked grade per location/timeline thread).
### Added
- **Multi-character method** (`chassis.md`): per-character @-tag + description + identity lock ("in every shot they appear in"), an explicit "These are N distinct characters…" disambiguation line, generic-extras rule (no identity bleed into crowds), and **story names never enter prompts** — @-tags only.
- **Banned-vocabulary discipline** (`chassis.md`): **ask the user up front** whether anything must never appear; if yes, that concept's entire vocabulary is excluded from every prompt in any form (including negations and near-synonyms) — steer with richer positive description; the list grows when a render misbehaves.
- **Sequenced product reveal** (`delivery/music-video.md`): product incidental at natural scale through the body (wording in References + Setup + Closing); the label/hero framing gets one dedicated slow close-out segment; all other props affirmatively unlabeled (readable prop text garbles).
- **Per-segment delivery ritual** (`delivery/music-video.md`): rolling "Locked:" ledger, complete prompt every time (never fragments), numbered asset lines (`1 — @image_1 — file (role)`), Notes block (risks, playback watch-list, split fallback, next-segment preview), a content-filter pre-check, and audit-don't-reassure against the numbered rulebook.
- Model layer (`models/seedance.md`): new symptom→fix rows — wrong attribute recurring (vocabulary ban), identity bleed into extras, product scale inflation / label garble, readable prop text; smeared-segment fix now points to the split fallback.
- Example (`examples/pixar-disney-music-video.md`) rewritten to v2 demonstrating all of the above (12-shot fast-cut segment + ledger + notes ritual).
### Fixed
- Marketplace manifest: `ai-ugc` version synced to 1.0.1 (was lagging at 1.0.0).

## ai-animation@1.2.0 — 2026-07-14
### Added
- **Beat-cut music-video mode** (`references/delivery/music-video.md`) — the main path for **full songs** (built from the team's SRT idea): a finished song + **SRT timestamped lyrics** + brief + images → per-segment prompts whose scenes **hard-cut in time with the beat and the lyrics**, with **no lip-sync**.
- The core reframe baked in: **the SRT is input for the prompt-writer, never pasted into the video prompt** — the writer computes the lyric-to-scene map, the BPM bar grid (`240 ÷ BPM`), ≤14s segment windows on line/downbeat boundaries, and rebased local timestamps; the model receives only timestamped `hard cut to:` beats.
- **Segment manifest** as the checkable artifact (window / lyric lines / scene / local cut points) — doubles as the edit sheet; solves the "manually cutting a 7–9 minute song" problem at the planning level.
- **Silent-visuals default** — no audio attached, so the 15s audio-input limit stops constraining full songs; the track is laid over in the edit. Optional per-segment audio slice as `rhythm reference only` when motion must ride the beat.
- Worked example (`examples/pixar-disney-music-video.md`, flagged v1 — test & calibrate): inputs → lyric-to-scene map → manifest (with a rebase check) → a full chorus-segment prompt → edit assembly.
- Model layer additions (`models/seedance.md`): timestamped-beat adherence is good but not frame-exact; morph-vs-hard-cut and cut-density symptom→fix rows.
### Changed
- `delivery/singing.md` repositioned as the **special case** (a character visibly sings — jingle ads, sung hooks); full songs defer to `music-video.md` for windowing/manifest/assembly.

## ai-animation@1.1.0 — 2026-07-14
### Added
- **Singing delivery layer** (`references/delivery/singing.md`) — plugs into the chassis's self-contained Voice/Audio seam. The song arrives **finished** (e.g. from Suno) with its lyrics; the skill writes sung lip-sync prompts, never asks the model to compose vocals (unreliable).
- The three sung-lip-sync rules: tag the track's role (`lip-sync … to @audio1`), **always transcribe the lyrics in the prompt** alongside the attached track (audio alone gets misheard), and ≤14s per generation (13s safe).
- **Fidelity ladder** for attaching the song: tagged audio + transcript by default → **black-screen MP4 as a video reference** when rhythm drifts (Seedance follows video refs much more tightly) → native beat sync as a free win (camera/action land on the rhythm).
- **Full-song segment workflow** (in scope for v1): split at phrase boundaries, one ≤13–14s generation per segment, constant reference pack + identical lock wording across segments, assemble in the edit.
- Two sung modes: **on-screen singer** (mouth featured, lip-sync binds) and **sung montage** (track over b-roll, free movement).
- Worked sung example (`examples/pixar-disney-singing.md`, flagged v1 — test & calibrate): a 12s sung jingle ad + the full-song segment pattern.
- Model layer additions (`models/seedance.md`): supplied-audio mechanics + three new symptom→fix rows (misheard lyrics, timing drift, invented extra music).

## ai-song@1.0.0 — 2026-07-14
### Added
- New **`ai-song`** skill: Suno song-prompt system — turns a finished ad script (often **3 hooks + 1 body**) into a paste-ready Suno package (a Style field + the script sung **verbatim** inside Suno's structure tags + settings). The words are locked verbatim; the skill formats and styles only.
- Current model layer: **Suno v5.5, Pro tier** (`references/models/suno.md`) — the two-field split, structure tags, Exclude Styles & sliders, Personas, the **identical-body method** (one master + Replace Section, so each hook is regenerated in-context and matches the body), the **long-song method** (Extend + Get Whole Song + free-DAW cleanup, since Studio is Premier-only), brand-name phonetic respelling, and a symptom→fix table.
- Default sound layer **`high-energy-nonrap`** (fast, driving, gapless, sung — never rap): a genre menu with BPM anchors and an audience→genre hint map. The sound layer is swappable.
- Chassis tuned for songs: format-don't-write, the verbatim rule, structure-tagging from the whole script, the 2–3-treatment sound-decision step, and a small **visual/timing seed** to hand off to the animation skill.
- A worked example (flagged v1 — test & calibrate) and repo plumbing: registered in `AGENTS.md`, `CLAUDE.md`, and the plugin marketplace manifest.

## ai-animation@1.0.0 — 2026-07-13
### Added
- New **`ai-animation`** skill: animated video-ad prompt system — turns a finished script + already-made images (character, scene, product) into ready-to-paste **image-to-video** prompts. **Pixar/Disney 3D** is the first style; the style layer is swappable and a singing/voice delivery mode is planned on top.
- Current model layer: **ByteDance Seedance 2.0** (`references/models/seedance.md`) — durations, the @-tag reference-role mechanism, the no-negative-field rule, and a symptom→fix table.
- Chassis tuned for animation: image-first (the start frame carries the look), lean affirmative anchors instead of the older locked-text "character bible" / negative blocks, smooth virtual camera, animation-principle motion, relaxed lip-sync (head may move during speech), and a **default ≤15s multi-scene** generation to save video-team time.
- The `pixar-disney-3d` style, a self-contained Voice/Audio block (the seam for a future singing skill), and a worked example (flagged v1 — test & calibrate).
- Repo plumbing: registered in `AGENTS.md`, `CLAUDE.md`, and the plugin marketplace manifest.

## ai-ugc@1.0.1 — 2026-06-16
### Changed
- **Voice is now composed per creator and locked per project**, instead of a single fixed woman-persona block. The agent infers a fitting voice (any gender/age/accent/energy) from the creator reference + brief, writes it with a consistent formula, then locks it for that project (reused verbatim across its clips). The Lymphoria voice remains as a labeled worked example. Backward-compatible — existing prompts still valid.

## ai-ugc@1.0.0 — 2026-06-16
### Added
- Initial **`ai-ugc`** skill: realistic UGC talking-head video-ad prompt system (script + reference images → ready-to-paste prompts).
- Chassis (section structure + locked/variable + performance craft), the Voice section, and the `realistic-ugc` style.
- Current model layer: **Google Gemini Omni** (`references/models/gemini-omni.md`) — durations, reference mechanism, camera tokens, negatives, and a symptom→fix table from real testing.
- Worked examples (Lymphoria hooks).
- Repo plumbing: `AGENTS.md`, `CLAUDE.md`, plugin marketplace manifest, and background research in `docs/`.
