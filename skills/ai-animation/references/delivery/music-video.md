# Delivery layer — Beat-cut music video (song + SRT → hard cuts on lyric & beat)

> The main path for **full songs** (minutes long, e.g. from Suno). No lip-sync — scenes **hard-cut in time with the beat and with what the lyrics are saying**. Swaps into the chassis's Voice/Audio block and takes over scene-beat timing (Sections 5–6). Load this file only for music-video jobs. (A character who must visibly *sing* a line → `singing.md`.)

## The core reframe: the SRT is for YOU, not for the video model
There are two models in this pipeline. **You** (the prompt-writer) read the full SRT + brief and do all the timing intelligence — mapping, windowing, arithmetic. **The video model** receives only what it can obey: per-segment prompts with timestamped scene beats, tagged images, and pacing language. **Never paste the SRT into a video prompt** — it's your input, not the model's.

## The input contract (what must arrive finished)
- **The song** — the finished full-length track.
- **The SRT** — timestamped lyrics for that track (Suno's aligned lyrics, or Whisper: `whisper song.mp3 --output_format srt`).
- **The BPM + the Suno style prompt** — the beat grid and the vibe vocabulary (ask for them; BPM is detectable if missing).
- **The brief / script / story context** — what the video should show, section by section.
- **The images** — character / world / product, tagged as usual (`chassis.md` Section 1).

## The workflow (deterministic timing, generative visuals)
1. **Lyric-to-scene map** — from the brief, assign each lyric section (verse/build/chorus/bridge) a scene: location, action, energy. This is the creative step; everything after is computation.
2. **Compute the beat grid** — one bar (4/4) = `240 ÷ BPM` seconds (120 BPM → 2.0s; 90 BPM → ~2.67s). Default cut cadence: every 2 bars in verses, every 1–2 bars in the chorus.
3. **Window the song into segments** — walk the SRT and cut generation windows of **≤14s** (13s safe), edges on **lyric-line boundaries snapped to the nearest downbeat** — never mid-word, never mid-bar.
4. **Build the segment manifest** (the checkable artifact — eyeball it before generating anything):

   | Seg | Song window | Lyric lines in window | Scene (from the map) | Local cut points |
   |---|---|---|---|---|
   | 3 | 0:26.0–0:39.5 | "…chorus lines…" | B — rooftop, golden hour | 0 / 3.4s / 7.2s / 10.8s |

5. **Rebase every timestamp** — prompts run on segment-local time: `local_t = srt_t − segment_start` (a line at 0:29.4 in a segment starting 0:26.0 → `[3.4s]`). **This subtraction is the #1 silent-error spot — do it in the manifest, then check one row by hand.**
6. **Write one prompt per segment** on the chassis — same tagged references + identity lock + style anchor **verbatim in every segment**; scene beats carry the hard cuts at the local timestamps.
7. **Assemble in the edit** — the full song is laid over the cut-together visuals. The manifest doubles as the edit sheet; nudge any cut the model landed a few frames off.

## Audio: silent by default
Since nothing lip-syncs, **generate silent visuals** — the song is added in the edit, and the 15s audio-input limit stops existing as a constraint. Attach that segment's audio slice (`@audio1 as rhythm reference only — no dialogue, no lip-sync`) **only** when you want the model's native beat-pull on motion *within* a scene (dance, marching, impacts on the beat). Slice per segment only in that case: `ffmpeg -i song.mp3 -ss 26.0 -t 13.5 seg3.mp3` (re-encode, don't `-c copy` — copy cuts land off-time).

## Writing the segment's beats (drops into chassis Sections 5–6)
Per cut, one line: local timestamp → `hard cut to` → the shot + one camera move. Pacing language comes from the style prompt + BPM, stated affirmatively:

> *Format: vertical 9:16, 13.5 seconds, music-video segment 3 of 12 — silent visuals, the song is added in the edit. Pacing: energetic 128 BPM synth-pop; snappy motion; every move lands on a beat.*
>
> *[0–3.4s] Rooftop at golden hour, the fox mid-leap between AC units, coat flaring with follow-through. Camera: fast eased lateral track.*
> *[3.4s] Hard cut to: close-up, she lands and looks up, eyes catching the sun. Camera: static framing, she rises into it.*
> *[7.2s] Hard cut to: wide — the whole skyline behind her as she throws her arms out on the chorus peak. Camera: slow eased push-in.*
> *[10.8s] Hard cut to: the product on the parapet, label to camera, her hand entering to grab it. Camera: locked hero framing.*
>
> *Voice / Audio: none — silent visuals for edit assembly.*

## What the timing can and can't promise
In-generation cut timing is **good, not frame-exact** — the model lands `[3.4s]` within a fraction of a second. On-lyric scene changes read fine at that tolerance; the edit does the final frame-exact nudge against the manifest. Never promise the team beat-perfect cuts straight out of generation.

## Symptom → fix (music-video-specific starting points)
| Symptom | Fix |
|---|---|
| Cuts land in the wrong places entirely | Check the rebase arithmetic in the manifest (global vs. local time) — the usual culprit is an un-subtracted segment start. |
| Model blends/morphs between shots instead of cutting | Say `hard cut to:` explicitly at each timestamp; one distinct location/framing change per cut (near-identical shots invite morphing). |
| Too many cuts → smeared, chaotic output | Cap at ~4–5 cuts per segment; slow the cadence to every 2 bars; move the faster cutting to the edit. |
| Motion ignores the beat (when it matters) | Attach the segment's audio slice as `rhythm reference only`, and write the action peaks on the downbeat timestamps. |
| Character drifts across the many segments | Same fixes as multi-scene ads (`models/seedance.md`): one constant character reference + identical lock wording in every segment. |
| Energy feels flat vs. the song | Map chorus vs. verse in the lyric-to-scene step — bigger action, tighter cut cadence, and a pacing line ("euphoric chorus peak") on chorus segments. |

*Confidence: the beat-grid math, SRT rebasing, and edit-side assembly are deterministic by construction; in-generation `hard cut` adherence, cut-count ceilings, and rhythm-reference behavior are informed starting points — calibrate on the first real song and fold wins back here and into `models/seedance.md`.*
