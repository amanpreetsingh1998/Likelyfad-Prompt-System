# Likelyfad Prompt System

**In one line:** give it a short **script** + a couple of **photos**, and it writes you a ready-to-paste **AI video prompt** for realistic, creator-style (UGC) video ads. You paste that prompt into **Google Gemini Omni** to make the video.

**You don't need to know anything about AI video or prompt-writing.** Just follow the steps below.

---

## ✅ What it makes right now
- **Realistic UGC talking-head ads** — one real-looking person talking to the camera (selfie-style), optionally holding a product. Vertical, short (**4–10 seconds**), made for TikTok / Reels / Shorts.
- Works for **any brand or product**.

## 🚫 What it can't do yet (please don't ask for these)
- Animated / cartoon / claymation styles
- Any model other than Gemini Omni
- More than one person on screen, or clips longer than 10 seconds
- Need something that's not on the "can do" list? **Ask the admin** — don't try to force it, or the result will come out wrong.

---

## 🔑 One-time setup
1. Accept the **GitHub invite** to this repo (check your email / GitHub notifications). The repo is private, so you need access.
2. Sign in to your **GitHub account inside Claude Code**.

If you can open this repo on GitHub, you're ready.

---

## ▶️ How to use it — 4 steps (every time)

**1. Open a Claude Code session in this repo** (`Likelyfad-Prompt-System`, branch `main`).

**2. Paste this exact message to start:**
```
Use the ai-ugc skill. I'll give you a script and reference images — produce the ready-to-paste Gemini Omni prompt.
```

**3. Give it two things:**
- **The script** — the exact words the person will say. Keep it short (a few seconds' worth — one or two sentences).
- **The photos** — attach:
  - the **person** (face clearly visible),
  - the **product** (if there is one — a clear shot of the label),
  - the **background / scene** (this can be the same photo as the person).

**4. Copy what it gives you.** You'll get a **prompt in a grey box**, plus the **video length** and a **numbered list of which photos to use**. Then:
- open **Gemini Omni**,
- paste the prompt,
- attach the photos **in the order it listed**,
- generate your video. ✅

That's the whole process.

---

## 📋 What to give it — quick checklist
- [ ] The **spoken line(s)** — short
- [ ] A clear **photo of the person** (face visible)
- [ ] A **photo of the product** (if any)
- [ ] A **photo of the setting** (or reuse the person photo)

Clearer photos = better results.

---

## ✔️ Do  /  ❌ Don't

**Do**
- Use the **starter message** above; just give it the script + photos.
- Keep each spoken line **short** (it's a 4–10 second video).
- Paste the prompt it gives you **exactly** as-is.

**Don't**
- ❌ Don't write or rewrite the prompt yourself, or change its wording.
- ❌ Don't ask for styles that aren't built yet (animated, claymation, etc.).
- ❌ Don't paste a long script into one clip — break it into short lines (or just ask it to split a long script for you).
- ❌ Don't skip the photos — it needs them to lock the person, product, and background.

---

## 💡 Example (so you can see how it goes)

**You give it:**
- Script: `Stop buying collagen that tastes like chalk — this one's actually good, okay? Three weeks in and my skin is unreal.`
- Photos: the woman in her kitchen + the collagen tub.

**It gives back:** a full prompt in a grey box, ending with something like:
> **Duration:** 10 seconds
> **Assets to use, in order:** 1) scene / background photo · 2) the person · 3) the product

**You then:** paste the prompt into Gemini Omni, attach those 3 photos in that order, and generate.

---

## 🛠️ If something looks off
- Just say what's wrong in plain words — e.g. `the camera looks too still`, `make it 6 seconds instead`, or `she should hold the bottle higher` — and it'll adjust the prompt for you.
- If the **video itself** comes out wrong (background changed, product label looks warped, hands look off), tell the admin — those are known issues we've already tuned the system to avoid, and we can fix them.

---

## (Optional) Use it in any session
So you don't have to open this repo each time, install it once in Claude Code:
```
/plugin marketplace add amanpreetsingh1998/Likelyfad-Prompt-System
```
Then just paste the starter message + your script + photos in any session.

---

<sub><b>For maintainers:</b> system internals live in <code>skills/ai-ugc/</code> (entry: <code>SKILL.md</code>); agent instructions in <code>AGENTS.md</code>; research + version history in <code>docs/</code> and <code>CHANGELOG.md</code>. Keep "Omni" out of names — the model is a swappable layer in <code>skills/ai-ugc/references/models/</code>.</sub>
