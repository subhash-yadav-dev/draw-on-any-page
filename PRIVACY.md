# Privacy Policy — Draw on Any Page — Marker & Screenshot

**Effective:** 2026-09-17
**Extension:** `Draw on Any Page — Marker & Screenshot` (Chrome Web Store ID: `lpfbljkomajgaofgdjiecmdinonjofap`)
**Homepage / Support:** This GitHub repository (e.g. `https://github.com/YOURNAME/draw-on-any-page`) — replace `YOURNAME` with your GitHub username before publishing.

## Summary

This extension **does not collect, transmit, sell, or share any user data**. All data stays on your device. We do not use analytics, tracking, advertising, or remote servers.

## Data Collected

**None.** The extension does not collect personal information, browsing history, keystrokes, or page content for transmission.

## Data Stored Locally (on-device only)

- **Drawings:** Strokes JSON array (tool, color, thickness, points, text) stored via `chrome.storage.local`, keyed by `hostname+pathname` (e.g. `mm_strokes_example.com/path`). Used to keep drawings page-anchored when you scroll and to restore after reload until you click **Clear**.
- **Preferences:** Toolbar position (`mm_toolbar_pos`), visibility (`mm_toolbar_visible`), selected color/thickness. Stored via `chrome.storage.local`.

No data leaves your device. Screenshots are composited locally (`OffscreenCanvas` + `tabs.captureVisibleTab`) and downloaded to your device — never uploaded.

## Permissions Explained

- `storage` — Save drawings and toolbar state locally.
- `activeTab` + `scripting` — Capture visible tab for “Screenshot with drawings” (`chrome.tabs.captureVisibleTab`).
- `host_permissions <all_urls>` — Inject the Shadow DOM toolbar + canvas overlay on any website you visit, because the single purpose is “draw on any page” for meetings/presentations. Justification is shown on the Store Privacy tab.
- **Remote code:** Not used. All code is bundled in the ZIP (`src/content.js`, `src/background.js`, etc.). CSP is `script-src 'self'; object-src 'none'`. No `eval`, no CDN.

## Third Parties

None. No third-party SDKs, no Google Analytics, no external fetches.

## Children

Not directed to children. No age-restricted data collected.

## Changes

We may update this policy with extension updates. The effective date above will change. Continued use after an update constitutes acceptance.

## Contact

Open an **Issue** in this GitHub repository for privacy questions. This repository’s **Issues** page is the official support channel (also set as the Store **Support URL**).

---

For Chrome Web Store **Privacy practices** tab: select **“Does not handle user data”** (or **No, I do not collect or transmit user data**) and certify compliance with the Developer Programme Policies. Paste a link to this file (raw GitHub URL, e.g. `https://raw.githubusercontent.com/YOURNAME/draw-on-any-page/main/PRIVACY.md` or the GitHub page `https://github.com/YOURNAME/draw-on-any-page/blob/main/PRIVACY.md`) as the **Privacy Policy URL**.

