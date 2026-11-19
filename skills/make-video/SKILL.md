---
name: make-video
description: Produce a finished video as code — product launch, feature drop, walkthrough, onboarding, "what's new" update, or weekly social content cut for LinkedIn, X and YouTube. Scenes are HTML rendered by HyperFrames; voice and music from ElevenLabs; Whisper word timings drive captions and cuts; AntV charts, diagrams and infographics; optional Seedance people shots, HeyGen Video (OpenRouter) b-roll clips, Blender 3D, Topaz 4K upscale. Use for "make a video", "launch video", "feature video", "product walkthrough video", "cut this for LinkedIn/X/YouTube", or "update the video".
---

# Make a video

A video is a project folder. Every change is a file edit plus a re-render. Never hand-edit rendered output.

## Project layout

```
<video-name>/
  brief.md          # audience, goal, length, platforms, CTA
  script.md         # numbered scenes: VO line, on-screen text, visual
  audio/            # vo_XX.mp3, music.mp3, words.json
  footage/          # Seedance clips, Blender renders, screen recordings
  <hyperframes project files>
  out/              # renders, never edited by hand
```

## Setup (do this yourself; never ask the user to run commands)

This plugin runs in Claude Code (the desktop app's Code tab or a terminal) and in Cowork. At the start of each session, check for `node` (22+), `ffmpeg`, Whisper (`python -m whisper --help`) and the HyperFrames skills. Always run Whisper as `python -m whisper`, which works even when Windows has not added `whisper` to PATH yet. Install anything missing yourself:

- HyperFrames skills, once for all projects: `npx skills add heygen-com/hyperframes -g`
- Python 3.12 if `python` is missing: `winget install Python.Python.3.12` on Windows, `brew install python` on macOS
- Whisper: `python -m pip install -U openai-whisper`. The first transcription downloads the speech model, about 460 MB.
- FFmpeg: `winget install Gyan.FFmpeg` on Windows, `brew install ffmpeg` on macOS, `sudo apt-get install -y ffmpeg` on Linux (Cowork)
- Node 22+: `winget install OpenJS.NodeJS.LTS` on Windows, `brew install node` on macOS, and on Linux the NodeSource setup or `npx -y node@22`

Tell the user in one line what you installed. In Cowork, if a download is blocked, tell the user to allow network access for Cowork in the desktop app's settings and try again. If a new install isn't found on PATH, tell them to fully quit and reopen the desktop app.

## Pipeline

Run the stages in order. Skip optional ones the brief does not need, and say which you skipped.

1. **Brief.** Read `brief.md`. If it is missing, ask only for what you cannot infer: audience, goal, length, target platforms, CTA. Write it.
2. **Script.** Write `script.md`: one row per scene with VO line, on-screen text and visual. Spoken pace is about 2.5 words a second, so check the total against the target length. Get the user's OK on the script before spending money on generation.
3. **Scaffold.** `npx hyperframes init <video-name>` (needs Node 22+ and FFmpeg). Follow the HyperFrames skills for composition syntax, linting and preview. Do not guess the syntax.
4. **Voice and music.** See [references/audio.md](references/audio.md).
5. **Word timings.** See [references/timing.md](references/timing.md). Scene starts, caption words and hard cuts come from `audio/words.json`, never from estimates.
6. **Generated clips (optional).** For people shots, use Seedance: [references/people-shots.md](references/people-shots.md). Every other AI clip (b-roll, product moments, abstract shots) uses HeyGen Video via OpenRouter: [references/ai-clips.md](references/ai-clips.md).
7. **3D shots (optional).** Only when a shot truly needs real 3D. Render in the background, `blender -b scene.blend -o //../footage/shot_####.png -a`, then place the frames or the encoded clip as video in a scene.
8. **Scenes.** One HTML scene per script row. Time each scene and caption from `words.json`. Use AntV for charts, diagrams and infographics: [references/graphics.md](references/graphics.md). Use the brand's real fonts, colours and product screenshots from the repo when they exist.
9. **Preview, then render.** Run `npx hyperframes preview`, look at the result, and fix what is wrong before the final `npx hyperframes render`. Use draft quality while you iterate.
10. **Finish and cut.** See [references/finishing.md](references/finishing.md) for the 4K upscale and per-platform versions.

## Updating an existing video

Change the smallest file that fixes it: a VO line means regenerating that one `vo_XX.mp3` and re-running timings; a UI change means swapping the screenshot or editing the scene. Then re-render. Do not regenerate assets that did not change, because generation costs money.

## Keys

This skill uses two keys: `ELEVENLABS_API_KEY` for voice and music, and `OPENROUTER_API_KEY` for every generated clip (Seedance and HeyGen). They live in a key file, which plugin updates never touch. Variables already set in the environment also work.

- **Claude Code:** `~/.video-studio/.env`
- **Cowork,** or anywhere Notepad can't be opened: `video-studio.env` in the folder the user picked. Cowork's sandbox is reset between sessions, so the key file must live in the user's folder.

Load whichever exists in the same Bash command that makes each API call:

```bash
for f in "$HOME/.video-studio/.env" "./video-studio.env"; do [ -f "$f" ] && { set -a; . "$f"; set +a; }; done; curl ...
```

**If a key is missing,** set up the file for the user. The user should never need a terminal:

1. If the file doesn't exist, create it at the right location from the list above with exactly these lines:
   ```
   # Paste your keys after the = sign. No quotes, no spaces. Then save and close.
   OPENROUTER_API_KEY=
   ELEVENLABS_API_KEY=
   ```
2. Open it for them: `notepad "$HOME/.video-studio/.env"` on Windows, `open -e ~/.video-studio/.env` on macOS. In Cowork you can't open apps, so tell them: "Open your folder in File Explorer, right-click `video-studio.env` → Open with → Notepad."
3. Tell them: "Paste your keys after the = signs, save, close Notepad, then tell me 'done'." In Cowork, also warn them not to share or upload that folder while the key file is in it. Keys come from openrouter.ai/keys and elevenlabs.io → Profile → API Keys.

Rules:
- Never print, `cat`, read or echo the key file or the keys. Only source it. To check a key is filled in without showing it, use `grep -c '^OPENROUTER_API_KEY=.' "$f"`.
- Never ask for keys in chat, and never copy them into project files, scripts or logs.
