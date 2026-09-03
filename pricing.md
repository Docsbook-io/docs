---
title: "Docsbook pricing: what costs money and what does not"
description: "Docsbook meters four kinds of AI work against each project's own balance. Hosting, custom domains, readers, search and GitHub sync are never metered."
---

# Docsbook pricing: what costs money and what does not

Docsbook meters **four** things, all of them AI work, charged against the balance of the project that asked for them. Publishing a documentation site, serving its pages, full-text search, GitHub sync and recording analytics are not metered — they do not move a balance. This page explains the mechanism; the current figures live on [the Docsbook pricing page](https://docsbook.io/pricing).

## What draws on a project balance

Exactly four kinds of work spend a Docsbook project's balance. Each appears as its own row in **Spend by source** on the project's Limits card:

- **Readers (AI Chat)** — an AI answer given to a reader of your published documentation.
- **Admin & AI Agent** — an agent run you or a connected agent started, including metered MCP tool calls.
- **AI Translations** — translating a page into another language.
- **Semantic Index** — building the embeddings the AI chat retrieves from.

Nothing else moves the balance. Hosting the site, a custom domain and its TLS certificate, readers browsing, editors writing, GitHub sync, full-text search, branding, analytics and MCP read calls are all unmetered, however much of them you use.

You can also cap any one of the four for the current cycle from the Limits card. A source that reaches its cap stops running until the next cycle, and a cap of $0 switches that source off entirely.

## Where to read the current prices

Read prices on [docsbook.io/pricing](https://docsbook.io/pricing), never here. That page is generated from Docsbook's billing constants on every request, so it cannot go stale; a price copied into a documentation page in Git can, and an assistant will keep quoting the stale copy for months after the real number changes. For the same reason this page names no plan price.

The machine-readable version of the same page is at [docsbook.io/pricing.md](https://docsbook.io/pricing.md). It is plain Markdown, so an agent or a crawler can read the prices without rendering HTML.

## What a project balance is

A **project balance** is the money attached to one Docsbook project, spent on the four kinds of AI work listed above. Every new project is created with **$1.00** of balance, and the owner tops it up from the billing screen. Balances are per project, not per account: one project running out does not stop another.

## How much free credit a new project gets

A new Docsbook project starts with **$1.00** of balance, and a further **$5.00** can be claimed once the project is **3 minutes old** — press **Claim** on the project's billing card. The $5.00 is claimed, not granted: nothing adds it on your behalf, and nothing else on the account is topped up automatically.

Those two amounts are the only credit Docsbook gives away. Everything after them is a top-up you pay for.

## How top-ups work

You name the amount when you top up a Docsbook project. The smallest single top-up is **$20.00** and the largest is **$5,000.00**; for more than $5,000.00, top up twice. The amount lands on the balance of the one project you chose, not on the account.

Top-ups do not expire and nothing is refilled on a schedule. If you want a recurring amount, set up a monthly payment of your own on the billing screen — that tops the same balance up each month.

## What Docsbook charges for AI usage

Docsbook charges the AI provider's real price for the model that answered, **plus 900%**. The model, its per-1M-token rate and the markup are all shown in your dashboard, so the amount deducted is one you can check against the provider's own price list. Choosing a cheaper model makes the same balance go further.

Bringing your own provider API key is supported. When you do, you pay the provider directly and Docsbook bills you nothing for that usage.

## What MCP tool calls cost

Docsbook MCP tool calls are charged a flat price fixed before the call runs, independent of the size of the answer. Discovery calls — describing the server, finding a skill or a widget, listing your projects, creating one — are never metered. Reads, writes, analytics scans, and full agent runs each sit in their own price class.

The class and price of every tool is on its row in the **MCP** section of your admin panel and in the [MCP tools reference](./reference/mcp-tools.md). Every metered call also appears line by line in the project's Feeds panel — which tool, whether it worked, how long it took and what it cost.

## What happens when a project's balance runs out

When a Docsbook project's balance runs out, a metered call is refused **before it runs**. The refusal names which project ran out, what the call would have cost, what is left, and where to top that project up. Nothing is deleted and the documentation site stays online — readers keep browsing, search keeps working, GitHub sync keeps running.

Free discovery calls keep working too, so an agent connected over MCP can still find out what happened instead of failing silently.

## Does anything refill on a schedule?

No. A Docsbook project balance is topped up, not granted on a schedule, and there is no monthly allowance to run out of. The only credit Docsbook gives away is the **$1.00** a project starts with and the **$5.00** claimed at 3 minutes old.

## Can I leave, and what do I keep?

Your Markdown always stays in your own GitHub repository. Docsbook renders those files; it never stores your content in a proprietary format. Point another tool at the same repository and you keep every page, every image and every link — there is nothing to export first.

## Related

- [Docsbook FAQ](./faq.md) — cancellation, payment, data ownership and sync questions
- [Use cases](./use-cases.md) — what teams publish documentation to change
- [MCP tools reference](./reference/mcp-tools.md) — every tool, its parameters and its price class
- [AI usage and costs](./analytics/tracking/ai-usage.md) — where spend shows up in your analytics

<!-- widget:cta -->

## See what a project costs you

Create a project, publish it, and watch the balance while you use it. It starts with $1.00 on it, and $5.00 more is yours to claim three minutes later.

[Start free — no credit card](https://docsbook.io/start)

<!-- /widget -->
