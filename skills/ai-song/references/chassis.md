# Chassis — the song-prompt structure (model-agnostic)

The reusable skeleton for every song package. **Locked** bits are pasted/handled the same every time; **variable** bits change per song. (Suno-specific wording — fields, tags, limits, the identical-body & long-song methods — lives in `models/suno.md`; the sound lives in `styles/<style>.md`.)

## The core principle: format the script, don't write it
The script arrives **finished and written as a song**. Your job is to lay it into the exact shape the model needs and dress it with the right sound — **not** to compose lyrics. So the words are **locked (verbatim)**; what you add is **structure, sound, and settings**.

## Section order (of the delivered package)
1. **Sound (Style field)** *(variable per song, one sound per set)* — genre, BPM, mood, vocal, production. → `styles/<style>.md` + `models/suno.md`.
2. **Words (Lyrics field)** *(locked verbatim, you add only tags/cues/breaks)* — the script sung exactly, inside section tags. → below + `models/suno.md`.
3. **Settings** *(variable)* — Exclude Styles, slider values, Persona, stated BPM + key. → `models/suno.md`.
4. **Variants** *(variable)* — for a 3-hook script, Hook 2 / Hook 3 as swap blocks. → `models/suno.md` (Job A).
5. **Assembly runbook** *(locked method)* — the generate/Replace-Section/Extend/export steps. → `models/suno.md`.
6. **Visual / timing seed** *(variable)* — the hand-off note for the animation skill. → below.

## Locked vs. variable
- **Locked:** the **verbatim words** (never change them); the assembly method; the gap-killing structure rules.
- **Per set (decided once, then reused):** the sound treatment, the Persona, the slider values, the BPM + key.
- **Variable (per song):** which script, the section map, the tags, the visual/timing seed.

## The verbatim rule (how to write Section 2)
The ad script **is** the lyrics. **Never** change, reword, reorder, trim, or pad a word. You add only three things:
- **[Section tags]** — derived from the script's own shape (see below).
- **(Vocal cues)** — sparing performance cues in parentheses or medium-reliability tags (`[Belted]`, `[Whispered]`), only where they serve the delivery.
- **Line breaks** — to phrase the words into singable lines.

Do **not** repeat a line to manufacture a hook/chorus **unless the script already repeats it**. The one allowed spelling change is a **brand-name phonetic respell** (same word, sung-spelling only) — flag it and get the user's OK (→ `models/suno.md`).

## Structure-tagging craft (how to derive Section 2's tags)
1. **Read the whole script first** and derive its **full section map** — however many hooks/verses/choruses it actually contains. The section count is the **script's**, not a fixed number.
2. **For a 3-hooks + 1-body script:** tag **Hook 1** as the opening section (`[Chorus]` — the earworm, opening on vocals, never `[Intro]`), then the **body** as its following sections (`[Verse 1]`, `[Chorus]`, `[Verse 2]`, …). Keep the hook a clean, self-contained section so it can be swapped in-context (Job A).
3. **Keep it continuous** — no `[Bridge]` / `[Instrumental]` gaps in a driving song; end on `[Outro: Cold End]` / `[End]`.
4. **Long script?** Derive the full map first so numbering stays right across Extend chunks (→ `models/suno.md`, Job B).

## The sound-decision step (how to run Workflow step 2)
Read the script, then **propose 2–3 distinct fast, non-rap sonic treatments** — each a different genre + vocal + BPM take on the *same* script (e.g. eurodance anthem vs liquid DnB vs pop-punk). Lead with the **script's own vibe/energy**; use the audience only as a **hint/tie-breaker** if it's evident from the script (map → `styles/<style>.md`). The user picks one; that becomes the set's locked sound (Style string + Persona + sliders + BPM/key). Only vary the *sound* across treatments — **never** the words.

*Philosophy: make it sound like a real song, not a "buy-buy-buy" jingle — real sections, real hook, driven by the script's emotion.*

## The visual / timing seed (how to write Section 6)
End every package with a **short, light** note for the downstream animation skill — not full visual direction, just a clean seam:
- **Hook timing** — where the hook lands and how long it runs.
- **Section beats** — the rough timestamped shape (so scenes can be cut to it).
- **Mood / energy curve** — the feel to match on screen.

Keep it to a few lines. Full visual/scene direction belongs to the animation skill; this is only the hand-off.
