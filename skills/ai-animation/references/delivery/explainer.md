# Delivery layer — Direct 3D explainer (narration → beats → hard cuts)

> The timing and narration grammar for the **direct 3D explainer** style (the "Zack D" style). Pairs with `../styles/direct-3d-explainer.md` — load both, and load neither for Pixar or music jobs. Takes over chassis Sections 3, 5 and 6 (format, scene beats, audio).

## The core objective
**Every second delivers a new, instantly readable visual fact.** The viewer understands the current idea in about one second. One dominant idea at a time, large subjects, sparse functional backgrounds, literal visualization of the narration, frequent changes of angle/scale/state, direct hard cuts.

## New-fact cadence
A new readable visual fact every **0.8–1.8 seconds**; default **1.0–1.5**.

**A new fact is not always a cut.** It can be any of: a hard cut · a wide-to-macro scale change · a new viewing angle · a hand beginning an action · a visible state change · a cutaway appearing · a layer separating · a pathway activating · a comparison completing · a reaction becoming readable.

**Continuous-process exception.** A procedural shot may run longer if its physical state visibly advances: `touch → press → deform → separate → reveal → settle`. The camera can stay locked while the mechanism itself delivers a fact roughly every second.

## The two visual modes — alternate them
- **Narrative reenactment** — for incidents, decisions, reactions, consequences, human context. One principal character action per beat; only the objects needed to understand it; recognizable but stripped locations; large readable poses; hard cuts between wide, close, overhead, POV and detail. Emotion comes from **visible behaviour**, not atmospheric coverage.
- **Explanatory demonstration** — for mechanisms, internal processes, technical objects, anatomy, comparisons, transformations. One isolated object, body region or mechanism; cyan gradient space; macro, cutaway, transparent-body, cross-section or exploded view; oversized important components; stable colour ownership; direct actions — press, pull, rotate, separate, reveal, fill, compress, dissolve.

**Typical arc:**
```text
Incident or surprising image → immediate context → close observation
→ macro or internal reveal → visible mechanism → consequence
→ simple resolution or return to the hook
```
Never run a whole piece of identical diagrams or identical character shots.

## The input contract (what must arrive, or be asked for, before writing)
- **The narration or script** — the finished words, in order. This is the master clock.
- **The images** — character(s), key prop(s), and any style plate, tagged per `../chassis.md`. **One authority per attribute** (`../models/seedance.md`).
- **The banned list** — ask up front whether any attribute, look, or concept must never appear, and apply the vocabulary discipline in `../chassis.md`.
- **Aspect and length** — 9:16 by default; the finished piece is usually 30–60s assembled from several renders.

**You do NOT need a start frame per location.** Character references plus the repeated style, background-rule and lighting lines are enough for an independent hard cut, and fast editing conceals small environment differences. Reuse a previous final frame only for a continuous action, exact geometry, a transformation, or a deliberate return to the same composition.

## The workflow
1. **Break the narration into concrete clauses.** One clause, one visual construction. Clauses — not seconds — decide where cuts land.
2. **Assign a construction to each clause** using the translation table below, plus its visual mode and its grade token.
3. **Write the beat sheet** — every beat gets one focal subject, one main verb, one camera move, and an end state.
4. **Window into renders** — group beats into **4–10s** clips on clause boundaries, never mid-clause. An 8s clip holds **5–7 beats**. Keep **no more than about five materially different scenes** in one generation.
5. **Build the beat manifest** (the checkable artifact, and the edit sheet):

   | Clip | Narration clause | Mode | Construction + grade | Local beat times | Split fallback |
   |---|---|---|---|---|---|
   | 3 | "…the pressure builds…" | Explanatory | Chamber bows, amber stress — cyan void | 0 / 1.2 / 2.4 / 3.6 | 3A beats 1–2 · 3B beats 3–4 |

6. **Rebase to clip-local time** — every prompt runs from `0`. `local_t = global_t − clip_start`. Check one row by hand; this is the silent-error spot.
7. **Write one complete prompt per clip** on the style template, references and locks **verbatim** in every clip.
8. **Assemble in the edit** — join the clips, then add narration, captions and any critical label text in post.

## Script-to-visual translation
| Narration need | Visible construction |
|---|---|
| Repetition | Same composition with an obvious state change |
| Pressure | Chamber bows, or force visibly compresses |
| Blockage | Passage visibly narrows |
| Attention or attraction | Gaze direction, or a signal pathway activates |
| Accumulation | A layer grows thicker |
| Penetration | An object crosses a surface at visible depth |
| Failure | Load transfers, or a structure loses function |
| Smell or condition throughout a space | A distributed atmospheric volume |
| Exact quantity | Individually timed actions, or countable indicators |

**One main verb per beat:** reach, touch, press, open, close, lift, enter, travel, bind, activate, compress, split, dissolve, transfer, leave, return.

**Emotion becomes behaviour** — gaze, brows, head turn, lean, hand hesitation, interpersonal distance, voluntary continuation or reversal. Behaviour reads faster than mood lighting.

## Shot-line mechanics (shared with the music-video layer)
This layer and `music-video.md` are the **same cutting engine on a different clock** — that one is locked to lyric timestamps, this one to narration clauses. The shared mechanics:
- Each shot line **opens with its grade token**, states one action, and **closes with exactly one `Camera:` move**.
- Write `Hard cut to:` explicitly at each timestamp. Make adjacent shots **materially different** in angle, scale, framing or state, or they blend and morph.
- **Pre-declare a split fallback** per clip — two clean halves, same references and locks. Fire it only if the render smears.
- Repair an over-long shot by **subdividing it in place**, never by retiming the downstream clause-locked beats.

## Audio — narration goes in post
The generation carries ambience and foley only; the voice is added in the edit.
> **Audio:** environment ambience and synchronized foley, with clean space for narration added in editing.

Keep sound **literal**: a press gets a click, a door a latch, cloth a whoosh, a signal one pulse. Separate narration, ambience, foley, mechanism sound, sparse transitions, and at most one restrained reveal impact. Avoid constant whooshes and cinematic hits.

## Quality control — run before delivering
- **Frame** — understandable in one second? one obvious focal point? subject large enough? background simpler than subject? hands, props and mechanisms separated? caption area usable?
- **Timing** — a new fact every 0.8–1.8s? beats aligned to clauses? any shot lingering without evolving? would splitting reduce blur?
- **Continuity** — identities distinct and stable? wardrobe consistent? left and right consistent? limb chain plausible? prop scale stable? repeated actions reset between counts?
- **Explanation** — is the mechanism shown, not just a reaction? is every arrow, particle, highlight and cutaway functional? are colours consistent with their owned function? are global conditions shown globally? are comparisons countable and honest?
- **Text** — is generated text truly necessary? label stationary and front-facing? post replacement planned?

## Delivery format (extends the chassis output format)
Every clip package contains: the **one complete fenced prompt** · **duration** · **generation mode** · **aspect ratio** · the **ordered asset list** as `1 — @image_1 — file (role)` · **the narration clause(s) this clip covers** · and a **brief risk note only when a known failure is likely**. Never a fragment or a "same as the last one but…" diff.

## Symptom → fix (this layer)
| Symptom | Fix |
|---|---|
| A five-second paragraph drifts or smears | Timestamp smaller beats; split the clip into two shorter renders with identical references and locks. |
| Adjacent shots morph instead of cutting | Change angle, scale or state between them; write `Hard cut to:` at each timestamp. |
| The action reads too small on a phone | Fill 55–90% of the frame with the subject; move close when the narration names it. |
| Camera drifts and reveals nothing | Aim one move per beat at the active subject; use a locked camera when the mechanism itself evolves. |
| Several actions smear together | One subject and one verb per timestamp; never put independent actions in one block. |
| A global condition emits from one small point | Define the full volume and distribution across the whole intended space. |
| A polished set competes with the fact | Reduce the location to three to five primitives; raise fill and simplify the light. |
| The look drifts shot to shot | Repeat the grade token on every shot line, and keep the background rule and lighting lines in every clip. |

*Confidence: the cadence, mode split, translation table and QC list come from a real study calibrated on public shorts plus observed render failures. The clause-map, manifest, rebasing and assembly workflow are adapted from the proven music-video layer and are flagged v1 — calibrate on your first production run and fold wins back into `../models/seedance.md`.*
