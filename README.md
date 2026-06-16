# Likelyfad Prompt System

**In one line:** give it your **script**, your **reference images**, and the **line you want to film**, and it writes a ready-to-paste **AI video prompt** for realistic, creator-style (UGC) video ads — with the performance, emotion, camera, and voice all worked out for you. You paste that prompt into your **Google Gemini Omni** project to generate the video.

**You don't need to know anything about AI video or prompt-writing.** Just follow the steps.

---

## ✅ What it makes right now
- **Realistic UGC talking-head ads** — one real-looking person talking to camera (selfie-style), optionally holding a product. Vertical, short (**4–10 seconds**), for TikTok / Reels / Shorts.
- Works for **any brand or product**.

## 🚫 What it can't do yet (don't ask for these)
- Animated / cartoon / claymation styles
- Any model other than Gemini Omni
- More than one person on screen, or clips longer than 10 seconds
- Need something not on the "can do" list? **Ask the admin** — don't force it, or the result comes out wrong.

---

## 1) Load it into your AI (once, at the start of a session)

This works in any capable AI agent — pick yours:

- **Claude Code** — open a session **in this repo** (`Likelyfad-Prompt-System`, branch `main`); it loads automatically. Then say: *"Use the ai-ugc skill."*
  *(Optional: run `/plugin marketplace add amanpreetsingh1998/Likelyfad-Prompt-System` once to use it in any session without opening the repo.)*
- **OpenAI Codex / Cursor / other coding agents** — open or connect this repo in the agent; it automatically reads **`AGENTS.md`** at the top of the repo and follows it to the skill. Then say: *"Follow the ai-ugc skill in this repo."*
- **ChatGPT / Claude.ai / Gemini (a plain chat, no repo access)** — on GitHub, open **`skills/ai-ugc/SKILL.md`**, copy all of its text into the chat, and say: *"Follow this skill; ask me for any files it references."* When it asks for a referenced file (the chassis, the model file, the style), open that file on GitHub and paste its text in too.
  *(Smoothest with a repo-connected agent like Claude Code or Codex — a plain chat just means you paste the files in yourself.)*

Once it's loaded, do the 3 steps below.

---

## 2) The 3 steps to make a clip

**Step 1 — Give it the full script first.**
Paste your **entire script** (all the hooks + the body). Let it read and understand it — the emotion, the story, and the performance that implies: the **voice/audio**, and the **face, eye, hand, and body movements**, beat by beat. *Don't ask for a prompt yet — this step is just understanding.*

**Step 2 — Give it your reference images and say what each one is.**
Attach and label your three references:
- **First-frame image** — the exact opening shot (the person in their setting). Locks the look, framing, and background.
- **Character set** — the multi-angle photo of the person. Keeps their face and identity consistent as the camera moves.
- **Product image** — a clean photo of the product (e.g. the bottle), so its **label and design don't distort** in the video.

Tell it which image is which and how you want them used.

**Step 3 — Give it the one line you want to film; it writes the prompt.**
Paste the single line/hook for this clip. It must fit **4, 6, 8, or 10 seconds — never longer than 10.** Using everything from Steps 1–2 (the emotion, the voice, the movement plan, and your images), it writes the full Gemini Omni prompt for that line — performance, micro-movements, camera, and voice — built to generate cleanly. **Repeat Step 3 for each line/hook** you want.

---

## 3) Generate it in Gemini Omni
You'll get a **prompt in a grey box**, plus the **clip length** and a **numbered list of the images to use**. Then, in the **Gemini Omni project you already prepared for this video** (with your images ready):
- paste the prompt,
- add the images **in the listed order**,
- generate. ✅

---

## 💡 Example — the Lymphoria video
- **Step 1 (script):** paste the full Lymphoria script (the 3 hooks + body). It maps the emotion + the performance.
- **Step 2 (images):** attach + label —
  1. the **first-frame image** (the woman in her setting, holding the bottle),
  2. her **character set** (the multi-angle reference),
  3. the **Lymphoria bottle** product photo (so the label stays crisp — no distortion).
- **Step 3 (the line):** paste one hook, e.g.:
  > *"Do not buy Lymphoria lymphatic drainage for your cellulite. They said it would help with the dimples on my thighs and how heavy my legs felt, okay? But they did not warn me how fast it would work."*
- **It gives back:** the full ~10-second Omni prompt for that hook, ending with:
  > **Duration:** 10 seconds
  > **Assets to use, in order:** 1) first-frame image · 2) character set · 3) Lymphoria bottle
- **You then:** paste it into your prepared Omni project, add those 3 images in that order, and generate.

---

## ✔️ Do  /  ❌ Don't

**Do**
- Give the **full script first**, then the **images**, then the **line to film** — in that order.
- Keep each line **short** (it must fit 4–10 seconds).
- Always attach all three references (**first-frame, character set, product**) so the face, background, and product label stay locked.
- Paste the prompt it gives you **exactly** as-is.

**Don't**
- ❌ Don't write or rewrite the prompt yourself.
- ❌ Don't ask for styles that aren't built yet (animated, claymation, etc.).
- ❌ Don't try to generate more than 10 seconds in one clip — break long scripts into separate lines.
- ❌ Don't skip the reference images, or the product label / background / face can drift.

---

## 🛠️ If something looks off
- Just say what's wrong in plain words — e.g. `the camera looks too still`, `make it 6 seconds instead`, `she should hold the bottle higher` — and it'll adjust the prompt for you.
- If the **video itself** comes out wrong (background changed, label warped, hands look off), tell the admin — those are known issues we've already tuned the system to avoid, and we can fix them.

---

<sub><b>For maintainers:</b> system internals live in <code>skills/ai-ugc/</code> (entry: <code>SKILL.md</code>); agent instructions in <code>AGENTS.md</code>; research + version history in <code>docs/</code> and <code>CHANGELOG.md</code>. Keep "Omni" out of names — the model is a swappable layer in <code>skills/ai-ugc/references/models/</code>.</sub>
