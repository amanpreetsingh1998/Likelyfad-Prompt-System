# Prompt log (humans only — track what works)

Lightweight versioning/quality log for prompt attempts (adapted from Google's prompt-engineering whitepaper). Fill a row per notable generation so we learn what works and can roll back. **Not loaded by agents.**

| Date | Name / version | Goal | Model | Duration | Prompt (link or file) | Worked? | Notes |
|---|---|---|---|---|---|---|---|
| 2026-06-16 | ai-ugc hook v1 | Lymphoria hook, talking-head | Gemini Omni | 10s | `skills/ai-ugc/examples/realistic-ugc.md` | partial → fixed | Needed handheld-shake + background-lock + anti-mirror fixes (now baked into the model layer) |
| 2026-07-14 | ai-song build 1 — anti-gap A/B | Kill instrumental intros / dead air | Suno v5.5 Pro | ~short | `skills/ai-song/references/models/suno.md` | OK | **Belt-and-suspenders won.** Positive phrases + in-Style negations + the wide 7-entry Exclude list produced far fewer gaps than the guide-site advice to trim to 2–5 and drop negations. Refutes the pink-elephant lore *on this account*. |
| 2026-07-14 | ai-song build 1 — Replace Section | Swap the leading hook, keep the body | Suno v5.5 Pro | ~short | `skills/ai-song/references/models/suno.md` (Job A) | **no** | Leading-hook swap did not produce usable output — its documented weak spot confirmed. **Demoted.** Replaced by standalone hook mini-gens with a locked Voice + external editor drop-join. |
| 2026-07-14 | ai-song build 1 — best gapless run | Fastest, most gapless take | Suno v5.5 Pro | ~short | `skills/ai-song/references/styles/high-energy-nonrap.md` | OK | Dance-pop at 148 and 160 BPM both stayed **sung, never rapped**. `vocals dominate the mix` + `singer begins on the first beat` was the strongest string. Guitar-led pop-rock invited riffs and turnarounds — worse. |
| 2026-07-14 | ai-song build 1 — short hook gens | Standalone hook clips | Suno v5.5 Pro | ~4s | `skills/ai-song/references/models/suno.md` | partial → fixed | Short generations always pad an instrumental tail even with `[End]`. Fix is the editor Crop, not more rolls. |
| 2026-07-23 | ai-animation music video, run 1 | Beat-cut segments from song + SRT | Seedance 2.0 | ≤14s/segment | `skills/ai-animation/references/delivery/music-video.md` | partial → fixed (**prompt-side only**) | Cut pacing inverted to a **~1.5s per-shot ceiling**; "fast edit, calm characters" split added after characters rendered frantic; per-shot grade tokens added after the look drifted shot-to-shot; identity bled into background extras; product inflated toward hero scale and labels garbled. All folded into the model layer. **Playback validation still pending.** |

## Awaiting their first real run (do not treat as tested)
| Item | File | What to watch |
|---|---|---|
| ai-animation — direct 3D explainer style | `skills/ai-animation/examples/direct-3d-explainer.md` | Do 5–7 beats hold inside an 8s render, or does it smear and need the split? Does amber stay on stress only? Does a stripped location stay stripped? Do two clips match well enough to sit side by side? |
| ai-song — hook mini-gen + editor join | `skills/ai-song/examples/three-hooks-one-body.md` | Does the Voice lock actually hold the singer across standalone hook gens? Does the riser-and-drop join read as intentional, especially when hook lengths vary a lot? |
| ai-animation — sung lip-sync | `skills/ai-animation/examples/pixar-disney-singing.md` | Does the transcript-plus-track rule hold the words? Does timing drift enough to need the black-screen-MP4 fallback? |
| ai-ugc — Voice composed per creator | `skills/ai-ugc/references/chassis.md` | Does a composed voice stay identical across a project's clips? |

## How to use
- Add a row whenever you test a new prompt or variant. One row per **finding**, not per render — several findings from one build get several rows.
- **Worked?** = `OK` / `partial → fixed` / `no`. Say plainly when something failed; a demoted method is more valuable than a vague partial.
- If a fix was needed, note it **and** fold the lesson into that model layer's symptom→fix table. The log records what happened; the model file is what agents actually read.
- Move an item out of *Awaiting their first real run* the moment it is genuinely run.
- Bump the skill/style `version:` when you change a locked section, log it in `CHANGELOG.md`, and tag the release `<skill>@<version>`.
