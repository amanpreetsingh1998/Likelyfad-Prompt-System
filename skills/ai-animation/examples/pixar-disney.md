# Examples — Pixar / Disney 3D (worked draft, v1 — test & calibrate)

> **Not yet production-tested.** Drafted from the chassis + research to show the shape. Your team runs the first real Pixar ad and we tune from the feedback, folding wins back into `models/seedance.md`. Swap the character/product/brand for your own.

A single **15-second multi-scene** generation — one animated mascot carries the whole ad across three scenes (talking-head hook → b-roll → hero), from one start frame + a character reference + a product image. This is the default shape: one render, multiple scenes, no per-scene start frame.

## 15s multi-scene ad — canonical prompt

```
References: Use @image1 as the first frame and the world (a bright sunny kitchen). Use @image2 as the character — a rounded, friendly cartoon honey-bear mascot; keep the same face, design, and honey-gold fur throughout. Use @image3 as the product — a jar of "GoldenSpoon" honey; preserve its label, shape, and colors exactly.

Style: 3D animated feature film, Pixar/Disney-style render — keep this exact animation render style, character design, and color palette consistent from the first frame to the last. Smooth, appealing, expressive animation.

Format: vertical 9:16, 15 seconds, talking-head + b-roll animated ad.

Setup: the honey-bear mascot in a sunny kitchen, holding the GoldenSpoon jar. Same character identity throughout.

[0–5s] Scene 1 — hook: the bear looks at camera, big expressive eyes, brows lifting with excitement, a small anticipation dip before it leans in and taps the jar twice on "real." He says: "Okay, this honey is actually real." Accurate lip sync, natural pace, in English. Camera: slow smooth push-in, eased.

[5–10s] Scene 2 — b-roll: same bear, same kitchen, tips the jar and a thick golden ribbon of honey pours onto a stack of pancakes; the honey stretches and settles with believable weight, steam curling up. No dialogue here. Camera: gentle downward crane following the pour, eased.

[10–15s] Scene 3 — hero: the bear holds the jar up beside its cheek, label to camera, a warm satisfied grin, ears giving a little follow-through bounce as it settles into the pose. He says: "One spoon. You'll get it." Accurate lip sync. Camera: slow orbit to a clean hero framing, eased to a stop.

Voice / Audio: warm, upbeat, friendly male mascot voice, mid-energy and playful; slight emphasis on "real" and "one spoon." Ambient: soft sunny-kitchen room tone, a light honey-drizzle sound on the pour. No music.

Closing: keep the same bear face, design, and honey-gold fur, and the same Pixar/Disney render style, consistent across all three scenes.
```

**Duration:** 15 seconds.
**Assets to use, in order:** 1) `@image1` (first frame + world) · 2) `@image2` (character) · 3) `@image3` (product). No external audio.

## Why it's built this way (the animation deltas)
- **One 15s multi-scene render**, not three clips — the character carries across scenes; the b-roll pour needs no separate start frame. Saves the video team time.
- **Lean text, image-led** — no written character bible or render-token stack; identity + look come from `@image2` and the start frame. Only the three affirmative anchors (role tag, identity lock, style anchor) hold it.
- **Affirmative only** — "No music" is the one allowed content note; there's no "no realism / no photoreal" (Seedance has no negative field — those backfire).
- **Head moves while speaking** — unlike the realistic system, the talking bear nods/leans on its lines (Seedance syncs mouth + head together).
- **Smooth virtual camera** — eased push-in / crane / orbit, one move per scene; no "handheld jitter."

## To calibrate (fold wins back into `models/seedance.md`)
Run it, then note: did the character hold across all three scenes? did the style stay Pixar (no photoreal creep)? did lip-sync land? was 15s / 3 scenes too much? Adjust, and log the fix.
