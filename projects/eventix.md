---
title: Eventix
created: 2026-07-06
tags:
  - project
  - side-project
status: active
source_path: /home/mada/side_projects/eventix
---

# Eventix

## Outcome

Build and maintain a Go REST API for event organization and ticketing with authentication, SQLite persistence, mock payments, ticket reservations, refunds, background jobs, and an admin risk dashboard.

## Context

- Local path: `/home/mada/side_projects/eventix`
- Related map: [[projects]]
- Stack: Go, SQLite, Chi, JWT, Docker Compose
- Main entry points: `cmd/server`, `cmd/worker`

## Current capabilities

- Attendee and organizer authentication
- Event and ticket-tier management
- Order creation with 10-minute ticket reservations
- Mock payment flow that issues tickets
- Refund request and organizer/admin review flow
- Ticket QR code generation and check-in
- Background worker for emails, reservation expiration, and risk analysis
- Admin risk dashboard at `/admin/risk`

## Useful commands

```bash
make dev
make worker
make test
make test-race
docker compose up --build
```

## Next actions

- [ ] Review the current project status and define the next milestone.
- [ ] Capture any known bugs, design decisions, or deployment notes.
- [ ] Decide whether this project is still active, paused, or ready to archive.

## Open questions

- What is the intended deployment target?
- Is the next focus API completeness, frontend polish, reliability, or deployment?
- Which flows still need manual or automated verification?

