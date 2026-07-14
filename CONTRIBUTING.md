# Maintaining this repo (`asuramaya/asuramaya`)

This single repo is **both**:
- the **GitHub profile README** (`README.md`, renders on github.com/asuramaya), and
- the source for **asuramaya.com** (`index.html`, served by GitHub Pages — `CNAME` points the domain here).

It's a static site: no build step, no dependencies. Edit, commit to `main`, and Pages redeploys in ~1–2 minutes.

---

## Adding / featuring a project

asuramaya.com has **three** sections now, each with a different job:

- **Work** — the actual live apps, embedded and running right in the page (see below). Not screenshots — the real thing.
- **Experience** — static, hand-written (resume/skills, synced from `resume.html`). Not repo-driven.
- **Activity** — **fully automatic and uncapped**, the "whatever's actually moving right now" surface. Two widgets, same data source: a full-card carousel (every public repo, with its README preview image) and, below it, a one-line-per-repo commit ticker. Neither is curated or capped.

### Work — embedded live apps, not screenshots

`LIVE_APPS` in `index.html`'s script is an ordered array of `{ key, label, url }`.
The first app's `url` is also the iframe's `src` in the HTML directly (with
`loading="lazy"`) — that's native browser behavior, not custom JS: the app
loads once you actually scroll to it, "just there," no polling or
IntersectionObserver needed. Adding a **second** entry automatically turns on
a tab bar (hidden while there's only one) — clicking a tab swaps the iframe's
`src` immediately.

**Only embed a project's already-public, edge-deployed build** (e.g.
hector-vector.com, hcirnieh.com) — never a `localhost`-only desktop/companion
app; those need the owner's own GPU/weights and can't run for a visitor.
Before adding one, confirm it doesn't block framing:

```bash
curl -sI https://the-app.example.com | grep -i "x-frame-options\|content-security-policy"
```

No output means no restriction (the current default for both hector-vector.com
and hcirnieh.com — checked 2026-07-13). If either header is present and
excludes `asuramaya.com`, that repo's own deploy config needs a
`frame-ancestors` fix first — that's a change to *that* project, not this one.

### Activity — automatic, uncapped, nothing to maintain

On load, every public, non-fork, non-archived repo under the owner is fetched
**once** and used for both widgets in this section:

1. **The carousel** gets a full card per repo — description, topics, stars, language, last-push, and a README preview image (the first PNG/JPEG/GIF/WebP in that repo's `README.md`, status badges skipped; relative paths resolve against the default branch). A repo whose README has no image shows a **"missing image" placeholder** — fix it by adding one, ideally a real screenshot rather than a logo/mascot.
2. **The ticker** gets that repo's single latest commit, merged with everyone else's and sorted by recency — one line per repo. Bot/noise commits (`chore(deps):`, `bump `, `[bot]`, etc.) are filtered by `isNoise()`.

Push to any public repo and it appears in both places on the next load — nothing to edit, nothing to feature. That's deliberate: this section exists to show total breadth and cadence, not a curated best-of.

> README previews are fetched from `raw.githubusercontent.com` (a CDN), so they do **not** count against the GitHub API rate limit. The per-repo commit fetch does — budget ~1 call per repo per fresh (non-cached) load.

### The "Selected Work" list in `README.md` — manual ✍️

The profile README is hand-curated prose, separate from the site. To add a project, add one bullet to the
**Selected Work** list, matching the existing style:

```markdown
- [`repo-name`](https://github.com/asuramaya/repo-name) — one-sentence description of what it does and why it matters.
```

Keep it to a single sentence; lead with the concrete capability.

---

## Where the site logic lives (`index.html`)

All inside the inline `<script>` IIFE near the bottom:

- `OWNER`, `STORAGE_KEY`, `CACHE_TTL_MS` — config at the top of the IIFE.
- `fetchData()` — pulls `users/<OWNER>/repos?sort=pushed` **once** (every public, non-fork, non-archived repo) and builds both `repos` (with README images, for the carousel) and `items` (one latest commit per repo, sorted by recency, for the ticker) from the same set — nothing is filtered down further.
- `cardHtml(m)` / `buildCards(repos)` — render the carousel's cards purely from repo metadata.
- `render(repos, items)` — builds cards, then inits the pixel-media effect and the carousel (must run **after** cards exist), then renders the ticker.
- `load()` — cache-first (30 min), serves a stale cache on API failure, and falls back to a "Projects on GitHub" card if there's no data at all (GitHub's unauthenticated limit is 60 req/hr per IP — this now costs ~1 call per repo for the ticker, so it scales with total repo count).

**If you change the cached data shape, bump `STORAGE_KEY`** (e.g. `-v7` → `-v8`) so visitors don't read an incompatible cache.

## Verifying changes

```bash
# extract the inline script and syntax-check it
python3 - <<'PY'
import re; html=open("index.html").read()
open("/tmp/site.js","w").write(re.search(r"<script>\s*(\(function\(\).*?)</script>", html, re.S).group(1))
PY
node --check /tmp/site.js
```

Then open `index.html` in a browser (or wait for the Pages deploy) and confirm the carousel populates and the activity feed loads.
