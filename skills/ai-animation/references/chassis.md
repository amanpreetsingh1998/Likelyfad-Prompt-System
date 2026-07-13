# Chassis — the prompt structure (model-agnostic)

The reusable skeleton for every animated-ad prompt. **Locked** bits are affirmative anchors reused every time; **variable** bits change per ad. (Seedance-specific wording — reference roles, the negatives rule, durations — lives in `models/seedance.md`; the look lives in `styles/<style>.md`.)

## The core principle: the image does the heavy lifting
We work **image-first** — a finished Pixar still is the start frame and character art is attached — so Seedance already preserves the subject's identity, composition, and style. The prompt text therefore stays **lean**: it carries **motion, camera, scene beats, and voice**, plus just three short affirmative anchors (role tag, identity lock, style anchor). Don't re-describe what the image already shows.

## Section order (keep this order in the prompt)

1. **References / Assets** *(variable subject, locked method)* — @-tag every supplied asset and state its role in one phrase (first frame, character, character set, location, product). This tagging is the #1 consistency lever. → `models/seedance.md`.
2. **Style anchor** *(locked per style)* — one affirmative clause naming the render family + "keep it consistent first frame to last." → `styles/pixar-disney-3d.md`.
3. **Format / Duration / Mode** *(variable)* — aspect ratio, the length (default ≤15s multi-scene), and the audio mode (talking-head / voiceover / product-world).
4. **Global setup** *(variable)* — one line: who/what + the world; plus a one-line identity lock only for what motion can break ("same face, design, outfit throughout").
5. **Scene beats** *(variable)* — timestamped scenes within the one generation; per scene: action + camera + motion. B-rolls carried by the tagged character/world + text (no fresh start frame). See Motion craft.
6. **Voice / Audio** *(self-contained block; variable)* — delivery mode + voice character + audio mix + ambient. The seam for the future singing layer. See below.
7. **Closing anchors** *(locked)* — restate the identity lock + the affirmative style-consistency line.

## Locked vs. variable
- **Locked (affirmative anchors, every prompt):** the style anchor, the identity-lock phrasing, the closing style-consistency line.
- **Variable (per ad/scene):** references & roles, duration/mode, scene beats, motion, dialogue, audio.

## Default to one ≤15s multi-scene generation
Generation is slow, so **pack the ad into a single ≤15s render** whenever the script allows. Seedance holds one character across multiple scenes in a single generation, and animation is mostly **b-roll** — so you do **not** need a separate start frame per scene. Structure it as timestamped scene beats (`[0–4s] … [4–9s] … [9–15s] …`) with clean transitions and one camera move per beat. Use a shorter single clip only when a shot must be generated on its own. Scene/word budgets → `models/seedance.md`.

## Reference tagging (how to write Section 1)
@-tag each asset and state its role once — the model won't infer roles reliably. Default handles:
- `@image1` → **first frame** (the opening scene still; also sets the world + framing).
- `@image2` → the **character** (identity: face, design, outfit). A character image / character sheet is the usual anchor; keep a character SET to ~3 clean, same-lighting angles, not ten.
- `@image3…` → **location** plate(s) and the **product** (preserve exact shape / label / colors).

> Phrase it plainly: *"Use @image1 as the first frame and the world. Use @image2 as the character — keep the same face, design, and outfit throughout. Use @image3 as the product — preserve its label and shape exactly."* The `@` is just a handle; the stated **role** is what works. Tag only what you're actually given.

## Motion & Performance craft (how to write Section 5)
Animation wants **exaggeration and timing**, not restraint (the opposite of realistic UGC). Thread the animation principles:
- **Squash & stretch** — compress on impact/landing, stretch on a jump; keep the character's volume.
- **Anticipation** — a small wind-up before a big move (crouch before jump, breath before a line).
- **Follow-through / overlap** — hair, cloth, ears lag behind the body; fingers settle last. Avoid everything stopping at once.
- **Arcs** — curved paths, not straight lines.
- **Easing** — ease-in/ease-out; never linear, mechanical motion.
- **Weight** — keep believable gravity/weight (Seedance is strong here) — just make it stylized-snappy, not "realistic."

For **talking scenes**, tie beats to words like the realistic system does — brows, eyes, hands, lean, head — but **animation allows head movement and gesture during speech** (Seedance syncs mouth + head + expression together; the realistic "freeze the head during speech" rule does NOT apply here). Push expressions a little bigger than life.

## Voice / Audio block (Section 6) — self-contained on purpose
Keep this a clean, separable block so the future **singing** layer can swap in without touching motion or style. It carries the **delivery mode**:
- **Talking-head** — an on-screen character speaks: embed the line naturally (`She says: "…"`), 5–10 words, tag the language, note "accurate lip sync, natural pace." (Seedance prefers `says:` over bracketed `[Dialogue]:` tags.)
- **Voiceover / narrated** — no on-screen speaker (or the mouth isn't featured): describe the VO voice + line; lip-sync rules don't bind, so the character/world can move freely.
- **Product / world (no character)** — no dialogue; ambient / sound design only.

Then the **audio mix**: voice character (age/tone/energy), any per-word emphasis, ambient bed. **Music is optional per brief** — include it only when asked; don't hard-lock "no music." (Singing mode — a music track + lyrics — will extend this block later; leave it clean.)
