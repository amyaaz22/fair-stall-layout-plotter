# Fair Stall Layout Plotter

A true-to-scale floor plan tool for laying out vendor stalls for a food & fair event, built to eventually drive stall pricing off the plotted area.

## What it does

- Draws the hall to real scale (default 30.8 m × 20.5 m, editable) with a 60×60 cm tile grid as a placement reference.
- Click to drop points; consecutive clicks auto-chain into a measured line (live distance + bearing shown as you go).
- Type an exact distance + bearing instead of eyeballing a click.
- Close a traced path into a labeled stall — area (m²) and bounding size are computed automatically.
- Zoom, pan, and rotate the whole view to match the angle of a hand-drawn sketch.
- Select any stall to rotate it or check its area/dimensions; delete mode to remove dots or stalls.
- Snap to tile (0.6 m), metre, or off.

## Running it

No build step — it's a single static page.

```bash
# from this folder
python3 -m http.server 8000
# then open http://localhost:8000
```

Or just open `index.html` directly in a browser.

## Data storage

This started as a Claude artifact, where drawings are saved to a small shared store tied to that artifact (the `window.claude` runtime). Outside that environment — running it locally like this — the page automatically falls back to your browser's `localStorage`, so your layout is saved on this device only. See `makeLocalDoc()` and `boot()` in `index.html` if you want to swap in a real backend (e.g. so the layout and stall statuses are shared across a team, not just one browser).

## Where this is headed

Next planned step: use each stall's computed area (already shown per-stall and as a running total) to calculate stall prices — e.g. a rate per m², possibly varying by zone or aisle. That logic doesn't exist yet; the layout data (`hall`, `points`, `stalls`) is the input it'll need.

## Working on this with Claude Code

Open this folder with `claude` and describe what you want changed — e.g. "add a price-per-m² field to each stall and show the total", "add an export to CSV of stall number + area", "replace localStorage with a small backend so multiple people can edit the same layout". The whole app is in `index.html`: plain HTML/CSS/JS, SVG for the drawing canvas, no framework or build tooling.
