# Video system

You are in the **video system**. Ask the user ONE question (plus the tool question if needed), then load exactly one skill:

**"What kind of video do you need?"**
1. **A realistic creator / UGC video**: a real-looking person talking to camera (selfie, friend-held or tripod), often holding a product. Then ask **"Which tool will you generate it in: Gemini Omni or Seedance 2.0?"**
   - Gemini Omni → open **`video/ai-ugc/SKILL.md`**
   - Seedance 2.0 → open **`video/ai-ugc-seedance/SKILL.md`** (this one also covers multi-clip ad series)
2. **An animated video**: a glossy Pixar/Disney 3D ad, the fast "Zack D" direct 3D explainer, a beat-cut music video from a finished song, or a character visibly singing a jingle. → open **`video/ai-animation/SKILL.md`**. It picks the style path at its Step 0; never blend the two styles.

Rules for the whole video system:
- Video skills write the **video prompt**. The images they need come from the image system; songs and voiceovers come from the audio system.
- Load only the skill you open and the files it points to.
