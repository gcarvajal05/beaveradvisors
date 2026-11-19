# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

Static marketing site for Beaver Advisors (financial advisory business), in Spanish. There is no build system, package manager, bundler, or test suite — each page is a single self-contained `.html` file with all CSS inlined in a `<style>` block in the `<head>` and no external JS framework.

Pages:
- `index.html` — the main landing page (hero, about, services, testimonials, founder, contact — these are anchor sections, not separate routes).
- One HTML file per service, each linking back to `index.html` anchor sections (`#about`, `#services`, `#testimonials`, `#founder`, `#contact`) via the nav bar:
  - `arranca-bien.html` (displayed as "Despegar")
  - `chill-books.html` (displayed as "Contabilidad Mensual")
  - `control-financiero.html`
  - `diagnostico-financiero.html`
  - `estructuracion-financiera.html`
  - `plan-financiero-anual.html`
  - `preparacion-banco-inversionista.html`
  - `cfo-estrategico.html`
  - `auditoria-financiera.html`
  - `auditoria-interna.html`
  - `certificacion-ingresos.html`

## Development

There are no build/lint/test commands — edit the HTML files directly and open them in a browser (or use a local static server) to preview.

The GitHub CLI (`gh`) is available in this environment for working with issues, PRs, and the repo on GitHub.

## Architecture / conventions

- Each service page duplicates the same CSS (custom properties for colors, nav, hero, section styles) inline rather than sharing a stylesheet — when changing shared visual style (colors, nav, typography), the same edit must be repeated across all files.
- Design tokens are defined as CSS custom properties at the top of each page's `:root` block, and are consistent across pages. **Token names are legacy from the previous brand and no longer describe the color** — see "Brand identity" below for what each one actually holds.
- Fonts are loaded from Google Fonts CDN: `Manrope` only (all weights 300–800).
- Navigation on service pages links back to anchors in `index.html` (`index.html#services`, etc.), not to standalone pages — `index.html` is the only page with real in-page sections.
- Page titles follow the pattern `<Service Name> · Beaver Advisors`; `index.html`'s title is the full tagline.

## Brand identity

Source files live outside the repo (the brandboard PDF and logo PNG/JPG/AI exports). The site uses a dark navy theme built from the brand palette:

| Brand color | Hex | Held by token(s) | Used for |
|---|---|---|---|
| Azul marino | `#0B1A2B` | `--ink` | page background (cards `--off` `#112338`, hover `--mid` `#1B3350`) |
| Lima | `#D7FF5C` | `--teal` | primary CTA buttons (`.nav-cta`, `.btn-gold`, `.btn-teal`, `.form-submit`), labels, numbers, check/arrow bullets |
| Lila | `#ABA6FF` | `--purple`, `--gold`, `--lavender` | accent words (`em`, hero rotator), secondary button (`.btn-purple`), highlighted cards |
| Celeste | `#8FC7F4` | `--lavender-2`, `--mint` | decorative only (hero art) |

- Text on lima/lila backgrounds must be navy (`var(--ink)`), never white — white fails contrast on both.
- Manrope has no true italic, so `font-style` is `normal` everywhere (a global `em{font-style:normal}` rule keeps the UA default from faux-italicizing); emphasis is done with color instead.
- Logo assets are in `assets/`: `logo-white.png` (wordmark for dark backgrounds, used in every nav and footer as an `<img>`; `en/` pages reference it as `../assets/logo-white.png`) and `favicon.png`. Only the white wordmark and favicon are used on the dark site; other logo variants (black/navy wordmark, isotipo) exist in the brand files if a light surface is ever needed.
- The homepage hero has no photo. `.hero-art` is an inline SVG built from the brand's graphic elements (lilac arch, thin lime arc, lime dot, celeste quarter-circle); on screens ≤900px only the faint arch remains so text stays legible. `index.html` and `en/index.html` each carry their own copy.

## English version (`en/`)

- `en/` mirrors the root exactly — one English translation per Spanish page, same filenames (`en/index.html`, `en/chill-books.html`, etc.), so relative links within a language folder (`index.html`, `chill-books.html`, `#services`, ...) resolve correctly without a `../` or `en/` prefix.
- Each page's `<nav>` has a `.lang-switch` control (in `.nav-right`, next to `.nav-links`) that links to the other language's version of the *same* page: root pages link to `en/<file>`, `en/` pages link back to `../<file>`.
- When editing content on a Spanish page, make the matching edit on its `en/` counterpart (and vice versa) to keep the two versions in sync — there is no shared content source, so translations can drift silently otherwise.
- `en/index.html`'s word-rotator script (`const words = [...]`) must stay translated in parallel with the root's.
