# Swing Baseball

Phone-as-bat baseball PWA (GitHub Pages). Standalone modes work with no setup.

## Claude pitching mode

A desktop MCP server lets Claude throw the pitches. The two sides talk through a secret gist
(`request.json` / `result.json`); the pitch flight and swing timing run entirely on the phone,
so network latency never affects timing.

- Page → "Claude link": paste a classic GitHub token with only the `gist` scope (stored in this
  device's localStorage, never in the repo). Do this inside the installed Home Screen app.
- Page → "Start — Claude pitching".

### Protocol

`request.json` (written by the MCP): `{"id": <increasing number>, "type": "fastball|changeup|slider|curveball", "x": -1.8..1.8, "y": -1.8..1.8, "mph": 60..105}`
Zone is x,y in [-1,1]; x<0 inside / x>0 away (righty), y<0 high / y>0 low. `type`, `x`/`y`, `mph` are optional (random if omitted).

`result.json` (written by the page): `{"id": <request id>, "pitch": {...}, "swung": bool, "swing": {timing, bat, ev, la, spray, dist} | null, "events": [...], "state": {...}}`
On start the page writes `{"id": <last>, "ready": true, "state": {...}}`.

### Suspense hold and reveal
For a ball in play the phone plays the bat crack immediately but holds the outcome (field animation, message, scoreboard) for ~1.2–2.6 s. `result.json` is still written right away with `"hold": true` so the desktop can start its replay; when the phone reveals the outcome it rewrites it with `"hold": false, "revealed": true`, and the MCP only returns the result to Claude then (so Claude can't spoil it).
Optional desktop sync: with "Claude mode: wait for the desktop reveal" on, the phone holds up to 10 s until the desktop writes `reveal.json` = `{"id": <request id>}` to the gist.

### Sound
Synthesized placeholders by default (master volume capped at 80%, compressor + soft clipper). Real files: see `sfx/README.md`.
