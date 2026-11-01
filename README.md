# Hi, I'm Kris Riisgaard Larsen

**Full-Stack Software Developer · C# / .NET · React · TypeScript · APIs & Integrations**

I'm a full-stack software developer with more than seven years of professional software development experience and a strong foundation in C#/.NET, APIs and system integrations.

I enjoy building solutions across the entire application stack, combining backend architecture and business logic with frontend development and user experience.

My experience includes C#/.NET, React, Angular, TypeScript and Blazor, with a focus on maintainable code, automated testing and delivering practical software solutions.

The projects below are public portfolio projects that complement my professional experience. Each README states what is implemented, what is simulated and what is deliberately out of scope.

---

## Start here — three projects to review

These public portfolio projects can be evaluated from screenshots, architecture notes and tests **without installing anything**. Each has a documented way to run the demo locally with free tools; no paid hosting is required.

| Project | Engineering focus | Review and run locally |
| --- | --- | --- |
| **[Room Booking](https://github.com/kris7011/meeting-room-booking)** | .NET 10 + Angular, Microsoft Entra ID, multi-tenant security, concurrency and idempotent booking | [Reviewer guide](https://github.com/kris7011/meeting-room-booking/blob/main/docs/REVIEWER_GUIDE.md) · [Web screenshot](https://github.com/kris7011/meeting-room-booking/blob/main/docs/images/angular-demo.png) · [Mobile client](https://github.com/kris7011/room-booking-mobile) |
| **[ShiftPlanner API](https://github.com/kris7011/shift-planner-api)** | .NET 10 + React, Clean Architecture, explainable scheduling rules, CSV import and tests | [Reviewer guide](https://github.com/kris7011/shift-planner-api/blob/main/docs/REVIEWER_GUIDE.md) · [Dashboard screenshot](https://github.com/kris7011/shift-planner-api/blob/main/docs/images/overview-status.png) |
| **[CommerceFlow](https://github.com/kris7011/commerce-flow)** | Node.js + TypeScript, event-driven services, RabbitMQ/PostgreSQL, transactional outbox and recovery | [Reviewer guide](https://github.com/kris7011/commerce-flow/blob/main/docs/REVIEWER_GUIDE.md) · [Order timeline screenshot](https://github.com/kris7011/commerce-flow/blob/main/docs/assets/order-timeline.png) |

**How to evaluate the work:** each reviewer guide links to a technical walkthrough, the relevant code and the automated tests, as well as clearly stated limitations. The projects are engineering demonstrations, not claims of production deployments. The booking system's anonymous demo does not require Microsoft sign-in; its authenticated features have separate setup requirements.

---

## Core skills

| Area | Technologies and practices |
|---|---|
| **Backend** | C#, .NET 8–10, ASP.NET Core (Minimal APIs and Web API), REST API design, Problem Details, dependency injection, OpenAPI/Swagger |
| **Frontend** | TypeScript, JavaScript, React, Angular (Signals, Reactive Forms, RxJS), Blazor, HTML, CSS, Tailwind CSS |
| **Mobile and desktop** | React Native / Expo, Flutter and Flame, Python Tkinter |
| **Integrations and messaging** | RabbitMQ (publisher confirms, dead-lettering), transactional outbox, idempotent consumers, third-party HTTP APIs, Microsoft Entra ID (OAuth 2.0 with PKCE), managed-to-native interop (C ABI, `LibraryImport`) |
| **Databases** | PostgreSQL, SQLite, Entity Framework Core and migrations, Azure Cosmos DB |
| **Architecture** | Clean Architecture, ports and adapters, feature folders, event-driven architecture, multi-tenant isolation, Architecture Decision Records |
| **Testing** | xUnit, `WebApplicationFactory` integration tests, Vitest, Playwright, pytest, Flutter widget and integration tests, Catch2, failure-mode and concurrency tests against real infrastructure |
| **CI/CD and cloud** | GitHub Actions, Docker, GitHub Container Registry, Azure App Service, Azure Static Web Apps |
| **Also** | Node.js, Python, FastAPI, Dart, C++20, C17, CMake, Linux |

---

## Featured projects

| Project | Focus | Main stack | Status |
|---|---|---|---|
| [Room Booking](https://github.com/kris7011/meeting-room-booking) ([mobile](https://github.com/kris7011/room-booking-mobile)) | Multi-tenant room booking with Microsoft sign-in | C#/.NET 10, EF Core, Angular 21, React Native / Expo | Complete |
| [CommerceFlow](https://github.com/kris7011/commerce-flow) | Reliable messaging between microservices | TypeScript, Node.js, RabbitMQ, PostgreSQL | Released, extended after v1.0.0 |
| [GridFlex EMS](https://github.com/kris7011/gridflex-ems) | ASP.NET Core API driving a native C++ controller | C#/.NET 10, C++20, C, Python, Docker | Released, extended after v1.0.0 |
| [ShiftPlanner API](https://github.com/kris7011/shift-planner-api) | Explainable, rule-based workforce scheduling | C#/.NET 10, EF Core, React | Working portfolio version |
| [Asset Portfolio Ops](https://github.com/kris7011/asset-portfolio-ops) | Full-stack operations platform with Azure CI/CD | C#/.NET 10, EF Core, React, Azure | Working demo |
| [ResilienceOps](https://github.com/kris7011/resilience-ops) | Operational risks, mitigation actions and incidents | C#/.NET 10, EF Core, Angular 21 | In development |
| [AI Deal Agent](https://github.com/kris7011/ai-deal-agent) | Product search with an external API integration | Python, FastAPI, SQLite, React | Prototype |
| [Python Shift Planner Desktop](https://github.com/kris7011/python-shift-planner-desktop) | Desktop shift planning with workload analysis | Python, Tkinter, ReportLab | Working desktop app |
| [Color Dodge](https://github.com/kris7011/color-dodge) | Arcade game with three modes | Flutter, Dart, Flame | Learning project |

### [Room Booking](https://github.com/kris7011/meeting-room-booking)

`C#` `.NET 10` `Minimal API` `EF Core` `SQLite` `Angular 21` `React Native` `Expo` `Microsoft Entra ID` `Playwright`

A multi-tenant meeting room booking platform in two repositories: the [ASP.NET Core API and Angular client](https://github.com/kris7011/meeting-room-booking), and the [React Native / Expo mobile app](https://github.com/kris7011/room-booking-mobile). Organisations manage their own rooms and members; members find the smallest free room for a group and book it, without double bookings and without seeing another organisation's data.

- **The API is the only authority:** it validates the access token and reads memberships and roles (Owner, Admin, Member) from its own database on every request. Invitations need the token *and* a verified matching e-mail; the last Owner can never be removed.
- **Correct under pressure:** no overlapping bookings even with parallel requests, safe retries with an `Idempotency-Key`, access re-checked inside each transaction, and booking details hidden from Members.
- **Sign-in:** Microsoft Entra ID with the authorization code flow and PKCE in the Android app (tokens in SecureStore) and the Angular client, plus optional e-mail one-time-code sign-in through Entra External ID.
- **Tested:** 441 backend integration tests, 31 Angular tests, 506 mobile unit tests and 38 Playwright end-to-end tests of the mobile web build against the real API. The Android development build was checked by hand on a real device.

*Scope:* development builds only, no app store release. E-mail (External ID) users cannot accept invitations by design, and iOS sign-in is implemented but not tried on a device.

### [CommerceFlow](https://github.com/kris7011/commerce-flow)

`TypeScript` `Node.js` `RabbitMQ` `PostgreSQL` `Docker` `GitHub Actions`

An event-driven order workflow of five independent services that collaborate only through RabbitMQ events. The business logic is intentionally simple; the focus is on staying consistent when the network, the broker or the database fails.

- **Transactional outbox:** stock changes and their events are committed in one PostgreSQL transaction. An event is marked as published only after RabbitMQ has confirmed it and routed it to a queue.
- **Idempotent order submission:** `POST /orders` requires an `Idempotency-Key`; a unique index means retries, even concurrent ones, can never create duplicate orders.
- **Order timeline:** the Order Service records every event of an order and serves a page that shows its actual steps, outcome and duplicates.
- **Tests that prove failure behaviour:** integration and end-to-end tests run against real PostgreSQL and RabbitMQ and cover crashes, broker outages, duplicate deliveries and concurrent orders.

*Scope:* payment and delivery are simulated, and the project explicitly does not claim exactly-once delivery.

### [GridFlex EMS](https://github.com/kris7011/gridflex-ems)

`C#` `ASP.NET Core` `C++20` `C17` `Python` `CMake` `Docker` `GitHub Actions`

A modular, simulated energy management system (solar, battery storage, building load and grid) in which an HTTP request travels from ASP.NET Core into a native C++ controller.

- **Managed-to-native integration:** ASP.NET Core API → application layer → `NativeControllerGateway` → source-generated `LibraryImport` → versioned C ABI → C++ controller, with `SafeHandle` lifetime management and liveness/readiness health checks.
- **Interactive energy dashboard:** a local web dashboard runs a scenario with the real C++ controller deciding every interval through the API, then replays the day with each decision, the limit behind it and a Python reference strategy for comparison.
- **Delivery pipeline:** GitHub Actions workflows for Python, C, C++, the backend, the software-in-the-loop path and the container, and a non-root Linux image published to GitHub Container Registry.

*Planned, not yet implemented:* Azure deployment and cloud monitoring. The system does not control real electrical equipment.

### [ShiftPlanner API](https://github.com/kris7011/shift-planner-api)

`C#` `.NET 10` `ASP.NET Core` `EF Core` `SQLite` `React` `TypeScript` `xUnit`

A healthcare-oriented workforce scheduling system that assigns shifts and explains every decision.

- **Clean Architecture** (Domain, Application, Infrastructure and API) with a rule-based scheduling engine: skill matching, workload balancing, maximum assignments, and same-day and night-to-day protection.
- **Explainable decisions:** candidate-level failure reasons, shift assignment analysis and what-if simulation.
- **CSV import with preview:** every row is validated with the same rules as the scheduler; nothing is saved until an explicit, one-time confirmation that re-checks the current schedule in one transaction. Duplicates are detected per row and per file, and a week can be exported in the import format.
- **Tested:** 101 unit tests, 46 API integration tests and 13 React component tests in GitHub Actions, plus a Docker smoke test.

*Scope:* a simplified public version that uses demo logic and demo data.

### [Asset Portfolio Ops](https://github.com/kris7011/asset-portfolio-ops)

`C#` `.NET 10` `Minimal API` `EF Core` `React` `TypeScript` `Azure` `GitHub Actions`

A full-stack platform for investment operations (sample domain: fine wine), covering assets, customer portfolios, inventory, purchase requests, risk indicators and audit events.

- **Business rules in the backend:** a purchase-request state machine that rejects invalid transitions, and risk indicators for portfolio concentration, low inventory and pending exposure.
- **Valuation history and purchase preview:** price history per asset and portfolio, and a read-only preview of how a purchase would change concentration before anything is created. The schema is managed with EF Core migrations, including a safe baseline for older databases.
- **CI/CD to Azure:** GitHub Actions workflows test and deploy the API to Azure App Service and the React frontend to Azure Static Web Apps.

*Scope:* a demo without authentication, using demonstration valuation data. It uses SQLite, and Cosmos DB is disabled by default to keep costs low.

### [ResilienceOps](https://github.com/kris7011/resilience-ops)

`C#` `.NET 10` `Minimal API` `EF Core` `SQLite` `Angular 21` `OpenTelemetry` `xUnit`

An operational resilience application for risks, the mitigation actions that reduce them, and the incidents in which a risk occurred.

- **Incident management:** incidents linked to a risk and its mitigation actions, with a responsible person, a Reported → Investigating → Resolved → Closed lifecycle (with reopening) and an append-only status timeline. Invalid moves return `409`.
- **Consistency:** a unique index on the timeline makes concurrent status changes return `409` instead of corrupting the history; migrations are additive and keep existing data.
- **Observability:** OpenTelemetry tracing with optional export to Azure Monitor.
- **Tested:** API integration tests against migrated SQLite (including a race between two status changes) and Angular component tests.

*Planned, not yet implemented:* authentication, Azure hosting and an audit log.

### [AI Deal Agent](https://github.com/kris7011/ai-deal-agent) - prototype

`Python` `FastAPI` `SQLite` `React` `TypeScript` `SerpAPI` `pytest` `Vitest`

A prototype that turns a natural-language product request into ranked product suggestions with prices, match scores and explanations.

- **External API integration:** a FastAPI backend calls Google Shopping through SerpAPI. A local cache and a two-level guard prevent accidental live calls and protect the API quota.
- **Price history and comparison:** prices are stored in SQLite, dated by when the data was fetched from the source, so cached results never create false history. Every result shows its origin (live, cache or demo) and freshness, and up to four products can be compared side by side.
- **Offline demo:** clearly labelled fictional demo data can be loaded without an API key or any paid call.

*Status:* parsing and matching are rule-based. LLM-based parsing and deployment are planned, not implemented.

### [Python Shift Planner Desktop](https://github.com/kris7011/python-shift-planner-desktop)

`Python` `Tkinter` `ReportLab` `pytest` `GitHub Actions`

A desktop shift planner for 24/7 departments that assigns shifts from CSV files and explains its decisions.

- **Rule-based assignment** with skills, capacity, rest-time rules, personalised workload scoring and 28-day fairness for nights and weekends.
- **Editable calendar:** shifts can be changed by hand, checked with the scheduler's own rules (refused changes show every reason), and undone step by step.
- **PDF export** that never overwrites a file without confirmation; the input CSV files are never modified.

*Scope:* edits are kept in memory and exported as PDF; saving an edited schedule is not implemented.

### [Color Dodge](https://github.com/kris7011/color-dodge)

`Flutter` `Dart` `Flame` `SharedPreferences`

A small arcade game used to learn Flutter and the Flame engine.

- **Three modes:** Survival, a date-seeded Daily Challenge, and Color Match, where you steer into blocks of your own colour, build combos and survive colour changes and faster levels.
- **Testable game rules:** Color Match's rules are pure Dart with unit tests; widget tests run a seeded game through the real game loop.
- **Local progression:** best scores, levels and combos are stored on the device.

*Verified:* Color Match was played end to end on Windows desktop with an integration test; other platforms are not verified for that mode.

---

## How I work

- **Complete features, end to end:** the API, data model, user interface, tests and CI are delivered together.
- **Business rules live in the backend** and are tested in isolation. Infrastructure sits behind small interfaces.
- **Failure modes are designed and tested,** not assumed away: retries, idempotency, health checks and explicit error contracts.
- **Automation from the start:** builds, tests and container publishing run in GitHub Actions.
- **Honest documentation:** READMEs state limitations and trade-offs plainly, and key decisions are recorded.

---

I'm interested in software development opportunities across the full stack, including roles focused on backend engineering, frontend development or a combination of both.
