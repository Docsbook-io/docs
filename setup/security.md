---
title: "Security & Data Protection"
description: "How Docsbook protects user data — TLS, OAuth scopes, secret storage, MCP tokens, webhook signing, and workspace isolation."
---

# Security & Data Protection

This page describes the security model of the Docsbook platform: what is encrypted, what is signed, and where the trust boundaries lie.

## Transport security

All traffic to `docsbook.io` and customer-attached domains is served over HTTPS. Certificates are issued automatically by Let's Encrypt and managed by Vercel. HTTP requests are redirected to HTTPS at the edge.

## GitHub OAuth scopes

Docsbook authenticates users via GitHub OAuth (`next-auth` v5) and requests the **minimum** scope required to index public documentation:

- `read:user` — username and email for the account record
- `public_repo` — read access to public repositories the user owns

Docsbook does **not** request `repo` (private repositories) or `write` scopes.

## Secret storage

User-supplied secrets — AI provider API keys, custom webhook secrets, MCP tokens — are stored encrypted at rest in PostgreSQL. Decryption happens only inside server-side code paths (API routes and cron handlers) and never reaches the browser.

## Payment data

Card numbers, CVCs, and bank details never touch Docsbook servers. The entire payment surface is hosted by [Paddle](./paddle-billing.md), which is PCI-DSS Level 1 certified. Docsbook stores only Paddle customer IDs and transaction metadata.

## MCP authentication

The MCP server uses OAuth 2.0 Authorization Code flow with PKCE:

- Authorization codes are short-lived and stored in `mcp_auth_codes`.
- Bearer access tokens are stored in `mcp_tokens` and scoped to the user's workspaces.
- Every tool call re-checks workspace ownership before reading or writing.
- Tokens can be revoked from the user dashboard at any time.

## Webhook signatures

Outbound webhook deliveries are signed with the per-subscription HMAC secret using SHA-256, in the Stripe-compatible format:

```
X-Docsbook-Signature: t=<unix_ts>,v1=<hex_hmac>
```

The signed payload is `<unix_ts>.<raw_body>`. Verify on your side by recomputing the HMAC with the secret returned at registration time. Reject any request older than five minutes to prevent replay.

## Workspace isolation

Every API route — REST, MCP, and cron — re-resolves the requested workspace and verifies that the authenticated user owns it. There is no cross-workspace data access at the database layer; the `workspaceId` foreign key is part of every relevant query's `WHERE` clause.

## Vendor lock-in

Documentation content lives in the user's own GitHub repository. Docsbook holds only derived state — indexes, translations, analytics events. Canceling a subscription does not delete the source files; they remain in GitHub.

## Public visibility

Published documentation is intentionally public — that is the product. Workspaces themselves (settings, analytics, AI configuration) are private and visible only to the GitHub owner.

## Related

- [Webhooks reference](../webhooks.md)
- [MCP server overview](../ai/mcp.md)
- [Paddle billing](./paddle-billing.md)
