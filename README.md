# ejs-starter

A minimal [Electron.js](https://www.electronjs.org/) starter template — the smallest practical foundation for building a cross-platform desktop app, with no framework or bundler overhead.

## What's included

- **Main process** (`main.js`) — creates a single `BrowserWindow` and loads the renderer
- **Preload script** (`preload.js`) — safe, context-isolated bridge to the main process via `contextBridge`
- **Renderer** (`index.html`) — plain HTML/CSS/JS, no build step required
- **Security defaults** — `contextIsolation: true` and `nodeIntegration: false`
- **npm scripts** — `start` (run in dev), `package` / `make` hooks for distribution with [electron-forge](https://www.electronforge.io/)

## Getting started

```bash
# clone the template
git clone https://github.com/your-username/ejs-starter.git
cd ejs-starter

# install dependencies
npm install

# launch the app
npm start
```

## Project structure

```
ejs-starter/
├── src/
│   ├── main.js        # Main process entry point
│   ├── preload.js     # Context-isolated preload bridge
│   └── index.html     # Renderer UI
├── package.json       # App metadata, scripts, and dependencies
└── README.md
```

## Requirements

- [Node.js](https://nodejs.org/) 18+ (bundles npm)
- Electron is installed automatically via `npm install` — no global install needed

## Extending

Since there is no framework or bundler, you can add React, Vue, or a bundler (Vite, webpack) only when you need it. For small apps, vanilla HTML/CSS/JS keeps startup fast and the toolchain invisible.

## License

MIT
