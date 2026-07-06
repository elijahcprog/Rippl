# Rippl

> See the ripple effects of your biggest life decisions before you make them.

Rippl is a financial scenario planning web app. It lets you model major life events — changing jobs, buying a home, having a kid — and see the projected financial impact before you commit.

[![Status](https://img.shields.io/badge/status-MVP%20in%20development-yellow)](#roadmap)
[![Next.js](https://img.shields.io/badge/Next.js-14-black?logo=next.js)](https://nextjs.org/)
[![License](https://img.shields.io/badge/license-UNLICENSED-lightgrey)](#license)

---

## Table of Contents

- [About](#about)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Available Scripts](#available-scripts)
- [Project Structure](#project-structure)
- [Documentation](#documentation)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## About

Big life decisions are usually made with a spreadsheet, a gut feeling, or both. Rippl gives people a structured way to model "what if" scenarios — a new job offer, a mortgage, a career break, a kid — and see how each one ripples through their finances over time.

This repo is developed following a full software engineering lifecycle (PRD → architecture/ADRs → implementation → validation), not just shipped as fast as possible. Product decisions are hypothesis-driven and tagged for validation status as the product evolves.

## Features

- **Scenario modeling** — create and compare multiple financial "what if" scenarios side by side
- **Life event templates** — pre-built modeling for common events (job change, home purchase, having children, etc.)
- **Projected impact visualization** — see the financial trajectory of a decision before making it
- **Account security** — 2FA-backed authentication
- **Notifications** — browser/email notifications for scenario updates and milestones

> Feature set reflects the current PRD and will evolve as user story hypotheses are validated. See [Documentation](#documentation).

## Tech Stack

| Layer | Choice | Notes |
|---|---|---|
| Framework | [Next.js](https://nextjs.org/) | Single Next.js app for MVP — frontend + API routes. See ADR-001. |
| Language | TypeScript | |
| Scenario Engine | In-process (Next.js API routes) | Flagged as a likely extraction candidate into a standalone service post-MVP as compute/isolation needs grow |
| Hosting | TBD | |
| Database | TBD | |

Architecture decisions are documented as ADRs in [`/docs/adr`](./docs/adr) as they're made — see [ADR-001](./docs/adr/001-frontend-framework.md) for the frontend framework decision and reasoning.

## Architecture

High-level architecture is documented using the [C4 model](https://c4model.com/) (Context → Container → Component → Code).

- **Context diagram** — Rippl and its external actors/systems
- **Container diagram** — the Next.js app boundary, and the scenario engine as a logical container within it
- **Component diagram** — internal component breakdown
- Diagrams live in [`/docs/architecture`](./docs/architecture)

Key architectural decision: the scenario engine is built *inside* the Next.js app for MVP rather than as a separate backend service, to avoid premature complexity. This is a consciously deferred decision, not an eliminated one — see [ADR-001](./docs/adr/001-frontend-framework.md) and the architecture docs for the conditions under which it would be extracted.

## Getting Started

### Prerequisites

- Node.js (LTS recommended)
- npm / pnpm / yarn

### Installation

```bash
# Clone the repo
git clone https://github.com/<your-org>/rippl.git
cd rippl

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env.local

# Run the dev server
npm run dev
```

The app will be available at `http://localhost:3000`.

## Environment Variables

Create a `.env.local` file in the project root. See `.env.example` for the full list. Typical variables include:

```bash
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Auth
AUTH_SECRET=

# Database (once selected)
DATABASE_URL=
```

> Never commit `.env.local` or any file containing real secrets.

## Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start the local development server |
| `npm run build` | Build the app for production |
| `npm run start` | Run the production build locally |
| `npm run lint` | Run linting |
| `npm run test` | Run the test suite |

## Project Structure

```
rippl/
├── app/                  # Next.js app directory (routes, pages, API routes)
├── components/           # Shared UI components
├── lib/                  # Core logic, including the scenario engine
├── docs/
│   ├── prd/              # Product Requirements Document
│   ├── adr/              # Architecture Decision Records
│   └── architecture/     # C4 diagrams, data models, API specs
├── public/               # Static assets
├── .env.example
└── README.md
```

## Documentation

- **PRD** — [`/docs/prd`](./docs/prd) — functional/non-functional requirements, user stories, goals & success metrics, assumptions, constraints, open questions
- **ADRs** — [`/docs/adr`](./docs/adr) — architectural decisions, alternatives considered, and consequences (positive and negative)
- **Architecture** — [`/docs/architecture`](./docs/architecture) — C4 diagrams, data model, API design, failure modes, security architecture

## Roadmap

- [x] Web Plan & PRD
- [x] Tech stack decision (Next.js-only MVP)
- [ ] System design: data modeling, API design, C4 diagrams, failure modes, security architecture
- [ ] MVP implementation
- [ ] User story hypothesis validation
- [ ] Post-MVP: evaluate scenario engine extraction into a standalone service

## Contributing

This project currently follows a solo/small-team workflow with structured PRs:

1. Create a branch from `main`
2. Make your changes, following existing code style (linting enforced via `npm run lint`)
3. Open a PR with a clear description of the change and its rationale
4. Reference related ADRs or PRD sections where relevant

## License

Currently unlicensed / private. To be determined before any public release.
