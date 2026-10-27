## Purpose
Guidance for AI coding agents working on this repo: a small static website (iRDC, the NE300 interactive reference data card) hosted on Netlify. There is no build step.

## Key files
- `index.html`: the whole app. Popup UI (`#equationPopup`), MathJax setup, the popup renderer and one delegated click handler.
- `img/rdc_both.svg`: the card artwork. Clickable hotspots are invisible `rect` elements with ids `prc-<n>` (e.g. `prc-13`).
- `equations.json`: popup content, one entry per hotspot:
  `{ "id": "prc-<n>", "column": "left|middle|right", "title": "...", "equations": ["\\[...\\]"], "variables": [{ "sym": "\\(...\\)", "def": "... [units]" }], "description": [{ "p": "..." } or { "eq": "\\[...\\]" }] }`
- `_headers`: Netlify cache rules.

## How it works
On load, `index.html` fetches the SVG and `equations.json`, inserts the SVG into `#rdcContainer`, and adds one click listener on the SVG. Clicking an element whose id starts with `prc-` renders that entry into the popup and typesets it with MathJax (pinned to 3.2.2). `column` only affects popup placement: `right` places it toward the centre-left; `left` and `middle` place it beside the click.

## Adding or editing an equation
1. Edit or add the entry in `equations.json`. LaTeX goes in `\\( \\)` (inline) or `\\[ \\]` (display), with backslashes escaped for JSON.
2. For a new equation, also draw an invisible rect over it in `img/rdc_both.svg` (Inkscape) with the matching `prc-<n>` id.

## Local preview
```bash
python3 -m http.server 8000
# open http://localhost:8000/
```
The page must be served over HTTP (it uses `fetch`), not opened as a file. A missing hotspot id is reported in the browser console.

## Gotchas
- Popup content is inserted with `innerHTML`; do not put `<script>` or `<style>` in `equations.json`.
- Keep embedded images in the SVG small; the whole SVG is downloaded on every first visit.
