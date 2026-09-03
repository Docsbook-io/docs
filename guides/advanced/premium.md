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

Migration onto Docsbook, full branding setup, agent configuration and Slack or pull-request integrations can be done for you rather than by you. Those are done-for-you services rather than capabilities you switch on; the [pricing page](https://docsbook.io/pricing) says which are included.

## What any of this costs

Only work that calls an AI model costs money: answers the reader-facing assistant writes, pages translated into another language, work you ask the admin assistant or the on-page editor to do, and building the semantic index. Every capability in the table above is available to every project; none of them is withheld until you pay.

Everything else in that table — hosting, the custom domain and its SSL certificate, GitHub sync, keyword search, branding, navigation, widgets, feedback and analytics — costs nothing from the balance, however much traffic the site gets.

Two pages carry the detail, and this one deliberately repeats neither:

- [Docsbook pricing](../../pricing.md) — what a project balance is, the free credit a new project starts with, and how top-ups work.
- [How Docsbook charges for AI usage](../../content/setup/pricing-spec.md) — how a single call is priced, how to cap one source of spend, and how billing and cancellation work.

Current prices are published at [docsbook.io/pricing](https://docsbook.io/pricing), regenerated on every request. A price written into a documentation page is a copy that goes stale silently, so none appears here.

## Next steps

- [Set up a custom domain](./custom-domain.md) — serve the docs from `docs.yourcompany.com`.
- [Enable AI translations](./translation.md) — the capability that draws on the balance fastest.
- [Restrict who can read your docs](./sso.md) — password or your own identity provider.
- [How Docsbook charges for AI usage](../../content/setup/pricing-spec.md) — the metering in detail.
