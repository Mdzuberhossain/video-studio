# AI clips: b-roll, product moments, abstract shots (HeyGen Video via OpenRouter)

Use this for every generated clip **except people shots**, which go to Seedance ([people-shots.md](people-shots.md)). Before reaching for a generated clip, ask whether an HTML scene can show it, because those are free to re-render.

## Cost check first

The user quoted about $0.018/s (Nov 2026). OpenRouter prices vary by resolution and change over time, so read the current rate from `GET https://openrouter.ai/api/v1/videos/models`. Before generating, show the user the shot list with seconds × rate = estimated total and get an OK.

## Generate (async)

Model: `heygen/heygen-video-1`. Read its accepted parameters (duration, resolution, aspect ratio, reference image) from `/api/v1/videos/models`; don't guess field names.

```bash
# 1. submit → 202 with a job id
curl -s -X POST https://openrouter.ai/api/v1/videos \
  -H "Authorization: Bearer $OPENROUTER_API_KEY" -H "Content-Type: application/json" \
  -d '{"model": "heygen/heygen-video-1", "prompt": "<shot prompt>"}'

# 2. poll until status is completed (every ~10 s; stop on failed/expired and report it)
curl -s https://openrouter.ai/api/v1/videos/$JOB_ID -H "Authorization: Bearer $OPENROUTER_API_KEY"

# 3. download
curl -s https://openrouter.ai/api/v1/videos/$JOB_ID/content \
  -H "Authorization: Bearer $OPENROUTER_API_KEY" -o footage/clip_XX.mp4
```

- Prompt for each shot: subject, setting, camera move, lens and framing, lighting, mood, duration. Match the composition's aspect ratio.
- Ask for the shortest duration that covers the scene's VO span from `words.json`. Every extra second is paid for.
- Write the prompt and job ID next to the scene in `script.md`, so the clip can be regenerated or audited.
- Requests fail with a 400 if the OpenRouter key enforces ZDR mode. If that happens, tell the user and don't retry.
