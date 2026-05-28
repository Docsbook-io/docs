# Billing

**Paddle** (`@paddle/paddle-node-sdk`) — per-workspace billing.

## Plans

| Plan | Type | Price | Constant |
|---|---|---|---|
| Free | — | $0 | — |
| PRO | Lifetime | $150 | `proLifetime` in `constants.ts` |
| PRO+ | Monthly | $59/mo | `proPlusMonthly` in `constants.ts` |

## Flow

1. User clicks Upgrade in `PricingModal`
2. Paddle Checkout opens (overlay)
3. After payment Paddle sends a webhook to `/api/paddle`
4. Webhook updates the plan in the `users` / `workspaces` table
5. `plan_capabilities` are recalculated automatically

**Webhooks:** `src/app/api/paddle/route.ts`
**Env vars:** `PADDLE_API_KEY`, `PADDLE_WEBHOOK_SECRET`

## Analytics

Implemented via **Axiom** (`@axiomhq/js`, `next-axiom`).

### Metrics
- Page views
- Unique visitors
- Top pages by traffic
- Referrers (traffic sources)
- Search queries within documentation
- Reader countries
- AI usage: requests, translations, limits, remaining quota

### Periods (depend on plan)
- Free: last 24 hours
- PRO / PRO+: 1 / 7 / 14 / 30 days

**API:** `GET /api/analytics?workspaceId=...&period=24h|7d|14d|30d`
**Components:** `src/components/analytics/DocsAnalytics.tsx`, `AiUsagePanel.tsx`

## Database

**PostgreSQL (Neon serverless)** via Drizzle ORM.

### Main tables

| Table | Description |
|---|---|
| `users` | GitHub ID, username, email, plan (free/pro/pro_plus), Paddle customer ID |
| `workspaces` | ~70 fields: all workspace settings (branding, UI, AI, SEO, domain, languages, AI Chat system prompt + hooks, translation mode, Paddle subscription) |
| `mcp_tokens` | Bearer tokens for MCP authentication |
| `mcp_auth_codes` | OAuth Authorization Code + PKCE (temporary codes) |
| `payments` | Payment history via Paddle |
| `indexed_repos` | Indexed repositories |

**Schema:** `src/db/schema.ts`
**Migrations:** `pnpm migrate` (required after schema changes)
