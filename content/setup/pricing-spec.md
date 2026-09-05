---
title: "How Docsbook bills AI usage against a project balance"
description: "What a project balance is, which actions spend it, how a call is priced, and where to set a per-source ceiling so one job cannot absorb everything."
---

# How Docsbook charges for AI usage

Docsbook meters money, not features. Each **project** carries its own balance, every AI call is charged against that project's balance at what the call cost plus a markup, and the dashboard shows the model, its per-1M-token rate and the markup, so the amount deducted is one you can check.

Current prices are published at **[docsbook.io/pricing](https://docsbook.io/pricing)**. That page is generated from the live billing constants on every request, so it is the only place a price is guaranteed to be current — this page deliberately quotes none.

For the short version of the model, read [Docsbook pricing](../../pricing.md). This page is the operational detail: what a balance is, which action spends it, and where to put a ceiling on one source.

## What a project balance is

A project balance is a single pot of money attached to one documentation project, not to your account. Projects do not share a balance: spending on one never drains another. When a project's balance is exhausted, AI usage on that project stops until it is topped up; nothing is charged beyond what was already paid, and there is no overage bill.

[Docsbook pricing](../../pricing.md) covers the rest of that story — the credit a new project starts with, the welcome bonus, and the top-up limits. This page does not repeat it.

## Which actions spend the balance

Only work that calls an AI model costs money. Everything Docsbook does with your markdown is free of the balance.

| Spends the balance | Does not spend the balance |
|---|---|
| Answers the reader-facing AI assistant writes | Serving and reading your documentation site |
| Translating a page into another language | Hosting, your custom domain and its SSL certificate |
| Work you ask the admin AI agent or editor to do | Full-text keyword search |
| Building the semantic index over your docs | GitHub sync, the web editor, and the Edit on GitHub link |
| | Branding, navigation, widgets, feedback and event tracking |

The practical consequence: a documentation site with search, custom branding and a custom domain can run indefinitely without spending anything, and the cost starts the moment a model is asked to write or translate something.

## How a single call is priced

Usage is priced in money, not in tokens. Every call is charged at the real price the provider charges for the model that answered, plus a markup. The model that ran, its per-1M-token rate and the markup all appear in your dashboard beside the deduction.

You can choose which model runs. A cheaper model makes the same balance go further, and switching costs nothing.

You can also bring your own provider API key. The provider then bills you directly for usage and Docsbook bills you nothing for it.

## Cap one source of spend

From the **Usage** tab in workspace settings you can set an optional per-cycle ceiling on each individual spend source:

| Source | What it covers |
|---|---|
| Readers (AI Chat) | Answers written for visitors to your site |
| Admin & AI Agent | Work you ask the assistant to do on your docs |
| AI Translations | Pages translated into your enabled languages |
| Semantic Index | Embedding your pages so search matches by meaning |

A ceiling answers "AI translations must not run away with this project's balance." When a source reaches its ceiling it stops and the other sources keep running. A blank field means no ceiling; `$0` switches that source off entirely.

Each ceiling is drawn as a marker on the matching bar under **Spend by source**, so the balance and your own limit stay visible together.

## Billing and cancellation

Billing runs through **Paddle**, which acts as the merchant of record and handles card processing, EU VAT and US sales tax. Docsbook never sees your card number.

Manage or cancel from the dashboard at [docsbook.io/chat](https://docsbook.io/chat). Your markdown stays in your GitHub repository throughout, so leaving is an export rather than a migration.

Billing questions go to [support@docsbook.io](mailto:support@docsbook.io).

## Related

- [Docsbook pricing](../../pricing.md) — the model in one page, and the link to the live figures.
- [AI chat](../../ai-chat/chat.md) — the reader-facing assistant, the largest single consumer of a project balance.
- [Translations](../../translation/README.md) — how a page is queued, translated and re-translated.
- [AI usage analytics](../../analytics/tracking/ai-usage.md) — where the balance actually went.
