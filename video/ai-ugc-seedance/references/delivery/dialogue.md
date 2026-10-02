# Delivery — dialogue, performance, and the audio block

How spoken lines are written into the beats, and how the voice is directed. Tags: **[proven]** production, 2+ ad series · **[one series]** production, a single ad series · **[guide]** published guides, uncontradicted · **[trial]** untested.

## Lines
- **Verbatim from the script, with exactly three exceptions,** each shown to the user when used: (1) numbers written as words; (2) a hard brand or product name respelled phonetically; (3) `...` added where a line continues across clips. Nothing else changes. Never reword. Most production lines were short, but lines of 11–14 words also rendered well [proven]. The guides' 5–10-word rule is a **fix** for mushy sync, not a limit.
- **Numbers spelled out**, the way they're said: `twenty dollars`, `two for one`. Where a homophone is possible, say so: `spoken as the word "four", NOT as a numeral, NOT as "for"` [one series].
- **Hard names are spelled phonetically**, and the spaces are explained as articulation cues [one series]:
  > The brand name is written as "<Pho net ic>" — the spaces are articulation cues for the audio engine, NOT audible pauses. Spoken as one continuous flowing <N>-syllable word "<phonetic>" with no gap between the chunks.
- **A line can span a beat or break across beats.** Trailing `...` marks a line that continues mid-thought.
- **Commas that must be heard:** `the comma is rendered as a tiny natural break in speech, NOT a long pause, just enough separation that "<word>" and "<word>" land as two distinct words` [one series].
- **Non-verbal reactions** get their own tag: `[Reaction sound, non-verbal]: soft approving "Mmm" through closed lips` [one series].
- **Tagged format**, if you use one, is `[Dialogue/Casual, English]: "…"`, with the delivery in the label and never in parentheses after the quote [guide]. Production also wrote `He says: "…"` inline [proven]. Both work; pick one per project.

## Word-pinned performance [proven]
The production prompts tie every gesture and expression to the exact word it lands on:
```
She says: "<line>." On "<word>," her right hand makes a small natural emphasis flick at chest height, eyebrows lift a fraction. On "<word>," small chin-down emphasis nod, closed-cadence finality. Eyes hold camera contact through the final 0.4 seconds.
```
- **Channels:** hands (with side and height: "at chest height"), eyebrows, mouth corners, chin, eyes (to camera, a brief drift away and back), lean, shrug, exhale.
- **Scale words keep it real:** `small`, `a fraction`, `tiny`, `natural`, and the `NOT theatrical, NOT a hero move` guard.
- **Head motion on words is allowed.** Nods, tilts and head shakes on spoken words rendered well [proven]. If a specific line's sync goes mushy, move that line's head motion to just before or after it [guide fix].
- **Slow is allowed.** Deadpan or deliberate beats can run near 1 word/second; production's locked reaction clips did. Write the gaps as **held silences with durations**, so the model doesn't fill them.
- **Resting baseline:** say where the hands return between gestures ("settles back to the lap baseline").
- **Eyes:** default locked on camera. A drift away and back reads as thinking or remembering. Hold eye contact on the verdict.

## The audio block [proven]
Write it after the beats, in this order:
1. **Voice spec:** the timbre-only clause when `@audio1` is used, then age, gender, accent, pace. For example, `Late-20s American woman, natural everyday American accent, fast confident TikTok-creator pace`.
2. **Mic and room:** `Clear and close-mic sounding as if recorded on iPhone front camera at <arm's length / tripod distance>. Slight room reverb from the <room>, NOT dry studio sound.`
3. **Register** in one line, then **per line:** emphasis (`Slight emphasis on…` / `Heavy emphasis on…`), pitch (`voice goes up slightly on…`), and **cadence** on the last word.
4. **Held silences with durations** [one series]: `Held silence of 0.3 seconds after "<word>."`. Put an action inside a silence when it needs time, such as `this held silence is when she reaches off-frame and lifts the bottle into view`.
5. **Cut sound:** `The internal hard cuts are silent — NO transition sound, NO clicks, NO whoosh, dialogue continues seamlessly across the cuts.`
6. **Action sounds or their absence:** a sound that should exist (`soft natural slicing sound … subordinate to the voice`), or one that must not (`The bottle toss is silent — NO impact thud, NO whoosh`).

### Cadence: open or closed [proven]
- **Open (mid-thought):** `open-ended trailing cadence on "<word>" — voice sustains a slight upward or held pitch, does NOT drop. The audio should sound like a comma, NOT a period. Soft inhale audible at the very end as if she is about to keep speaking.`
- **Closed:** `Closed-cadence finality on "<word>" — voice settles down, sentence terminates naturally. The audio should sound like a period, NOT a comma. Soft natural exhale audible after "<word>".`
- **A hard close** adds: `NOT a soft conversational fade — the period is hard.`

## Register lock — when the words would pull the delivery [one series]
The model reads tone from the words. When a line would naturally sound different from the brief (a product spec read as a sales pitch, a prescription read as calm advice), add both blocks:
```
LOCKED REGISTER — <register> delivery throughout the ENTIRE clip from the first word to the last word. <What the register is and who it's aimed at.> NOT softer, NOT more conversational, NOT casual, NOT <the specific wrong readings>. The <register> IS the default state and does NOT shift.

CRITICAL: the script for this clip ("<all lines>") would naturally read as <the wrong reading>. OVERRIDE that reading completely. The register is locked <register>. The script's words are the content, the <register> is the delivery, do NOT let the words drift the register toward their natural reading.
```
- **Name who the energy lands on:** `The <frustration> lands on <the target>, NOT on the viewer.`
- **Across a series,** name the clips the register carries over from: `the same register from the <earlier> clip carried directly forward, no register reset`.
