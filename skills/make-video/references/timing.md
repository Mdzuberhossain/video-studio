# Word timings (Whisper)

```bash
pip install -U openai-whisper   # once
whisper audio/vo.mp3 --model small --language en --word_timestamps True --output_format json --output_dir audio
mv audio/vo.json audio/words.json
```

`words.json` → `segments[].words[]`, each `{ "word", "start", "end" }` in seconds.

Use it for:
- **Scene starts:** a scene starts at the `start` of its first VO word, minus about 0.15 s of lead-in.
- **Captions:** show 2 to 4 words at a time. Each word appears at its `start` and is highlighted until its `end`.
- **Cuts on the beat:** place hard cuts and kinetic text hits on word `start` times, not between words.

Whisper often misspells product names. Fix the `word` text in `words.json` against `script.md` and keep the timings.
Use `faster-whisper` instead if it is installed, since it gives the same word timestamps faster.
