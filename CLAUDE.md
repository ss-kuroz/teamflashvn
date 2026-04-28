# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a zero-build static HTML website serving as a proposals hub for Team Flash VN, a Vietnamese esports organization. The site consists of a landing page (`index.html`) linking to presentation pages (e.g., `media-2026-april-proposal.html`). All content is in Vietnamese (`lang="vi"`).

## Development

- **No build system, package manager, or compilation step.** Files are served directly as static assets.
- **To preview locally:** serve the repository root with any static file server, e.g. `npx serve` or `python -m http.server`.
- **No test suite, linter, or formatter is configured.**

## Architecture

- **Landing page (`index.html`):** semantic HTML with a proposal card grid. Each card links to a detailed proposal page via relative paths.
- **Proposal pages:** single-file HTML presentations using [Reveal.js](https://revealjs.com/) (loaded from CDN) with custom CSS in `css/proposal.css`. Slides are defined as `<section>` elements inside `<div class="reveal"><div class="slides">`.
- **Styles:** custom CSS in `css/index.css` (landing page) and `css/proposal.css` (presentations). Dark theme with orange/gold accents, glassmorphism cards, and responsive breakpoints.
- **Dependencies (all CDN):** Google Fonts (Inter, Montserrat), FontAwesome 6.4.0, Reveal.js 4.3.1.

## Important Patterns

- **Mobile handling for Reveal.js:** proposal pages include inline JavaScript that disables Reveal.js initialization on viewports `<= 768px`, falling back to natural vertical scroll. This is a deliberate workaround for Reveal.js portrait layout issues. The `proposal.css` file contains extensive `@media` queries that override Reveal.js layout classes with `!important` to force block display on mobile.
- **Adding a new proposal:** create an HTML page in the repository root, link to it from `index.html` by adding a card in the `.grid` container, and add corresponding styles to `css/proposal.css` if needed.
- **Proposals are self-contained:** each proposal page is a single HTML file with inline slide content and CDN-linked dependencies.
- **Design tokens:** the site uses a consistent dark theme with `#FF8C00` (orange), `#FFD700` (gold), `#4caf50` (green), `#2196f3` (blue), `#ff5252` (red), and `#b388ff` (purple) as accent colors. Reuse these when adding new components.

## Repository Notes

- `.gitignore` explicitly ignores `.github`, `.vscode`, and `.local`, yet these directories may have previously contained tracked files (force-added).
