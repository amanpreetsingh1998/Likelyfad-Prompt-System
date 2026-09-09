---
style: direct-3d-explainer
aliases: zack-d, zack-d-style, explainer, direct 3d explainer
version: 1.0.0
updated: 2026-09-09
---

# Style — Direct 3D Explainer (the "Zack D" style)

Fast, high-retention vertical 3D explainer: **semi-realistic, game-engine-like** characters and props, sparse functional backgrounds, bright phone-screen readability. Every second delivers a **new readable visual fact**. This is the style people mean when they say *"Zack D style"*.

> **This is NOT the Pixar path.** It's a separate style with its own look, camera, lighting, and timing. Don't blend the two files. Timing and narration grammar for this style live in `../delivery/explainer.md` — load both.

> **Provenance:** an independent study of a fast visual-explainer language, calibrated against public shorts. Apply the observable grammar — clarity, pacing, scale changes, cutaways, physical demonstrations. **Never** copy any channel's name, logo, voice, branding, recurring characters, or individual scenes. The file is named for the *format*, not the creator.

## How it differs from `pixar-disney-3d.md` (read once, then don't mix)
| | Pixar/Disney 3D | Direct 3D explainer |
|---|---|---|
| Characters | Rounded, cute, feature-film | Semi-realistic, game-engine faces, strong silhouettes |
| Backgrounds | The world in the start frame | Cyan void, or a location built from 3–5 primitives |
| Lighting | Soft, warm, cinematic | Bright frontal key, high fill, saturated, readable |
| Camera | Slow eased dolly / orbit / crane | Quick push, snap reframe, short track, or locked |
| Motion | Animation principles, squash & stretch | Explanatory mechanism — press, separate, reveal |
| Length | One 15s multi-scene render | 4–10s renders, assembled in the edit |
| Cadence | ~3–4 scenes in 15s | A new fact every 0.8–1.8s |

## The one doctrinal break: this style's prompt DOES carry background and lighting
Everywhere else in this skill, the start frame carries the look and the prompt stays lean. **This style is the exception.** It hard-cuts to a new stripped location or a cyan void every second or so, and no single start frame can carry that forward. So the prompt gets two extra standing lines — a **Background rule** and a **Lighting/color** line — right after the style anchor. Everything else stays lean: references carry appearance, text carries motion.

## The style anchor (paste this — affirmative, no negatives)
> **Visual lock:** semi-realistic 3D explainer animation, clean synthetic surfaces, strong readable silhouettes, bright saturated phone-screen contrast — keep this exact render style and palette consistent from the first frame to the last.

## Characters
Semi-realistic proportions suited to the subject, slightly stylized game-engine-like faces, simple sculpted hair masses, clean synthetic skin and clothing, moderate detail, **expressions readable at phone size**. Steer positively toward this. Do not write the cute-proportions or photographic-skin wording into a prompt even to reject it — see Writer-notes below.

## Backgrounds — pick one per shot
1. **Abstract explainer space** — cyan-to-blue gradient, optional faint grid, plain floor and shadow catcher, one subject. Use for mechanisms, anatomy, internal process, comparison.
2. **Stripped location** — three to five large necessary objects, broad wall/floor/sky planes, minimal texture, almost no decoration. Use for human context and reenactment.

**Sufficient constructions** — a location needs only this much:
```text
Bedroom  = bed + chair + window + door plane
Office   = desk + chair + monitor + wall
Hospital = bed + rail + monitor + window plane
Street   = road strip + curb + building plane + vehicle
Workshop = table + tool + wall + storage shape
```
The background supports the fact. It is never a hero asset.

## Scale and composition
- The main subject fills **55–90% of the frame**. Edge cropping is fine when it aids clarity.
- Establishing shots are brief and utilitarian. Move close the moment narration names the object or action.
- Keep the **lower 15–20% simple** — captions live there.

## Lighting (standing prompt line)
> **Lighting:** bright frontal or upper-front key, strong readable fill, clear edge separation, simple contact shadows, modest ambient occlusion, saturated phone-screen contrast.

Environmental light may set time or mood, but faces, hands, props, and mechanisms stay visible.

## Color ownership — color explains function
Assign a colour to a function and keep it for the whole piece. Decorative particles and random accents weaken clarity.

| Function | Colour |
|---|---|
| Airflow, clean motion, neutral force | Pale cyan |
| Stress, warning, important contact | Amber / yellow |
| Contamination or problem material | Brown, red, or dark amber |
| Active biological or signal pathway | Magenta-pink |
| Neutral anatomy | Ivory, muted rose, soft red |
| Technical background | Cyan / blue |

## Materials
```text
Skin: clean synthetic CGI surface, restrained detail.   Hair: sculpted clumps, clear silhouette.
Fabric: basic weave, readable folds, stable colour.     Metal: clean satin, simple highlights.
Plastic: molded form, uniform finish.                   Glass: readable thickness, controlled transparency.
Anatomy: smooth educational forms, strong layer separation.
```
Material sophistication must never compete with the mechanism.

## Camera for this style
Preferred views: frontal demonstration, three-quarter medium, extreme close-up, overhead, POV, side cross-section, transparent cutaway, functional orbit.

**One move per beat**, drawn from: quick push-in · short pullback · snap reframe · short lateral or vertical track · brief explanatory orbit · **locked camera when the mechanism itself evolves**.

Camera motion points at the fact. Steer away from decorative choreography, slow prestige drifts, long rack-focus handoffs, and any move that reveals nothing — as a *writing* decision, not as prompt text.

## Writer-notes are never prompt text
Every "avoid / don't default to" line in this file is guidance **to you**. Naming a concept summons it, even negated, and Seedance has no negative field (`../models/seedance.md`). Convert each one to what you *do* want:

```text
smooth stabilized camera        clean correct five-finger hands
simple cyan background          fully covered adult characters
one intact object               bright even readable lighting
```

## Fill-in template
Fill the `[BRACKETS]`; keep the anchors as written. Beat timing and the narration map → `../delivery/explainer.md`. Reference roles → `../models/seedance.md`.

```
References: Use @image1 as the [character identity and wardrobe authority]. Use @image2 as the [prop geometry and colour authority]. [One authority per attribute.]

Visual lock: semi-realistic 3D explainer animation, clean synthetic surfaces, strong readable silhouettes, bright saturated phone-screen contrast — keep this exact render style and palette consistent from the first frame to the last.

Background rule: [cyan-to-blue gradient explainer space with a plain floor and one subject] / [stripped location built from: OBJ + OBJ + OBJ + plane].

Lighting/colour: bright frontal key, strong fill, clear edge separation, simple contact shadows, saturated contrast. [Colour ownership: FUNCTION is PALE CYAN, FUNCTION is AMBER.]

Format: vertical 9:16, [N] seconds, [N] beats, a new readable visual fact every [0.8–1.8s].

[0–Xs] [grade token]. [One subject performs one action]. Camera: [one move].
[Xs] Hard cut to:
[X–Ys] [grade token]. [Next fact]. Camera: [one move].

Motion: [verbs, state changes, timing, end state].
Audio: [ambience and synchronized foley, with clean space for narration added in editing].
Continuity: [identity, geometry, colour, and state invariants].
```

## Notes
- Two standing lines this style adds that no other style uses: **Background rule** and **Lighting/colour**. Keep both in every prompt.
- Repeat the **grade token at every shot line** — at this cut density the single style line is not enough to hold the look.
- Any on-screen text, number, or label belongs to the edit, not the generation (`../models/seedance.md` → Text & labels).
