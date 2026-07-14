# Changelog

All notable changes to this system are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/). Each skill also carries its own `version:` in its `SKILL.md` front-matter; releases are git-tagged as `<skill>@<version>` (e.g. `ai-ugc@1.0.0`).

## [Unreleased]

## ai-song@1.0.0 — 2026-07-14
### Added
- New **`ai-song`** skill: Suno song-prompt system — turns a finished ad script (often **3 hooks + 1 body**) into a paste-ready Suno package (a Style field + the script sung **verbatim** inside Suno's structure tags + settings). The words are locked verbatim; the skill formats and styles only.
- Current model layer: **Suno v5.5, Pro tier** (`references/models/suno.md`) — the two-field split, structure tags, Exclude Styles & sliders, Personas, the **identical-body method** (one master + Replace Section, so each hook is regenerated in-context and matches the body), the **long-song method** (Extend + Get Whole Song + free-DAW cleanup, since Studio is Premier-only), brand-name phonetic respelling, and a symptom→fix table.
- Default sound layer **`high-energy-nonrap`** (fast, driving, gapless, sung — never rap): a genre menu with BPM anchors and an audience→genre hint map. The sound layer is swappable.
- Chassis tuned for songs: format-don't-write, the verbatim rule, structure-tagging from the whole script, the 2–3-treatment sound-decision step, and a small **visual/timing seed** to hand off to the animation skill.
- A worked example (flagged v1 — test & calibrate) and repo plumbing: registered in `AGENTS.md`, `CLAUDE.md`, and the plugin marketplace manifest.

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
