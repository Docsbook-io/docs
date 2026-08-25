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
| **Conversations** | Questions | Chat threads readers started in the selected window |
| **Conversations** | Answered | Share of conversations that showed a sign of value (a citation click, a like, an outbound click) |
| **Conversations** | Savings | Estimated support cost avoided, based on answered conversations |
| **Conversations** | Cost | Total billed AI spend for the window, shown as one line against Savings |
| **Conversations** | Outcome | Breakdown of answered, dead-end, and unrated conversations — open any group straight into **Dialogs** |
| **Dialogs** | Per-dialog cost | Shown next to each conversation's estimated savings right in the list; open one for the full cost/savings breakdown and its complete question-and-answer transcript |

Cost breakdown by provider/model, monthly limits, translation usage, and time
ranges are unchanged — see the sections below.

## How to Open

1. Open your documentation site's admin
2. Click the **Chat** row in the sidebar — it opens into its own page, the same way **Settings** does
3. The **Conversations** card shows the totals; scroll down to **Dialogs** to browse
   individual conversations and their cost. **Dialogs** loads older conversations
   automatically as you scroll — there's no separate time range or filters to set
   there, since **Conversations** already covers both for the whole page

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
