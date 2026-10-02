# Examples — Pixar / Disney 3D, beat-cut music video (worked draft, v2 — calibrated to the first production run)

> Prompt-side calibrated against a real multi-segment production; **playback validation still pending**. Shows the full method: SRT in → manifest → one fast-cut segment prompt out, with the delivery ritual around it. Swap the character/song/brand for your own.

The job: a full Suno song becomes a beat-cut music video — **no lip-sync**, scenes hard-cutting with the lyrics and the beat. The song is added in the edit; the generations are silent visuals.

## The inputs (what arrived)
- **Song:** "Golden Morning" — 3:12, **120 BPM** (bar = 2.0s), Suno style prompt: *"upbeat feel-good acoustic pop, sunny, hand-claps, warm."*
- **SRT:** timestamped lyrics for the full track.
- **Brief:** the honey-bear's morning — wake up groggy → kitchen ritual → golden-hour joy; GoldenSpoon jar is the hero object, **label saved for the close-out segment**.
- **Banned list (asked up front):** user said none — list starts empty, grows if a render misbehaves.
- **Images:** `@image1` start frame (sunny kitchen), `@image2` character (honey-bear), `@image3` product (jar).

## Step 1 — lyric-to-scene map (the creative step)
| Song section | Lyrics say | Scene + thread grade |
|---|---|---|
| Verse 1 (0:00–0:16) | waking up slow, grey morning | A — bedroom, groggy bear — **cool muted grade** |
| Build (0:16–0:26) | something's waiting downstairs | B — hallway/stairs — grade warming |
| Chorus 1 (0:26–0:42) | "golden morning… whole day blooms" | C — kitchen ritual — **warm golden grade** |
| … | … | … |

## Step 2 — clocks
**The SRT lyric timestamps are the master clock — cuts land where the words land.** The 120 BPM grid (bar = 2.0s) is the secondary clock: it fills cut points between lyric events and sets the **~1.5s per-shot ceiling**. No shot lingers.

## Step 3 — the segment manifest (check one row's arithmetic by hand before generating)
| Seg | Song window | Lyric lines in window (from SRT) | Scene + grade | Local cut points | Split fallback |
|---|---|---|---|---|---|
| 1 | 0:00.0–0:12.0 | "Slow eyes open… grey ceiling stares back" | A, cool | 0 / 1.4 / 2.6 / 4.0 / 5.2 / 6.6 / 8.0 / 9.3 / 10.7 | 1A shots 1–5 · 1B shots 6–9 |
| 2 | 0:12.0–0:26.0 | "But something smells like sunshine… down the stairs" | A→B, warming | 0 / 1.2 / 2.4 / 3.8 / 5.0 / 6.4 / 7.8 / 9.0 / 10.4 / 11.8 / 13.0 | 2A / 2B |
| 3 | 0:26.0–0:39.5 | "Golden morning, golden spoon… whole day blooms" (chorus) | C, warm | 0 / 1.2 / 2.3 / 3.5 / 4.6 / 5.8 / 7.0 / 8.1 / 9.3 / 10.4 / 11.6 / 12.5 | 3A shots 1–6 · 3B shots 7–12 |
| … | … | … | … | … | … |

Rebase check, seg 3: chorus line starts at **0:29.5** in the SRT → `29.5 − 26.0 =` **`[3.5s]`** local. ✓

## Step 4 — one segment's delivery (seg 3, the chorus)

**Locked:** one character (honey-bear, same design throughout) + the jar at natural scale, **label not featured** (saved for close-out); kitchen thread = warm golden grade; all props unlabeled; fast punchy editing, calm character motion.

```
References: Use @image1 as the first frame and the world (a bright sunny kitchen). Use @image2 as the character — a rounded, friendly cartoon honey-bear mascot; keep his face, design, and honey-gold fur consistent in every shot he appears in. Use @image3 as the product — a jar of honey; keep its shape and design consistent, held naturally at casual everyday scale. One character and one product.

Style: 3D animated feature film, Pixar/Disney-style render — keep this exact animation render style, character design, and color palette consistent from the first frame to the last. Smooth, appealing, expressive animation, cinematic depth of field with soft creamy bokeh.

Format: vertical 9:16, 13.5 seconds, music-video segment 3 of 14 — silent visuals, the song is added in the edit. Pacing: upbeat feel-good 120 BPM acoustic pop; the editing and camera are fast and punchy with rapid hard cuts every second or so, while the character moves at a calm, believable, slightly slow-motion pace. The joyful golden peak of the morning.

Setup: the @image2 character in the sun-flooded kitchen at the happy peak of his morning ritual with the small honey jar. The jar stays small and casual in his paws, held naturally. Same identity throughout.

[0–1.2s] Warm golden grade. The @image2 character slides across the kitchen floor in socks, arms wide, sun blasting through the window. Camera: fast eased lateral track with him.

[1.2s] Hard cut to: warm grade. Close on his socked feet gliding to a stop, ears bouncing with follow-through. Camera: low and close on the slide.

[2.3s] Hard cut to: warm grade. His paws lift the small jar from the counter, an easy everyday gesture. Camera: close on the jar in his paws.

[3.5s] Hard cut to: warm grade. The lid pops open and a curl of golden light rises; his eyes go huge with delight. Camera: tight on his delighted face.

[4.6s] Hard cut to: warm grade. A thick golden ribbon of honey starts to pour onto pancakes. Camera: close on the ribbon leaving the jar.

[5.8s] Hard cut to: warm grade. Overhead — the honey spirals onto the stack, stretching and settling with believable weight. Camera: locked overhead on the spiral.

[7.0s] Hard cut to: warm grade. His face in profile watching the pour, pure anticipation. Camera: side close-up, eased drift.

[8.1s] Hard cut to: warm grade. He sets the small jar down easily on the counter, a light daily habit. Camera: on the casual set-down.

[9.3s] Hard cut to: warm grade. He lifts the plate of glistening pancakes with both paws, steam curling. Camera: eased rise with the plate.

[10.4s] Hard cut to: warm grade. Wide — he spins once through the sunbeam with the plate, tail wagging with overlap. Camera: smooth eased arc around him.

[11.6s] Hard cut to: warm grade. Close on his beaming face in full sun, eyes closing happily. Camera: still, tight on his joy.

Voice / Audio: none — silent visuals for edit assembly.

Closing: keep the @image2 character's face, design, and honey-gold fur consistent in every shot; the jar stays small and natural in scale with a consistent shape; keep the same warm golden sunlit Pixar/Disney render style across every shot.
```

**Duration:** 13.5 seconds.
**Assets to use, in order:**
1 — `@image1` — kitchen_start_frame.png (first frame + world)
2 — `@image2` — honeybear_character.png (character)
3 — `@image3` — goldenspoon_jar.png (product)
No audio attached — silent.

**Notes on this one:** 12 shots, longest 1.3s — nothing over the 1.5s ceiling; long chorus lines covered in multiple angles (the pour = 3 angles). Jar kept small/casual, label never pushed to camera — the hero/label moment waits for the close-out segment. Watch in playback: does the jar hold its shape across shots 3–8, and do the cuts actually cut (no morphing)? Split fallback ready: 3A shots 1–6 / 3B shots 7–12. Filter: low risk. Next: segment 4 — the first bite and the "whole day blooms" payoff.

## Step 5 — assembly
Cut the segments together on the manifest's global timestamps, lay the full song over, nudge any cut the model landed a few frames off. Lyric/caption overlays happen here, never in generation.

## Why it's built this way (the music-video deltas)
- **The SRT never enters the prompt** — the prompt-writer computes with it; the model only sees rebased local timestamps.
- **Lyric timestamps outrank the beat grid** — cuts land where words land; the grid fills the gaps and sets the ~1.5s ceiling.
- **Fast cuts, calm character** — the pacing line splits editing energy from character motion, so speed never reads as frantic.
- **Per-shot anchors** — every shot line opens with the thread's grade token and closes with one `Camera:` move; that's what holds the look at 12 cuts.
- **Silent generations** — no audio attached; the 15s audio limit stops existing, and a 3-minute song is just ~14 manifest rows.
- **Sequenced product reveal** — natural scale everywhere, label saved for one dedicated slow segment.
- **The ritual around the prompt** — Locked ledger on top, numbered assets, Notes block with playback watch-list and the pre-declared split fallback.

## To calibrate (fold wins back into `delivery/music-video.md` + `models/seedance.md`)
Run one full song, then note: did ~1s cutting hold or smear (did the split fallback fire)? did cuts land near their timestamps? did the character and product survive all segments? Adjust, and log the fix.
