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

### Interview focus from latest feedback

- At the start of the interview, lead with stack and experience that are closest to the .NET Developer role.
- Explain project experience more clearly and in more detail: context, role, stack, technical decisions, constraints, and result.
- After .NET-relevant points are covered, mention other stacks as additional strengths, not as the opening focus.

### Opening answer - .NET Developer focus

Use this order when asked "tell me about yourself":

> Saya Muhammad Ghafuri, backend-focused Software Engineer dengan pengalaman sekitar 3 tahun di API development, system integration, database-backed workflows, dan production support. Untuk kebutuhan posisi .NET Developer, bagian yang paling relevan dari pengalaman saya adalah C#/.NET foundation, OOP, REST API design, SQL terutama Microsoft SQL Server, debugging production issue, dan integrasi sistem enterprise seperti ERP/order-management workflows.
>
> Di pengalaman terakhir saya di iSystem Asia untuk client CelcomDigi, saya banyak bekerja di area backend dan integration flow: memahami business workflow, menyesuaikan API contract, menjaga data flow antar sistem, membantu UAT, rollout, dan production debugging. Selain itu saya juga punya pengalaman di Laravel, Node.js/TypeScript, Go, Redis, Docker, dan React. Stack tambahan itu membantu saya memahami backend secara luas, tapi untuk role ini saya akan fokus menonjolkan kemampuan yang paling dekat dengan .NET: C#, API, SQL, integration, reliability, dan maintainable backend code.

Shorter 30-second version:

> Saya backend-focused Software Engineer dengan pengalaman di API, SQL, system integration, dan production support. Untuk posisi .NET Developer, saya ingin menonjolkan pengalaman yang relevan dengan C#/.NET foundation, OOP, REST API, Microsoft SQL Server, dan enterprise integration. Di iSystem Asia saya menangani workflow order-management dan integrasi ERP, termasuk API updates, payload contract, UAT, rollout, dan debugging production. Selain itu saya punya pengalaman tambahan di Laravel, Node.js/TypeScript, Go, Redis, Docker, dan React.

### Tech stack order for early interview

Start with:

- C#/.NET-relevant foundation: C#, OOP, backend service design, REST API concepts.
- Database: Microsoft SQL Server, relational modeling, transactions, indexes, constraints.
- Integration: API contracts, payload validation, ERP/order synchronization, data flow debugging.
- Reliability: production debugging, logging, rollout support, UAT validation, failure investigation.
- Backend fundamentals: authentication, authorization, background jobs, idempotency, error handling.

Then add:

- Laravel/PHP for enterprise backend work.
- Node.js/TypeScript/Hono for REST APIs and government freelance systems.
- Go for side projects with stronger backend architecture practice.
- Redis, Docker, GitHub integrations, React/Vite as supporting tools.

Avoid opening with:

- "Saya lebih banyak pakai Go/Node/Laravel" before explaining .NET-relevant fundamentals.
- Too many stack names without tying them to backend responsibilities.
- A project list without explaining decisions and results.

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

### Detailed project explanations

#### Project 1: Enterprise NCCF and ERP integration - iSystem Asia

Use this as the most relevant professional project for a .NET Developer interview because it shows enterprise backend, SQL, API contracts, integration, UAT, and production support.

Spoken version:

> Project yang paling relevan dari pengalaman profesional saya adalah enterprise NCCF/order-management workflow untuk client CelcomDigi di iSystem Asia. Sistem ini digunakan untuk mendukung workflow order-management dan integrasi dengan ERP. Peran saya adalah mengerjakan backend dan integration changes, termasuk API update, order synchronization, item distribution, payload contract, defect fixing, UAT support, rollout coordination, dan production debugging.
>
> Secara teknis, fokus saya bukan hanya menambah endpoint, tapi memastikan data flow antar sistem tetap konsisten. Saya perlu memahami payload yang dikirim, validasi data, mapping antar sistem, query/database behavior, dan impact perubahan ke workflow bisnis. Karena sistem enterprise biasanya melibatkan beberapa stakeholder, saya juga mendokumentasikan contract, trade-off, dan issue agar perubahan bisa divalidasi dengan jelas saat UAT maupun rollout.
>
> Hasilnya, saya mendapatkan pengalaman yang sangat relevan untuk backend enterprise: menjaga API contract, debugging data flow, bekerja dengan SQL/database, koordinasi release, dan memastikan perubahan tidak merusak core workflow. Ini relevan dengan .NET Developer karena concern utamanya sama: backend service yang maintainable, reliable, terintegrasi dengan sistem lain, dan aman untuk production.

Technical details to mention:

- Domain: enterprise order-management and ERP integration.
- Stack exposure: Laravel services, Creatio, Microsoft SQL Server, Redis/Node.js support, ERP data flows.
- Responsibilities: API changes, synchronization flow, payload contract documentation, defect fixes, UAT, rollout support.
- Strong signal: enterprise integration and production reliability.

Potential follow-up answer:

> Kalau ditanya tantangannya, tantangan terbesar adalah perubahan kecil di satu flow bisa berdampak ke sistem lain. Jadi saya biasanya mulai dari memahami contract dan data state, cek query atau log yang relevan, reproduksi issue, lalu validasi fix terhadap skenario UAT yang paling berisiko.

#### Project 2: Eventix - ticketing API

Use this when asked for a deeper backend architecture example.

Spoken version:

> Eventix adalah side project backend untuk event ticketing. Saya membuat API untuk attendee dan organizer authentication, event management, ticket tier, order creation, reservation, mock payment, ticket issuing, refund flow, QR ticket check-in, background worker, dan admin risk review.
>
> Bagian paling penting dari project ini adalah workflow order dan ticket reservation. Ketika user membuat order, sistem harus menahan inventory sementara agar ticket tidak oversold. Kalau pembayaran berhasil, reservation berubah menjadi ticket yang issued. Kalau user tidak bayar dalam batas waktu, worker akan expire reservation dan mengembalikan inventory. Dari sini saya belajar memodelkan state, transaksi, race condition, background job, dan idempotency.
>
> Walaupun stack-nya Go dan SQLite, konsep backend-nya transferable ke .NET: controller/handler layer, service layer, repository/data access, transaction boundary, role-based authorization, background worker, consistent error handling, dan database-backed workflow.

Technical details to mention:

- Stack: Go, SQLite, Chi, JWT, Docker Compose.
- Backend concepts: REST API, JWT auth, reservations, mock payments, refunds, workers, QR ticketing, risk checks.
- Relevant to .NET: layered backend design, transactions, authorization, background jobs, SQL persistence.

Potential follow-up answer:

> Kalau saya implement di .NET, pendekatannya bisa mirip: ASP.NET Core Web API untuk endpoint, Entity Framework atau Dapper untuk data access, SQL Server untuk persistence, hosted service atau queue worker untuk expiration job, dan middleware/filter untuk auth serta error handling.

#### Project 3: SITAMPANPARAT - government mapping and reporting system

Use this when asked about end-to-end ownership and client delivery.

Spoken version:

> SITAMPANPARAT adalah freelance project untuk client pemerintahan, fokusnya mapping/reporting system yang mendukung mobile workflow. Saya mengerjakan backend, geospatial data, Docker deployment, dan document/report generation.
>
> Secara teknis saya membangun REST API dengan Node.js, TypeScript, Hono, PostgreSQL/PostGIS, dan visualisasi berbasis Leaflet. Tantangannya adalah data bukan hanya table biasa, tapi ada geospatial data, koordinat, area mapping, dan kebutuhan report. Jadi saya perlu memikirkan API shape, query ke PostGIS, struktur data yang mudah dikonsumsi frontend, dan deployment yang bisa dijalankan konsisten.
>
> Project ini menunjukkan kemampuan saya untuk mengambil ownership dari requirement sampai delivery: memahami kebutuhan client, membangun API, mengelola database, menyiapkan deployment, dan menghasilkan output report yang digunakan user.

Technical details to mention:

- Stack: Node.js, TypeScript, Hono, PostgreSQL/PostGIS, Leaflet, Docker.
- Responsibilities: backend API, geospatial data model, deployment, reporting/document generation.
- Strong signal: end-to-end delivery, SQL/data modeling, client communication.

#### Project 4: Svara Aircast - performance and monitoring

Use this when asked about optimization, reliability, or measurable impact.

Spoken version:

> Di Svara Aircast, saya bekerja pada platform radio streaming automation. Salah satu kontribusi saya adalah optimasi file I/O dan stream-processing path yang menurunkan CPU usage sekitar 30%. Selain itu saya juga mendesain real-time audio silence detection untuk membantu monitoring ketika ada masalah audio.
>
> Dari project ini saya belajar bahwa backend atau system work tidak selalu hanya CRUD. Kadang bottleneck ada di I/O, proses streaming, atau observability. Pendekatan saya adalah memahami path yang paling berat, melihat behavior runtime, memperbaiki bagian yang paling berdampak, lalu memastikan perubahan tetap reliable untuk production.

Technical details to mention:

- Domain: media streaming and automation.
- Responsibilities: production features, performance optimization, monitoring feature.
- Result: approximately 30% CPU usage reduction.
- Strong signal: measurable optimization and operational reliability.

#### Project 5: Mini PaaS - platform and integration prototype

Use this only after stronger professional examples, or when asked about integration/platform thinking.

Spoken version:

> Mini PaaS adalah side project untuk mempelajari platform engineering secara bertahap. Saya membuat Go API dan React frontend untuk user auth, app CRUD, GitHub App installation, repository and branch selection, simulated deployment records, dan log streaming menggunakan Server-Sent Events.
>
> Saya sengaja membatasi milestone pertama pada workflow dan contract: user bisa connect GitHub, pilih repository, trigger simulated deployment, lalu melihat deployment log. Real Docker build dan runtime infrastructure belum saya masukkan di milestone ini supaya interface, data model, dan user flow-nya matang dulu.
>
> Nilai teknisnya adalah integration design, incremental delivery, deployment lifecycle modeling, dan real-time log streaming.

Technical details to mention:

- Stack: Go, SQLite, React, Vite, TypeScript, GitHub App integration.
- Concepts: external integration, deployment records, SSE log streaming, staged delivery.
- Strong signal: platform mindset and pragmatic milestone planning.

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

- [ ] Practice opening answer with .NET-relevant stack first.
- [ ] Prepare one concise explanation of C#/.NET foundation, REST API, and SQL Server relevance.
- [ ] Practice detailed explanation of iSystem Asia NCCF/ERP integration project.
- [ ] Practice detailed explanation of Eventix using reservation/payment workflow.
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
