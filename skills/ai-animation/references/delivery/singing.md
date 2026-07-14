# Delivery layer — Singing (a finished song + lyrics + sung lip-sync)

> The delivery mode that swaps into the chassis's **Voice / Audio block (Section 6)**. Everything else — references & roles, style anchor, scene beats, motion craft — stays exactly as `chassis.md` says. Load this file only for sung jobs. (Model mechanics for supplied audio → `models/seedance.md`.)

## The input contract (what must arrive finished)
- **The song** — a finished track (e.g. from Suno), delivered as segment(s) of **≤14 seconds** each (13s to be safe). We never ask the video model to *compose* the singing — generating vocals from lyrics alone is unreliable; lip-syncing to a supplied track is the reliable path. True music generation happens upstream, like images do.
- **The lyrics** — the exact text, with which lines fall in which segment.
- **The images** — start frame / character / world / product, tagged as usual (`chassis.md` Section 1).

## Two sung modes (pick per beat, mixable in one generation)
- **On-screen singer** — the character performs to camera, mouth featured: sung lip-sync binds. Frame medium/close, front-facing on the sung lines (same mouth-visibility rule as speech).
- **Sung montage / music-video b-roll** — the track plays over action with no featured mouth: lip-sync doesn't bind, the character and camera move freely with the music.

## The three rules that make sung lip-sync land
1. **Tag the track with its role.** *"Lip-sync the character's singing to @audio1."* An untagged track gets treated as mood music at best. A track used only for rhythm/mood is a different role — say which one it is.
2. **Always transcribe the lyrics in the prompt.** A tagged audio file alone gets misheard — the model replicates what it *thinks* it hears and fluffs words. Spelled-out lyrics + the attached track together produce dramatically better mouth shapes. Put the segment's exact lines in the scene beats, tied to the action.
3. **One segment per generation, ≤14s.** A full song is a series of segment renders (workflow below) assembled in the edit — never one long ask.

## Fidelity ladder — how to attach the song
1. **Default:** the tagged audio segment + transcribed lyrics.
2. **If rhythm/timing drifts** (output *sounds* similar but the intervals wander — common with music): convert the segment to a **black-screen MP4** and attach it as a *video* reference instead — the model follows video references much more tightly than raw audio, so the timing holds.
3. **Free win — beat sync:** a supplied track with a strong beat pulls camera moves and character actions onto the rhythm automatically. Write with it, not against it: one camera move per musical phrase, action peaks on the downbeats.

## Writing the sung Voice/Audio block (drops into Section 6)
State, in order: the delivery mode + track role → the performance character → the mix.

> *Sung performance: the character sings live on screen, lip-synced to @audio1 — accurate sung lip sync, in English. She sings: "…exact lyric lines for this segment…". Delivery: bright and playful, belting the last line, eyes closing on the high note. Audio: @audio1 is the only music and the master timing; soft room ambience under it.*

The supplied track **is** the mix — never ask for additional generated music on top; ambient/foley under it only if the brief asks.

## Performance craft for sung scenes
- **Rich delivery cues beat dry ones** — "belts the chorus, shoulders lifting on the build, eyes closing on the high note" lands; "sings naturally" doesn't.
- **Push the animation principles onto the music** — anticipation crouch into a downbeat, follow-through on hair/cloth through a spin, gesture arcs riding the phrase. The body dances while the mouth syncs (mouth + head + body sync together on this model).
- **Emotion follows the song's arc** — map verse/build/chorus to escalating expression and camera energy, not one flat mood.

## Full songs — the segment workflow
1. **Split the finished track** into ≤13–14s segments at musical phrase boundaries (never mid-word).
2. **One generation per segment.** Reuse the SAME character reference and the same identity-lock + style-anchor wording in every segment; describe each segment's scene in text. Small constant reference pack (start frame + character) beats a big varied one for drift.
3. **Per segment, transcribe only that segment's lines** — tied to that segment's beats.
4. **Assemble in the edit.** Lyric text on screen is an edit overlay — never generated in the video.

## Symptom → fix (singing-specific starting points)
| Symptom | Fix |
|---|---|
| Sung words come out wrong / mumbled | Transcribe the exact lyrics in the prompt alongside the tagged track — never rely on the audio alone. |
| Rhythm sounds close but timing wanders off the track | Attach the segment as a black-screen MP4 *video* reference instead of raw audio. |
| Sync goes rubbery late in a segment | Cut the segment shorter (≤13s) at a phrase boundary. |
| Mouth barely moves on sung lines | Feature the mouth: front-facing, medium/close framing; make it an on-screen-singer beat, not montage. |
| Character drifts across song segments | Same fixes as multi-scene ads (`models/seedance.md`) — one constant character reference + identical lock wording in every segment. |
| Model invents extra music over the track | State the role plainly: "@audio1 is the only music and the master timing." |

*Confidence: the transcript rule, the black-screen video trick, segment limits (≤14s), and beat-sync behavior are community-tested findings on supplied-audio lip-sync; the delivery-cue and segment-workflow specifics are informed starting points — calibrate on real sung generations and fold wins back here and into `models/seedance.md`.*
