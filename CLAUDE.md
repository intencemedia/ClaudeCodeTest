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
- **sniper.html** — First-person retro arcade sniper game with panoramic scrolling, 5x scope zoom, enemy AI, and particle effects
- **tictactoe.html** — Tic Tac Toe with AI opponent

## Development

No build tools, bundlers, or package managers. To test changes, open the HTML file in a browser:
```
open sniper.html
```

## Git Workflow

This project uses Git with GitHub remote. After making changes, commit with a descriptive message and push to `origin/main`. The GitHub repo is at `github.com/intencemedia/ClaudeCodeTest`.

## Conventions

- Each game must be a single self-contained HTML file — no external assets or dependencies
- Canvas games use a fixed logical resolution (e.g., 800x600) with `imageSmoothingEnabled = false` for pixel art aesthetic
- Game state is managed with module-level variables (no classes/frameworks)
- Retro arcade aesthetic: scanlines, monospace fonts, CGA/EGA-inspired palettes
