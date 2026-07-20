# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

WP Essentials — a static single-page site for an online store concept ("The online store designed for cadets"), aimed at West Point cadets and parents. There is no build tooling, package manager, or test suite; the entire site is a single `index.html` plus one stylesheet.

## Structure

- `index.html` — the only page. Contains a header (`.header`/`.logo-box`), a goldenrod nav bar (`.nav-box`/`.nav-list`) with placeholder links (currently pointing to `http://slither.com/io`), and a two-column flex layout (`.flex-row` with `.flex-text` and `.flex-image`) for the hero content and `Morrisfish.jpg`.
- `wp-essentials-stylesheet.css` — all styling, linked directly from `index.html`. No preprocessor, no build step — edit and reload.
- `Morrisfish.jpg` — hero image referenced by `index.html`.
- `.github/workflows/static.yml` — GitHub Actions workflow that deploys the entire repo root to GitHub Pages on every push to `main` (or manual dispatch). Anything committed to `main` goes live as-is.

## Development

There is no local server, bundler, or dependency install required. Open `index.html` directly in a browser (or serve the folder with any static file server) to preview changes.

Because deployment mirrors the repo root straight to GitHub Pages on push to `main`, changes pushed to `main` are live immediately — there is no staging step or build artifact to inspect first.

## Notes

- Nav links in `index.html` are placeholders and not yet pointed at real destinations.
