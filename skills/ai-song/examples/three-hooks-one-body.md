# Examples — 3 hooks + 1 body (worked draft, v1 — test & calibrate)

> **Not yet production-tested.** Drafted from the chassis + research to show the shape. Your team runs the first real song and we tune from the feedback, folding wins back into `models/suno.md`. Swap the brand/script for your own.

A short, fast **dance-pop** brand song from an invented script (`Lumé`, a focus/energy drink). One **master** = Hook 1 + Body; Hooks 2 & 3 are **Replace-Section swap blocks** so each hook is regenerated *in-context* and matches the same body. The words are **verbatim** — only tags, a vocal cue, line breaks, and one flagged brand respelling were added.

## The package (this is the full deliverable shape)

**1) STYLE field** — paste into Suno's *Style of Music* box:
```
dance-pop, 128 BPM, driving four-on-the-floor, high-energy, bright belted female vocals, catchy melodic topline, vocal-forward production, singer begins on the first beat, continuous vocals, polished modern mix
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
- **Exclude Styles:** `rap, hip-hop, spoken word, instrumental break, extended intro` (2–5 max — the only home for negations)
- **Sliders:** Weirdness ~30% · Style Influence ~75% (note the exact values and reuse them for every hook swap)
- **Persona:** create one from the winning master take (female, bright, energetic) and reuse it for both hook swaps
- **Stated BPM + key:** 128 BPM, key of F♯ minor
- **Brand respelling (flagged):** "Lumé" is respelled **LOO-may** in the sung lyrics so Suno pronounces it right — same word, sung-spelling only. OK to keep?

**4) Hook variants** — in the finished master, use **Replace Section** on the opening `[Chorus]` and paste one of these (re-paste the Style string, keep the same Persona + sliders):
```
[Chorus]
Wake me up, wake me up, LOO-may
Chase the heavy fog away
```
```
[Chorus]
Charge me up, charge me up, LOO-may
Feel the switch flip on today
```

**5) Assembly runbook:**
1. Generate the **master** (Style + Lyrics above + settings). Iterate until the **body** is right; make a **Persona** from that take.
2. **Variant 2:** on the master, **Replace Section** the opening `[Chorus]` → paste Hook 2, re-paste the Style string, keep the Persona + slider values. Export WAV.
3. **Variant 3:** same, with Hook 3. Export WAV.
4. **Editor pass on each keeper:** play it once; **Crop / Remove Section** any instrumental slip (credit-free), then export. You now have 3 songs sharing a consistent body, each continuous hook→body. (Short song — no Extend needed here.)

**6) Visual / timing seed (hand-off to the animation skill):**
- **Hook** lands at 0s, ~4s long — the brand name hits on the downbeat of the hook's last line.
- **Beats:** `[0–4s]` hook · `[4–12s]` verse 1–2 (the pitch) · cold end ~16–20s.
- **Mood:** bright, propulsive, "afternoon slump → switched-on"; energy rises into the hook and holds.

**Duration:** ~16–20 seconds (short). **External audio:** none.

## Why it's built this way (the song deltas)
- **Verbatim words** — the script is sung exactly; only `[tags]`, one brand respelling, and line breaks were added. No line was repeated to force a chorus.
- **Two fields, strict** — genre/BPM/vocal live in the Style box; only words + tags in the Lyrics box.
- **Gapless + non-rap** — opens on the hook (no `[Intro]`), no `[Bridge]`/`[Instrumental]`, **no blank lines between sections** (blank space invites instrumental fills), `[End]` as the literal last line; BPM + sung genre up front, rap excluded via Exclude Styles (never "no X" in Style — pink-elephant effect).
- **Matched hooks** — the master + Replace-Section method regenerates each hook *inside* the body, so tempo/key/voice match; hooks are **not** rendered separately.
- **One sound per set** — the Style string + Persona + sliders + BPM/key are frozen across all three variants.

## To calibrate (fold wins back into `models/suno.md`)
Run it, then note: did the hook come in immediately with no dead air? did it stay **sung** (never rap)? did Replace Section swap the hook cleanly while the **body stayed consistent** and the seam stayed seamless — especially if your real hooks **vary a lot in length** (the #1 thing to watch)? did the brand name pronounce right? Adjust, and log the fix.
