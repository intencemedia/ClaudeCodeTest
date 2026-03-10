# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains self-contained browser games, each implemented as a single HTML file with no external dependencies. All CSS, JavaScript, and game logic live inline within each file.

## Architecture

Each game is a standalone `.html` file that can be opened directly in a browser (`open <file>.html`). Games use:
- HTML5 Canvas API for rendering (2D context)
- `requestAnimationFrame` game loops
- Procedural audio via Web Audio API (no sound files)
- Pointer Lock API for mouse-based camera control (sniper game)

### Current Games

#### sniper.html — First-Person Retro Arcade Sniper Game
- **Canvas**: 800x600 viewport over a 3200x600 panoramic world
- **Scene**: Desert environment with gradient sky (purple-to-orange sunset), sun with glow, distant mountains (parallax 0.3x), mid-ground hills (parallax 0.6x), jagged terrain with cacti and rocks
- **Enemies**: Tiny pixel sprites (~7px tall) at ~400m distance, olive drab uniforms with helmets, walk left/right with 2-frame leg animation. Spawn at random terrain positions, 8+ active at a time
- **Enemy speed**: Base speed is `(0.3 + random * 0.4 * difficulty) / 4` — intentionally slowed to 1/4 of original speed per user request
- **Sniper rifle**: Drawn in screen space (bottom-right, angled -0.25 rad). Dark barrel, wood stock, scope tube with blue lens, magazine, trigger guard, bolt handle, skin-colored hands with fingers
- **Shooting**: 'A' key fires, 800ms bolt-action cooldown, recoil animation (Y offset decays via `*= 0.88`), muzzle flash (yellow rect, 8 frames)
- **Hit detection**: Crosshair center mapped to world-space, hit radius 6px (zoomed) / 10px (unzoomed). On hit: enemy removed, 15-25 explosion particles spawned, score +100, "KILL!" flash
- **Scope zoom**: Toggle with Z key or right-click. 5x magnification via `ctx.scale(5,5)` centered on screen. Circular aperture (radius 250px) using `ctx.clip()`, thick black scope ring border. Green crosshair with mil-dot marks every 40px, red center dot, "400m" range text
- **Particles**: Red/orange/yellow rectangles (1-3px), random velocity with upward bias, gravity 0.08/frame, life 30-50 frames with alpha fade
- **HUD**: Green monospace text — score (top-left), ammo as `|` bars (bottom-left, 5 rounds), reload indicator with animated dots, zoom indicator (top-right), threat level (bottom-right)
- **Ammo/reload**: 5 rounds per magazine, 'R' to manual reload, auto-reload when empty, 2000ms reload time
- **Difficulty**: Ramps every 15 seconds (+0.2, max 3.0), increases enemy count and speed
- **Audio**: Procedural via Web Audio API — gunshot is white noise burst (120ms) through bandpass filter at 800Hz; hit confirm is sine wave beep (80ms, 800Hz)
- **Retro polish**: `imageSmoothingEnabled = false`, scanline overlay (every other row at 8% black opacity), CGA/EGA color palette
- **Camera**: Pointer Lock API, mouse panning with sensitivity 0.5 (normal) / 0.15 (zoomed), vertical panning clamped to ±100px

#### tictactoe.html — Tic Tac Toe
- CSS Grid layout with AI opponent, win detection, and hover effects

## Development

No build tools, bundlers, or package managers. To test changes, open the HTML file in a browser:
```
open sniper.html
```

## Git Workflow

This project uses Git with GitHub remote at `github.com/intencemedia/ClaudeCodeTest`. After every change, commit with a descriptive message and push to `origin/main` so there is always a saved version to revert to.

## Conventions

- Each game must be a single self-contained HTML file — no external assets or dependencies
- Canvas games use a fixed logical resolution (e.g., 800x600) with `imageSmoothingEnabled = false` for pixel art aesthetic
- Game state is managed with module-level variables (no classes/frameworks)
- Retro arcade aesthetic: scanlines, monospace fonts, CGA/EGA-inspired palettes
- Always commit and push after changes so the user can revert if needed
