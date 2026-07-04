# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

Static marketing site for Beaver Advisors (financial advisory business), in Spanish. There is no build system, package manager, bundler, or test suite — each page is a single self-contained `.html` file with all CSS inlined in a `<style>` block in the `<head>` and no external JS framework.

Pages:
- `index.html` — the main landing page (hero, about, services, testimonials, founder, contact — these are anchor sections, not separate routes).
- One HTML file per service, each linking back to `index.html` anchor sections (`#about`, `#services`, `#testimonials`, `#founder`, `#contact`) via the nav bar:
  - `arranca-bien.html`
  - `chill-books.html`
  - `control-financiero.html`
  - `diagnostico-financiero.html`
  - `estructuracion-financiera.html`
  - `plan-financiero-anual.html`
  - `preparacion-banco-inversionista.html`

## Development

There are no build/lint/test commands — edit the HTML files directly and open them in a browser (or use a local static server) to preview.

The GitHub CLI (`gh`) is available in this environment for working with issues, PRs, and the repo on GitHub.

## Architecture / conventions

- Each service page duplicates the same CSS (custom properties for colors, nav, hero, section styles) inline rather than sharing a stylesheet — when changing shared visual style (colors, nav, typography), the same edit must be repeated across all files.
- Design tokens are defined as CSS custom properties at the top of each page's `:root` block (e.g. `--purple`, `--teal`, `--lavender`, `--ink`, `--cream`), and are consistent across pages.
- Fonts are loaded from Google Fonts CDN: `Playfair Display` (serif, headings) and `DM Sans` (sans-serif, body).
- Navigation on service pages links back to anchors in `index.html` (`index.html#services`, etc.), not to standalone pages — `index.html` is the only page with real in-page sections.
- Page titles follow the pattern `<Service Name> · Beaver Advisors`; `index.html`'s title is the full tagline.
