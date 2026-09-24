# Quantis-PC

The Windows download home for the **Quantis** desktop app.

**Download:** https://contractgroup.github.io/Quantis-PC/

## What this repo is

A single static landing page (`index.html` + `assets/`) served by GitHub Pages.
Its only job is to give people a friendly place to click **Download for Windows**.
There is no application source code here.

The download button points at a stable, always-latest installer link, so this page
never needs updating when a new version ships:

| File | Stable link |
| --- | --- |
| Windows installer | `…/desktop-releases/Quantis-latest-setup.exe` |
| macOS disk image | `…/desktop-releases/Quantis-latest.dmg` |
| Updater feed | `…/desktop-releases/latest.json` |

Base URL: `https://api.contractgroup.co.uk/storage/v1/object/public/`

The page reads `latest.json` at load time to show the current version and date,
and falls back to sensible defaults if that request fails.

## Where the app actually lives

The desktop app is the **Tauri shell** in the main Quantis web repo, under
[`src-tauri/`](https://github.com/ContractGroup/Quantis/tree/main/src-tauri). It
bundles the web build and self-updates from the `latest.json` feed above.

## How a release is cut

Releases are produced from the **main Quantis repo**, not here:

1. Bump `version` in `src-tauri/tauri.conf.json`.
2. Run `scripts/release-desktop.sh` (or push a `desktop-v<version>` tag).
3. `.github/workflows/desktop-release.yml` builds the Windows NSIS installer and
   the macOS universal DMG, then publishes both plus `latest.json` to the public
   Supabase Storage bucket `desktop-releases`, and creates a GitHub Release.

Installed apps poll `latest.json` and update themselves. This page always serves
whatever the current release is, so no change here is needed per release.

## Editing the page

Edit `index.html` directly (styles are inline; brand assets live in `assets/`).
To preview locally, serve the folder over HTTP, for example:

```bash
python3 -m http.server 4599 --directory .
```

then open `http://localhost:4599`.

## Known follow-ups

- **Code signing.** The installer is signed for update integrity but not with an
  Authenticode certificate, so Windows SmartScreen warns of an unknown publisher
  on first run. An EV code-signing certificate removes that warning.
- **Custom domain.** Pages currently serves from `contractgroup.github.io`. A
  `download.contractgroup.co.uk` CNAME can be added later.
