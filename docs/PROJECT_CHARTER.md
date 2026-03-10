# 🚀 Nave Estelar - Project Charter

## 1. Project Overview

| Field | Value |
|-------|-------|
| **Project Name** | Nave Estelar |
| **Type** | Web Game (HTML5 Canvas) |
| **Genre** | Space Shooter |
| **Status** | ✅ COMPLETO |
| **Start Date** | 2026-03-09 |
| **Live URL** | https://rodcas1982.github.io/nave-estelar/ |
| **Repo** | https://github.com/rodcas1982/nave-estelar |

## 2. Description

Classic space shooter game where the player controls a spaceship, shoots asteroids and enemy ships, and tries to get the highest score. Mobile-first with on-screen touch controls.

## 3. Game Mechanics

### Player
- Spaceship at bottom of screen
- 3 lives (hearts)
- Health bar indicator
- Movement:
  - **Desktop:** Arrow keys or A/D
  - **Mobile:** On-screen buttons (left/right)
- Shooting:
  - **Desktop:** Spacebar
  - **Mobile:** Fire button

### Enemies

| Type | Appears | Behavior | Points |
|------|---------|----------|--------|
| Asteroids | Always | Fall from top, various sizes | 100 |
| Enemy Ships (Red) | Score > 500 | Move down and **shoot back** | 250 |

### Difficulty Levels
- 🥰 **Fácil** - Slow spawn, weak enemies
- ⚖️ **Normal** - Default (selected)
- 💀 **Difícil** - Fast spawn, more HP

### Scoring System
- 100 points per asteroid destroyed
- 250 points per enemy ship destroyed
- High score saved to localStorage
- Difficulty affects spawn rate

## 4. Tech Stack

- **HTML5 Canvas** - Game rendering
- **JavaScript** - Game logic (single file)
- **CSS** - Styling (embedded in HTML)
- **No frameworks** - Pure vanilla JS
- **GitHub Pages** - Hosting

## 5. UI Elements

| Element | Location |
|---------|----------|
| Score | Top-left |
| High Score | Top-left (below score) |
| Health Bar | Top-left (below high score) |
| Lives | Top-right (hearts) |
| Mobile Controls | Bottom (always visible) |
| Start/Game Over Overlay | Center screen |

## 6. Game Code Structure

```javascript
// Main sections in index.html:
- CSS styles (lines ~1-120)
- HTML structure (~120-200)
- JavaScript:
  - Canvas setup
  - Game state variables
  - Difficulty settings
  - Input handling (keyboard + touch)
  - Game functions: resetGame(), startGame(), gameOver()
  - spawnEnemy() - asteroids + enemy ships
  - update() - game loop update
  - draw() - rendering
  - gameLoop() - requestAnimationFrame
```

## 7. Features Implemented

| Feature | Status | Notes |
|---------|--------|-------|
| Player movement | ✅ | Arrow keys + touch |
| Shooting | ✅ | Spacebar + touch button |
| Asteroids | ✅ | Fall from top, collision |
| Enemy ships (red) | ✅ | Shoot back after 500 pts |
| Health bar | ✅ | Top-left corner |
| Lives system | ✅ | 3 hearts |
| Score tracking | ✅ | + localStorage high score |
| Difficulty selector | ✅ | Easy/Normal/Hard |
| Mobile controls | ✅ | Always visible |
| Zoom disabled | ✅ | Fixed viewport |
| Responsive design | ✅ | Works on mobile/desktop |

## 8. Deployment

### GitHub Pages
- **URL:** https://rodcas1982.github.io/nave-estelar/
- **Branch:** main
- **Source:** / (root)

### Deploy Commands
```bash
cd /home/kali/.openclaw/workspace/nave-estelar
git add .
git commit -m "Description"
git push origin main
# Auto-deploys to GitHub Pages in ~30 seconds
```

## 9. Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-09 | Initial release |
| 1.1 | 2026-03-09 | Add health bar, zoom fix |
| 1.2 | 2026-03-09 | Add enemy ships that shoot, move health bar |

## 10. Future Improvements (Optional)

- [ ] Add ship selector (5 different colors)
- [ ] Power-ups (shield, triple shot, speed boost)
- [ ] Boss levels
- [ ] Sound effects
- [ ] Particle explosions improvement
- [ ] Background music

---

**Created:** 2026-03-09  
**Author:** Nova (for Gerardo)  
**Last Updated:** 2026-03-09
