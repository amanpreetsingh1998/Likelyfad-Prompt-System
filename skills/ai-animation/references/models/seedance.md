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

### One owner per attribute
Each attribute gets **exactly one authoritative asset**. Two assets claiming the same attribute blend into an average of both.
```text
Character sheet  -> face, proportions, hair, clothing
Prop sheet       -> object geometry, colours, mechanical parts
Environment image-> layout and camera axis
Style image      -> render language and palette
```
Never assume an `@image` tag assigns its own role — the tag is only a handle; the **stated role** is what works.

### Multi-panel and collage limitation (don't over-promise this)
An `@image` tag addresses the **complete uploaded image**. "Use the object in the far-left panel" is best-effort natural language — **not** a crop, mask, bounding box, or reliable region selector.
- Describe the wanted object **explicitly in words**; don't rely on pointing at a panel.
- Never assign several conflicting authorities inside one collage.
- Expect more drift when a sheet holds multiple angles, hands, labels, environments, or unrelated examples.
- **Never promise the team precise regional selection from a collage.** If a sheet can't be separated, describe the final object's construction explicitly instead.

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

**Reusing a previous clip's final frame** follows the same logic: useful for a continuous action, exact geometry, a transformation, or a deliberate return to the same composition — **unnecessary for a deliberate hard cut**, where it only constrains the new shot. For independent cuts, character references plus repeated style/background language are sufficient, and fast editing conceals small environment differences.

## Negatives — Seedance has NO negative field (critical)
There is **no `negative_prompt`** on any Seedance 2.0 endpoint, and **negated words backfire** — writing "no blur / no realism / no photoreal" makes the model treat those nouns as content signals and *add* them. So in the video prompt:
- **Affirmative phrasing only.** "no shaky camera" → "smooth stabilized move." "no realism" → "keep the 3D animated render." "no extra fingers" → "clean, correct hands."
- **True negatives belong in the image step** (Nano Banana / Seedream *do* have negative fields) — i.e. the future front-half skill, not here.

## Style & identity locks — keep them tiny (the image already carries them)
Seedance preserves a tagged start frame's subject, composition, and style, so do **not** paste a written character bible or a render-token stack. Keep only three short affirmative anchors:
1. **Role tag** — `@image2 is the character`.
2. **Identity lock, only for what motion can break** — `same face, design, and outfit throughout`.
3. **Style anchor** — `keep the 3D animated / Pixar-style render consistent from first frame to last`.

## Motion safeguards (model failure modes, any style)

### Exact repeated actions
For an exact number of presses, sprays, taps, rotations, or impacts:
1. Prefer **one stable shot** — different angles per cycle multiply hand, object, and count errors.
2. Give **each cycle its own timestamp**.
3. Describe `start -> action -> result -> reset`.
4. Put a brief **pause** between cycles.
5. State the total in an explicit **action-count line**.
```text
[0.0-1.0s] First press: actuator down, one pulse, actuator returns.
[1.0-1.4s] Stable pause.
[1.4-2.4s] Second press: actuator down, one pulse, actuator returns.
Action count: exactly two complete presses.
```

### Cloth and flexible geometry
Lock the fabric's colour, size, thickness, and attachment points. Describe the stages — `grip -> gather -> lift -> arc -> cover -> settle`. **Keep the whole action inside one generation** and use **fewer cuts during the most complex deformation**; where a cut would break the geometry, deliver the next fact through a **state change** instead.

### Particles and fields — define source and distribution
State where an effect starts and how far it spreads, or the model emits a global condition from one suspicious point.
- **Localized:** "one narrow pulse begins at the nozzle and travels to the target."
- **Room-wide:** "a thin translucent field occupies the complete room volume; sparse wisps are distributed across the full source surface and surrounding air, slightly denser near the source and dispersing toward the walls and ceiling."

If the narration describes a whole room, body, chamber, or surface, **depict the full region**.

## Anatomy and handedness (the hand-failure protocol)
Hand failures come from ambiguous left/right instructions, detached close-ups, another person's hand inside a prop sheet, conflicting camera orientation, simultaneous actions, or an obscured grip.

For any hand-critical shot, define all six: **camera side · character side · visible limb chain · grip anatomy · active finger · resting-hand state.**
```text
Camera views the character's left profile. The left shoulder, upper arm, elbow,
forearm, wrist, and hand remain visibly connected. The wrist follows a neutral
line into the forearm. The left thumb opposes four naturally articulated fingers.
The left index finger performs the action.
```
- Keep some **forearm visible** in macro shots, and show how the hand connects to the body.
- **One hand, one task.** Describe thumb **opposition** rather than choreographing every finger.
- Stabilize the camera for a small mechanism.
- **Audit every "left" and "right" before delivery** — mixed sides are the single commonest cause.

## Text, labels, and graphics
Exact readable text on moving 3D props is **unreliable**. Prompting improves hierarchy and placement but **cannot guarantee spelling or stability** — never promise pixel-perfect generated typography.
- Captions, numbers, and critical labels are added **in post**.
- When a prop's text is genuinely required, give it **one dedicated slow or stationary hero shot**: label plane **square to camera**, **move the camera rather than rotating the object**, and treat the label as a fixed preprinted texture.
- State the exact text, capitalization, hierarchy, line order, and placement — then plan post-production texture replacement for pixel-perfect delivery.
- Every other prop in the piece is affirmatively **unlabeled/blank**.

## Mature or sensitive context
- State plainly that **all characters are clearly adults**.
- Imply context through clothing, bedding, expressions, and staging.
- Keep decisions and contact **visibly voluntary**; open hands and relaxed body language for invitational touch.
- Focus on emotion, consequence, or humour.
- Use clear ordinary cinematic language — **never attempt filter evasion** — and preserve platform-safe coverage.

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
| Beat-cut segment comes out smeared/chaotic | Fire the segment's pre-declared split fallback: two thematic halves as separate renders, same references + locks (→ `../delivery/music-video.md`). |
| A wrong attribute keeps rendering (body type, style, mood) | Ban that concept's entire vocabulary from the prompt — including negations and near-synonyms — and describe the wanted attribute in richer positive detail (→ vocabulary discipline in `../chassis.md`). |
| A tagged character's identity bleeds into background extras | Write extras explicitly generic ("a varied, generic background crowd of new incidental people") and keep the distinct-characters disambiguation line. |
| Product inflates toward hero scale / label garbles in casual shots | Weave natural-scale wording ("small, casual, held naturally") into References + Setup + Closing; feature the label only in its one dedicated slow reveal segment, never at fast-cut speed. |
| Readable text on props garbles | Make every prop affirmatively unlabeled/blank; any on-screen text belongs to the edit, not the generation. |
| Repeated action duplicates or loses count | One stable shot, one timestamp per cycle, a pause between cycles, and an explicit action-count line. |
| Wrong hand, twisted wrist, or a hand detached from its arm | Lock camera side and body side, keep the limb chain visibly connected, keep forearm in frame, audit every left/right. |
| Fabric changes size or colour across cuts | Lock colour/size/thickness/attachment; keep the deformation inside one generation with fewer cuts. |
| A global condition emits from one small point | Define the full volume and distribution across the whole intended region. |
| References blend into an average | One owner per attribute; never let two assets claim the same attribute. |
| A collage/multi-panel sheet drifts or picks the wrong object | Describe the wanted object explicitly in words; an @-tag addresses the whole image, not a region. |
| Adjacent shots morph instead of hard-cutting | Make them materially different in angle, scale, framing, or state. |
| Prompt goes mushy as it grows | Let the references carry appearance and the text carry motion; shorten the style anchor. |
| Mood lighting hides the subject | Raise the fill, simplify the light, and keep faces, hands, and mechanisms visible. |

*Confidence: durations / inputs / no-negative-field / native lip-sync are from Seedance / fal.ai docs; exact multi-scene counts and drift fixes are community-sourced starting points — calibrate against your own generations and fold wins back into this table.*
