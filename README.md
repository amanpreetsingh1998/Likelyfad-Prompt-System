# New Prompt System

A library of master prompt frameworks for generating content. Each framework is a
locked, reusable template: swap the per-video variables, keep the locked sections
intact, and paste into the target engine.

## Frameworks

| Framework | Engine | Output | File |
|---|---|---|---|
| Google Omni | Google Omni | 8s vertical 9:16 realistic UGC video | [`Google-Omni/MASTER-PROMPT.md`](Google-Omni/MASTER-PROMPT.md) |

> Companion to the existing v1–v4 prompt frameworks — same idea (a fundamental
> template you adapt per piece), built specifically for Google Omni.

## How it works

Every framework file is split into:

- **Master Template** — the verbatim, paste-ready default. This is the fundamental; keep it as the default.
- **Variable Slots** — the only parts that change per video (reference image, subject, scene, reveal/punchline, dialogue, voice).
- **Locked Sections** — realism + format rules that stay constant unless new intel changes them.
- **Changelog / Intel Log** — every adjustment is recorded as the template improves over time.
