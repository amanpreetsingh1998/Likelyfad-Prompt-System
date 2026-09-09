# Likelyfad Prompt System

**In one line:** give it your **script** and your **reference images**, and it writes ready-to-paste **AI prompts** — for realistic creator-style video ads, for animated video ads and explainers, and for brand songs. You paste what it gives you into the tool it names and generate.

**You don't need to know anything about AI prompting.** Pick the skill that matches your job and follow its steps.

---

## ✅ What it makes right now

| You want | Skill | Goes into |
|---|---|---|
| A real-looking person talking to camera, selfie-style, holding your product | **`ai-ugc`** | Google Gemini Omni |
| An animated ad, glossy Pixar/Disney look, a character telling your product story | **`ai-animation`** (Pixar path) | ByteDance Seedance 2.0 |
| A fast explainer — semi-realistic 3D, hard cuts, a new fact every second, voiceover on top. **The "Zack D" style** | **`ai-animation`** (explainer path) | ByteDance Seedance 2.0 |
| A music video cut to the beat of a song you already have | **`ai-animation`** (music-video mode) | ByteDance Seedance 2.0 |
| A character who visibly sings your jingle | **`ai-animation`** (singing mode) | ByteDance Seedance 2.0 |
| A brand song built from an ad script, usually 3 hooks + 1 body | **`ai-song`** | Suno v5.5 (Pro) |

Everything works for **any brand or product**. Vertical, short-form, for TikTok / Reels / Shorts.

## 🚫 What it can't do yet (don't force it)
- Any model other than the ones listed above. The model is a swappable layer, so ask the admin to add one.
- Animation styles beyond Pixar/Disney 3D and the direct 3D explainer.
- Realistic UGC clips longer than 10 seconds, or with more than one person on screen.
- Writing your script, choosing your marketing angle, or making your images. Those arrive already done.

Need something not on the list? **Ask the admin.** Forcing it produces a bad prompt.

---

## 1) Load it into your AI (once, at the start of a session)

- **Claude Code** — open a session **in this repo** and it loads automatically. Then say which job you want, e.g. *"Use the ai-ugc skill."*
  *(Optional: run `/plugin marketplace add amanpreetsingh1998/Likelyfad-Prompt-System` once to use it in any session without opening the repo.)*
- **OpenAI Codex / Cursor / other coding agents** — open or connect this repo; the agent reads **`AGENTS.md`** automatically and follows it to the right skill. Then say: *"Follow the ai-animation skill in this repo."*
- **ChatGPT / Claude.ai / Gemini (a plain chat, no repo access)** — on GitHub, open the skill's `SKILL.md`, copy all of its text into the chat, and say: *"Follow this skill; ask me for any files it references."* When it asks for a referenced file, open that file on GitHub and paste it in too.

---

## 2) The steps, per skill

### 🎥 `ai-ugc` — realistic talking-head ads
**Step 1 — give it the full script first.** Paste your entire script, all hooks plus body. Let it read the emotion and the performance that implies. Don't ask for a prompt yet.

**Step 2 — give it your reference images and label each one.**
- **First-frame image** — the exact opening shot. Locks look, framing, background.
- **Character set** — the multi-angle photo. Keeps the face consistent as the camera moves.
- **Product image** — a clean product photo so the label doesn't distort.

**Step 3 — give it the one line you want to film.** It must fit **4, 6, 8, or 10 seconds, never longer than 10.** You get the full prompt for that line. Repeat for each line.

### 🎬 `ai-animation` — animated ads and explainers
**Step 1 — say which style you want.** This matters more than anything else. **Pixar/Disney** is the glossy cartoon-mascot look. The **"Zack D" style** is the fast semi-realistic explainer with hard cuts and narration added afterwards. They are separate systems and must never be blended, so the skill will ask if it isn't clear.

**Step 2 — hand over the finished script or narration, plus your story context.** It will ask whether anything must **never** appear. Answer honestly; that list is enforced for the whole project.

**Step 3 — hand over your already-made images**, labelled: the character, the scene or start frame, the product.

**Step 4 — say what you want generated.** You get a complete prompt per clip, plus the clip length and the numbered asset list.

**For a music video:** hand over the finished song, its **SRT timestamped lyrics**, the BPM, and the story. You get one prompt per segment plus an edit sheet. The visuals generate silent and you lay the song over them in the edit.

### 🎵 `ai-song` — a brand song from an ad script
**Step 1 — paste the whole script** and confirm which lines are the 3 hooks and which are the body.

**Step 2 — pick the sound.** It proposes two or three fast, non-rap treatments. You choose one for the whole set.

**Step 3 — you get the package:** the Style field, the Lyrics field with your words **verbatim**, the settings, the hook variants, and a step-by-step assembly runbook.

**Your words are never changed.** The skill only adds section tags, vocal cues, and line breaks. The one exception is respelling a brand name so Suno pronounces it right, and it will always flag that and ask.

---

## 3) Generate it
You'll get a **prompt in a grey box**, plus the **length** and a **numbered list of images to use**. In the tool the skill named, paste the prompt, add the images **in the listed order**, and generate. ✅

---

## ✔️ Do  /  ❌ Don't

**Do**
- Give the **full script first**, then the **images**, then the specific thing you want made.
- Say which **animation style** you want up front.
- Attach every reference the skill asks for, so faces, backgrounds, and product labels stay locked.
- Paste the prompt it gives you **exactly** as-is.
- Tell it up front if something must **never** appear in the visuals.

**Don't**
- ❌ Don't write or rewrite the prompt yourself.
- ❌ Don't mix the Pixar and explainer styles in one job.
- ❌ Don't ask for styles or models that aren't built yet.
- ❌ Don't exceed 10 seconds in one realistic UGC clip.
- ❌ Don't skip the reference images.

---

## 🛠️ If something looks off
- Say what's wrong in plain words, e.g. `the camera looks too still`, `make it 6 seconds`, `the cuts are too slow` — and it will adjust the prompt.
- If the **generated video or song** comes out wrong (background changed, label warped, hands look off, dead air before the vocals), tell the admin. Most of these are known issues already tuned for, and each new one gets folded back into the system so it doesn't happen twice.

---

<sub><b>For maintainers:</b> internals live in <code>skills/&lt;skill&gt;/</code> (entry: <code>SKILL.md</code>); agent instructions in <code>AGENTS.md</code>; research and version history in <code>docs/</code> and <code>CHANGELOG.md</code>. Keep model names out of structure and naming — each model is a swappable layer under <code>skills/&lt;skill&gt;/references/models/</code>. Log every notable generation in <code>docs/prompt-log.md</code> and fold the lesson into that model's symptom→fix table.</sub>
