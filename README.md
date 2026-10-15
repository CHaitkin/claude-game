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

The main menu has **PLAY** and **CONTROLS** (↑ ↓ and Enter, or click). The controls also appear on screen for the first 10 seconds of every run, and the first time roadblocks come at you in a run, a tip at the top shows the jump keys (once per run; continuing after a crash doesn't repeat it). The pause menu offers **RESUME**, **RESTART** and **MAIN MENU**.

## How it plays

- **Speed** ramps from about 120 to about 520 km/h over roughly two and a half minutes. Radial blur, light streaks, camera shake and the rattle of the craft all scale with it.
- **Boost** (hold Shift) adds about 50% more speed and doubles distance points. It drains a meter, and **gold hex rings** refill it.
- **Rings** raise your score. Every 4 in a row adds to the multiplier (up to ×8). If you go too long without a ring, the multiplier drops.
- **Bordered walls** must be dodged. **Chevron roadblocks** must be jumped. In later zones, **sweepers** rotate around the tunnel.
- **Near misses** (swerving late past a wall) are worth bonus points.
- **Run structure:** REDLINE → FURNACE → **Hunter: THE GRINDER** → HEMORRHAGE → WHITEOUT → **Hunter: THE MAW**, then the loop repeats, harder. The second Hunter of a lap is the tougher fight. Each zone lasts about 24 seconds. WHITEOUT, the fastest zone, sends about 40% fewer obstacles and only their simpler groups: no shifting corridors or checkerboard walls, two-lane gates, small scatters, single roadblock rows and two slow sweepers.

### Hunter fights

1. The Hunter roars past you into the dark, charges back face-first, then rushes past to drop in behind you. Obstacles in your way are cleared when it arrives, and nothing can hit you until the chase starts. The tunnel straightens out for the whole fight.
2. For 30 seconds it chases you. The bar at the top is your **gap**: it shrinks unless you boost, and if it reaches zero you're caught.
3. When it's close, it **lunges**. A red strip flashes on your lane, so steer out of it.
4. You get **3 shields** for the fight. Hits from lunges or obstacles cost a shield, and losing all three ends the run.
5. After 30 seconds it overshoots ahead of you, exposing a **glowing core** in one lane of its tail. Steer into that lane and boost into the core to destroy it.

A line under the Hunter's bar tells you what to do at each moment ("HOLD SHIFT TO BOOST", "DODGE THE RED LANE", "STEER INTO THE GOLD LANE", "RAM THE CORE"). Once the core is exposed, a gold lane of chevrons on the floor leads to it, a target ring marks it, and arrows at the screen edge show which way to steer.

### Clearing a lap

Destroying THE MAW clears the lap. The tunnel turns into a light show (every zone's colours cycling, fireworks, a victory warp) behind a **LAP CLEARED** screen with your stats. From there, **START LAP 02** carries on with your score into a harder second lap, or **MAIN MENU** ends the run.

### After a crash

The results screen offers **Continue from** the zone or Hunter you crashed in, or **Start over**. Choose with ↑ ↓ and Enter, or click. Continuing puts you back at the start of that zone or Hunter, with the score, speed and rings you had when you entered it. R always starts over.

## Demo helpers

In the browser console:

```js
redline.boss(0)      // jump straight to THE GRINDER
redline.boss(1)      // jump straight to THE MAW
redline.skipChase()  // skip to the Hunter's overshoot and core

redline.autopilot(true)            // the game plays itself: dodges, jumps, boosts, rams cores; it can't crash
redline.startAt(3, { runTime: 84 }) // start partway through a run (3 = HEMORRHAGE, late-run speed)
redline.stats()                     // what the autopilot did: rings, jumps, boost time, zones, clips (would-be hits)
redline.record({ seconds: 15 })     // record a 1920×1080 MP4 take ending on a REDLINE title card (intro: true adds an opening title)
```

`record()` renders a fixed 1920×1080 frame and writes MP4 (H.264) with the browser's own recorder; pass `upload: '<url>'` to POST the file somewhere, otherwise it returns the size and stats. The browser writes a fragmented MP4; to make a standard one for social apps on a Mac, run it through Apple's built-in converter:

```bash
avconvert --source take.mp4 --preset Preset1920x1080 --output REDLINE.mp4
```

Recorded videos go in `promo/`, which git ignores.
