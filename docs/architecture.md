# Architecture

## Overview

The project is a pnpm monorepo with a React frontend, an Express API server, and a PostgreSQL database. The API contract is defined in OpenAPI and code-generated into typed client hooks and Zod schemas before any feature work starts.

## Service Layout

```
Browser (React + Vite)
    |
    | HTTP
    |
Express API (TypeScript)
    |-- Auth and RBAC middleware
    |-- SPRS score calculation
    |-- SSP assembler
    |-- PDF export
    |-- File storage service
    |
PostgreSQL (Drizzle ORM)
    |
Object Storage (evidence files, PDF exports)
```

## Monorepo Structure

```
cmmc-compass/
├── artifacts/
│   ├── api-server/        # Express backend
│   └── web/               # React + Vite frontend
├── lib/
│   ├── api-spec/          # OpenAPI 3.0 spec (source of truth)
│   ├── api-client/        # Generated React Query hooks
│   ├── api-zod/           # Generated Zod schemas
│   └── db/                # Drizzle schema and migrations
├── data/
│   └── CMMC_CONTROLS.json # Control seed data
└── scripts/
```

## API Contract

The OpenAPI spec in `lib/api-spec/openapi.yaml` is the source of truth. Updating it and running codegen produces new client hooks and validation schemas. Do not hand-write API types.

```bash
pnpm --filter @workspace/api-spec run codegen
```

## SPRS Score Calculation

Score starts at 110 and decrements by a per-control value (1, 3, or 5 points) for every practice not marked Met. Score is recalculated server-side on every assessment update and returned in the organization summary endpoint.

## Evidence Storage

Evidence files are stored as independent entities with a many-to-many join to control assessments. A single file can satisfy multiple controls without duplication. The join table is `evidence_control_map`.

## Multi-Tenancy

Every organization row has an optional `consultancy_id`. All queries that return organization data are scoped to the requesting user's organization or consultancy. Cross-tenant access is blocked at the middleware layer.

## Roles

| Role | Access |
|---|---|
| Contractor Admin | Full read/write within their organization |
| Contractor User | Read/write assessments and evidence |
| Consultant Reviewer | Read and comment only across assigned clients |
| Consultant Admin | Full access across all client organizations |
