---
style: high-energy-nonrap
version: 1.0.0
updated: 2026-07-14
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
[genre], [BPM] BPM, driving beat, high-energy, [vocal — e.g. bright belted female vocals], catchy melodic topline, continuous vocals, vocals start immediately, no instrumental breaks, polished modern mix
```

**Exclude Styles:** `rap, hip-hop, spoken word, instrumental break, breakdown, slow tempo`
**Sliders:** Weirdness low · Style Influence high (note exact values; reuse across the set)

## Banned words in the Style field (they backfire here)
Avoid hype/cinematic words that trigger long intros or vague results: `cinematic`, `epic`, `orchestral`, `atmospheric`, `stunning`, `breathtaking`, `professional voiceover`. Say the concrete sound instead (`driving`, `belted`, `polished mix`).

## Notes
- One sound per set — the chosen treatment's Style string + Persona + sliders + BPM/key are reused across all 3 hook variants and every extend.
- Everything about *matching the body* and *building long songs* is method, not sound → `models/suno.md`.
