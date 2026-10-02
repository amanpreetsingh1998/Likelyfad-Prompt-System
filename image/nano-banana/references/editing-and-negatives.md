# Editing and negative prompting

> From the Nano Banana Pro Prompting Guide v2.0 (April 2026), kept as written. Part numbers refer to that guide; the skill maps each part to a file (see SKILL.md, "What to read, and when").

# Part 7 — Editing: Conversational Mode and Preservation Contracts

## 7.1 The conversational edit (default workflow)

With Pro, editing is session-based and conversational. No mode declaration. No explicit base-image reference.

**Example session:**

- *Turn 1:* Generate an image (as described in Part 2).
- *Turn 2:* "Change the lighting to sunset, keep everything else identical."
- *Turn 3:* "Swap the dress for a black slip dress, same fabric quality, same length."
- *Turn 4:* "Make it a 16:9 landscape crop centered on her face."

Each turn preserves prior context by default. You only specify what changes.

## 7.2 Semantic masking (no brush, no coordinates)

v1 described spatial region logic and layout anchors. Pro goes further: you describe the mask in natural language and the model identifies the region.

**Examples:**
- "Change just the jacket from brown to olive green."
- "Add a pair of sunglasses, leave everything else identical."
- "Replace the sky with a stormy overcast sky, preserve the foreground exactly."
- "Remove the lamp from the background."
- "Make the sign in the distance read 'OPEN' instead of 'CLOSED'."

The model recomputes lighting, reflections, and shadows appropriately when you change one element. Semantic masking is a core Pro capability and eliminates the need for the complex spatial-region declarations v1 required.

## 7.3 The named-preservation pattern

For edits where drift is a risk (identity, brand assets, architectural features), explicitly name what must stay:

```
Change: swap the background from studio gray to a sunlit marble countertop.
Preserve: the perfume bottle shape, label text, cap color, glass tint, and catchlight highlights exactly as in the original.
```

This formulation consistently outperforms "keep everything the same" because it tells the model specifically what has authority.

## 7.4 Partial transformations

You can apply a style to only part of an image. State the scope explicitly:

- "Apply a watercolor style only to the background. The person remains photorealistic."
- "Convert only the sky to an illustrated painterly style. The ground and subject stay photographic."
- "Change the art style of the poster on the wall to anime; the room stays real."

## 7.5 Edit types Pro handles cleanly

- **Lighting change** ("change to golden hour," "change to blue hour," "add neon practicals")
- **Weather change** ("make it rain," "add fresh snow")
- **Time of day** ("same scene at night")
- **Season** ("convert this summer scene to winter")
- **Outfit change** ("change shirt to black turtleneck")
- **Expression** ("change to a warm smile")
- **Background swap** ("same subject, new background of [description]")
- **Object addition** ("add a coffee cup on the table")
- **Object removal** ("remove the lamp")
- **Text replacement on signs, products, labels**
- **Color grading** ("apply a teal-orange cinematic grade")
- **Style transfer** ("render in watercolor / anime / oil painting style")
- **Aspect ratio / crop change** ("crop to 9:16 centered on the face")
- **Age progression/regression** ("show what this person looks like 20 years older")
- **Perspective change** ("same scene from a low angle looking up")

## 7.6 Edit types that require more care

- **Complex multi-element edits** — break into two or three sequential edits rather than one
- **Edits that conflict with physics** (adding a shadow where no light source exists) — model may refuse or produce artifacts
- **Edits requiring precise brand-hex colors** — approximate result, finish in post
- **Adding text to an existing image** — works, but treat text specs with the same rigor as Part 4

## 7.7 When to start fresh vs. edit

**Edit when:**
- The image is 80%+ correct
- You want to preserve identity/setting across iterations
- You're refining composition, lighting, or details

**Start fresh when:**
- The concept is fundamentally wrong
- The subject is wrong
- The composition is broken
- You've done 10+ edits in a session and drift has accumulated

## 7.8 Deprecated v1 edit patterns

Remove these from your templates:

- `mode: EDIT` declarations at the top of prompts (Pro is conversational)
- Explicit "base image" reference in conversational edits (the session handles this)
- Rigid preserve/change JSON blocks for single-turn edits (use prose preservation contracts instead)
- Spatial coordinate declarations for masks (use semantic descriptions)

---

# Part 8 — Negative Prompting: The Modern View

This section is a significant departure from v1. Negatives are no longer a mandatory layer; they're a narrow insurance tool.

## 8.1 Why negatives are largely deprecated

The original Nano Banana (and all diffusion-era models before it) benefited from negative prompt blocks because the models lacked a reasoning layer to infer common exclusions. You had to tell Stable Diffusion "no extra fingers, no duplicate limbs, no watermarks, no text artifacts" because it would otherwise produce them.

Pro's reasoning layer infers these exclusions automatically. Explicit negatives for common issues — anatomy, watermarks, duplicate objects, fused limbs, warped faces — are now usually unnecessary and can actively hurt results by over-constraining the model.

Google's official guidance is now: **use positive framing — describe what you want, not what you don't want.**

## 8.2 Positive reframing (always try this first)

| Negative (old way) | Positive (Pro way) |
|---|---|
| "no cars" | "empty street" |
| "no people" | "empty room" |
| "no clutter" | "minimalist clean background" |
| "no extra fingers" | *(nothing — the model handles this)* |
| "no watermarks" | *(nothing — the model handles this)* |
| "not cartoony" | "photorealistic, natural skin texture" |
| "no warped face" | "natural proportions, identity-locked to reference" |
| "no text artifacts" | *(nothing; or wrap text in quotes per Part 4)* |
| "no blurry background" | "sharp throughout" or "shallow DoF with clean bokeh" |

## 8.3 The narrow cases where negatives still earn their place

Three specific scenarios justify explicit negatives:

**1. Identity-lock insurance for critical AI-influencer work.** See Part 5.5. Use the Sider-validated list: *"Avoid: age change, face warp, asymmetrical eyes, extra fingers, logo distortion, text artifacts, blended faces, identity drift."*

**2. Multi-image reference exclusion.** When combining references, specify what not to carry over from each: *"Ignore the background of Image 1. Ignore the color palette of Image 2."* See Part 6.8.

**3. Brand-safety constraints for production pipelines.** For programmatic batch generation going to client review: *"Exclude: competitor logos, celebrity likenesses, copyrighted characters, offensive symbols."* This is a compliance layer, not a quality layer.

## 8.4 Negative prompting anti-patterns (remove from templates)

- Long generic negative blocks at the end of every prompt ("lowres, blurry, bad anatomy, watermark...")
- Style-exclusion negatives ("not AI-looking," "not generic") — state the positive style instead
- Over-specified physics negatives ("no floating objects, no impossible shadows") — redundant for Pro
- Negatives that duplicate preservation contracts ("don't change the face" + "preserve facial features") — pick one, use positive

## 8.5 The one-liner rule

If you do use negatives, keep them to one compact line. Anything longer is probably a sign you should restructure the positive prompt instead.

---

