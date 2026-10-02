---
name: character-casting
description: Use this skill whenever the user wants characters, character reference sheets, transformation (before/after, week-by-week) sheets, or location reference images built from an ad script, in any of four styles: Pixar simple cartoon, Pixar high fidelity, Realistic Movie or UGC iPhone. Also for casting any recurring character (including UGC creators) so every person is a unique, recognisable, age-true individual. Writes Seedream 5.0 Pro or Nano Banana Pro prompts.
version: 1.0.0
updated: 2026-10-02
---

# Character casting: characters, transformations and locations (image system)

You turn a **full ad script** into a **minimal cast plan**, then **copyable prompts**:
- base character reference sheets;
- reference-guided transformation edits;
- location reference images.

Every person must feel like **a specific, recognisable individual who happens to belong to the audience**, never a generic AI face. Load only the file for the step you are on.

## The flow (ask ONE question per message; wait for each answer; skip anything already given)
1. **Ask for the full script.** Never single scenes: the whole script shows who recurs, who transforms, and which locations are needed.
2. **Ask for the style**, as a plain numbered list:
   1. Pixar — simple cartoon / less HD
   2. Pixar high fidelity
   3. Realistic Movie
   4. UGC iPhone
3. **Ask which model the prompts are for:** Seedream 5.0 Pro (default for these masters) or Nano Banana Pro. Keep that model for every sheet and edit of the project.
4. **Ask for the target audience only if the script doesn't make it clear:** "Who is this ad for? Age, gender, and US background if known."
5. **Read the theory**, then **present the cast, transition and location plan** and **wait for approval**. → `references/theory.md` + `references/workflow.md` ("Find the cast", "Propose the reference-sheet plan").
   - Example: `Main woman — Before base, week 1, week 6; Doctor — one stable sheet; Kitchen — one location; Total: 2 people, 4 character images, 1 location.`
6. **After approval, deliver ONE prompt per message, starting with the main character's Before/base sheet.** Wait for "next" or a revision before the next one.
   - Characters first, then transitions, then locations in story order.
   - If the user asks for all the prompts at once, give them all.

## What to read, and when
- **Always, before casting anyone:** `references/theory.md`. Unique, recognisable, age-true people; the audience notes; the transformation rule; the **Final Editor Check**.
- **To plan, describe, dress and transform:** `references/workflow.md`. It covers:
  - the cast rules and the concern-matched plan;
  - the base-prompt assembly and the 160–230-word descriptions;
  - the outfit formula and the cartoon proportions;
  - the transition edits and revisions.
- **Words for faces, hair and skin:** `references/vocabulary.md`. **Clothing range:** `references/wardrobe.md`. **Visible problems** (cellulite, swelling, bloating, puffiness): `references/problem-areas.md`, which carries the tested wording and the failed-render lessons.
- **The style master (read the chosen one in full, copy it unchanged):** `masters/characters/<style>.md`. For locations: `masters/locations/<style>.md` + `references/locations.md`.
- **The model file for the chosen model:** `references/models/seedream-5-pro.md` or `references/models/nano-banana-pro.md`.

## Sheet layout rule
- **The character's full body appears in the video → a 5-view full-body sheet** (front, 3/4 front, left profile, 3/4 back, back), 16:9. All four masters already specify this.
- **Only ever shown chest-up → a 3-view sheet** (front, 3/4 front, profile) is enough. See the model file for the one-line instruction.

## Must-never
- Never change a master's wording. A base prompt = the complete master + two line breaks + the character description.
- Never put camera, lighting, location, action, dialogue or product directions inside the character description.
- Never invent a visible body change for a non-visible concern (e.g. erectile dysfunction, odour).
- Never make a before/problem character smile.
- Never chain a transition from the previous stage: every stage edits from the ORIGINAL Before sheet.
- Never write "keep everything the same" or a long lock list in a transition. It suppresses the change.
- Never switch models in the middle of a character.
- No generic perfect AI face, no repeated face template across a cast, no stereotypes (see the theory).

## Output format
- Above every prompt, in bold: **Generation model: Seedream 5.0 Pro** (or **Nano Banana Pro**).
- For transitions, also: **Upload the already-created Before reference image of [character].**
- One heading per character, then a one-line `Casting context: …` outside the block, then one fenced `text` block with the complete prompt.
- For revisions, always return the ENTIRE revised prompt, never a fragment.
- After the prompts, remind the user to run the Final Editor Check (`references/theory.md`) on every generated image before it is used in a video.

## Hand-off to video
These sheets feed `video/ai-animation` (Pixar path: `@image2` = the character sheet) and `video/ai-ugc` / `video/ai-ugc-seedance` (the identity reference). Use the same style for the stills as the video path.
