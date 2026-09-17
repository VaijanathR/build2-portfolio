# Build2 — Spec-driven personal page

Single-page site built strictly to `SPEC.md`. Content sources:

- `resume.pdf` — source for the two About paragraphs (not invented)
- `projects.md` — source for the Projects section (title + one-line description + link)

## Verified against acceptance criteria

- All three project links return HTTP 200 (checked with `curl`)
- Lighthouse: accessibility 100/100, performance 100/100 (headless Chrome, local server)
- Renders with no horizontal overflow at a 375px viewport (checked with Puppeteer)

## Structure

- `index.html` — page markup
- `css/style.css` — dark background, single light-blue accent (`#7ec8e3`)
- `resume.pdf`, `projects.md` — source-of-truth content files

## Deploying

Static site, no build step. Push to `main` and GitHub Pages serves it directly.
