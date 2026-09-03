---
title: "MCP server security: auth, data residency and limits"
description: "Authentication, token scopes, visitor anonymisation, webhook signing, data residency and the compliance gaps of the Docsbook MCP server, for security reviewers."
---

# MCP Server — Trust & Security

This page documents the security properties of the Docsbook MCP server for teams that review a vendor before connecting AI agents to production infrastructure. It states what the server does, where each kind of data lives, and — in the last two sections — what Docsbook does **not** have yet.

Read it alongside the [MCP Server reference](./mcp.md), which covers the tools themselves.

## How does the Docsbook MCP server authenticate a client?

The Docsbook MCP server uses **OAuth 2.1 Authorization Code with PKCE** — there is no password-based or API-key-only flow.

- The client initiates a standard Authorization Code request, redirecting the user to `docsbook.io/mcp/authorize`.
- After consent, Docsbook issues a short-lived authorization code. The code is exchanged for a Bearer token using the PKCE code verifier, so the code is useless if intercepted in transit.
- Bearer tokens are stored by the MCP client (e.g. Claude Code) and presented on every subsequent call.
- OAuth metadata is published at `https://docsbook.io/.well-known/oauth-authorization-server` in the RFC 8414 format every conforming MCP client can auto-discover.

**Anonymous fall-through is not possible.** Two tools — `get_info` and `find_skill` — return data without authentication because they expose only public catalog information. Every other tool requires a valid Bearer token tied to a Docsbook account.

## What is a Docsbook MCP token allowed to do?

A Docsbook MCP token is bound to one account and carries a **scope**, and the scope is what separates reading from writing. The check runs server-side on every call and cannot be bypassed by the client.

| Scope | What it can do |
|---|---|
| No token | `get_info` and `find_skill` only — public catalog information |
| Read-only | Every reporting, search, outline and analytics tool |
| Read-write | The same, plus committing pages, filing issues, and changing settings |

A tool that spends money — a model-backed call, an outbound fetch, a whole agent run — is additionally refused when the project's balance is empty. That refusal names the project, what the call draws and what is left, so an agent can report the cause instead of retrying.

When a call is refused for any of these reasons, the server returns a structured error rather than a generic 403, so the agent can surface a clear message instead of failing silently.

## What visitor data can an MCP client read?

An MCP client can read a derived `visitor_id`, a country, and page-level events — never an IP address, a name or an email. Docsbook collects page-view events for workspace owners. Visitor identities are anonymised before they reach any external surface, including the MCP server.

```
visitor_id = sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0, 16)
```

- Raw IP addresses are stored in Axiom (the analytics back-end) but are never returned from any MCP tool or API endpoint.
- `get_top_visitors`, `get_page_journeys`, and `get_visitor_activity` return only the derived `visitor_id`, country, and page-level events.
- The salt (`VISITOR_ID_SALT`) is a server-side environment variable. Without it, `visitor_id` values cannot be re-linked to IPs even by someone with direct Axiom access.

Every MCP tool that returns visitor data requires an authenticated token scoped to the workspace owner. There is no anonymous or cross-workspace path to visitor-level data.

## How are Docsbook webhooks signed?

All outbound Docsbook webhook deliveries are signed with **HMAC-SHA256**. The signature is in the `X-Docsbook-Signature-256` header:

```
X-Docsbook-Signature-256: sha256=<hex>
```

The secret is set by the workspace owner at registration time and never returned in plaintext after that. Docsbook uses the same verification scheme as Stripe webhooks, so existing HMAC verification libraries work without modification.

Delivery history, retry state, and the ability to replay a delivery are exposed through MCP tools (`list_webhook_deliveries`, `replay_webhook_delivery`) and the admin panel.

**Chat hooks are not signed.** The pre-, post- and streaming hooks of the docs assistant are plain JSON POSTs with no HMAC header — see [Chat Hooks](./chat-hooks.md). Do not reuse webhook verification code there and assume it verifies anything.

## Data residency and ownership

**Your documentation content stays in your GitHub repository.** Docsbook reads from GitHub via the GitHub API and indexes page metadata — it does not copy markdown files into its own storage.

| Data | Where it lives |
|---|---|
| Markdown content | Your GitHub repository |
| Workspace settings (branding, AI config, plan) | Neon serverless Postgres (AWS us-east-1) with point-in-time recovery |
| Analytics events | Axiom (US region) |
| Cache (search index, skill catalog) | Redis |
| MCP Bearer tokens | Neon Postgres, hashed |

Because the source of truth is GitHub, there is no migration step if you stop using Docsbook. The repository continues to exist, unchanged. Stopping payment stops the metered work — it does not delete your Markdown, your workspace settings, or your analytics history.

## What Docsbook does not have yet

These do not exist today. They are listed here so a security review can rule Docsbook out quickly rather than discover it in week three:

| Capability | Status |
|---|---|
| SOC 2 Type II audit | On the roadmap — no report to share today |
| SAML SSO for signing in to Docsbook | On the roadmap — account sign-in is GitHub OAuth, and MCP clients use the OAuth flow above |
| Data Processing Agreement (DPA) | On the roadmap — no countersigned DPA available today |
| Team accounts and RBAC | On the roadmap — access is per account, with no roles inside a workspace |
| Audit log of admin actions | Not available — `get_change_history` covers content commits, not settings changes |
| Contractual SLA | Not offered |

One capability that **does** exist is easily confused with the first two rows: a *private workspace* can be unlocked by a password or by your own OIDC identity provider (Google Workspace, Entra ID, Okta) through `update_access`. That is SSO for **readers of a docs site**, not SSO for **members of your Docsbook account**.

Two consequences worth stating plainly, because they are the ones reviewers ask about:

- **There are no roles.** Anyone who can sign in to an account can do everything that account can do. Separating a writer from an administrator is not possible today.
- **Chat hooks carry no signature**, so an endpoint you expose to them must authenticate by some other means.

If your organisation has specific compliance requirements — a GDPR DPA, a HIPAA BAA, a security questionnaire — write to `support@docsbook.io` and ask what exists today. The honest answer may be that it does not.

## Related

- [MCP Server](./mcp.md) — tool reference, installation, and what a call draws on.
- [AI Chat Hooks](./chat-hooks.md) — the unsigned pre/post/streaming hooks, and what each can actually change.
- [Webhooks](../webhooks.md) — full event schema, payload examples and signature verification.
- [Sources](./sources.md) — what an agent is allowed to read on your behalf.
