# Bit Planes — Physics Demo

A browser recreation of the side-view aerial-combat game **Bit Planes** by medv
(https://medv.io/bit-planes/). Single-file HTML5 canvas game. The whole point of
this project is that the **flight physics are ported verbatim** from the original
game's deobfuscated source — do not "improve" or simplify them.

## Files
- `index.html` — self-contained version, sprites embedded as base64 (works by just opening it)
- `index-external.html` — same game, loads sprites from `sprites/` folder (easier to read/edit; needs a local server to avoid CORS on file://, e.g. `python3 -m http.server`)
- `sprites/` — PNG assets (black backgrounds already keyed to transparent, cropped)

Use whichever you prefer. If editing the code a lot, work in `index-external.html`.

## How to run
Open `index.html` directly in a browser. For `index-external.html`, run a local
server in this folder first: `python3 -m http.server 8000` then visit
`http://localhost:8000/index-external.html`.

## Controls
- Arrow Up/Down (or W/S): thrust level (0–17)
- Arrow Left/Right (or A/D): elevator / pitch
- Space: fire gun
- X: deploy missile
- C: catapult (relaunch)

## Physics — ported from source, DO NOT change the model
The flight model is force-based and must stay faithful to the original:
- Constants (object `C`): m=4 (global time-scale), l=100 (speed reference),
  d=1.5 (turn divisor), e=5 (rotation speed), h=3 (life), k=17 (max thrust),
  a=9.81 (gravity), f=15 (ammo), i=2 (missiles).
- `planeForces()`: force = gravity + thrust(along forward) + lift(along normal,
  = speed × clampDead(angleOfAttack, 50°)) + drag(= 2^(speed − 100), exponential).
  Above the stratosphere all aero forces zero out.
- Integration is a **fixed timestep accumulator** at 1/60s with the m=4 scale
  (`function frame()` and `step()`), matching the original's `Q` loop.
- `applyElevator()`: turn authority falls off with speed (`1 − speed/(l·d)`).
- Vector helpers are named `Vv`, `Vc`, `Vadd`, etc. (NOT single-letter `V` —
  that caused a name collision bug earlier; keep them prefixed).

## Known-good behavior (verified by simulation)
- Plane starts landed at full thrust, taxis, takes off ~1s, climbs steadily.
- With no pitch input it flies stably and is never deleted.
- Holding full pitch into the ground crashes it — that's correct.

## Bugs fixed so far (don't reintroduce)
1. `V`/`Vv` vector-helper name collision froze input — helpers are now `Vv`-prefixed.
2. Takeoff crash: the plane was deleted the instant it left the runway because its
   collision circles still overlapped the ground. Fix is in `step()`'s ground
   block: on takeoff, lift the plane clear (`position.y = ground − radius − 2`)
   and give upward velocity (`velocity.y = −4`) so the crash check can't fire.
3. Plane sprite faced backwards: `drawPlane()` undoes the body rotation
   (`ctx.rotate(−p.angle)`) and mirrors horizontally when heading left
   (`headingLeft = −Math.cos(p.angle) < 0`, sprite nose points right).

## Sprites
- Fly__1_/Fly__2_: plane, alternated for propeller animation
- Shoot__1_/Shoot__2_: flashed briefly when firing
- Dead__1_: shown when destroyed
- BG.png: parallax background (sky + hills)
- Bullet__1_–5_: muzzle-flash / exhaust glow shapes (currently unused as flame;
  bullets in-game are small drawn dots)
- Source: pzUH "Free Plane Sprites" on itch.io, CC-friendly free asset.

## Things you might tune
- Crash-angle tolerance (currently 50°) in `step()` — loosen if it crashes too easily.
- `PLANE_DRAW_W` (46) — on-screen plane size.
- AI difficulty in `aiUpdate()`.
- Add the muzzle-flash sprite drawn at the gun when firing.
- Tint AI planes different colors (sprite is pre-colored green, would need recolor-on-load).
