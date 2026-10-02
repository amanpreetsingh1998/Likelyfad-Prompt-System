# Handing stills to video tools

> From the Nano Banana Pro Prompting Guide v2.0 (April 2026), kept as written. Part numbers refer to that guide; the skill maps each part to a file (see SKILL.md, "What to read, and when").

## Our own video system (Likelyfad, added 2026-10-02)
The stills made here feed the skills in `video/`:
- **`video/ai-ugc`** (Gemini Omni): `@image1` = the first frame (scene + framing + wardrobe), `@charecterset` = the identity sheet, `@productbottle` = the clean product shot.
- **`video/ai-ugc-seedance`** (Seedance 2.0): a first frame, a face image and a product label close-up. Read that skill's SKILL.md for the exact roles.
- **`video/ai-animation`** (Seedance 2.0, Pixar / Zack D): `@image1` = the scene or start frame, `@image2` = the character (5-view full-body sheet when the full body is shown, 3-view when chest-up), `@image3` = the product.
Make the stills in the SAME style as the video path (a Pixar still for the Pixar path). Generate all of a character's stills in one model.

# Part 13 — Video Pipeline Integration

Pro is image-only, but in production ad workflows it's the first step of a longer pipeline. This section has no v1 equivalent.

## 13.1 The dominant pipeline pattern

The most common production workflow across studios as of April 2026:

1. **Concept + script** — Gemini / Claude for ideation, script, shot list
2. **Keyframe generation** — Nano Banana Pro for hero stills, character sheets, scene anchors
3. **Motion generation** — Veo 3.1 (polished), Sora 2 (fast), or Seedance 2.0 (UGC-native) to animate between keyframes
4. **Avatar / talking head** — HeyGen Avatar 4 or Arcads for on-camera dialogue segments
5. **Post-production** — Topaz for upscaling, Premiere/CapCut for editing, Adobe Express for graphic overlays

This pipeline delivers ~70% cost reduction vs. traditional production per published case studies (AIStudios, Creative Pad Media, VidAU).

## 13.2 Nano Banana Pro's role as keyframe generator

Pro is uniquely suited to the keyframe role because of:

- Identity consistency via character sheets (Part 5.2)
- Session memory across keyframes (Part 1.5)
- Precise composition control
- High-resolution output (4K feeds Veo/Sora hi-res pipelines cleanly)

**Recommended workflow:**
1. Generate character sheet (Part 11.11) — one time
2. Generate keyframe #1 (opening shot) with the character sheet as reference
3. In the same session, generate keyframes #2, #3, #4 by conversational edit (Part 7.1) — same character, new scenes/poses/expressions
4. Export all keyframes at 2K or 4K
5. Hand off to video tool

## 13.3 Handoff to Veo 3.1

**Best for:** polished, audio-native, physically realistic final output. The current gold standard for high-quality AI video.

**Handoff format:** upload two keyframes (start and end of shot). Veo generates the motion between them.

**Prompt for Veo in this handoff:**
> Animate from [start keyframe] to [end keyframe]. Motion: [describe the action — "the subject picks up the perfume bottle, unscrews the cap, and applies it to her wrist"]. Camera: [static / slow push-in / handheld]. Duration: [5–8 seconds].

**Limits:** Veo 3.1 is expensive per second, slow to generate, and capped at 8 seconds per shot. Plan shot lengths accordingly.

## 13.4 Handoff to Sora 2

**Best for:** fast iteration, social-ready motion, meme-adjacent formats. Less physically realistic than Veo but significantly faster.

**Handoff format:** single keyframe + motion prompt, or text-to-video with Nano Banana Pro keyframe as style reference.

**Use case fit for paid social:** A/B test variants where you need 5 motion versions of the same keyframe quickly.

## 13.5 Handoff to Seedance 2.0

**Best for:** UGC-style video directly from one image. Seedance is specifically tuned for the "creator content" aesthetic.

**Handoff format:** single keyframe + action prompt.

**Use case fit:** for the Scent Swap reaction concept and other UGC-style ads. Seedance produces natural-looking human motion from a single still.

## 13.6 Handoff to HeyGen / Arcads (talking avatars)

**Best for:** on-camera spoken dialogue, testimonial-style ads.

**HeyGen Avatar 4** — best lip sync, slightly robotic body language. Use for head-and-shoulders dialogue shots.

**Arcads** — library of licensed AI actors, fast A/B variant generation, native ad-creative workflow. Best for high-volume UGC-dialogue production.

**Workflow:**
1. Generate character identity in Nano Banana Pro (character sheet)
2. Upload to HeyGen / Arcads as actor reference (if supported) OR select a library actor that matches
3. Generate dialogue segment with voice
4. Stitch with Veo/Sora B-roll in post

**Note on consistency:** HeyGen and Arcads have their own character libraries that may not perfectly match a Nano Banana Pro character. For brand continuity across static ads and video ads, decide upfront: either use an Arcads actor as your canonical persona (and generate matching stills in Nano Banana Pro), or use a Nano Banana Pro persona (and accept that video dialogue segments will use a different-looking avatar). Mixing both invariably creates identity mismatch.

## 13.7 Upscaling and finishing

**Topaz Video AI** — upscales AI-generated video from 1080p to 4K cleanly, reduces temporal artifacts.

**DaVinci Resolve / Premiere** — final color grading to match keyframes across cuts (important: Veo and Sora have slightly different color science; a grading pass unifies them).

## 13.8 Cost envelope for a paid-social ad production sprint

Rough numbers as of April 2026 (changes monthly):

- Nano Banana Pro: $0.13–$0.24 per image, 20 images for a typical ad sprint = $3–$5
- Veo 3.1: ~$2–$4 per 5-second shot, typical 30-second ad = ~$15–$25
- Sora 2: Cheaper, ~$0.50–$1 per shot
- HeyGen/Arcads: $30–$100/month depending on tier
- Topaz + editor software: sunk cost

**Total direct software cost per ad: ~$20–$50.** The labor cost (briefing, prompt engineering, review, client iteration) dwarfs this. Don't over-optimize on API spend.

---

