# Google Omni — UGC Talking-Head Prompt System (Working Notes, v1)

- **Status:** Working capture of the system as built so far. NOT the final SOP (SOP to be formalized later).
- **Engine:** Google Omni
- **Use case:** Realistic UGC talking-head ad clips (e.g., Lymphoria), assembled from short generations.
- **Last updated:** 2026-06-16
- **Push status:** Local only — not pushed (per standing instruction). Pushing handled separately when greenlit.

---

## Hard specs

- **Duration = four fixed buckets only: 4s / 6s / 8s / 10s.** Pick ONE per clip; Omni hard-caps at the bucket length (overlong dialogue gets chopped off the end).
- **Dialogue must be sized to the bucket** (fast TikTok pace, with headroom so nothing is cut off):
  - 4s ≈ 12–16 words
  - 6s ≈ 20–26 words
  - 8s ≈ 28–34 words
  - 10s ≈ 36–44 words
- **One continuous take per generation.** No internal cuts.
- **Vertical 9:16.**
- **Jump-cuts / angle-shifts are done in the EDIT** (separate generations stitched), never inside one prompt.
- **Hard-cut-inside-the-generation concept = deferred to a future v2.** This version stays single continuous take.

## The 3-reference system

- **`@image1`** — scene + background + left-right layout + framing + wardrobe (the locked starting look).
- **`@charecterset`** — identity/likeness consistency across angles (face, hair, body). NOT its grey studio background.
- **`@lymphoriabottle`** — exact bottle + crisp label/text lock.
- **Hardest lock available:** set `@image1` as the **start/first frame** when Omni allows it.

## The chassis — 11 sections, fixed order

1. Format & Duration
2. Quality / Fidelity Lock — *locked*
3. Reference / Identity — *locked structure, swap subject details*
4. Scene — *locked structure (background lock), swap setting*
5. Camera — *locked (handheld)*
6. Performance & Micro-Movement — *variable per line*
7. Voice — *locked (verbatim block below)*
8. Dialogue — *variable per clip*
9. Audio / Environment — *locked*
10. Style — *locked*
11. Negative Constraints — *locked*

**Locked = paste verbatim every clip. Variable = the Dialogue line + the per-line performance beats.**

## The locked Voice block (verbatim, every clip)

> Warm, natural, everyday-woman American voice with a light, casual Southern lilt — real and slightly textured, never polished or announcer-like. Fast-paced TikTok-style delivery: energetic, quick, and run-on, like she's excitedly rattling off her story to her followers, not calm or composed. She talks fast and casual with natural momentum and candid emphasis, while still staying clear and easy to understand.

## The 6 hard-won rules (gotchas → fixes)

1. **Handheld shake** — foreground it as the camera's primary behavior; kill hedging words ("subtle/tiny"); tie it to her hand + breathing; never let the still reference photo cue "hold still."
2. **Background** — *lock* to `@image1` ("do not recreate/redesign"). The phrase "consistent with" makes Omni reinvent the background every generation.
3. **No mirroring** — forbid horizontal flip/reverse; pin the bottle hand AND the bare shoulder to `@image1`'s side (flipping was swapping the hand).
4. **Bottle** — one single hand, same side, never switches; label crisp via `@lymphoriabottle`.
5. **Voice** — identical block on every clip for consistent output.
6. **First frame** — use `@image1` as start frame when possible (physically prevents drift/mirror).

## Output format (every delivery)

- The prompt goes in a **code block — only the prompt** inside it.
- **After** the code block: **(a) Duration** (exact bucket) and **(b) Assets to use, in order.**

---

## Canonical example — current working prompt (Hook 3, 10s)

```
Create a vertical 9:16 realistic UGC video, about 10 seconds long, filmed as one continuous handheld iPhone selfie take with constant, natural camera shake the whole time. It should feel like a real woman holding her phone in her own hand and filming herself talking fast outdoors.

Quality / Fidelity Lock: Use the exact same lighting, texture, and iPhone image quality as @image1. Do not sharpen the footage. Do not enhance skin texture. Do not apply any AI beauty filter, skin smoothing, HDR effect, cinematic polish, artificial clarity, or stylized color grade. Keep the video raw, organic, and true to @image1, with the same warm natural daylight, sunlit green foliage, realistic exposure, visible freckles and natural skin texture, and authentic outdoor smartphone look.

Reference / Identity: Use @image1 as the exact reference for the scene, background, wardrobe, and composition — preserve its background and left-right layout exactly as shown and do not recreate, redesign, mirror, or flip it. Use @charecterset as the identity and consistency reference for the woman. Preserve her exact likeness: fair freckled skin with natural texture and fine lines, green/hazel eyes, auburn/reddish wavy shoulder-length hair, her real facial structure and age, and her warm, relatable look. Use @charecterset only to keep her face, hair, and body accurate — do not import its plain grey studio background. Keep her in the same white off-the-shoulder eyelet top as @image1, with the bare shoulder on the same side as @image1. Use @lymphoriabottle as the exact reference for the bottle in her hand: match the green-and-cream "LYMPHORIA lymphatic drainage" label, its layout, colors, and all text exactly, and keep it crisp and readable at all times. The bottle label and text must never warp, morph, melt, stretch, or distort.

Scene: Keep the exact same background as @image1 — a dense, sunlit green leafy hedge and foliage directly behind her. Do not recreate, redesign, or change the background; keep it identical and stable throughout the entire clip. She is standing outdoors in front of it, holding the Lymphoria dropper bottle, casually filming a selfie video on her phone. Do not add any people, roads, paths, or pavement — just her and the green background exactly as in @image1.

Camera: This is a handheld iPhone selfie video — she holds the phone in her own hand at arm's length, so the camera is moving the entire time. Throughout the whole clip the frame clearly and continuously bobs, sways, and drifts with natural handheld motion, gently wobbling and re-adjusting the way a real phone moves when someone films themselves talking, driven by her hand, her breathing, and small body shifts. The camera is never on a tripod, never stabilized, and never perfectly still — there is always live, visible handheld movement. Vertical 9:16, eye-level, medium close-up with her head, shoulders, and the bottle near her chest visible, with the bottle on the same side of the frame as @image1. Use @image1 only for framing and identity, not as a cue to hold the camera still. One continuous take. The only camera motion is this natural handheld shake — no deliberate zooms, pans, whip pans, cinematic moves, or cuts.

Performance & Micro-Movement: She talks fast and candid, like a real TikTok creator rattling off a story — animated and energetic, never stiff or staged. Throughout: natural uneven blinking, continuous subtle breathing movement in her chest and shoulders, small natural weight shifts and live head movement, and constant believable facial micro-expressions. She holds the bottle exactly as in @image1 — in the same single hand, on the same side of the frame, near her chest, with the label facing the camera — and keeps it in that same hand for the entire clip; the bottle never switches hands or sides. Her wrist stays relaxed and naturally mobile, never rigid. Only her other, free hand does any gesturing. As she says "Do not buy," she gives a mock-serious warning look with brows slightly pulled together, direct eye contact with the lens, and a small assertive head dip, lifting and lightly featuring the bottle on "Lymphoria." On "they said it would help," her eyebrows lift into relatable venting energy and her free hand gestures vaguely down toward her thighs and legs, with a quick head tilt and eyebrow flash on "okay?" On "but they did not warn me how fast it would work," her eyebrows raise high with a slight head pull-back, her eyes widen, she holds the look with fewer blinks, and a small amused smirk creeps in with a tiny "can you believe it" beat from her free hand.

Voice: Warm, natural, everyday-woman American voice with a light, casual Southern lilt — real and slightly textured, never polished or announcer-like. Fast-paced TikTok-style delivery: energetic, quick, and run-on, like she's excitedly rattling off her story to her followers, not calm or composed. She talks fast and casual with natural momentum and candid emphasis, while still staying clear and easy to understand.

Dialogue: She speaks directly to the camera with accurate lip sync at a fast, natural, conversational TikTok pace, saying exactly: "Do not buy Lymphoria lymphatic drainage for cellulite. They said it would help with my thighs and how heavy my legs felt by evening, okay? But they did not warn me how fast it would work."

Audio / Environment Sound: Realistic iPhone-recorded outdoor audio — soft natural ambience, light breeze, faint distant birds, a gentle rustle of leaves, and open-air spaciousness. Her voice is close and real to the phone microphone, not studio-polished. Avoid traffic noise, indoor room tone, crowd noise, music, fake cinematic sound design, or clean podcast-style audio.

Style: Authentic TikTok/Reels UGC. Raw handheld smartphone selfie footage with natural iPhone camera shake. Natural skin texture with visible freckles. Slightly imperfect, candid realism. A real woman energetically telling her followers about a product outdoors in natural daylight.

Negative Constraints: No text overlays. No captions. No subtitles. No logos other than the existing label on the bottle. No VFX. No 3D. No cartoon. No beauty filter. No skin smoothing. No face morphing. No identity drift. No flicker. No warped, melted, or distorted bottle label or text. No warped hands, no extra or missing fingers, no deformed bottle. The bottle must stay in the same single hand and on the same side of the frame as @image1 for the entire clip; it must never switch hands or jump to the other side. Do not mirror, flip, or horizontally reverse the shot; keep the same left-right layout as @image1, including the bare shoulder on the same side. Do not recreate, redesign, regenerate, replace, or alter the background; keep the exact green foliage, hedge, layout, depth, and composition from @image1 identical and stable for the entire clip; the background must not change. Do not add any people, roads, paths, or pavement. Do not change her outfit, hair, skin, freckles, or the bottle. Do not use the plain grey studio background from @charecterset. Do not add any deliberate camera zoom, pan, whip pan, or cut. Do not make the camera tripod-static, stabilized, locked-off, smooth, or perfectly still — natural handheld iPhone camera shake must stay visible for the entire clip.
```

## The 3 hook dialogue lines (10s bucket)

- **Hook 1:** "Do not buy Lymphoria lymphatic drainage for your cellulite. They said it would help with the dimples on my thighs and how heavy my legs felt, okay? But they did not warn me how fast it would work."
- **Hook 2:** "Do not buy Lymphoria lymphatic drainage for dimpled thighs. They said it would help with my cellulite and my puffy legs, okay? But they did not warn me how fast it would work."
- **Hook 3:** "Do not buy Lymphoria lymphatic drainage for cellulite. They said it would help with my thighs and how heavy my legs felt by evening, okay? But they did not warn me how fast it would work."

## Open items / next

- Body segmentation into 4/6/8/10s buckets (each segment sized to a bucket).
- Decide which body lines are said to camera vs. voiced over before/after B-roll inserts.
- Hard-cut v2 (internal hard cut concept) — test separately.
- Deep research on Omni prompting tips → fold credible findings back into this system.
- Formalize this into the SOP (with QA checklist + troubleshooting table).
