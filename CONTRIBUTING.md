# Maintaining this repo (`asuramaya/asuramaya`)

This single repo is **both**:
- the **GitHub profile README** (`README.md`, renders on github.com/asuramaya), and
- the source for **asuramaya.com** (`index.html`, served by GitHub Pages — `CNAME` points the domain here).

It's a static site: no build step, no dependencies. Edit, commit to `main`, and Pages redeploys in ~1–2 minutes.

---

## Adding / featuring a project

There are two surfaces. **One is automatic, one is manual.**

### 1. The work carousel on asuramaya.com — automatic ✅

The carousel is **fully dynamic**. On load it calls the GitHub API for the owner's
repos sorted by push date and renders cards for the **latest `MAX_CARDS` (10)**
that are **public, non-fork, non-archived**. There is no hardcoded project list.

So to feature a project on the site, a future agent (or human) does **nothing to this repo** — just:

1. **Push the project repo public** under `asuramaya`. It appears automatically, newest-push first.
2. On that repo, set a good **GitHub description** (becomes the card blurb) and **topics** (become the card tags). Cards also show stars, primary language, and last-push time.
3. **The card preview is the first image in that repo's `README.md`** (PNG/JPEG/GIF/WebP; status badges are skipped). Relative paths resolve against the repo's default branch. A repo whose README has no image shows a **"missing image" placeholder** — fix it by adding an image to that repo's README (e.g. `![demo](docs/demo.png)`).

To **hide** a repo from the carousel: archive it or make it private (both are filtered out). To **show more/fewer**: change `MAX_CARDS` in `index.html`.

> README previews are fetched from `raw.githubusercontent.com` (a CDN), so they do **not** count against the GitHub API rate limit.

> Ordering is **by push recency** (newest first) — intentional, so the freshest work leads. There is deliberately no manual ordering list to keep in sync.

### 2. The "Selected Work" list in `README.md` — manual ✍️

The profile README is hand-curated prose. To add a project, add one bullet to the
**Selected Work** list, matching the existing style:

```markdown
- [`repo-name`](https://github.com/asuramaya/repo-name) — one-sentence description of what it does and why it matters.
```

Keep it to a single sentence; lead with the concrete capability.

---

## Where the carousel logic lives (`index.html`)

All inside the inline `<script>` IIFE near the bottom:

- `OWNER`, `MAX_CARDS`, `STORAGE_KEY`, `CACHE_TTL_MS` — config at the top of the IIFE.
- `fetchData()` — pulls `users/<OWNER>/repos?sort=pushed`, filters, and grabs recent commits for the activity feed.
- `cardHtml(m)` / `buildCards(repos)` — render cards purely from repo metadata.
- `render(repos, items)` — builds cards, then inits the pixel-media effect and the carousel (must run **after** cards exist).
- `load()` — cache-first (30 min), serves a stale cache on API failure, and falls back to a "Projects on GitHub" card if there's no data at all (GitHub's unauthenticated limit is 60 req/hr per IP).

**If you change the cached data shape, bump `STORAGE_KEY`** (e.g. `-v5` → `-v6`) so visitors don't read an incompatible cache.

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
