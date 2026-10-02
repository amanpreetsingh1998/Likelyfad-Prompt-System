# Prompt structure, mindset, deprecated patterns and the pre-flight checklist

> From the Nano Banana Pro Prompting Guide v2.0 (April 2026), kept as written. Part numbers refer to that guide; the skill maps each part to a file (see SKILL.md, "What to read, and when").

# Part 1 — Model Nature and Mindset

## 1.1 What Nano Banana Pro actually is

Nano Banana Pro is the image head of Google's Gemini 3 Pro model. It inherits Gemini 3's reasoning layer, which means it does three things the original Nano Banana (Gemini 2.5 Flash Image) could not:

- **It reasons before rendering.** It parses your instructions, builds an internal logical plan, resolves constraints, then synthesizes pixels. You can actually see this in the API thinking trace — interim "thought images" appear in the backend during generation. These are free (not billed) and are useful for debugging prompt adherence.
- **It infers from context.** Telling it "this is for a premium DTC skincare brand's Meta ad" or "for a Brazilian high-end gourmet cookbook" meaningfully changes plating, depth of field, lighting, and composition. The old model ignored this; Pro uses it as a prior.
- **It can ground in real-world knowledge.** When you ask for factual or data-driven visualizations (news events, weather, stocks, real places), the model can invoke Google Search mid-generation. This is covered in depth in Part 9.

Internally, the model still prioritizes in this order: logical consistency → structural compliance → constraint satisfaction → visual realism → aesthetic coherence. This hasn't changed. What's changed is how you encode instructions — less ceremony, more clarity.

## 1.2 Instruction hierarchy (updated)

When instructions conflict, the model resolves them in this order — highest to lowest priority:

1. **Hard constraints** — explicit preservation rules, counts, prohibited elements
2. **Structural instructions** — layout, composition, spatial relationships, labeled sections
3. **Physical definitions** — camera, lighting, material behavior
4. **Contextual framing** *(promoted from v1's lowest tier)* — audience, purpose, era, genre
5. **Stylistic intent** — aesthetic mode, reference style
6. **Descriptive flavor** — mood, atmosphere adjectives

**The critical change from v1:** contextual framing is now a meaningful steering signal, not ignorable flavor. "For a premium DTC skincare brand" or "for a Gen-Z TikTok ad" sits above stylistic keywords in real-world influence. v1 treated this as bottom-of-stack noise; that was wrong for Pro.

**What stays the same:** never bury critical intent in low-priority language. "A cinematic portrait, don't change the face" still fails because face preservation is being smuggled into descriptive flavor. The correct form remains an explicit preservation clause.

## 1.3 Context and audience framing (new)

This is the biggest underused lever in Pro. The reasoning model builds a prior from context signals and applies it to every other decision in the prompt.

Examples of how context changes output without you specifying the mechanics:

- *"for a premium DTC skincare brand's Meta ad"* → soft commercial studio lighting, neutral palette, center-framed composition, shallow DoF, subtle product hero
- *"for a Gen-Z TikTok organic post"* → direct flash, slight sensor grain, casual framing, messy background, high saturation
- *"for a Brazilian high-end gourmet cookbook"* → overhead plating, natural window light, muted earth-tone props, depth of field calibrated to food photography standards
- *"for a 1990s grunge magazine editorial"* → film grain, mixed indoor/natural lighting, slightly underexposed shadows, desaturated color grade

**Use contextual framing when:** you want the model to infer conventions you don't want to spell out. This saves 5–10 lines of camera/lighting/composition instruction per prompt.

**Don't use it as a substitute for specifics** when you have a strong creative vision. Context sets defaults; explicit camera/lighting/material instructions override them. The two layers stack cleanly.

**Anti-pattern:** contradicting context with explicit direction. *"For a gritty documentary photojournalism project. Studio softbox lighting with beauty dish."* — the model will resolve one of these silently. If you want studio lighting, don't prime it with a documentary context.

## 1.4 The "edit, don't re-roll" philosophy (new)

This is the single biggest behavioral change from v1's mental model.

**The old (v1) pattern:** write a detailed prompt, generate, evaluate, rewrite the prompt, regenerate. Each generation is independent. This was correct for the original Nano Banana, Midjourney, Flux, and Stable Diffusion — models without persistent session state.

**The new (Pro) pattern:** write a reasonable first prompt, generate, then conversationally edit inside the same session. *"That's great, but change the lighting to sunset."* *"Keep everything the same but swap the dress for the one in the reference I just uploaded."* *"Make the text neon blue instead."*

Why this works in Pro:

- Session-based memory retains character identity, environmental consistency, and prior decisions across turns
- Semantic masking lets you describe what to change in words — no brush, no coordinates, no mask image
- The reasoning layer recomputes lighting, reflections, and shadow physics when you change one element (it doesn't just paste a new object in)

**Operational consequences:**

- Your cost per usable asset drops significantly. You get 80% of the way there on the first generation, then spend 3–5 cheap edits to hit 100%, instead of 5–10 full regenerations.
- First-prompt perfectionism is a trap. Get to 80% fast, edit the rest.
- Conversation-aware prompt chains outperform standalone prompts. The session accumulates context that individual prompts can't carry.

**When to break this rule:** if the image is fundamentally wrong (wrong subject, wrong scene, wrong composition), start fresh. Editing is for the last 20%, not for rescuing a broken concept.

## 1.5 Session-based character memory (new)

Once you define a character in a session — either by describing them in detail or by uploading a reference — Nano Banana Pro retains that character for the rest of the session. You don't re-describe them.

**Example session flow:**

- Turn 1: *"Generate a 28-year-old woman with shoulder-length auburn hair, freckles across her nose, wearing a cream linen button-down. Soft natural window light from left, 35mm, f/2.0."* → Image A
- Turn 2: *"Now put her on a Mediterranean beach at golden hour."* → Image B, same face
- Turn 3: *"Same scene, but she's laughing and holding a glass of rosé."* → Image C, consistent identity
- Turn 4: *"Now a close-up, same woman, different outfit — she's wearing a black slip dress at a rooftop bar at night."* → Image D, consistent identity

No re-description needed. The model carries her identity across turns.

**Implications for studio workflow:**

- Define your AI-influencer persona once per session, then generate an entire ad variant library
- Pair this with character sheets (Part 5.2) for identity that survives across sessions
- Don't switch tabs mid-production — each session is its own memory space

**When session memory fails:**

- After ~15–20 turns in the same session, drift begins
- If you upload a new person-reference mid-session, the model may blend them
- If you go idle for hours, session state can degrade

**Mitigation:** for critical identity continuity (an ongoing AI influencer, a recurring brand persona), maintain a frozen character sheet image you re-upload as reference at the start of each session or each batch.

---

# Part 2 — The Default Prompt Structure

## 2.1 Google's official 5-element formula

The canonical formula from the Google Cloud "Ultimate prompting guide for Nano Banana" (March 2026) and the official Gemini blog post is:

> **Subject + Action + Location/context + Composition + Style**

Optionally followed by:
- Editing instructions
- Exact text (wrapped in quotes)
- Factual/brand constraints
- Reference-image roles

This is the baseline. For most ad-creative work you'll extend it slightly; for quick iteration it's enough as-is.

**Example (bare 5-element):**
> A woman in her late 20s pouring coffee into a ceramic mug, standing at a sunlit kitchen counter, medium shot from the waist up, soft cinematic lifestyle photography.

This prompt works. The old v1 instinct is to add ten more lines of JSON scaffolding. Resist it.

## 2.2 The extended hybrid labeled-prose structure (your default)

For production ad work where you need more control than the 5-element formula but don't want full JSON ceremony, use hybrid labeled-prose. This is the pattern Guillaume Vernade (Google DevRel) uses in the official viral-thumbnail templates, and it's what every major community creator has converged on.

**Structure:**

```
Subject: [one specific sentence — materiality, named identity if consistent]
Action: [what's happening in one clear sentence]
Location: [setting with atmospheric cues]
Composition: [framing + aspect ratio, e.g., "medium-full shot, center-framed, 4:5"]
Camera: [lens/aperture/hardware, e.g., "shot on Fujifilm X-T4, 35mm, f/2.0"]
Lighting: [specific setup — see Part 3.2 for vocabulary]
Style: [medium + color grade, e.g., "editorial fashion, muted teal cinematic grade, 1980s film grain"]
Text: [if any — always wrapped in quotes, specify font + weight + color + position]
Context: [for whom/why — one phrase, optional but high-leverage]
```

For edits, append:
```
Preserve: [what stays exactly the same]
Change: [what's different]
```

For multi-reference work, append:
```
Reference roles: Image 1 = [role], Image 2 = [role], Image 3 = [role]
```

**Why this works:** it reads as prose to the reasoning model (which prefers natural language) but behaves structurally like JSON (parameter isolation, clear ownership, no keyword collisions). You get the best of both worlds.

**A complete example (product ad for the dupe perfume project):**

```
Subject: A hand holding a minimalist 50ml amber glass perfume bottle with a matte gold cap, label reads "No. 214".
Action: Lifting the bottle toward soft morning light.
Location: Marble bathroom vanity with blurred greenery in background.
Composition: Close-up, product-centered, 4:5 vertical.
Camera: Shot on Canon R5, 85mm macro, f/2.8.
Lighting: Soft natural window light from 10 o'clock, subtle gold reflection on glass, low-contrast shadow on marble below.
Style: Premium commercial beauty photography, warm cinematic color grade.
Text: Overlay bottom-center in bold sans-serif white: "Inspired by Libre."
Context: For a premium DTC fragrance brand's Meta ad.
```

This is your default shape. Save it as a template.

## 2.3 When to use pure short prose

One to three sentences, no labels. Use this when:

- The concept is simple and the first generation is exploratory
- You're using Search grounding ("Infographic showing how the EU carbon market works" — short prompts work fine here)
- You're using the consumer Gemini app rather than the API
- You're iterating in a session and the earlier prompt already set most of the context

**Example:** *"A minimalist cream-colored perfume bottle on a sunlit marble surface, shot on film, 4:5 vertical."*

That's it. The model fills in competent defaults. Don't over-specify when you don't need to.

## 2.4 When to use full JSON

JSON still has a place. Use it when:

- **You're running a batch/programmatic pipeline** where only one field changes per call (e.g., generating 50 product shots where only the bottle name changes)
- **You're doing multi-subject/multi-character work** and need strict color/outfit separation to prevent "rainbow vomit" where background hues bleed onto wardrobe
- **You're building an identity-locked AI-influencer library** where reproducibility matters more than creative nuance
- **You're programmatically composing prompts** from a CMS or spreadsheet

**Example JSON for batch product shots:**

```json
{
  "subject": {
    "type": "perfume_bottle",
    "size_ml": 50,
    "glass_color": "amber",
    "cap": "matte gold",
    "label": "No. 214",
    "count": 1
  },
  "environment": {
    "surface": "white marble vanity",
    "background": "blurred green foliage",
    "time_of_day": "morning"
  },
  "camera": {
    "lens_mm": 85,
    "aperture": "f/2.8",
    "framing": "close-up",
    "aspect_ratio": "4:5"
  },
  "lighting": {
    "key": "soft natural window",
    "direction": "10 o'clock",
    "fill": "none",
    "contrast": "low"
  },
  "style": "premium commercial beauty photography, warm cinematic grade",
  "preserve": ["label text exact", "bottle shape exact"],
  "text_overlay": {
    "content": "Inspired by Libre",
    "font": "bold sans-serif",
    "color": "white",
    "position": "bottom center"
  }
}
```

**Do not use full JSON as default.** It's ceremony for single-shot creative work. It shines specifically in production pipelines.

## 2.5 The structure decision tree

```
Is this a single-shot exploratory prompt?
├── YES → Short prose (2.3)
└── NO → Is it a production batch with one variable per call?
         ├── YES → Full JSON (2.4)
         └── NO → Is it multi-subject with color/outfit bleed risk?
                  ├── YES → Full JSON (2.4)
                  └── NO → Hybrid labeled-prose (2.2) ← DEFAULT
```

Default to hybrid. Escape to JSON only for the two specific cases. Escape to short prose only for exploration or session continuations.

## 2.6 What to stop doing (v1 patterns to retire)

- **Do not** start every prompt with `mode: GENERATE` or `mode: EDIT` declarations. Pro is conversational — declare mode only if you're doing full JSON.
- **Do not** use a rigid 10-field schema for every prompt. It's overkill.
- **Do not** add "8K, masterpiece, trending on artstation, hyperdetailed, award-winning" or similar quality-spam. It's treated as noise at best, as over-prompting at worst.
- **Do not** lead with a long `negative:` block. See Part 8 for why.
- **Do not** encode brand voice or audience as stylistic flavor at the end. Put it in `Context:` where it actually steers output.

---

# Part 14 — Deprecated Patterns (Remove from Old Templates)

If you're migrating from v1 to v2, purge these patterns from saved templates and SOPs.

## 14.1 Quality-spam keywords (DELETE)

Remove:
- "8K" / "4K" / "UHD" (unless declaring actual output resolution)
- "masterpiece"
- "trending on artstation"
- "hyperdetailed"
- "award-winning photography"
- "best quality"
- "ultra realistic"
- "photorealistic" (when used as a generic boost, not a specific style directive)

These do not help and may over-prompt.

## 14.2 Mandatory negative blocks (DELETE)

Remove the long generic negative blocks:
- "lowres, blurry, bad anatomy, bad hands, extra fingers, watermark, signature, text artifacts, oversaturated..."

See Part 8. Negatives are now narrow insurance, not default layer.

## 14.3 Rigid 10-field JSON as default (DELETE)

Remove: the habit of starting every prompt with the full JSON skeleton from v1 Part 2.2.7 (mode / intent / subject / environment / camera / lighting / materials / composition / constraints / negative).

Keep: JSON only for the specific cases in Part 2.4 (batch, multi-subject, brand systems).

## 14.4 Explicit mode declarations (DELETE)

Remove:
- `"mode": "GENERATE"` / `"mode": "EDIT"` as first-line declarations
- `mode: GENERATE` in structured text prompts

Pro is conversational. Mode is inferred from context.

## 14.5 "Don't change the face" in prose (REPLACE)

Remove: *"A cinematic portrait, don't change the face"*

Replace with: *"Preserve: facial features, bone structure, skin tone, eye color. Change: [specific element]."*

Preservation contracts must be explicit and named.

## 14.6 Style-as-physics substitutions (DELETE)

Remove:
- "iPhone photo" as a style label

Replace with:
- "Shot on iPhone with direct flash, deep DoF, small sensor look, slight noise"

Always express intent as physics, not as style shortcuts. This one v1 got right and it's still right.

## 14.7 "Descriptive flavor" deprioritization (UPDATE)

Remove the mental model that "descriptive flavor" (mood, context, audience) is lowest-priority and should be minimized.

Replace with: treat audience/purpose framing as a high-leverage contextual layer (Part 1.3). This is a genuine upgrade to how you prompt Pro.

## 14.8 Atomic-instruction dogma (SOFTEN)

v1 was strict: "each instruction should address one variable only." This is still broadly correct, but Pro tolerates and often benefits from compound natural-language descriptions. "Warm golden hour backlight with a slight rim glow on the edges of her hair" is fine — it's not three atomic instructions, it's one cohesive lighting description.

## 14.9 Global edit-scope locks (REPLACE)

Remove: global preservation locks ("preserve everything except [X]").

Replace with: named preservation contracts ("Preserve: [specific list]. Change: [specific list].").

Named lists outperform global locks in Pro.

## 14.10 "One-shot correctness" goal (SHIFT)

v1's mental model: write a perfect prompt, generate once, ship.

Pro's workflow: write a reasonable prompt, generate, iterate conversationally to perfection. "80% first-shot correctness + cheap conversational polish" outperforms "one-shot perfection attempts" on both quality and cost. See Part 1.4.

---

# Part 16 — Pre-Flight Validation Checklist

Before submitting any prompt for production work, run this checklist mentally. This replaces v1's 7.11 pre-flight checklist.

## 16.1 Structure check

- [ ] Am I using the right structure for this task? (Hybrid labeled-prose as default; JSON only for batch/multi-subject/brand systems; short prose for exploration)
- [ ] Is aspect ratio declared?
- [ ] Is context/audience framing included if it would help?

## 16.2 Subject check

- [ ] Subject is specific (not "a woman" but "a 28-year-old woman with shoulder-length auburn hair")
- [ ] Count is explicit if more than one
- [ ] Identity preservation is explicit if using a reference

## 16.3 Physics check

- [ ] Camera specified (lens + framing + aperture or DoF)
- [ ] Lighting specified (source + direction + hardness + color temp)
- [ ] Materials specified where they matter (fabric, surface, finish)

## 16.4 Text check (if text is in the image)

- [ ] All text wrapped in quotes
- [ ] Font described (weight + classification)
- [ ] Color specified
- [ ] Position specified
- [ ] For long strings: copy verified separately first

## 16.5 Edit check (if editing)

- [ ] Preserve list is explicit and named
- [ ] Change list is explicit and bounded
- [ ] Not trying to do too many changes in one turn (split into 2–3 turns if complex)

## 16.6 Reference check (if multi-image)

- [ ] Each reference has an assigned role
- [ ] Each attribute has one source (no conflict)
- [ ] Unwanted elements from references are explicitly excluded

## 16.7 Deprecated-pattern check

- [ ] No quality-spam keywords ("8K", "masterpiece", etc.)
- [ ] No long generic negative block
- [ ] No `mode:` declarations in a conversational prompt
- [ ] No "style-as-physics" shortcuts

## 16.8 Output check

- [ ] Resolution tier is appropriate (2K default; 4K for text-heavy or print)
- [ ] Aspect ratio matches target platform

## 16.9 Verification plan (if grounded)

- [ ] If the prompt uses Search grounding, a manual fact-check pass is planned before shipping

If any check fails, fix the prompt before generating. If you're confident on all checks, ship.

---

# Appendix A — One-page quick reference (print this)

**Default structure (hybrid labeled-prose):**
```
Subject: [specific + materiality]
Action: [one sentence]
Location: [setting]
Composition: [framing + aspect ratio]
Camera: [lens + aperture + hardware]
Lighting: [source + direction + hardness + temp]
Style: [medium + grade]
Text: "[exact]" in [font + color + position]
Context: [for whom / why]
[Preserve + Change if editing]
[Reference roles if multi-image]
```

**Five operational rules:**
1. Edit, don't re-roll (80% first-shot + conversational polish)
2. Wrap all text in quotes
3. Name preservation contracts explicitly
4. No generic negative blocks; positive reframing instead
5. Default 2K resolution, 4K for text-heavy

**Five things to purge from old prompts:**
1. Quality-spam keywords (8K, masterpiece, etc.)
2. Long generic negative blocks
3. Rigid 10-field JSON as default
4. `mode: GENERATE` / `mode: EDIT` declarations
5. Style-as-physics shortcuts ("iPhone photo")

**Five new capabilities to actually use:**
1. Context/audience framing as a steering layer
2. Session-based character memory
3. Character sheets for cross-session identity
4. Semantic masking for edits
5. Search grounding for data-driven visuals (with verification)

