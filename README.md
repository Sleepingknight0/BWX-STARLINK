# Starlink Mission Control — 3D Explainer

Static, browser-based Starlink 3D explainer (Thai + English UI).

**[Live demo →](https://starlink-plum.vercel.app)**

- **Guide mode** — 9-step interactive brief (Dishy → LEO → gateway → ISL)
- **Simulation mode** — 24-hour orbit model of the working constellation

Open [index.html](./index.html) over HTTP (not `file://`).

## Local

```bash
python -m http.server 8000
# → http://localhost:8000/index.html
```

No build step. Three.js, pbf, and geobuf load from CDNs.

## Deploy

Static hosting (Vercel, Netlify, GitHub Pages). Root is the site root; `vercel.json` sets clean URLs and asset caching.

## Docs

- `docs/starlink-specs-2026.md` — sourced technical reference; every figure carries a provenance tag, check numbers against it before changing them
- `design-system/MASTER.md` — color tokens, typography, spacing, and the accessibility checklist; follow it for any UI change
- `AGENTS.md` / `CLAUDE.md` — project conventions for agents

Refresh the snapshotted coverage and Natural Earth data in `assets/data/` with:

```bash
node scripts/snapshot-starlink-map.mjs
```

## License

MIT — see [LICENSE](LICENSE).
