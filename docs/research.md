# Background research (humans only — agents do not load this)

The "why" behind the system. Kept out of the agent load path on purpose (loading it would bloat context). Confidence flagged; many web sources were snippet-only (egress limits), GitHub sources were fetched first-hand.

## Why the repo is lean (context engineering)
- The context window is finite working memory ("RAM" — Karpathy's LLM-OS analogy). Bloated context measurably *reduces* accuracy and increases hallucination — evidenced by **Lost-in-the-Middle** (Stanford), **Context Rot** (Chroma), and **NoLiMa** (ICML 2025). So: load the smallest high-signal set; page in detail on demand ("progressive disclosure").
- Anthropic's litmus test: *"Would removing this line cause a mistake? If not, cut it. Bloated files cause the model to ignore your actual instructions."*

## Why Skills + AGENTS.md
- **AGENTS.md** is the cross-tool standard (OpenAI/Google/Cursor/Copilot/Aider…; now under the Linux Foundation). `CLAUDE.md` bridges it for Claude Code; a short `.github/copilot-instructions.md` bridges Copilot.
- **Anthropic Agent Skills** are the gold-standard progressive-disclosure unit: `name+description` (always loaded, the trigger) → `SKILL.md` body (on trigger, <500 lines) → bundled references/examples (on demand). 40 skills ≈ ~1,500 tokens resident.
- `@`-imports in CLAUDE.md load at launch (NOT lazy) — so the entry **names** files; the agent opens them on demand.

## Versioning
- Per-module versions (front-matter `version:`), git tags `<skill>@x.y.z`, root `CHANGELOG.md` in Keep-a-Changelog format. No filename suffixes. MAJOR bump only when a prompt's input/output contract breaks.

## Gemini Omni (current model) — see `skills/ai-ugc/references/models/gemini-omni.md` for the working facts
- Confirmed first-hand (Gemini Omni API prompt repo): durations 4/6/8/10, 9:16, 1–5 reference images, native lip-sync, named-voice presets, SynthID, no public API at launch.
- Community/snippet-sourced (lower confidence): exact resolution, pricing, some safety specifics.

## Loops (maintenance) — assessed, deferred for now
- Agentic loops (ReAct; scheduled/background runs; "Ralph" while-loops) shine on large *running* codebases with automated test signals — mostly overkill for a small prompt repo. Two real future fits: (1) a scheduled **consistency check** (do all referenced file paths resolve?); (2) a monthly **propose-only** "re-research the model facts → draft a diff." Guardrails if adopted: open PRs (never push), lock sections off-limits, hard caps.

## Key sources
- Karpathy: context engineering / LLM-OS; repos nanoGPT, llm.c, nn-zero-to-hero (minimalism, one-concept-per-file).
- Anthropic: Agent Skills, Claude Code memory docs, "effective context engineering."
- OpenAI: AGENTS.md standard, Cookbook `registry.yaml` index pattern, GPT-4.1 prompting guide.
- Google: Gemini prompt-design (prefixes/delimiters; "favor instructions over constraints"); ADK global vs per-agent instructions.
- Real repos studied: anthropics/skills, f/prompts.chat, EvoLinkAI gpt-image prompts, nano-banana prompts, awesome-ai-video-prompts.
