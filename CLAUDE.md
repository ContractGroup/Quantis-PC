# CLAUDE.md — Quantis-PC

The Windows download **home** for the Quantis desktop app. This repo is a single
static GitHub Pages landing page, not application source.

## What is and isn't here

- **Here:** `index.html` (the download page, inline styles), `assets/` (brand
  mark), `favicon.svg`. Served by GitHub Pages at
  `https://contractgroup.github.io/Quantis-PC/`.
- **Not here:** the app itself. The desktop app is the **Tauri shell** in the
  main Quantis web repo (`../Quantis/src-tauri/`), released via `desktop-v*` tags
  through `.github/workflows/desktop-release.yml`. See that repo to change the app
  or cut a release.

## Rules for this repo

- It is a plain static page. Do **not** add a build system, framework, or
  dependencies.
- The download button must point at the **stable** installer link
  (`…/desktop-releases/Quantis-latest-setup.exe`), never a versioned URL. Version
  and date are read live from `latest.json` with a graceful fallback.
- Copy is UK English, Procore-grade brand voice, **no emoji, no emdashes**.
- Brand colour is Quantis purple (`#5d147c` light, `#7d1a9c` / `#b579ff` dark).
  Keep the page theme-aware (light and dark).
- Verify visually in both colour schemes before pushing (serve over HTTP; the
  browser blocks `file://` and the live-version fetch).
