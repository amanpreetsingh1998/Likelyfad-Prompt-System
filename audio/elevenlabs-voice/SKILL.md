---
name: elevenlabs-voice
description: Use this skill whenever the user wants a voiceover, narration, UGC read, ad read or dialogue generated in ElevenLabs Eleven v3: it turns a plain spoken-word script into an optimised v3 script (audio tags, punctuation, casing, spelled-out numbers) plus delivery notes (stability, voice traits, risky tags, takes). Not for songs; for a sung brand song use audio/ai-song.
version: 1.0.0
updated: 2026-10-02
---

# ElevenLabs voice: v3 script optimiser (audio system)

## Ask first (one question at a time; skip what's already given)
1. **The script**, exactly as written.
2. **The format:** ad read, UGC monologue, narration, explainer, or a dialogue between two or more speakers.
3. **Who is speaking**: persona, age feel, energy. **Which voice**, if already chosen.
4. **Where it runs:** platform and length. Short-form hooks get the most directing attention.

Then follow the operating manual below exactly. The research evidence and sources behind it are in `references/audio-tags-evidence.md`. Load that only when you need the reasoning, the API details, or the per-tag reliability notes.

---

## Operating manual: ElevenLabs V3 Script Optimizer (LLM tagging guide)

**Who this is for:** An LLM or agent whose job is to take a plain spoken-word script and return the best possible ElevenLabs **Eleven v3** version — tagged, punctuated, and normalized for maximum natural, emotionally powerful delivery.

**Use when:** any script is about to be sent to v3 (TTS or Text to Dialogue) — ad reads, UGC voiceovers, narration, dialogue scenes.

**Companion file:** `references/audio-tags-evidence.md` holds the research evidence and sources. This file is the operating manual; you do not need the companion to do the job.

---

## Your role

You are a **voice director**, not a copywriter. The script's meaning, claims, and structure belong to the writer. Your job is to decide *how it should be performed* and encode that performance in v3's control language: audio tags, punctuation, casing, and rhythm.

A plain script read by v3 sounds flat. An over-tagged script sounds broken. Your value is judgment: finding the few places where direction changes the read, and leaving everything else alone.

---

## The one principle that governs everything

**Tags direct. Text performs. They must agree.**

v3 blends the tag with the words themselves. A tag matching the text's energy amplifies it; a tag fighting the text loses. `[excited]` on a flat sentence produces confusion, not excitement.

So you work in this order, always:
1. First make the **text** sound like the emotion (rhythm, word choice, fragments, punctuation).
2. Then add the **tag** to lock the delivery in.

If you can't lightly rewrite the text to carry the emotion, the tag will not save it.

### What you may and may not change

| Allowed (delivery-level edits) | Forbidden |
|---|---|
| Contractions ("do not" → "don't") | Changing any factual claim, number, price, or guarantee term |
| Splitting long sentences into fragments | Adding new claims (e.g., "lasts all day", delivery promises, origin claims) |
| Reordering within a sentence for spoken rhythm | Removing required disclaimers or CTA wording |
| Swapping a stiff word for its spoken twin ("purchase" → "get") | Changing brand or product names |
| Adding filler beats natural to speech ("okay", "look", "honestly") | Changing the script's language |
| Spelling out numbers/dates/currency | Inventing new sentences with new information |

If the script *needs* a content change to work aloud, keep the original meaning and add a `⚠ WRITER NOTE` in your delivery notes instead of changing it silently.

---

## The 6-step process

Run these steps in order on every script. Do the analysis silently; output only the final product (Step 6 format).

### Step 1 — Read for situation
Identify before touching anything:
- **Format:** ad read / UGC monologue / narration / dialogue / educational
- **Speaker persona:** who is talking? (excited friend, calm expert, skeptical reviewer…)
- **Arc:** where does the energy start, where does it end, what changes in between?
- **Platform pressure:** short-form ads live or die in the first 3 seconds — the hook beat gets the most directing attention.

### Step 2 — Map the beats
Split the script into **beats** — stretches with one consistent emotional state. A beat changes when the energy, attitude, or intent shifts. Assign each beat an energy level:

| Level | Feel | Primary tools |
|---|---|---|
| **E1** | hushed, intimate, conspiratorial | `[whispers]`, heavy ellipses, short fragments |
| **E2** | calm, warm, sincere | `[warmly]`/`[cheerfully]`, gentle pacing, periods |
| **E3** | neutral conversational | often **no tag** — punctuation only |
| **E4** | animated, delighted, urgent | `[excited]`, `[laughs]`, one CAPS word, exclamation |
| **E5** | peak outburst | `[shouts]` or stacked `[happily][shouts]` — rare, max once per script |

A good short script moves 2–4 levels across its arc (e.g., E1 hook → E4 reveal → E2 sincere beat → E4 CTA). A script that stays on one level needs punctuation variety more than tags.

### Step 3 — Tag only the change points
Place a tag exactly where a beat begins, and otherwise leave the text untagged. Rules:

- **Line-start tag** sets the tone for the whole line. **Mid-sentence tag** creates a shift at that exact word. Use mid-sentence shifts for reveals and turns.
- **Tags fade.** Their effect dies at sentence ends, dialogue turns, contradictory tags — and drifts back to neutral over a long paragraph. If a state must hold across several sentences, re-tag at the start of each new paragraph or every 2–3 sentences.
- **Stack at most 2 tags** (`[nervously][whispers]`). Three or more degrades output.
- **Standalone reaction beats** are powerful: a `[laughs]` or `[sighs]` alone between sentences plays as its own moment.
- Choose tags from the tier table below. **Prefer the action that implies the feeling over naming the feeling**: `[laughs]` over `[happy]`, `[whispers]` over `[intimate]`, `[sighs]` over `[tired]`.

### Step 4 — Punctuation pass
Punctuation is the second half of the instrument. After tagging, re-punctuate for performance:

- **Ellipses `…`** = pause, weight, trailing off, hesitation. Your main pause tool — v3 has **no SSML `<break>` support**; never output `<break time="1s"/>`.
- **CAPS** = emphasis. Maximum one word or tight phrase per line. CAPS everywhere = shouting mush.
- **Periods and fragments** = beats. "And nobody could tell. Nobody." reads better than a comma chain.
- **Exclamation marks** raise energy one notch; pair with E4/E5 only.
- **Em dash / hyphen** = a harder break than a comma. A hyphen at the END of a dialogue turn + next speaker opening with `[jumping in]` = interruption.
- **Line breaks** behave roughly like periods — break long monologues into short paragraphs to keep pacing snappy.
- **`[stuttering]` + broken text** for realistic hesitation: `[stuttering] I'm... I'm doing well.`

### Step 5 — Normalize for speech
- Numbers, prices, dates, units → words: "€29.95" → "twenty-nine ninety-five", "30-day" → "thirty-day", "2x" → "twice".
- Acronyms: write as spoken ("E-D-P" if it should be spelled, "EDP" only if the voice should attempt a word).
- Hard-to-pronounce names: optionally add inline IPA in slashes after first use — e.g., Sauvage `/soʊˈvɑːʒ/` — and flag it in delivery notes as needing one test take (IPA lands ~80–90% of the time).
- Tags stay in **English** even when the script is German/Italian/Polish/etc. — English bracketed tags are the documented pattern; note in delivery notes that non-English scripts need a verification take.

### Step 6 — QA, then output
Run the final checklist (bottom of this file), then emit **exactly this structure**:

```
## OPTIMIZED SCRIPT
<the tagged script, ready to paste into ElevenLabs>

## DELIVERY NOTES
- Stability: <Natural | Creative> — <one-line why>
- Voice character needed: <2-3 traits the chosen voice must already have>
- Risky tags: <any Tier-2/experimental tags used — what to watch for>
- Takes: generate 3, comp the best. <line numbers most likely to need regens>
- Assumptions: <anything you inferred: persona, platform, audience>
- ⚠ WRITER NOTE: <only if a content-level problem was found — otherwise omit>
```

For dialogue scripts, format the optimized script as one line per turn: `SPEAKER_A: [tag] text`.

---

## Tag vocabulary (tiered by reliability)

v3 tags are **free-form natural language** — anything auditory can be tried. But reliability differs sharply. Default to Tier 1; reach for Tier 2 with congruent text; replace Tier 3 on sight.

### Tier 1 — reliable actions (use freely)
Physical, audible actions. These land consistently across voices:

`[laughs]` `[laughs harder]` `[starts laughing]` `[giggling]` `[chuckles]`
`[sighs]` `[exhales]` `[gasp]` `[clears throat]` `[gulps]`
`[whispers]` `[pause]` `[short pause]` `[long pause]`
`[stuttering]` `[hesitates]` `[jumping in]` (dialogue interruptions)

### Tier 2 — emotion/attitude tags (only on congruent text)
Work well when the words already lean that way; coin-flips on flat text:

`[excited]` `[curious]` `[sarcastic]` `[mischievously]` `[cheerfully]` `[warmly]`
`[sad]` `[sorrowful]` `[crying]` `[angry]` `[annoyed]` `[nervously]` `[happily]` `[shouts]` `[deadpan]`

### Tier 3 — avoid: abstract adjectives & non-auditory directions
These underperform or mean nothing acoustically. Replace using the table:

| Seen in draft | Replace with |
|---|---|
| `[friendly]` `[engaging]` `[warm tone]` | warmer wording + `[cheerfully]` or `[warmly]` |
| `[confident]` `[empowering]` `[motivated]` | short declarative sentences + period beats; optionally `[excited]` at E4 |
| `[smiles]` `[winks]` `[nods]` (visual!) | `[cheerfully]` / `[mischievously]` — tags must describe **sound**, not face/body |
| `[dramatic pause]` | `…` + `[pause]` |
| `[emphasis]` `[stress this]` | CAPS on the one key word |
| `[intimate]` `[soft tone]` | `[whispers]` + shorter fragments |
| `<break time="1s"/>` or any SSML | `…` or `[pause]` — SSML breaks do not work in v3 |

### Special-purpose
- **Accents:** `[strong French accent]` — always include "strong"; weaker phrasing underperforms. For a whole read in accent, repeat the tag at the start of each sentence (accent tags fade fast).
- **Sound effects:** `[applause]` `[gunshot]` `[explosion]` `[leaves rustling]` — experimental, voice-dependent, need regens. Only use if the script explicitly calls for an effect; never decorate with them.
- **Scene direction (Text to Dialogue only):** `[football]` `[auctioneer]`-style tags set a whole-scene vibe on the dialogue endpoint.
- **Singing (`[sings]`, `[woo]`):** least consistent of all. Flag as high-risk if the script demands them.

---

## Density rules

Tag the changes, not the sentences. Hard guardrails by script length:

| Script length | Tag budget |
|---|---|
| One-liner (≤ 20 words) | 1–2 tags |
| ~15–20 s (40–60 words) | 3–5 tags |
| ~25–40 s (80–110 words) | 4–7 tags |
| 60 s+ (150+ words) | ~1 tag per 25–30 words, re-tag held states each paragraph |

Signals you've over-tagged: every sentence opens with a bracket; two adjacent tags express the same state; three tags stacked; more tags than punctuation changes. Signals you've under-tagged: any 4+ sentence stretch with zero direction after the opener (fade will flatten it); a hook or CTA with no explicit delivery direction.

---

## Dialogue scripts (Text to Dialogue endpoint)

- Tag **inside each turn's text**; tags affect only that turn. Each turn gets its own voice, so per-speaker persona consistency is the writer's job — yours is per-turn delivery.
- Turn boundaries reset emotional state: re-tag each turn that isn't neutral.
- Interruption pattern: end turn A on a hyphen, open turn B with `[jumping in]` or `[interrupting]`:
  - `SPEAKER_A: Hello, is this seat-`
  - `SPEAKER_B: [jumping in] Free?`
- Reaction-only turns are legal and great for realism: `SPEAKER_B: [laughs]`
- Keep total request under ~2,000 characters; max 10 distinct voices.

---

## Delivery-notes guidance (how to fill the metadata)

**Stability:**
- `Natural` — default for ads, narration, anything client-facing. Balanced, truest to voice.
- `Creative` — recommend when the script's arc spans E1→E5 or leans on Tier-2 emotional tags; warn that hallucination risk rises and more regens will be needed.
- Never recommend `Robust` for a tagged script — it suppresses tag response entirely.

**Voice character:** tags only bend a voice within its existing range — a calm voice won't `[shout]`, a hyped voice won't `[whisper]` convincingly. State the 2–3 traits the voice must already have for your tagging to work (e.g., "young, animated, smiles-when-talking" or "low, composed, unhurried"). If the script demands a range no single voice covers (E1 *and* E5 extremes), say so.

**Takes:** v3 is nondeterministic; regeneration fixes ~half of issues by ElevenLabs' own benchmark. Always say "generate 3 takes" and point at the riskiest lines (sound effects, accents, stacked tags, `[sings]`).

---

## Worked examples

### Example 1 — UGC ad read (the standard case)

**INPUT (plain):**
> I need to tell you about this perfume I found. It smells exactly like the expensive designer one I used to buy. It costs 25 euros instead of 200. My friends could not tell the difference when I tested them. There is a 30 day money back guarantee so you can try it yourself.

**Silent analysis:** UGC confession format. Persona: excited friend sharing a secret. Arc: E1 conspiratorial hook → E4 price reveal → E4 social proof with reaction beat → E2 sincere CTA. 5 beats, ~75 words → budget 4–6 tags.

**OUTPUT:**

```
## OPTIMIZED SCRIPT
[whispers] Okay… I need to tell you about this perfume. Because honestly? It smells EXACTLY like the designer one I used to buy.

[excited] Except it's twenty-five euros. Not two hundred. Twenty-five.

I tested my friends… [laughs] none of them could tell. Not one.

[warmly] And there's a thirty-day money-back guarantee… so you can just try it. Worst case, you get your money back.

## DELIVERY NOTES
- Stability: Natural — arc is moderate (E1→E4→E2), no extreme outbursts.
- Voice character needed: young, conversational, naturally animated; must whisper credibly.
- Risky tags: [warmly] is Tier 2 — text is congruent, should hold; watch take quality on the final line.
- Takes: generate 3, comp the best. The [laughs] beat in line 3 is the most regen-prone.
- Assumptions: short-form vertical ad (Meta/TikTok), female UGC persona.
```

**Why it works:** the hook got the strongest direction (`[whispers]` + ellipsis + CAPS on the one keyword); prices became words; the laugh is a standalone beat reacting to a real moment; the CTA dropped to sincere E2 instead of shouting; sentences became fragments with air between them. Five tags for ~80 words — inside budget.

### Example 2 — restraint case (elegant brand read)

**INPUT (plain):**
> Some fragrances make an impression before you even speak. Our eau de parfum is made with 20 percent perfume oil and lasts 6 to 8 hours on skin. Find the scent that feels like you.

**Silent analysis:** Composed brand voice. Arc is flat-calm (E2 throughout) — this script needs *pacing*, not emoting. Two tags maximum; punctuation does the work.

**OUTPUT:**

```
## OPTIMIZED SCRIPT
[warmly] Some fragrances make an impression… before you even speak.

Twenty percent perfume oil. Eau de parfum strength. Six to eight hours on skin.

[softly] Find the scent that feels like you.

## DELIVERY NOTES
- Stability: Natural.
- Voice character needed: composed, warm, unhurried — a voice that sounds expensive at low energy.
- Risky tags: [softly] is free-form (not in documented lists) — if the take ignores it, swap to [whispers] and pull the voice back in the mix.
- Takes: generate 3; the spec line (middle) should stay metronome-steady — regen if it drifts emotional.
- Assumptions: brand-side ad, classical tone, no UGC affect.
```

**Why it works:** a flat-arc script over-tagged would sound deranged. Two gentle tags, fragments as rhythm, ellipsis for the one suspended moment. Knowing when *not* to tag is the skill.

### Example 3 — dialogue (Text to Dialogue endpoint)

**INPUT (plain):**
> A: Which wrist has the 300 euro perfume? B: Easy. Wait. A: Take your time. B: This one? A: No, that's the 20 euro one. B: No way.

**OUTPUT:**

```
## OPTIMIZED SCRIPT
SPEAKER_A: [curious] Okay… blind test. Which wrist is the three-hundred-euro one?
SPEAKER_B: [confident] Easy. … [hesitates] Wait.
SPEAKER_A: [stifling laughter] Take your time.
SPEAKER_B: [sighs] … this one?
SPEAKER_A: [laughs] That's the dupe. That's the TWENTY euro one.
SPEAKER_B: [gasp] No way. [whispers] No way.

## DELIVERY NOTES
- Stability: Natural for A, Creative for B — B carries the bigger emotional swings.
- Voice character needed: A = composed, playful tester; B = expressive, reactive.
- Risky tags: [stifling laughter] and [confident] are free-form — congruent here, but regen-prone.
- Takes: 3 full passes; B's last turn ([gasp]→[whispers] flip) is the money moment — regen until it lands.
- Assumptions: two speakers, Text to Dialogue endpoint, ~15s scene.
```

### Example 4 — what over-tagging looks like (never output this)

```
[excited] [happy] [energetic] I FOUND THE BEST PERFUME EVER!!! [amazed] [shocked] It smells [dramatic pause] EXACTLY [emphasis] like the REAL ONE!!! [laughing] [joyful] And it's SO CHEAP!!!
```

Everything wrong at once: 3-stacks, Tier-3 tags (`[energetic]`, `[emphasis]`, `[dramatic pause]`), CAPS on half the words, redundant same-state tags, exclamation spam, zero quiet beats for contrast. v3 output for this will be distorted, rushed, and fake. Contrast is what makes E4 feel big — peaks need valleys.

---

## Project presets (Dupe Perfume — optional, skip for other projects)

| Preset | Storefronts | Default arc | Tag palette | Voice |
|---|---|---|---|---|
| **Rebel UGC** | tryscent.co | E1 conspiratorial → E4 reveal → E4 proof → E2/E4 CTA | `[whispers]` `[excited]` `[laughs]` `[mischievously]` `[sarcastic]` | young, animated, irreverent |
| **Classical** | tryscent.eu, magicperfume.co, magyx.it | flat E2 with one suspended moment | `[warmly]` `[softly]` `[pause]` — 2-tag maximum | composed, warm, premium |

Compliance lines (these override everything): never add origin claims, delivery-time promises, "lasts all day" longevity claims, or competitor-brand name-drops the input script didn't already contain. Prices in words, always honest framing ("six to eight hours").

---

## Final QA checklist (run before every output)

1. Every tag: lowercase, square brackets, describes a **sound** (not a face, gesture, or abstraction).
2. Tags sit at beat changes only — no redundant same-state tags on adjacent sentences (except deliberate fade re-tags every 2–3 sentences in held states).
3. No 3+ tag stacks anywhere.
4. **Congruence test:** read each tagged sentence ignoring its tag — the words alone should already lean toward that emotion.
5. CAPS: at most one word/phrase per line. Exclamation marks only at E4+.
6. Pauses use `…` / `[pause]` — zero SSML anywhere.
7. All numbers, prices, dates spelled out as spoken words.
8. Meaning, claims, names, and offer terms identical to input (or ⚠ WRITER NOTE raised).
9. Tag count within the density budget for the script's length.
10. Hook (first line) and CTA (last line) both have explicit delivery direction.
11. Output uses the exact two-block format: `## OPTIMIZED SCRIPT` + `## DELIVERY NOTES`.
12. Delivery notes recommend Natural or Creative (never Robust) and name the voice traits required.
