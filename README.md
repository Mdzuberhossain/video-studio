# video-studio

A Claude Code plugin that makes launch videos, feature drops, walkthroughs and LinkedIn / X / YouTube cuts as code. Claude writes each scene as HTML, HyperFrames renders it to MP4, ElevenLabs makes the voice and music, Whisper times the captions, AntV draws the charts, and Seedance 2.5 and HeyGen Video (via OpenRouter) make the AI clips. Change one line, render again.

## Install

**Claude desktop app:** click **+** next to the prompt box → **Plugins** → **Add marketplace** → enter `Mdzuberhossain/video-studio` → **Add plugin** on video-studio. Restart the app.

**Claude Code in a terminal:**

```
/plugin install video-studio --marketplace Mdzuberhossain/video-studio
```

Answer `y` to add the marketplace, then press Enter.

## Use

Open the **Code** tab, pick a folder for your videos, and ask:

> Make a 30-second launch video for [feature]. Audience: [who]. Platforms: LinkedIn.

The first time, Claude installs what it needs (Node, FFmpeg, Python, Whisper, HyperFrames) and opens Notepad for your keys. Paste your keys, save, and type `done`. It shows you the script first, and the cost before any paid AI clip.

## You need

- An **OpenRouter** key (openrouter.ai/keys) with credit, for AI video clips.
- An **ElevenLabs** key (elevenlabs.io → Profile → API Keys), for voice and music.

Keys are stored only on your computer, in `~/.video-studio/.env`. Never paste them into a chat.

Optional: Blender for 3D shots and Topaz Video for 4K upscaling. Claude skips them if they're missing.
