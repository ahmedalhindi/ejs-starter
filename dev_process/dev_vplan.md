# dev_vplan.md

Verification plan: how each sub-task and iteration in `dev_plan.md` is
verified. Checks are run by the agent unless marked **(manual)** — GUI
verification requires a human or a display.

## I1 — Minimal runnable scaffold

### I1.1 `package.json` + Electron devDependency

| Check | Command | Expected |
|-------|---------|----------|
| package.json is valid JSON with required fields | `node -e "const p=require('./package.json'); console.log(p.name, p.main, p.scripts.start)"` | prints app name, `src/main.js`, `electron .` |
| Electron installed | `npm ls electron --depth=0` | `electron@<version>` present |
| `node_modules` is ignored | `git check-ignore -q node_modules && echo ignored` | prints `ignored` |

### I1.2 `src/main.js`

| Check | Command | Expected |
|-------|---------|----------|
| Syntax valid | `node --check src/main.js` | exit 0, no output |
| Security flags set | `grep -q "contextIsolation: true" src/main.js && grep -q "nodeIntegration: false" src/main.js && echo ok` | prints `ok` |
| App launches | `npm start` (short run) | window opens, no errors in terminal **(manual: visually confirm)** |

### I1.3 `src/preload.js`

| Check | Command | Expected |
|-------|---------|----------|
| Syntax valid | `node --check src/preload.js` | exit 0, no output |
| Uses contextBridge only | grep for `require('electron')` inside preload is limited to `contextBridge`/`ipcRenderer` usage | no `nodeIntegration`-style API leak |
| API reachable from renderer | run app, open DevTools console in renderer | `window.electronAPI` (or chosen name) exposes the version object **(manual)** |

### I1.4 `src/index.html`

| Check | Command | Expected |
|-------|---------|----------|
| Renders app name + versions | `npm start` | page shows "ejs-starter" and Electron/Chrome/Node versions from preload **(manual)** |

### I1.5 `.gitignore`

| Check | Command | Expected |
|-------|---------|----------|
| Core entries present | `grep -q "node_modules" .gitignore && echo ok` | prints `ok` |
| out/ and dist/ ignored | `git check-ignore -q out dist && echo ok` | prints `ok` |

### I1.6 README alignment

| Check | Command | Expected |
|-------|---------|----------|
| Structure matches reality | `ls src/` + diff against README tree block | each README path exists |

### I1 definition of done

- All I1 sub-task checks pass, including the GUI smoke test.
- `npm start` runs clean with **no errors in the DevTools console**.
- Working tree only contains intended files; `git status` shows no strays.

## I2 — Packaging with electron-forge

### I2.1 Forge config

| Check | Command | Expected |
|-------|---------|----------|
| forge deps installed | `npm ls @electron-forge/cli --depth=0` | present |
| Config present | `node -e "require('./forge.config.js'); console.log('ok')"` (or per forge template) | prints `ok` |

### I2.2 Package build

| Check | Command | Expected |
|-------|---------|----------|
| Packaged app produced | `npm run package` | exits 0; `out/ejs-starter-win32-x64/` (platform-dependent) exists |
| Packaged app launches | run the packaged `.exe` / binary | app window opens **(manual)** |

### I2 definition of done

- All I2 checks pass.
- `out/` stays ignored (`git check-ignore out`).
