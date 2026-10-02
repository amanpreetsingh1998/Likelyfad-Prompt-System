# Likelyfad Prompt System 2.0

**In one line:** paste this repo's link into any AI chat, answer a few questions, and it writes ready-to-paste prompts for **images**, **videos** and **audio** for short-form ads: characters, creator videos, Pixar-style animation, brand songs and voiceovers.

**You don't need to know anything about AI prompting.** The system asks you what it needs, one question at a time.

---

## ▶️ How to start (any AI: Claude, ChatGPT, Codex, Claude Code, Cursor, Gemini)

1. Open a new chat in your AI tool.
2. Paste the repo link and one sentence:

   > https://github.com/amanpreetsingh1998/Likelyfad-Prompt-System
   > Read AGENTS.md in this repo and follow it.

3. It asks: **"What do you want to create? 1) An image 2) A video 3) Audio."** Answer, then answer its next questions.
4. You get a prompt in a grey box, plus the settings and the list of images to upload. Paste it into the tool it names and generate.

*Claude Code users: open a session in this repo (it reads `CLAUDE.md` automatically), or run `/plugin marketplace add amanpreetsingh1998/Likelyfad-Prompt-System`.*

---

## 🗂️ The three systems

### 🖼️ Image
| You want | Skill | Goes into |
|---|---|---|
| Characters for a whole script: a cast plan, **character sheets** (5-view full body, or 3-view chest-up), **before/after or week-by-week transformation** sheets, and **location** references. Styles: Pixar simple, Pixar high fidelity, Realistic Movie, UGC iPhone | **`character-casting`** | Seedream 5.0 Pro *or* Nano Banana Pro (it asks which) |
| Any other image: product shots, lifestyle or UGC stills, thumbnails, text-heavy posters and ads, comparison or before/after images, language versions of an ad, infographics, first frames for a video, editing an image | **`nano-banana`** | Nano Banana Pro |

Every character is cast as **a specific, recognisable person** (real face details, real age, real variety) and never a generic AI face. That's the casting theory in `image/character-casting/references/theory.md`.

### 🎥 Video
| You want | Skill | Goes into |
|---|---|---|
| A real-looking person talking to camera, selfie-style, holding your product | **`ai-ugc`** | Google Gemini Omni |
| The same kind of creator video filmed as a selfie, by a friend or on a tripod, including an ad split into several clips | **`ai-ugc-seedance`** | ByteDance Seedance 2.0 |
| An animated ad in the glossy Pixar/Disney look, **or** the fast **"Zack D"** explainer, **or** a music video cut to a finished song, **or** a character singing your jingle | **`ai-animation`** | ByteDance Seedance 2.0 |

### 🎵 Audio
| You want | Skill | Goes into |
|---|---|---|
| A brand song from an ad script (usually 3 hooks + 1 body), including long 5–10 minute songs | **`ai-song`** | Suno v6 (Pro) |
| A voiceover, ad read, narration or dialogue | **`elevenlabs-voice`** | ElevenLabs Eleven v3 |

Everything works for **any brand or product**. Vertical, short-form, for TikTok / Reels / Shorts.

---

## ✔️ Do  /  ❌ Don't

**Do**
- Give the **whole script** when it asks. It needs the full story to plan characters, clips and songs.
- Answer its questions; say "next" to get the next prompt.
- Attach every reference image it asks for, in the order it lists.
- Paste the prompt **exactly** as given.
- Check every generated character against the editor checklist before using it in a video.

**Don't**
- ❌ Don't rewrite the prompt yourself.
- ❌ Don't mix models for one character (e.g. the Before in Seedream and the After in Nano Banana).
- ❌ Don't mix the Pixar and Zack D styles in one video.
- ❌ Don't ask for styles or models that aren't listed. Ask the admin to add them.

---

## 🧪 What's tested and what isn't

Each skill marks its rules by evidence (tested on our renders, from the official docs, or untested). New in 2.0 and **not yet tested on real renders**:
- `character-casting`: Seedream vs Nano Banana, and the transformation flow.
- `nano-banana`: the guide as a skill.
- `elevenlabs-voice`.
- `ai-song` 1.2.0: Suno v6 and the long-song recipe.
- `ai-ugc` 1.0.2: Google's Omni guidance.

If a result comes out wrong, tell the admin what went wrong in plain words. Every fix gets folded back in so it doesn't happen twice.

---

## 🛠️ If something looks off
Say what's wrong in plain words ("the face changed between views", "the song turns to whispering after 4 minutes", "make it 6 seconds") and it will adjust the prompt.

---

<sub><b>For maintainers:</b>
<ul>
<li><b>Entry and menus:</b> <code>AGENTS.md</code> → <code>image/SYSTEM.md</code> · <code>video/SYSTEM.md</code> · <code>audio/SYSTEM.md</code> → one skill's <code>SKILL.md</code>.</li>
<li><b>Model wording</b> lives in each skill's <code>references/models/</code> (the swappable layer). Model names may appear in a skill's own name (allowed since 2026-09-16).</li>
<li><b>Paths:</b> old <code>skills/&lt;name&gt;/</code> paths are signposts; see <code>docs/MOVED.md</code>.</li>
<li><b>History and logs:</b> research and the prompt log are in <code>docs/</code> (humans only); version history is in <code>CHANGELOG.md</code>.</li>
<li><b>Logging rule:</b> log every notable generation in <code>docs/prompt-log.md</code> and fold the lesson into that model's symptom→fix table.</li>
</ul></sub>
