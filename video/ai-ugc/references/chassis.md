# Chassis — the prompt structure (model-agnostic)

The reusable skeleton for every UGC prompt. **Locked** sections are pasted verbatim every time; **variable** sections change per video. (Model-specific exact wording — camera tokens, negatives, reference mechanism — lives in `models/gemini-omni.md`.)

## Section order (keep this order)

1. **Format & Duration** *(variable)* — vertical 9:16, realistic UGC, the chosen duration bucket, one continuous handheld take.
2. **Quality / Fidelity Lock** *(locked)* — raw smartphone look; no beautify / HDR / sharpening / color grade; match the reference image's texture, lighting, freckles, exposure.
3. **Reference / Identity** *(variable subject, locked method)* — name each reference and its role; preserve likeness exactly; use the scene image as the first frame. (Mechanism + exact phrasing → `models/gemini-omni.md`.)
4. **Scene** *(variable)* — lock the exact background from the reference ("do not recreate/change"); describe only what's actually there.
5. **Camera** *(locked method)* — handheld selfie with natural shake; no zoom/pan/cuts. (Exact tokens → `models/gemini-omni.md`.)
6. **Performance & Micro-Movement** *(variable)* — the per-line acting map (see below).
7. **Voice** *(composed per creator, then locked for the project — see below)*.
8. **Dialogue** *(variable)* — the exact spoken line + "accurate lip sync, fast natural pace."
9. **Audio / Environment** *(variable scene, locked realism)* — real phone-mic outdoor sound; no studio/music/cinematic design.
10. **Style** *(locked per style)* — see `styles/<style>.md`.
11. **Negative Constraints** *(locked)* — tight cue line + the model-specific locks (→ `models/gemini-omni.md`).

## Locked vs. variable

- **Locked (verbatim every clip):** Quality/Fidelity Lock, Camera method, Style, Negative Constraints.
- **Per project (composed once to fit the creator, then locked + reused verbatim):** the Voice block.
- **Variable (per clip):** Duration, Reference subject details, Scene, Performance map, Dialogue.

## Voice — compose it per creator, then lock it for the project

The voice is **not fixed to one person** — it can be **any creator**: any gender, age, accent, or energy. What keeps output consistent is the rule: **compose a voice that fits the creator, then lock that exact block and reuse it verbatim on every clip for that creator/project** (so the voice never drifts clip-to-clip).

**How to set the voice (do this automatically — the user shouldn't have to ask):**
1. If the user states a voice, use it.
2. Otherwise, **infer a fitting voice from the creator reference image + the brand/script vibe** — match the apparent gender, age, and energy of the person on screen.
3. Write a 2–3 sentence voice block using the formula below.
4. **Lock it for the project:** reuse that exact block verbatim on every clip for this creator. On Gemini Omni, also pick the **same named voice preset** each time (see `models/gemini-omni.md`).

**Formula (fill each slot):**
> [warmth/tone] + [gender & age feel] + [accent/region] + [texture] + [pacing & energy] + [delivery style], while still staying clear and easy to understand.

| Slot | Examples |
|---|---|
| Warmth / tone | warm · confident · chill · bubbly · deadpan |
| Gender & age | everyday woman in her 30s · older man · young guy in his 20s |
| Accent / region | light casual Southern US · neutral American · British · Australian |
| Texture | natural and slightly textured · smooth · a little raspy · gravelly |
| Pacing & energy | fast-paced TikTok run-on (default for UGC) · calm and measured · punchy |
| Delivery | candid and unpolished, never announcer-like |

**Default for this style:** energetic, **fast-paced TikTok delivery** (a UGC hallmark) — keep that pacing unless the brief calls for calmer; vary the *persona* slots (gender / age / accent / texture) to match the creator.

**Worked example — the Lymphoria project's locked voice (a model to copy, NOT a global default):**
> Warm, natural, everyday-woman American voice with a light, casual Southern lilt — real and slightly textured, never polished or announcer-like. Fast-paced TikTok-style delivery: energetic, quick, and run-on, like she's excitedly rattling off her story to her followers, not calm or composed. She talks fast and casual with natural momentum and candid emphasis, while still staying clear and easy to understand.

Once you've composed a creator's voice block, treat it like a locked section **for that project** — verbatim on every clip.

## Performance & Micro-Movement craft (how to write Section 6)

Write the body alive and candid — never stiff. **Always thread through every clip:** natural uneven blinking; continuous subtle breathing in chest/shoulders; small weight shifts and live head movement; constant facial micro-expressions. If holding a product: one hand holds it the whole time with a relaxed, freely-moving wrist (never rigid), label toward camera; the *other* hand gestures.

Then tie beats to specific words. The expressive channels:
- **Eyes / blink** — default locked to lens (trust); motivated glances on show-and-tell; **reduce blinks + hold gaze** on the big reveal for intensity; uneven, never robotic.
- **Brows** — the main engine: up for surprise/value, knit/down for frustration.
- **Hands** — conversational beats; count on lists; point to body/product; dismiss the "villain" lines; kept in selfie frame.
- **Lean** — *in* for secrets/reveals/value, *back* for confident/sassy lines. The body's main storytelling tool.
- **Head** — micro-nods to affirm, tilt on "okay?"-type check-ins, small shake on negatives, chin-up on confidence.
- **Energy curve** — don't play it flat; ride from mock-warning → proud → peak reveal → frustrated dip → credible → confident close.

Keep it candid and slightly imperfect — **not announcer-like, not overacted.**
