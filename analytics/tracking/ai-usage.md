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
| **Conversations** | Questions | Chat threads readers started, all of them |
| **Conversations** | Answered | Share of conversations where the model, reading the transcript, judges the reader actually got an answer to what they asked |
| **Conversations** | Savings | Estimated support cost avoided, based on answered conversations |
| **Conversations** | Cost | Total billed AI spend behind those conversations, shown as one line against Savings |
| **Dialogs** | Per-dialog cost | Shown next to each conversation's estimated savings right in the list; open one for the full cost/savings breakdown and its complete question-and-answer transcript |

The Chat page reports **everything** — every conversation still on record —
and has no interval control. The tiles and the conversation list under them
always describe the same set, so the two can never quote different numbers for
the same question.

**Answered is read, not inferred.** A separate model pass reads each
conversation's transcript and decides whether the reader came away with a real
answer or was left re-asking. Conversations are judged a handful at a time as
you open the page, so the figure fills in over a few visits rather than all at
once, and a conversation still waiting shows as unjudged rather than as
unanswered. Under five judged conversations the tile falls back to the older
signal-of-value reading (a citation click, a like, an outbound click) and says
so when you hover it. The answered/dead-end/unrated **outcome** split on
Analytics still uses that older reading throughout.

**Hover any tile to see the last 24 hours.** Each of the four carries the same
reading over the past day: Savings, Questions and Earned as their own figure,
Answered as a count ("2 of 3") rather than a percentage, because over a single
day a percentage swings by whole points per conversation. A quiet day shows
zeros and says so — that is a reading, not a gap.

Conversations are kept for **30 days**, which is how far back "everything"
goes. Asking the in-product assistant for the Conversations card by name still
gives you the card with its own 24h / 7d / 30d pills.

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
3. The four tiles across the top show the totals for everything on record —
   hover one for its last-24-hours figure. The conversation table directly
   under them is those same conversations, one per row, with its own search,
   filters and column picker on a single row above it. Open a row for that
   conversation's full transcript and its cost/savings breakdown
4. The table loads a page of conversations at a time rather than the whole
   history at once, so the page opens at the same speed whether the assistant
   has answered fifty questions or five hundred. Its footer says how many are
   on screen and how many there are in all; **Load more** fetches the next
   batch. Search and filters apply to what has been loaded, so on a long
   history load more if a filter looks emptier than you expect

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
