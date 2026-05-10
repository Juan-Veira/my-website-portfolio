# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML5 portfolio site — no build step, no framework, no package manager. Three files drive the entire site: [index.html](index.html), [style.css](style.css), and [script.js](script.js).

Deployed to Netlify/Vercel; [_headers](_headers) sets HTTP security headers and CSP.

## Development

Open `index.html` directly in a browser, or use any static file server:

```powershell
# Python (if available)
python -m http.server 8080

# Node (if available)
npx serve .
```

No compilation, linting, or test suite.

## Architecture

### index.html — Single-page layout

Five sections in order: `#about` (hero), `#projects`, `#certificates`, `#contact`, footer. Navigation links scroll to each section via anchor IDs.

The hero section has a two-column grid: left column is bio/CTA buttons, right column is skill badges organized by category (`.skill-group`).

Project cards use a `.project-card` wrapper with a colored accent bar (`::before` pseudo-element using inline `--accent` CSS variable), image, tech stack badges, and link buttons.

The certificates section is a CSS-only infinite-scroll carousel: cards are duplicated in the DOM so the loop is seamless.

### style.css — CSS custom properties theming

All colors are defined as variables at `:root`:
- `--color-bg: #080E1C` (dark navy background)
- `--color-primary: #14B8A6` (teal — primary actions/accents)
- `--color-secondary: #818CF8` (indigo)
- `--color-amber: #FBBF24` (yellow — highlight/warning states)

Button variants follow a `btn--*` modifier pattern (`btn--primary`, `btn--outline`, `btn--ghost`, `btn--disabled`).

### script.js — Three independent features

1. **Canvas particle network** (lines 8–89): 90 colored particles bounce inside a `<canvas>` layered behind the hero. Particles within 140px draw connecting lines. Redraws on `resize`.
2. **Mobile hamburger menu** (lines 91–107): toggles `.open` on the nav links container; auto-closes on link click.
3. **Active nav highlighting** (lines 109–126): `IntersectionObserver` on the four main sections updates `.active` on the matching nav anchor.

## Content & Images

Project screenshots and certificate images live in [Docs/Images/](Docs/Images/). When adding a new project card or certificate card, place the image there and reference it with a relative path like `Docs/Images/filename.ext`.
