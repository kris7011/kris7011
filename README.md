# Hi, I'm Kris Riisgaard Larsen

**Backend-focused software developer · C# / .NET · REST APIs · integrations · software architecture**

I build backend systems where correctness matters: clear domain boundaries, explicit failure handling, automated tests that prove the behaviour, and CI pipelines that keep it that way. Most of my work is in C# and ASP.NET Core. I also use TypeScript/Node.js, Python and C/C++ when a problem calls for them.

The projects below are public portfolio projects. Each README states what is implemented, what is simulated and what is deliberately out of scope.

---

## Core skills

| Area | Technologies and practices |
|---|---|
| **Backend** | C#, .NET 8–10, ASP.NET Core (Minimal APIs and Web API), REST API design, Problem Details, dependency injection, OpenAPI/Swagger |
| **Integrations and messaging** | RabbitMQ (publisher confirms, dead-lettering), transactional outbox, idempotent consumers, third-party HTTP APIs, managed-to-native interop (C ABI, `LibraryImport`) |
| **Databases** | PostgreSQL, SQLite, Entity Framework Core and migrations, Azure Cosmos DB |
| **Architecture** | Clean Architecture, ports and adapters, feature folders, event-driven architecture, Architecture Decision Records |
| **Testing** | xUnit, `WebApplicationFactory` integration tests, Vitest, pytest, Catch2, failure-mode and concurrency tests against real infrastructure |
| **CI/CD and cloud** | GitHub Actions, Docker, GitHub Container Registry, Azure App Service, Azure Static Web Apps |
| **Frontend** | TypeScript, React, Angular (Signals, Reactive Forms, RxJS), Tailwind CSS |
| **Also** | Node.js, Python, FastAPI, C++20, C17, CMake, Linux |

---

## Featured projects

| Project | Focus | Main stack | Status |
|---|---|---|---|
| [CommerceFlow](https://github.com/kris7011/commerce-flow) | Reliable messaging between microservices | TypeScript, Node.js, RabbitMQ, PostgreSQL | v1.0.0 released |
| [GridFlex EMS](https://github.com/kris7011/gridflex-ems) | ASP.NET Core API driving a native C++ controller | C#/.NET 10, C++20, C, Python, Docker | v1.0.0 released, further milestones planned |
| [ShiftPlanner API](https://github.com/kris7011/shift-planner-api) | Explainable, rule-based workforce scheduling | C#/.NET 9, EF Core, React | Working portfolio version |
| [Asset Portfolio Ops](https://github.com/kris7011/asset-portfolio-ops) | Full-stack operations platform with Azure CI/CD | C#/.NET 10, EF Core, React, Azure | Working demo |
| [Meeting Room Booking](https://github.com/kris7011/meeting-room-booking) | Full-stack CRUD app with strict booking rules | C#/.NET 8, EF Core, Angular 21 | Complete |
| [AI Deal Agent](https://github.com/kris7011/ai-deal-agent) | Product search with an external API integration | Python, FastAPI, React | Prototype |

### [CommerceFlow](https://github.com/kris7011/commerce-flow)

`TypeScript` `Node.js` `RabbitMQ` `PostgreSQL` `Docker` `GitHub Actions`

An event-driven order workflow of five independent services that collaborate only through RabbitMQ events. The business logic is intentionally simple; the focus is on staying consistent when the network, the broker or the database fails.

- **Transactional outbox:** stock changes and their events are committed in one PostgreSQL transaction. An event is marked as published only after RabbitMQ has confirmed it and routed it to a queue.
- **At-least-once delivery with idempotent consumers:** duplicates are expected and handled, and stock can never be reserved twice for the same order.
- **Tests that prove failure behaviour:** integration and end-to-end tests run against real PostgreSQL and RabbitMQ and cover crashes, broker outages, duplicate deliveries and concurrent orders. CI runs on Node.js 22 and 24.

*Scope:* payment and delivery are simulated, and the project explicitly does not claim exactly-once delivery.

### [GridFlex EMS](https://github.com/kris7011/gridflex-ems)

`C#` `ASP.NET Core` `C++20` `C17` `Python` `CMake` `Docker` `GitHub Actions`

A modular, simulated energy management system (solar, battery storage, building load and grid) in which an HTTP request travels from ASP.NET Core into a native C++ controller.

- **Managed-to-native integration:** ASP.NET Core API → application layer → `NativeControllerGateway` → source-generated `LibraryImport` → versioned C ABI → C++ controller, with `SafeHandle` lifetime management and liveness/readiness health checks.
- **Layered native code:** a C hardware abstraction layer with simulated sensors, actuators and failure injection, plus an independent Python simulation engine.
- **Delivery pipeline:** five GitHub Actions workflows (Python, C, C++, backend and container) and a non-root Linux image published to GitHub Container Registry, with actions and base images pinned to immutable versions.

*Planned, not yet implemented:* Azure deployment, monitoring and a frontend dashboard. The system does not control real electrical equipment.

### [ShiftPlanner API](https://github.com/kris7011/shift-planner-api)

`C#` `.NET 9` `ASP.NET Core` `EF Core` `SQLite` `React` `TypeScript` `xUnit`

A healthcare-oriented workforce scheduling system that assigns shifts and explains every decision.

- **Clean Architecture** (Domain, Application, Infrastructure and API) with a rule-based scheduling engine: skill matching, workload balancing, maximum assignments, and same-day and night-to-day protection.
- **Explainable decisions:** candidate-level failure reasons, shift assignment analysis and what-if simulation for planning decisions.
- **React and TypeScript dashboard** (Danish UI) on top of the REST API, with 59 xUnit tests running in GitHub Actions.

*Scope:* a simplified public version that uses demo logic and demo data.

### [Asset Portfolio Ops](https://github.com/kris7011/asset-portfolio-ops)

`C#` `.NET 10` `Minimal API` `EF Core` `React` `TypeScript` `Azure` `GitHub Actions`

A full-stack platform for investment operations (sample domain: fine wine), covering assets, customer portfolios, inventory, purchase requests, risk indicators and audit events.

- **Business rules in the backend:** a purchase-request state machine that rejects invalid transitions, and risk indicators for portfolio concentration, low inventory and pending exposure.
- **Replaceable audit store:** audit events sit behind an `IAuditEventStore` interface with in-memory and Azure Cosmos DB implementations.
- **CI/CD to Azure:** GitHub Actions workflows test and deploy the API to Azure App Service and the React frontend to Azure Static Web Apps.

*Scope:* a demo without authentication. It uses SQLite, and Cosmos DB is disabled by default to keep costs low.

### [Meeting Room Booking](https://github.com/kris7011/meeting-room-booking)

`C#` `.NET 8` `Minimal API` `EF Core` `SQLite` `Angular 21` `Tailwind CSS` `xUnit`

A full-stack meeting room booking application, built as a technical assignment with emphasis on clear structure and correct business rules.

- **Authoritative API rules:** overlapping bookings are rejected on both create and update, and errors are returned as Problem Details with clear 400, 404 and 409 responses.
- **Modern Angular frontend:** Signals, Reactive Forms, RxJS and Tailwind CSS 4, with explicit UTC handling.
- **Tested end to end:** 15 backend integration tests using `WebApplicationFactory` and isolated SQLite databases, 8 Vitest frontend tests, and separate backend and frontend CI jobs.

### [AI Deal Agent](https://github.com/kris7011/ai-deal-agent) — prototype

`Python` `FastAPI` `React` `TypeScript` `SerpAPI` `pytest`

A prototype that turns a natural-language product request into ranked product suggestions with prices, match scores and explanations.

- **External API integration:** a FastAPI backend calls Google Shopping through SerpAPI. A local cache and a two-level guard prevent accidental live calls and protect the API quota.
- **Transparent ranking:** rule-based requirement parsing, Danish/English feature matching, and scoring with badges and explanations. Searches can be saved and re-run.
- **React and TypeScript frontend**, with pytest tests for parsing, scoring, matching and saved searches.

*Status:* parsing and matching are rule-based today. LLM-based parsing, database storage and deployment are planned, not implemented.

---

## How I work

- **Business rules live in the backend** and are tested in isolation. Infrastructure sits behind small interfaces.
- **Failure modes are designed and tested,** not assumed away: retries, idempotency, health checks and explicit error contracts.
- **Automation from the start:** builds, tests and container publishing run in GitHub Actions.
- **Honest documentation:** READMEs state limitations and trade-offs plainly, and key decisions are recorded.

---

I'm open to backend and full-stack developer roles, particularly in C# and .NET.
