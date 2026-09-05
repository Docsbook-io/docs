---
title: "MCP server security: what a token can do, and what it cannot"
description: "The Docsbook MCP server's authentication model, token scopes, ownership checks, call log, outbound guards and the gaps against the MCP specification — written for a security reviewer."
tldr: "Docsbook's MCP server authenticates with an OAuth authorization-code flow and issues an opaque Bearer token carrying one of two scopes, read or read-write. Every tool resolves its project by owner, so a token cannot touch a project its account does not own. Tokens do not expire, nothing is rate-limited, and there is no SOC 2 report, DPA, SSO or role model today."
---

# MCP server security

This page is written for the person who has to approve connecting an AI agent to Docsbook. It states what the [MCP server](./mcp.md) actually does today — how a client authenticates, what each scope can reach, what is written down, what leaves the network — and then names, in two separate sections, where Docsbook falls short of the Model Context Protocol specification and what compliance artefacts do not exist yet.

Nothing here is aspirational. Where a control is missing it is listed as missing.

## What you get

A connected client holds one opaque Bearer token, bound to one Docsbook account, carrying one of two scopes. The scope is chosen by a human on a consent screen — not requested by the client. Every tool that acts on a project resolves that project by *owner*, so a token that names a workspace id belonging to somebody else gets nothing back, not that workspace: that is the boundary between tenants, and it holds on every tool.

The boundary between reading and writing is narrower than the two scope names suggest, and the section below says exactly which tools enforce it and which do not. Read that before you treat a read-only token as a containment measure.

Every metered call writes one row to your project's own call log: which tool, what went in, what came back, how long it took and what it drew. Arguments and results are redacted by key before they are stored, so an API key passed to a tool is never written down.

What you do not get: token expiry, refresh tokens, rate limiting, roles inside an account, or an audit report.

## How the authentication works

### The authorization flow

Docsbook is its own authorization server and its own resource server. It issues opaque tokens for itself; it never accepts, forwards or re-uses a token issued by anyone else.

| Step | What happens |
|---|---|
| Discovery | An unauthenticated request to the server endpoint returns `401` with `WWW-Authenticate: Bearer resource_metadata="…/.well-known/oauth-protected-resource"`. That document names the resource and its authorization server; `/.well-known/oauth-authorization-server` carries the endpoints in RFC 8414 form. |
| Client registration | A `POST` to the registration endpoint returns a fresh `client_id` in RFC 7591 form. Clients are **not persisted** — the id is minted statelessly, and the authorization endpoint accepts any `client_id`. |
| Authorization | The client sends `response_type=code`, a `redirect_uri`, a `state` of at least 8 characters, and normally a PKCE `code_challenge`. The parameters are stored against the `state` and the browser is sent to a consent page. The row expires after 10 minutes. |
| Consent | The consent page requires a signed-in Docsbook account and an explicit click. It carries one checkbox — *Allow editing documentation* — which decides the scope. There is no "remember this client" cookie and no silent re-approval path: every authorization shows the screen. |
| Token exchange | The code is exchanged at the token endpoint for a Bearer token. When the client supplied a PKCE challenge with method `S256`, the verifier is checked and a mismatch is refused. The code is single-use: it is cleared on the first successful exchange. |

The published metadata declares a public-client model — `code_challenge_methods_supported: ["S256"]`, `token_endpoint_auth_methods_supported: ["none"]`, `grant_types_supported: ["authorization_code"]`. There is no client secret and no client-credentials grant.

### What the token is

The token is 48 bytes from the platform CSPRNG, rendered as 96 hexadecimal characters. It carries no claims: it is a lookup key into a row holding the account, the scope, and a revocation timestamp.

- **It does not expire.** No `expires_in` is returned and no refresh token is issued. A token is valid until it is revoked.
- **Revocation is immediate.** Revoking from the panel stamps the row, and every subsequent call fails the lookup — there is no cache in front of it.
- **It is stored as issued, not hashed.** Treat a Docsbook MCP token the way you would treat a password: if the machine holding it is compromised, revoke it rather than assume it aged out. (What *is* encrypted at rest is listed under [what leaves your workspace](#what-leaves-your-workspace).)
- **Last use is recorded** on every call, so an unused token is visible in the panel's token list.

### What each scope can do

Scope is a single string compared exactly. Anything that is not the write scope is treated as read-only — an unrecognised value fails closed.

| Caller | What answers |
|---|---|
| No token, unscoped endpoint | Nothing. `401` with the discovery header. |
| No token, repo-scoped endpoint (`/{owner}/{repo}/api/mcp/server`) | Five tools: `get_info`, `find_skill`, `find_widget`, `list_content_widgets`, and `search` over that one published site. Never metered, never billed to anyone. |
| Read-only token | Every reporting, search, outline and analytics tool, plus `run_docs_analyze`, which runs in audit mode — **and, today, the settings writers listed below** |
| Read-write token | Everything the account can do |

**The scope check does not cover every writer today, and you should plan around that.** It is enforced on exactly eight tools: `write_docs`, `create_issue`, `connect_source`, `configure_source`, `enable_agent`, and the three `run_docs_*` runs that write. Those refuse a read-only token before doing anything.

Every other state-changing tool — the `update_*` and `set_*` settings writers, `update_access`, webhook registration and removal, goal and funnel creation, translation upload, approval and deletion, `create_workspace` — is gated only by project ownership, not by scope. A read-only token can therefore change a project's settings, arm a webhook or delete a translation on a project its account owns. It still cannot commit a page, file an issue, connect a source or arm an agent.

Treat the read-only scope as "cannot publish or wire up new capabilities", not as "cannot change anything". If containment matters more than that, use a separate Docsbook account that owns only the project you are willing to expose. This is a defect, listed again under [limits](#limits-and-open-questions), not a design.

A tool that does enforce the check answers a read-only token with a structured `READ_ONLY_TOKEN` error naming the tool and saying how to re-authorize — not a bare `403`, and not a silent no-op. The same shape applies when a project's balance is empty (`INSUFFICIENT_BALANCE`, naming the project, the price and the remainder) and when a plan does not include the capability (`PLAN_RESTRICTION`, naming the tier).

The anonymous `search` is the only tokenless tool that reads a project, and it is refused three ways: on an endpoint pinned to no project, on a project whose visibility is private (which also covers a lapsed plan), and when the project has no balance left to pay for the query embedding. It takes no project argument, so it can only ever read the site it is pinned to.

### What one token cannot reach

Every tool resolves its target workspace from the explicit `workspace_id`, the `repo` argument, or the endpoint's own pin — and in all three cases the lookup is filtered by the token's account. A workspace the account does not own resolves to nothing, and the tool answers "workspace not found". The billing resolver applies the same filter, so naming a stranger's project id cannot draw down a stranger's balance either.

Two further boundaries are worth stating because they surprise people:

- **`write_docs` commits to the Docsbook-hosted repository using Docsbook's own GitHub credentials.** A site served from a repository in your own GitHub account is refused with `NO_GITHUB_ACCESS` rather than committed to. An MCP token is therefore not a way to push to your GitHub organisation.
- **A skill running in audit mode cannot mutate.** While an `audit`-mode skill is active, an explicit list of writers plus every tool whose name begins `update_`, `set_`, `register_webhook_`, `enable_` or `disable_` is refused before it executes. `run_docs_analyze` sets that mode for its whole run, which is why it is safe on a read-only token.

## What is recorded

Every MCP call — metered or not, successful or not — writes one row to the project's call ledger, and the project's owner can read it in the Feeds panel.

| Recorded | Not recorded |
|---|---|
| Tool name, billing class, price, cents actually deducted, duration, success flag, background run id, and who asked (agent, panel, schedule, event) | The caller's IP address |
| The call's arguments and its result, serialised, redacted and truncated | The raw payload — only the redacted, truncated rendering is stored |
| The account that called and the project the call was about | Any value under a key containing `apikey`, `api_key`, `authorization`, `credential`, `password`, `passwd`, `secret`, `token`, `private_key`, `privatekey`, `session` or `cookie` |

Two details of the redaction matter for review. It matches on the **key**, case-insensitively and as a substring, not on the shape of the value — guessing what a secret looks like has a shape it misses. And it runs on the way *out* as well as the way in, so a tool that echoes its own input cannot leak a key through its result. Each side is cut at 8 000 characters with a marker saying how many were dropped.

Reader-level analytics never carry an identity to an MCP client. A visitor is a pseudonym: `sha256(salt | repository | ip)`, truncated to 16 hexadecimal characters, with the salt held server-side. `get_top_visitors`, `get_page_journeys` and `get_visitor_activity` return that pseudonym, a country and page-level events; no tool returns an IP address, a name or an email. The pseudonym is scoped to one repository, so the same reader on two of your sites is two unrelated ids.

## What leaves your workspace

| Data | Where it goes | Encrypted at rest |
|---|---|---|
| Page text, headings and titles | Copied into Docsbook's Postgres for full-text search, and embedded as vectors for semantic search | No — stored as content |
| Page text sent for embedding, chat and agent work | OpenRouter, the model provider, on Docsbook's key or on your own key if you set one | n/a — in transit only |
| Reader events | Docsbook's analytics store, including raw IPs, which no API returns | n/a |
| Your OIDC client secret for private docs | Docsbook's Postgres | **Yes** — AES-GCM, key derived from the platform secret |
| A GitHub token you connect for a private repository source | Docsbook's Postgres | **Yes** — same scheme; the API answers only whether a token exists |
| Your own model API key (bring-your-own-key) | Docsbook's Postgres, and the provider on every call it funds | No — stored as given, and stripped from every workspace payload the API returns |
| MCP Bearer tokens | Docsbook's Postgres | No — see above |
| Pages fetched by `fetch_url`, `read_source` and the crawler | Out to the address you named | n/a |

Two claims the security page of a documentation vendor usually makes, corrected:

- **"Your content never leaves your repository" is not true here.** Docsbook stores a searchable copy of your page text and its vector embeddings, and sends page text to a model provider to build those embeddings and to answer chat and agent calls. What *is* true is that GitHub remains the source of truth, so stopping payment stops the metered work without deleting your Markdown.
- **Outbound fetches are guarded, not merely trusted.** Before any fetch the scheme is checked, the hostname is resolved, and a resolved address in a private or reserved range is refused — and the check is re-run on every redirect hop, so a public URL cannot bounce into an internal one. `robots.txt` is honoured and the response is capped. The skill fetcher is narrower still: it will only fetch from the catalog's own host and path prefix, so it cannot be turned into an arbitrary-URL proxy.

## Webhooks and chat hooks are not the same thing

Outbound webhook deliveries are signed. The signature is HMAC-SHA256 over **the exact bytes sent**, in `X-Docsbook-Signature-256: sha256=<hex>`, alongside `X-Docsbook-Event`. A Discord or Slack incoming-webhook URL is reshaped for that platform before signing, so the signature always covers what your endpoint actually receives. The secret is set at registration, is at least 16 characters, and is never returned in plaintext afterwards. Delivery attempts time out at 15 seconds and the response is stored truncated.

**Chat hooks carry no signature.** The pre-, post- and streaming hooks of the docs assistant are plain JSON `POST`s with a 5-second timeout and no HMAC header. Do not reuse your webhook verification code there and assume it verified something. The pre-hook can also return `inject_context`, whose text enters the assistant's prompt — an endpoint you point a chat hook at can therefore influence what the assistant says, so treat it as trusted infrastructure, authenticate it by some other means, and do not point one at a URL you do not control.

## Why this is the right way (evidence)

| Rule Docsbook follows | Why it matters to the thing consuming it | Source |
|---|---|---|
| Mint our own opaque tokens; never accept or forward one issued elsewhere | "MCP servers **MUST NOT** accept any tokens that were not explicitly issued for the MCP server" | [MCP security best practices, Token Passthrough](https://modelcontextprotocol.io/specification/2026-07-28/basic/security_best_practices) |
| Answer an unauthenticated call with `WWW-Authenticate` naming the protected-resource metadata | "MCP servers **MUST** implement OAuth 2.0 Protected Resource Metadata (RFC9728)" | [MCP authorization](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization) |
| Verify the PKCE `S256` verifier at the token endpoint and publish `code_challenge_methods_supported` | "If `code_challenge_methods_supported` is absent, the authorization server does not support PKCE and MCP clients **MUST** refuse to proceed" | [Authorization security considerations](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization/security-considerations) |
| Show a consent screen on every authorization instead of remembering a client | The confused-deputy attack works by reaching a *skipped* consent screen: "Cookie present, consent skipped" | [MCP security best practices, Confused Deputy](https://modelcontextprotocol.io/specification/2026-07-28/basic/security_best_practices) |
| Keep the scope set to two, chosen by a person, rather than a catalog of scopes a client asks for | Poor scope design means "expanded blast radius: stolen broad token enables unrelated tool/resource access" | [MCP security best practices, Scope Minimization](https://modelcontextprotocol.io/specification/2026-07-28/basic/security_best_practices) |
| Refuse a resolved private or reserved IP, and re-check on each redirect | Clients and servers **SHOULD** block "Link-local: `169.254.0.0/16` (including cloud metadata endpoints)" | [MCP security best practices, SSRF](https://modelcontextprotocol.io/specification/2026-07-28/basic/security_best_practices) |
| Bind every tool's target to the caller's ownership rather than to an id it supplied | Servers "**MUST NOT** treat possession of a state handle as authentication" and should bind state to the verified principal | [MCP security best practices, State Handle Hijacking](https://modelcontextprotocol.io/specification/2026-07-28/basic/security_best_practices) |
| Vet the skills your agent loads, including ours | "Skills that fetch data from external URLs pose particular risk, as fetched content may contain malicious instructions" | [Anthropic, Agent Skills](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) |

One more point belongs to your client rather than to us: the MCP specification tells clients to "consider tool annotations to be untrusted unless they come from trusted servers", and to keep "a human in the loop with the ability to deny tool invocations" ([MCP tools](https://modelcontextprotocol.io/specification/2026-07-28/server/tools)). A read-write Docsbook token is exactly the case that deserves that human.

## Where Docsbook does not meet the MCP specification today

These are measured against the `2026-07-28` revision. Each is a gap in Docsbook, not a disagreement with the spec.

| Requirement | What Docsbook does | Severity for a reviewer |
|---|---|---|
| "Authorization servers **MUST** validate exact redirect URIs against pre-registered values" | Validates the `redirect_uri`'s **scheme** against an allowlist — HTTPS, loopback, and a fixed list of editor deep-link schemes — and does not compare it to a registered value at exchange time, because clients are not persisted | The one to raise first. Combined with a consent screen that does not display the redirect target, a user who clicks through a crafted link can approve a grant that lands somewhere else. The screen does require a deliberate click every time; it is not skippable. |
| "Authorization servers **SHOULD** issue short-lived access tokens" and rotate refresh tokens for public clients | Issues a token with no expiry and no refresh token | A leaked token is valid until somebody revokes it |
| Servers **MUST** "rate limit tool invocations" | Does not rate-limit. The project balance is the only limiter, and an unmetered discovery call has no limiter at all | Budget your risk in money, not in requests |
| PKCE at the authorization code | Verified when the client supplies a challenge with method `S256`; a client that supplies none still completes the flow | Every mainstream MCP client sends PKCE; the server does not currently insist |
| Protocol revision | The server speaks the initialization-based revisions the current SDK supports, latest `2025-11-25`, over a stateless HTTP transport | A `2026-07-28`-only client will not connect |
| `scope` in the `WWW-Authenticate` challenge and `scopes_supported` in metadata | Neither is published; scope is picked on the consent screen | Clients cannot discover the two scopes programmatically |

## What Docsbook does not have yet

Listed so a review can rule Docsbook out in an hour rather than in week three.

| Capability | Status |
|---|---|
| SOC 2 Type II | Not offered — no report to share |
| Data Processing Agreement | Not offered — no countersigned DPA today |
| Contractual SLA | Not offered |
| SAML SSO for signing in to Docsbook | Not offered — account sign-in is GitHub OAuth |
| Team accounts, roles, RBAC | Not offered — access is per account, and anyone who can sign in to an account can do everything that account can do |
| Audit log of account events | Not offered — sign-ins, token issuance and plan changes are not exposed as an event log. MCP tool calls *are* logged, in full, per project; content commits are readable through change history |
| Penetration test report | Not offered |

One capability is routinely confused with the second and fourth rows: a **private workspace** can be gated by a password or by your own OIDC provider through `update_access`, on every plan. That is single sign-on for the **readers of your documentation site**. It is not single sign-on for the **members of your Docsbook account**, and it grants no MCP access.

If your organisation needs a specific artefact — a GDPR DPA, a BAA, a completed questionnaire — write to `support@docsbook.io` and ask what exists. The answer today may well be that it does not.

## Limits and open questions

- **Under question: hosting regions.** This page deliberately names no region for the database or the analytics store. Both are managed services whose region is a deployment setting rather than something a reader can verify from Docsbook's behaviour, and an earlier version of this page named regions with no source. Ask support for the current answer in writing if data residency is part of your review.
- **The pseudonymous visitor id is a pseudonym, not anonymisation.** It is a salted hash of an IP address truncated to 64 bits. Anyone holding the salt *and* the raw event store could re-derive it; the guarantee is that the salt is not in the data and no API returns an IP. Whether that satisfies your regulator is a question for your regulator.
- **A read-write token is a full administrative credential.** There is no way to grant "may edit pages but may not change settings", or "may read analytics but not chat transcripts". The scope ladder has two rungs.
- **The read-only scope is incompletely enforced.** Eight tools check it; the settings, webhook, goal and translation writers do not, and some of those tools' own descriptions claim they require a read-write token when nothing checks. Until that is closed, the reliable boundary is account ownership, not scope — so isolate by account, and read the enforced list above rather than a tool's description.
- **Nothing here is independently attested.** Every statement above is checkable in Docsbook's behaviour — issue a read-only token and watch a writer refuse; connect a project you do not own and watch it not resolve — but no third party has audited it. Treat this page as a specification you can test, not as a certification.
- **Availability and price are on the [pricing page](https://docsbook.io/pricing).** No figure is quoted here, because a price copied into documentation goes stale in silence.

## Related

- [MCP Server](./mcp.md) — the tools themselves, and what a call draws on
- [Agent-ready content](./README.md) — the four machine surfaces and how they fit together
- [Docs Skills](./skills.md) — what a skill can and cannot do while it runs
- [Webhooks](../reference/webhooks.md) — the full event schema and signature verification
- [AI Chat Hooks](../ai-chat/chat-hooks.md) — the unsigned pre/post/streaming hooks
- [Sources](../ai-chat/sources.md) — what an agent is allowed to read on your behalf
