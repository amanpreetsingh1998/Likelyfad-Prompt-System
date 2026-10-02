# Model layer — Google Gemini Omni (current)

> This is the **swappable** file. Everything Omni-specific lives here; the chassis/styles/performance never mention a model. When we move to a new model, replace this file (and add `models/<new>.md`).

> **Source tags.** Untagged lines are **tested** by us (the 2026-06 runs). Lines tagged **[google]** come from Google's own guide, *"Creative prompting with Gemini Omni in Google Flow"* (@FlowbyGoogle, 2026-10-01). They are **not yet tested on our UGC clips**. Where a [google] line and a tested line disagree, the tested line wins until a render settles it, and that render gets logged in `docs/prompt-log.md`.

## Hard specs (confirmed)

- **Duration:** four fixed buckets — **4 / 6 / 8 / 10 seconds** (hard cap; overlong dialogue gets cut off the end).
- **Aspect ratio:** **9:16** vertical (supported).
- **References:** up to **1–5 reference images** per generation.
- **Audio:** native synced audio + lip-sync. Voices are **named presets** (e.g. `aoede`, `kore`, `zephyr`, `puck`…), optionally shaped by a voice description. **Use the same named voice every clip for consistency.**
- **Mandatory SynthID watermark** on every output (plan for TikTok/Meta AI-content disclosure).
- **Cuts are the model's default, so ask for one take.** [google] *"By default, Gemini Omni attempts to cut between multiple angles"*; a continuous shot must be stated explicitly. UGC talking-heads are always one continuous take, so every prompt says so twice: in the Format line (*"one continuous handheld take"*) and in the Negatives (*"No scene cuts"*). Internal hard-cuts via a timestamped cut-list are possible but drift — treat as v2 (see Timing below).

## Dialogue word budgets (fast TikTok pace, with headroom)

| Bucket | Words |
|---|---|
| 4s | 8–12 |
| 6s | 12–18 |
| 8s | 16–24 |
| 10s | 20–30 (push toward the top only for deliberately fast delivery) |

## References — how to write them (this model)

Gemini Omni keys off the **described role** of each reference, not a special symbol. Keep named handles **and state each one's role once**:
- `@image1` → scene + background + framing + wardrobe → **also use as the first frame**.
- `@charecterset` (or `@creator`) → the person's identity across angles (face, hair, freckles, body). Do **not** import its background if it's a studio sheet.
- `@productbottle` (or similar) → the exact product — preserve label, shape, colors.

> Phrase it plainly: *"Use @image1 as the first frame and the exact scene/background. Use @charecterset as the identity reference — keep her face, hair, and freckles. Use @productbottle as the product — preserve its label, shape, and colors exactly."* (The `@` is just a handle; the **role description** is what works.)

**More reference types the model accepts** [google]. These are optional and untested for UGC; use one only when the brief supplies the asset:
- **Tagged ingredients.** In Flow, name each asset as you add it, then tag it in the prompt (the `@` handles above are the same idea). Google: you have *"more creative control"* with tagged images than with text alone.
- **A video clip as a motion and audio reference.** Pattern: *"Using this video as a motion and audio reference, change the subject to @charecterset, keep everything else the same."* For us, a real creator's phone clip could set the handheld rhythm and delivery. Caution: rewriting an uploaded *real person's* speech is blocked (see Limits), so the clip sets motion and audio feel only, never the words.
- **First AND last frame.** A start frame fixes composition, palette and subject *"before the camera starts moving"*, which Google says gives *"the least amount of drift"*. We already use @image1 as the first frame. A last frame is new: use it only when the clip must end on a set pose (e.g. product held to camera for the edit).
- **Style transfer.** *"Match the color grading of this image to my scene."* Not for UGC by default, because the Quality/Fidelity Lock already pins the look to @image1.

## Camera tokens (this model)

- **Force handheld:** *"handheld iPhone selfie, held in her own hand, constant natural camera shake — small sway, drift, tiny bounces the whole time."*
- **Never** write **locked-off / static / tripod / stabilized** — the model freezes the shot.
- No deliberate zoom / pan / whip-pan / cuts — only natural handheld motion.
- **Google names camera type outright** [google], e.g. *"Handheld fisheye camera shot of the character in the room."* That supports our handheld wording. Do NOT copy Google's *"No camera movement"* negative: on UGC it freezes the shot, which is our tested failure.

## Timing — beats inside one clip [google]

Google endorses timing in plain language or timecode brackets:
```
[0-3s] ...
[3-6s] ...
```
or *"At 2 seconds, ... At 5 seconds, ..."*. For a talking-head, this is a candidate way to pin a gesture or product lift to a moment. Our word-pinned gestures ("On 'okay?', a head tilt") are the **tested** method; keep them as the default. Try timecodes only as a test variant, inside a single continuous take and never as a cut-list.

**Speed changes:** Google says granular beats vague: *"4x the moving speed"* works better than *"fast"*. Not needed for UGC by default.

## Negatives — keep a tight cue line, prefer positive phrasing

Negatives that reliably work: **"no captions, no on-screen text, no morphing, no warping, no extra fingers."** For everything else, say what you DO want (e.g. *"hands relaxed, five fingers, bottle held steadily"* beats *"no warped hands"*). Don't bloat the negative list.

Google's own list [google] confirms short structural negatives work on this model: *No dialogue · No scene cuts · No extra sound effects · No plastic textures · No camera movement.* For UGC, take **No scene cuts** (now in the locked Negatives) and **No plastic textures** (fits the Fidelity Lock, but only as a test variant). **Never** use *No camera movement* (it freezes the shot) or *No dialogue* (we always have dialogue).

Captions stay **off**. Omni can render kinetic text natively [google], but our captions are added in the edit, so "no captions, no on-screen text" stays.

## Fix a near-miss by editing, not regenerating [google]

Omni can **edit an existing clip through conversation**. When a clip is right except for one thing, edit it instead of re-rolling the whole generation. Google's rule: keep the edit *"hyper-focused"*, because a long description *"can accidentally trigger unintended environmental changes"*. End every edit with **"Keep everything else the same."**

Pattern: `[one specific change]. Keep everything else the same.`
- *"Make the label on the bottle read exactly as in @productbottle. Keep everything else the same."*
- *"Remove the second person in the background. Keep everything else the same."*

Untested by us. Watch for whether the edit holds lip-sync, voice and the handheld shake. If it breaks them, regenerate as before.

## Symptom → fix table (from real testing)

| Symptom | Fix |
|---|---|
| Camera frozen / no shake | Remove "locked-off/static"; foreground handheld shake; tie it to her hand + breathing; don't let the still photo cue stillness. |
| Background changes every generation | Lock it: *"keep the exact background from @image1, do not recreate or change it."* Use @image1 as the **first frame**. Avoid "consistent with." |
| Shot mirrors / flips; product switches hands | Forbid it: *"do not mirror, flip, or horizontally reverse; keep the same left-right layout as @image1 (bare shoulder + product on the same side)."* First-frame locking prevents it. |
| Product label distorts | Pass the product as its own reference; *"preserve the label, shape, and colors exactly; the label must not warp, morph, or stretch."* |
| Empty/unwanted background elements | Describe only what's in the reference; *"do not add people, roads, or pavement."* |
| Speech rushed / cut off | Trim to the bucket's word budget, or move up a bucket. |
| Clip cuts to another angle mid-take [google, untested] | State the one-take twice (Format line + *"No scene cuts"*), per Google's default-cuts note. |
| Everything right except one detail (label text, a stray object) [google, untested] | Edit the clip: *"[the one change]. Keep everything else the same."* Regenerate only if the edit breaks lip-sync, voice or shake. |

## Limits to respect

- **Access:** the Gemini app / Google Flow / YouTube Shorts (manual generation). Our June note said "no public API at launch". Third-party blogs now report an API preview since 2026-06-30 at about $0.10/s, and a version named "Omni 1.1 Flash". Both are **unverified** (no Google source checked). Google's guide calls the model **"Gemini Omni Flash"**.
- Face-swap, outfit-swap, and rewriting an uploaded person's speech are blocked; real-person likeness may be gated — keep the creator a consistent persona.

*Confidence: durations / 9:16 / 1–5 images / lip-sync / SynthID are first-hand confirmed; [google] lines come from Google's official Flow guide (2026-10-01) and are untested on our clips; some community-sourced items in `docs/research.md` with confidence flags.*
