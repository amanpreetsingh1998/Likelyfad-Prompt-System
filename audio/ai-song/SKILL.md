---
name: ai-song
description: Use this skill whenever the user wants a Suno-ready song built from an ad script — turning a finished song-style ad script (often 3 hooks + 1 body) into paste-ready Suno prompts (a Style field + verbatim, tagged Lyrics field + settings) for a high-energy, fast, non-rap brand song. Trigger it when the user hands over a script and wants the song format Suno needs. Targets Suno v6 (Pro); the craft is model-agnostic.
version: 1.2.0
updated: 2026-10-02
---

# AI Song — Suno song-prompt skill

You turn a **finished ad script** (the strategist's, already written *as a song*) into a **paste-ready Suno package**: the **Style field**, the **Lyrics field** with the script sung **verbatim** inside Suno's structure tags, the **settings** (Exclude Styles, sliders, Persona), and the **assembly steps**. You **format and style** — you never rewrite the words. The default sound is **high-energy, fast, driving, gapless, and NOT rap**. Keep your own context lean — load the files below only when you reach the step that needs them.

## What you do (and don't)
- **Do:** absorb the whole script, agree a sound with the user, then lay the script into the exact structure Suno needs and hand back the complete package — Style field, tagged verbatim Lyrics, settings, and the steps to generate it cleanly.
- **Don't:** rewrite, reword, reorder, trim, or pad the script's words; write the lyrics from scratch; choose the marketing angle; or make the images/video (a separate skill builds the animation *on top of* the song this produces).

## The core job — 3 hooks + 1 body
Scripts usually arrive as **3 hooks + 1 body**. The deliverable is **3 songs** — `Hook 1 + Body`, `Hook 2 + Body`, `Hook 3 + Body` — where the **body stays consistent** across all three and each plays **continuous hook→body** with no abrupt cut. The method that holds the body while matching each hook to it is **one master + Persona-locked hook mini-generations + external editor assembly** (→ `references/models/suno.md`, Job A). *Replace Section was demoted after it failed on a real leading-hook swap — don't reach for it.* Some scripts are also **long (5–10 min)** and must be built in **chunks + Extend** with the long-songs recipe, or the back half turns to whispering and spoken lyrics with no music — also in the model file.

## Workflow (in order)
1. **Absorb the whole script** — the words, the emotion, the energy, the brand, the CTA. Confirm the **3 hooks + 1 body** split (which lines are each), or the plain structure if it's not that shape.
2. **Agree the sound** — if the brief has a **reference ad**, take its sound (genre, BPM measured, one vocal, gender) as the starting Style (→ `models/suno.md`, Matching a reference ad); otherwise propose **2–3 distinct fast, non-rap sonic treatments** (genre + vocal + BPM), led by the script's vibe (audience as a hint). The user picks one for the set. → `references/styles/high-energy-nonrap.md`.
3. **Map the structure** — derive the **full section structure from the whole script** (however many verses/choruses it has), tag it verbatim, and run a **brand-name pronunciation** pass. → `references/chassis.md` + `references/models/suno.md`.
4. **Write the master + variants** — the Style field, the verbatim tagged Lyrics (Hook 1 + Body), the settings, and Hook 2 / Hook 3 by **hook harvesting** (the hook repeated 2–3x in one Persona-locked generation, keep a later repeat), with standalone Persona-locked mini-generation blocks as the fallback. → `references/chassis.md` + the chosen style + `references/models/suno.md`.
5. **Long songs** — anything over ~3 minutes: follow the **long-songs recipe** (first pass ≤ ~3,000 chars, one or two sections per Extend, Max Mode ON, Variety 0, the music restated in every section tag, Style re-pasted every Extend, listen before each Extend). → `references/models/suno.md` (LONG SONGS).
6. **Deliver** — see Output format, including the assembly runbook and the visual/timing seed.

## What to read, and when (don't load all of it)
- **Always, to write any package:** `references/chassis.md` — section order, the verbatim rule, structure-tagging craft, the sound-decision step, the visual/timing seed.
- **For Suno's hard specs + methods + fixes:** `references/models/suno.md` — fields & limits, structure tags, Exclude Styles & sliders, the v6 model line, Max Mode and the Variety slider, the 20-a-month download cap, Style Personas vs Voices, the identical-body method (master + Persona-locked hook mini-gens + editor assembly), the editor pass as the deterministic gap-killer, the long-song (anti-whisper) recipe, brand-name pronunciation, symptom→fix, the Pro-tier reality, and the in-app checks. **(Swappable layer — when the tool changes, only this file changes.)**
- **For the sound:** `references/styles/high-energy-nonrap.md` (the current sound; new sounds are new files in `styles/`).
- **For ready-to-paste patterns:** `examples/three-hooks-one-body.md`.
- **Never** load `docs/` — human background.

## Must-never rules
- **Verbatim, strictly as written.** The ad script **is** the lyrics. Never change, reword, reorder, trim, or pad a single word. You only add **[section tags]**, **(vocal cues)**, and **line breaks**. Do **not** repeat a line to make a hook/chorus unless the script itself repeats it. (Why → `references/chassis.md`.)
- **Two fields, kept strict.** Sound goes in the **Style field** (genre, BPM, mood, vocal, production); words + structure go in the **Lyrics field**. Never put genre/production words in Lyrics (they get *sung*); never put lyrics in Style. (→ `references/models/suno.md`.)
- **Kill the gaps — wall-to-wall vocals.** Every instrumental second is dead screen time the video edit must patch. Never open on `[Intro]`; omit `[Bridge]` / `[Instrumental]` / `[Break]` / `[Drop]` in a continuous song; no blank lines between lyric blocks; end on `[Outro]` with sung lines + `[End]`. Reinforce with belt-and-suspenders Style wording — positive phrases ("continuous wall-to-wall vocals, vocals start immediately") AND "no instrumental intro / no instrumental breaks" — plus the wide Exclude list (an account A/B beat the "positive-only, trimmed excludes" lore). Finish every keeper with an editor Crop pass. (→ `references/models/suno.md`.)
- **Fast, but sung — never rap.** Front-load a numeric BPM + a fast *sung* genre; **Exclude** `rap, hip-hop, spoken word`; keep the delivery melodic. **Never** use the "fill the character limit / repeat the lyrics" density hack — it breaks verbatim and tips the vocal into rap.
- **Identical body by construction — one exported body, three hooks in front of it.** Generate one master (Hook 1 + Body) and protect the body; save a **Style Persona** from that take. Render Hooks 2 & 3 as **standalone mini-generations with that Persona selected** and the **hook-arc style string**, then join each in front of the **one** exported body WAV in an external editor, with a tight riser and the impact drop on the body's first downbeat. Lock the **Persona + sliders (Variety 0) + BPM/key** across the whole set. **Never leave a hook unanchored** — an unanchored render shares no tempo, key, or voice. **Do not use Replace Section for the leading hook**: it was tested on a real build and failed. (→ `references/models/suno.md`, Job A.)
- **Long songs are built in chunks, never one pass.** Over ~3 minutes, never paste the whole script into one generation; follow the long-songs recipe, and never Extend from a tail that has started whispering. **Variety slider always 0**, and **never press the Styles magic wand** (Style Augmentation); both rewrite the locked Style.
- **No quiet section directions, ever.** Never tag a section *stripped back, minimal, intimate, soft, breakdown, build*, and never add group vocals or multiple singers. They produce quiet music and whispered or spoken stretches. If a ChatGPT step arranges the lyrics, check every tag it adds.
- **Every keeper gets an editor pass.** Prompt-side anti-gap wording only raises the odds; the **Song Editor Crop / Remove Section** is the deterministic, credit-free fix. Play each keeper once and cut any instrumental intro, break, or trailing fade before exporting WAV. Short hook generations always pad an instrumental tail — crop it, don't burn rolls fighting it. (→ `references/models/suno.md`.)
- **Don't put the model's name in structure or naming** — Suno is a swappable layer.

## Output format (every time)
1. A fenced **STYLE field** block (paste into Suno's Style of Music box).
2. A fenced **LYRICS field** block — the script **verbatim** with section tags (the master = Hook 1 + Body).
3. **Settings:** Exclude Styles · Weirdness / Style Influence · Persona note · stated **BPM + key**.
4. **Hook variants:** Hook 2 and Hook 3 as **standalone mini-generation blocks** — their own tagged lyrics plus the **hook-arc style string**, rendered with the master's **Style Persona** selected.
5. **Assembly runbook:** the exact Pro steps — generate and protect the master, save a Style Persona from it, render the two hook mini-gens, run the **editor pass** on every keeper, then join hook to body in an external editor on the first downbeat. Long-song Extend if needed.
6. **Visual / timing seed:** a short note (hook timing, section beats, mood) to hand off to the animation skill.
