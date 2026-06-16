# Model layer — Google Gemini Omni (current)

> This is the **swappable** file. Everything Omni-specific lives here; the chassis/styles/performance never mention a model. When we move to a new model, replace this file (and add `models/<new>.md`).

## Hard specs (confirmed)

- **Duration:** four fixed buckets — **4 / 6 / 8 / 10 seconds** (hard cap; overlong dialogue gets cut off the end).
- **Aspect ratio:** **9:16** vertical (supported).
- **References:** up to **1–5 reference images** per generation.
- **Audio:** native synced audio + lip-sync. Voices are **named presets** (e.g. `aoede`, `kore`, `zephyr`, `puck`…), optionally shaped by a voice description. **Use the same named voice every clip for consistency.**
- **Mandatory SynthID watermark** on every output (plan for TikTok/Meta AI-content disclosure).
- One continuous take per generation. (Internal hard-cuts via a timestamped cut-list are possible but drift — treat as v2.)

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

## Camera tokens (this model)

- **Force handheld:** *"handheld iPhone selfie, held in her own hand, constant natural camera shake — small sway, drift, tiny bounces the whole time."*
- **Never** write **locked-off / static / tripod / stabilized** — the model freezes the shot.
- No deliberate zoom / pan / whip-pan / cuts — only natural handheld motion.

## Negatives — keep a tight cue line, prefer positive phrasing

Negatives that reliably work: **"no captions, no on-screen text, no morphing, no warping, no extra fingers."** For everything else, say what you DO want (e.g. *"hands relaxed, five fingers, bottle held steadily"* beats *"no warped hands"*). Don't bloat the negative list.

## Symptom → fix table (from real testing)

| Symptom | Fix |
|---|---|
| Camera frozen / no shake | Remove "locked-off/static"; foreground handheld shake; tie it to her hand + breathing; don't let the still photo cue stillness. |
| Background changes every generation | Lock it: *"keep the exact background from @image1, do not recreate or change it."* Use @image1 as the **first frame**. Avoid "consistent with." |
| Shot mirrors / flips; product switches hands | Forbid it: *"do not mirror, flip, or horizontally reverse; keep the same left-right layout as @image1 (bare shoulder + product on the same side)."* First-frame locking prevents it. |
| Product label distorts | Pass the product as its own reference; *"preserve the label, shape, and colors exactly; the label must not warp, morph, or stretch."* |
| Empty/unwanted background elements | Describe only what's in the reference; *"do not add people, roads, or pavement."* |
| Speech rushed / cut off | Trim to the bucket's word budget, or move up a bucket. |

## Limits to respect

- No public API at launch — used via the Gemini app / Google Flow / YouTube Shorts (manual generation).
- Face-swap, outfit-swap, and rewriting an uploaded person's speech are blocked; real-person likeness may be gated — keep the creator a consistent persona.

*Confidence: durations / 9:16 / 1–5 images / lip-sync / SynthID are first-hand confirmed; some community-sourced items in `docs/research.md` with confidence flags.*
