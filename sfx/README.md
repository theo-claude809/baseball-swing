# Sound files

The page makes synthesized placeholder sounds. To use real ones, drop short mp3/ogg/wav files here and list them in `manifest.json`:

```json
{ "crack_solid": "crack_solid.mp3", "whiff": "whiff.mp3" }
```

Any name not listed keeps its synthesized placeholder. Names:

| name | when |
|---|---|
| `crack_weak` / `crack_solid` / `crack_barrel` | bat contact (by exit velocity: <85 / 85-99 / 100+ mph) |
| `whiff` | swing and a miss |
| `mitt` | pitch reaches the catcher (take or miss) |
| `foul` | foul ball |
| `catch` | an out in play (played at the reveal) |
| `windup` | "get ready" cue before each pitch |
| `inning` | end-of-inning splash |
| `cheer` | home run (only if "Crowd cheers" is on) |
| `ump_strike` / `ump_ball` / `ump_out` | optional umpire calls (no synthesized fallback) |

All sound goes through a master volume (capped at 80%), a compressor and a soft clipper.
Check each file's license (CC0 is simplest).
