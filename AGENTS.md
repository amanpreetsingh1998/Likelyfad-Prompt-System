# AGENTS.md — Likelyfad Prompt System

> **If you are an AI agent or LLM:** this repo is a library of prompt **skills**. To do a job, open the relevant skill and load **only the files it points you to** — do not load the whole repo. Keeping context lean is a hard requirement here; bloated context degrades accuracy.

## Skills available
- **`ai-ugc`** — turns a script + reference images into ready-to-paste realistic-UGC talking-head video-ad prompts. Current model: Google Gemini Omni. **Entry point: `skills/ai-ugc/SKILL.md`.**
- **`ai-song`** — turns a finished ad script (often **3 hooks + 1 body**) into ready-to-paste **Suno** song prompts (a Style field + the script sung **verbatim** inside structure tags + settings) for a high-energy, non-rap brand song. Current model: Suno v5.5 (Pro). **Entry point: `skills/ai-song/SKILL.md`.**

## How to operate
1. Pick the skill that matches the job (realistic talking-head video → `ai-ugc`; a Suno song from an ad script → `ai-song`) and open its `SKILL.md`, then follow it.
2. It will tell you which files to read **on demand** — the current model file, the chosen style, examples. Load them only when you reach that step.
3. The user hands over the inputs (a **script + reference images** for video; an **ad script** for a song); you output ready-to-paste prompts in the skill's required format.

## Hard rules
- Do **not** preload the whole repo. Open the skill entry, then page in detail as needed.
- Do **not** load `docs/` — it's human background, not for the model.
- Keep the skill's **locked sections** (e.g. the Voice block) **verbatim** — never reword them.

*(Claude Code reads `CLAUDE.md`, which points here. Codex, Cursor, Copilot, and others read this file directly.)*

*(For Claude Code users, `ai-song` is also registered as a proper Agent Skill via `.claude/skills/ai-song` — a symlink to `skills/ai-song`, so there is one source of truth. It auto-loads on trigger or via `/ai-song`. To use it outside this repo: copy the `skills/ai-song` folder into `~/.claude/skills/` for personal use in any project, or zip it and upload as a custom skill on claude.ai.)*
