---
title: "Theneo vs Docsbook: pricing, API tooling and AI search compared"
description: "Theneo and Docsbook compared on API-reference tooling, developer portals, MCP/llms.txt for AI agents, and pricing — including the cases where Theneo is the better pick."
tldr: "Theneo builds specifically around API references — REST, AsyncAPI, SOAP, GraphQL and gRPC, with a playground, code generation and spec-diff changelogs; Docsbook is a general documentation platform that reads the Markdown already in your GitHub repo and redeploys on every push."
status: generated
version: "0.1"
---

# Theneo vs Docsbook: pricing, API tooling and AI search compared

Theneo and Docsbook are both AI-forward documentation platforms that treat being usable by an AI agent — not just a human reader — as a first-class feature: both ship an MCP server and `llms.txt` out of the box. Where they differ is scope and starting point. Theneo (founded 2021) is built specifically around API references — REST, AsyncAPI, SOAP, GraphQL and gRPC — with an API playground, code generation and automated changelogs generated from spec diffs, plus a dedicated developer-portal product for private, SSO-gated docs. Docsbook is a general documentation platform: it reads the Markdown you already keep in a GitHub repository and redeploys on every push, whether that repo holds API references, product guides or both.

We make Docsbook. This page names the cases where Theneo is the better choice, and it quotes no Theneo price or feature we could not read on Theneo's own site.

## Side-by-side comparison

| Feature | Theneo | Docsbook |
|---|---|---|
| Best fit | API-heavy teams wanting a dedicated developer portal with a live API playground | Docs already live as Markdown in a GitHub repo, API or otherwise |
| Content source | Imported/authored per-project in Theneo's own web editor, with a live collaboration mode | Reads `README.md` and `docs/` from your repo as written |
| API format support | REST, AsyncAPI, SOAP, GraphQL, gRPC — with a built-in API playground and code generation | OpenAPI support; general Markdown for everything else |
| GitHub sync | Yes — listed as an integration alongside Bitbucket sync, a CLI and a VS Code extension | Yes — the primary workflow; redeploys on every push |
| MCP server | Yes — marketed on the homepage as "MCP Server + llms.txt", tier gating not confirmed from the public pricing page | Included; discovery calls (listing tools, projects) are unmetered on every plan |
| `llms.txt` | Yes — marketed alongside the MCP server | Auto-generated per workspace, plus `llms-full.txt` |
| AI chat for readers | "Ask AI" listed as a homepage feature | Part of the Pro plan ($20/month, $20 AI allowance included) |
| Automated changelog | Yes — generated from API spec diffs, flags breaking changes automatically | Changelog is a Markdown page you maintain yourself |
| Doc versioning | Yes — listed as an API Reference feature | Not supported — one version per branch (see [Documentation versioning](../guides/advanced/documentation-versioning.md)) |
| Private portals / SSO | SAML SSO (Microsoft Entra ID, Okta), custom SSO, password-protected projects — from Business plan up | Privacy & access controls, collaborators — on every plan |
| Base pricing | Free, then $120/month/workspace (Business), $400/month (Growth), custom (Enterprise) | Free, then $20/month per project (Pro), custom (Enterprise) |

## How much does each one cost?

As of 2026-09-20, [theneo.io/pricing](https://theneo.io/pricing) listed a Free plan (1 public project, 2 private projects, up to 2,000 API endpoints, up to 20 team members), a Business plan at $120/month per workspace (2 public / 5 private projects, up to 5,000 endpoints, 50 members), a Growth plan at $400/month (10 public / 10 private projects, up to 10,000 endpoints, 100 members), and custom Enterprise pricing with unlimited projects and endpoints. The site's own feature matrix uses checkmark icons per tier that did not extract as plain text in this check, so exactly which tier unlocks MCP, `llms.txt` or SSO could not be confirmed here — check the current matrix on Theneo's own pricing page before you budget.

Docsbook does not price per workspace or per API endpoint. A Free plan covers branding, navigation, analytics, custom domain, OpenAPI support and collaborators at $0; Pro is $20/month per project with a $20 monthly AI allowance included (this is what unlocks the reader-facing AI chat and live auto-translation) and overage capped by default; Enterprise is a flat price for unlimited projects, contact sales. Current numbers live on [docsbook.io/pricing](https://docsbook.io/pricing), generated from the live pricing constants on every request.

## How different is the setup?

**Theneo** is built around API specs: import or author your REST, AsyncAPI, SOAP, GraphQL or gRPC definitions and Theneo generates an interactive reference with a live API playground, request/response code samples, and a changelog that flags breaking changes automatically when the spec changes. Editing happens in Theneo's own web editor, with live collaboration between team members. GitHub and Bitbucket sync exist as integrations alongside a CLI and VS Code extension.

**Docsbook** starts from a repository, full stop: connect a GitHub repo and the site redeploys on every push, reading the Markdown you already have. OpenAPI specs are supported as one input among others, but there is no dedicated API playground or spec-diff changelog generator — the tradeoff for a platform that treats API docs and product docs the same way rather than specializing in one.

## How do the AI-search features differ?

Both platforms market an MCP server and `llms.txt` as core features rather than an afterthought — this is not a gap either side can claim over the other from what's publicly documented. The differences that could be confirmed from each platform's own site:

- **Reader-facing AI chat** — Theneo's homepage lists "Ask AI" as a feature; Docsbook's AI chat for readers is part of the $20/month Pro plan, with the model provider configurable (OpenAI, Anthropic, Gemini, OpenRouter, or bring your own key on Free).
- **Plan gating** — Theneo's own pricing matrix renders as icons rather than text, so which tier includes MCP/`llms.txt`/Ask AI could not be confirmed in this check. Docsbook's discovery-level MCP calls (listing tools, projects) are unmetered on every plan; AI answers themselves draw on a project's AI balance.
- **Translation** — Docsbook auto-translates to 15 supported language codes as part of the Pro plan, each indexed separately with `hreflang`; Theneo's published feature list does not name a translation or multi-language pipeline as of 2026-09-20.

## When should you choose Theneo?

- Your documentation is primarily API references, and you want a live playground, generated code samples and an automated changelog driven by spec diffs.
- You need SOAP, AsyncAPI or gRPC support specifically — formats Docsbook does not target.
- You want a dedicated private developer portal with SAML SSO (Entra ID, Okta) and are budgeting from $120/month up.

## When should you choose Docsbook?

- Your docs already live (or you want them to live) as Markdown in a GitHub repository, versioned and reviewable like code, covering more than just an API reference.
- You want a documentation platform priced per project from $20/month rather than per workspace from $120/month.
- You want the same platform to cover product guides, an API reference and a multi-language rollout, without specializing in one.

## The bottom line

Theneo is a strong choice if your documentation is API-reference-first and you want a live playground, spec-driven changelogs and enterprise SSO, and $120/month-and-up fits your budget. Docsbook is the better fit if your docs are broader than an API reference, already live as Markdown in a repo, and you want a lower entry price with translation and AI chat available as you grow into the Pro plan.

[Start free — no credit card](https://docsbook.io/?start=1)

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->
- [AI documentation platforms compared](./ai-docs-platform-comparison.md) — the same question across four managed platforms
- [ReadMe vs Docsbook](./readme-vs-docsbook.md) — the same comparison against another API-reference-first competitor
- [Best documentation platforms for startups in 2026](./best-docs-platforms-for-startups-2026.md) — the wider field of platforms a startup might weigh against Docsbook
<!-- /widget -->
