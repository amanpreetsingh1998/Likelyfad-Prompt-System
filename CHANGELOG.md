# Changelog

All notable changes to this system are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/). Each skill also carries its own `version:` in its `SKILL.md` front-matter; releases are git-tagged as `<skill>@<version>` (e.g. `ai-ugc@1.0.0`).

## [Unreleased]

## ai-animation@1.1.0 — 2026-07-14
### Added
- **Singing delivery layer** (`references/delivery/singing.md`) — plugs into the chassis's self-contained Voice/Audio seam. The song arrives **finished** (e.g. from Suno) with its lyrics; the skill writes sung lip-sync prompts, never asks the model to compose vocals (unreliable).
- The three sung-lip-sync rules: tag the track's role (`lip-sync … to @audio1`), **always transcribe the lyrics in the prompt** alongside the attached track (audio alone gets misheard), and ≤14s per generation (13s safe).
- **Fidelity ladder** for attaching the song: tagged audio + transcript by default → **black-screen MP4 as a video reference** when rhythm drifts (Seedance follows video refs much more tightly) → native beat sync as a free win (camera/action land on the rhythm).
- **Full-song segment workflow** (in scope for v1): split at phrase boundaries, one ≤13–14s generation per segment, constant reference pack + identical lock wording across segments, assemble in the edit.
- Two sung modes: **on-screen singer** (mouth featured, lip-sync binds) and **sung montage** (track over b-roll, free movement).
- Worked sung example (`examples/pixar-disney-singing.md`, flagged v1 — test & calibrate): a 12s sung jingle ad + the full-song segment pattern.
- Model layer additions (`models/seedance.md`): supplied-audio mechanics + three new symptom→fix rows (misheard lyrics, timing drift, invented extra music).

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
