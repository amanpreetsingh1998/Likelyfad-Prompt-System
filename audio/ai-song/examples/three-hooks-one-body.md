# Examples — 3 hooks + 1 body (worked draft, v2 — method calibrated, shape still to test)

> **Updated 2026-09-09 to the calibrated method.** The shape is drafted; the *method* now reflects the 2026-07 account build, where **Replace Section failed on a leading-hook swap** and was demoted. Hooks 2 and 3 are standalone mini-generations with the master's **Voice** locked, joined to one exported body in an external editor. Keep folding render results back into `models/suno.md`. Swap the brand/script for your own.

A short, fast **dance-pop** brand song from an invented script (`Lumé`, a focus/energy drink). One **master** = Hook 1 + Body, which is also ad #1 and the source of the **Voice**; Hooks 2 & 3 are **standalone mini-generations** with that Voice locked, then joined in front of the one exported body WAV in the edit. The words are **verbatim** — only tags, a vocal cue, line breaks, and one flagged brand respelling were added.

## The package (this is the full deliverable shape)

**1) STYLE field** — paste into Suno's *Style of Music* box:
```
dance-pop, 128 BPM, driving four-on-the-floor, high-energy, bright belted female vocals, catchy melodic topline, continuous wall-to-wall vocals, vocals start immediately, no instrumental intro, no instrumental breaks, polished modern mix
```

**2) LYRICS field** — paste into Suno's *Lyrics* box (the master = Hook 1 + Body, verbatim):
```
[Chorus]
Light me up, light me up, LOO-may
Turn my afternoon around today
[Verse 1]
Three in the afternoon and I'm already done
Staring at the screen but my brain's on the run
[Verse 2]
One little sip and the gray turns to gold
Clean quick energy, do what I'm told
No sugar crash, no shaky hands
Back in the game, back on my grind again
[End]
```

**3) Settings:**
- **Exclude Styles:** `rap, hip-hop, spoken word, instrumental intro, instrumental break, breakdown, slow tempo` (wide list — account-tested better than a trimmed one)
- **Sliders:** Weirdness ~30% · Style Influence ~75% (note the exact values and reuse them for every hook mini-generation)
- **Voice:** create one from the winning master take (song page ⋯ menu; "Personas" are named **Voice** in the current UI) and select it for both hook mini-generations
- **Stated BPM + key:** 128 BPM, key of F♯ minor
- **Hook-arc style string** (for the two hook mini-gens only — the body keeps the full-throttle string above):
  ```
  dance-pop, 128 BPM, bright belted female vocals, stripped minimal opening, sparse percussion, vocals dominate the mix, singer begins on the first beat, tension building gradually, rising energy toward a full driving drop, catchy melodic topline, ends cold on the final word
  ```
- **Brand respelling (flagged):** "Lumé" is respelled **LOO-may** in the sung lyrics so Suno pronounces it right — same word, sung-spelling only. OK to keep?

**4) Hook variants** — each is its **own standalone generation**, rendered with the master's **Voice** selected, the **hook-arc style string**, and the same sliders. Paste as the complete Lyrics field:
```
[Chorus]
Wake me up, wake me up, LOO-may
Chase the heavy fog away
[End]
```
```
[Chorus]
Charge me up, charge me up, LOO-may
Feel the switch flip on today
[End]
```
Roll 2–3 of each and judge **only the vocal part**. A short generation pads an instrumental tail even with `[End]` — that's expected, crop it in the editor rather than re-rolling.

**5) Assembly runbook:**
1. Generate the **master** (Style + Lyrics above + settings). Iterate until the **body** is right — it's the asset you protect. This take is also ad #1.
2. Make a **Voice** from the winning master take, and note the exact slider values.
3. **Hook 2 and Hook 3:** render each as a standalone mini-generation — the block from step 4 as the whole Lyrics field, the **hook-arc string** as the Style, the master's **Voice** selected, same sliders.
4. **Editor pass on every keeper** (master and both hook clips): play it once, then **Crop / Remove Section** any instrumental intro, break, or trailing fade. Credit-free and deterministic. Crop each hook clip to its last sung word.
5. **Export the body once.** From the master, export the body section as a single WAV and reuse that one file for all three ads — this is what makes the body identical by construction.
6. **Join in an external editor:** hook clip, then a tight riser, with the **impact drop landing on the body's first downbeat**. Butt-cut on the transient; add a short equal-power crossfade only if a tail rings. Keep the drop to about one beat. Pitch-preserving time-stretch fixes small tempo drift; a sour take gets re-rolled, not rescued.
7. You now have 3 songs sharing a genuinely identical body, each playing continuous hook to body. (Short song — no Extend needed here.)

**6) Visual / timing seed (hand-off to the animation skill):**
- **Hook** lands at 0s, ~4s long — the brand name hits on the downbeat of the hook's last line.
- **Beats:** `[0–4s]` hook · `[4–12s]` verse 1–2 (the pitch) · cold end ~16–20s.
- **Mood:** bright, propulsive, "afternoon slump → switched-on"; energy rises into the hook and holds.

**Duration:** ~16–20 seconds (short). **External audio:** none.

## Why it's built this way (the song deltas)
- **Verbatim words** — the script is sung exactly; only `[tags]`, one brand respelling, and line breaks were added. No line was repeated to force a chorus.
- **Two fields, strict** — genre/BPM/vocal live in the Style box; only words + tags in the Lyrics box.
- **Gapless + non-rap** — opens on the hook (no `[Intro]`), no `[Bridge]`/`[Instrumental]`, **no blank lines between sections** (blank space invites instrumental fills), `[End]` as the literal last line; BPM + sung genre up front; belt-and-suspenders anti-gap wording (positive phrases + in-Style negations + the wide Exclude list — account-tested).
- **Matched hooks** — each hook is anchored to the master by its **Voice**, and the body is one exported file reused three times, so consistency is structural rather than hoped for. **Replace Section is not used**: it failed on a real leading-hook swap and was demoted.
- **Two strings, not one** — the body renders at full throttle; the hooks use the arc string so they build into the drop instead of slamming in hot.
- **One sound per set** — the Voice + sliders + BPM/key are frozen across all three variants.

## To calibrate (fold wins back into `models/suno.md`)
Run it, then note: did the hook come in immediately with no dead air? did it stay **sung** (never rap)? did the Voice lock actually hold the singer across the standalone hook gens — the one mismatch no edit can hide? did the riser-and-drop join read as intentional, or did the energy reset sound like a seam, especially where your real hooks **vary a lot in length**? did the brand name pronounce right? Adjust, and log the fix.
