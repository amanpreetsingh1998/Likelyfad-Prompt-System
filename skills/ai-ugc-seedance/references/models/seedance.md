# Model layer — ByteDance Seedance 2.0 (realistic UGC)

> The **swappable** file. Everything Seedance-specific for *realistic* UGC lives here. When the model changes, replace this file.
>
> **Not the same file as `ai-animation/references/models/seedance.md`.** Same model, different craft. The animation file says *affirmative phrasing only — negated words backfire*; that holds for stylized 3D. The owner's **realistic** production prompts use NOT-lists heavily and rendered well. Neither rule is universal — never port one into the other.

Tags: **[proven]** production, 2+ ad series · **[one series]** production, a single ad series · **[guide]** published guides, uncontradicted · **[trial]** untested.

## Hard specs [guide]
- **Duration:** 4–15s. Production clips ran **5–12s**; 15s is the ceiling, not the target.
- **Inputs:** up to **9 images + 3 videos + 3 audio** (videos ≤15s combined, audio ≤15s combined), **12 assets max**.
- **Resolution:** native **480p / 720p**; higher tiers are platform upscales. 24fps native.
- **Aspect:** 9:16 for this skill (say "vertical 9:16" in the camera line).
- **Native audio and lip-sync**, multi-language — always name the language or accent.
- **Default platform assumption: Higgsfield.** Its editor pastes assets as `<<<image_1>>>` / `<<<avatar:…>>>` — those are copy artefacts. Always write `@image1`, `@image2`, `@audio1`, `@video1`.

## Reference roles — the phrasing is the instruction
Seedance does not infer an asset's job; the sentence you write is the role.

| Role | Phrasing | Source |
|---|---|---|
| First frame (the clip starts from this exact composition) | `@image1 as the first frame.` | [proven] |
| Identity only (face/look; scene may differ) | `@image2 as character face and identity reference across all angles.` | [proven] |
| Location + framing + lighting | `@image1 as composition, location, lighting, and framing reference — match this exact <setting>, <camera angle>, <lighting>, <key objects>.` | [proven] |
| Held position for one sub-shot | `@image3 as the <held-in-hand / pointing> pose reference for sub-shot two — <describe the pose>.` | [one series] |
| Product label fidelity | `@image4 as the product label fidelity reference — <label transcribed>. The label and all text stays stable and readable throughout, NOT warping, NOT distorting, NOT morphing across the cuts.` | [proven] |
| Voice timbre only | `voice timbre references @audio1 — extract voice character only (tone, pitch, accent, room acoustic), do NOT copy or reproduce any dialogue or words from @audio1. The character speaks ONLY the dialogue written in this prompt, in the voice style of @audio1.` | [proven] |
| Extend a previous clip | `@video1 as the video to extend from — continue from the exact last frame.` | [one series] |
| Camera movement copy | `completely reference all camera movement effects from @video1` | [guide] |

- **First frame vs identity are different jobs** — "@image1 as the first frame" is not "the woman from @image1". Use both when you have both. [guide]
- **One owner per attribute.** Two assets claiming the same attribute blend. [guide]
- **Identifiable real people are filtered** on most platforms; use generic realistic personas. [guide]

## Negation policy for realistic UGC [proven]
The production prompts combine affirmative description with **NOT-lists**, and they rendered well. Use negatives for four jobs:
1. **Strip model defaults** — the closer: `No music, no logo, no text on screen, no subtitles.`
2. **Hold the phone look** — `NOT tripod, NOT selfie, NOT cinematic, NOT polished, NOT color graded` and `no 3D, no cartoon, no VFX`.
3. **Stop prop and framing drift** — `NOT a hero shot`, `NEVER swaps hands`, `NO zoom, NO scale change`.
4. **Stop register drift** — `NOT softer, NOT casual, NOT a soft outro`.

Always say what you **do** want as well. **If a render shows the very thing a NOT-line names**, rewrite that one line affirmatively (the animation-side lesson) and re-roll — see the table.

## Voice sample (`@audio1`) [guide unless noted]
- **MP3 only** — WAV/AAC/FLAC can upload and silently fail.
- **3–8 seconds** is the sweet spot; quality drops past ~10s. Clean, close-mic, no reverb or background noise, recorded a little slower than natural speech, **same language** as the dialogue.
- Always use the **timbre-only clause** [proven]. Then still describe the voice in the audio block — age, gender, accent, pace [proven].

## Lip-sync realities [guide]
- Front-facing or slight three-quarter; profile shots break sync.
- The face should fill enough of the frame — mouths go vague in wide shots.
- The first-frame / identity portrait matters: sharp, even light, mouth relaxed.
- Production prompts **did** put nods, tilts and head shakes on spoken words and kept a slow push-in over a line, and rendered well [proven]. The guides forbid it. If sync goes mushy, see the table.

## Text and labels
- **Transcribe the label word for word**, top to bottom, in the subject block and again in maintain, [proven], plus `NO text hallucination, NO alternate spelling, NO additional text` [one series].
- Give the label its own reference image and keep the label **facing camera** [proven].
- Add `show all details of the <product> faithfully` [guide, used in production].
- Printed shirts: `graphic facing forward, NOT mirrored, NOT reversed, NOT flipped` [one series].
- Perfect generated typography is still not guaranteed. If a label must be pixel-exact, plan a post replacement [guide].

## Symptom → fix table
| Symptom | Fix | Source |
|---|---|---|
| Person looks frozen or mannequin-like | Add the alive block from frame zero, with a stated blink minimum | [proven] |
| Product jumps hands or sides of frame | Pin hand + side (viewer perspective), `NEVER swaps`, restate in maintain | [proven] |
| Label garbles or changes | Label reference image + full transcription + slower hand movement; post replacement if critical | [proven] / [guide] |
| Shirt graphic or text mirrored | `NOT mirrored, NOT reversed, NOT flipped` | [one series] |
| Delivery drifts to the script's natural tone | LOCKED REGISTER block + CRITICAL override line | [one series] |
| Brand or product name mispronounced | Phonetic spelling with the articulation-cue note | [one series] |
| "four" heard as "for", numbers garbled | Spell numbers out [proven]; add `NOT as a numeral, NOT as "for"` [one series] | mixed |
| Cut adds a whoosh or click | `The internal hard cuts are silent — NO transition sound` | [proven] |
| A thrown or set-down object makes noise | State its silence explicitly | [one series] |
| Duplicate objects appear | Count line: `Only ONE <object> exists in the scene.` | [one series] |
| Clip ends too final (or too open) for the stitch | Specify cadence: comma vs period, soft inhale vs settled exhale | [proven] |
| Lip-sync goes mushy | Shorten that line (5–10 words) or split the clip; remove head motion **during that line only**; lock the camera for it; front-facing | [guide] |
| Audio goes mushy past ~8s | Split into two clips and stitch | [guide] |
| Accent drifts or sounds off-language | Name the language and accent; voice sample in the same language | [guide] |
| Model adds music or captions | The closer, every clip | [guide] / [proven] |
| Dialogue cut off at the end | Move it earlier, shorten it, or extend the duration | [guide] |
| Looks commercial, not phone-shot | Camera identity NOT-list + 2 micro-details; remove "cinematic/professional" | [guide] / [proven] |
| Face drifts across cuts | `same person across frames` + identity reference + fewer cuts | [guide] |
| The negated thing appears ("NOT a crowded room" → a crowded room) | Rewrite that line affirmatively and re-roll | [trial] |
| Audio distorts or has artefacts | Re-roll; if it persists, generate silent and add voiceover in post | [guide] |
