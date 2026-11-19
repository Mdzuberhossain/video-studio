# Finishing and platform cuts

## Platform versions: re-render instead of cropping

The scenes are HTML, so render each aspect ratio natively. Do not crop a 16:9 master.

| Platform | Size | Notes |
|---|---|---|
| YouTube | 1920×1080 (16:9) | full length, chapters if it runs over 2 minutes |
| LinkedIn | 1080×1350 (4:5) or 1080×1080 | burned-in captions (most viewers watch muted), hook in first 2 s |
| X | 1080×1350 (4:5) or 1920×1080 | under 2:20, burned-in captions |
| Shorts / Reels / TikTok | 1080×1920 (9:16) | under 60 s, keep text out of the bottom 20 % |

For each version, change the composition size, check that layouts reflow (text inside safe areas), shorten the cut where the platform needs it, and render to `out/<video>_<platform>.mp4`.

## 4K upscale (Topaz)

Every final video gets upscaled to 4K with Topaz Video. Render the final at 1920×1080 (or the platform size), then upscale ×2. Topaz Video is a paid desktop app and can't be installed for the user.

- **If Topaz Video is installed,** use the FFmpeg that ships inside it (in the Topaz Video install folder) with its `tvai_up` filter at scale 2. Check the installed version's docs for the model name and the required model-folder environment variables before running. Write the result to `out/<video>_4k.mp4`.
- **If it isn't installed,** say so in one line, render HyperFrames directly at 3840×2160 instead, and carry on. Never block the video on Topaz.

Draft renders are never upscaled. Upscale only the version the user approves.

## Final check before handing over

- Play each output. Check the A/V sync at the first and last VO line.
- `ffprobe out/*.mp4`: confirm the size, duration and an audio stream are present.
- Report the file paths, durations, and anything skipped.
