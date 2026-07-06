---
title: Mini PaaS
created: 2026-07-06
tags:
  - project
  - side-project
status: active
source_path: /home/mada/side_projects/mini-paas
---

# Mini PaaS

## Outcome

Build a small platform-as-a-service in vertical slices, currently focused on a Go API, React/Vite frontend, GitHub App repository selection, and simulated deployment records with log streaming.

## Context

- Local path: `/home/mada/side_projects/mini-paas`
- Related map: [[projects]]
- Stack: Go, SQLite, React, Vite, TypeScript, GitHub App integration
- Main entry points: `backend`, `frontend`

## Current capabilities

- User registration, login, logout, and session-backed `GET /api/me`
- App CRUD
- GitHub App install, callback, setup, installation linking, repository listing, and branch listing
- Simulated app deployments
- Deployment records and log streaming over Server-Sent Events
- Frontend routes for login, registration, dashboard, GitHub connection, app creation, app detail, and deployment detail

## Known milestone boundary

Real Docker builds, repository cloning, Caddy updates, and runtime logs are intentionally not implemented in the current milestone.

## Useful commands

```bash
cd backend
go test ./...
go run ./cmd/api
```

```bash
cd frontend
npm install --cache .npm-cache
npm run dev
npm run build
```

## Next actions

- [ ] Define the next milestone after simulated deployments.
- [ ] Decide when to introduce real build and runtime infrastructure.
- [ ] Capture GitHub App setup decisions and gotchas.

## Open questions

- What is the minimum real deployment path: Docker build first, routing first, or logs first?
- Should the next slice target local-only deployments or a remote server?
- What level of isolation is required before deploying real user apps?

