# CLAUDE.md

Guidance for working in this repo.

## What this is

Kevin Li's personal portfolio site — a single-page showcase of side projects.
Plain static HTML/CSS with **no build step, no framework, no dependencies**. The
entire site is one file: [`index.html`](./index.html).

- **Live:** https://kevin-li-site.vercel.app
- **GitHub:** https://github.com/snowwarrior1-alt/personal-site
- **Host:** Vercel project `kevin-li-site` (team scope `snowwarrior1-alts-projects`)

## Files

| File | Purpose |
|------|---------|
| `index.html` | The whole site — markup + inline `<style>`. Edit this for any content or design change. |
| `vercel.json` | Security response headers (CSP, X-Frame-Options, etc.). |
| `.gitignore` | Excludes `.vercel`, `.claude/`, local project folders (`mapcrowd/`, `tracker/`), logs, OS junk. |

## Deploy workflow

Changes go to `main` and deploy via the Vercel CLI (there is **no** local dev
server — it's a static file). After editing:

```bash
git add index.html
git commit -m "…"
git push
vercel --prod --scope snowwarrior1-alts-projects
```

To preview a content change locally, just open `index.html` in a browser.

## Conventions

- **Theme:** dark, minimal. Colors/spacing are CSS custom properties in `:root`
  (`--bg`, `--surface`, `--accent`, etc.) — reuse them, don't hard-code values.
- **External links:** always `target="_blank" rel="noopener noreferrer"`.
- **Security headers** live in `vercel.json`; the CSP allows the inline `<style>`
  block (`style-src 'unsafe-inline'`) but blocks all scripts (`script-src 'none'`).
  Adding any `<script>` would require loosening the CSP.

## Adding / editing a project card

Projects live in `<section id="projects">` inside `.projects`. Newest project
goes **first**. Each card follows this structure:

```html
<div class="card">
  <div class="card-header">
    <span class="card-title">PROJECT NAME</span>
    <div class="card-links">
      <a class="badge live" href="LIVE_URL" target="_blank" rel="noopener noreferrer">↗ Live</a>
      <a class="badge github" href="REPO_URL" target="_blank" rel="noopener noreferrer">GitHub</a>
    </div>
  </div>
  <p class="card-desc">One or two sentences on what it does.</p>
  <div class="tag-row">
    <span class="tag">Tech</span>
    <!-- … -->
  </div>
</div>
```

- The `live` badge is optional (omit if there's no deployment); the `github`
  badge is optional too (omit for private repos).
- Write descriptions and tech tags from the project's **actual repo** (its
  README / `package.json` / `CLAUDE.md`) rather than guessing.

## Current projects

Tracker, Furnisher, MapCrowd, Do I Want to Know, BookTracker, SurveyTok.
