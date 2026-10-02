---
style: high-energy-nonrap
version: 1.1.0
updated: 2026-10-02
---

# Style — High-Energy, Non-Rap (brand-agnostic)

Fast, driving, gapless brand songs with **continuous sung vocals** — energetic and modern, **never rap or spoken-word**. Works for **any brand**; the brand is just the script's words + the sound you pick. This is the house default for ad songs.

## What defines this sound
- **Fast + driving** — a front-loaded numeric **BPM** and a propulsive pulse (`driving beat`, `four-on-the-floor`, `relentless`, `non-stop momentum`).
- **Gapless** — vocals in immediately, no instrumental intro, no mid-song breakdown, a hard cold end. (Structure rules → `models/suno.md`.)
- **Sung, not rapped** — melodic, belted, hook-forward delivery; rap/hip-hop/spoken-word actively excluded.
- **Polished, radio-ready mix** — clean and present, not lo-fi.

## Pick a genre from the menu (fast, sung, non-rap)
Lead with the **script's vibe**; offer 2–3 as distinct treatments. BPMs are typical anchors (a strong bias, not a lock):

| Genre | Feel / BPM |
|---|---|
| Liquid drum & bass | breakneck, sung topline · ~174 |
| Dance-pop | glossy, belted hooks · ~128 |
| Eurodance | euphoric, catchy · ~135 |
| Electropop / synth-pop | bright, driving · ~124 |
| Pop-punk | fast, anthemic, youthful · 160–200 feel |
| Power-pop / pop-rock | big guitar choruses · fast |
| Hyperpop | loud, glitchy, very fast · high |
| Hardstyle / happy hardcore | euphoric belted, relentless kick · ~150 |
| Trance / uplifting trance | soaring vocals · ~138 |
| Future house / house-pop | four-on-the-floor + pop topline · ~126 |

**Avoid** (bias to rap/spoken/slow): trap, drill, boom bap, hip-hop, nu-metal, grime, ballad.

## Audience → genre (a HINT only — use when the script makes the audience obvious)
Curated to this fast/non-rap family. Lead with the script's vibe; reach for this only as a tie-breaker.

| Audience (if evident) | Lean toward |
|---|---|
| Gen Z women | dance-pop, hyperpop, electropop |
| Gen Z men | EDM, pop-punk, future house |
| Millennial women | dance-pop, electropop, power-pop |
| Millennial men | pop-punk, power-pop, house-pop |
| Fitness / hype | hardstyle, drum & bass, EDM |
| Gamers | hyperpop, future house, DnB |
| Tech / SaaS | electropop, future house, EDM |
| Beauty / skincare | dance-pop, hyperpop, electropop |
| General / broad | dance-pop, eurodance |

*(If the demo isn't obvious from the script, don't guess — pick on the script's energy alone.)*

## Style-field template (fill the `[BRACKETS]`; keep the rest)
Comma-separated, genre first, BPM front-loaded, ~15–30 words. Reinforce gapless + anti-rap. Exclude-Styles + settings → `models/suno.md`.

```
[genre], [BPM] BPM, driving beat, high-energy, [vocal — e.g. bright belted female vocals], catchy melodic topline, continuous wall-to-wall vocals, vocals start immediately, no instrumental intro, no instrumental breaks, polished modern mix
```

**Exclude Styles:** `rap, hip-hop, spoken word, instrumental intro, instrumental break, breakdown, slow tempo` (wide list — an account A/B beat the trimmed "2–5 entries" version; keep it wide)
**Advanced → More Options:** Vocal Gender set · Personalize Off · Duration Auto (Custom = test) · **never press the Styles magic wand**. **Sliders:** **Variety Off (0)** (or the Style gets rewritten) · Weirdness low · Style Influence high (note exact values; reuse across the set) · **Max Mode ON** for anything over 2 minutes
**Long songs (5–10 min):** add `full band throughout, sung vocals throughout` to the Style string, add `whisper, whispered vocals, a cappella, ambient, narration` to Exclude, and follow the long-songs recipe in `models/suno.md` (untested on v6)

## Optional pacing block (paced ads: energetic, transformation, urgency) [from a peer team's SOP; untested by us]
Append to the Style string when the song must feel fast, not just have a high BPM:
```
nearly continuous singing, gaps under one second, short syllabic rhythmic phrasing, quick line-to-line delivery, no sustained notes, no long held vowels, no melisma, no vocal runs
```
Not for slow or emotional songs. Watch that dense lines don't tip into rap (keep the rap Exclude).

## Account-proven strings (male ad set, 2026-07 render A/Bs — on v5.5, now retired; re-test on v6)
Best gapless run so far — **dance-pop beat anthemic pop-rock** (guitar-led rock invites riffs/turnarounds between phrases; four-on-the-floor pop keeps the topline riding the beat):
```
high-energy dance-pop, 160 BPM, driving four-on-the-floor beat, gritty belted male vocals, vocals dominate the mix, singer begins on the first beat, wall-to-wall continuous vocals, catchy melodic topline, tight punchy modern mix
```
**Exclude Styles for that run:** `instrumental intro, instrumental break, breakdown, rap, spoken word`
Notes: `vocals dominate the mix` measurably pulled vocals forward; 148 → 160 BPM both stayed sung. The hook-arc variant (stripped opening building toward a drop) lives in `models/suno.md` (Job A).

## Banned words in the Style field (they backfire here)
Avoid hype/cinematic words that trigger long intros or vague results: `cinematic`, `epic`, `orchestral`, `atmospheric`, `stunning`, `breathtaking`, `professional voiceover`. (`anthemic` was flagged by one guide as an intro-trigger but tested fine on our account; "no instrumental intro / no instrumental breaks" phrases also tested fine — better than without, despite pink-elephant lore.) Say the concrete sound instead (`driving`, `belted`, `polished mix`).

## Notes
- One sound per set — the chosen treatment's Style string + Style Persona + sliders (Variety 0) + BPM/key are reused across all 3 hook variants and every extend.
- Everything about *matching the body* and *building long songs* is method, not sound → `models/suno.md`.
