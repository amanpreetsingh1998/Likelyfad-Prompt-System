# Google's Gemini Omni guide, mapped to our ai-ugc skill (humans only, agents do not load this)

**Source:** *"Creative prompting with Gemini Omni in Google Flow"*, posted by @FlowbyGoogle on X, 2026-10-01: https://x.com/flowbygoogle/status/2105398907702595802. Google's guide is written for all kinds of video (films, ads, design). This page keeps only what bears on realistic UGC talking-heads and says what we did with each tip. The working rules agents read are in `skills/ai-ugc/references/models/gemini-omni.md`, tagged **[google]**.

**Status:** taken into ai-ugc 1.0.2 on 2026-10-01. **Not yet rendered.** Every [google] line is a candidate until a test clip confirms it (see `docs/prompt-log.md`, "Awaiting their first real run").

| # | Google's tip (paraphrased) | What it means for UGC | What we did |
|---|---|---|---|
| 1 | Give high-level creative constraints (detail, costume, micro-expression, timing) instead of micro-managing. | Our Performance map already does this per line. | No change. |
| 2 | Anchor with a start frame, and optionally an end frame, for least drift. | We already use @image1 as the first frame. An end frame could fix the closing pose. | Added as an optional reference type. |
| 3 | Tag "ingredients": named images, and video clips as motion **and audio** references. | A real creator's phone clip could set handheld rhythm and delivery. Speech rewriting of a real person stays blocked. | Added as an optional reference type, with the caution. |
| 4 | Refine pacing granularly ("4x speed", ramp to slow motion). | Rarely needed for talking-heads. | Noted only. |
| 5 | Transfer and mix styles (pose, look, color grade). | Our Fidelity Lock already pins the look to @image1. | Noted as not-by-default. |
| 6 | Omni renders kinetic typography natively. | Captions are added in our edit. | No change; "no captions, no on-screen text" stays. |
| 7 | **Omni cuts between angles by default; a one-take must be stated.** | Contradicts our old line "one continuous take per generation". | **Changed:** the one-take is now stated twice (Format line + "No scene cuts" in the locked Negatives). New must-never in SKILL.md. |
| 8 | Direct cuts and transitions explicitly for multi-shot work. | Not UGC (one take). | No change. |
| 9 | **Edit an existing clip conversationally; keep the edit narrow; end with "Keep everything else the same."** | Cheaper fix for one wrong detail (label text, stray object) than a full re-roll. | **Added:** a "Fix a near-miss by editing" section, two symptom rows, and workflow step 6. |
| 10 | **Direct beats with timecodes ("[0-3s] ...") or "At 2 seconds ..."; audio syncs to visuals.** | Could pin a gesture or product lift to a moment. Our tested method is word-pinned gestures. | Added as a **test variant** only; word-pinning stays the default. |
| — | Short structural negatives work: No dialogue / No scene cuts / No extra sound effects / No plastic textures / No camera movement. | "No scene cuts" fits. "No plastic textures" is a test variant. **"No camera movement" freezes our handheld shot** (our tested failure), and we always have dialogue. | Took "No scene cuts"; flagged the two that must never be used. |

## Also learned, unverified
- Google's guide names the model **"Gemini Omni Flash"**.
- Third-party blogs (not Google sources) report an API preview since 2026-06-30 at about $0.10/s, and an "Omni 1.1 Flash" version in September 2026. Our June note said "no public API at launch". Check a Google source before relying on either.

## The test this sets up (agreed with Aman 2026-10-01, to run later)
One real brief, two prompts: the current tested prompt vs the 1.0.2 prompt. Judge: does it ever cut mid-take; does lip-sync, voice and handheld shake hold. Separately, try one conversational edit on a near-miss clip. Log every finding in `docs/prompt-log.md`; promote or demote [google] lines on the result.
