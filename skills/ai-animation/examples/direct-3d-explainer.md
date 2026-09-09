# Examples — Direct 3D Explainer / "Zack D" style (worked draft, v1 — test & calibrate)

> **Not yet production-tested.** Drafted from `../references/styles/direct-3d-explainer.md` + `../references/delivery/explainer.md` to show the shape. Your team runs the first real explainer and we tune from the feedback, folding wins back into `../references/models/seedance.md`. Swap the subject, character, and product for your own.

A **24-second narrated explainer** assembled from **three 8-second renders**. It alternates the two visual modes — narrative reenactment for the human context, explanatory demonstration for the mechanism — and ends on a product beat. Narration and captions are added in the edit.

## Inputs
- **Narration script** (the master clock), broken into clauses below.
- `@image1` — character identity and wardrobe authority (a semi-realistic adult, casual clothing).
- `@image2` — prop geometry and colour authority (the product).
- **Banned list:** none declared for this example.

## Clause map + beat manifest (the checkable artifact, and the edit sheet)

| Clip | Narration clause | Mode | Construction + grade | Local beats | Split fallback |
|---|---|---|---|---|---|
| 1 | "You look down at your phone…" | Narrative | Stripped desk corner, neutral grade | 0 / 1.3 / 2.6 / 4.0 / 5.4 / 6.7 | 1A beats 1–3 · 1B beats 4–6 |
| 2 | "…and your neck carries the load." | Explanatory | Cyan void, spine cutaway, amber stress | 0 / 1.2 / 2.5 / 3.8 / 5.1 / 6.5 | 2A beats 1–3 · 2B beats 4–6 |
| 3 | "Support it, and the load comes back off." | Narrative + product | Same desk, neutral grade, product beat | 0 / 1.4 / 2.8 / 4.2 / 5.6 | 3A beats 1–3 · 3B beats 4–5 |

**Colour ownership for the piece:** neutral anatomy is ivory and soft red · stress and load are **amber** · clean corrected motion is **pale cyan**. Locked for all three clips.

## Clip 1 — narrative reenactment (8s)

```
References: Use @image1 as the character identity and wardrobe authority — keep the same face, proportions, hair, and clothing in every shot.

Visual lock: semi-realistic 3D explainer animation, clean synthetic surfaces, strong readable silhouettes, bright saturated phone-screen contrast — keep this exact render style and palette consistent from the first frame to the last.

Background rule: stripped location built from desk + chair + monitor + plain wall plane. Broad simple planes, minimal texture, no decoration.

Lighting/colour: bright frontal key, strong readable fill, clear edge separation, simple contact shadows, saturated contrast. Amber owns stress and load; pale cyan owns clean corrected motion.

Format: vertical 9:16, 8 seconds, 6 beats, a new readable visual fact every 1.3 seconds. All characters are clearly adults.

[0-1.3s] Neutral grade. Wide: the @image1 character sits upright at the desk, phone flat on the table, shoulders level. Camera: brief establishing hold, slight push-in.
[1.3s] Hard cut to:
[1.3-2.6s] Neutral grade. Medium three-quarter: the character lifts the phone and the head begins to tilt forward. Camera: snap reframe to three-quarter.
[2.6s] Hard cut to:
[2.6-4.0s] Neutral grade. Close on the face angled down, eyes tracking the screen, brows relaxed and unaware. Camera: quick push-in.
[4.0s] Hard cut to:
[4.0-5.4s] Neutral grade. Side profile: the head hangs further forward and the neck line lengthens visibly. Camera: locked side view.
[5.4s] Hard cut to:
[5.4-6.7s] Neutral grade. Overhead: the rounded shoulders and forward head read clearly from above. Camera: short vertical track down.
[6.7s] Hard cut to:
[6.7-8.0s] Neutral grade. Extreme close on the base of the neck, an amber glow beginning to gather at the joint. Camera: macro push, easing to a stop.

Motion: the character moves at a calm believable pace — lift, tilt, settle, hold. Each beat ends in a clear stable state before the cut. The amber glow appears only in the final beat and grows steadily.
Audio: quiet room ambience and light synchronized foley, with clean space for narration added in editing.
Continuity: same face, proportions, hair, and clothing in every shot; same desk construction; amber owns stress throughout.
```

**Duration:** 8 seconds. **Mode:** reference-to-video. **Aspect:** 9:16.
**Assets to use, in order:** `1 — @image1 — character.png (character identity and wardrobe authority)`.
**Narration covered:** "You look down at your phone…"

## Clip 2 — explanatory demonstration (8s)

```
References: no character reference in this clip — the subject is an isolated anatomical mechanism.

Visual lock: semi-realistic 3D explainer animation, clean synthetic surfaces, strong readable silhouettes, bright saturated phone-screen contrast — keep this exact render style and palette consistent from the first frame to the last.

Background rule: abstract explainer space — cyan-to-blue gradient with a faint grid, plain floor and shadow catcher, one subject centred.

Lighting/colour: bright frontal key, strong fill, clear edge separation, modest ambient occlusion. Neutral anatomy is ivory and soft red; amber owns stress and load; pale cyan owns clean corrected motion.

Format: vertical 9:16, 8 seconds, 6 beats, a new readable visual fact every 1.3 seconds.

[0-1.2s] Cyan grade. A single ivory neck-and-upper-spine model floats centred and upright, filling most of the frame. Camera: brief explanatory orbit.
[1.2s] Hard cut to:
[1.2-2.5s] Cyan grade. Side cross-section: the outer layer becomes transparent and the stacked vertebrae separate into readable segments. Camera: locked side view.
[2.5s] Hard cut to:
[2.5-3.8s] Cyan grade. The spine tilts forward and amber intensity gathers at the base joint as the angle increases. Camera: short lateral track.
[3.8s] Hard cut to:
[3.8-5.1s] Cyan grade. Macro on the loaded joint: the amber region compresses and the gap between two segments visibly narrows. Camera: locked macro.
[5.1s] Hard cut to:
[5.1-6.5s] Cyan grade. Split comparison: upright ivory spine on the left, forward amber-loaded spine on the right, both fully visible. Camera: short pullback to hold both.
[6.5s] Hard cut to:
[6.5-8.0s] Cyan grade. The forward spine straightens, amber drains away and a pale cyan sweep travels up the corrected line. Camera: quick push-in, easing to a stop.

Motion: one mechanism action per beat — float, separate, tilt, compress, compare, release. Each state settles before the cut. The compression is a visible narrowing, not a colour change alone.
Audio: soft neutral ambience with one restrained impact on the release, and clean space for narration added in editing.
Continuity: one intact spine model with stable geometry and scale; ivory and soft red for neutral anatomy, amber for load, pale cyan for correction, consistent across every shot.
```

**Duration:** 8 seconds. **Mode:** text-to-video. **Aspect:** 9:16.
**Assets to use, in order:** none — this clip is generated from the standing style, background, and lighting lines.
**Narration covered:** "…and your neck carries the load."
**Risk note:** the split comparison at 5.1s is the densest beat. If it smears, fire the pre-declared split — clip 2A is beats 1–3, clip 2B is beats 4–6, same standing lines.

## Why it's built this way (the deltas from the Pixar path)
- **Background rule and Lighting/colour are standing prompt lines.** The piece hard-cuts to new locations and a cyan void, so no single start frame can carry the look. This is the one place the skill breaks image-first, and it is deliberate.
- **A grade token opens every shot line.** At six cuts in eight seconds the single style line will not hold the look on its own.
- **Cuts land on narration clauses**, not on even intervals. Clauses are the master clock, exactly as lyric timestamps are in the music-video layer.
- **8 seconds, six beats, one verb each** — inside the five-materially-different-scenes guidance, with a split fallback pre-declared per clip.
- **Colour is functional, not decorative.** Amber means load everywhere in the piece; the meaning never shifts.
- **Narration is added in post.** The generation carries ambience and foley only, so no lip-sync constrains anything.
- **No claim is baked into the prompt.** Any figure or medical claim belongs to the narration the team writes and verifies, and to captions added in the edit.

## To calibrate (fold wins back into `../references/models/seedance.md`)
Run it, then note: did six beats in eight seconds hold, or did it smear and need the split? did the amber stay on stress only, or leak into decoration? did the anatomy keep stable geometry across the cuts? did the stripped desk stay stripped, or did the model decorate it? did the two clips match in look well enough to sit next to each other in the edit? Adjust, and log the fix.
