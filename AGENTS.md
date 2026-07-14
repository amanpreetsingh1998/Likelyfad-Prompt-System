# AGENTS.md — Likelyfad Prompt System

> **If you are an AI agent or LLM:** this repo is a library of prompt **skills**. To do a job, open the relevant skill and load **only the files it points you to** — do not load the whole repo. Keeping context lean is a hard requirement here; bloated context degrades accuracy.

## Skills available
- **`ai-ugc`** — turns a script + reference images into ready-to-paste realistic-UGC talking-head video-ad prompts. Current model: Google Gemini Omni. **Entry point: `skills/ai-ugc/SKILL.md`.**
- **`ai-animation`** — turns a finished script + already-made images (character, scene, product) into ready-to-paste **animated** video-ad prompts (Pixar/Disney 3D first). Also handles music from a **finished song**: **beat-cut music videos** (song + SRT timestamps → scenes hard-cut to the beat and lyrics, no lip-sync) and **sung lip-sync** (jingle ads, a character visibly singing). Current model: ByteDance Seedance 2.0 (image-to-video). **Entry point: `skills/ai-animation/SKILL.md`.**

## How to operate
1. Pick the skill that matches the job (realistic talking-head → `ai-ugc`; animated → `ai-animation`) and open its `SKILL.md`, then follow it.
2. It will tell you which files to read **on demand** — the current model file, the chosen style, examples. Load them only when you reach that step.
3. The user gives you a **script + reference images** (and, for animation, story context); you output ready-to-paste prompts in the skill's required format (a code block + a duration + an ordered asset list).

## Hard rules
- Do **not** preload the whole repo. Open the skill entry, then page in detail as needed.
- Do **not** load `docs/` — it's human background, not for the model.
- Keep the skill's **locked sections** (e.g. the Voice block) **verbatim** — never reword them.

*(Claude Code reads `CLAUDE.md`, which points here. Codex, Cursor, Copilot, and others read this file directly.)*
