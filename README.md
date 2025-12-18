# Logo Maker (hosted)

Single-file Fabric.js canvas for creating or previewing logos; designed to embed easily in a host (e.g., React Native WebView).

**Project structure**
- `index.html`: All UI, canvas logic, and Fabric.js loading live here (no build step or extra assets).

**Run locally**
- Open `index.html` directly in a browser, or serve the folder:
  ```bash
  python3 -m http.server 8000
  # visit http://localhost:8000
  ```

**What it does**
- Add shapes (rect, circle, triangle, line, star, polygon) and editable text.
- Import SVG strings into the canvas.
- Background control (solid color or transparent checkerboard).
- Alignment helpers: center align, snapping guides to canvas center and other objects.
- Object transforms: move/nudge, scale, rotate, duplicate; group/ungroup; lock/hide; bring/send in stack order.
- History and export: undo/redo; export PNG/JPEG (multiplier and quality) or SVG.
- Canvas utilities: zoom in/out, set zoom, theme toggle (light/dark).

**Host/app integration**
- `window.handleRNMessage` receives commands from the host (mirrors React Native WebView `postMessage` flow).
- Supported message types include: `ADD_SHAPE`, `ADD_TEXT`, `ADD_SVG`, `UPDATE_OBJECT`, `NUDGE_POSITION`, `SET_SCALE`, `ROTATE_OBJECT`, `SET_ZOOM`, `ZOOM_IN`, `ZOOM_OUT`, `ALIGN_CENTER_H`, `ALIGN_CENTER_V`, `DELETE_SELECTED`, `DUPLICATE_SELECTED`, `GROUP_SELECTED`, `UNGROUP_SELECTED`, `BRING_FORWARD`, `SEND_BACKWARD`, `BRING_TO_FRONT`, `SEND_TO_BACK`, `SET_BACKGROUND`, `UNDO`, `REDO`, `EXPORT`, `GET_LAYERS`, `SET_LAYER_VISIBILITY`, `SET_LAYER_LOCK`, `SELECT_LAYER`, `SET_THEME`, and `DESELECT`.
- Events are emitted back to the host via `window.ReactNativeWebView.postMessage` when selections change, history updates, exports complete, etc.; see `sendToRN` calls in `index.html` for payload shapes.

**Development notes**
- Fabric.js is loaded from CDN in `index.html`; no package install is required.
- Tweak sizes, colors, and behaviors directly in `index.html`; use devtools for live edits.

**License**
MIT (add LICENSE file if you need one checked in).
