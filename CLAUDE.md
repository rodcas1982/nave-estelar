# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Game

No build system or dependencies. Open directly or use a local server to avoid CORS issues with image assets:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

## Architecture

The entire game is a single file: **`index.html`** (≈1375 lines). All HTML, CSS, and JavaScript live together. There is no module system, bundler, or package manager.

### Code Sections

The JavaScript is organized with `// ============ SECTION ============` markers. Key sections in order:

| Section | Lines | Purpose |
|---|---|---|
| GAME CONFIG | ~313 | Canvas setup, game state variables, game object arrays |
| ASSET PRELOADING | ~371 | Loads PNG sprites; falls back to canvas drawing if images fail |
| SOUND SYSTEM | ~403 | Web Audio API synthesis — no external audio files |
| PLAYER CLASS | ~539 | Movement, shooting, shield, engine glow, sprite drawing |
| BULLET / ENEMY BULLET | ~660, ~748 | Projectile classes with `update()` + `draw()` |
| ENEMY CLASS | ~684 | Enemy movement patterns, shooting behavior, sprite |
| BOSS CLASS | ~771 | Multi-phase boss with health bar, attack patterns |
| POWER-UP CLASS | ~959 | Four power-up types: shield, doubleShot, rapidFire, speed |
| GAME LOOP | ~1140 | Main `requestAnimationFrame` loop — calls update/draw on all objects |
| CONTROLS | ~1341 | Keyboard + touch event listeners |

### Game State

Global variables declared around line 326:
- `gameRunning`, `score`, `lives`, `health`, `level`, `difficulty`, `kills`, `combo`
- `activePowerUps` — object tracking remaining duration of each power-up
- `achievements[]` — array of achievement objects with `unlocked` flag
- `player`, `bullets[]`, `enemies[]`, `particles[]`, `powerUps[]`, `enemyBullets[]`, `boss`
- High score persisted via `localStorage` key `naveEstelarHighScore`

### Asset Loading Pattern

`preloadAssets()` loads images into the `assets{}` object. Every `draw()` method checks `if (assets['key'] && assets['key'].complete)` before using sprites, and draws canvas shapes as fallback. This is the pattern to follow when adding new sprites.

### Sound

`playSound(type)` generates sounds procedurally with Web Audio API oscillators — no audio files. Add new sounds by adding a case to the switch in `playSound()` (~line 414).

## Commit Conventions

- `🎨` — visual/asset changes
- `🚀` — new version or major feature
- `🐛` — bug fix
- `♻️` — refactor

## Deploy

Push to `main` deploys automatically to GitHub Pages: `https://rodcas1982.github.io/nave-estelar/`

The `index.html.backup.v*` files are stable version snapshots — useful as rollback references.
