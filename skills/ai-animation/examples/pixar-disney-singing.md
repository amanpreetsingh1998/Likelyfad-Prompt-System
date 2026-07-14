# Examples — Pixar / Disney 3D, sung delivery (worked draft, v1 — test & calibrate)

> **Not yet production-tested.** Drafted from `references/delivery/singing.md` + research to show the shape. Your team runs the first real sung generation and we tune from the feedback, folding wins back into `delivery/singing.md` and `models/seedance.md`. Swap the character/song/brand for your own.

Two shapes: a single **≤14s sung jingle ad** (one render), and the **full-song segment pattern** (a chunked music video). Both assume the song arrived finished (e.g. from Suno) with its lyrics.

## 1) 12s sung jingle ad — canonical prompt

One render: the mascot sings an 8s jingle hook to camera, then a 4s sung-montage product beat. The supplied track (`@audio1`, 12s) is the master timing.

```
References: Use @image1 as the first frame and the world (a bright sunny kitchen). Use @image2 as the character — a rounded, friendly cartoon honey-bear mascot; keep the same face, design, and honey-gold fur throughout. Use @image3 as the product — a jar of "GoldenSpoon" honey; preserve its label, shape, and colors exactly. Lip-sync the character's singing to @audio1 — @audio1 is the only music and the master timing.

Style: 3D animated feature film, Pixar/Disney-style render — keep this exact animation render style, character design, and color palette consistent from the first frame to the last. Smooth, appealing, expressive animation.

Format: vertical 9:16, 12 seconds, sung jingle ad.

Setup: the honey-bear mascot in a sunny kitchen, holding the GoldenSpoon jar. Same character identity throughout.

[0–8s] Scene 1 — sung hook, on-screen singer: the bear sings to camera, front-facing, medium-close so the mouth is featured. Accurate sung lip sync, in English. He sings: "Golden mornings, golden spoon — real honey makes the whole day bloom." Delivery: bright and bouncy, riding the beat; a little anticipation dip into the downbeat, brows lifting on "real," arms opening wide on "bloom" with follow-through in the ears. Camera: slow smooth push-in, eased, one move for the whole phrase.

[8–12s] Scene 2 — sung montage, product beat: the vocals carry over b-roll — the same bear slides the jar label-forward to camera and a golden ribbon of honey loops behind it, stretching and settling with believable weight on the music's peaks. No featured mouth here. Camera: gentle eased orbit to a clean hero framing, landing on the final beat.

Voice / Audio: sung performance lip-synced to @audio1; @audio1 is the only music and the master timing. Soft sunny-kitchen room tone under the track.

Closing: keep the same bear face, design, and honey-gold fur, and the same Pixar/Disney render style, consistent across both scenes.
```

**Duration:** 12 seconds.
**Assets to use, in order:** 1) `@image1` (first frame + world) · 2) `@image2` (character) · 3) `@image3` (product) · 4) `@audio1` (the finished 12s jingle track — lip-sync source + master timing).

> **If the timing wanders off the track:** re-run with the jingle converted to a black-screen MP4 attached as `@video1` ("follow the song in @video1 — it is the master timing"), per the fidelity ladder in `delivery/singing.md`.

## 2) Full song — the segment pattern

A 40s song becomes ~3 segment renders, split at phrase boundaries, assembled in the edit. Every segment reuses the SAME references and the SAME lock wording; only the scene, lyrics, and camera change:

| Segment | Track piece | Shape |
|---|---|---|
| 1 | 0–13s (verse) | on-screen singer — establish the world, sung hook to camera |
| 2 | 13–26s (build) | sung montage — b-roll riding the build, action peaks on downbeats |
| 3 | 26–40s (chorus) | on-screen singer — biggest performance, belt the chorus, hero framing on the final beat |

Per segment: same `@image1`/`@image2` (+ product if featured), same identity lock + style anchor verbatim, that segment's audio piece as `@audio1`, and **only that segment's lyric lines transcribed**. Lyric text on screen is added in the edit, never generated.

## Why it's built this way (the sung deltas)
- **The song arrives finished** — the prompt never asks the model to compose vocals; it lip-syncs to the supplied track (the reliable path).
- **Lyrics are transcribed in the beats** even though the track is attached — audio alone gets misheard; track + transcript together nail the mouth shapes.
- **The track is declared "only music and master timing"** — blocks invented extra music, and buys the free beat sync (camera and action land on the rhythm).
- **Mouth featured only where lip-sync binds** — singer beats are front-facing medium/close; montage beats move freely.
- **≤14s per render** — the full-song pattern is segments + edit assembly, not one long ask.

## To calibrate (fold wins back into `delivery/singing.md` + `models/seedance.md`)
Run it, then note: did the sung words land or mush? did the timing hold to the track (or need the black-screen upgrade)? did the character survive across segments? did beat sync actually show up? Adjust, and log the fix.
