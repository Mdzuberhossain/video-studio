# People shots (Seedance 2.5 via OpenRouter)

Use this only when the brief needs on-camera people. These are the most expensive clips: Seedance 2.5 costs about $0.10/s at 480p and more at higher resolutions. Read the live rate from `GET https://openrouter.ai/api/v1/videos/models`. Show the user the shot list with seconds × rate = estimated total and get an OK before generating.

## Generate

Use the same async OpenRouter flow as [ai-clips.md](ai-clips.md) (submit, then poll, then download), with model `bytedance/seedance-2.5` and `OPENROUTER_API_KEY`. Read its accepted parameters from `/api/v1/videos/models` and don't guess field names. The listing says it supports 4–30 s clips, aspect ratios from 9:16 to 21:9, first- and last-frame images, and generated audio.

- Prompt for each shot: subject, wardrobe, setting, framing (e.g. medium close-up, eye level), lighting, camera move, and the exact line they speak, in quotes.
- To keep the same character across shots, reuse the same first-frame reference image and the same description in every shot.
- Generate at the composition's aspect ratio, using the shortest duration that covers the line. Save to `footage/person_XX.mp4`, and write the prompt and job ID next to the scene in `script.md`.
- If the person speaks, the clip's audio is the voice-over for that scene. Run it through Whisper the same way as the VO track.

Never generate a real, identifiable person (founder, customer, celebrity) without that person's documented consent.
