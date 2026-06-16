# Prompt log (humans only — track what works)

Lightweight versioning/quality log for prompt attempts (adapted from Google's prompt-engineering whitepaper). Fill a row per notable generation so we learn what works and can roll back. Not loaded by agents.

| Date | Name / version | Goal | Model | Duration | Prompt (link or file) | Output (link) | Worked? | Notes |
|---|---|---|---|---|---|---|---|---|
| 2026-06-16 | ai-ugc hook v1 | Lymphoria hook, talking-head | Gemini Omni | 10s | `skills/ai-ugc/examples/realistic-ugc.md` | — | partial → fixed | Needed handheld-shake + background-lock + anti-mirror fixes (now baked into the model layer) |

## How to use
- Add a row whenever you test a new prompt or variant.
- "Worked?" = OK / partial / no. If a fix was needed, note it AND fold the lesson into the model layer's symptom→fix table.
- Bump the skill/style `version:` when you change a locked section; log it in `CHANGELOG.md`.
