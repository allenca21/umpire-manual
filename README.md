# Little League Umpire's Manual — Mobile Reader (2026 Edition, v3)

A mobile-first, offline-capable Progressive Web App (PWA) for reading the
Little League Umpire's Manual. Installable to the iOS or Android home screen
for an app-like experience.

## What's new in v3

- **Offline-save banner** — appears after first launch with a clear
  "Download (~17 MB)" button. Pre-caches all 175 pages so the manual works
  with no internet at the field.
- **Offline status in the menu** — a footer at the bottom of the TOC drawer
  shows whether the manual is saved offline, and lets you trigger or
  re-trigger the download.
- **`install-sop.pdf`** and **`install-sop.txt`** — one-page printable
  install guide for sharing with your crew. Both iPhone and Android steps.

## Earlier features (v2)

- 3-step text size toggle (Small / Medium / Large) in the header
- Section 2 (Instructions to Umpires) broken into 12 subsections
- All text sections have rich subsection TOCs (168 deep links total)
- Blank pages skipped during navigation
- Bookmark button moved from page overlay to footer toolbar
- Larger, more tappable footer controls

## Core features

- Hierarchical TOC with 168 deep links
- Full-text search across the entire manual with highlighted snippets
- Bookmarks stored locally on device
- Swipe between pages, jump to page by number, prev/next, bookmark
- Pinch-to-zoom on diagrams (handled natively by the browser)
- Dark mode toggle
- Works offline after the user taps "Download" once

## How to host & deploy to your crew

### Step 1 — Get an HTTPS URL (5 minutes)

Pick one:

- **Netlify Drop** (no signup): Open https://app.netlify.com/drop in a
  browser, drag the `manual` folder onto the page. You get an HTTPS URL
  immediately.
- **Netlify / Vercel / Cloudflare Pages** (free signup): Drag-drop the
  folder into the dashboard for a permanent URL.
- **GitHub Pages**: Create a repo, upload the files, enable Pages from
  the main branch.

### Step 2 — Update the SOP with your URL

Open `install-sop.txt` (or regenerate `install-sop.pdf` with the included
Python script in `/home/claude/make_sop.py`) and replace `YOUR-URL-HERE`
with the real hosted URL.

### Step 3 — Share the SOP

- Text or email `install-sop.txt` to your crew.
- Or print `install-sop.pdf` and hand out at the next clinic.

Each umpire follows the 6 steps and ends up with a working offline app
on their home screen.

## Files

- `index.html` — the reader app (one file, no build step)
- `data.js` — TOC + search index
- `manifest.webmanifest` — PWA manifest
- `sw.js` — service worker (offline)
- `pages/p-001.jpg … p-175.jpg` — every page as a JPEG
- `icons/` — app icons (180/192/512px + maskable for Android)
- `install-sop.pdf` / `install-sop.txt` — install guide for your crew

## Phase 2: Native iOS/Android wrappers

When ready, this folder drops into a SwiftUI `WKWebView` shell (iOS) or
Android `WebView` (Android). State persists inside. From there you can
match the visual style of the "What's the Call?" apps, distribute via
App Store / Play Store, and add native features.

## Annual content updates

When Little League publishes a new edition:
1. Replace the source PDF
2. Re-run the extraction (Python script — ping me)
3. Bump the `CACHE` constant in `sw.js` so installed apps refresh

## Size

Total: ~17 MB (almost all page images). Initial download to use the
app: ~400 KB. The 17 MB is downloaded all-at-once when the user taps
"Download for offline use".
