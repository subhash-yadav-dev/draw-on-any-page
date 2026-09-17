# Draw on Any Page — Marker & Screenshot

Draggable annotation toolbar that works on **every website** — draw, highlight & annotate like a real canvas, perfect for meetings, presentations, and online classes.

> Chrome Web Store: **Draw on Any Page — Marker & Screenshot** (`Draw, highlight & annotate any page. Pen, shapes, text + screenshot with drawings for meetings.`)

## Features

- **Draw on any page** — Always-visible vertical toolbar (Shadow DOM), draggable anywhere (clamped inside window, never under Chrome header), remembers position, toggles with `Alt+Shift+H`
- **Tools (10):** Pen, Pixel eraser (`destination-out`), Stroke eraser (delete whole shape), Line, Rectangle, Circle, Arrow, Frame/Highlight, Text (`T` → click to type, `Enter` to add), Hand (drag to move any stroke)
- **Colors & Thickness:** 9-color palette (2 per row, no overflow) + thickness slider `1-20px`, live preview
- **Page-anchored drawings:** Strokes stored as document coordinates (`clientX+scrollX`) and rendered with `translate(-scrollX, -scrollY)` so they stay at the page spot when you scroll — top drawings don’t float to the bottom
- **Undo / Redo / Clear** with full history stack (`HistoryManager`)
- **Screenshot with drawings:** Composites `tabs.captureVisibleTab` + `canvas.toDataURL()` via background service worker (`OffscreenCanvas`)
- **Hide keeps drawings:** Hiding toolbar (`×` or `Alt+Shift+H`) only hides the toolbar (`canvas pointerEvents=none`) — drawings stay visible

## Install (unpacked)

1. `chrome://extensions` → Developer mode **ON** → **Load unpacked** → select `chromeExtension` folder
2. Visit any `https://` site — toolbar appears top-left (drag via `⋮⋮`)
3. Toggle: `Alt+Shift+H` or click extension icon

## Chrome Web Store

- **Name:** `Draw on Any Page — Marker & Screenshot` (38 chars, hits exact search `draw on any page`)
- **Store listing:** see `store-assets/description.txt`
- **Icons:** `128×128` with `96×96` artwork + `16px` transparent padding (per [Supplying Images](https://developer.chrome.com/docs/webstore/images#icons)), PNG, works on light/dark
- **Screenshots:** `screenshots/*` — `1280×800`, 24-bit PNG no alpha, full bleed
- **Promo:** `store-icon/icon-512x512.png` (generate `440×280` small promo from it)
- **Package:** `dist/draw-on-any-page.zip`

## Architecture (SOLID)

- **S:** `CanvasManager` (canvas only), `ToolbarManager`+`DragManager` (UI), `StorageService`, `ScreenshotService`, `HistoryManager`, each `Tool`
- **O:** `ITool` + `ToolRegistry` (`Map`) — new tool = 1 file + `ToolRegistry.register('id', Cls)` in `src/tools/index.js` (e.g. `TextTool`, `HandTool` already added)
- **L:** Any `ITool` substitutable in `CanvasManager`
- **I:** `ITool`, `IStorage`, `IRenderer` segregated
- **D:** `Container` DI — `CanvasManager` depends on abstractions

```
src/core/{ITool,ToolRegistry,CanvasManager,HistoryManager,Container}
src/tools/{Pen,PixelEraser,StrokeEraser,Line,Rect,Circle,Arrow,Frame,Text,Hand} + base/BaseTool
src/ui/{ToolbarManager,DragManager}
src/services/{StorageService,ScreenshotService,ShortcutService}
src/content.js (self-contained runtime, no bundler) + src/background.js
```

Add a new tool: copy `src/tools/TextTool.js` pattern → `ToolRegistry.register('myTool', MyTool)` → toolbar auto-renders.

## Permissions Justification (for Store Privacy tab)

- `activeTab` — `tabs.captureVisibleTab` for screenshot composite
- `host_permissions <all_urls>` — “Draw on Any Page” must inject on any site for meeting use
- `scripting` — inject content script + fallback `executeScript` on icon click
- `storage` — persist strokes + toolbar state via `chrome.storage.local`
- `remote code` — none (all bundled locally, CSP `script-src 'self'`)

## Support

Open an issue in this repo. No backend, no tracking — see `PRIVACY.md`.

## License

MIT
