---
title: "AI Usage & Cost Statistics"
description: "Monitor your AI chat requests, translation usage, and estimated costs per model. Track spending across different AI providers and models."
---

# AI Usage & Cost Statistics

Monitor how your AI features are being used and estimate the costs associated with each AI request.

## What You'll See

Usage and cost live inside the **Conversations** and **Dialogs** cards now, not a
separate "AI Usage" section — the numbers are more useful next to the
conversations that produced them:

| Card | Metric | Description |
|---|---|---|
| **Conversations** | Questions | Chat threads readers started in the last 24 hours |
| **Conversations** | Answered | Share of conversations that showed a sign of value (a citation click, a like, an outbound click) |
| **Conversations** | Savings | Estimated support cost avoided, based on answered conversations |
| **Conversations** | Cost | Total billed AI spend over the same 24 hours, shown as one line against Savings |
| **Dialogs** | Per-dialog cost | Shown next to each conversation's estimated savings right in the list; open one for the full cost/savings breakdown and its complete question-and-answer transcript |

The Chat page reports **the last 24 hours** and has no interval control. It
answers "what did the assistant do today", and the tiles and the conversation
list under them always describe the same window, so the two can never quote
different numbers for the same question. Longer-range chat reading lives on the
**Analytics** page, which has its own date-range picker (see below). Asking the
in-product assistant for the Conversations card by name still gives you the
card with its own 24h / 7d / 30d pills.

Cost breakdown by provider/model, monthly limits, translation usage, and time
ranges are unchanged — see the sections below.

The fuller breakdown of your chat traffic — topics, why readers came, top
searches, languages, outbound links, and the answered/dead-end/unrated
outcome split — no longer lives on this page. It now sits at the bottom of
the **Analytics** page, as two cards ("What readers asked" and "Where the
answers led"), reading Analytics' own date-range picker instead of a second
period control here. Clicking a row there no longer opens it into
**Dialogs** — that jump only works from within the Chat page itself.

## How to Open

1. Open your documentation site's admin
2. Click the **Chat** row in the sidebar — it opens into its own page, the same way **Settings** does
3. The four tiles across the top show the totals for the last 24 hours; the
   conversation table directly under them is every one of those conversations,
   one per row, with its own search, filters and column picker on a single row
   above it. Open a row for that conversation's full transcript and its
   cost/savings breakdown

## Cost Estimation

Docsbook estimates costs based on:

- **Token counts**: Approximated from text length (~4 characters per token)
- **Model pricing**: Current market rates for popular models (OpenAI, Anthropic, Gemini, etc.)
- **Per-request breakdown**: Input tokens (question) × input price + output tokens (answer) × output price

Supported pricing models:

| Provider | Models |
|---|---|
| **OpenAI** | GPT-4, GPT-4o, GPT-4o mini, GPT-3.5 Turbo |
| **Anthropic** | Claude 3 Opus, Sonnet, Haiku |
| **Google** | Gemini Pro, Gemini Pro Vision |
| **Others** | OpenRouter and custom models (default rates) |

> **Note**: Estimated costs are approximate and may differ from actual provider invoices due to token counting differences, special pricing, and volume discounts.

## Monthly Limits

AI usage is metered in money, not in requests. Each paid plan includes a monthly AI budget:

| Plan | Monthly AI budget |
|---|---|
| **Free** | $0.15 |
| **Pro** | $85.00 |
| **Business** | $200.00 |

Every call is charged at the model provider's real price plus a 150% markup, so a cheaper model stretches the same budget further.

When a plan exceeds its monthly budget, AI usage simply pauses until the next billing cycle — see [Pricing & Plans](../../content/setup/pricing-spec.md#usage-budget) for details. You're never billed above your plan's price.

## Translation Usage

Translation requests use a separate monthly quota:

| Plan | Translations/Month |
|---|---|
| **Free** | 0 translations |
| **PRO** | 50 translations |
| **PRO+** | 500 translations |

Learn more: [AI Translations](../../ai/translations.md)

## Cost Breakdown by Model

The cost breakdown table shows your spending by AI provider and model:

- **Provider**: Which AI service (OpenAI, Anthropic, Gemini, etc.)
- **Model**: The specific model used (e.g., `gpt-4o-mini`)
- **Count**: Number of requests using this model
- **Estimated Cost**: Total cost for requests using this model

The models are sorted by total cost, so you can quickly see which models are driving your AI expenses.

## Custom API Keys

If you've set your own API keys for OpenAI, Anthropic, or Gemini, the costs are:

- **Calculated by the provider** (not estimated by Docsbook)
- **Visible in your provider's billing dashboard** (OpenAI Platform, Anthropic Console, Google Cloud)
- **Not included in Docsbook usage limits** (you manage costs separately)

Learn more: [Using Your Own API Keys](../../ai/chat.md#custom-api-keys)

## Time Ranges

AI usage metrics are available for:

| Range | Plan required |
|---|---|
| Last 24 hours | Free |
| Last 7 days | Pro |
| Last 30 days | Business |

> **Start using AI chat today.**
> [Create a documentation site →](https://docsbook.io/connect)
