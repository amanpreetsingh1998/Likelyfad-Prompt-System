# Model layer: Nano Banana Pro (alternative for character and location sheets)

> **Status: UNTESTED for these masters.** The masters were written for Seedream 5.0 Pro. A Seedream-vs-Nano-Banana test is planned; until it reports, Seedream is the default and Nano Banana is the alternative the user can choose. The general Nano Banana craft lives in `image/nano-banana/`.

When the user picks a **Nano Banana** prompt:
- **The casting does not change.** The theory, the cast plan, the 160–230-word character description, the outfit formula, the problem-area wording and the transition logic are identical.
- **Base sheet: keep the chosen master unchanged, then append the description.** It is the same assembly as Seedream, so the two models can be compared fairly.
  - If the render shows the "over-prompted AI look", or ignores the five-view layout, use the short form below. Nano Banana's own guide warns that very long, dense prompts look more AI-made (`image/nano-banana/references/models/nano-banana-pro.md`, failure mode "The AI look on over-prompted images").
  - Log the result in `docs/prompt-log.md`.
- **Short form (fallback, untested):** hybrid labeled-prose from `image/nano-banana/references/prompt-structure.md`.
  - **Subject:** the character description.
  - **Composition:** the master's sheet layout: five full-body views in a row (front 0°, 3/4 front 45°, left profile 90°, 3/4 back 135°, back 180°), the same character in each view, nothing cropped, 16:9.
  - **Camera:** orthographic-like, 85–100mm equivalent, all views sharp.
  - **Lighting:** the master's lighting lines.
  - **Style:** the master's style definition, in positive form; for the Pixar masters, keep "strongly exaggerated cartoon proportions".
  - **Background:** neutral seamless, no text.
  - Turn the master's "NO …" lists into positive descriptions (Nano Banana guide, Part 8.2). Keep one narrow insurance line at most.
- **Transition edits:** a conversational edit in the SAME session where the Before was made, or a new session with the original Before sheet uploaded as the reference. The workflow's transition rules still apply: a short identity reminder plus concrete changes plus the new outfit, **no blanket "keep everything the same" lock**. This overrides Nano Banana's usual Preserve/Change contracts for transformation stages only.
- **Sessions drift after about 15–20 turns.** Start a fresh session and re-upload the Before sheet.
- **3-view vs 5-view:** same rule as Seedream (5 views when the full body is shown, 3 chest-up views otherwise).
- One model per character: never make a Before in one model and its transitions in the other.
