# Personal Site — Product / Design / Engineering Brief

_Written 2026-07-03 by a Claude portfolio review session. Audience: a future Opus
session. The site is a deliberate single-file, no-script static page — respect
that constraint; most "improvements" would be regressions. Verify current state
first._

## 0. Status ledger (2026-07-05) + how to pick up

**Shipped ✓** — hero section; Energy Map + PersonalAssist cards; de-AI'd copy pass; the site now auto-deploys from `main` (see CLAUDE.md).
**Next → (optional, low priority)** — add one compressed screenshot per project card (the highest-value remaining change; keeps the no-script CSP intact); keep cards newest-first.
**Constraint** — single static file, `script-src 'none'` CSP. Any JS idea is out of scope by design.

## 1. Product roadmap (PM)
The site's job is to convert a visitor (recruiter, collaborator) into a click on
a live project. Three worthwhile changes, nothing more:
1. **Add screenshots.** Text-only cards undersell visual apps (Furnisher,
   MapCrowd, EnergyMap are *maps and canvases*). One small static image per card
   (compressed WebP, `loading="lazy"`) keeps the no-script constraint intact.
   This is the highest-value change on the whole site.
2. **Add the EnergyMap card once it deploys** (see EnergyMap brief P0), newest
   first, per the card conventions in CLAUDE.md.
3. **One-line "what I did" per card** — the cards say what each app does; add
   the PM/product angle ("designed the study instrument", "0→1 solo build,
   live users") since the site positions Kevin as a product manager, and the
   current copy reads engineer.

## 2. Design audit
The pale/tan minimal theme is cohesive and loads instantly — leave the system
alone. Two nits: (a) hover-only affordances (`card:hover` border) have no
touch equivalent — fine, but ensure focus-visible styles exist for keyboard
users; (b) with screenshots added, keep cards scannable — image left or top at
fixed aspect, never full-bleed.

## 3. Engineering audit
Nothing structural — it's one static file with a locked-down CSP (`script-src
'none'`) and security headers in `vercel.json`. Keep it that way:
- Adding analytics would require loosening the CSP; if curiosity strikes, use
  Vercel's server-side analytics rather than any client script.
- When adding images, no CSP change is needed for self-hosted files
  (`img-src 'self'` — verify the directive exists; add it if absent).

## 4. Surprise & delight (CSS-only — the CSP allows no scripts)
- **A view-source easter egg**: a friendly HTML comment at the top of
  `index.html` ("👋 you read source? we should talk — <email>"). Developers and
  technical recruiters *always* peek; costs one line.
- **Card hover personality**: a 1–2° tilt + soft shadow lift on `.card:hover`
  (pure CSS transform, respects `prefers-reduced-motion`). Enough motion to
  feel handcrafted, cheap enough to keep the no-framework purity.
- **CSS-only dark mode**: a checkbox-hack toggle flipping the `:root` palette
  to a warm-dark equivalent. A no-JS dark mode is itself the flex — it
  demonstrates craft within constraints, which is the site's whole thesis.
