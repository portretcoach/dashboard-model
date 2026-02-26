# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-page client dashboard for kids portrait photography sessions at Studio Iris van 't Riet. Clients who book a session receive this page with preparation info, styling tips, location, pricing, and terms.

## Architecture

- **Single HTML file** (`index.html`, ~1360 lines): all HTML, CSS, and JavaScript inline. No build tools, no framework. Language: Dutch (`lang="nl"`).
- **Iframe embed**: designed to be embedded in the main irisvantriet.nl website. JS sends `postMessage` to parent: `{ type: 'resize', height }` and `{ type: 'scrollToTop' }`. A `MutationObserver` auto-updates height on DOM changes.
- **Tab navigation**: vanilla JS toggles `.active` class on `.section` divs. Nav buttons have `data-section` attributes matching section `id` values. Sections: stappenplan, voorbereiding, kleding, sessie, locatie, nadesessie, prijzen, delijst, contact, voorwaarden.
- **Images**: all portfolio and location photos are local in `images/`. No external CDN dependencies.

## Running Locally

```bash
cd "/Users/irisvalentina/Desktop/dashboard kinderportret"
python3 -m http.server 8080
```
Then open `http://localhost:8080`

## Design Tokens

CSS custom properties in `:root`:
- `--teal-dark: #264d5e` (primary dark blue, matches irisvantriet.nl header)
- `--teal: #2f6178` and `--teal-light: #3a7a94` (lighter variants)
- `--terra: #b8897a` (accent, used for headings and highlights), `--terra-light`, `--terra-pale` (lighter variants)
- `--cream: #f5f0eb` (page background), `--cream-dark: #ebe3db`
- `--gold: #c9a96e` (used in header gradient accent line)
- Text colors: `--text-dark: #2a2a2a`, `--text-medium: #5a5a5a`, `--text-light: #8a8a8a`
- Fonts: Playfair Display (headings) + Inter (body), loaded from Google Fonts

## Key CSS Classes

- `.card` — content blocks within sections
- `.highlight` — dark teal background boxes; text inside uses `rgba(255,255,255,0.85)`
- `.tip` — terra-accented tip boxes
- `.do-dont` with `.do-col` / `.dont-col` — green/red comparison columns (Wel/Liever niet)
- `.cool-col` / `.warm-col` — blue/gold comparison columns (for color type advice)
- `.color-grid` / `.color-swatch` — grid of color circles with labels
- `.styling-photos` — 2-column image grid for portfolio photos; add `.trio` class for 3-column
- `.price-table` — styled pricing tables

## Content Guidelines

- All text is written in **first person** (ik-vorm), as if written by Iris herself
- No em-dashes (—) anywhere in the content
- Text on dark (teal) highlight boxes uses `rgba(255,255,255,0.85)` for softer contrast
- The styling guide content was adapted from an adult/entrepreneur version for children
