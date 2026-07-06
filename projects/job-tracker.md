---
title: Job Tracker
created: 2026-07-06
tags:
  - project
  - side-project
status: active
source_path: /home/mada/side_projects/job-tracker
---

# Job Tracker

## Outcome

Build and maintain a Cloudflare Workers application that scans Gmail, extracts job applications, tracks application statuses, applies Gmail labels, shows analytics, creates reminders, and exports XLSX files.

## Context

- Local path: `/home/mada/side_projects/job-tracker`
- Related map: [[projects]]
- Stack: Cloudflare Workers, Cloudflare D1, static browser UI, Google OAuth, Gmail API
- Main entry points: `src/worker.js`, `public/app.js`

## Current capabilities

- Google OAuth and Gmail API integration
- Inbox and Sent mail scanning
- Job application extraction
- Status tracking
- Gmail label application
- Analytics
- No-response reminders
- XLSX export
- Local D1 migrations

## Useful commands

```bash
npm run dev
npm run db:migrate:local
npm test
npm run typecheck
npm run build
npm run deploy
```

## Next actions

- [ ] Review current production readiness.
- [ ] Capture any Gmail OAuth setup notes that are easy to forget.
- [ ] Decide whether analytics, reminder quality, or deployment is the next priority.

## Open questions

- Is this intended for personal use only or for multiple users?
- What labels and statuses should be considered canonical?
- What reminder timing should be the default?

