# Google Omni — Master Prompt (Template Default)

- **Engine:** Google Omni
- **Output:** 8-second vertical 9:16 realistic UGC video
- **Role:** Fundamental / master template — the default for every Google Omni generation
- **Version:** v1.0
- **Last updated:** 2026-06-16

This is the fundamental prompt for all Google Omni video content. The block below is the
locked starting point. Per video, swap only the **Variable Slots**; never touch the
**Locked Sections** unless new intel says otherwise. As more info comes in, update the
template and record the change in the Changelog at the bottom.

---

## How to use

1. Upload the reference photo and refer to it in the prompt as `@image1`.
2. Replace the **Dialogue** line with the new script.
3. Update the **Variable Slots** (subject, scene, reveal/punchline, voice, end-pan target) to match the new photo + idea.
4. Leave the **Locked Sections** exactly as written (Quality / Fidelity Lock, camera discipline, audio realism, Style, Negative Constraints).
5. Paste the **Master Template** block into Google Omni.

---

## Master Template (paste-ready — verbatim default)

```
Create an 8-second vertical 9:16 realistic UGC video.

Quality / Fidelity Lock: Use the exact same lighting, texture, and iPhone image quality as the reference image. Do not sharpen the footage. Do not enhance skin texture. Do not apply any AI beauty filter, skin smoothing, HDR effect, cinematic polish, artificial clarity, or stylized color grade. Keep the video raw, organic, and true to the reference image, with the same warm golden-hour lighting, natural softness, realistic exposure, imperfect smartphone texture, and authentic beach atmosphere.

Reference: Use @image1 as the exact identity and scene reference for the older surfer man. Preserve his facial structure, skin tone, curly gray hair, facial lines, sunglasses, tattoos, lean surfer build, age, and overall likeness exactly. Keep him shirtless, wearing olive/green shorts, seated in the same wooden beach chair with relaxed older-surfer energy. Preserve the same rugged beach look and overall realism from the reference.

Scene: Sandy golden-hour beach. Keep the environment consistent with @image1: beach sand, soft sunset light, black Jeep behind him, surfboard beside him, and subtle ocean/beach background. The setting should feel rugged, coastal, casual, and authentic. Out in the water, about 300–400 feet from shore, there is a massive ultra-luxury superyacht anchored offshore. It should feel like an absurdly expensive 100-million-dollar yacht: very large, striking, and clearly luxurious, but still realistically distant in the background until the camera pans to it.

Camera: Static iPhone perspective at first, vertical 9:16, eye-level medium shot. Match the framing closely to @image1: seated pose, upper body, crossed legs, chair, and beach setting visible. One continuous take. Locked-off phone camera feel during the main line, with only very subtle natural micro-movement. No cuts, no zooms, no whip pans, and no cinematic movement during the first part of the shot.

Ending Camera Beat: Immediately after he says the line, the camera naturally pans away from him toward the ocean, like the filmer is following his comment and revealing what he is talking about. The pan should feel like a real iPhone operator casually turning the phone, not a polished cinematic move. The camera lands on a huge ultra-luxury yacht sitting 300–400 feet out from shore in the water. Hold on the yacht briefly at the end so the joke lands. The yacht should look massive, expensive, and unmistakably high-end even at that distance.

Performance / Action: The surfer stays seated in the chair, relaxed and casual. He looks toward the camera and delivers the line with a laid-back, matter-of-fact surfer attitude, like he is casually mentioning something ridiculous. His expression should feel amused and cool, not overly acted. After he says the line, he can subtly glance or gesture toward the water as the camera pans away to reveal the yacht. Natural blinking, subtle head movement, and believable mouth movement. The overall performance should feel candid and authentic.

Voice: Give him a rough, gravelly older-surfer voice. His voice should sound sun-weathered, raspy, slightly low, lived-in, and a little gritty, while still staying clear and understandable. Delivery should feel calm, casual, amused, and unpolished, not acted or announcer-like.

Dialogue: He says exactly, with accurate lip sync and natural pacing: "I gotta get back to my boat."

Timing / Performance Beat: He delivers: "I gotta get back to my boat." Right after the line, the camera naturally pans away from him toward the water and reveals the enormous yacht offshore.

Audio / Environment Sound: Audio should sound like realistic iPhone-recorded beach audio. Include soft ocean waves in the distance, light coastal breeze, subtle open-air spaciousness, faint sand/beach ambience, and natural outdoor sound. His voice should sound close and real to the phone microphone, not studio-polished. As the camera pans toward the ocean, the ambient beach and water sound should remain consistent and natural. Avoid city noise, traffic, indoor room tone, crowd noise, fake cinematic sound design, or overly clean podcast-style audio.

Style: Authentic TikTok/Reels UGC. Raw smartphone footage. Natural skin texture. Slightly imperfect realism. Believable candid beach moment with a funny luxury reveal at the end.

Negative Constraints: No text overlays. No captions. No subtitles. No logos. No VFX. No 3D. No cartoon. No beauty filter. No face morphing. No identity drift. No flicker. No jitter. No warped hands. No extra fingers. Do not change his outfit, sunglasses, tattoos, chair, Jeep, surfboard, or overall beach layout. Avoid excessive camera movement except for the natural end pan toward the water to reveal the yacht.
```

---

## Variable Slots (change per video)

These are the only parts that change when you send a new photo + script. Everything else stays locked.

| Slot | Default (surfer / yacht) | Swap with |
|---|---|---|
| **Subject identity** | older surfer man — facial structure, skin tone, curly gray hair, facial lines, sunglasses, tattoos, lean surfer build, shirtless, olive/green shorts, wooden beach chair | the person + defining features pulled from the new `@image1` |
| **Scene / environment** | sandy golden-hour beach, black Jeep behind, surfboard beside, soft sunset light, ocean background | the new setting + key background objects in `@image1` |
| **Absurd-luxury reveal** | massive $100M ultra-luxury superyacht, 300–400 ft offshore | the new punchline visual the camera reveals at the end |
| **Dialogue (script)** | "I gotta get back to my boat." | the new spoken line (keep it short — ~8s of footage) |
| **Voice character** | rough, gravelly, sun-weathered, raspy older-surfer voice | a voice that matches the new subject's age/look/energy |
| **End-pan target** | camera pans to the yacht and holds for the joke | whatever the new reveal is (the camera lands + holds on it) |

---

## Locked Sections (do not change without new intel)

These carry the realism and the UGC feel. Keep them identical across every video.

- **Quality / Fidelity Lock** — raw iPhone look; no sharpening, beautify, skin smoothing, HDR, cinematic polish, artificial clarity, or color grade.
- **Camera discipline** — static + one continuous take, subtle natural micro-movement only, no cuts/zooms/whip pans; the single natural end pan is the only deliberate move.
- **Audio realism** — iPhone-recorded outdoor sound; voice close to the phone mic; no city/traffic/indoor/crowd/studio/podcast tone or fake cinematic sound design.
- **Style** — authentic TikTok/Reels UGC, natural skin texture, slightly imperfect realism, candid moment with the reveal landing the joke.
- **Negative Constraints** — full list as written (no text/captions/subtitles/logos/VFX/3D/cartoon, no beauty filter, no face morphing, no identity drift, no flicker/jitter, no warped hands/extra fingers, and no changing the subject's locked props/outfit/layout).

---

## Changelog / Intel Log

- **v1.0 (2026-06-16):** Established the master template from the surfer / $100M-yacht default. Preserved the prompt verbatim as a paste-ready block and wrapped it with Variable Slots (swap per video) and Locked Sections (keep constant). Future intel/adjustments get logged here.
