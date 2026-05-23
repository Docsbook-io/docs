---
title: "Paddle Billing Integration"
description: "How Docsbook integrates with Paddle for per-workspace billing — checkout flow, webhook events, environment variables, and refund policy."
---

# Paddle Billing Integration

Docsbook uses [Paddle](https://www.paddle.com/) as its Merchant of Record for all subscriptions and one-time payments. Paddle handles tax compliance, fraud screening, PCI-DSS card storage, and payouts. Docsbook never touches raw card data.

## Architecture

The billing flow is per-workspace:

1. The user clicks **Upgrade** in `PricingModal`.
2. The Paddle Checkout overlay opens with the workspace ID attached as `customData`.
3. After successful payment, Paddle sends a webhook to `https://docsbook.io/api/paddle`.
4. The webhook handler updates the `users` and `workspaces` tables in Postgres.
5. `plan_capabilities` are recomputed on the next request — gating new features automatically.

## Supported plans

| Plan  | Type      | Price        |
| ----- | --------- | ------------ |
| Free  | —         | $0           |
| PRO   | Lifetime  | $150 one-off |
| PRO+  | Recurring | $59 / month  |

Prices and product IDs live in `src/utils/constants.ts` (`proLifetime`, `proPlusMonthly`).

## Implementation files

| File                                       | Responsibility                            |
| ------------------------------------------ | ----------------------------------------- |
| `src/app/api/paddle/route.ts`              | Webhook endpoint (signature verification) |
| `src/utils/paddle/handleWebhook.ts`        | Event handler — updates plans             |
| `src/utils/paddle/checkout.ts`             | Server-side checkout URL generation       |
| `src/components/PaddleCheckout.tsx`        | Paddle.js overlay loader                  |
| `src/components/PaddleQueryHandler.tsx`    | Reads `?paddle=success` and refreshes UI  |

## Environment variables

```bash
PADDLE_API_KEY=pdl_live_...        # Server-side Paddle API key
PADDLE_WEBHOOK_SECRET=pdl_ntfn_... # HMAC secret for webhook signature
```

In sandbox use `pdl_sdbx_*` keys against `sandbox-api.paddle.com`.

## Handled webhook events

| Event                  | Effect                                                            |
| ---------------------- | ----------------------------------------------------------------- |
| `subscription.created` | Activate plan, set `plan_started_at`, store Paddle customer ID    |
| `subscription.updated` | Sync plan tier, next billing date, payment method status          |
| `subscription.canceled`| Downgrade to Free at period end, emit `plan.downgraded` event     |
| `transaction.completed`| Insert row in `payments` table; for lifetime PRO — activate plan  |

All events go through `handleWebhook`, which is idempotent on Paddle's `notification_id`.

## Refund policy

Docsbook offers a **30-day refund** on both PRO lifetime and the first month of PRO+. Refunds are issued through the Paddle dashboard; the resulting `transaction.payment_refunded` webhook downgrades the workspace.

## Local testing

1. Create a sandbox account at `sandbox-vendors.paddle.com`.
2. Use sandbox keys in `.env.local`.
3. Forward webhooks with `ngrok http 3000` and register the public URL as a notification destination in the Paddle dashboard.
4. Trigger test transactions from the sandbox checkout — they accept card `4242 4242 4242 4242`.

## Related

- [Pricing specification](../content/setup/pricing-spec.md)
- [MCP server overview](../ai/mcp.md)
