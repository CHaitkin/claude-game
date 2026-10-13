# REDLINE

A rhythm-heavy tunnel runner in the spirit of Thumper. You fly a chrome craft down an endless, snaking tunnel of red light at speeds that keep climbing. Fly through gold rings, jump the roadblocks, dodge the walls, and outrun the Hunters.

## Run it

It's a single file: open `index.html` in a browser (Chrome works best). Three.js and the font load from CDNs, so you need an internet connection.

If your browser blocks the file, serve the folder instead:

```bash
python3 -m http.server 8000
```

Then go to http://localhost:8000.

## Controls

| Key | Action |
| --- | --- |
| ← → / A D | Steer (the tunnel spins around you) |
| ↑ / W / Space | Jump |
| ↓ / S | Slam back down |
| Hold Shift | Boost |
| P / Esc | Pause |
| R | Quick restart |
| M | Mute |
| Enter | Start / retry |

The controls appear on screen for the first 10 seconds of every run.

## How it plays

- **Speed** ramps from about 120 to about 520 km/h over roughly two and a half minutes. Radial blur, light streaks, camera shake and the rattle of the craft all scale with it.
- **Boost** (hold Shift) adds about 50% more speed and doubles distance points. It drains a meter, and **gold hex rings** refill it.
- **Rings** raise your score. Every 4 in a row adds to the multiplier (up to ×8). If you go too long without a ring, the multiplier drops.
- **Bordered walls** must be dodged. **Chevron roadblocks** must be jumped. In later zones, **sweepers** rotate around the tunnel.
- **Near misses** (swerving late past a wall) are worth bonus points.
- **Run structure:** REDLINE → FURNACE → **Hunter: THE MAW** → HEMORRHAGE → WHITEOUT → **Hunter: THE GRINDER**, then the loop repeats, harder. Each zone lasts about 24 seconds.

### Hunter fights

1. The Hunter roars past you, turns to show its face, then drops in behind you.
2. For 30 seconds it chases you. The bar at the top is your **gap**: it shrinks unless you boost, and if it reaches zero you're caught.
3. When it's close, it **lunges**. A red strip flashes on your lane, so steer out of it.
4. You get **3 shields** for the fight. Hits from lunges or obstacles cost a shield, and losing all three ends the run.
5. After 30 seconds it overshoots ahead of you, exposing a **glowing core** in one lane of its tail. Steer into that lane and boost into the core to destroy it.

## Demo helpers

In the browser console:

```js
redline.boss(0)      // jump straight to THE MAW
redline.boss(1)      // jump straight to THE GRINDER
redline.skipChase()  // skip to the Hunter's overshoot and core
```
