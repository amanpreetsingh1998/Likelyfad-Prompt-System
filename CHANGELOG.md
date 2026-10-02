# Changelog

All notable changes to this system are documented here. Format follows [Keep a Changelog](https://keepachangelog.com/). Each skill also carries its own `version:` in its `SKILL.md` front-matter; releases are git-tagged as `<skill>@<version>` (e.g. `ai-ugc@1.0.0`).

## [Unreleased]

## System 2.0.0 — 2026-10-02: image / video / audio
A major restructure (Aman, Telegram msgs 100–113). The repo is now three separate systems. **Start from `AGENTS.md`**: it asks "What do you want to create? 1) An image 2) A video 3) Audio", opens that system's `SYSTEM.md` menu, and loads exactly one skill.
### Changed
- **Moved:** `skills/ai-ugc`, `skills/ai-ugc-seedance` and `skills/ai-animation` → `video/`; `skills/ai-song` → `audio/`. The file names inside each skill are unchanged.
- **Old paths:** `skills/<name>/SKILL.md` are now signposts (removed in a later release). The full map is in `docs/MOVED.md`.
- **Registration updated:** `AGENTS.md` is rewritten as the start menu; `CLAUDE.md`, the README (a new landing-page guide), the marketplace (2.0.0, new sources), the `.claude/skills/` symlinks and `docs/` paths all follow.
### Added
- **`image/character-casting` 1.0.0:** from the team's Unique Character Casting system.
  - The casting theory (unique, recognisable, age-true people; audience notes; the transformation rule; the Final Editor Check).
  - The script → cast plan → base sheets → reference-guided transition edits workflow.
  - Vocabulary, wardrobe and problem-area wording.
  - 4 character + 4 location style masters, kept byte for byte.
  - A **Seedream 5.0 Pro or Nano Banana Pro** choice, with one model per character. Nano Banana use is untested.
  - The 5-view (full body) vs 3-view (chest-up) rule.
- **`image/nano-banana` 1.0.0:** the Nano Banana Pro Prompting Guide v2 (April 2026), split into the skill shape, with a question-first entry, house character-sheet rules, and a hand-off map to the video skills. The examples are kept as written.
- **`audio/elevenlabs-voice` 1.0.0:** the ElevenLabs v3 Script Optimizer as the operating manual, with the Audio Tags guide as the evidence reference.
- `docs/MOVED.md`, `docs/nano-banana-sources.md`, and new "awaiting first run" rows in the prompt log.
### Also released in this version (were local, untested on renders)
- `ai-ugc` 1.0.2 and `ai-song` 1.2.0 (entries below).
### Backup
- The pre-2.0 state is kept on the branch `backup/pre-2.0-2026-10-02` (= `d5fd0b3`), plus a local git bundle.

## ai-song@1.2.0 — 2026-10-02 (released untested on v6 renders; live test pending)
Suno retired every model before **v6** (launched 2026-09-09), including the v5.5 this skill was calibrated on. The model layer is retargeted to v6, and a recipe is added for the production failure on long songs: 8–10 min songs turning into whispered or spoken lyrics with little or no music. Every line in `models/suno.md` is now tagged **[official]** (read on Suno's pages, 2026-10-01/02), **[v5.5-tested]** (our July calibration, not yet re-run on v6) or **[community]**.
### Changed
- **`models/suno.md`** rewritten for v6:
  - the model line;
  - **Max Mode** (ON for anything over 2 min);
  - the **Variety slider at 0** (Suno: reduce it to 0 "to retain full control of your style tags");
  - the **20-a-month Pro download cap**;
  - the two official commercial-rights wordings, which disagree;
  - **Style Personas vs Voices** (Job A now uses a Style Persona; v6 "Voices" is voice cloning of a real human singer);
  - the v6 editor (Remove, Edit Lyrics / Replace Section with plain-language edits, Extend);
  - a new **LONG SONGS** recipe: chunked passes, Max Mode, the music restated in every section tag, Style re-pasted every Extend, anti-whisper Exclude entries, listen before each Extend, repair a whispered span;
  - new symptom rows;
  - a new **candidate** Job A method: swap the leading hook in-song with v6 Replace Section (untested; it failed on v5.5).
- `[Whispered]`, `[Spoken]`, `[Interlude]` and `[Breakdown]` moved from "medium reliability" to never-use in our songs.
- **`SKILL.md`**: targets v6; new must-never (long songs in chunks, Variety 0); Persona replaces Voice throughout; the long-song workflow step now follows the recipe.
- **`styles/high-energy-nonrap.md` 1.1.0**: Variety 0, Max Mode, long-song Style and Exclude additions; the proven strings are marked as v5.5.
- **`chassis.md`**, **`examples/three-hooks-one-body.md`**: Persona wording, v6 settings, and the download count. The example is marked not yet re-rendered on v6.
- **In-app check (Aman's screenshots, 2026-10-02):** the v6 Advanced screen and its defaults are recorded: Max Mode Off, Variety Off, Weirdness and Style Influence 50%, and three new settings (Vocal Gender, Duration Custom/Auto, Personalize "My Taste"). Our settings: Max Mode On, Variety Off, Vocal Gender set, Personalize Off; Custom Duration is a test.
- README and marketplace: Suno v6. Prompt log: two new "awaiting first run" rows.
- **Second research round (5 Sonnet agents, 2026-10-02)** folded into `models/suno.md`:
  - the magic wand is Style Augmentation, so never press it [official]; Personas live under + Voice [official]; Replace Section needs a 10–30s selection [official];
  - long songs: a tighter first pass (1,800–2,500 chars) and one section per Extend; never change BPM or Style mid-chain; set the Extend point 3–5s before a dead spot; the "Keeper Boundary";
  - 6–12 syllables per line; v6's muffled baseline (strip layers, put the vocal in front);
  - Vocal Gender may slip; Custom Duration is "a target, not a guarantee";
  - the conflicts are recorded, not resolved: v6 sites say in-Style negations backfire and Exclude should be short, the opposite of our v5.5 A/B (so it is the first v6 A/B); 15–30 vs 120–180-word Style; one-pass 8 min vs chunks.
- **Peer production SOPs (shared privately, 2026-10-02)** folded in. Techniques only, restated, with no identifiers, tagged [peer-SOP]; Kang's own reasoning is tagged [Kang idea]:
  - the pacing block (no sustained notes or melisma, gaps under 1s);
  - hook harvesting (first-choice Job A hook method);
  - overlap-splice as the Job B fallback, behind Extend-from-timestamp, with the full lock and a join check;
  - a "Matching a reference ad" section;
  - a ban on quiet section directions (stripped back / minimal / intimate / breakdown / build) and group vocals, a likely cause of the whisper stretches;
  - the v5.5 hook-arc string marked hook-clips-only.
- Aman's go to bake everything in and test it on a live project (TG msgs 82, 84).
### Open for Aman
- The research recommends a **repeating chorus** to keep long songs sung. Our verbatim rule forbids repeating a line the script doesn't repeat. This is unchanged pending his call.

## ai-ugc@1.0.2 — 2026-10-01 (released untested on renders; test pending)
Takes in Google's own prompting guide for the model, *"Creative prompting with Gemini Omni in Google Flow"* (@FlowbyGoogle, 2026-10-01). Every new line is tagged **[google]** and is untested on our clips; where it disagrees with a tested line, the tested line wins until a render settles it. Tip-by-tip mapping: `docs/gemini-omni-flow-guide.md`.
### Changed
- **`models/gemini-omni.md`**: the model **cuts between angles by default**, so the one-take is now stated explicitly (this replaces the old claim "one continuous take per generation"). New sections: more reference types (video as a motion and audio reference, last frame, style transfer), timing with timecodes (a test variant; word-pinned gestures stay the default), Google's negatives list with the two that must never be used on UGC (*No camera movement*, *No dialogue*), and **fixing a near-miss by conversational edit** ("Keep everything else the same"). Two new symptom rows. The access line now flags reports of an API preview and an "Omni 1.1 Flash" version as unverified.
- **Locked Negatives** (`styles/realistic-ugc.md` 1.0.1, `chassis.md`, `examples/realistic-ugc.md`): open with **"No scene cuts."**. The example's line is marked as not yet re-rendered.
- **`SKILL.md`**: new must-never (always state the one-take), workflow step 6 (fix a near-miss by editing), and a note that [google] lines are untested.
### Note
- Version collision: the parked `naming-rule-patch` branch also claimed ai-ugc 1.0.2. If it is ever revived, it takes the next number.

## ai-animation@1.4.1 — 2026-09-18
Wording-only patch.
### Changed
- **`models/seedance.md`:** the "negated words backfire" rule now states its scope. It applies to animated and stylized prompts, and points to `ai-ugc-seedance`, whose realistic production prompts use NOT-lists. This stops an agent "fixing" one skill against the other.

## ai-ugc-seedance@1.0.0 — 2026-09-18
A new, separate skill for **realistic UGC generated in Seedance 2.0**. `ai-ugc` stays the Gemini Omni skill. They are separate on purpose: Seedance's realistic and animated crafts obey different rules. The animation skill writes affirmative-only prompts, and the realistic production prompts use NOT-lists heavily.
### Added
- **Built from production prompts, not guides.** The rules come from the owner's production Seedance UGC prompts that rendered well. Where two published guides disagree with them, the production prompts win and the guide rule becomes a symptom→fix. Every rule is tagged by the breadth of its evidence: **[proven]** (seen across at least two separate production ad series), **[one series]** (a single series: likely sound, less tested), **[guide]**, or **[trial]**. The council found that the first draft had tagged single-series techniques as proven.
- **Three guide rules overturned by production evidence:** prompt length (production ran ~600–1,500 words against a 280-word guide ceiling), negations (NOT-lists and `no 3D, no cartoon, no VFX` work on realistic UGC), and head movement during spoken lines (word-pinned nods rendered well across three series; a slow push-in across a spoken beat rendered well in one series and is offered as a tagged variant). The guides' 5–10-word line limit is likewise a fix for mushy sync, not a limit.
- **Chassis** (`references/chassis.md`): the 13-block order every production prompt followed. It covers per-hand jobs and screen sides, the alive block with a blink minimum from frame zero, timed beats with word-pinned performance, a maintain block that restates every lock, the closer, a speaking-rate ceiling (~3.5 words/second), and a 10-point audit.
- **Model layer** (`references/models/seedance.md`): hard specs, reference-role phrasing (first frame, identity, held-position per sub-shot, label fidelity, timbre-only voice sample, extend-from-video), this skill's negation policy, text and label handling, and a symptom→fix table.
- **Style** (`references/styles/raw-iphone-ugc.md`): four camera setups named by who holds the phone (friend-held, selfie, tripod, locked reaction), each committing to one camera truth, plus the locked look block.
- **Delivery layers:** `dialogue.md` (verbatim lines, phonetic names, word-pinned gestures, the audio block, open vs closed cadence, the **LOCKED REGISTER + CRITICAL override** against script-driven tone drift), `clip-series.md` (planning 5–12s clips that stitch mid-sentence, continuity, internal hard cuts), and `trial-formats.md` (founder talking head, street interview, hands-only voiceover, two-person dialogue — all **[trial]**, never run in production).
- **Examples** (flagged v1): friend-held with internal jump cuts, a tripod two-clip product series, and a locked reaction clip. Every brand, product, person, and script is invented.
- Registered in `AGENTS.md`, `CLAUDE.md`, the plugin marketplace, the README, the prompt log, and `.claude/skills/ai-ugc-seedance`.
### Changed
- **README maintainer note:** "keep model names out of structure and naming" becomes "keep model-specific wording inside each skill's `references/models/` file". The owner allowed a model or tool name in a skill's own name on 2026-09-16, and this skill's name uses it.

## ai-song@1.1.0 — 2026-09-09
Fixes a contradiction that made the entry point prescribe a method its own model file had already retired. The 2026-07 calibration demoted **Replace Section** after it failed on a real leading-hook swap, but `SKILL.md` and the worked example still walked through it — so an agent reading only the entry point got the failed method.
### Changed
- **`SKILL.md`** now states the calibrated Job A: one master (Hook 1 + Body) that is also ad #1, a **Voice** made from that take, Hooks 2 and 3 as **standalone mini-generations with that Voice locked** and the **hook-arc style string**, then a join to the **one exported body WAV** in an external editor on the first downbeat. Replace Section is called out as demoted so nobody reaches for it again.
- **New must-never: every keeper gets an editor pass.** The Song Editor Crop / Remove Section is the deterministic, credit-free gap fix; prompt wording only raises the odds. Short hook generations always pad an instrumental tail — crop rather than re-roll.
- **Output format** updated: hook variants are standalone mini-generation blocks, and the assembly runbook covers master, Voice, mini-gens, editor pass, and the drop-join.
- **Naming synced to the current UI** — Personas are called **Voice**.
- **`models/suno.md`**: the "hooks don't match the body" symptom row no longer recommends the demoted method; the open render test is updated from the Replace-Section question (now answered) to whether the mini-gen plus Voice-lock plus drop-join holds tempo, key, and voice across a set.
- **`examples/three-hooks-one-body.md`** rewritten to v2 on the calibrated method — standalone hook blocks with `[End]`, the hook-arc string, and a seven-step assembly runbook.

## Repo maintenance — 2026-09-09
### Fixed
- **README rewritten.** It described only `ai-ugc` and told readers animated styles could not be done yet, which had been untrue since July. It now covers all three skills, both animation styles, and the music and song paths.
- **Release tag map established** (see below). The changelog promised `<skill>@<version>` tags and none existed. Every past release now has a defined target commit. **The tags could not be pushed from the session that created them** — GitHub refused the `refs/tags/*` push with a 403 while branch pushes to the same repo succeeded, so that session's credential was scoped to branch refs only. Anyone with normal push rights can create them in one paste from a local clone:

  ```
  git tag -a ai-ugc@1.0.0       9526422 -m "ai-ugc 1.0.0 — initial realistic-UGC talking-head skill (Gemini Omni)."
  git tag -a ai-ugc@1.0.1       5918bcd -m "ai-ugc 1.0.1 — Voice composed per creator, locked per project."
  git tag -a ai-animation@1.0.0 e993fc9 -m "ai-animation 1.0.0 — Seedance image-to-video, Pixar/Disney 3D style."
  git tag -a ai-animation@1.1.0 2c7ef74 -m "ai-animation 1.1.0 — sung lip-sync delivery layer."
  git tag -a ai-animation@1.2.0 1073948 -m "ai-animation 1.2.0 — beat-cut music-video mode (song + SRT)."
  git tag -a ai-animation@1.3.0 e639d35 -m "ai-animation 1.3.0 — calibration from the first real music-video run."
  git tag -a ai-song@1.0.0      bd6a43d -m "ai-song 1.0.0 — Suno song prompts from ad scripts, incl. the 2026-07 calibration."
  git tag -a ai-animation@1.4.0 cb97c95 -m "ai-animation 1.4.0 — direct 3D explainer (the Zack D style) as a separate path."
  git tag -a ai-song@1.1.0      b5b553a -m "ai-song 1.1.0 — entry point realigned to the calibrated Job A method."
  git push origin --tags
  ```

  Each target is the commit where that version's content was **final**, not necessarily where it was introduced. `ai-song@1.0.0` is the clearest case: it absorbed the July render calibration without a version bump, so its tag points at the merged calibrated state.
- **All three skills registered as Agent Skills.** Only `ai-song` had a symlink under `.claude/skills/`; `ai-ugc` and `ai-animation` now do too, so each auto-loads outside this repo.
- **Prompt log brought current.** It held a single June row. It now carries the findings from the July Suno build and the July animation music-video run, plus an explicit "awaiting their first real run" table so untested work is never mistaken for calibrated work.

## ai-animation@1.4.0 — 2026-09-09
Adds the **direct 3D explainer** style (the "Zack D" style) as a **second, separate style path** inside `ai-animation` — not a variant of Pixar/Disney 3D, and not related to the song or music layers. Ported from a production-calibrated external style guide (v2.0, 2026-09-02) that was itself adapted from this skill and refined on observed render failures.
### Added
- **New style** (`styles/direct-3d-explainer.md`): semi-realistic game-engine-like characters, cyan-void explainer space or locations built from 3–5 primitives, bright flat phone-readable lighting, a **colour-ownership table** (colour explains function, not decoration), material rules, and this style's camera menu (quick push, snap reframe, locked when the mechanism evolves). Includes a Pixar-vs-explainer delta table and a "writer-notes are never prompt text" guard.
- **New delivery layer** (`delivery/explainer.md`): the **new-fact cadence** (a readable visual fact every 0.8–1.8s, and the insight that a fact is not always a cut), the two visual modes (narrative reenactment vs. explanatory demonstration), the **input contract**, the narration **clause map → beat manifest → rebase → assembly** workflow, the **script-to-visual translation table**, narration-in-post audio, a QC checklist, and a symptom→fix table.
- **Worked example** (`examples/direct-3d-explainer.md`, flagged v1 — test & calibrate): a 24s narrated explainer as three 8s clips, demonstrating both visual modes, the beat manifest, and the two standing lines this style adds.
- **Step 0 style router** in `SKILL.md` — a decision table plus trigger vocabulary so the Pixar and explainer paths are never blended or co-loaded.
### Changed
- **Model layer** (`models/seedance.md`) gained style-agnostic craft hoisted out of the guide, which improves Pixar work too: **one owner per attribute**; the **multi-panel/collage limitation** (an `@image` tag addresses the whole image, never a region — never promise region-picking); final-frame reuse nuance; **motion safeguards** (exact repeated-action counts, cloth and flexible geometry staging, particle/field distribution); the **anatomy and handedness protocol** (camera side, body side, limb chain, grip, active finger, resting hand); expanded **text and label** craft; a **mature/sensitive context** checklist; and nine new symptom→fix rows.
- **Chassis** (`chassis.md`): motion and camera craft is now explicitly **style-scoped** (the animation-principle doctrine is Pixar's, not universal — only "stabilized, purposeful, one move per beat" is universal); added one-owner-per-attribute, the narrated-explainer delivery mode, a mature-context section, and a note that the explainer style legitimately adds Background-rule and Lighting/colour lines to the prompt.
- **`SKILL.md`** description widened from ads-only to ads **and** explainers, with "Zack D" as trigger vocabulary; camera must-never rescoped per style; new must-nevers for attribute ownership, left/right auditing, and not promising generated typography; explainer fields added to the output format.
- Repo plumbing updated: `AGENTS.md`, `CLAUDE.md`, and the plugin marketplace manifest.
### Notes
- Provenance is handled deliberately: the file is named for the **format**, not the creator, and the style file carries the source guide's disclaimer — apply the observable grammar, never copy any channel's name, branding, voice, characters, or individual scenes.

## ai-animation@1.3.0 — 2026-07-23
Calibration from the first real music-video production run (prompt-side; playback validation pending).
### Changed
- **Cut pacing inverted** (`delivery/music-video.md`): a **per-shot ceiling (~1.5s, no lingering)** replaces the old cuts-per-segment cap — 10+ cuts per segment is normal; long lyric lines are covered in multiple angles of the same action, never held. Each segment pre-declares a two-half **split fallback**, fired only if the render smears.
- **Timing authority**: SRT lyric timestamps are the **master clock** (cuts land where words land); the beat grid is secondary. Ceiling violations are repaired by **subdividing the shot in place** — downstream lyric-locked timestamps never move.
- **Fast edit ≠ fast characters**: the Format line now splits editing energy (fast punchy hard cuts) from character motion (calm, believable, slightly slow-motion) — omitting the split makes characters frantic.
- **Per-shot anchors**: every shot line opens with its thread's grade token and closes with exactly one `Camera:` move; grades double as story-thread markers (one locked grade per location/timeline thread).
### Added
- **Multi-character method** (`chassis.md`): per-character @-tag + description + identity lock ("in every shot they appear in"), an explicit "These are N distinct characters…" disambiguation line, generic-extras rule (no identity bleed into crowds), and **story names never enter prompts** — @-tags only.
- **Banned-vocabulary discipline** (`chassis.md`): **ask the user up front** whether anything must never appear; if yes, that concept's entire vocabulary is excluded from every prompt in any form (including negations and near-synonyms) — steer with richer positive description; the list grows when a render misbehaves.
- **Sequenced product reveal** (`delivery/music-video.md`): product incidental at natural scale through the body (wording in References + Setup + Closing); the label/hero framing gets one dedicated slow close-out segment; all other props affirmatively unlabeled (readable prop text garbles).
- **Per-segment delivery ritual** (`delivery/music-video.md`): rolling "Locked:" ledger, complete prompt every time (never fragments), numbered asset lines (`1 — @image_1 — file (role)`), Notes block (risks, playback watch-list, split fallback, next-segment preview), a content-filter pre-check, and audit-don't-reassure against the numbered rulebook.
- Model layer (`models/seedance.md`): new symptom→fix rows — wrong attribute recurring (vocabulary ban), identity bleed into extras, product scale inflation / label garble, readable prop text; smeared-segment fix now points to the split fallback.
- Example (`examples/pixar-disney-music-video.md`) rewritten to v2 demonstrating all of the above (12-shot fast-cut segment + ledger + notes ritual).
### Fixed
- Marketplace manifest: `ai-ugc` version synced to 1.0.1 (was lagging at 1.0.0).

## ai-animation@1.2.0 — 2026-07-14
### Added
- **Beat-cut music-video mode** (`references/delivery/music-video.md`) — the main path for **full songs** (built from the team's SRT idea): a finished song + **SRT timestamped lyrics** + brief + images → per-segment prompts whose scenes **hard-cut in time with the beat and the lyrics**, with **no lip-sync**.
- The core reframe baked in: **the SRT is input for the prompt-writer, never pasted into the video prompt** — the writer computes the lyric-to-scene map, the BPM bar grid (`240 ÷ BPM`), ≤14s segment windows on line/downbeat boundaries, and rebased local timestamps; the model receives only timestamped `hard cut to:` beats.
- **Segment manifest** as the checkable artifact (window / lyric lines / scene / local cut points) — doubles as the edit sheet; solves the "manually cutting a 7–9 minute song" problem at the planning level.
- **Silent-visuals default** — no audio attached, so the 15s audio-input limit stops constraining full songs; the track is laid over in the edit. Optional per-segment audio slice as `rhythm reference only` when motion must ride the beat.
- Worked example (`examples/pixar-disney-music-video.md`, flagged v1 — test & calibrate): inputs → lyric-to-scene map → manifest (with a rebase check) → a full chorus-segment prompt → edit assembly.
- Model layer additions (`models/seedance.md`): timestamped-beat adherence is good but not frame-exact; morph-vs-hard-cut and cut-density symptom→fix rows.
### Changed
- `delivery/singing.md` repositioned as the **special case** (a character visibly sings — jingle ads, sung hooks); full songs defer to `music-video.md` for windowing/manifest/assembly.

## ai-animation@1.1.0 — 2026-07-14
### Added
- **Singing delivery layer** (`references/delivery/singing.md`) — plugs into the chassis's self-contained Voice/Audio seam. The song arrives **finished** (e.g. from Suno) with its lyrics; the skill writes sung lip-sync prompts, never asks the model to compose vocals (unreliable).
- The three sung-lip-sync rules: tag the track's role (`lip-sync … to @audio1`), **always transcribe the lyrics in the prompt** alongside the attached track (audio alone gets misheard), and ≤14s per generation (13s safe).
- **Fidelity ladder** for attaching the song: tagged audio + transcript by default → **black-screen MP4 as a video reference** when rhythm drifts (Seedance follows video refs much more tightly) → native beat sync as a free win (camera/action land on the rhythm).
- **Full-song segment workflow** (in scope for v1): split at phrase boundaries, one ≤13–14s generation per segment, constant reference pack + identical lock wording across segments, assemble in the edit.
- Two sung modes: **on-screen singer** (mouth featured, lip-sync binds) and **sung montage** (track over b-roll, free movement).
- Worked sung example (`examples/pixar-disney-singing.md`, flagged v1 — test & calibrate): a 12s sung jingle ad + the full-song segment pattern.
- Model layer additions (`models/seedance.md`): supplied-audio mechanics + three new symptom→fix rows (misheard lyrics, timing drift, invented extra music).

## ai-song@1.0.0 — 2026-07-14
### Added
- New **`ai-song`** skill: Suno song-prompt system — turns a finished ad script (often **3 hooks + 1 body**) into a paste-ready Suno package (a Style field + the script sung **verbatim** inside Suno's structure tags + settings). The words are locked verbatim; the skill formats and styles only.
- Current model layer: **Suno v5.5, Pro tier** (`references/models/suno.md`) — the two-field split, structure tags, Exclude Styles & sliders, Personas, the **identical-body method** (one master + Replace Section, so each hook is regenerated in-context and matches the body), the **long-song method** (Extend + Get Whole Song + free-DAW cleanup, since Studio is Premier-only), brand-name phonetic respelling, and a symptom→fix table.
- Default sound layer **`high-energy-nonrap`** (fast, driving, gapless, sung — never rap): a genre menu with BPM anchors and an audience→genre hint map. The sound layer is swappable.
- Chassis tuned for songs: format-don't-write, the verbatim rule, structure-tagging from the whole script, the 2–3-treatment sound-decision step, and a small **visual/timing seed** to hand off to the animation skill.
- A worked example (flagged v1 — test & calibrate) and repo plumbing: registered in `AGENTS.md`, `CLAUDE.md`, and the plugin marketplace manifest.

## ai-animation@1.0.0 — 2026-07-13
### Added
- New **`ai-animation`** skill: animated video-ad prompt system — turns a finished script + already-made images (character, scene, product) into ready-to-paste **image-to-video** prompts. **Pixar/Disney 3D** is the first style; the style layer is swappable and a singing/voice delivery mode is planned on top.
- Current model layer: **ByteDance Seedance 2.0** (`references/models/seedance.md`) — durations, the @-tag reference-role mechanism, the no-negative-field rule, and a symptom→fix table.
- Chassis tuned for animation: image-first (the start frame carries the look), lean affirmative anchors instead of the older locked-text "character bible" / negative blocks, smooth virtual camera, animation-principle motion, relaxed lip-sync (head may move during speech), and a **default ≤15s multi-scene** generation to save video-team time.
- The `pixar-disney-3d` style, a self-contained Voice/Audio block (the seam for a future singing skill), and a worked example (flagged v1 — test & calibrate).
- Repo plumbing: registered in `AGENTS.md`, `CLAUDE.md`, and the plugin marketplace manifest.

## ai-ugc@1.0.1 — 2026-06-16
### Changed
- **Voice is now composed per creator and locked per project**, instead of a single fixed woman-persona block. The agent infers a fitting voice (any gender/age/accent/energy) from the creator reference + brief, writes it with a consistent formula, then locks it for that project (reused verbatim across its clips). The Lymphoria voice remains as a labeled worked example. Backward-compatible — existing prompts still valid.

## ai-ugc@1.0.0 — 2026-06-16
### Added
- Initial **`ai-ugc`** skill: realistic UGC talking-head video-ad prompt system (script + reference images → ready-to-paste prompts).
- Chassis (section structure + locked/variable + performance craft), the Voice section, and the `realistic-ugc` style.
- Current model layer: **Google Gemini Omni** (`references/models/gemini-omni.md`) — durations, reference mechanism, camera tokens, negatives, and a symptom→fix table from real testing.
- Worked examples (Lymphoria hooks).
- Repo plumbing: `AGENTS.md`, `CLAUDE.md`, plugin marketplace manifest, and background research in `docs/`.
