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

## 4K upscale (Topaz, optional)

Only for the master or YouTube cut. Use Topaz Video (the desktop app's CLI or the Topaz API, whichever the user has). If it is not available, skip this step and say so. Rendering HyperFrames at 3840×2160 directly is often cleaner than upscaling anyway, so try that first.

## Final check before handing over

- Play each output. Check the A/V sync at the first and last VO line.
- `ffprobe out/*.mp4`: confirm the size, duration and an audio stream are present.
- Report the file paths, durations, and anything skipped.
