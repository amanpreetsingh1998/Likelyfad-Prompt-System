# Changelog

All notable changes to this system are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/). Each skill also carries its own `version:` in its `SKILL.md` front-matter; releases are git-tagged as `<skill>@<version>` (e.g. `ai-ugc@1.0.0`).

## [Unreleased]

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
