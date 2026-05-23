---
title: "Database Schema & Migrations"
description: "Docsbook database reference — PostgreSQL on Neon with Drizzle ORM, core tables, migration workflow, and backup strategy."
---

# Database Schema & Migrations

Docsbook stores all persistent state in PostgreSQL hosted on [Neon](https://neon.tech) (serverless, autoscaling). The schema is defined in TypeScript using [Drizzle ORM](https://orm.drizzle.team).

## Stack

- **Database:** PostgreSQL 15 on Neon serverless
- **ORM:** Drizzle ORM with `postgres-js` driver
- **Schema location:** `src/db/schema.ts`
- **Migration tool:** `drizzle-kit`

## Core tables

| Table                   | Purpose                                                                      |
| ----------------------- | ---------------------------------------------------------------------------- |
| `users`                 | GitHub user ID, username, email, plan (`free` / `pro` / `pro_plus`), Paddle customer ID |
| `workspaces`            | 60+ columns: branding, UI toggles, AI settings, SEO, custom domain, enabled languages, Source-of-Truth graph, Paddle subscription state |
| `mcp_tokens`            | Bearer tokens for MCP authentication                                         |
| `mcp_auth_codes`        | OAuth 2.0 Authorization Codes + PKCE challenges (short-lived)                |
| `payments`              | History of Paddle transactions                                               |
| `indexed_repos`         | Cache of indexed GitHub repositories and last commit SHA                     |
| `webhook_subscriptions` | Registered webhooks per workspace (URL, secret, enabled events)              |
| `webhook_deliveries`    | Delivery history with status, retry count, response code, payload           |
| `translations`          | Published translations per page and language                                 |
| `translation_drafts`    | Pending translations awaiting approval                                       |

The `workspaces` table is intentionally wide — most settings are flat columns rather than JSON, which keeps Drizzle types narrow and queries indexable.

## Migration workflow

After editing `src/db/schema.ts`:

```bash
# Generate a new SQL migration file
pnpm drizzle-kit generate

# Apply migrations to the target database
pnpm migrate
```

`pnpm migrate` reads `DATABASE_URL` from the environment and applies any pending migrations in `drizzle/`. Run it in CI or manually after deploying schema changes — schema changes are **not** considered complete until `pnpm migrate` has run against production.

Migrations are forward-only. Avoid destructive changes (column drops, type narrowing) without a two-step deploy: ship the additive change first, backfill, then remove the old column in a follow-up.

## Backups

Neon provides point-in-time recovery within the retention window of the active plan. The Docsbook production project retains 7 days of PITR. For longer-term backups, scheduled logical dumps can be enabled via Neon's branching feature.

## MCP read access

PRO+ workspaces expose two read-only entry points into the database via MCP:

- `get_doc_graph` reads `workspaces.doc_graph` (TOON or JSON)
- `read_doc_sections` reads sections by canonical refs against the same graph

Writes through MCP go through ordinary API handlers and respect plan capabilities.

## Local development

Spin up a local Postgres or use a Neon dev branch. Point `DATABASE_URL` at it, run `pnpm migrate`, then `pnpm dev`. The Drizzle Studio GUI is available with `pnpm drizzle-kit studio`.

## Related

- [Deployment & infrastructure](./deployment.md)
- [Security & data protection](./security.md)
