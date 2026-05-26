# Resume — sven0219/resume

Static single-page resume site. Vanilla HTML/CSS/JS, no build step, no dependencies.

## Quick start

```
# No install needed — just open index.html in a browser
open index.html
```

## Architecture

- **`index.html`** — app entrypoint (inline JS, no bundler). Never cached (Cache-Control headers in `<meta>`).
- **`styles/main.css`** — all styles in one file. CSS custom properties for theming (`:root[data-theme='light']`).
- **`content/site.json`** — all content, bilingual (`zh`/`en`). Fetched at runtime via `fetch()`.
- **`assets/`** — static images (QR codes, screenshots). Referenced from `site.json` and `index.html`.
- **`docs/cache-versioning.md`** — cache-busting convention.
- **`CNAME`** — GitHub Pages custom domain (`resume.svenshen.me`).

Push to `main` → auto-deploys to GitHub Pages via origin `https://github.com/sven0219/resume`.

## When editing content (`content/site.json`)

Every localizable field is `{ "zh": "...", "en": "..." }`. Non-localized fields (e.g. `email`, `toolchain`) are plain strings.

## When editing CSS or JSON

Bump the `v=YYYYMMDD+letter` cache-busting query string in **both** places in `index.html`:
- line 15: `<link rel="stylesheet" href="styles/main.css?v=...">`
- line 450: `fetch('content/site.json?v=...')`

Use the same value for both. `index.html` changes alone do NOT need a bump (it is never cached).

## No tests, no lint, no CI

No test framework, no linter, no typechecker, no CI workflows. No package.json. Deployments happen by pushing to `main` — GitHub Pages serves the repo root directly.
