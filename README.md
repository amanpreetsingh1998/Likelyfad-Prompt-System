# Likelyfad Prompt System

A versioned, agent-loadable library of prompt **skills** for producing content with AI models.

Built lean on purpose: an agent loads only the skill (and the one style) it needs — never the whole library — so the context window stays small and the output stays accurate.

## Skills

| Skill | What it produces | Current model (swappable) | Folder |
|---|---|---|---|
| `ai-ugc` | Realistic UGC talking-head video ads (short, vertical, lip-synced) | Google Gemini Omni | [`skills/ai-ugc/`](skills/ai-ugc/) |

## How to use it

- **Claude Code / Claude API / Agent SDK** → install the skill (below); it auto-loads when you ask for UGC video prompts.
- **Any other agent (Codex / Cursor / etc.)** → point it at [`AGENTS.md`](AGENTS.md).
- **As a human** → open the skill folder and read `SKILL.md`, then the style + examples.

### Install in Claude Code
```
/plugin marketplace add amanpreetsingh1998/likelyfad-prompt-system
```
Then the `ai-ugc` skill is available in your sessions. (Universal fallback that works in any agent: see `AGENTS.md`.)

## Layout

```
skills/        capabilities as portable Skills (lean entry + on-demand detail)
docs/          background research + prompt log — for humans, NOT loaded by agents
CHANGELOG.md   version history (per-skill versions live in each skill's front-matter)
AGENTS.md      universal agent entry point
```

## Design principles

1. **Lean / progressive disclosure** — tiny always-loaded entry, detail paged in only when needed.
2. **Model is a swappable layer** — model specifics live in `skills/ai-ugc/references/models/`; the craft (chassis, performance, styles) doesn't mention any model, so models can change without rework.
3. **Locked vs. variable** — realism-critical blocks are locked (reused verbatim); only the script/scene/performance change per video.
