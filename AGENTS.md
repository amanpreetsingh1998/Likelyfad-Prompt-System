# AGENTS.md: Likelyfad Prompt System 2.0

> **If you are an AI agent or LLM (Claude, ChatGPT, Codex, Gemini, Cursor or any other): this is your entry point.** This repo is a library of prompt **skills**, organised into three systems: **image**, **video** and **audio**. Do not load the whole repo. Follow the steps below and load only the files you are pointed to; bloated context degrades accuracy.

## Step 1: ask the user (start here, every new session)
Ask exactly this, then wait for the answer:

**"What do you want to create?**
**1) An image** (characters, character sheets, transformations, locations, product shots, posters, thumbnails, first frames…)
**2) A video** (realistic UGC creator videos, animated Pixar / Zack D videos, music videos…)
**3) Audio** (a brand song, or a voiceover / narration)"

## Step 2: open that system's menu
- **Image** → open **`image/SYSTEM.md`**
- **Video** → open **`video/SYSTEM.md`**
- **Audio** → open **`audio/SYSTEM.md`**

Each SYSTEM.md asks one more question and sends you to exactly one skill's `SKILL.md`.

## Step 3: follow the skill
The skill asks for its inputs (one question at a time), tells you which files to read **on demand**, and gives the exact output format. Follow it.

## All skills (for reference; still route through the menus above)
| System | Skill | What it makes | Entry |
|---|---|---|---|
| Image | `character-casting` | Cast plans, character sheets (5-view full body / 3-view chest-up), before/after transformation edits, location references, in 4 styles. Seedream 5.0 Pro or Nano Banana Pro prompts | `image/character-casting/SKILL.md` |
| Image | `nano-banana` | Any other image, or an edit, with Nano Banana Pro | `image/nano-banana/SKILL.md` |
| Video | `ai-ugc` | Realistic UGC talking-head prompts for Gemini Omni | `video/ai-ugc/SKILL.md` |
| Video | `ai-ugc-seedance` | Realistic UGC prompts for Seedance 2.0, incl. multi-clip series | `video/ai-ugc-seedance/SKILL.md` |
| Video | `ai-animation` | Animated prompts for Seedance 2.0: Pixar/Disney 3D or the Zack D explainer; music videos; sung lip-sync | `video/ai-animation/SKILL.md` |
| Audio | `ai-song` | Suno song prompts from an ad script, incl. long 5–10 min songs | `audio/ai-song/SKILL.md` |
| Audio | `elevenlabs-voice` | ElevenLabs v3 voiceover / dialogue scripts with audio tags | `audio/elevenlabs-voice/SKILL.md` |

## Hard rules
- Ask before you assume: use the menus; ask one question at a time.
- Load only what the current step needs. Never preload the repo. Never load `docs/` (human background only).
- Keep every skill's **locked** text verbatim (style masters, voice blocks, locked prompt sections).
- Old links to `skills/<name>/` are signposts only; the map is in `docs/MOVED.md`.

*(Claude Code reads `CLAUDE.md`, which points here. All seven skills are also registered for Claude Code under `.claude/skills/`.)*
