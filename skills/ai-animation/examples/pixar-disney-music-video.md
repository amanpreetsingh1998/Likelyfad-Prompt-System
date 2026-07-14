# Examples — Pixar / Disney 3D, beat-cut music video (worked draft, v1 — test & calibrate)

> **Not yet production-tested.** Drafted from `references/delivery/music-video.md` to show the full computation: SRT in → manifest → one segment prompt out. Your team runs the first real song and we tune from the feedback. Swap the character/song/brand for your own.

The job: a full Suno song becomes a beat-cut music video — **no lip-sync**, scenes hard-cutting with the beat and the lyrics. The song is added in the edit; the generations are silent visuals.

## The inputs (what arrived)
- **Song:** "Golden Morning" — 3:12, **120 BPM** (bar = 2.0s), Suno style prompt: *"upbeat feel-good acoustic pop, sunny, hand-claps, warm."*
- **SRT:** timestamped lyrics for the full track.
- **Brief:** the honey-bear's morning — wake up groggy → kitchen ritual → golden-hour joy; GoldenSpoon jar is the hero object.
- **Images:** `@image1` start frame (sunny kitchen), `@image2` character (honey-bear), `@image3` product (jar).

## Step 1 — lyric-to-scene map (the creative step)
| Song section | Lyrics say | Scene |
|---|---|---|
| Verse 1 (0:00–0:16) | waking up slow, grey morning | A — bedroom, groggy bear, muted light |
| Build (0:16–0:26) | something's waiting downstairs | B — hallway/stairs, growing light |
| Chorus 1 (0:26–0:42) | "golden morning… whole day blooms" | C — kitchen, honey ritual, full sun |
| … | … | … |

## Step 2 — the grid + windows
120 BPM → bar = 2.0s. Cut cadence: every 2 bars (4.0s) in the verse, every bar-to-2-bars in the chorus. Windows of ≤14s, edges on lyric-line starts snapped to downbeats.

## Step 3 — the segment manifest (check one row's arithmetic by hand before generating)
| Seg | Song window | Lyric lines in window (from SRT) | Scene | Local cut points |
|---|---|---|---|---|
| 1 | 0:00.0–0:12.0 | "Slow eyes open… grey ceiling stares back" | A | 0 / 4.0 / 8.0 |
| 2 | 0:12.0–0:26.0 | "But something smells like sunshine… down the stairs" | A→B | 0 / 4.0 / 8.0 / 12.0 |
| 3 | 0:26.0–0:39.5 | "Golden morning, golden spoon… whole day blooms" (chorus) | C | 0 / 3.5 / 7.5 / 11.5 |
| … | … | … | … | … |

Rebase check, seg 3: chorus line starts at **0:29.5** in the SRT → `29.5 − 26.0 =` **`[3.5s]`** local. ✓

## Step 4 — one segment's prompt (seg 3, the chorus)

```
References: Use @image1 as the first frame and the world (a bright sunny kitchen). Use @image2 as the character — a rounded, friendly cartoon honey-bear mascot; keep the same face, design, and honey-gold fur throughout. Use @image3 as the product — a jar of "GoldenSpoon" honey; preserve its label, shape, and colors exactly.

Style: 3D animated feature film, Pixar/Disney-style render — keep this exact animation render style, character design, and color palette consistent from the first frame to the last. Smooth, appealing, expressive animation.

Format: vertical 9:16, 13.5 seconds, music-video segment 3 of 14 — silent visuals, the song is added in the edit. Pacing: upbeat feel-good 120 BPM acoustic pop; warm and sunny; every action lands on a beat.

Setup: the honey-bear in the sun-flooded kitchen at the joyful peak of his morning. Same character identity throughout.

[0–3.5s] The bear slides across the kitchen floor in socks, arms wide, morning sun blasting through the window; his ears bounce with follow-through as he stops at the counter. Camera: fast eased lateral track with him.

[3.5s] Hard cut to: close-up — the jar lid pops open and a curl of golden light rises; his eyes go huge with delight. Camera: static framing, slight eased push.

[7.5s] Hard cut to: top-down — a thick golden ribbon of honey spirals onto pancakes, stretching and settling with believable weight, landing its loops on the beat. Camera: locked overhead, slow eased rotate.

[11.5s] Hard cut to: wide — the bear hoists the jar overhead like a trophy, label to camera, pure joy, tail wag with overlap. Camera: slow eased push-in to a hero framing.

Voice / Audio: none — silent visuals for edit assembly.

Closing: keep the same bear face, design, and honey-gold fur, and the same Pixar/Disney render style, consistent across all shots.
```

**Duration:** 13.5 seconds.
**Assets to use, in order:** 1) `@image1` (first frame + world) · 2) `@image2` (character) · 3) `@image3` (product). **No audio attached** — silent by default; attach a `rhythm reference only` slice just for segments where motion must ride the beat (e.g. a dance segment).

## Step 5 — assembly
Cut the segments together on the manifest's global timestamps, lay the full song over, nudge any cut the model landed a few frames off. Lyric/caption overlays happen here, never in generation.

## Why it's built this way (the music-video deltas)
- **The SRT never enters the prompt** — the prompt-writer computes with it; the model only sees rebased local timestamps.
- **Silent generations** — no lip-sync means no audio needed; the 15s audio limit stops existing, and a 3-minute song is just ~14 manifest rows.
- **Cuts are math** — lyric starts snapped to the 120 BPM downbeat grid; the edit makes them frame-exact.
- **`Hard cut to:` is written explicitly** at each timestamp with a distinct framing change — near-identical shots invite morphing instead of cutting.
- **Same references + lock wording in all 14 segments** — that's what holds the bear together across the whole video.

## To calibrate (fold wins back into `delivery/music-video.md` + `models/seedance.md`)
Run one full song, then note: did the cuts land near their timestamps? did any shot morph instead of cutting? did 4 cuts/segment hold or smear? did the character survive all segments? Adjust, and log the fix.
