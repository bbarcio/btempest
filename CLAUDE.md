# CLAUDE.md

## Project Overview

**btempest** is a browser-based recreation of the classic 1981 Atari arcade game Tempest. The entire game is implemented in a single `index.html` file (~1,500 lines) with no external dependencies or build system.

## Tech Stack

- Pure JavaScript (ES6+), HTML5, CSS3
- HTML5 Canvas 2D for rendering
- Web Audio API for dynamic sound generation
- PWA support (inline service worker + manifest) for offline play
- Google Fonts: IBM Plex Mono

## Project Structure

```
index.html   — The entire game (HTML, CSS, JS, inline PWA assets)
README.md    — Project title
```

There is no build step, no bundler, no package manager. Just open `index.html` in a browser.

## Running the Game

Open `index.html` in any modern browser. No server required (though a local server avoids occasional CORS issues with service workers).

## Architecture

- **Single game-state object (`gs`)**: holds mode, score, entities, timers — the single source of truth.
- **Entity arrays**: `bullets[]`, `enemies[]`, `rimEnemy[]`, `spikes[]`, `particles[]`.
- **State machine**: game modes cycle through `title → playing → dead/zoom/gameover`.
- **Tube system**: 15 procedural tube shapes (11 closed, 4 open) defined in `TUBE_SHAPES`. Each tube has `N = 16` lanes.
- **Rim enemy FSM**: flippers that reach the rim use a sliding/flipping state machine along lane segments.
- **Depth-based 3D**: enemies travel down the tube using a depth parameter `[0–1]`.

## Key Constants & Configuration

- `N = 16` — lanes per tube
- `PAL` object — full color palette (bg, tube, player, enemies, HUD, etc.)
- Difficulty scales with level: `waveCap = 6 + level * 3`, `spawnRate = max(28, 90 - level * 6)`
- Trackpad/spinner tuning: `SPIN_THRESHOLD`, `SPIN_FRICTION`, `SPIN_MAX`
- Mobile dead zone: `DEAD_ZONE_FRAC = 0.28`

## Input

- **Desktop**: Arrow keys / WASD (move), Space / X (shoot), Z (superzapper), M (mute), trackpad/wheel (spinner)
- **Mobile**: Touch-based aiming with spring physics, auto-fire, on-screen superzapper and mute buttons

## Code Style

- Dense, minified-style JS with section headers using box-drawing characters (`─`, `═`)
- Helper utilities: `lerp()`, `lerpPt()`, `rand()`, `randi()`, `wrap()`, `glow()`, `noGlow()`
- ES6 throughout: arrow functions, destructuring, `const`/`let`
- No external linter or formatter configured

## When Making Changes

- Everything lives in `index.html`. There is no module system.
- Test changes by opening the file in a browser — there is no automated test suite.
- The inline service worker caches aggressively; hard-refresh or clear cache when testing locally.
- Mobile detection uses UA sniffing + feature detection (line ~30s); keep both paths in sync.
