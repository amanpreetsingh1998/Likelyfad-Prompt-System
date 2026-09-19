# Trial formats — not yet run in production

> **Every format in this file is [trial].** They come from published guides, not from production prompts that rendered well. Write them on the full chassis (`../chassis.md`) — the guides' short templates are only a **shape**, not the length or detail to copy. Flag the output to the user as trial, and log the result so the format can be promoted to proven or dropped.

## Founder / premium talking head [trial]
**Use for:** a founder or expert speaking straight to camera, with a calmer and more premium feel than creator UGC.
- **Camera:** `Fixed stable camera at eye-level, medium close-up, 50mm lens feel, subject in upper 2/3, soft window light from one side, neutral background.` Commit to locked; don't add handheld shake.
- **Performance:** calm, knowledgeable, held eye contact; the product can be set down or slid toward camera between lines.
- **Audio:** `Ambient room tone`, and no music.
- **Open question:** does the production look block (`35mm handheld real-life shooting texture`) fight a locked premium frame? Test both with and without it.

## Street interview, several people [trial]
**Use for:** social-proof hooks where different people each give one line.
- One person per shot, **one line each**, about 3 seconds per shot. The first person can return at the end as a callback.
- Each person gets a one-sentence anchor: age range, visible features, clothing, one action (grabs the mic, leans in, stops chewing).
- All shots share one location type and light, and the camera identity is restated at the end.
- **The guides warn** that multi-person lip-sync in one generation is unreliable. If more than ~5 people, or any line is long, **generate each person as their own clip** and cut them together.

## Hands-only with voiceover [trial]
**Use for:** zero face risk and a premium product feel.
- `No face, hands only throughout.` Overhead or close framing; the hands open, lift, turn and use the product.
- Either one short voiceover line at the end, tagged `[Voiceover/Calm, English]`, or generate the clip silent and add the voice in post: `No on-screen dialogue in this clip. Ambient sound only. Leave audio space for a voiceover added in post.`
- Product fidelity: label reference, transcription, `show all details of the <product> faithfully`.

## Two-person dialogue [trial]
**Use for:** a conversation where both people speak.
- One reference image per person, each with an identity role line.
- They **take turns**, never overlap. Cut to the speaker each time (over-the-shoulder, favouring the speaker); reactions go between lines, not during them.
- About 0.5 seconds of pause between speakers.
- **Related production case [one series, 1 prompt]:** production did run a two-person scene where **only one person speaks** and the other is described as `silent throughout the entire clip, no dialogue at any point`. That rendered well. Real back-and-forth dialogue has not been tested.

## Hybrid: on-screen lines plus voiceover [trial]
**Use for:** long explanations. A speaker on screen for the hook and the sign-off, with hands or product B-roll plus a voiceover in the middle.
- Generate the on-screen clips on the chassis. Generate the middle clip silent with `Leave audio space for a voiceover added in post`. Record or generate the voiceover separately.
