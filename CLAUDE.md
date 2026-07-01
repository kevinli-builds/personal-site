# CLAUDE.md

Guidance for working in this repo.

## What this is

Kevin Li's personal portfolio site — a single-page showcase of side projects.
Plain static HTML/CSS with **no build step, no framework, no dependencies**. The
entire site is one file: [`index.html`](./index.html).

- **Live:** https://kevin-li-site.vercel.app
- **GitHub:** https://github.com/kevinli-builds/personal-site
- **Host:** Vercel project `kevin-li-site` (team scope `snowwarrior1-alts-projects`)

## Local workspace

This repo now lives in its own dedicated folder, **`C:\Users\snoww\Personal Site\`**,
moved out of the project workspace so the portfolio isn't tangled with the app repos.

The sibling projects live separately in **`C:\Users\snoww\Mapper-Tracker\`** (renamed
from `Map` → `Mapper+Tracker` in June 2026; the `+` broke Turbopack's `next dev` HMR,
so keep the path free of `+` and spaces), which holds them as independent git repos:

| Subfolder | Project | GitHub | Live |
|---|---|---|---|
| `mapcrowd/` | MapCrowd | `kevinli-builds`/`MapCrowd` | mapcrowd.vercel.app |
| `tracker/` | Tracker | `kevinli-builds/Tracker` | dailytally.vercel.app |

- This (personal-site) repo only tracks the portfolio files; the app repos live in
  the separate workspace folder above, each with its own `CLAUDE.md`.
- **Shared Supabase:** MapCrowd and Tracker share one Supabase project named
  **"Mapper+Tracker"** (ref `tmycdgnofvmbyrmpqohw`) — the free tier caps you at 2
  projects. Each app owns its own tables and per-user RLS; Tracker's tables don't
  touch MapCrowd's data. **Furnisher** stays on its own Supabase project for now
  (established app; not worth a risky live-data migration), but the user is open
  to folding it in later.

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

- **Theme:** pale/tan, light, minimal. Colors/spacing are CSS custom properties in
  `:root` (`--bg` cream, `--text` warm brown, `--accent` ochre, etc.) — reuse them,
  don't hard-code values.
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
