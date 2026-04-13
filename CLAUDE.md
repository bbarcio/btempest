# CLAUDE.md

## Project overview

btempest is a browser-based implementation of the classic Tempest arcade game. It is a single-file HTML5/Canvas application written in vanilla JavaScript with no external dependencies or build tools.

## How to run

Open `index.html` in any modern web browser. No build step or installation required.

## Project structure

```
index.html   # Complete game implementation (~1500 lines of embedded CSS + JS)
README.md    # Project readme
CLAUDE.md    # This file
```

## Code conventions

- 2-space indentation
- camelCase for variables and functions
- UPPER_CASE for constants
- Section headers use ASCII art dividers: `// ─── SECTION NAME ───────`
- Compact, minimal code style

## Key sections in index.html

- **Icon / Manifest / Service Worker**: PWA setup (dynamically generated)
- **Canvas setup**: Responsive canvas with mobile detection
- **Palette**: Color definitions
- **Geometry**: Tube shape definitions (Circle, Square, Triangle, Star, Plus, Hexagon)
- **Game state & input**: Keyboard and touch input handling
- **Rendering**: `drawTube`, `drawPlayer`, `drawEnemies`, `drawBullets`, etc.
- **Update/physics**: Collision detection, entity movement
- **Main loop**: `requestAnimationFrame`-based game loop

## Testing

No automated tests. Test manually by opening `index.html` in a browser and verifying:
- Desktop: arrow keys to move, spacebar to shoot
- Mobile: touch controls for movement and shooting
- Game states: title screen, gameplay, level transitions, game over
