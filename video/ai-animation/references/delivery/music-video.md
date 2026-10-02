# Delivery layer — Beat-cut music video (song + SRT → hard cuts on lyric & beat)

> The main path for **full songs** (minutes long, e.g. from Suno). No lip-sync — scenes **hard-cut in time with the lyrics and the beat**. Swaps into the chassis's Voice/Audio block and takes over scene-beat timing (Sections 5–6). Load this file only for music-video jobs. (A character who must visibly *sing* a line → `singing.md`.)

## The core reframe: the SRT is for YOU, not for the video model
There are two models in this pipeline. **You** (the prompt-writer) read the full SRT + brief and do all the timing intelligence — mapping, windowing, arithmetic. **The video model** receives only what it can obey: per-segment prompts with timestamped shot beats, tagged images, and pacing language. **Never paste the SRT into a video prompt** — it's your input, not the model's.

## The input contract (what must arrive, or be asked for, before writing)
- **The song** — the finished full-length track.
- **The SRT** — timestamped lyrics for that track (Suno's aligned lyrics, or Whisper: `whisper song.mp3 --output_format srt`).
- **The BPM + the music style prompt** — the beat grid and the vibe vocabulary (ask; BPM is detectable if missing).
- **The brief / story / script** — what the video shows, section by section; the characters and threads.
- **The images** — character(s) / world / product, tagged per `chassis.md` (two+ characters → the multi-character method there).
- **The banned list — ask up front:** ask the user whether any attribute, look, or concept must **never** appear (body types, styles, moods, clothing, tones). If they give one, apply the vocabulary discipline in `chassis.md` for the whole project; if they say none, proceed normally — and start the list the moment a render surfaces something unwanted.

## The workflow (deterministic timing, generative visuals)
1. **Lyric-to-scene map** — from the brief, assign each lyric section a scene: location, action, energy, and its **thread grade** (each location/timeline thread gets one locked color grade — e.g. warm = thread A, cool = thread B — kept for the whole video). This is the creative step; everything after is computation.
2. **Clocks** — **the SRT lyric timestamps are the master clock: cuts land where the words land.** The beat grid (one 4/4 bar = `240 ÷ BPM` seconds) is the *secondary* clock — use it to place cuts between lyric events and to set the shot ceiling, never to pull a lyric-driven cut off its word.
3. **Window the song into segments** — walk the SRT and cut generation windows of **≤14s** (13s safe), edges on lyric-line boundaries — never mid-word.
4. **Build the segment manifest** (the checkable artifact — eyeball it before generating anything):

   | Seg | Song window | Lyric lines in window | Scene + grade | Local cut points | Split fallback |
   |---|---|---|---|---|---|
   | 3 | 0:26.0–0:39.5 | "…chorus lines…" | B — rooftop, warm | 0 / 1.1 / 2.3 / 3.5 / … | 3A shots 1–5 · 3B shots 6–10 |

5. **Rebase every timestamp** — prompts run on segment-local time: `local_t = srt_t − segment_start` (a line at 0:29.4 in a segment starting 0:26.0 → `[3.4s]`). **This subtraction is the #1 silent-error spot — do it in the manifest, then check one row by hand.**
6. **Write one prompt per segment** on the chassis — same tagged references + identity locks + style anchor **verbatim in every segment**; shot beats carry the hard cuts at the local timestamps.
7. **Assemble in the edit** — the full song is laid over the cut-together visuals. The manifest doubles as the edit sheet; nudge any cut the model landed a few frames off.

## Pacing — fast cuts, calm characters
- **Per-shot ceiling, not a cut cap: no shot longer than ~1.5s** (≈ one bar at fast tempos), and no lingering ever. 10+ cuts in a full segment is normal, not a smell.
- **A long lyric line is covered in multiple angles of the same action** (wide → close → detail), never by holding one shot.
- **The speed lives in the editing and camera — the characters stay calm.** Write it into the Format line every time: *"the editing and camera are fast and punchy with rapid hard cuts, while the characters move at a calm, believable, slightly slow-motion pace."* Asking for "fast pace" without this split makes the characters frantic.
- **Pre-declare the split fallback** per segment in the manifest — two clean thematic halves (same references and locks). Fire it **only** if the rendered segment smears; it's the safety valve that lets cut density stay high.
- **Repairing a ceiling violation: subdivide the shot in place** — split it into two angles at the same boundaries. Never retime downstream cuts; they're lyric-locked.

## Audio: silent by default
Since nothing lip-syncs, **generate silent visuals** — the song is added in the edit, and the 15s audio-input limit stops existing as a constraint. Attach that segment's audio slice (`@audio1 as rhythm reference only — no dialogue, no lip-sync`) **only** when you want the model's native beat-pull on motion *within* a scene (dance, marching, impacts on the beat). Slice per segment only in that case: `ffmpeg -i song.mp3 -ss 26.0 -t 13.5 seg3.mp3` (re-encode, don't `-c copy` — copy cuts land off-time).

## Writing the segment's shots (drops into chassis Sections 5–6)
Per shot, one line with **three fixed anchors**: it **opens with the thread's grade token**, states the action on the tagged reference(s), and **closes with exactly one `Camera:` move**. At high cut counts, the once-per-prompt style line is not enough — the per-shot grade token is what holds the look shot to shot.

> *Format: vertical 9:16, 12.0 seconds, music-video segment 3 of 12 — silent visuals, the song is added in the edit. Pacing: driving 128 BPM synth-pop; the editing and camera are fast and punchy with rapid hard cuts every second or so, while the characters move at a calm, believable, slightly slow-motion pace.*
>
> *[0–1.1s] Warm golden-hour grade. The @image2 character mid-leap between rooftop AC units, coat flaring with follow-through. Camera: fast eased lateral track.*
> *[1.1s] Hard cut to: warm grade. Close on her boots landing, dust puffing on the beat. Camera: low and close on the landing.*
> *[2.3s] Hard cut to: warm grade. Her face tilts up, eyes catching the sun. Camera: tight eased push on her face.*
> *[3.5s] Hard cut to: warm grade. Wide — she throws her arms out against the skyline on the chorus peak. Camera: slow eased push-in.*
> *…(continue on the lyric timestamps)…*
>
> *Voice / Audio: none — silent visuals for edit assembly.*

## The product across segments — sequenced reveal
The product stays **incidental and at natural scale** through the body of the video — "small, casual, held naturally, natural everyday scale" woven into References, Setup, AND Closing (the model inflates products toward hero scale on its own). The **label/hero framing gets exactly one dedicated close-out segment** — a slow, simple shot where the label is featured cleanly. Featuring a label at fast-cut speed is how labels garble; every other prop in the video is affirmatively **unlabeled/blank** (readable text on props garbles — on-screen text belongs to the edit).

## Per-segment delivery ritual (what keeps a long production coherent)
- **Open with the "Locked:" ledger** — one line restating every standing decision (character/outfit locks, product-scale call, thread grades, design choices) so nothing silently drifts between segments.
- **Deliver the complete prompt every time** — never a fragment or a "same as segment N but…" diff.
- **Asset list as numbered lines:** `1 — @image_1 — <filename> (role)`.
- **Close with a Notes block:** known risks in this segment, what to watch in playback, the split fallback, and a one-line preview of the next segment.
- **Filter pre-check:** scan the segment for anything a generation filter may flag (distress, clinical/medical staging, etc.) and adjust before it's sent.
- **Audit, don't reassure:** when the user asks "is everything we agreed in there?", verify the segment line-by-line against the numbered locked-rules list and report each item — including misses. The rulebook grows over the project; keep it numbered.

## What the timing can and can't promise
In-generation cut timing is **good, not frame-exact** — the model lands `[3.4s]` within a fraction of a second. On-lyric scene changes read fine at that tolerance; the edit does the final frame-exact nudge against the manifest. Never promise the team beat-perfect cuts straight out of generation.

## Symptom → fix (music-video-specific starting points)
| Symptom | Fix |
|---|---|
| Cuts land in the wrong places entirely | Check the rebase arithmetic in the manifest (global vs. local time) — the usual culprit is an un-subtracted segment start. |
| Model blends/morphs between shots instead of cutting | Say `hard cut to:` explicitly at each timestamp; one distinct location/framing change per cut (near-identical shots invite morphing). |
| Rendered segment smears at high cut count | Fire the pre-declared split: generate the two thematic halves as separate renders (same references + locks), rejoin in the edit. |
| Characters look rushed, frantic, or angry | The pacing split line is missing or diluted — fast cuts belong to the editing/camera; restate the calm, slightly slow-motion character pace. |
| A shot exceeds the ~1.5s ceiling | Subdivide it into two angles at the same boundaries; never retime the downstream lyric-locked cuts. |
| Look drifts shot-to-shot within a segment | Open every shot line with the thread's grade token; keep the closing style-consistency line. |
| Motion ignores the beat (when it matters) | Attach the segment's audio slice as `rhythm reference only`, and write the action peaks on the downbeat timestamps. |
| Character drifts across the many segments | Same fixes as multi-scene ads (`models/seedance.md`): one constant reference set + identical lock wording in every segment. |
| Energy feels flat vs. the song | Map chorus vs. verse in the lyric-to-scene step — bigger action and tighter cutting on the chorus, and a pacing line ("euphoric chorus peak") on those segments. |

*Confidence: the beat-grid math, SRT rebasing, and edit-side assembly are deterministic by construction. The per-shot ceiling, pacing split, per-shot grade anchors, split fallback, and delivery ritual come from the first real production run (prompt-side, playback validation pending) — calibrate against renders and fold wins back here and into `models/seedance.md`.*
