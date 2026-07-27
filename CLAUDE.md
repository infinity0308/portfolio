# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static personal portfolio site for Thwaha Shuhaib (Software Developer — Django, Flutter, full-stack web). Single page (`index.html`) with in-page anchors: hero, about, experience, work, skills, contact. No build step, no package manager, no framework, no test runner, no linter.

## File layout

- `index.html` — markup, inline SVG social icons, Google Fonts (Fraunces + Epilogue)
- `css/styles.css` — all styling; CSS custom properties at top under `:root` (palette, type, spacing, motion)
- `js/main.js` — single IIFE: footer year, header `.scrolled` toggle on scroll, mobile nav toggle, `IntersectionObserver`-driven `.reveal` animations
- `images/profile.png` — profile image
- `README.md`, `LICENSE`

## Local dev / preview

No install. Open `index.html` directly, or serve the folder (any static server works):

```bash
# Python (if available)
python -m http.server 8000

# Node (if available)
npx --yes serve .
```

Then visit `http://localhost:8000`. Hot-reload not needed — refresh after edits.

## Architecture notes

- **Reveal animation pattern**: any element with class `reveal` fades+rises when scrolled into view (8% threshold, `-8%` bottom rootMargin). `.hero .reveal` items get staggered `transition-delay` via `:nth-child` and are force-shown via `requestAnimationFrame` in `js/main.js`. Respects `prefers-reduced-motion` in CSS.
- **Theme**: light, editorial, violet-accent. All colors and motion live in `:root` CSS variables — change `--accent`/`--bg-deep`/etc. there, not inline. `data-theme` switching is not implemented; only one theme.
- **Mobile nav**: `.nav-toggle` (hidden ≥901px) toggles `.nav-menu.open`. Closes on link click and sets `aria-expanded`.
- **Header**: fixed, gains `.scrolled` class past 24px scroll for a bottom border. Backdrop blur + gradient.
- **Project cards**: fourth card uses `.project-card--accent` modifier to span two columns on ≥768px and re-arrange into a 3-col grid.
- **Social icons**: GitHub/LinkedIn/X/Instagram SVGs in `index.html` currently point to `href="#"` — placeholders, must be replaced with real URLs.
- **Contact**: `mailto:thwahashuhaib6@gmail.com` is the only live outbound link besides the Brain Institute project link.

## Editing conventions

- Content text lives in `index.html`. Keep section count and `section-num` (01–05) in sync when adding/removing sections.
- New reveal-animated elements just need the `reveal` class; the observer picks them up automatically.
- New colors or spacing scale → add/edit variables in `:root`, don't hardcode.
- Keep `js/main.js` dependency-free; if a feature needs a library, discuss before adding (this is a zero-deps site on purpose).

## What this repo does NOT have

- No `package.json`, `requirements.txt`, lockfile, CI, or `.cursorrules`/`.github/copilot-instructions.md`.
- No automated tests, linter, or formatter configured. Manual review only.
- No `build`/`test`/`lint` commands to run.
