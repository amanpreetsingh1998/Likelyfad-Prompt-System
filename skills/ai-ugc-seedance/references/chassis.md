# Chassis — the prompt structure (every clip)

Every production prompt that worked used the **same block order**. Keep it. Early blocks carry the most weight, so references and the camera identity come first; the closer comes last. Tags: **[proven]** production, 2+ ad series · **[one series]** production, a single ad series · **[guide]** published guides, uncontradicted · **[trial]** untested.

## Inputs — absorb before writing [proven]
- **The whole script**, every clip of the series — the delivery of clip 3 depends on how clip 2 ended.
- **Each reference and its one job:** first frame · character identity · a held-position/pose image for a later beat · product label close-up · location · voice sample.
- **The persona:** age range, look, accent, the register (e.g. "sassy know-it-all", "blunt no-nonsense expert", "flat deadpan").
- **What must never appear** — ask up front. Anything named is excluded in every clip.
- **Objects the script names but the references don't show** (a line says "pillow" and no pillow is in the scene): ask before adding or substituting one. Never let the words and the action disagree, like saying "pillow" while spraying a blanket.
- **Which camera setup** (selfie / friend-held / tripod) → `styles/raw-iphone-ugc.md`.

## The block order [proven]

### 1. References — one role line each, at the very top
```
@image1 as the first frame.
@image2 as character face and identity reference across all angles.
@image3 as the <held-position / pose> reference for <which beat>.
@image4 as the product label fidelity reference — <label transcribed exactly>.
voice timbre references @audio1 — extract voice character only (tone, pitch, accent, room acoustic), do NOT copy or reproduce any dialogue or words from @audio1. The character speaks ONLY the dialogue written in this prompt, in the voice style of @audio1.
```
Phrasing and the full role list → `models/seedance.md`.

### 2. Consistency + energy line
```
same person across frames. Dynamic energy. <Register> throughout.
```

### 3. Camera identity line — who holds the phone
One sentence stack: device + who films + angle + framing + motion truth + the NOT-list + realism line + pace/cut line + duration + ratio. Templates per setup → `styles/raw-iphone-ugc.md`. Always state the **number of internal hard cuts** here if there are any ("with two internal hard cuts").

### 4. Subject block — the person and exactly what each hand does
- Match the reference: `sits on <the sofa / bench / chair>, matching @image1`.
- Wardrobe, hair, skin, makeup, jewellery in concrete detail — **the same wording in every clip of the series**.
- **Each hand gets a job, and a side:** "her <hand> holds … on the <LEFT/RIGHT> SIDE of frame from viewer perspective … her other hand is free and gestures". If both hands are empty, say so: `Both hands are completely empty throughout. No bottle, no phone, no product anywhere in frame.`
- **Read the frame side off the first-frame image — never derive it from the hand.** A person facing the camera shows their right hand on the viewer's LEFT, but front-camera footage is often mirrored, so the same hand can appear on either side. Look at where the object sits in `@image1` as the viewer sees it, write that side, and add `exactly as shown in @image1`. If there's no first frame, or it's unclear, ask. The side of the frame is what locks placement; the hand's name is secondary. [proven for pinning; the mirror caution is from a fresh-agent test, 2026-09-18]
- **Props on the table** are named and pinned: `scene dressing only, NOT touched, NOT picked up`. Count unique objects: `Only ONE <object> exists in the scene.`
- **The product, when held:** incidental by default — `held loosely as a casual extension of the hand … NOT a focus, NOT a hero presentation`. The label faces camera; the side never changes. (Exact label handling → `models/seedance.md`, Text and labels.)

### 5. Background block
```
Background matches @image1: <every visible element: walls, shelves, window, plants, light direction>. No other people in the frame.
```

### 6. The alive block — never a frozen person [proven]
```
The scene is alive from frame zero through the entire <N> seconds with continuous natural micro-motion — active before the first word, NOT starting only when dialogue begins. <hair/locs> shift slightly with her breathing, chest rises and falls, natural eye blinking distributed across the clip with at least <N/2> natural blinks, including one blink within the first 1 second, eyebrow micro-flickers, mouth-corner micro-tensions between words, subtle facial muscle tensions and releases, tiny breath-driven shifts in the shoulders. <camera motion truth: "The friend-held camera bob is natural and continuous from frame zero."> NOT frozen, NOT static.
```
- **Blinks:** about one per 2 seconds, stated as a minimum.
- **Hands at rest:** give a **resting baseline** ("hands clasped in her lap") and say hands only lift for the named gesture moments, then settle back — `NOT held rigid, NOT theatrical, NOT constantly moving`.

### 7. Timed beats — the dialogue lives here
```
[0-2s] <Shot label>. <framing>, camera locked. <register, pace, eyes>. She says: "<line verbatim>." On "<word>," <gesture + face>. On "<word>," <gesture + face>. <end state of the beat>.

[HARD CUT — instant frame-to-frame transition at 2s, slight 5-10 degree angle pivot, same composition scale, NO zoom, NO scale change, NO motion blur, NO dissolve, NO fade]

[2-4s] ...
```
- **Timecodes on every beat**; beats of 1.5–5s.
- **Word-pinned performance** (`On "X," …`) — see `delivery/dialogue.md`.
- **Internal hard cuts** are written as their own bracketed line with the full transition spec. Keep **the same scale** unless a tighter frame is the point ("10-15% tighter framing on …").
- **State the end of the clip** — open (mid-thought) or closed — inside the last beat. → `delivery/clip-series.md`.

### 8. Audio block
Voice spec (timbre clause, age, gender, accent, pace, mic distance, room reverb) → the register → **per-line** emphasis and cadence → **held silences** with durations → the cut sound rule (`The internal hard cuts are silent — NO transition sound, NO clicks, NO whoosh`) → any action sound or its explicit absence. → `delivery/dialogue.md`.

### 9. LOCKED REGISTER + CRITICAL override — when the words pull the wrong way
Only when a line would naturally be read in a different tone than the brief. → `delivery/dialogue.md`.

### 10. Ambient block
```
<Room> ambient underneath at low volume — <3-4 specific quiet sounds>. Real <room> recorded on a phone, not isolated studio audio. No music score.
```

### 11. Look block — locked per project
→ `styles/raw-iphone-ugc.md`.

### 12. Maintain block — restate every lock
```
Maintain her identity from @image2, same outfit, same face, same hair, same build, same <setting> from @image1 throughout. Voice character continuity from @audio1, timbre only, NOT content. <prop rules per beat, with sides and NEVER-swaps>. <label exact, "NO text hallucination, NO alternate spelling">. <count rules>. Realistic hand anatomy with five fingers, stable proportions, sharp focus on face.
```
Repeating the locks here is deliberate: the production prompts restate every prop, side, and count rule a second time at the end.

### 13. Closer — every clip, verbatim
```
No music, no logo, no text on screen, no subtitles.
```

## Locked vs. variable
- **Locked for the project (verbatim in every clip):** the camera identity line for the chosen setup, the look block, the voice spec, the wardrobe description, the closer.
- **Variable per clip:** duration, beats and timecodes, dialogue, word-pinned gestures, prop state, cut count, the register (only when the script turns), the ending (open/closed).

## Length and pace [proven]
- **Length follows specificity.** Production prompts ran ~600–1,500 words and rendered well; the guides' 120–280-word ceiling is not used here. Don't pad — but don't cut a lock to save words.
- **Speaking rate** in the production prompts: up to ~3.7 words/second at fast TikTok pace, ~1.6–2.6 at deliberate pace. Leave room for held silences. If a clip's lines exceed ~3.5 words/second, split the clip.
- **Clip length:** 5–12s in production; 15s is the model ceiling, not a target.

## Audit — before delivering any clip
1. Every asset has a role line; one asset per attribute; the voice sample has the timbre-only clause.
2. **Left/right** is read off `@image1` and is the same in the subject block, every beat, and the maintain block.
3. Each prop's state is stated per beat and again in maintain; unique objects are counted.
4. Every object the dialogue names is in the scene, or the user was asked. Dialogue is **verbatim** from the script; numbers spelled out; brand names phonetically spelled if hard to say.
5. The cut count in the camera line equals the number of `[HARD CUT]` lines; cuts are declared silent.
6. The blink minimum matches the duration.
7. Words per second fit the duration.
8. The ending is declared open or closed in both the last beat and the audio block.
9. The register lock is present if any line's natural reading fights the brief.
10. The closer is the last line.
