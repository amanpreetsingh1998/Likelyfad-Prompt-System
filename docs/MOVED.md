# Moved files: Likelyfad Prompt System 2.0 (October 2026)

The repo is now organised into three systems. **Start from `AGENTS.md`**: it asks what you want to create (image, video or audio) and loads only the right skill.

| Old path (before 2.0) | New path |
|---|---|
| `skills/ai-ugc/` | `video/ai-ugc/` |
| `skills/ai-ugc-seedance/` | `video/ai-ugc-seedance/` |
| `skills/ai-animation/` | `video/ai-animation/` |
| `skills/ai-song/` | `audio/ai-song/` |
| — (new) | `image/nano-banana/` |
| — (new) | `image/character-casting/` |
| — (new) | `audio/elevenlabs-voice/` |

The old `skills/<name>/SKILL.md` files are short signposts that point here. They will be removed in a later release. Internal file names inside each skill did not change; only the top folder moved.
