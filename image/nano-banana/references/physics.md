# Physical realism: camera, lighting, materials, composition

> From the Nano Banana Pro Prompting Guide v2.0 (April 2026), kept as written. Part numbers refer to that guide; the skill maps each part to a file (see SKILL.md, "What to read, and when").

# Part 3 — Physical Realism (Camera, Lighting, Materials, Composition)

This is the section where v1 was mostly right. The physics vocabulary still does the heavy lifting. Some of it has been tightened based on community testing.

## 3.1 Camera

### 3.1.1 Mandatory camera parameters (minimum set)

For any shot where realism matters, specify at least:

- **Lens** — focal length or descriptor ("85mm portrait lens," "24mm wide-angle," "macro," "fisheye")
- **Framing** — close-up, medium shot, medium-full, full body, extreme wide, overhead/top-down
- **Aperture OR depth of field** — pick one vocabulary and stick to it (`f/1.8` or "shallow depth of field," not both contradicting)
- **Camera hardware (optional but high-leverage)** — specific camera bodies steer the look meaningfully

### 3.1.2 Lens semantics table

| Lens | Behavior |
|---|---|
| 24mm wide-angle | Environmental context, subtle distortion at edges, deep DoF |
| 35mm | Natural documentary look, mild environmental context |
| 50mm "nifty fifty" | Human-eye perspective, clean portraits |
| 85mm portrait | Flattering compression, smooth subject isolation |
| 100mm+ telephoto | Strong background compression, product hero shots |
| Macro | Extreme close-up, shallow DoF, micro-texture emphasis |
| Fisheye / 14mm ultra-wide | Circular distortion, interior/architecture, action sports |

### 3.1.3 Camera hardware that steers look

Naming specific hardware triggers learned priors. Examples the community has validated:

- **"Shot on Fujifilm X-T4"** — clean modern color science, sharp, film-simulation look
- **"Shot on Canon R5"** — warm skin tones, commercial cleanliness
- **"Shot on Sony A7IV"** — neutral, slightly cool, editorial
- **"Shot on a disposable camera"** or **"Kodak FunSaver"** — lo-fi, flash, slight blur, nostalgic color
- **"Shot on iPhone selfie with direct flash"** — harsh key light, small sensor look, deep DoF, slight noise — *this is the canonical "authentic UGC" lens*
- **"GoPro action cam"** — ultra-wide, deep DoF, slight distortion
- **"1980s color film, slightly grainy"** — film halation, desaturated shadows, warm tones
- **"35mm film, Portra 400"** — classic editorial film palette, soft skin rendering
- **"Polaroid"** — square frame, muted saturation, light leak

### 3.1.4 Depth of field is a camera result, not an adjective

v1 was correct on this and it's still true. Don't say "blurry background." Say "f/1.8, shallow depth of field, subject tack sharp, background softly blurred." The physical encoding produces a more natural bokeh than the adjective.

### 3.1.5 Common camera failures

- **Over-specifying** multiple contradictory lens and aperture values → model picks one silently
- **Mismatched lens and framing** (e.g., "100mm telephoto, full body wide shot in a small room") → physically impossible, model improvises
- **Film look + digital camera body** (e.g., "shot on Sony A7IV with heavy grain") → contradicts, resolve to one

## 3.2 Lighting

### 3.2.1 Lighting is directional physics, not mood

v1 was right about this. "Cinematic lighting" is useless; "soft key light from 10 o'clock, low contrast, no rim" is useful.

### 3.2.2 Required lighting attributes

- **Primary source** — natural window, softbox, hard direct sun, practical (lamp/neon), direct flash
- **Direction** — clock position (10 o'clock, 2 o'clock), or left/right/front/back/above
- **Hardness** — soft diffused vs. hard (sharp-edged shadows)
- **Color temperature** — warm (golden hour, tungsten), neutral (midday), cool (overcast, blue hour)
- **Fill** — fill light presence/absence, or ambient bounce
- **Optional: rim/hair light** — backlight separation

### 3.2.3 Lighting vocabulary that works

- **"Three-point softbox setup"** — controlled commercial look
- **"Chiaroscuro lighting"** — high contrast, strong shadows, dramatic
- **"Golden hour backlight"** — warm rim, long shadows, halation
- **"Blue hour ambient"** — cool, low-contrast, twilight
- **"Hard direct flash"** — harsh shadows, flat subject, UGC/event photography look
- **"Soft window light from left, low contrast"** — editorial natural
- **"Overcast diffused daylight"** — flat, even, no hard shadows
- **"Neon practical lighting, cyan and magenta"** — cyberpunk/nightlife
- **"Candlelight practical, warm 2200K, low contrast"** — intimate interior
- **"Tungsten room light + window daylight mix"** — realistic domestic interior

### 3.2.4 Lighting overrides style

If you specify lighting and style that conflict, lighting wins. "Cinematic high-key lighting" and "moody noir aesthetic" fight each other; the concrete lighting description dictates the final image.

### 3.2.5 Color temperature stops unreal tones

Explicitly saying "warm 3200K" or "neutral 5500K" or "cool 7000K" prevents the model from arbitrary color drift. For brand-color-critical work, specify.

## 3.3 Materials

### 3.3.1 Materials are physical properties, not adjectives

"Luxurious fabric" fails. "Heavy navy linen with visible weave, slight natural wrinkle, matte finish" works.

### 3.3.2 Material vocabulary

**Fabrics:**
- Linen (visible weave, natural wrinkle, matte)
- Silk (smooth, high sheen, flowing drape)
- Wool tweed (textured, warm, structured)
- Cotton twill (clean drape, moderate sheen)
- Velvet (plush pile, light-direction-dependent sheen)
- Leather (natural grain, moderate sheen, creases at stress points)
- Denim (twill weave, indigo variation, worn edges)

**Hard materials:**
- Brushed aluminum (fine directional grain, cool neutral)
- Polished chrome (mirror-finish, high reflectivity, environment reflections)
- Matte ceramic (clean, low reflection, slight texture)
- Raw clay (rough, earthy, matte)
- Carrara marble (veined white, polished, cool highlights)
- Concrete (rough grain, warm gray, subtle variation)
- Weathered oak (visible grain, natural color variation, satin finish)

**Glass/liquid:**
- Amber glass (warm translucency, subtle tint, environment-lit edges)
- Frosted glass (diffuse transmission, soft edge light)
- Crystal (high clarity, sharp refraction, rainbow edge glints)
- Water (surface tension, refraction, minor caustics)

### 3.3.3 Skin realism rules

- Always include "natural skin texture" or "visible pores"
- Avoid "flawless skin" (reads as plastic)
- For age, be specific: "late 20s, fine laugh lines, unretouched"
- Avoid global "photoreal" label — it's infra-red to Pro, no effect

### 3.3.4 Reflectance control

If a material should be matte, say matte. If high-gloss, say it. Missing reflectance info produces inconsistent shine behavior across regenerations. Brands that live or die by surface finish (cosmetics, jewelry, premium packaging) should always specify.

## 3.4 Composition

### 3.4.1 Framing vocabulary (use precisely)

- **Extreme close-up** — detail only (an eye, a logo, a texture)
- **Close-up** — head and shoulders, or single product
- **Medium close-up** — upper chest to head
- **Medium shot** — waist up
- **Medium-full** — thigh up
- **Full body** — entire subject
- **Wide** — subject plus significant environment
- **Extreme wide / establishing** — landscape scale, subject small

### 3.4.2 Aspect ratio is declared explicitly

Pro supports 1:1, 3:2, 2:3, 3:4, 4:3, 4:5, 5:4, 9:16, 16:9, 21:9. Always state the ratio. For paid social, the common ones:

- **1:1** — Instagram feed default
- **4:5** — Instagram feed portrait (best real estate)
- **9:16** — Stories, Reels, TikTok
- **16:9** — YouTube, landing pages, banner
- **21:9** — cinematic hero
- **3:4** — Pinterest, print

### 3.4.3 Subject positioning

Explicit beats implicit. "Subject center-framed" or "subject left-third, negative space right" or "subject slightly off-center, golden-ratio right" will be honored. "Well-composed" will not.

### 3.4.4 Foreground/midground/background separation

For scenes with depth, name the three layers explicitly. "Foreground: wildflowers softly blurred. Midground: subject in focus. Background: out-of-focus forest, bokeh highlights." This is far more reliable than "scene with depth."

---

