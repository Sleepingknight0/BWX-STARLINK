# Starlink Mission Control

An interactive, browser-based 3D explainer for the Starlink network, combining a guided learning experience with a 24-hour constellation simulation.

[Open the live demonstration](https://starlink-plum.vercel.app)

## Overview

Starlink Mission Control presents satellite, terminal, gateway, coverage, and inter-satellite link concepts through a responsive mission-control interface.

The experience is delivered as static HTML, CSS, and JavaScript. It requires no application framework, compilation step, or server runtime.

The interface supports Thai and English. This documentation is maintained in English.

## Experience modes

### Guide mode

A nine-step interactive briefing introduces the path from a user terminal to low Earth orbit, ground gateways, and optical inter-satellite links.

### Simulation mode

A 24-hour model visualizes orbital motion, active network paths, coverage states, and multiple camera perspectives.

## Key capabilities

- Interactive Three.js globe and satellite scenes.
- Guided explanations with synchronized camera and network states.
- Time-based constellation simulation.
- Coverage visualization from local snapshot data.
- Desktop, mobile, mouse, keyboard, and touch support.
- Reduced-motion handling and accessible status patterns.
- Static deployment to common hosting providers.

## Technology

| Area           | Implementation                                       |
| -------------- | ---------------------------------------------------- |
| Application    | Static HTML, CSS, and JavaScript                     |
| 3D rendering   | Three.js r128 and WebGL                              |
| Map decoding   | PBF and Geobuf                                       |
| Runtime assets | Local images, video, GeoJSON, protobuf, and textures |
| Validation     | Playwright-based desktop and mobile checks           |
| Hosting        | Vercel or any static web host                        |

Three.js, PBF, and Geobuf are loaded from content delivery networks at runtime.

## Run locally

Serve the repository over HTTP:

```bash
python -m http.server 8000
```

Open `http://localhost:8000/index.html`.

Do not rely on `file://` for validation. Browser security rules and media loading can behave differently when the page is opened directly from disk.

The same server can be started through the package script:

```bash
npm run start
```

## Validation

Install the Playwright development dependency:

```bash
npm install
```

Keep the local server running on port `8000`, then run the automated check in another terminal:

```bash
npm run check
```

The check exercises desktop and mobile layouts, all guide steps, simulation behavior, accessibility-related states, page errors, and console errors.

Additional scripts capture focused mobile and satellite-model screenshots under `output/playwright/`.

## Data snapshots

The coverage map uses versioned files under `assets/data/` so normal page loads do not depend on live third-party requests.

Refresh the Starlink availability and Natural Earth snapshots with:

```bash
node scripts/snapshot-starlink-map.mjs
```

Review the generated files and `starlink-map-metadata.json` before committing. Availability data is time-sensitive and should always include a retrieval timestamp.

## Repository structure

```text
.
|-- index.html                         # Primary application
|-- starlink-3d-v1 (1).html           # Alternate standalone version
|-- assets/
|   |-- data/                          # Coverage and geographic snapshots
|   |-- gen/                           # Generated scene artwork
|   |-- real/                          # Reference photography
|   |-- tex/                           # Scene textures
|   `-- video/                         # Short visual sequences
|-- docs/
|   |-- starlink-specs-2026.md         # Sourced technical reference
|   `-- facts-registry-design.md       # Fact provenance design
|-- design-system/MASTER.md            # Visual and accessibility rules
|-- scripts/                           # Validation and snapshot utilities
|-- vercel.json                        # Static hosting and cache policy
`-- package.json                       # Local commands and validation dependency
```

`index.html` and the alternate HTML file are independent documents. A change to one is not automatically applied to the other.

## Documentation standards

Technical figures must be checked against [`docs/starlink-specs-2026.md`](docs/starlink-specs-2026.md) and labeled with appropriate provenance.

Follow [`design-system/MASTER.md`](design-system/MASTER.md) for visual tokens, responsive behavior, interaction targets, motion, and accessibility requirements.

Repository conventions are documented in [`AGENTS.md`](AGENTS.md) and [`CLAUDE.md`](CLAUDE.md).

## Deployment

The repository root is the static site root. `vercel.json` routes `/` to `index.html`, enables clean URLs, and applies long-lived cache headers to assets.

The project can also be deployed to Netlify, GitHub Pages, Cloudflare Pages, or another static host.

## Accessibility and quality checklist

- Verify keyboard navigation and visible focus states.
- Verify touch targets and narrow mobile layouts.
- Verify reduced-motion behavior.
- Confirm that all runtime assets load without errors.
- Confirm that status is never communicated by color alone.
- Review the browser console and network panel.
- Test both HTML variants when shared assets change.

## License

Released under the [MIT License](LICENSE).
