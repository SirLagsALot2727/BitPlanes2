# 🛩️ Bit Planes

A browser recreation of the side-view aerial-combat game **[Bit Planes](https://medv.io/BitPlanes2/)** by medv — with the **force-based flight physics ported faithfully from the original**. It's a single, self-contained HTML file: no build step, no dependencies, no server. Just open it and fly.

<!-- Add a screenshot to make this pop: save one as screenshot.png in the repo root, then uncomment the line below.
![Bit Planes](screenshot.png)
-->

## ✈️ Play

**The whole game is one file.** To play, you only need `index.html`:

- **Easiest:** download `index.html` and double-click it. That's it.
- **From the repo:** clone or copy the files, then open `index.html` in any modern browser.

```bash
git clone https://github.com/SirLagsALot2727/BitPlanes2.git
cd BitPlanes2
open index.html        # macOS  (use 'start' on Windows, 'xdg-open' on Linux)
```

### Host it free on GitHub Pages
Because it's a single static file, you can publish a playable link in seconds:

1. Push this repo to GitHub.
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch**, pick `main` / `/root`, Save.
3. Your game goes live at `https://SirLagsALot2727.github.io/BitPlanes2/`.

## 🎮 Controls

| Action | Player 1 | Player 2 (co-op / split modes) |
| --- | --- | --- |
| Thrust up / down | `↑` / `↓` (or `W` / `S`) | `W` / `S` |
| Pitch (elevator) | `←` / `→` (or `A` / `D`) | `A` / `D` |
| Fire gun | `Space` | `1` |
| Deploy missile | `X` | `2` |
| Catapult (relaunch) | `C` | `3` |

Hold full thrust to take off; ease the elevator to climb. Diving into the ground at a steep angle crashes you — that's intended.

## 🕹️ Game modes

**Classic** — Death Match · Teams · Duel · Survival
**Fun** — Swarm · Domination · Revenge
**New** — Time Dilation · Last Plane Standing · Infection · Time Attack · Protect the Cow
**Local Multiplayer** — Split Duel · Overpowered Duel · Time Dilation Duel · Teamwork · Co-op Survival

> ⏱️ **Time Dilation** modes give you live sliders that bend time — speed up your own plane and bullets while slowing the enemy squad to a crawl.

> 🥚 There's also a secret mode hidden somewhere in the **Credits**… tap around and you might unlock the *Flight Lab*, a sandbox where you assign modifiers (invincibility, time warp, overpowered) to each side, add bots, or go co-op.

## 📁 Project layout

| File | What it is |
| --- | --- |
| `index.html` | The complete game — sprites embedded as base64. **This is the deliverable.** |
| `index-external.html` | Same game, but loads PNGs from `sprites/` — easier to read/edit (needs a local server, e.g. `python3 -m http.server`). |
| `sprites/` | PNG assets (plane, bullets, background), backgrounds keyed to transparent. |
| `CLAUDE.md` | Developer notes: the physics model, constants, and design history. |

> Editing tip: for big changes work in `index-external.html` (or the readable parts of `index.html`) and run a local server to avoid `file://` CORS on the external sprites.

## ⚙️ How it works

The flight model is **force-based and ported verbatim** from the original game's source — gravity, thrust along the forward vector, lift proportional to speed × angle-of-attack, and exponential drag, integrated with a fixed-timestep accumulator. The point of the project is fidelity to that model, so the physics aren't "improved" or simplified. See `CLAUDE.md` for the full breakdown of constants and behavior.

## 🙏 Credits

- Original **Bit Planes** game and flight physics: **[medv](https://medv.io/BitPlanes2/)**
- Plane sprites: **pzUH** — *"Free Plane Sprites"* (itch.io)
- This recreation: **Evan Scott**, built with **Claude**

## 📄 License

No license has been chosen yet, so by default all rights are reserved. (You can add an `MIT`/`Unlicense`/etc. `LICENSE` file later to let others reuse the code.) Note that the original game concept belongs to medv and the sprites to pzUH under their respective terms.
