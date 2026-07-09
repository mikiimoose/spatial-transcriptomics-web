# Spatial TME Atlas

An interactive 3D website for exploring the tumor microenvironment of biliary tract
cancer (10x Visium spatial transcriptomics, GEO **GSE316402**). Replicate tissue
sections are stacked into a navigable pseudo-3D model, and matched **pre- vs
post-treatment** biopsies are shown side by side with synced rotation.

## Features

- **Two synced 3D stacks** — baseline vs on-treatment, drag to rotate both together, scroll to zoom.
- **Six color modes** — cell-type class (tumor / immune / stromal / transitional), invasive front, and the checkpoint (PD1/PD-L1), CXCL12–CXCR4, TGF-β and TLS signaling scores.
- **Treatment-response comparison** — tumor area, immune infiltration, interface size and interface signaling, with post − pre deltas.
- **Patient selector**, adjustable point size, section spacing, score threshold, and section outlines.

Built with [Three.js](https://threejs.org/). No build step — it's a single static HTML file.

## Run locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy (GitHub Pages)

1. Push this repository to GitHub.
2. Repo **Settings → Pages → Build and deployment**.
3. Source: **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. Your site publishes at `https://<user>.github.io/<repo>/`.

`index.html` is fully self-contained (the 3D runtime and libraries are inlined), so
no other files are required to serve the site.

## Data note

The spot coordinates and expression/pathway scores shown are **illustrative** — they
are generated to match the structure of the analysis pipeline (spot classes, invasive
front, interface signaling, TLS). To use real data, export the pipeline's `spot_table`
(spot `x/y/z`, `spot_class`, and the `pw_*` / `sig_TLS` score columns) and replace the
`generateSpots()` routine in the source with a loader for those values.

## Repo contents

- `index.html` — the built, self-contained site. **This is what gets served.**
- `src/Tumor Atlas.dc.html` — human-readable source (markup + the Three.js logic class).
- `src/support.js` — small runtime the source needs to run when opened directly.

To tweak the visuals or logic, edit the source in `src/` (open
`src/Tumor Atlas.dc.html` in a browser to preview), then re-inline it into a fresh
`index.html` for deployment.
