# Model layer — Suno v5.5, Pro tier (current)

> The **swappable** file. Everything Suno-specific lives here; the chassis / styles / craft never name a model. When we move tools, replace this file (and add `models/<new>.md`).
>
> **Plan reality: Suno PRO ($10/mo), NOT Premier — so there is NO Suno Studio.** Every method below runs on Pro + the team's normal video/audio editor (CapCut / Premiere / DaVinci Resolve / Audacity). Don't design around Studio.

## The two fields — keep them strict
Work in **Custom Mode** (not Simple). Two boxes, and mixing them is the #1 quality killer:
- **Style of Music field** = the *sound world* — genre, sub-genre, BPM, mood, vocal type, instruments, production. Comma-separated tags, **space after each comma**, **genre first**, ~**15–30 words** (over ~40 = mush). Cap ~1,000 chars.
- **Lyrics field** = the *sung words + structure* — the script verbatim, with section tags, vocal cues, and phonetic respellings. Cap ~**5,000 chars**. **More lyrics = a longer song, not a denser one** — Suno derives duration from the lyrics, so packing toward the cap does NOT squeeze out instrumentals; past ~3,000 chars it tends to rush, skip, or truncate lyrics instead (the ~3,000 figure is community folklore from one source cluster; the rush mechanism is multi-source, and applies to v4.5/v5/v5.5 alike). **Structure tags only work here**, never in Style.

Rule of thumb: *sound world → Style; sung words + arrangement → Lyrics.* Genre/production words placed in Lyrics get **sung**; lyrics placed in Style are ignored.

## Hard specs (v5.5)
- **Single generation:** ~**8 minutes** max, ~**5,000-char** lyrics. Longer songs → **Extend** (below).
- **Each Extend:** ~+60s; chainable; **Get Whole Song** stitches an extend chain into one file (free).
- **Export on Pro:** WAV + MP3 + video. **Stems:** Split-from-Mix (2 stems, ~10 cr) and Auto Split (up to 12 stems, ~50 cr). Advanced Split (~100 instruments) and MIDI are Premier-only.
- **Full commercial rights on Pro.** 2,500 credits/mo.

## Structure / meta tags (Lyrics field)
Each tag on its **own line**, immediately before that section's lyrics. Tags are **probabilistic signals, not commands** — reliable when the words and the Style agree.
- **High reliability (use freely):** `[Verse]` / `[Verse 1]` (number them), `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[Outro]`, `[End]`. `[End]` / `[Outro: Cold End]` = hard stop.
- **Medium (reinforce intent in Style too):** `[Whispered]`, `[Belted]`, `[Spoken]`, `[Harmonies]`, `[Staccato]` (crisp separated syllables — best for enunciating brand names). Colon-modifiers work on v5+: `[Chorus: big harmonies, full band]`.
- **Low (use sparingly, test):** ad-libs, sound-effect tags, exotic composite tags.
- **Section count:** 6–8 sections is the stable norm; 10+ makes delivery *rushed*. ("More tags = more instrumental turnarounds between sections" is unsupported — gaps come from blank lines and gap-inviting tags, not from section count.)
- **Parentheses are SUNG** (backing vocals) — never write instructions like "(no instrumental)" in the Lyrics field; brackets are read, parens are performed.
- **BPM / key go in the Style field as plain text** (`140 BPM, key of A minor`), never as bracket tags. Numeric BPM is a **strong bias, not a hard lock**.

## Fast, driving, gapless — but NOT rap
1. **Front-load BPM + a driving adjective** in Style: `174 BPM, liquid drum & bass, relentless, driving...`. Word-tempo → BPM: mid ~90–120, uptempo ~120–140, fast ~140+.
2. **Fast *sung* genres (not rap):** drum & bass (~174), dance-pop (~128), eurodance (~135), electropop, pop-punk (160–200 feel), hyperpop, hardstyle (~150), trance (~138), future/house-pop (~126). **Avoid** (bias to rap/spoken/slow): trap, drill, boom bap, hip-hop, nu-metal, grime. (Menu → `styles/high-energy-nonrap.md`.)
3. **Kill gaps structurally:** never open `[Intro]` (that's the dead-air trap — open on `[Chorus]`/`[Verse 1]` with a lyric on the next line); **omit** `[Bridge]` / `[Instrumental]` / `[Break]` / `[Drop]`; **no blank lines between lyric blocks** (blank space invites instrumental fills — keep the text tight against the tags); end on `[Outro]` carrying 1–2 *sung* lines, then `[End]` as the literal last line. Style reinforcement is **positive-only**: `vocal-forward production, singer begins on the first beat, continuous vocals, non-stop momentum` — never "no X" phrases in Style (pink-elephant effect: "no drums" *adds* drums; negations belong in Exclude Styles). Prompt-side is probabilistic; the **deterministic** fix is the editor pass (below).
4. **Stay sung, not rapped:** lead with `melodic, sung, belted, catchy topline, big singalong chorus` (caution: "anthemic" is flagged by one source as an intro-trigger word — prefer the concrete phrases); **Exclude Styles:** `rap, hip-hop, spoken word` (more reliable than typing "no rap"). Cramming too many words per section flips Suno into double-time = rap — and the "fill the character limit" hack doesn't shrink instrumentals anyway (it lengthens or rushes the song). If a dense script must *stay* dense (gapless ads), fix rushing with **more line breaks on long lines** (verbatim-safe), steadier syllable counts line-to-line, and calmer delivery descriptors — **never** by raising BPM, and never by thinning words when gaplessness is the goal.

## Exclude Styles & Creative Sliders (Pro)
- **Exclude Styles** (Advanced Options): list what to keep out — e.g. `rap, hip-hop, spoken word, guitar solo, extended intro`. Keep to **2–5** specific exclusions (more and effectiveness collapses); they're guidance, not hard bans, so also assert the positive genre. This is the **only** correct home for negations — "no X" phrasing inside the Style field backfires.
- **Sliders:** **Weirdness low + Style Influence high** for predictable, on-brand output. **Note your exact slider values** and reuse them across a set (esp. for the 3-hook and long-song jobs). Turn OFF the "Prompt Enhancement" helper when hand-tuning — it rewrites your Style.

## Personas — lock the singer across a set
A **Persona** captures a chosen take's vocal + style so later generations sing in the same voice. Create from your best take; **set gender explicitly**. Reuse it for every hook swap and every extend so the voice never drifts. (v5.5 **Voices** = clone from a recorded sample; confirm availability on Pro.)

## The editor pass — the deterministic gap-killer (Pro)
Every prompt-side gap technique only raises the odds. After **Get Whole Song**, play the track once and use the **Song Editor**: **Crop / Remove Section** deletes instrumental intros, mid-song breaks, and outro fades **credit-free**; **Replace Section** regenerates a bad span. Budget one editor pass per keeper before exporting WAV — any gap that survives the prompts dies here, not in the video edit.

## Brand names & tricky words — fix BEFORE generating (permanent after)
Suno sings from spelling, not meaning, so coined brand names mispronounce.
- **Phonetically respell** the *sung* pronunciation (`NovaGrip → NOH-vah-grip`); hyphens act as syllable/beat separators; capitalize to segment.
- Acronyms → hyphenate/space (`A-I`) or spell as words; numbers → words. Use **one spelling** everywhere the name appears; `[Staccato]` on the brand line for crisp enunciation.
- **This is the ONE place spelling may change** — it changes spelling, not the word. Flag each respelling and get the user's OK; it doesn't violate the verbatim rule (the word is the same).

## Job A — 3 hooks + 1 body with a consistent body
Separate renders of body and hooks will **not** share the same tempo/key/vocal take, so they won't match. Generate each hook **in-context** instead:
1. **Master:** generate one song = **Hook 1 + Body**. Open on the hook as its own tagged section (`[Chorus]`), then the body sections. Lock **Persona + slider values + BPM/key**. Iterate until the **body** is right — it's the asset you protect.
2. **Variants:** use **Replace Section** to regenerate **only the hook** → Hook 2, then Hook 3. Because the new hook is generated inside the master, it inherits the body's tempo/key/voice and leads seamlessly into it. Replace Section **is a Pro feature** (no Studio needed).
3. **Export** all three (WAV).

> **Known weak spot to test on render 1:** Replace Section is least reliable when the swapped section is at the very **start** *and* the hooks **vary a lot in length** (a much-longer/shorter hook can over-generate or nudge the body). If it struggles, fallbacks: keep hooks closer in length; keep the hook on a clean bar/section boundary; or assemble in an external editor (reuse one exported body WAV + a hook clip in front, tempo-matched + crossfaded). Calibrate and fold the winner back here.

## Job B — long songs (7–9 min) via Extend
No Studio warp-lock on Pro, so **minimize drift natively, then clean up in a free DAW.**
- **Derive the full section map from the whole script first** so tag numbering (`[Verse 4]`…) is right end-to-end.
- **Generate the longest coherent block in ONE pass** (fit as much as ≤5,000 chars / ~8 min) — one pass = zero seams for most of the song.
- **Extend minimally (aim ≤2).** Per extend: **re-paste the exact Style string incl. BPM + key** (style is NOT inherited — omitting it is the #1 drift cause), keep the **same Persona + frozen sliders**, extend from a **clean bar line / phrase end starting slightly early** (never mid-word), and paste **only the next lyric block** (never earlier lines, or it re-sings/restarts).
- **Get Whole Song** after each keeper extend (clean recovery points), then **download WAV**.
- **Fix residual drift in a free DAW** (DaVinci Resolve / Audacity): loudness-match sections, pitch-preserving Change-Tempo to conform a drifting tail to the master BPM, equal-power crossfade seams; **re-extend** a key-clashed section rather than pitch-shifting.
- **Quality ceiling:** clean to a normal listener at one pass + ~1 extend; drift audible past ~2–3 extends. High-BPM driving tracks hide seams better than sparse ones. This long body can also be the "body" for Job A.

## Symptom → fix table (starting points — calibrate on real generations)
| Symptom | Fix |
|---|---|
| Long instrumental intro / dead air | Remove `[Intro]`; open on `[Chorus]`/`[Verse 1]` with a lyric on the next line; add "singer begins on the first beat, vocal-forward production" to Style; avoid build-words (epic, cinematic, orchestral, possibly anthemic); crop any residue in the editor. |
| Mid-song slowdown / gap | Omit `[Bridge]` / `[Instrumental]`; delete blank lines between lyric blocks; chain vocal sections; add "continuous vocals" to Style (positive phrasing only); Remove Section in the editor if it still appears. |
| Drifts into rap / machine-gun | Assert `melodic, sung, belted` + a sung genre; Exclude `rap, hip-hop, spoken word`; don't overstuff a section; if the script must stay dense, add line breaks on long lines + steady syllable counts and calm the descriptors (never raise BPM). |
| Genre drift | Raise Style Influence; 1–2 genre tags, dominant first; cut opposing tags. |
| Off-key / wobbly vocals | State gender explicitly; add `pitch perfect, in tune`; resolve conflicting Style tags. |
| Brand name mispronounced | Phonetically respell before generating (permanent after); `[Staccato]` on the brand line. |
| Abrupt / awkward ending or long fade | `[Outro]` with 1–2 sung lines, then `[End]` as the last line; don't leave the song tag-less; crop a lingering fade in the editor. |
| Instrumental gap survives every prompt fix | Song Editor **Crop / Remove Section** (credit-free, deterministic) before export. |
| Hooks don't match the body | Don't render hooks separately — use the master + Replace Section (Job A). |
| Voice changes across hooks/extends | Lock one Persona + frozen sliders across the whole set; re-paste Style each extend. |
| Tempo/voice drift on a long song | Fewer extends; re-paste Style incl. BPM/key each extend; DAW Change-Tempo + crossfade on cleanup. |

## Confirm in-app (all limits were sourced from docs behind a fetch block — verify on the real account)
- True ~8-min single-pass cap and ~5,000-char lyrics limit on this account.
- Whether **Voice cloning** and any monthly **download cap** apply on Pro.
- **Get Whole Song** reliably reassembles a 4+ extend chain without re-charging.
- Current **stem credit costs**; that **Custom Models** is Premier-only.
- **The render-1 test:** does Replace Section cleanly swap a variable-length leading hook while keeping the body consistent + the seam seamless?

*Confidence: field separation, structure tags, Exclude Styles, sliders, Personas, Extend/Get-Whole-Song, and Pro-vs-Premier tiering are corroborated across multiple 2026 sources; exact numeric limits and the identical-body/long-song seam behavior are starting points to calibrate on your own account — fold wins back into this table.*

*Research pass (2026-07): a web-verification sweep (official Suno help docs + prompting-guide sites; Reddit unreachable to the crawler) confirmed: more lyrics → longer/rushed song, NOT fewer instrumentals (packing the char cap is not a gap-suppression technique); in-Style "no X" negations backfire (pink-elephant) — negations go in Exclude Styles (2–5 entries); blank lines between lyric blocks invite instrumental fills (single-cluster source); `[Outro]` + sung lines + `[End]` is the consensus anti-fade ending; editor Crop/Remove Section is the only deterministic gap fix. Guide-site corroboration may share one lore cluster — keep calibrating on real renders.*
