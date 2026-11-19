# video-studio

Make launch videos, feature updates, walkthroughs and LinkedIn / X / YouTube clips just by asking Claude. Claude writes the script, makes the voice-over, music, charts and AI clips, adds timed captions, and renders an MP4. To change something, ask, and Claude renders it again.

Built on HyperFrames (scenes), ElevenLabs (voice and music), Whisper (caption timing), AntV (charts), and Seedance 2.5 and HeyGen Video through OpenRouter (AI clips).

---

## Before you start

You need three things:

1. **The Claude desktop app** on a paid plan: [claude.com/download](https://claude.com/download)
2. **An OpenRouter key** (for AI video clips): go to [openrouter.ai/keys](https://openrouter.ai/keys), click **Create key**, and copy it. Add a few dollars of credit under **Credits**.
3. **An ElevenLabs key** (for voice and music): go to [elevenlabs.io](https://elevenlabs.io), then **Profile → API Keys → Create**, and copy it.

Keep both keys somewhere safe. **Never paste them into a Claude chat.**

---

## Option A: Claude Code (recommended)

This runs on your own computer and is the most reliable way to use the plugin.

### 1. Install the plugin

1. Open the Claude desktop app and click the **Code** tab at the top.
2. Pick any folder (for example, make a new folder called `Videos`).
3. Paste this message and press **Enter**:

   ```
   Install the Claude plugin from https://github.com/Mdzuberhossain/video-studio by running `claude plugin marketplace add Mdzuberhossain/video-studio` and then `claude plugin install video-studio@video-studio`. If the `claude` command isn't found, use `npx -y @anthropic-ai/claude-code` in its place. Then tell me to restart the app.
   ```

4. Click **Allow** when Claude asks.
5. **Fully quit Claude** (Windows: right-click the Claude icon near the clock → **Quit**; Mac: **Claude → Quit**) and open it again.

### 2. Add your keys

1. In the **Code** tab, send:

   ```
   Set up my video-studio API keys and open the file in Notepad.
   ```

2. Claude installs the tools it needs the first time. This takes a few minutes, and if Windows asks "allow changes?", click **Yes**.
3. Notepad opens with two lines. Paste your keys straight after the `=` signs, like this:

   ```
   OPENROUTER_API_KEY=sk-or-v1-...
   ELEVENLABS_API_KEY=sk_...
   ```

4. Press **Ctrl+S** (Mac: **Cmd+S**), close Notepad, and type **done** in Claude.

### 3. Make a video

Send something like:

```
Make a 30-second launch video for [your product]. Audience: [who it's for]. Platform: LinkedIn.
```

Claude shows you the script first and waits for your OK. Before any paid AI clip, it shows you the cost. The finished video is saved in the **out** folder inside the folder you picked.

---

## Option B: Claude Cowork

Cowork works inside a safe sandbox on your computer. The steps are almost the same; only the install and the keys differ.

### 1. Install the plugin

1. Open the Claude desktop app and click **Plugins** in the left sidebar.
2. Click **+** (or **Add**), then **Add marketplace**.
3. Paste `Mdzuberhossain/video-studio` and confirm.
4. Find **video-studio** in the list and click **Install**.
5. Fully quit Claude and open it again.

### 2. Add your keys

1. Start a **Cowork** task and **choose a folder** for your videos (for example `Videos`).
2. Send:

   ```
   Set up my video-studio API keys.
   ```

3. Claude creates a file called `video-studio.env` in that folder.
4. Open the folder in File Explorer (Mac: Finder). Right-click `video-studio.env` → **Open with → Notepad** (Mac: TextEdit).
5. Paste your keys after the `=` signs, save, close it, and type **done** in Claude.

**Don't share or upload that folder while `video-studio.env` is in it.** It holds your keys.

### 3. Make a video

Same as Option A: ask for the video you want. If Claude says a download is blocked, turn on network access for Cowork in the desktop app's **Settings**, then ask again.

---

## What it costs

- **Free:** scenes, text, charts, captions, and re-rendering as many times as you like.
- **ElevenLabs:** voice and music use your ElevenLabs plan.
- **OpenRouter, per second of AI video:** HeyGen Video from about $0.01/s. Seedance 2.5 (people on camera) from about $0.10/s.

Claude always shows you the total and waits for your OK before spending money.

## Problems?

| What you see | What to do |
|---|---|
| `/video-studio` doesn't appear | Fully quit Claude and open it again. |
| "Key is missing" | Repeat step 2 (Add your keys). |
| A Windows "allow changes?" pop-up | Click **Yes**. Claude is installing a tool it needs. |
| A tool still "not found" after installing | Fully quit Claude and open it again. |

Optional extras: install **Blender** for 3D shots and **Topaz Video** for 4K upscaling. Claude skips them if they're missing.

License: MIT
