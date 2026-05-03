# CorroTech PM Planner

## Overview

A SaaS-style Preventive Maintenance (PM) management system for industrial/corrosion engineering companies. Features a live dashboard, PM creation form, auto-ID generation, and database-backed status tracking.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite (artifacts/corrotech-pm) at `/`
- **API framework**: Express 5 (artifacts/api-server) at `/api`
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Features

- **Dashboard**: 4 clickable status cards (Pending, Scheduled, Completed, Overdue) that filter the PM records table in real time
- **PM Planner**: Form to create PM schedules with auto-generated IDs (CORROTECH-PM-XXXX format)
- **Auto Status**: Status auto-calculated based on next PM date (overdue if past due)
- **Notifications**: Configurable notification settings (1 week, 3 days, 1 day before due)
- **Frequency**: 1 Month, 3 Months, or 6 Months scheduling

## DB Schema

- `pm_records` — all PM records
- `pm_sequence` — auto-increment counter for PM IDs

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)

## Note on codegen

After running codegen, the `lib/api-zod/src/index.ts` gets regenerated. Manually ensure it only exports `./generated/api` (not `./generated/types` or `./generated/api.schemas`) to avoid duplicate export errors.

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
