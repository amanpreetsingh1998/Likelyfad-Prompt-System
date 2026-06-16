# AGENTS.md — Likelyfad Prompt System

> **If you are an AI agent or LLM:** this repo is a library of prompt **skills**. To do a job, open the relevant skill and load **only the files it points you to** — do not load the whole repo. Keeping context lean is a hard requirement here; bloated context degrades accuracy.

## Skills available
- **`ai-ugc`** — turns a script + reference images into ready-to-paste realistic-UGC video-ad prompts. **Entry point: `skills/ai-ugc/SKILL.md`.**

## How to operate
1. Open `skills/ai-ugc/SKILL.md` and follow it.
2. It will tell you which files to read **on demand** — the current model file, the chosen style, examples. Load them only when you reach that step.
3. The user gives you a **script + reference images**; you output ready-to-paste prompts in the skill's required format (a code block + a duration + an ordered asset list).

## Hard rules
- Do **not** preload the whole repo. Open the skill entry, then page in detail as needed.
- Do **not** load `docs/` — it's human background, not for the model.
- Keep the skill's **locked sections** (e.g. the Voice block) **verbatim** — never reword them.

*(Claude Code reads `CLAUDE.md`, which points here. Codex, Cursor, Copilot, and others read this file directly.)*
