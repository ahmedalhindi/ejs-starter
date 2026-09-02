# dev_plan.md

Iterations derived from `dev_requirements.md`. Each iteration is a milestone /
major feature and maps to requirements. Sub-tasks are listed per iteration.

Status legend: `proposed` → `approved` → `in progress` → `verified` → `done`.

## I1 — Minimal runnable scaffold (Milestone 1)

Goal: `npm start` launches a secure Electron window showing a working
main → preload → renderer pipeline.

Covers: R1, R2, R3, R4, R5, R6, R8 — **status: proposed**

| Sub-task | Description | Covers | Status |
|----------|-------------|--------|--------|
| I1.1 | Create `package.json` (metadata, `main`, `start` script) and add Electron as a devDependency | R1 | proposed |
| I1.2 | Implement `src/main.js` — single `BrowserWindow`, secure defaults, load renderer | R2, R3 | proposed |
| I1.3 | Implement `src/preload.js` — `contextBridge` API exposing versions | R4 | proposed |
| I1.4 | Implement `src/index.html` — minimal UI showing app name + versions | R5 | proposed |
| I1.5 | Add `.gitignore` (node_modules, out, dist) | R6 | proposed |
| I1.6 | Align `README.md` structure section with actual files | R8 | proposed |

## I2 — Packaging with electron-forge (Milestone 2)

Goal: `npm run package` produces a runnable packaged app in `out/`.

Covers: R7 — **status: proposed**

| Sub-task | Description | Covers | Status |
|----------|-------------|--------|--------|
| I2.1 | Add electron-forge, init the forge config (maker config incl. current platform) | R7 | proposed |
| I2.2 | Verify `npm run package` produces a launchable app in `out/` | R7 | proposed |

## Cross-cutting notes

- Iterations build on each other: I2 depends on I1 being done.
- Branch naming: `I1.4-index-html`, `I2.1-forge-config`, etc.
