# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A static WebAR/360° experience built with **A-Frame 1.5** and vanilla JS, deployed to **Vercel** and embedded in Google Sites. No build step, no bundler — the project is a single `index.html` plus static assets.

**Theme:** Two Colombian films — *El abrazo de la serpiente* (1915 Amazon) and *La estrategia del caracol* (1993 Bogotá).

## File Structure

```
index.html                  — entire app (A-Frame scene + UI + JS)
vercel.json                 — Vercel headers & caching config
assets/img/
  amazon_360.jpg            — equirectangular 360° image (user must supply)
  bogota_360.jpg            — equirectangular 360° image (user must supply)
  hotspot.svg               — info hotspot icon (gold "i" on dark circle)
assets/audio/
  amazon_jungle.mp3         — looping jungle ambience (user must supply)
  city_bogota.mp3           — looping city ambience (user must supply)
ACADEMIC_DELIVERABLES.md    — Steps 3–5 academic content (English)
DEPLOYMENT_GUIDE.md         — Vercel deploy + QR + Google Sites instructions
```

## Architecture

### `index.html` — all-in-one structure

1. **Scene Selector** (`#scene-selector`) — full-screen landing UI; calls `UIManager.loadScene()`.
2. **`<a-scene>`** — hidden until a movie is selected. Contains:
   - `<a-assets>`: preloads both sky images, both audio files, hotspot SVG.
   - `<a-sky id="sky">`: src swapped dynamically by UIManager.
   - `<a-entity id="hotspots-serpiente">` and `<a-entity id="hotspots-caracol">`: 4 `<a-image>` hotspots each; toggled visible/invisible on scene switch.
   - `<a-entity id="ambient-sound">`: single sound component, src swapped on scene switch.
   - Camera with gaze cursor (`fuse="true"`, `fuse-timeout="1500"`) for VR/mobile compatibility.
3. **Info overlay** (`#info-overlay`) — appears on hotspot click; populated from `data-badge`, `data-title`, `data-body` attributes.
4. **HUD** (`#hud`) — Back button + Mute toggle, shown only while inside a scene.
5. **`UIManager` IIFE** — controls all state: scene switching, audio start/mute, card open/close.

### Key behaviors
- **Audio autoplay bypass:** `UIManager.loadScene()` shows a notice and attaches a one-time `click`/`touchstart` listener to start audio on first user gesture.
- **Hotspot interaction:** Both click (desktop/touch) and gaze-fuse (VR headset) fire `UIManager.openCard(el)`, which reads `data-*` attributes.
- **Scene switch:** Does not reload the page — swaps `<a-sky src>`, toggles hotspot group visibility, and swaps `sound` component src.

## Deployment

```bash
npm install -g vercel
vercel login
vercel --prod          # from project root
```

Assets must be present in `assets/` before deploying. See `assets/img/README_IMAGES.txt` and `assets/audio/README_AUDIO.txt` for free sources.

## Mobile Performance Rules

- 360° images: JPG ≤ 4 MB each, 4096×2048 px max.
- Audio: MP3 128 kbps, ≤ 3 MB each.
- Never use PNG for 360° images.
- A-Frame `renderer` is configured without `physicallyCorrectLights` to reduce GPU load on mobile.

## Academic Content

All Steps 3–5 content is in `ACADEMIC_DELIVERABLES.md` (English, intermediate level). Do not modify tone or reading level unless the instructor explicitly requests it.
