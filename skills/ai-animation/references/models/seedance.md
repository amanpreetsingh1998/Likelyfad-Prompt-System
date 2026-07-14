# Model layer — ByteDance Seedance 2.0 (current)

> The **swappable** file. Everything Seedance-specific lives here; the chassis / styles / motion never name a model. When we move models, replace this file (and add `models/<new>.md`).

## Hard specs (confirmed)
- **Duration:** 4–15s, continuously selectable. **Default to 15s** for animated ads (one multi-scene render saves generation time; ~3–4 meaningful scenes fit in 15s — more than ~5 risks drift/blur). If unsure of a look, validate at ~5s first, then run the full length.
- **Aspect ratio:** 9:16 (default for social), 16:9, 1:1, 21:9.
- **Inputs:** up to **9 images + 3 videos (≤15s) + 3 audio (≤15s)**, **12 assets max** per generation. Roles are set by @-tag + your stated description (below).
- **Modes:** **image-to-video** (a start frame) and **reference-to-video** (multiple tagged `@image` refs). `end_image` (start+end) exists but we don't use it by default (below).
- **Audio:** native synced audio + **lip-sync**, 8+ languages (cleanest: Mandarin, then English). `generate_audio` toggle.
- **Resolution:** 480p / 720p / 1080p / 4K (1080p & 4K need the `std` mode; `fast` = 480/720 only). 4K is upscaled, not native.

## References — how to write them (this model)
Seedance keys off the **@-tag + your stated role**, and will NOT reliably infer roles. Always tag and label:
- `@image1 as the first frame` → the opening scene; sets world + framing.
- `@image2 as the character` → identity across the whole clip (Seedance preserves it). A character sheet works best at ~3 clean, same-lighting angles.
- `@image3 as the location` / `@image4 as the product` → environment / product (preserve label, shape, colors).

> Untagged or vaguely-referenced assets are where drift lives. One phrase per asset, up top.

## Supplied audio & sung lip-sync (this model)
For singing (a finished track + lyrics — workflow → `../delivery/singing.md`), the mechanics on Seedance:
- **Tag the track's role** like any asset: `Lip-sync the character's singing to @audio1` (a rhythm/mood-only track is a different role — say which).
- **Transcribe the words in the prompt even with the track attached** — audio alone gets misheard (tests saw "Seedance 2.0" come back as "CGI 2.0" until the words were spelled out); track + transcript together is the fix.
- **Raw audio references can drift in rhythm/intervals** (very noticeable with music). The high-fidelity workaround: convert the segment to a **black-screen MP4 and attach it as a video reference** — Seedance follows video references much more tightly.
- **Keep sung segments ≤14s (13s safe)** — under the 15s ceiling; longer sync goes rubbery.
- **Beat sync is native:** a strong-beat track pulls camera moves and action onto the rhythm automatically — write camera beats to the musical phrases.
- **Beat-cut music videos** (→ `../delivery/music-video.md`) usually need **no audio attached at all** — silent visuals + timestamped `hard cut to:` beats; the song is laid over in the edit. Timestamped-beat adherence is good but **not frame-exact** (within a fraction of a second) — the edit does the final nudge. Attach a segment's audio slice tagged `rhythm reference only — no dialogue, no lip-sync` just when motion must ride the beat within a scene.

## End frames — off by default
`end_image` (start→end interpolation) only helps when the **ending is a fixed target**: an on-screen transformation, a before→after, or a logo/product reveal outro — **and** only when the start and end share near-identical framing (mismatched framing "morphs into a smeared mess"). Our default is **start frame + tagged elements + motion in text**, so skip end frames unless a shot genuinely needs one.

## Negatives — Seedance has NO negative field (critical)
There is **no `negative_prompt`** on any Seedance 2.0 endpoint, and **negated words backfire** — writing "no blur / no realism / no photoreal" makes the model treat those nouns as content signals and *add* them. So in the video prompt:
- **Affirmative phrasing only.** "no shaky camera" → "smooth stabilized move." "no realism" → "keep the 3D animated render." "no extra fingers" → "clean, correct hands."
- **True negatives belong in the image step** (Nano Banana / Seedream *do* have negative fields) — i.e. the future front-half skill, not here.

## Style & identity locks — keep them tiny (the image already carries them)
Seedance preserves a tagged start frame's subject, composition, and style, so do **not** paste a written character bible or a render-token stack. Keep only three short affirmative anchors:
1. **Role tag** — `@image2 is the character`.
2. **Identity lock, only for what motion can break** — `same face, design, and outfit throughout`.
3. **Style anchor** — `keep the 3D animated / Pixar-style render consistent from first frame to last`.

## Symptom → fix table (starting points — calibrate on real generations)
| Symptom | Fix |
|---|---|
| Character drifts / redesigns across scenes | Tag the character explicitly (`@image2 is the character`); add the identity-lock line; keep the character set to ~3 clean angles, not many. |
| Style creeps toward photoreal in motion | Add the affirmative style anchor + closing consistency line; make sure the start frame is fully stylized. Never write "no realism" (it backfires). |
| Prompt "generation failed" / mush | Too many conflicting *visual* descriptors — the start frame already sets the look; cut visual re-description, keep motion/scene/voice. Don't overstuff a 15s render past ~4 scenes. |
| Camera looks stiff / video-game-ish | Ask for eased moves ("smooth ease-in/ease-out dolly"), one move per beat; avoid linear/robotic motion. |
| Lip-sync mushy | ≤10-word lines; front-facing, clear-mouthed character design; tag the language; frame the speaking scene medium/close. |
| Multi-scene character inconsistency | One character reference for the whole generation; describe each new scene in text rather than swapping references mid-prompt. |
| Sung words wrong / mumbled (supplied track) | Transcribe the exact lyrics in the prompt alongside the tagged track — never rely on the audio alone. |
| Timing wanders off the supplied track | Attach the segment as a black-screen MP4 *video* reference instead of raw audio; keep it ≤13s. |
| Extra music invented over a supplied track | State the role plainly: "@audio1 is the only music and the master timing." |
| Shots morph/blend instead of hard-cutting | Write `hard cut to:` explicitly at each timestamp, with a distinct location/framing change per cut — near-identical shots invite morphing. |
| Beat-cut segment comes out smeared/chaotic | Cap ~4–5 cuts per segment; slow the cadence (cut every 2 bars); move faster cutting to the edit. |

*Confidence: durations / inputs / no-negative-field / native lip-sync are from Seedance / fal.ai docs; exact multi-scene counts and drift fixes are community-sourced starting points — calibrate against your own generations and fold wins back into this table.*
