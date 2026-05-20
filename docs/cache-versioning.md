# CSS & JSON Cache Versioning

This site uses query-string version hashes to bust browser caches.

## Where

- `index.html` line 14 — `<link rel="stylesheet" href="styles/main.css?v=20260520d" />`
- `index.html` line 450 — `fetch('content/site.json?v=20260520d', ...)`

## Convention

    v=YYYYMMDD + letter suffix

- `YYYYMMDD` — date of the deployment
- `letter` — incremental per bump on that day (`a`, `b`, `c`...)

## When to bump

Bump **both** hashes whenever `styles/main.css` or `content/site.json` changes and you want browsers to pick up the new version immediately.

Do **not** bump if the change is only to `index.html` itself (e.g. JS logic, HTML structure), since `index.html` is never cached (`Cache-Control: no-cache, no-store, must-revalidate`).
