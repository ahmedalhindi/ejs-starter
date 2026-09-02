# dev_requirements.md

Single source of truth for what this project must do. Status per the legend in
`dev_process.md`. No priority is needed — all requirements have to be worked
through.

Scope: this repo is a **minimal Electron.js starter template** — the smallest
practical foundation for a cross-platform desktop app, no framework or bundler.

## Requirements

| ID | Requirement |
|----|-------------|
| R1 | The project provides a `package.json` with app metadata (`name`, `version`, `description`), `main` pointing at the main-process entry, and scripts to start the app (`npm start`). |
| R2 | The main process (`src/main.js`) creates a single `BrowserWindow` and loads the renderer. |
| R3 | The window uses secure defaults: `contextIsolation: true` and `nodeIntegration: false`. |
| R4 | A preload script (`src/preload.js`) exposes a minimal, read-only API to the renderer via `contextBridge` (e.g. Electron / Chrome / Node versions). |
| R5 | The renderer (`src/index.html`) is a plain HTML/CSS/JS page that displays the app name and the versions from the preload API, proving the main → preload → renderer pipeline works. |
| R6 | A `.gitignore` excludes `node_modules/`, `out/`, and `dist/`. |
| R7 | Distribution is set up with electron-forge: `npm run package` produces a packaged app in `out/`, and `make` is wired for installers. |
| R8 | `README.md`'s structure section matches the real files after scaffolding. |

## Out of scope (for now)

- Any framework, bundler, or TypeScript (deliberately vanilla).
- Auto-updates, code signing, and CI.
