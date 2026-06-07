# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

A static memorial website for Rigoberto Vito Pernía — first mayor of Municipio Autónomo Seboruco, Táchira, Venezuela. Written entirely in Spanish. No build tools, no package manager, no framework — pure HTML, CSS, and vanilla JS.

## Deployment

Push to `main` and Netlify deploys automatically. No build step.

```bash
git add <files>
git commit -m "descripción del cambio"
git push
```

To preview locally: open `index.html` directly in a browser, or use any static file server:

```bash
python3 -m http.server 8080
```

## File structure

| File | Purpose |
|------|---------|
| `index.html` | Single-page site with all four sections |
| `styles.css` | All styling (Spectral serif + JetBrains Mono, `oklch()` colors) |
| `image-slot.js` | Custom `<image-slot>` web component |
| `assets/` | Site images (portrait, book covers, town photos) |

## Sections in `index.html`

- `#inicio` — Hero with portrait
- `#sobre` — Biography, facts, and his written words
- `#seboruco` — Timeline, photo carousel (with `<image-slot>` slots), and map
- `#libros` — Two books; first awaits PDF, second links to Google Drive
- `#contacto` — `mailto:` form + contact info

## The `<image-slot>` component

Defined in `image-slot.js`. Allows drag-and-drop image replacement and persists state to `.image-slots.state.json` via `window.omelette.writeFile` (omelette canvas host bridge). Outside that runtime the slots are read-only. The component is a custom element with shadow DOM — do not style it from outside without using `::part()` selectors.

Attributes: `id` (required for persistence), `shape` (`rect`|`rounded`|`circle`|`pill`), `radius`, `mask`, `fit`, `placeholder`, `src`.

## Pending task (from README)

First book PDF is not yet digitized. When the PDF is available, find `Seboruco parte de su historia` in `index.html` and replace the `.btn.muted` disabled link with an active download link matching the second book's pattern.

## Design tokens

Defined as CSS custom properties on `:root` in `styles.css`. Color palette uses `oklch()`. Main colors: `--forest` (mountain green), `--paper` (warm off-white), `--ink` (dark green-tinted ink). Fonts: `--serif` (Spectral) for body, `--mono` (JetBrains Mono) for labels/eyebrows.
