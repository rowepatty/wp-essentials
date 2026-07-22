# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

WP Essentials — a static site for an online store concept ("The online store designed for cadets"), aimed at West Point cadets and parents. There is no build tooling, package manager, or test suite: a handful of hand-written HTML pages share one stylesheet.

## Structure

Five pages, each linking `wp-essentials-stylesheet.css`:

- `index.html` — home page. Header, nav, and a two-column flex hero (`.flex-row` with `.flex-text` and `.flex-image`) holding three headline/paragraph pairs and `Morrisfish.jpg`.
- `recommended-items.html` — the single shopping page. Uses the `.category-page` structure: `.category-heading`, `.category-description`, and `.category-section` blocks, each containing a horizontally scrolling `.product-row` of `.product-slot` cards (`.product-info` + independently scrolling `.product-review`). All product content is currently placeholder.
- `blog-posts.html` — blog index. A `.content-id` title bar above a `.blog-list-container` of `.blog-list` rows, one per post.
- `blog-first-post.html` — sample blog post, using `.blog-container` / `.blog`. Post filenames use a `blog-` prefix so posts group together.
- `about-the-website.html` — About page. Header and nav only; body is intentionally empty pending real content.

Assets: `wp-essentials-logo.png` (header logo, on every page) and `Morrisfish.jpg` (home hero).

`.github/workflows/static.yml` deploys the entire repo root to GitHub Pages on every push to `main` (or manual dispatch).

## Shared header and nav

Every page opens with the same two blocks — a `.header`/`.logo-box` containing the logo image linked to `index.html`, then a goldenrod `.nav-box`/`.nav-list` with exactly four links:

Home → `index.html` | Blog Posts → `blog-posts.html` | Recommended Items → `recommended-items.html` | About the Website → `about-the-website.html`

**There is no templating or includes.** The header and nav are copy-pasted into every page, so any change to either must be applied to all five files by hand. When adding a page, copy the header/nav block verbatim from an existing page rather than writing it fresh.

## Development

No local server, bundler, or dependency install. Open `index.html` in a browser, or serve the folder with any static file server.

Because deployment mirrors the repo root straight to GitHub Pages, anything pushed to `main` is live immediately — there is no staging step or build artifact to inspect first. Multi-file changes that leave nav links dangling (adding a page, renaming one) should be committed and pushed as a single complete change, not piecemeal.

Useful check before pushing — resolve every internal link:

```sh
for f in *.html; do grep -oh 'href="[^"]*"' "$f" | sed 's/href="//;s/"//' | while read t; do
  case "$t" in http*|"") ;; *) [ -f "${t%%#*}" ] && echo "OK $f -> $t" || echo "BROKEN $f -> $t";; esac
done; done | sort -u
```

## Notes

- Product entries, reviews, prices, blog filler text, and the About page body are all placeholder content awaiting real copy.
- The stylesheet contains two commented-out blocks (an early `.logo-box` text treatment and a `.content-box` rule) kept from earlier iterations.
- The site previously had five per-milestone shopping pages (`academic-year`, `cbt`, `cft`, `air-assault`, `cldt`). They were byte-identical apart from their headings and were consolidated into `recommended-items.html`; the milestone concept now lives in blog posts instead.
