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
