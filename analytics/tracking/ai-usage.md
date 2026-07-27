---
title: "AI Usage & Cost Statistics"
description: "Monitor your AI chat requests, translation usage, and estimated costs per model. Track spending across different AI providers and models."
---

# AI Usage & Cost Statistics

Monitor how your AI features are being used and estimate the costs associated with each AI request.

## What You'll See

The AI Usage panel displays:

| Metric | Description |
|---|---|
| **AI Requests** | Total number of AI chat questions asked by readers |
| **Monthly Limit** | Maximum requests allowed on your current plan |
| **Daily Trend** | Graph showing request volume over time |
| **Cost Breakdown** | Estimated costs per AI provider and model used |
| **Total Cost** | Cumulative estimated cost for all AI requests |
| **Translation Usage** | Number of document translations completed |

## How to Open

1. Open any page of your documentation site
2. Click the **Analytics** tab in the floating toolbar at the bottom
3. Select the **AI Usage** section to view your AI metrics

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

AI usage is metered in money, not in requests. Each plan includes a monthly AI budget:

| Plan | Monthly AI budget |
|---|---|
| **Free** | $0.15 |
| **Pro** | $15.00 |
| **Business** | $45.00 |
| **Growth** | $84.00 |
| **Scale** | $225.00 |

Every call is charged at the model provider's real price plus a 20% markup, so a cheaper model stretches the same budget further.

When a paid plan exceeds its monthly budget, additional usage is billed as overage up to a monthly cap you set in the Limits tab of workspace settings (default $20/month) — see [Pricing & Plans](../../content/setup/pricing-spec.md#overage-billing) for how the cap works. The Free plan has no overage and stops at its budget.

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
| Last 30 days | Growth / Business / Scale |

> **Start using AI chat today.**
> [Create a documentation site →](https://docsbook.io/connect)
