# Model layer — Suno v6, Pro tier (current)

> The **swappable** file. Everything Suno-specific lives here; the chassis / styles / craft never name a model. When we move tools, replace this file (and add `models/<new>.md`).
>
> **Plan reality: Suno PRO, NOT Premier — so there is NO Suno Studio** (Studio, with its BPM lock, MIDI, multitrack and plugins, is Premier-only [official]). Every method below runs on Pro + the team's normal video/audio editor (CapCut / Premiere / DaVinci Resolve / Audacity).

> **Source tags — read these before trusting a line.**
> - **[official]** = read on a Suno page (help.suno.com, suno.com/release-notes, suno.com/pricing), 2026-10-01/02.
> - **[v5.5-tested]** = proven on OUR account on v5.5 in 2026-07. **v5.5 is retired** [official], so these are the best starting point but are **not yet re-tested on v6**.
> - **[community]** = guide sites / forum reports: lore until a render on our account confirms it.
> - **[peer-SOP]** = from another ad-song production team's working SOPs (shared privately with Aman, 2026-10-02; field-used by them, untested by us).
> - **[Kang idea]** = Kang's own reasoning, from no source. A hypothesis to test, not a fact.
> When a render settles a line, change its tag and log it in `docs/prompt-log.md`.

## The model (since 2026-09-09)
- **Use `v6`** (flagship, Pro/Premier). `v6-wild` "takes ideas in less predictable directions"; `v6-mini` is the fast free tier. [official] All pre-v6 models are retired: "you can't generate new songs" with them. [official]
- **Max Mode** — a per-generation toggle: "when you want v6 to spend more on getting it right … best for: songs longer than two minutes … and keeping vocals and style consistent through the whole track." Costs more credits [official]; about 2x (20 per generation) [community]. **Default ON for anything over 2 minutes** (all long songs, every Extend, and the Job A master).
- **Variety slider** (new) — "introduce[s] variety in your outputs by adjusting and updating your style prompts. If you'd like to retain full control of your style tags, reduce the Variety slider to 0." [official] **Always 0.** Anything else silently rewrites our locked Style string, which breaks "same Style across the set".

## The v6 create screen, as Aman's account shows it (screenshots 2026-10-02) [seen in-app]
- **Songs** tab (also *Speech* and *Sounds*) → **Simple / Advanced**: use **Advanced** (the old "Custom Mode"). Model picker top-right: **v6**.
- Buttons above the fields: **+ Audio**, **+ Voice**, **+ Inspo**. The singer lock lives under **+ Voice**: "Style Personas are still available within the Voices menu". You make one from a song in your library via **Create > Voice** [official].
- **Lyrics** box, then a **Styles** box with tag chips and three buttons: a library button, a **blue magic-wand button** and a refresh button. The wand is **Style Augmentation**: it rewrites your Style input, and with My Taste on it pulls from "your listening and creation habits" [official]. **Never press it on our locked string.**
- **More Options**, with these defaults on the screenshot:

| Setting | Default seen | Our setting |
|---|---|---|
| Exclude styles | empty | house list |
| **Vocal Gender** (Male / Female) — NEW | unset | **always set it** to match the singer (also say it in Style). One v6 user reports it slipping ("keeps trying to change my mezzo soprano to a male voice") [press], so expect an extra roll |
| **Duration** (Custom / Auto) — NEW | Auto | Auto for normal songs. Custom reportedly runs from 10s to 6 min, default 3:00 [community]. It is "a target, not a guarantee": too few lyrics for the length get padded with instrumental [community]. **Test only**; never use Custom to stretch a short script |
| **Max Mode** | **Off** | **On** for anything over 2 min |
| Weirdness | 50% | low (note the value) |
| Style Influence | 50% | high (note the value) |
| **Variety** | **Off** (leftmost) | **Off** (= 0) |
| **Personalize ("My Taste")** — NEW | Off | **Off** (keeps the output on our Style, not the account's taste) |

## The two fields — keep them strict
Work in **Advanced** (formerly Custom Mode; not Simple). Two boxes, and mixing them is the #1 quality killer:
- **Style of Music field** = the *sound world* — genre, sub-genre, BPM, mood, vocal type, instruments, production. Comma-separated tags, **space after each comma**, **genre first**, ~**15–30 words** (over ~40 = mush) [v5.5-tested]. *Conflict:* one detailed v6 guide uses a long 120–180-word formula (genre+tempo → vocal performance verbs → each instrument → arrangement → production) [community]. Test before changing. Cap ~1,000 chars [community]. **There are no BPM/key fields** — BPM and key stay plain text in Style [official, by absence].
- **Lyrics field** = the *sung words + structure* — the script verbatim, with section tags, vocal cues, and phonetic respellings. Cap ~**5,000 chars** [community]. **More lyrics = a longer song, not a denser one**; past ~3,000 chars per generation delivery tends to rush, skip or truncate [community + v5.5-tested]. **Structure tags only work here**, never in Style.

Rule of thumb: *sound world → Style; sung words + arrangement → Lyrics.* Genre/production words placed in Lyrics get **sung**; lyrics placed in Style are ignored.

## Hard specs (v6, Pro)
- **Single generation:** "up to 8 minutes … across v6, v6-wild, and v6-mini". [official] Lyrics ~5,000 chars [community].
- **Generation cost:** "two songs with a total cost of 10 credits" (standard) [official]. 2,500 credits a month on Pro [official].
- **DOWNLOADS ARE CAPPED: Pro = 20 songs a month** (from 2026-09-03; Premier 60). "One song counts as one download, regardless of format"; downloading it again is free; its stems count as part of it; no rollover. [official] **This, not credits, is now the real limit.** Download only keepers; plan a month's sets around 20.
- **Stems on Pro:** Auto split and Split from mix; Advanced split is Premier-only. [official]
- **Commercial rights — two official pages disagree.** The download-limits FAQ: rights apply to songs "you download from the platform as a paying subscriber". The ownership article: ownership follows "subscription status at the time of creation". [official, both] Safe practice: make it on Pro AND download it on Pro.

## Structure / meta tags (Lyrics field)
Each tag on its **own line**, immediately before that section's lyrics. Tags are **probabilistic signals, not commands** — reliable when the words and the Style agree. (No official v6 tag guide exists; this list is inherited from v5.5. [v5.5-tested/community])
- **High reliability (use freely):** `[Verse]` / `[Verse 1]` (number them), `[Pre-Chorus]`, `[Chorus]`, `[Bridge]`, `[Outro]`, `[End]`. `[End]` / `[Outro: Cold End]` = hard stop.
- **Colon modifiers carry the arrangement:** `[Verse 3: full band, driving drums, sung]`. Use them to restate the music on every section of a long song (see Long songs). [community]
- **Medium:** `[Belted]`, `[Harmonies]`, `[Staccato]` (crisp syllables — best for brand names).
- **Never in our songs:** `[Whispered]`, `[Spoken]`, `[Interlude]`, `[Breakdown]`, `[Build]`, `[Instrumental]`, `[Break]`, `[Drop]`. They invite exactly the whisper / no-music stretches we are fighting.
- **Never use "quiet" section directions either:** *stripped back, minimal production, intimate vocal, soft, emotional vocal, sparse, breakdown, build, a surprise later in the song*. To the model they mean quiet music + a soft or whispered voice. A popular ChatGPT "song arranger" prompt suggests exactly these (`[Bridge - stripped back, emotional vocal]`, `[Breakdown - minimal production, intimate vocal]`), and it is a likely cause of the long whisper stretches [peer-SOP prompt + Kang idea on the mechanism]. If a ChatGPT step arranges the lyrics, check every tag it adds against this list. Also strip its "group vocals / multiple singers / call-and-response": we lock one singer.
- **Section count:** 6–8 sections per *generation* is the stable norm; 10+ rushes delivery. [v5.5-tested]
- **Parentheses are SUNG** (backing vocals) — never write instructions in parens in the Lyrics field.
- **BPM / key go in the Style field as plain text** (`140 BPM, key of A minor`), never as bracket tags. Numeric BPM is a **strong bias, not a hard lock**.

## Matching a reference ad (when the brief comes with one)
- **Use the reference for the SOUND, not as the song.** Export the reference ad's audio, then have it analysed into a Style string: genre, BPM, one vocal, gender, instrumentation, ≤1,000 chars. Then apply our gapless and pacing additions [peer-SOP flow].
- **Measure the BPM yourself** (tap tempo or the editor's grid). Don't trust a chatbot's guess from audio [Kang idea].
- **If you upload it (+ Audio / Cover):** trim it first to the loud, fully sung part, with no quiet intro or soft bridge [Kang idea]. Use it for the **first chunk only**. Once the first 2–3 min of OUR song are good, that becomes the anchor (Persona + Extend from it), and the ad is not used again [Kang idea]. Max Mode ON: "best for … covers where you want the result to stay close to the original" [official].
- **Why a reference drifts on a long song:** an ad is 30–60s long, so after it the model has nothing to copy and invents the rest [Kang idea]. + Inspo makes a NEW song in the style of a playlist (≥1 of your own songs; "3–5 songs" advised) [official], so it is not a copy tool.
- **Rights:** covering another brand's ad song for a client ad is a copyright risk. Taking only the style is safer [Kang idea; not legal advice].
- Style length: the reference flow produces ~1,000-char Style strings, far longer than our 15–30 words. Same open A/B as the long-formula question.

## Fast, driving, gapless — but NOT rap
1. **Front-load BPM + a driving adjective** in Style: `174 BPM, liquid drum & bass, relentless, driving...`. Word-tempo → BPM: mid ~90–120, uptempo ~120–140, fast ~140+.
2. **Fast *sung* genres (not rap):** drum & bass (~174), dance-pop (~128), eurodance (~135), electropop, pop-punk (160–200 feel), hyperpop, hardstyle (~150), trance (~138), future/house-pop (~126). **Avoid:** trap, drill, boom bap, hip-hop, nu-metal, grime. (Menu → `styles/high-energy-nonrap.md`.)
3. **Kill gaps structurally:** never open `[Intro]` (open on `[Chorus]`/`[Verse 1]` with a lyric on the next line); **omit** `[Bridge]` / `[Instrumental]` / `[Break]` / `[Drop]`; **no blank lines between lyric blocks**; end on `[Outro]` carrying 1–2 *sung* lines, then `[End]` as the literal last line. Style reinforcement is **belt-and-suspenders** [v5.5-tested]: positive phrases (`continuous wall-to-wall vocals, vocals start immediately, non-stop momentum`) AND explicit negations (`no instrumental intro, no instrumental breaks`). The v6 community is split on whether in-Style negations backfire [community]; our v5.5 A/B said they help. **v6 guide sites now repeat the opposite**: "no X" in Style gets read as "include X", and Exclude should stay at 1–3 terms (5 maximum) [community; every site repeats the same one anecdote, so it may be a single source]. That is the same lore we refuted on v5.5. **Keep our tested default, and make this the FIRST A/B on v6**: (a) negations in Style vs Exclude-field only; (b) a 3-term vs our 7-term Exclude list. **Say the start and end in plain sentences too** [community, v6], because tags are "hints, not commands" on v6. Test adding to Style: *"Opens on the first sung lyric line with no instrumental intro, no count-in. Ends on a hard stop on the last word. No outro, no fade."* The deterministic fix stays the editor pass.
4. **Pacing is more than BPM** [peer-SOP]: gaps, held notes, long vowels, melisma and vocal runs make even a high-BPM song feel slow, and that SOP's authors say banning them also stopped the slowdown or "warp" at the end of songs. For paced ads (energetic, transformation, urgency), add to Style: `nearly continuous singing, gaps under one second, short syllabic rhythmic phrasing, quick line-to-line delivery, no sustained notes, no long held vowels, no melisma, no vocal runs`. **Not for slow or emotional songs** (their caveat too). **Watch the trade-off:** v6 community advice says stretched vowels rescue a "reading, not singing" vocal [community], so banning sustain may push dense lines toward rap or speech. Test it with the rap Exclude in place. Bonus: clean timing makes the SRT and the animation hand-off easier.
5. **Stay sung, not rapped:** lead with `melodic, sung, belted, catchy topline, big singalong chorus`; **Exclude Styles:** `rap, hip-hop, spoken word`. Too many syllables per bar flips delivery to double-time or speech [community + v5.5-tested]. **Aim for 6–12 syllables per line; split any line over ~15** (verbatim-safe: a line break, never a word change) [community, many sources]. Number every verse (`[Verse 1]`, `[Verse 2]`…), and write a repeated chorus out in full each time the script repeats it. If a dense script must stay dense, fix it with **more line breaks on long lines** (verbatim-safe), steadier syllable counts and calmer descriptors — **never** by raising BPM.

## v6's baseline sound — what prompts cannot fix
Many v6 users report a muffled, compressed, "blanket over the speakers" sound compared with v5.5 [press, quoting users: MusicRadar, Digital Music News, Sep 2026]. Guides attribute it to v6's licensed training data and to codec artefacts [community]. Prompt fixes that help: **remove layers** (pads, backing vocals, reverb) instead of adding quality words ("crisp, radio-ready, mastered" are near-placebo); put the vocal in front: `vocals in front of the band, close and dry, loudest element in the mix` [community]. A buried vocal cannot be fixed by mastering afterwards; re-roll or Replace Section instead.

## Exclude Styles & sliders (Pro)
- **Exclude Styles** (official, Pro/Premier; "exclude … specific instruments, specific styles, or even specific vocal-styles") — house default: `rap, hip-hop, spoken word, instrumental intro, instrumental break, breakdown, slow tempo` [v5.5-tested; wide list beat the "trim to 2–5" lore on v5.5]. **Long songs add:** `whisper, whispered vocals, a cappella, ambient, narration` [community — test].
- **Sliders:** **Variety 0** [official]. **Weirdness low + Style Influence high** for predictable output (50% = "normal" on Weirdness [official]); creators disagree on v6 numbers: Weirdness 0–20% vs 30–50% (one 150-song test found 20% 'stale'; the peer SOP says 0%, after saying up to 50%) [community/peer-SOP]; Style Influence 75% flat vs ~65% for detailed prompts [community]. Start at **Weirdness 30, Style Influence 70** and adjust one at a time. **Note the exact values** and reuse them across a set.
- Turn OFF any "Prompt Enhancement" helper if it appears; it rewrites your Style. (Not seen on an official v6 page — check the UI.)

## Locking the singer on v6 — Personas vs Voices (CHANGED)
v6 has two different things, and our old guide's "Voice" = the first one:
- **Style Persona** — "save the essence of a song — its vocals, style, etc., and recall it for new songs" [official]. Made from one of your own generations. **This is what Job A needs** (lock the master's singer onto the hook clips). It does **not** guarantee an identical timbre [community], so judge the hooks by ear.
- **Voices** (voice cloning) — "record/upload and create with your own voice" (Pro [official]): upload 15s–4min of singing, then read a verification phrase aloud [official]. That is for a **real human's** voice, so it cannot clone the AI singer of a master. Not part of our method.
An **Extend** inherits the source track's voice/key/tempo — the no-Persona fallback.

## The editor (Pro) — repair, don't re-roll
All [official], Song Editor on the song:
- **Remove / Crop:** "Highlight a region … Click Remove … or press the Delete key." Credit-free gap killer: cut instrumental intros, breaks, whisper stretches and fades.
- **Edit Lyrics / Replace Section:** highlight a span → edit the lyrics → "Recreate Section" gives 2 alternates, and "Suno will create a new Whole Song including the updated section." v6 adds plain-language edits: "Change one section while preserving everything else" and "Update a single lyric without rebuilding the entire song." Minimum span is reportedly 10–30s [community].
- **Extend:** "Click the + icon at the far right of the track. Enter a prompt to steer the extension, or use Quick Extend."
- "Get Whole Song" as a separate v6 button is **not confirmed** [official pages silent]; Replace Section output is already a whole song.
- Budget **one editor pass per keeper before download** — any gap or whisper that survives the prompts dies here, not in the video edit.

## Brand names & tricky words — fix BEFORE generating
Suno sings from spelling, not meaning; no pronunciation feature exists on v6 [community].
- **Phonetically respell** the *sung* pronunciation (`NovaGrip → NOH-vah-grip`); hyphens act as syllable separators; capitalize to segment.
- Acronyms → hyphenate (`A-I`) or spell as words; numbers → words. **One spelling** everywhere; `[Staccato]` on the brand line.
- **The ONE place spelling may change** — flag each respelling and get the user's OK.
- **New repair:** if a brand word still comes out wrong, fix that one word with **Edit Lyrics** instead of re-rolling [official mechanism; untested by us].

## LONG SONGS (5–10 min) without whispering or dropped music — Job B
**The failure (our production, 2026-10):** on 8–10 min songs, long stretches turn into whispered or plainly spoken lyrics with no or very quiet music. v6 users report the same: "v6 doesn't sing. It reads"; songs get "weaker and degraded at the end to the point that it's barely just chords and drums". [community]

**Why it happens (ranked by evidence):**
1. **One generation pushed too long.** 8 min is the hard cap [official]; 9–10 min songs exceed it, and quality degrades in the back half of long single passes [community]. Over ~3,000 chars, delivery rushes or skips [community + v5.5-tested].
2. **Too many syllables per bar** — no room to hold notes, so the model flattens into speech [community, mechanism explained].
3. **The music loses its "signal"** — long runs of verse with no restated genre or arrangement drift toward narration [community].
4. **Extend without the Style re-pasted** — style is not inherited [v5.5-tested + community].
5. Gap-inviting tags, blank lines, parentheses [v5.5-tested].

**The recipe (verbatim-safe; every step keeps the script word for word):**
1. **Map the whole script first**, then cut it into chunks at section boundaries: **generation 1 ≈ 1,800–2,500 chars** for our dense ad scripts (3,000 is the outer edge where rushing and truncation start, and dense copy hits it sooner) [community, 5 sources]; each **Extend = ONE section** (two only if both are short). Give each section a single job. Never paste a 9-minute script into one generation.
2. **Settings for every pass:** model `v6`, **Max Mode ON** (it defaults to Off), **Variety Off**, **Vocal Gender set**, **Personalize Off**, the Styles wand off, the same Weirdness/Style Influence, and the same Style Persona once one exists.
3. **Style string:** the set's locked string + `full band throughout, fully sung, continuous band, singer begins on the first beat`. **Re-paste it in full on every Extend**, including BPM + key, and **never change BPM or Style mid-chain** (causes key or vocal swaps at the join) [community, 5 sources: the best-supported single fix]. Exclusions and negative constraints decay fastest across Extends, so restate them each time [community].
4. **Section tags restate the music:** `[Verse 4: full band, driving drums, sung, belted]`, `[Chorus: full band, big harmonies]` — on EVERY section, not only the first.
5. **Exclude:** the house list + `whisper, whispered vocals, a cappella, ambient, narration`.
6. **Lyrics hygiene:** line breaks on long lines (aim ≤ ~10 syllables per line), no blank lines, no `[Whispered]`/`[Spoken]`/`[Interlude]`/`[Breakdown]`, nothing in parentheses.
7. **Continuing past a chunk — two methods, Extend first:**
   - **A. Extend from a timestamp inside the good part (default).** An Extend continues the same audio, so it carries the voice, key and tempo [v5.5-tested]. That is the closest Suno comes to a lock; Pro has no tempo lock, which is Studio/Premier-only [official]. It also skips the slow start a fresh generation has [Kang idea].
   - **B. Overlap-splice (fallback when Extends keep degrading)** [peer-SOP]: make the next part a NEW generation whose lyrics start a few lines BEFORE the previous cut, because a fresh generation starts slow; then join on a line both parts sing, in the editor. Their verdict: "not always perfect, but it's possible". **No guarantee the voice, key or music match** [Kang idea]: separate generations share nothing by construction. Lock everything: a Style Persona from part 1, the identical Style string with BPM + key written, the same model, sliders, Vocal Gender, Variety Off, Max Mode. Keep their method's chunk size down to ours, not 5,000 chars (their own parts slow down at the end).
   - **Check every join by ear:** same tempo (measure it), same key, same singer. Small tempo drift → pitch-preserving time-stretch [v5.5-tested]. A different singer or key → re-roll that part, never patch it.
   **Extend only from a clean bar line or phrase end** that still has full music, never mid-word (mid-word timestamps garble the join or repeat the last 2 seconds) [community]. When repairing, set the Extend point **3–5s before** the spot where it went quiet, so the model hears full music, not near-silence [community]. Paste **only the next lyric block**. **Listen to the last 30s before every Extend** — if whispering has started, crop back to before it and re-extend from there; never extend a whispered tail (the Extend inherits it).
8. **The "Keeper Boundary":** mark the last good timestamp before anything degrades, and only ever rebuild after it [community, 2+ sources]. **Repair what survives:** a short whispered span → **Replace Section** (the selection must be **10–30s** [official]) or Edit Lyrics on that span, with the same lyrics plus "full band, sung"; Remaster and Cover are for tone and mix, not a confirmed fix for whispering [community]; a lost stretch → **Remove** it and re-extend from the last good bar.
9. **Download once, at the end** (one download; downloading every part burns the 20-a-month cap), then loudness-match and fix seams in a free DAW (pitch-preserving Change-Tempo for drift, equal-power crossfades; re-extend a key-clashed section rather than pitch-shifting).

**Where the evidence disagrees:** one creator generates up to 8 minutes in one pass with Custom Duration; two others keep each generation under ~3.5 min because degradation clusters in the back half [community]. Our failure (whispering after the halfway point) matches the second camp, so chunking is the default. **Quality ceiling:** fewer seams = better; high-BPM driving tracks hide seams. Every number above is a starting point — **this recipe has not yet been rendered on v6 on our account.**

## Job A — 3 hooks + 1 body with a consistent body [v5.5-tested method]
Separate unanchored renders will **not** share tempo/key/voice. The account-tested method (v5.5; re-test on v6):
1. **Master:** one generation = **Hook 1 + Body** (Max Mode ON, Variety 0) — the best hook→body transition you'll get, and it *is* ad #1. Iterate until the **body** is right, then save a **Style Persona** from it.
2. **Hooks 2/3 — first try HOOK HARVESTING** [peer-SOP]: in one generation, paste the hook lines 2–3 times in a row (plus a few body lines if there is room), with the master's Persona, style and sliders. A song's opening comes out slow, so the later repeats land at a better pace. Keep the best repeat and cut it out in the editor. It also gets around the ~10s generation floor and the padded tail. Verbatim-safe: the repeats only live in the working file, and the ad uses one copy. **Fallback — standalone mini-generations** with that **Persona selected**: lyrics = `[Chorus]` + the hook lines + `[End]`; style = the **hook-arc string** (below); same sliders. Roll 2–3, judge only the vocal. Short generations pad an instrumental tail even with `[End]` — **crop it in the editor** (`ends cold on the final word` in Style and `instrumental outro, fade out` in Exclude shorten it). *Alternative needing no Persona:* **Extend** the master with only the new hook block — it inherits voice/key/tempo — then slice the tail chorus off.
3. **Assemble in the external editor:** one exported body WAV reused for all three ads + a hook clip in front, joined with a **tight riser + impact drop on the body's first downbeat**. Keep the drop ~1 beat.
4. **Downloads:** master + 2 hook clips = **3 of the 20 monthly downloads** per set. Download only the final keepers.

**Short hook clips:** generations reportedly have a ~10s floor [community], so a 4s hook clip always comes with a tail. Crop it, as on v5.5.

**NEW candidate on v6 (test before trusting):** swap the leading hook **inside the master** with **Replace Section / plain-language edit** — select Hook 1, paste Hook 2's lines, "Recreate Section". Replace Section failed for leading-hook swaps on v5.5 [v5.5-tested]; v6 markets better section edits [official], but one report says the edit applied inconsistently while the voice held [community]. **Catch:** Replace Section needs a **10–30s** selection [official], and our hooks run about 4s. The swap only works if the selection is 10s or more, meaning the hook plus part of the body, which then gets re-sung too. No source confirms a clean swap of a song's first section [community]. Treat this as an upside to test, not the method. If it works, it removes the external join and uses one download per ad.

**The two-string pattern [v5.5-tested]:** a section renders at the energy its style string *describes*. The body wants the full-throttle string; a hook that should **build toward the drop** needs its own arc string, e.g.:
**Hook clips ONLY** (short, so they never reach the whisper zone). Never put "stripped / minimal / sparse" words in a body or long-song Style string:
`dance-pop, 160 BPM, gritty male vocals upfront, stripped minimal opening, sparse percussion, vocals dominate the mix, singer begins on the first beat, tension building gradually, rising energy toward a full driving drop, catchy melodic topline`

## Symptom → fix table
| Symptom | Fix |
|---|---|
| **Long song turns to whispering / spoken lyrics / music drops out** | Long-songs recipe: chunk (≤ ~3,000 chars first pass, 1–2 sections per Extend), Max Mode ON, music restated in every section tag, Style re-pasted every Extend, Exclude `whisper, a cappella, ambient, narration`; crop back + re-extend from the last good bar; Replace Section a short span. |
| Song degrades in the back half ("barely chords and drums") | Shorter first pass; Max Mode; extend in smaller chunks; never extend from a degraded tail. |
| Song feels slow despite a high BPM; drawn-out notes; slows or warps near the end | Pacing block in Style: gaps under 1s, short syllabic phrasing, no sustained notes / held vowels / melisma / runs [peer-SOP]; not for emotional songs; watch for rap drift. |
| Whisper stretches appear where a ChatGPT-arranged tag sits | Remove the quiet section directions (stripped back, minimal, intimate, breakdown, build) and group-vocal tags; restate `full band, sung`. |
| Hooks come out slow with pauses | Hook harvesting: repeat the hook 2–3x in one generation and keep a later repeat [peer-SOP]. |
| Style string seems rewritten / drifts between gens | **Variety slider to 0** [official]. |
| Long instrumental intro / dead air | Remove `[Intro]`; open on `[Chorus]`/`[Verse 1]` with a lyric next; "singer begins on the first beat, vocal-forward production" in Style; avoid build-words (epic, cinematic, orchestral); crop residue in the editor. |
| Mid-song slowdown / gap | Omit `[Bridge]` / `[Instrumental]`; delete blank lines; "continuous vocals" in Style; Remove Section if it persists. |
| Drifts into rap / machine-gun | `melodic, sung, belted` + a sung genre; Exclude `rap, hip-hop, spoken word`; line breaks + steady syllables; never raise BPM. |
| Genre drift | Style Influence up; Variety 0; 1–2 genre tags, dominant first. |
| Off-key / wobbly vocals | Set **Vocal Gender** in More Options and state gender in Style; `pitch perfect, in tune`; resolve conflicting tags. |
| Brand name mispronounced | Respell before generating; `[Staccato]`; if it persists, Edit Lyrics on that word. |
| Abrupt ending or long fade | `[Outro]` with 1–2 sung lines then `[End]`; crop a lingering fade. |
| Short standalone hook clip pads instrumental after `[End]` | Expected — crop to the last word. |
| Hooks don't match the body | Persona-locked mini-gens (or Extend-harvest) joined to ONE exported body WAV; or test the v6 Replace Section swap. |
| Voice changes across hooks/extends | One Style Persona + frozen sliders + Variety 0 across the set; re-paste Style each Extend; Max Mode. |
| Running out of downloads | Download only finished keepers; editor pass first; 20/month on Pro. |

## Confirm in-app
- SEEN 2026-10-02: Variety (defaults Off), Max Mode (defaults Off), Vocal Gender, Duration Custom/Auto, Personalize; no BPM/key fields. STILL TO CHECK: Max Mode's real credit cost; what the blue wand in Styles does; the longest Custom Duration allowed.
- Where Style Personas live now and that a Persona can be made from our own generation.
- Replace Section / Edit Lyrics on Pro, minimum span, and cost.
- Whether "Get Whole Song" still exists after Extends.
- The open render tests: see `docs/prompt-log.md` → "Awaiting their first real run".

*Confidence: v6 model line, Max Mode, Variety, 8-min cap, 10 credits/2 songs, the download cap, Studio Premier-only, Pro stems, Voices, Personas and the editor steps are [official] (pages read 2026-10-01/02). Character caps and the long-song mechanisms are [community]. Everything about Job A/B performance is [v5.5-tested] or untested on v6. Earlier calibration notes (v5.5, 2026-07: belt-and-suspenders beat positive-only; dance-pop + `vocals dominate the mix` was the best gapless run; Replace Section failed for leading-hook swaps; roll 2–3 before judging; change ONE variable per render) remain in git history and in `docs/prompt-log.md`.*
