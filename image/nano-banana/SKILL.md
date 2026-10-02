---
name: nano-banana
description: Use this skill whenever the user wants an IMAGE made or edited with Google Nano Banana Pro (Gemini 3 Pro Image): product hero shots, lifestyle or UGC-style stills, social thumbnails, text-heavy posters and ads, comparison or before/after images, multi-language variants, grounded infographics, keyframes or first frames for a video, single character sheets, or edits to an existing image. For a script-wide cast of characters, Pixar or realistic character reference sheets, or before/after transformation sheets, use image/character-casting instead.
version: 1.0.0
updated: 2026-10-02
---

# Nano Banana: image prompts (image system)

You write ready-to-paste **Nano Banana Pro** prompts: new images, and conversational edits of existing ones. Keep context lean: load only the file for the step you are on.

## Step 0: is this the right skill?
- **A cast of characters from a script, a Pixar-style or realistic character reference sheet, or a before/after transformation series** → stop and open `image/character-casting/SKILL.md`.
- Everything else visual (product, lifestyle, UGC frame, poster, thumbnail, comparison, before/after scene, translation, infographic, keyframe, a single character sheet, editing an image) → continue here.

## Ask first (one question at a time; skip any the user already answered)
1. **What are we making?** Product hero · lifestyle / product in a scene · UGC-style frame · viral thumbnail / social hook · text-heavy poster or ad · comparison ad · before / after pair · language variants of an existing ad · data infographic · first frame or keyframe for a video · a character sheet · edit an existing image · sketch → final render · cartoon pattern-interrupt.
2. **Which reference images do you have**, and what is each one for (identity, product, style, scene, pose, outfit)?
3. **Where will it run?** This sets the aspect ratio (1:1, 4:5, 9:16, 16:9, 21:9) and the resolution (2K default; 4K for text-heavy or print).
4. **Any exact text in the image?** Get the exact words, the font feel, the colour and the position.
5. **For whom?** The brand, the audience and the purpose: one line of context steers the model strongly.

## Workflow
1. **Pick the structure**: hybrid labeled-prose by default; short prose to explore; JSON only for batches or multi-subject colour separation. → `references/prompt-structure.md` (Part 2 + the decision tree).
2. **Start from the matching template** → `examples/templates.md` (Part 11 scenarios, Part 15 canonical templates). Fill the fields; don't rewrite the structure.
3. **Add physics** where realism matters: camera, lens, light, materials, composition → `references/physics.md`.
4. **If there is text** → `references/text.md`.
5. **If there is a person who must stay the same, or several reference images** → `references/identity-and-references.md`.
6. **If editing an existing image** → `references/editing-and-negatives.md`.
7. **Model facts, grounding, output control, failure modes** → `references/models/nano-banana-pro.md`. **(The swappable layer: if the model changes, only this file changes.)**
8. **If the still feeds a video** → `references/handoff-to-video.md`. It maps to our `video/` skills.
9. **Run the pre-flight checklist** (Part 16, in `references/prompt-structure.md`) before you deliver.

## Must-never
- No quality spam ("8K, masterpiece, trending on artstation, hyperdetailed").
- No long generic negative block. Describe what you want; keep any negative to one narrow line (Part 8).
- No `mode: GENERATE` / `mode: EDIT` lines in conversational prompts.
- No style shortcuts in place of physics ("iPhone photo" → "shot on iPhone with direct flash, deep DoF, small sensor look").
- Always state the aspect ratio. Always put rendered text in quotes, with font, colour and position.
- For identity edits, name what to preserve and what to change. **Exception:** before/after transformation stages, where a blanket lock suppresses the change (see `image/character-casting/`).
- Never mix models across one character's images.

## Output format (every time)
1. **Generation model: Nano Banana Pro**, shown in bold above the block.
2. One fenced block containing **only the prompt**.
3. Below it: **Aspect ratio** · **Resolution** · **Reference images, in order, with their roles** · **Suggested follow-up edits**: 1–3 short conversational edit lines for the last 20% ("edit, don't re-roll").
