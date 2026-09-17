# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A spec-driven, single-page static site (no build step, no dependencies) for Vaijanath Ruge, built
strictly to `SPEC.md`. Deployed as a GitHub Pages project site at
`github.com/VaijanathR/build2-portfolio`, live at https://vaijanathr.github.io/build2-portfolio/.
`.nojekyll` disables Jekyll processing so files are served as-is.

## SPEC.md is the source of truth

Read `SPEC.md` before making content or design changes. Key constraints it sets:

- **About** must be pulled from `resume.pdf`, not invented
- **Projects** entries (title + one-line description + link) must come from `projects.md`
- **Contact** is a real email address — no contact form
- Single page, dark background, exactly one accent color (light blue, `#7ec8e3` in `css/style.css`)
- Must render with no horizontal overflow at a 375px viewport
- Acceptance criteria: every Projects link resolves (no 404s), Lighthouse accessibility score ≥ 90,
  deployed URL responds within 2 seconds

Since the last update, the page also has an **Experience** section (full career timeline) sourced
directly from `resume.pdf` — this was an explicit follow-up request beyond the original `SPEC.md`
sections; keep both in sync with the resume if it changes.

## Structure

- `index.html` — single-page markup: About, Experience, Projects, Contact
- `css/style.css` — all styling; CSS custom properties on `:root` (`--bg`, `--text`, `--accent`, etc.),
  no dark/light toggle (dark is the only mode, per spec)
- `projects.md` — source-of-truth list for the Projects section; keep it and the `<ul class="project-list">`
  in `index.html` in sync
- `resume.pdf` — intentionally **not tracked** (gitignored). It contains a personal phone number and
  photo; it's used locally only as the source for About/Experience content, never committed or linked

## Verifying changes before pushing

This repo's acceptance criteria are meant to be checked, not assumed. There is no Chrome/Chromium
preinstalled in this environment — if you need to re-run Lighthouse or a 375px screenshot check, you
have to fetch a headless Chrome binary first (via `@puppeteer/browsers`, since the system has no
`unzip`, install the `yauzl` npm package alongside it so extraction works), then run `lighthouse` from
`node_modules/.bin` with `--chrome-flags="--headless=new --no-sandbox --disable-gpu"`. Do this in a
scratch directory (e.g. under `/tmp`), not inside this repo.

Minimum checks before considering a content/design change done:
1. Every link in the Projects section returns HTTP 200 (`curl -s -o /dev/null -w "%{http_code}" <url>`)
2. Lighthouse accessibility score ≥ 90
3. No horizontal scroll at a 375px viewport width

## Deploying

No build step — pushing to `main` deploys:

```bash
git add -A
git commit -m "Update site"
git push
```

GitHub Pages auto-builds on push; check status with:

```bash
gh api repos/VaijanathR/build2-portfolio/pages --jq .status
```

## Related

`../CH3Build1` is a separate, independent site for the same person (different repo, different design —
light/dark toggle, broader placeholder content). The two are not linked to each other and should be
edited independently.
