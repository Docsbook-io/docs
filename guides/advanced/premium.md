---
title: "What Docsbook includes and what actually costs money"
description: "The capabilities a Docsbook project can use, which of them draw on the project balance, and where to read the prices that are current right now."
---

# What Docsbook includes, and what costs money

Docsbook separates two questions that documentation tools usually mix. **What your site can do** is a list of capabilities. **What you pay** is metered in money against each project's balance, and only work that calls an AI model spends it.

Prices change, and a price copied into a documentation page goes stale silently. Read the current ones at **[docsbook.io/pricing](https://docsbook.io/pricing)** — that page is generated from the live billing constants on every request. This page describes the capabilities and the metering, and quotes no prices.

## Capabilities

| Capability | What it gives you | Guide |
|---|---|---|
| GitHub sync | Your markdown publishes as a site; a push updates it | [Manage your docs](../getting-started/managing-docs.md) |
| Branding and themes | Your colours, logo, light/dark, navigation | [Branding](../../design/style/branding.md) |
| SEO / GEO / AEO | Meta tags, sitemap, OpenGraph, JSON-LD, canonical URLs, one indexed page set per language | [SEO](../../content/features/seo.md) |
| Full-text search | Keyword search over every published page | [Search](../../content/features/search.md) |
| Live auto translations | 15 languages, re-translated when you edit a page | [Translations](./translation.md) |
| Custom domain | `docs.yourcompany.com` with an automatic SSL certificate | [Custom domain](./custom-domain.md) |
| AI support assistant | An assistant that answers readers from your indexed pages | [AI chat](../../ai/chat.md) |
| Assistant configuration | Custom system prompt, chat hooks, chat analysis | [Chat hooks](../../ai/chat-hooks.md) |
| Analytics | Views, visitors, top pages, referrers, search queries, goals and funnels | [Analytics](../../analytics/README.md) |
| Privacy and access control | Switch a workspace to private behind a password or your own OIDC identity provider | [Private docs](./sso.md) |
| Semantic search | Every section embedded, so the assistant finds a passage by meaning | [AI chat](../../ai/chat.md) |
| Hosted API reference | Renders your OpenAPI spec as an interactive page | [Content widgets](../../content/features/widgets.md) |
| Bring your own AI key | Your provider bills you for usage directly; Docsbook bills you nothing for it | [AI chat](../../ai/chat.md) |
| Webhooks and feed notifiers | Discord and webhook notifications on documentation events | [Webhooks](../../webhooks.md) |

Migration onto Docsbook, full branding setup, agent configuration and Slack or pull-request integrations can be done for you rather than by you. What a subscription covers is listed on the [pricing page](https://docsbook.io/pricing).

## What spends money, and what does not

Each project carries its own balance. A new project starts with **$1.00** of it. Spending on one project never touches another.

Only work that calls an AI model is charged:

- Answers the reader-facing assistant writes
- Pages translated into another language
- Work you ask the admin assistant or the on-page editor to do
- Building the semantic index over your docs

Everything else — hosting, your custom domain and its SSL certificate, GitHub sync, keyword search, branding, navigation, widgets, feedback, event tracking and the analytics that read it — costs nothing from the balance, no matter how much traffic the site gets.

When the balance runs out, AI usage on that project stops until the balance is restored. There is no overage bill.

For how a single call is priced, and how to cap one source of spend so translations cannot absorb everything, see [How Docsbook charges for AI usage](../../content/setup/pricing-spec.md).

## How payment works

1. Open your workspace in the Float Widget.
2. Click **Upgrade**.
3. Paddle checkout opens inline, on the Docsbook domain.
4. Enter your card details and confirm.

Payments are processed by **Paddle**, the merchant of record. Docsbook never sees your card number; Paddle handles PCI compliance, EU VAT and US sales tax. Cancel at any time from the dashboard at [docsbook.io/chat](https://docsbook.io/chat).

Your markdown never leaves your GitHub repository, so cancelling costs you no content — there is nothing to export back out.

## Frequently asked questions

### How soon after paying can I use what I paid for?

Immediately, as soon as Paddle confirms the payment or the trial starts. There is no provisioning step.

### Is a subscription per project or per account?

A subscription is bought once per **account**, and your projects draw on it. Each project still keeps its own balance for AI usage, so the two questions — what your account pays for and what a given project has spent — stay separate.

### What happened to the old lifetime plan?

The one-time lifetime plan is no longer sold. Customers who bought it keep it.

### Where do I find the price?

At [docsbook.io/pricing](https://docsbook.io/pricing), which is regenerated on every request. Any price written into a documentation page — including this one — would be a copy that can go stale.

## Next steps

- [Set up a custom domain](./custom-domain.md) — serve the docs from `docs.yourcompany.com`.
- [Enable AI translations](./translation.md) — the capability that draws on the balance fastest.
- [Restrict who can read your docs](./sso.md) — password or your own identity provider.
- [How Docsbook charges for AI usage](../../content/setup/pricing-spec.md) — the metering in detail.
