# ElevenLabs V3 Audio Tags — Speech Prompting Guide

*Compiled 2026-06-10 from a verified deep-research pass (99 agents, 25 claims confirmed 3-0 in adversarial verification, 0 refuted) plus a hand-checked practitioner sweep. Every claim is labeled by evidence tier:*

- **[OFFICIAL]** — verified verbatim against live ElevenLabs docs/blog/SDK on 2026-06-10. Trust these.
- **[COMMUNITY]** — practitioner-reported, plausible, but did *not* survive independent verification. Treat as hypotheses to test.
- **[SYNTHESIS]** — our own application to the perfume-ad use case. Untested until we run takes.

---

## TL;DR — the 10 rules

1. **Voice choice does 80% of the work.** Tags only bend a voice within its natural range — a calm voice won't `[shout]` convincingly. Pick the voice for the energy you need *before* writing tags. [OFFICIAL]
2. **Tags are lowercase, in square brackets, placed inline at the exact point delivery should change.** `[whispers] Something's coming… [sighs] I can feel it.` [OFFICIAL]
3. **Stability setting: Natural by default, Creative when you need big emotion, never Robust for tagged scripts** (Robust largely ignores tags). [OFFICIAL]
4. **Punctuation is half the instrument.** Ellipses `…` = pause/weight/trailing off. CAPS = emphasis. Normal punctuation = natural rhythm. Official example: `It was a VERY long day [sigh] … nobody listens anymore.` [OFFICIAL]
5. **No SSML `<break time>` tags in v3.** Pauses come from ellipses, punctuation, and tags like `[pause]`/`[sighs]`. [OFFICIAL]
6. **Tags combine and stack:** `[happily][shouts] We did it! [laughs]` — direct emotion moment-to-moment, not one global mood. [OFFICIAL]
7. **Action tags beat emotion tags for reliability.** `[whispering]`, `[laughs]`, `[sighs]`, `[pause]` land consistently; abstract feelings like `[friendly]`, `[motivated]`, `[engaged]` are coin-flips. [COMMUNITY]
8. **Tag effects fade.** They wear off at sentence ends, dialogue turns, contradictory tags — and drift back to neutral across paragraphs. Re-tag each new beat. [COMMUNITY]
9. **Write the text to already sound like the emotion.** Tags amplify congruent text; they fight incongruent text. Don't tag `[excited]` onto a flat sentence. [COMMUNITY, consistent with official "context-dependent" caveat]
10. **Regeneration is a production step, not a failure.** ElevenLabs' own benchmark: regenerating fixes ~half of quality issues. Budget 2–4 takes per line and pick. [OFFICIAL]

---

## 1. Mental model — how v3 "thinks"

V3 is not a tag-execution engine; it's a performance model steered by four inputs at once:

```
VOICE (its training range)  →  what's possible
STABILITY (Creative/Natural/Robust)  →  how far it will stray to obey you
TEXT (wording + punctuation + casing)  →  the baseline read
TAGS  →  moment-to-moment direction on top
```

All four must agree. A mismatch anywhere (serious corporate voice + `[giggles]`, Robust mode + heavy tags, flat text + `[excited]`) produces the "tags do nothing" complaints you see in forums. [OFFICIAL + COMMUNITY]

Official framing worth keeping in mind: v3 launched in alpha (June 2025, now GA) with the explicit warning that it **"requires more prompt engineering than our previous models."** This is a craft, not a checkbox. [OFFICIAL]

---

## 2. The tag inventory

There is **no fixed enum**. Official docs: tags are "natural-language instructions, not an enum parameter" — anything auditory and voice-plausible can work. The lists below are the officially documented examples, merged from three official taxonomies (best-practices docs, audio-tags blog, Text to Dialogue docs). [OFFICIAL]

### Officially documented tags

| Category | Tags |
|---|---|
| **Laughter family** | `[laughs]` `[laughs harder]` `[starts laughing]` `[wheezing]` `[giggling]` |
| **Breath & reactions** | `[sighs]` `[exhales]` `[clears throat]` `[gulps]` `[swallows]` `[snorts]` `[crying]` `[gasp]` |
| **Delivery direction** | `[whispers]` `[shouts]` `[stuttering]` `[cheerfully]` `[jumping in]` (interruption) |
| **Emotion / attitude** | `[sad]` `[angry]` `[happily]` `[sorrowful]` `[excited]` `[curious]` `[sarcastic]` `[mischievously]` |
| **Accents** | `[strong X accent]` — e.g. `[strong French accent]`; "strong" wording works better |
| **Sound effects** (experimental) | `[gunshot]` `[applause]` `[clapping]` `[explosion]` `[leaves rustling]` `[gentle footsteps]` |
| **Scene/overall direction** (dialogue endpoint) | `[football]` `[wrestling match]` `[auctioneer]` — sets a whole-scene vibe |
| **Unique/special** (least consistent) | `[sings]` `[woo]` |

Official caveat attached to the experimental rows: "Some experimental tags may be less consistent across different voices." [OFFICIAL]

### Community-tested reliability tiers [COMMUNITY — test before trusting]

- **Consistently land:** `[whispering]` `[laughs]` `[sighs]` `[giggles]` `[pause]` `[strong British accent]` (and other strong-accent variants), `[applause]`, `[gulps]`
- **Hit or miss:** `[sad]` `[sarcastic]` `[curious]` `[exhales]` — "sometimes very good, other times not"
- **Mostly disappoint:** abstract adjectives — `[friendly]` `[engaged]` `[empowering]` `[motivated]`
- **Why:** clear physical *actions* give the model an objective target; abstract *feelings* leave it interpreting. Prefer the action that implies the feeling (`[laughs]` over `[happy]`, `[whispers]` over `[intimate]`).
- Useful timing tags seen in the wild beyond official lists: `[short pause]` `[long pause]` `[rushed]` `[hesitates]` `[stammers]`.

### Tag behavior rules

- **Placement:** anywhere in the script; tag at line start sets the tone for the whole line, mid-sentence tags create a dynamic shift at that word. [OFFICIAL + COMMUNITY]
- **Duration:** a tag's effect lasts until a contradictory tag, end of sentence, or end of dialogue turn — and fades gradually over long paragraphs. Standalone reaction tags (`[laughs]`) play as a discrete beat; state tags (`[sarcastic]`) color the following words. [COMMUNITY]
- **Stacking:** back-to-back tags compound: `[nervously][whispers]`, `[happily][shouts]`. Some combos interact unpredictably — if a combo underperforms, swap a synonym or reorder. [OFFICIAL syntax / COMMUNITY caveat]
- **No documented cap** on tags per line or script — but density without congruent text degrades output. Practitioner heuristic: tag the *changes*, not every sentence; surround tags with context-rich text. [OFFICIAL absence + COMMUNITY]
- **For consistent style across a long read** (e.g., holding an accent), repeat the tag at the start of each sentence. [COMMUNITY — superscale's ad testing]

---

## 3. Settings & voice selection

### Stability (the master dial) [OFFICIAL]

| Mode | Behavior | Use for |
|---|---|---|
| **Creative** | Most emotional and expressive — "prone to hallucinations" | Big-energy UGC reads, character moments. Expect more bad takes; regen more. |
| **Natural** | Balanced, closest to the original voice recording | **Default.** Most ad VO. |
| **Robust** | Highly stable, "less responsive to directional prompts," ~v2 behavior | Long flat narration only. **Kills tags — don't use for tagged scripts.** |

Official recommendation verbatim: "For maximum expressiveness with audio tags, use Creative or Natural settings."

### Voice selection [OFFICIAL]

- Official docs call voice **"the most important parameter for Eleven v3."** Tag effectiveness depends on the voice's training samples — the same tag works on one voice and fails on another.
- Match voice character to script energy: "a meditative voice shouldn't shout and a hyped voice won't whisper convincingly."
- **Use IVCs (instant clones) or designed/library voices.** PVCs (professional clones) are explicitly *not fully optimized for v3* yet.
- For clones: record source audio with a broad emotional range if you want the clone to take emotional direction.
- Library hint: voices tagged "best for V3" in the voice library respond better to tags; neutral voices are most stable across languages/styles. [OFFICIAL + COMMUNITY]

### Pronunciation & normalization (matters for perfume names and prices)

- V3 supports inline IPA slash notation for tricky words, ~80–90% consistency. Useful for *Sauvage*, *Baccarat*, *Eau de Parfum*. [OFFICIAL]
- Spell out numbers, currencies, dates in the script: "twenty-nine ninety-five," not "€29.95." Models stumble on raw digits. [OFFICIAL]

---

## 4. Punctuation & text structure (the second instrument)

All official: [OFFICIAL]

- **Ellipses (`…`)** — add pauses and weight; signal trailing off.
- **CAPITALIZATION** — increases emphasis on those words.
- **Standard punctuation** — natural speech rhythm. Line breaks act roughly like periods.
- **Hyphen at turn end + `[jumping in]`** — interruptions between dialogue turns:
  - Speaker 1: `Hello, is this seat-`
  - Speaker 2: `[jumping in] Free?`
- Official showcase lines (steal these patterns):
  - `It was a VERY long day [sigh] … nobody listens anymore.`
  - `[whispers] Something's coming… [sighs] I can feel it.`
  - `[stuttering] I'm... I'm doing well, thank you.`
  - `[happily][shouts] We did it! [laughs]`

Community additions [COMMUNITY]: em dashes mark stronger breaks than commas; periods = full stop beats; "three dots create pauses… CAPS make things LOUDER." Stage emotional transitions gradually (laugh → wonder → sadness) rather than hard-cutting between extremes.

---

## 5. Reliability & the regeneration workflow [OFFICIAL]

- Output is **nondeterministic** — same input, different takes. The dialogue endpoint accepts a `seed` for repeatability.
- ElevenLabs' internal benchmark: **regenerating solves roughly half of quality issues**; most of the rest trace to the voice's training data (i.e., switch voices, don't keep re-rolling).
- Production workflow implied: generate ≥2–3 takes per script, comp the best lines. In the dashboard, up to 2 regenerations of identical content are free.
- Text to Dialogue is "still under active development, actual results may vary" — expect drift in behavior over time.

**Practical regen ladder when a line won't land** [COMMUNITY + SYNTHESIS]:
1. Regenerate once or twice (fixes ~50%).
2. Swap the tag for a synonym (`[laughs]` → `[chuckles]`, `[sad]` → `[sighs]` + sadder wording) or reorder stacked tags.
3. Rewrite the *text* to match the emotion harder (congruence beats tag strength).
4. Change stability mode (Creative ↔ Natural).
5. Change the voice. If a voice ignores a tag class repeatedly, it always will.

---

## 6. API usage (for pipeline automation)

**Model ID: `eleven_v3`** on the Create Speech / Stream Speech endpoints. [OFFICIAL — help center + SDK README]

```python
from elevenlabs.client import ElevenLabs

client = ElevenLabs(api_key="...")

audio = client.text_to_speech.convert(
    text="[excited] Okay wait… [whispers] this is the one. [laughs]",
    voice_id="JBFqnCBsd6RMkjVDRZzb",
    model_id="eleven_v3",
    output_format="mp3_44100_128",
)
```

**Multi-speaker: Text to Dialogue endpoint** (`POST /v1/text-to-dialogue`, v3-only, default model `eleven_v3`). Tags go *inside each speaker's `text` value* and steer only that turn. Max 10 unique voices per request; ~2,000-character cap across inputs per request; `seed` param for consistency. [OFFICIAL]

```python
from elevenlabs import DialogueInput

audio = client.text_to_dialogue.convert(
    inputs=[
        DialogueInput(text="[cheerfully] Hello, how are you?", voice_id="VOICE_A"),
        DialogueInput(text="[stuttering] I'm... I'm doing well, thank you.", voice_id="VOICE_B"),
    ]
)
```

GitHub references (all official ElevenLabs org):
- `github.com/elevenlabs/elevenlabs-python` — SDK; `text_to_dialogue/` module with `convert()`, `convert_with_timestamps`, async variants; README v3 examples.
- `github.com/elevenlabs/elevenlabs-js` — JS equivalent.
- `github.com/elevenlabs/elevenlabs-examples` — quickstarts per capability.
- Cookbook: `elevenlabs.io/docs/eleven-api/guides/cookbooks/text-to-dialogue`.

⚠️ URL rot note: the old guide at `/docs/best-practices/prompting/eleven-v3` and short `/docs/cookbooks/text-to-dialogue` paths now 404. Live pages: `/docs/overview/capabilities/text-to-speech/best-practices` and `/docs/eleven-api/guides/cookbooks/text-to-dialogue`.

---

## 7. The script-writing playbook

**Step 0 — Decide the read's emotional arc first** (e.g., conspiratorial hook → building excitement → grounded honest beat → confident CTA). Tags execute an arc; they can't invent one.

**Step 1 — Pick the voice for the arc's center of gravity.** High-energy UGC read → already-animated voice. Elegant brand read → composed warm voice. Check it's v3-friendly (library tag or IVC with range).

**Step 2 — Stability:** Natural. Go Creative only if Natural takes feel too safe.

**Step 3 — Write the text as a performance, not copy.** Fragments, contractions, real speech rhythm. The sentence itself should carry the emotion you'll tag.

**Step 4 — Tag only the change points.** Opening tone tag, then a tag wherever the energy shifts. One or two tags per beat; action tags over abstract emotions.

**Step 5 — Punctuation pass.** Ellipses where you want air. CAPS on the one word per line that matters. Period = beat.

**Step 6 — Generate 3 takes, comp the best.** Log which tags the chosen voice obeys/ignores — build a per-voice tag cheat sheet over time (nobody has published one; we have to earn ours).

### Density guardrail [SYNTHESIS from official + community]
For a 25–40s ad read (~80–110 words): **4–7 tags total** — opening tone, 2–4 shift points, maybe one reaction beat (`[laughs]`/`[sighs]`), one CTA-tone tag. If every sentence has a tag, you're steering the model into mush; if none do after the opener, the read flattens (tags fade).

---

## 8. Applied: perfume-ad patterns [SYNTHESIS — untested, for our first test batch]

*(Respect landmines: no origin claims, no delivery promises, honest longevity framing.)*

### A. UGC confession hook (TryScent.co rebel voice — female, mid-20s energy, Natural stability)

```
[whispers] Okay I'm not supposed to say this out loud…
[normal] but that two hundred euro perfume everyone keeps posting?
[sighs] I stopped wearing mine.
[mischievously] Because I found the same vibe… for like a tenth of the price.
[excited] And nobody at work could tell. NOBODY.
[laughs] My manager asked where I bought it.
[confident] Smell test it yourself — link's right there.
```

### B. Elegant brand read (Magic Perfume classical voice — composed, warm, Natural stability)

```
[warmly] Some scents introduce you… before you say a word.
[soft] Twenty percent perfume oil. Eau de parfum strength.
[pause] Six to eight hours on skin — we won't pretend it's forever. [gentle laugh] Nobody's is.
[confident] Crafted to feel familiar… priced to feel honest.
[warmly] Find the one that feels like you.
```

### C. Scent Swap dialogue (Text to Dialogue endpoint, two voices)

```
VOICE_A: [curious] Okay… blind test. Which wrist is the three hundred euro one?
VOICE_B: [confident] Easy. [sniffs] … [hesitates] Wait.
VOICE_A: [stifling laughter] Take your time.
VOICE_B: [sighs] … this one?
VOICE_A: [laughs] That's the dupe. That's the TWENTY euro one.
VOICE_B: [appalled] No way. [whispers] Don't tell my wife what she's been paying for.
```

### D. CTA delivery patterns to test
- Soft-close: `[warmly] You've got thirty days to fall in love with it… [pause] or it's on us.`
- Punch-close: `[excited] Smell Test Guarantee. THIRTY days. [confident] Go.`
- Conspiratorial: `[whispers] The link's in the corner. [mischievously] You didn't hear it from me.`

---

## 9. Open questions → our test plan

The research's biggest finding is a *negative* one: **no community tag-reliability matrix, no tag-density rule, and no ad/UGC case study survived verification.** Everything in section 8 needs empirical validation:

1. **Per-voice tag matrix** — for each shortlisted ad voice, run the ~15 core tags 3× each; log obey/ignore/garble. (Cheapest possible insurance before batch production.)
2. **Density A/B** — same script at 3 tags vs 7 tags vs 12 tags; find the mush point.
3. **Creative vs Natural hallucination rate** at our script lengths — is Creative's expressiveness worth the regen cost at 20 ads/month volume?
4. **UI trichotomy ↔ API numeric mapping** — how Creative/Natural/Robust maps to API `stability`/`similarity` values is undocumented; test if we automate via API.
5. **Short-prompt instability** — community claims very short generations are inconsistent; pad hooks with context lines and trim audio after? Test.

---

## Sources

**Official (verified live 2026-06-10):**
- elevenlabs.io/docs/overview/capabilities/text-to-speech/best-practices — canonical "Prompting Eleven v3"
- elevenlabs.io/docs/overview/capabilities/text-to-dialogue + /docs/eleven-api/guides/cookbooks/text-to-dialogue
- elevenlabs.io/blog/eleven-v3 (launch), /blog/v3-audiotags, /blog/eleven-v3-audio-tags-expressing-emotional-context-in-speech
- help.elevenlabs.io article 35869142561297 ("How do audio tags work with Eleven v3")
- github.com/elevenlabs/elevenlabs-python (SDK + text_to_dialogue module)

**Community/practitioner (unverified tier):**
- oguzhankocakli.medium.com — "My experience with ElevenLabs v3: what actually works"
- moelueker.com — v3 tutorial (settings, tags, scriptwriter GPT)
- medium.com/@v-jur-kh — "On text markup for the ElevenLabs v3 TTS" (tag duration/fading experiments)
- jonathanmast.com — v3 audio tags user guide (combos, mistakes)
- superscale.ai/learn/sound-effects-emotions — ad-VO tag reliability testing (actions > emotions)
