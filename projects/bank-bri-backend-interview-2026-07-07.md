---
title: Bank BRI backend interview
created: 2026-07-06
interview_date: 2026-07-07
interview_time: 10:00
timezone: Asia/Jakarta
company: Bank BRI
group: APP Group
role: Backend Developer
tags:
  - interview
  - career
  - backend
status: active
---

# Bank BRI backend interview

> [!important]
> Interview: Tuesday, 2026-07-07 at 10:00 AM WIB / Jakarta time.

## Interview details

- Company: Bank BRI
- Group: APP Group
- Role: Backend Developer
- Format assumption: technical + HR
- Related projects to discuss: [[eventix]], [[mini-paas]]
- Related map: [[projects]]

## Company context

- BRI is one of Indonesia's largest government-owned banks and was established in Purwokerto on 1895-12-16. Source: [BRI company profile](https://bri.co.id/web/guest/info-perusahaan).
- BRI emphasizes broad banking services, prudent governance, large real-time online network coverage in Indonesia, and continued product innovation. Source: [BRI homepage](https://bri.co.id/).
- BRImo is BRI's financial super app for customer transactions, including onboarding, payments, purchases, investment, insurance, financial tracking, international transfers, and overseas QR payments. Source: [BRImo](https://bri.co.id/web/guest/brimo).
- BRIAPI exposes banking APIs for partner integrations, including Direct Debit, BRIZZI, BRIVA, BaaS account-opening services, sandbox access, documentation, SDK/dev tooling, verification, and real-time monitoring. Source: [BRIAPI](https://developers.bri.co.id/en).

## Positioning

Short answer for "tell me about yourself":

> I am a backend-focused developer who likes building practical systems end to end: API design, authentication, database modeling, background jobs, and deployment flow. In my side projects, I built systems like Eventix, a Go ticketing API with reservations, payments, refunds, workers, and risk checks, and Mini PaaS, a Go and React platform prototype with GitHub App integration and deployment log streaming. For BRI, I am interested in backend work where reliability, secure data handling, and clear integration boundaries matter because banking systems serve many users and partners.

Why BRI:

> I am interested in BRI because it is a large Indonesian bank with real digital banking products such as BRImo and partner-facing APIs through BRIAPI. Backend work there is not only CRUD; it needs reliability, security, auditability, and good integration design. Those are the parts of backend engineering I want to grow in.

Why Backend Developer:

> Backend fits me because I like designing the logic behind a product: data models, APIs, transactions, authentication, background processing, and failure handling. I enjoy making systems predictable and maintainable.

## Backend topics to review

### REST API design

- Resource naming: `/users`, `/orders`, `/tickets`, `/deployments`.
- Use methods consistently: `GET`, `POST`, `PATCH` or `PUT`, `DELETE`.
- Return clear status codes: `200`, `201`, `400`, `401`, `403`, `404`, `409`, `500`.
- Validate input at the boundary.
- Keep error responses consistent.
- Design idempotency for payment-like or retryable operations.

### Authentication and authorization

- Authentication answers: "Who are you?"
- Authorization answers: "What are you allowed to do?"
- Common mechanisms: sessions, JWT, OAuth, API keys, signed requests.
- Banking relevance: protect account data, enforce role permissions, audit sensitive actions, avoid leaking tokens, rotate secrets.
- Be ready to explain organizer/admin/user role checks from [[eventix]].

### Database and SQL

- Explain schema design from entities and relationships.
- Know indexes for lookup-heavy fields.
- Know transactions for multi-step changes.
- Know constraints for data integrity.
- Banking relevance: money-like workflows must avoid partial updates and race conditions.

### Transactions and consistency

- Use transactions when multiple writes must succeed or fail together.
- Example: order payment should update order status, issue tickets, reduce inventory, and enqueue notification consistently.
- Handle duplicate requests with idempotency keys or unique constraints.
- Consider optimistic locking or row-level locking for inventory or balance-like records.

### Background jobs and queues

- Use background workers for slow or retryable work: email, notification, expiration, reconciliation, risk checks.
- Keep request-response paths fast.
- Track job status, retries, and failures.
- Make jobs idempotent because retries can happen.

### Logging and monitoring

- Log request IDs, user IDs when safe, operation names, latency, and failures.
- Do not log secrets, passwords, tokens, full card numbers, or sensitive personal data.
- Monitor error rate, latency, queue depth, database errors, and external API failures.

### Security basics

- Hash passwords; never store plaintext passwords.
- Use least privilege for roles and database access.
- Validate and sanitize inputs.
- Protect against SQL injection with parameterized queries.
- Use HTTPS, secure cookies, token expiration, and secret rotation.
- Avoid exposing implementation details in public error messages.

### Scalability basics

- Start with clean architecture and database indexes.
- Add caching for read-heavy data after measuring.
- Use queues for asynchronous work.
- Split services only when boundaries are clear and operational maturity exists.
- For banking: correctness and observability usually matter more than premature complexity.

## Project stories

### Story 1: Eventix API design

- Situation: Needed an event ticketing backend with attendees, organizers, events, ticket tiers, orders, payments, tickets, refunds, and admin risk review.
- Task: Design a maintainable backend with clear API boundaries and data consistency.
- Action: Built a Go REST API with feature-first structure, handlers, services, repositories, JWT auth, SQLite, ticket reservations, mock payment, refunds, background worker, QR ticketing, and risk assessment.
- Result: The project can model realistic ticketing flows and gives me concrete experience with transactions, authorization, background jobs, and failure cases.

Use this when asked:

- "Tell me about a backend project."
- "How do you design APIs?"
- "How do you handle transactions?"
- "How do you handle background jobs?"

### Story 2: Eventix ticket reservation consistency

- Situation: Ticket inventory should not be oversold when users create orders.
- Task: Reserve inventory during order creation and release it if payment is not completed.
- Action: Modeled reservations with a deadline, used payment against the existing hold, and used a worker to expire reservations and restore inventory.
- Result: The design separates reservation, payment, and expiration while protecting inventory consistency.

Use this when asked:

- "How do you avoid race conditions?"
- "How do you model payment-like flows?"
- "How would you design reliable order processing?"

### Story 3: Mini PaaS deployment flow

- Situation: Wanted to prototype a platform that connects GitHub repositories and creates deployments.
- Task: Build the backend and frontend flow before implementing real Docker builds and runtime infrastructure.
- Action: Built auth, app CRUD, GitHub App installation/repository selection, simulated deployment records, and Server-Sent Events log streaming.
- Result: The project demonstrates incremental delivery: define the interface and user workflow first, then replace simulation with real build/runtime steps later.

Use this when asked:

- "How do you approach a large feature?"
- "How do you design for future implementation?"
- "Have you worked with external integrations?"

## HR and behavioral answers

### Strengths

> I am comfortable breaking a problem into data model, API, business logic, and failure cases. I also like making the system understandable through clear structure and tests.

### Weakness

> Sometimes I can spend too much time improving structure before the feature is fully validated. I am working on balancing that by defining a small milestone first, shipping that, then refactoring based on what the feature actually needs.

### Why should we hire you?

> I can contribute as a backend developer who understands API design, data consistency, authentication, and practical implementation. I also learn independently through real projects, so I can ramp up on the team's stack and domain quickly.

### Handling pressure

> I first clarify the highest-risk issue, reproduce the problem, check logs/data, and isolate the failing component. Then I fix the smallest safe part, verify it, and communicate status clearly.

### Working with a team

> I prefer clear contracts: API shape, data model, expected behavior, and ownership. If something is unclear, I ask early and document the decision so the team does not repeat the same discussion.

## Questions to ask interviewer

- What systems or products does APP Group mainly own?
- What backend stack does the team use day to day?
- How does the team handle testing, code review, and deployment?
- What are the biggest backend reliability challenges the team is solving now?
- How are security, audit logging, and compliance handled in normal development work?
- What would success look like for this role in the first three months?

## Final checklist

- [ ] Prepare a 60-second self-introduction.
- [ ] Review [[eventix]] and explain API design, auth, reservations, payments, refunds, workers, and risk review.
- [ ] Review [[mini-paas]] and explain GitHub integration, deployment records, and log streaming.
- [ ] Review REST status codes and API design basics.
- [ ] Review SQL transactions, indexes, constraints, and race conditions.
- [ ] Review auth vs authorization.
- [ ] Prepare one question about APP Group ownership.
- [ ] Prepare one question about team stack and deployment.
- [ ] Join or arrive 10-15 minutes early.
- [ ] Keep answers concise: context, action, result.

## Last-hour review

1. Read the self-introduction out loud twice.
2. Open [[eventix]] and pick two concrete implementation details.
3. Open [[mini-paas]] and pick one integration detail.
4. Review the questions to ask interviewer.
5. Prepare water, notes, internet connection, and interview link/location.

## Post-interview notes

- Interviewers:
- Questions asked:
- Technical topics covered:
- Answers that went well:
- Answers to improve:
- Follow-up action:
- Result:

