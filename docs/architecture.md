# Architecture

## Overview

CMMC Compass is a monorepo with a clear separation between the frontend, backend, and shared libraries. All API contracts are defined in OpenAPI first, then code-generated into type-safe client hooks and Zod validation schemas.

## Service Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Web Browser                        │
│              React + Vite SPA                        │
└───────────────────────┬─────────────────────────────┘
                        │ HTTPS
┌───────────────────────▼─────────────────────────────┐
│                   REST API                           │
│            Express 5 + TypeScript                    │
│                                                      │
│  ┌──────────────┐  ┌──────────────┐                 │
│  │  Auth / RBAC │  │ Score Engine │                 │
│  └──────────────┘  └──────────────┘                 │
│  ┌──────────────┐  ┌──────────────┐                 │
│  │ SSP Assembler│  │  PDF Export  │                 │
│  └──────────────┘  └──────────────┘                 │
└───────────────────────┬─────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────┐
│              PostgreSQL Database                     │
│              Drizzle ORM (type-safe)                 │
└─────────────────────────────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────┐
│              Object Storage                          │
│   Evidence files · SSP exports · POA&M bundles       │
└─────────────────────────────────────────────────────┘
```

## Monorepo Structure

```
cmmc-compass/
├── artifacts/
│   ├── api-server/        # Express backend
│   └── web/               # React + Vite frontend
├── lib/
│   ├── api-spec/          # OpenAPI 3.0 — single source of truth
│   ├── api-client/        # Generated React Query hooks (from OpenAPI)
│   ├── api-zod/           # Generated Zod schemas (from OpenAPI)
│   └── db/                # Drizzle ORM schema and migrations
├── data/
│   └── CMMC_CONTROLS.json # Canonical control seed data
└── scripts/               # Utility and migration scripts
```

## API-First Design

The OpenAPI specification in `lib/api-spec/openapi.yaml` is the authoritative contract between frontend and backend. Code generation produces:

- **React Query hooks** — typed data fetching with caching and invalidation
- **Zod schemas** — runtime validation for all request and response bodies

Never hand-write API types. Always run codegen after modifying the spec:

```bash
pnpm --filter @workspace/api-spec run codegen
```

## SPRS Score Engine

The SPRS (Supplier Performance Risk System) score starts at **110** and decrements by a control-specific value (1, 3, or 5 points) for every practice not fully implemented.

Score is recalculated server-side on every control assessment update and returned in the organization summary endpoint. The frontend subscribes to this value and renders it in real time.

## Evidence Storage Model

Evidence files are stored as independent entities with a many-to-many relationship to control assessments. A single policy document can satisfy requirements across multiple controls — this is modeled correctly at the database level with a junction table, not by duplicating files.

## Multi-Tenancy (Track 3)

The data model is multi-tenant from day one. Every organization record has an optional `consultancy_id` foreign key. Consultancy-scoped queries filter by this relationship. Row-level authorization is enforced in the API middleware layer — no cross-tenant data leakage is architecturally possible.

## RBAC

| Role | Scope | Permissions |
|---|---|---|
| Contractor Admin | Organization | Full read/write, user management |
| Contractor User | Organization | Read/write assessments and evidence |
| Consultant Reviewer | Client org (read-only) | View and comment only |
| Consultant Admin | All client orgs | Full consultant access, push templates |
