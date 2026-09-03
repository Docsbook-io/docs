---
title: "See what your AI chat was asked and what it cost you"
description: "Read the Chat page of your Docsbook workspace: how many readers asked, how many got a real answer, what the conversations were worth, and what they billed."
---

# AI Usage & Cost Statistics

The Chat page of a Docsbook workspace reports what your AI assistant was asked, how much of it it actually answered, what those readers were worth, and what running the assistant billed against the project's balance. Answering a reader is one of the few things that spends that balance; reading this page is not.

## What you will see

Usage and cost live inside the **Conversations** and **Dialogs** cards now, not a
separate "AI Usage" section — the numbers are more useful next to the
conversations that produced them:

| Card | Metric | Description |
|---|---|---|
| **Conversations** | Revenue | What the readers who used your chat are worth, counted once per reader on the same scale the Potential column and Goals & funnels use |
| **Conversations** | Cost | What running the chat actually billed over the same window, from the AI usage ledger. Shown in red, because it is the one figure here where money leaves |
| **Conversations** | Savings | Estimated support cost avoided, based on answered conversations. An estimate, unlike the two figures before it |
| **Conversations** | Questions | Chat threads readers started, all of them |
| **Conversations** | Answered | Share of conversations where the model, reading the transcript, judges the reader actually got an answer to what they asked |
| **Dialogs** | Per-conversation Potential and Cost | The two money columns lead the table, ahead of Time. Open a row for that conversation's full breakdown and its complete question-and-answer transcript |

**Revenue is two things added up, and the tooltip keeps them apart.** Part of it
is readers who actually reached the page you declared as your goal, valued at
what that goal declares or at your average product price. The rest is a fraction
of that price assigned to readers who only match part of a converter's path — a
forecast, not money received. Hover the tile to see the split. A reader who
opened four conversations counts once, so the figure cannot climb just because
somebody had to re-ask.

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

**Hover a tile to see the last 24 hours.** Savings and Questions carry the same
reading over the past day as their own figure, and Answered carries a count
("2 of 3") rather than a percentage, because over a single day a percentage
swings by whole points per conversation. A quiet day shows zeros and says so —
that is a reading, not a gap. Revenue and Cost have no separate day figure:
both are read over the window the page is showing, and a second reading would
mean asking for the whole window again.

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

## How to open the Chat page

1. Open your documentation site's admin
2. Click the **Chat** row in the sidebar — it opens into its own page, the same way **Settings** does
3. The five tiles across the top show the totals for everything on record,
   leading with what the chat brought in and what it cost — hover one for its
   last-24-hours figure where it has one. The conversation table directly
   under them is those same conversations, one per row, with its own search,
   filters and column picker on a single row above it. Open a row for that
   conversation's full transcript and its cost/savings breakdown
4. The table loads a page of conversations at a time rather than the whole
   history at once, so the page opens at the same speed whether the assistant
   has answered fifty questions or five hundred. Its footer says how many are
   on screen and how many there are in all; **Load more** fetches the next
   batch. Search and filters apply to what has been loaded, so on a long
   history load more if a filter looks emptier than you expect

## How the cost of an AI request is estimated

Docsbook estimates the cost of an AI request from three things:

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

## What spends the balance, and what does not

AI usage is metered in money, not in requests: every project carries its own balance, and each call takes what that call was priced at. Choosing a cheaper model therefore makes the same balance go further, which is why the model picker exists.

| Spends the project balance | Costs nothing |
|---|---|
| An AI answer given to a reader in chat | Reading any analytics report |
| A question you ask the assistant in the panel | Hosting and serving your documentation |
| Translating a page | Serving an already-translated page |
| Building the semantic index and its embeddings | Branding, theming and navigation settings |
| A background agent run | Registering a webhook and receiving its deliveries |

When a project's balance runs out, AI usage pauses rather than overrunning: the assistant stops answering until the balance is topped up, and nothing else about the site changes. Current rates are published on the [Docsbook pricing page](https://docsbook.io/pricing.md).

Calls made on your own provider API key are counted here and billed by that provider instead, so they cost the project balance nothing.

## Cost breakdown by model

The cost breakdown table shows your spending by AI provider and model:

- **Provider**: Which AI service (OpenAI, Anthropic, Gemini, etc.)
- **Model**: The specific model used (e.g., `gpt-4o-mini`)
- **Count**: Number of requests using this model
- **Estimated Cost**: Total cost for requests using this model

The models are sorted by total cost, so you can quickly see which models are driving your AI expenses.

## Custom API keys

If you have set your own API keys for OpenAI, Anthropic, or Gemini, the costs of a call made on them are:

- **Calculated by the provider** (not estimated by Docsbook)
- **Visible in your provider's billing dashboard** (OpenAI Platform, Anthropic Console, Google Cloud)
- **Not deducted from the project balance** (you manage those costs with your provider)

Learn more: [AI chat](../../ai/chat.md) — choosing a provider and a model

## Time ranges

Ask the in-product assistant for the Conversations card by name and it comes with its own **24h**, **7d** and **30d** pills. Thirty days is the longest window: conversations are kept for 30 days, and the AI ledger is pruned to match, so there is nothing older to report.

## Related

- [Analytics overview](./overview.md) — the Spend figure and the two chat cards at the bottom of that page
- [Tracked events reference](./events.md) — the chat events behind these totals
- [AI chat](../../ai/chat.md) — configuring the assistant these numbers describe
- [How AI translations work](../../translation/ai-translations.md) — the other thing that spends the same balance
