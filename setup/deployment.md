---
title: "Deployment & Infrastructure"
description: "Docsbook infrastructure stack — Vercel hosting, Neon Postgres, Redis cache, Axiom logging, Paddle billing, and the full environment variable reference."
---

# Deployment & Infrastructure

Docsbook runs as a Next.js 16 application on Vercel, backed by a serverless Postgres database, a Redis cache, and a managed log/analytics pipeline.

## Stack

| Layer          | Service                              | Notes                                                  |
| -------------- | ------------------------------------ | ------------------------------------------------------ |
| Hosting        | Vercel                               | App Router with SSR, SSG, and ISR                      |
| Database       | Neon (serverless PostgreSQL)         | Accessed via Drizzle ORM                               |
| Cache          | Redis (`ioredis`)                    | Used for skills index, doc graph, rate limits          |
| CDN            | Vercel Edge Network                  | Static assets and ISR responses                        |
| Custom domains | Vercel Domains API                   | `addDomain` / `removeDomain` in `src/utils/vercel/`    |
| Cron           | Vercel Cron                          | Routes under `src/app/api/cron/*`                      |
| Logging        | Axiom (`@axiomhq/js`, `next-axiom`)  | Structured events and request logs                     |
| Billing        | Paddle                               | See [Paddle billing](./paddle-billing.md)              |
| Email          | Resend                               | Plan notifications, invoices, weekly digests           |
| AI             | OpenRouter (default), per-workspace overrides | Multi-provider with user-supplied keys        |

## Runtime selection

Most routes run on the Node.js runtime to access Postgres, Redis, and Octokit. The following run on the Edge runtime:

- `src/app/llms.txt/route.ts` and `llms-full.txt/route.ts`
- `src/app/[user]/llms.txt/route.ts`
- Static OG image generation under `src/app/api/og/`

Routes that initiate AI streaming (`api/ai-chat`, `api/translate`) use Node.js to keep long-lived streams stable.

## Cron jobs

| Schedule  | Route                                  | Purpose                                |
| --------- | -------------------------------------- | -------------------------------------- |
| Daily     | `src/app/api/cron/stale-check/`        | Emits `content.outdated` webhooks      |

Cron jobs are configured in `vercel.json` and protected by a shared `CRON_SECRET` header.

## Environment variables

```bash
# Database and cache
DATABASE_URL=postgres://...
REDIS_URL=redis://...

# Auth
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
NEXTAUTH_SECRET=
NEXTAUTH_URL=https://docsbook.io

# Billing — see paddle-billing.md
PADDLE_API_KEY=
PADDLE_WEBHOOK_SECRET=

# Observability
AXIOM_TOKEN=
AXIOM_DATASET=

# Email
RESEND_API_KEY=

# AI default provider
OPENROUTER_API_KEY=

# Custom domains
VERCEL_TOKEN=
VERCEL_PROJECT_ID=
VERCEL_TEAM_ID=

# Public
NEXT_PUBLIC_APP_URL=https://docsbook.io
```

Place these in `.env.local` for development and in Vercel project settings for production. Secrets are never committed.

## Deploys

Every push to `main` triggers a production deploy on Vercel. Preview deploys run on each pull request. Database migrations are not auto-applied — run `pnpm migrate` against the target environment after merging schema changes. See [Database schema](./database.md).

## Related

- [Paddle billing integration](./paddle-billing.md)
- [Security & data protection](./security.md)
- [Database schema](./database.md)
