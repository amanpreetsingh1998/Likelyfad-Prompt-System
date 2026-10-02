# Model layer: Nano Banana Pro (Gemini 3 Pro Image)

> From the Nano Banana Pro Prompting Guide v2.0 (April 2026), kept as written. Part numbers refer to that guide; the skill maps each part to a file (see SKILL.md, "What to read, and when").

# Nano Banana Pro Prompting Guide v2.0

**Version:** 2.0
**Last updated:** April 2026
**Model:** Nano Banana Pro (Gemini 3 Pro Image, `gemini-3-pro-image-preview`)
**Scope:** Image generation and editing only. Video handoff covered in Part 13.

---

# Part 9 — Search Grounding (New Capability)

This section has no v1 equivalent because the capability didn't exist. Search grounding is one of Pro's defining features and it's genuinely novel.

## 9.1 What search grounding is

Nano Banana Pro can invoke Google Search mid-generation to retrieve real-world information and use it as input to the image. This enables classes of output that no prior image model could produce:

- Current weather maps
- Real-time stock charts
- News event illustrations with accurate context
- Travel guide visuals with real landmarks and geography
- Infographics sourcing live data (population, election results, economic indicators)
- Product comparison visuals using real current prices

## 9.2 When grounding triggers

Grounding engages automatically when your prompt requests factual, current, or data-driven content. You don't declare "use search"; the model decides based on the request.

**Triggers grounding:**
- "Infographic showing current EU carbon prices"
- "Weather map of Europe for today"
- "Illustrated timeline of the 2024 US presidential election"
- "A visual of the top 10 most populous cities in 2026, with current populations"
- "Illustration of [current news event]"

**Does not trigger grounding:**
- Fictional / stylized scenes
- Generic product photography
- Personal creative work
- Anything that doesn't require external facts

## 9.3 The grounding prompt formula

Google's documented structure:

> [Source or search request] + [Analytical task] + [Visual translation]

**Example:**
> Search for the current average fragrance prices of Dior Sauvage, Creed Aventus, and Chanel Bleu de Chanel in Europe. Calculate how much a customer would save by buying a 100ml dupe at €22.99 instead. Visualize this as a clean horizontal bar chart in a minimalist editorial style, 16:9 landscape, warm cream background, bold sans-serif typography.

This produces a grounded infographic pulling live competitor prices.

## 9.4 The mandatory verification discipline

**Search grounding can hallucinate.** Google's own DevRel guide, as well as Simon Willison's and Max Woolf's analyses, have documented cases where grounded infographics mix real and fabricated data. The model sometimes grounds the first claim and then makes up subsequent ones.

**Always verify grounded output before shipping.** Spot-check every factual claim. Do not use grounded infographics for client deliverables without manual fact-check.

## 9.5 What grounding is genuinely useful for

- Rapid prototype visualizations for pitches and decks (where verified-before-shipping is the SOP)
- Internal research/exploration
- News-jacking social posts (with a manual fact-check pass)
- Travel and real-world location content
- Illustrated explanations of current events

## 9.6 What grounding is not useful for (yet)

- Final ad creative with factual claims (verify manually, then commission the real infographic separately if accuracy is critical)
- Financial or medical content (accuracy standards are too high)
- Any client-facing deliverable that depends on data precision

---

# Part 10 — Output Control (Aspect Ratio, Resolution, Context Window)

## 10.1 Aspect ratios (always declare)

Pro supports: 1:1, 3:2, 2:3, 3:4, 4:3, 4:5, 5:4, 9:16, 16:9, 21:9.

**Always state the aspect ratio in the prompt.** Implicit aspect ratios produce inconsistent results.

**For paid-social ad production specifically:**
- 1:1 — Instagram feed, LinkedIn, multi-platform fallback
- 4:5 — Instagram feed portrait (prime real estate, best feed performance)
- 9:16 — Stories, Reels, TikTok, YouTube Shorts
- 16:9 — YouTube, landing pages, Facebook link previews
- 21:9 — cinematic hero banners, YouTube thumbnails with letterbox

## 10.2 Resolution tiers and pricing

Pro outputs at three resolution tiers:

| Tier | Approx pixels | API cost (per image) | Best for |
|---|---|---|---|
| 1K | ~1024 px | ~$0.134 | Quick iteration, thumbnails, low-res social |
| 2K | ~2048 px | ~$0.134 | **Default for paid social ad production** |
| 4K | ~4096 px | ~$0.240 | Hero creative, print, billboard, text-heavy work |

**Operational guidance:**
- Default to 2K for Meta/TikTok ads — 2K downscales cleanly to platform specs with room for crop variants
- Use 4K only for hero shots, print deliverables, or text-heavy creative where legibility matters
- Use 1K for rapid exploration and A/B variant generation where final resolution can be regenerated once a direction is approved

**Batch economics:** for a 20-ads/month scope at 2K, API-only cost is roughly $2.68/month for generation. At 4K, $4.80. Negligible compared to labor time; don't over-optimize on this.

## 10.3 Context window (Pro vs. Flash)

- **Gemini 3 Pro Image:** 65,536 input tokens
- **Gemini 3.1 Flash Image:** 131,072 input tokens

Counterintuitively, Pro has half the context window of Flash. This matters for:

- Very long conversational editing sessions (when session memory + accumulated turns approach 65K)
- Prompts with many reference images (each image consumes tokens)
- Dense JSON prompts

**Practical implication:** for extended multi-turn ad production in a single session, if quality starts to degrade after ~15–20 turns, it's usually context pressure. Start a fresh session and re-seed with your character sheet.

## 10.4 Thinking mode output

When called via the API, Pro produces interim "thought images" visible in the thinking trace. These are:

- Not billed
- Useful for debugging prompt adherence
- Sometimes show the reasoning step-by-step (the model iterating on a hard layout)

For consumer app users (gemini.google.com), thinking mode is abstracted away and you see only the final image.

## 10.5 Output format controls

You can request specific output framing behavior:

- *"Output a tight crop with no borders."*
- *"Include 10% breathing room around the subject on all sides."*
- *"Output with a 1:1 safe zone centered, suitable for multi-platform crop."*

For campaigns targeting multiple platforms from one master asset, the 1:1 safe zone approach is high-leverage — generate at 16:9 with subject safely inside a centered 1:1 crop region, then you can export square, vertical, and landscape from one master.

---

# Part 12 — Known Failure Modes (Honest Documentation)

Pro is the best available image model, but it has failure modes. Knowing them up front saves rework. This section has no v1 equivalent.

## 12.1 Hands and complex anatomy

Hands in specific poses (holding objects at unusual angles, making specific gestures, close-up detail shots) still fail intermittently. Expect one Photoshop pass per 5–10 images for client-facing work.

**Mitigation:**
- Frame shots to avoid close-up hands where possible
- When hands must be visible, use simple poses (open palm, relaxed fist, holding object at natural grip)
- For critical shots, plan a hand touch-up in post

**Other anatomy failure zones:**
- Feet in unusual positions
- Crossed limbs (arms crossed over legs, etc.)
- Hair interacting with complex fabric
- Eyes in extreme close-up (asymmetry, catchlight inconsistency)

## 12.2 Exact brand-hex color matching

Pro cannot hit specific hex codes via prompting alone. "PANTONE 18-1138 Tangerine" or "#C41E3A" will be approximately correct, not pixel-accurate.

**Mitigation for brand-critical color:**
- Get the model close via descriptive language ("warm terracotta orange with slight red undertone")
- Apply a LUT or color-balance adjustment in post for exact brand color
- For logos especially, composite the actual vector logo over the generated background

## 12.3 Small text (<12px equivalent)

Text rendered at small scale degrades into gibberish. Pro's text rendering is strong at large scale but weakens sharply below a threshold.

**Mitigation:**
- Generate at higher resolution (2K minimum, 4K for dense text)
- If small text is critical, composite it in post using actual fonts
- Design compositions so critical text is prominent, not fine-print

## 12.4 Search grounding hallucinations

Grounded outputs sometimes mix real and fabricated data. The first claim may be grounded; subsequent claims may be invented.

**Mitigation:** always manually verify grounded data before shipping. See Part 9.4.

## 12.5 Cultural and idiomatic nuance in multilingual text

Pro renders foreign-language characters correctly, but occasionally produces phrasing that reads as direct-translation rather than native idiom.

**Mitigation:** have a native speaker proof any multilingual text before production use. This is critical for your Italian (magyx.it), German (magicperfume.co), and localized variants.

## 12.6 Reflection consistency

Identity appearing in mirrors, TV screens, or reflective surfaces sometimes diverges from the primary subject's identity.

**Mitigation:** explicit constraint (*"The reflection must show the same face, identical features"*) or post-composite the reflection separately.

## 12.7 Physics in composites

When compositing multiple references, light source direction, shadow angle, and environmental color temperature sometimes conflict. A subject lit from the left with hard shadows pasted into a background lit from above creates visual discord.

**Mitigation:** specify unified lighting explicitly (*"Unify lighting to match the background reference: soft window light from the upper left, warm 3200K"*). For critical work, generate subject and background separately with matched lighting specs, then composite.

## 12.8 Rainbow vomit (multi-subject color bleed)

When generating multiple subjects in one scene, background colors sometimes bleed onto wardrobe or product surfaces, creating "rainbow vomit" — clothing that picks up stray hues from the environment.

**Mitigation:** use JSON for multi-subject scenes (Part 2.4). Explicitly declare each subject's color separately and name the background color.

## 12.9 Session memory degradation

Session context degrades after ~15–20 turns. Quality drops, identity drifts, and the model starts producing results that feel "off."

**Mitigation:** for long production sessions, start fresh after ~15 turns and re-seed with your character sheet. For batch work, break into chunks.

## 12.10 Temporary image disappearance

Pro occasionally returns a "temporary image" or empty output, particularly on complex prompts. This is a known bug documented in community troubleshooting posts.

**Mitigation:** retry. If it persists, simplify the prompt by one or two elements. Complexity at the edge of the context window can trigger this.

## 12.11 The "AI look" on over-prompted images

Paradoxically, prompts with too many detail specifications produce images that look more AI-generated than prompts with fewer. The reasoning layer over-interprets dense specification into an uncanny-valley aesthetic.

**Mitigation:** prune prompts. Specify only what matters. Context framing (Part 1.3) often accomplishes what ten lines of adjectives attempt.

---

