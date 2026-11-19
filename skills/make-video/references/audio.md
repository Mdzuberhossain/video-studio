# Voice and music (ElevenLabs)

Use the ElevenLabs MCP tools if they are connected. Otherwise call the REST API with `ELEVENLABS_API_KEY`.

## Voice-over: one file per scene

Keeping one file per scene means a changed line costs one regeneration.

```bash
curl -s -X POST "https://api.elevenlabs.io/v1/text-to-speech/$VOICE_ID?output_format=mp3_44100_128" \
  -H "xi-api-key: $ELEVENLABS_API_KEY" -H "Content-Type: application/json" \
  -d '{"text": "<scene VO line>", "model_id": "eleven_multilingual_v2"}' \
  -o audio/vo_01.mp3
```

- Ask the user for a voice once and record its `voice_id` in `brief.md`. List voices with `GET /v1/voices`.
- Then join the files into one track for timing: `ffmpeg -f concat -safe 0 -i list.txt -c copy audio/vo.mp3`.

## Music

```bash
curl -s -X POST "https://api.elevenlabs.io/v1/music" \
  -H "xi-api-key: $ELEVENLABS_API_KEY" -H "Content-Type: application/json" \
  -d '{"prompt": "<mood, tempo, instruments; no vocals>", "music_length_ms": 60000}' \
  -o audio/music.mp3
```

Set the length to the video's length. Duck the music about 12 dB under the VO when you mix.

If an endpoint or field returns an error, check the current ElevenLabs API docs and do not guess.
