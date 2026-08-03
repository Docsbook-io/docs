---
title: "MCP Server — Trust & Security"
description: "Authentication, access control, data privacy, webhook signing, and data residency for the Docsbook MCP server. Intended for security reviewers."
---

# MCP Server — Trust & Security

This page documents the security properties of the Docsbook MCP server for teams that need to review it before connecting AI agents to production infrastructure.

## Authentication

The MCP server uses **OAuth 2.1 Authorization Code with PKCE** — there is no password-based or API-key-only flow.

- The client initiates a standard Authorization Code request, redirecting the user to `docsbook.io/mcp/authorize`.
- After consent, Docsbook issues a short-lived authorization code. The code is exchanged for a Bearer token using the PKCE code verifier, so the code is useless if intercepted in transit.
- Bearer tokens are stored by the MCP client (e.g. Claude Code) and presented on every subsequent call.
- OAuth metadata is published at `https://docsbook.io/.well-known/oauth-authorization-server` in the RFC 8414 format every conforming MCP client can auto-discover.

**Anonymous fall-through is not possible.** Two tools — `get_info` and `find_skill` — return data without authentication because they expose only public catalog information. Every other tool requires a valid Bearer token tied to a Docsbook account.

## Access control

Every tool in the server declares a minimum plan. The plan is checked server-side on each call; it cannot be bypassed by the client.

| Plan | What is accessible |
|---|---|
| Free | Workspace read/write, branding, UI settings, navigation, 24 h analytics, `find_skill`, SEO/GEO/AEO |
| PRO | + AI settings, language settings, full analytics (up to 30 d), pending translations |
| PRO+ | + page journeys, visitor drill-down, `query_events` |
| Business | + custom domain |

When a token does not have the required plan, the server returns a structured error — not a generic 403 — so the agent can surface a clear message rather than silently failing.

## Privacy and analytics data

Docsbook collects page-view events for workspace owners. Visitor identities are anonymised before they reach any external surface, including the MCP server.

```
visitor_id = sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0, 16)
```

- Raw IP addresses are stored in Axiom (the analytics back-end) but are never returned from any MCP tool or API endpoint.
- `get_top_visitors`, `get_page_journeys`, and `get_visitor_activity` return only the derived `visitor_id`, country, and page-level events.
- The salt (`VISITOR_ID_SALT`) is a server-side environment variable. Without it, `visitor_id` values cannot be re-linked to IPs even by someone with direct Axiom access.

The MCP tools that return visitor data are gated at the PRO+ plan and require an authenticated token scoped to the workspace owner.

## Webhook signing

All outbound webhook deliveries are signed with **HMAC-SHA256**. The signature is in the `X-Docsbook-Signature-256` header:

```
X-Docsbook-Signature-256: sha256=<hex>
```

The secret is set by the workspace owner at registration time and never returned in plaintext after that. Docsbook uses the same verification scheme as Stripe webhooks, so existing HMAC verification libraries work without modification.

Delivery history, retry state, and the ability to replay a delivery are exposed through MCP tools (`list_webhook_deliveries`, `replay_webhook_delivery`) and the admin panel.

## Data residency and ownership

**Your documentation content stays in your GitHub repository.** Docsbook reads from GitHub via the GitHub API and indexes page metadata — it does not copy markdown files into its own storage.

| Data | Where it lives |
|---|---|
| Markdown content | Your GitHub repository |
| Workspace settings (branding, AI config, plan) | Neon serverless Postgres (AWS us-east-1) with point-in-time recovery |
| Analytics events | Axiom (US region) |
| Cache (search index, skill catalog) | Redis |
| MCP Bearer tokens | Neon Postgres, hashed |

Because the source of truth is GitHub, there is no migration step if you stop using Docsbook. The repository continues to exist, unchanged. Cancelling a subscription downgrades the plan — it does not delete workspace settings or analytics history.

## Compliance roadmap

The following are in active development and not yet available:

| Feature | Status |
|---|---|
| SOC 2 Type II audit | On the roadmap |
| SAML SSO | On the roadmap |
| Data Processing Agreement (DPA) | On the roadmap |
| Team accounts and RBAC | On the roadmap |

If your organisation has specific compliance requirements — GDPR DPA, HIPAA BAA, security questionnaire — contact us at `hi@docsbook.io` to discuss what we can provide today.

## Related

- [MCP Server](./mcp.md) — Tool reference and installation.
- [AI Chat Hooks](./chat-hooks.md) — HMAC-signed pre/post-LLM hooks.
- [Webhooks](../webhooks.md) — Full event schema and payload examples.
