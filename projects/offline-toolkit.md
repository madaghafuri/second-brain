---
title: offline-toolkit
created: 2026-07-18
tags:
  - project
  - side-project
  - pwa
  - privacy
status: active
source_path: /home/mada/side_projects/offline-toolkit
---

# offline-toolkit

## Outcome

Client-side document/image toolkit — watermark, split, and convert PDFs and images entirely in the browser. Zero runtime egress, offline-first PWA deployed on Cloudflare Pages.

## Context

- Local path: `/home/mada/side_projects/offline-toolkit`
- Related map: [[projects]]
- Stack: React 18 + TypeScript + Vite, Vitest, Cloudflare Pages (static only)
- Deploy: static export to `dist/`, deployed via Wrangler
- Key dependencies: `pdf-lib`, `pizzip`, `fflate`, React Router v6

## Core operations (v1 scope, ADR-0001)

1. **Image watermark** — raster, drawn on `<canvas>`
2. **PDF split** — structured PDF, `pdf-lib`
3. **Image → PDF convert** — single raster asset wrapped into a PDF page
4. **Watermark on PDF** — overlay drawn per page via `pdf-lib`
5. **Watermark on Office (docx only at v1)** — zipped-XML, `pizzip` engine

Deferred: `.pptx` and `.xlsx` watermark (must slot behind same `ZippedXml` adapter seam)

## Architecture (ADR-0006)

Three deep modules, each with a single public function:

- `Watermark.apply(file, ink)` — abstracts over raster / PDF / zipped-XML via internal adapters
- `PdfSplit.split(file, spec)` — PDF page range extraction
- `ImageToPdf.convert(files, spec)` — images → multi-page PDF

All processing runs in a **Web Worker** (ADR-0007) using OPFS for large blobs; UI never imports `pdf-lib` / `pizzip` directly.

## Privacy guarantees (ADR-0002, ADR-0003)

- **Zero runtime egress**: CSP `connect-src 'none'` enforced by browser; CI guard (`npm run lint:no-external-urls`) fails build if any `http(s)://` URL appears in build output
- **No CDN deps at runtime**: all deps bundled; SRI hashes injected at build (`scripts/add-sri.mjs`)
- **Service worker** caches build assets only — never user files
- **No persistence opt-in**: settings (tool params only) in `localStorage` opt-in only (ADR-0010); OS theme preference only (ADR-0012)

## Development

```bash
npm install
npm run dev          # Vite dev server
npm run typecheck    # tsc --noEmit
npm run test         # vitest run
npm run test:watch   # vitest watch
npm run build        # tsc + vite build -> dist/ + SRI
npm run check:all    # typecheck + test + build + no-external-urls
```

Run `npm run check:all` before pushing; CI runs the same.

## Testing discipline (ADR-0011)

- **Test surface = public surface**: tests call `apply`, `split`, `convert` only; never import adapters/internal helpers
- **Golden-file snapshots** in `__snapshots__/` pin content-derived measures (page geometry, zip entries) — not raw bytes (pdf-lib timestamps)
- **Invariants** (page-count preservation, header injection) asserted inline
- **No egress tests** — CSP/CI guard is the privacy test

## ADR index

See `docs/adr/README.md` for the full decision tree. Key ADRs:

| ADR | Title |
|-----|-------|
| 0001 | Toolkit scope (v1) |
| 0002 | Static SPA, zero runtime egress, offline PWA |
| 0003 | Privacy proof: strict CSP + bundled deps + SRI + CI guard |
| 0004 | Tech stack: Vite + React + TS + vitest on Cloudflare Pages |
| 0005 | Library strategy: pdf-lib + Canvas + pizzip |
| 0006 | Module architecture: deep Watermark + PdfSplit + ImageToPdf |
| 0007 | Memory strategy: Web Worker + OPFS + blob-URL delivery |
| 0008 | UX surface: unified hub + per-tool workbench, no pdf.js |
| 0009 | Ink representation: target-agnostic watermark payload |
| 0010 | Settings persistence: tool params only, opt-in, localStorage |
| 0011 | Testing: interface + golden snapshots + invariants |
| 0012 | Hub hero + system-following light/dark theme |

## UX surface (ADR-0008, ADR-0012)

- **Unified hub** with hero + system-following light/dark theme (CSS-only, `prefers-color-scheme`, no JS toggle)
- **Per-tool workbenches** for each operation
- **No pdf.js** — PDF rendering only via canvas overlays

## Current status

- v1 scope defined (ADR-0001)
- Architecture, privacy model, tech stack, testing discipline locked (ADRs 0002-0012)
- Core modules implemented with golden-snapshot tests
- PWA manifest + service worker configured
- CI pipeline: typecheck → test → build → SRI → no-external-urls guard

## Next actions

- [ ] Implement Watermark workbench UI (ink editor, position/tile presets)
- [ ] Implement PDF Split workbench (page range selector, preview)
- [ ] Implement Image → PDF workbench (multi-image, page size/orientation)
- [ ] Wire worker + OPFS pipeline end-to-end
- [ ] PWA install prompt + offline verification
- [ ] Deploy to Cloudflare Pages (static export)

## Open questions

- Should `.pptx`/`.xlsx` watermark be v1.1 or v2? (ADR-0001 defers behind same `ZippedXml` adapter)
- Worker memory ceiling for large PDFs — OPFS streaming threshold?
- Accessibility audit for workbench controls (ink position presets, tile modes)