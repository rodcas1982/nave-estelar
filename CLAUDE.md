# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Game

No build system or dependencies. Open directly or use a local server to avoid CORS issues with image assets:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

## Architecture

The entire game is a single file: **`index.html`** (≈1885 lines). All HTML, CSS, and JavaScript live together. There is no module system, bundler, or package manager.

### Code Sections

The JavaScript is organized with `// ============ SECTION ============` markers. Key sections in order:

| Section | Lines | Purpose |
|---|---|---|
| GAME CONFIG | ~338 | Canvas setup, offscreen nebula canvas, game state variables |
| ASSET PRELOADING | ~410 | Image asset loading system (present but unused — canvas draws everything) |
| SOUND SYSTEM | ~441 | `playSound()` — procedural Web Audio API oscillator sounds |
| SCREEN SHAKE | ~563 | Camera shake effect on damage |
| INITIALIZE STARS | ~569 | Creates 150 star objects with pre-computed color strings |
| PLAYER CLASS | ~589 | Movement, shooting, shield, dual-engine glow, canvas ship drawing |
| BULLET CLASS | ~754 | Plasma bolt with trail + tip glow; no shadowBlur (batched in loop) |
| ENEMY CLASS | ~794 | Fighter + asteroid types, movement patterns, shooting |
| ENEMY BULLET | ~912 | Energy teardrop projectile; no shadowBlur (batched in loop) |
| BOSS CLASS | ~950 | Multi-phase warship with wings, cannons, pulsing core, health bar |
| FLOATING TEXT | ~1224 | Score/combo text that drifts upward |
| POWER-UP CLASS | ~1251 | Four types with rotating orb + canvas icon |
| CREATE PARTICLES | ~1382 | Particle spawning helper |
| SPAWN ENEMY | ~1389 | Enemy wave spawning logic |
| UPDATE UI | ~1408 | HUD rendering (score, lives, health bar, achievements) |
| CHECK ACHIEVEMENTS | ~1439 | Achievement unlock conditions |
| SHOW COMBO | ~1448 | Combo multiplier display |
| GAME OVER | ~1461 | Game over screen and high score saving |
| DIFFICULTY SELECTION | ~1481 | `selectDifficulty()` — updates button highlight without starting game |
| START GAME | ~1493 | Resets all state, starts loop |
| GAME LOOP | ~1528 | Main `requestAnimationFrame` loop |
| CONTROLS | ~1828 | Keyboard + touch event listeners |

### Game State

Global variables declared around line 353 (within GAME CONFIG):
- `gameRunning`, `gamePaused`, `score`, `lives`, `health`, `level`, `difficulty`, `kills`, `combo`
- `hitFlash` — countdown (18→0) that renders a red damage overlay on screen
- `activePowerUps` — object tracking remaining duration of each power-up
- `achievements[]` — array of achievement objects with `unlocked` flag
- `player`, `bullets[]`, `enemies[]`, `particles[]`, `powerUps[]`, `enemyBullets[]`, `boss`
- High score persisted via `localStorage` key `naveEstelarHighScore`

### Visual Systems

#### Background
- `nebulaCanvas` — offscreen `HTMLCanvasElement` that holds 4 animated nebula clouds
- Re-rendered every 60 frames (not every frame) to avoid radial-gradient cost at 60fps
- 150 stars with `colorStr` pre-computed at init; `big` flag for cross-sparkle stars

#### Drawing Pattern — No External Assets
All sprites are drawn with canvas 2D API. The codebase no longer relies on PNG files; the `assets{}` image-loading system is still present but all `draw()` methods use the canvas fallback paths unconditionally.

Key objects and their visual style:
| Object | Style |
|---|---|
| Player ship | Cyan/blue gradient hull, swept wings, dome cockpit, dual animated engine flames |
| Enemy fighter | Red gradient angular ship pointing downward, glowing core |
| Asteroid | Rotating irregular polygon, craters, rim highlight |
| Boss | Wide-wing warship with lateral cannons, pulsing energy core, panel lines |
| Player bullet | Cyan plasma bolt — trail gradient + ellipse core + radial tip glow |
| Enemy bullet | Orange/red teardrop — trail + ellipse core + radial tip glow |
| Power-ups | Rotating orb with orbiting tick-marks; canvas-drawn icon per type |
| Particles | Mix of circles and directional sparks (ellipse rotated to velocity angle) |

#### Performance Rules
`ctx.shadowBlur` is expensive — **never set it inside per-object `draw()` methods** for objects that appear in large numbers. Current pattern:
- Particles: **no shadowBlur** — color + globalAlpha is sufficient
- Player bullets: shadowBlur set **once** via `ctx.save()` wrapping the full batch in the game loop
- Enemy bullets: same batch approach, separated from collision logic
- Power-ups / boss / player ship: shadowBlur is acceptable (≤5 objects at once)

### Difficulty

`selectDifficulty(diff)` updates the visual selection state without starting the game.
`startGame(diff)` resets all state and begins the loop.

`difficultySettings` object holds per-difficulty values for `enemySpeed`, `spawnRate`, `enemyHealth`.

### Sound

`playSound(type)` generates sounds procedurally with Web Audio API oscillators — no audio files. Add new sounds by adding a case to the switch in `playSound()` (~line 452).

## Commit Conventions

- `🎨` — visual/asset changes
- `🚀` — new version, major feature, or performance improvement
- `🐛` — bug fix
- `♻️` — refactor

## Deploy

Push to `main` deploys automatically to GitHub Pages: `https://rodcas1982.github.io/nave-estelar/`

The `index.html.backup.v*` files are stable version snapshots — useful as rollback references.
