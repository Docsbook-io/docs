---
title: "What your AI actually cost, and what it was spent on"
description: "How Docsbook meters AI work: what is billed, how a call is priced, how it is attributed to a project balance, and what breakdowns the owner can read per model, route and tool."
tldr: "Every AI call and every metered MCP tool call writes a ledger row against one project's balance. Cost is the provider's own reported figure where the provider reports one, and a per-model rate card otherwise — never an estimate from character counts. Money is stored in millicents so sub-cent calls are not rounded to nothing, and what leaves the wallet is whole cents with the remainder carried."
---

# AI usage and cost

Metered AI is the one part of a documentation product where a wrong number
costs the owner real money. This page is the mechanism: what is metered, how a
call is priced, which balance it comes out of, what you can see afterwards, and
where the figures on two different screens can legitimately differ.

## What you get

Every AI call your project makes — a reader's question, your own question in
the panel, a translation, an embedding run, an agent step — writes a row
naming the surface that spent it, the model that ran, the tokens in and out,
what the provider charged, and what left your balance. Every metered MCP tool
call writes its own row naming the tool and its billing class.

From those rows you can read spend **by model**, **by surface**, **by budget
category**, **by conversation**, **by translated language and page**, and **by
MCP tool** — plus a per-day series for each. The headline **Spend** tile on the
[analytics overview](./overview.md) is the same two ledgers summed.

Reading any of this is free. Answering a reader is not.

## What spends the balance, and what does not

Usage is metered in **money, not requests**: each call takes what that call was
priced at, so choosing a cheaper model makes the same balance go further. That
is what the model picker is for, and it is available on every plan.

| Spends the project balance | Costs nothing |
|---|---|
| An AI answer given to a reader in chat | Reading any analytics report |
| A question you ask the assistant in the panel | Hosting and serving your documentation |
| Follow-up suggestions and conversation titles | Serving an already-translated page |
| Translating a page | Branding, theming, navigation, SEO settings |
| Building the semantic index and its embeddings | Registering a webhook and receiving deliveries |
| A background agent run | MCP discovery calls — finding out what the server can do |
| A metered MCP tool call | Reader events on your docs site |

**Reader events are priced but never charged.** The Usage view puts a figure
next to each event class so you can see what your traffic implies, and nothing
deducts it from anything. Billed money and metered-only money are kept in
separate totals precisely so one screen can never present the second as an
invoice.

**Calls on your own provider key are metered but not billed.** The row is still
written — with the provider's real cost, your model, your token counts — and
priced at **zero rather than dropped**, because a model missing from the
breakdown just for being on your key reads as "we never called it". Those calls
are also counted separately, so a `$0` next to real volume is explained rather
than left looking broken. Bringing your own key does not change what your plan
includes.

## How it is built

### Two charged ledgers, deliberately not one table

| Ledger | One row per | Key fields |
|---|---|---|
| Token bill | LLM call | surface (`ai-chat`, `agent-chat`, `translate`, `embed`, `followups`, `title`, `other`), budget category (`users`, `admin`, `translations`, `embeddings`), model, prompt/completion/total tokens, provider cost, markup frozen at call time, duration, conversation id, own-key flag, estimated-price flag; translations add the language, the page, and how many chunks were re-translated versus reused |
| MCP call bill | tool call | tool name, billing class frozen at call time, list price, duration, whether the call succeeded, the background run that executed it |

They are separate tables because an MCP call has no token bill — it has a name,
a class and a fixed list price — and because a large share of MCP calls
(discovery, listing your projects) belong to no project at all. Writing those
against an arbitrary project would be an invented attribution the usage chart
would then present as fact.

### How a call is priced

1. **The provider's own reported cost wins.** Where the provider returns what
   the call cost, that figure is used verbatim and the row is *not* marked
   estimated. It is authoritative in a way a local calculation cannot be,
   because it already accounts for prompt-cache discounts and mid-flight price
   changes.
2. **Otherwise, the model's catalogue rate.** Real prompt and completion token
   counts from the response, multiplied by that model's input and output rate
   per million tokens. Twelve chat models are in the catalogue with their own
   rates, plus a separate embedding catalogue.
3. **An unrecognised model falls to a deliberately pessimistic fallback rate**
   and the row is flagged `estimated`, so every surface can label it as a guess
   instead of presenting it as fact. Model lookup is exact-match only, never
   fuzzy: substring matching once priced a `-mini` model as its full-size
   namesake.

A markup is then applied and **frozen onto the row**, so historical rows stay
honest if the rate ever changes.

> Token counts come from the model API's own usage report. Docsbook does not
> approximate them from text length.

### Millicents, and the rounding that matters

The provider's cost is stored in **millicents** — a thousandth of a cent —
because a single cheap answer costs a small fraction of a cent and whole cents
would round almost every row to zero, making the breakdown chart lie.

What leaves the wallet is whole cents. The deduction **floors** to whole cents
and **carries the remainder** on the project, so a hundred sub-cent answers
eventually spend a cent rather than being either forgiven or over-charged.
Money is spent in one order: trial credit first, then the monthly allowance,
then any one-time balance.

**A consequence you can see on screen.** The column recording what actually
left the wallet on *that* call is `0` on nearly every row, because sub-cent
calls only move the carry. Newer surfaces — the Spend tile and the Usage view —
therefore rebuild each row's list price from the provider cost and the frozen
markup instead of summing that column, while two older screens still sum it.
Where those two disagree, the rebuilt figure is the more honest one.

### What happens when the balance runs out

Docsbook is pay-as-you-go. The balance does not refill on its own, and nothing
about your site changes when it empties — only AI work stops, and it stops in
the place that can explain itself:

| Surface | What happens |
|---|---|
| Reader chat | The request is refused before the model runs, with a reason code rather than a broken answer |
| Admin agent loop | Checked before the loop *and before every iteration*, so one long turn cannot burn the remainder mid-flight |
| Agent runs | The run is recorded as failed with a human sentence — the balance ran out, top it up and it runs again on its next trigger |
| Batch translation | The job halts and says so; remaining pages are untranslated, not silently skipped |
| Semantic index | Refused before the job row is even opened |
| MCP tools | A structured refusal naming the tool, its billing class, the project, the price per call, the balance remaining and a top-up link. Discovery tools keep working |

Because these are checks rather than reservations, a wallet can go **at most
one call past empty**; the next one fails closed.

**Overage** is an alternative to a hard stop, and it is opt-in and paid-plan
only. It is capped, billed on a fixed interval, and warns you on the way up at
75%, 85%, 90%, 95% and 100% of your cap through the
[usage webhooks](../../reference/webhooks.md). Translations and the semantic
index deliberately never draw on it: an index run is a large, deliberate,
cancellable action, and quietly turning one into an overage bill would be
hostile.

### The Chat page

The Chat page reports what your assistant was asked and what answering cost, on
one set of conversations with no interval control — so the tiles and the list
under them can never describe different sets.

| Tile | What it is |
|---|---|
| Revenue | What the readers who used the chat are worth, counted once per reader, on the same scale Goals and the Potential column use |
| Cost | What running the chat billed over the same window, from the usage ledger |
| Savings | Support cost avoided, from answered conversations — an **estimate**, at a single industry-default ticket rate, not your measured cost |
| Questions | Chat threads readers started |
| Answered | The share of conversations where a model, reading the transcript back, judges the reader actually got an answer |

**Answered is read, not inferred.** The older signal — a citation click, a
like, an outbound click — is a proxy that is wrong in both directions: a reader
who got a perfect answer and clicked nothing scores as unrated, and a reader
who clicked a cited page without reading it scores as answered. A separate
model pass reads each transcript instead. Verdicts are written once and reused,
and only a handful of new conversations are judged per page load, so the figure
fills in over a few visits rather than making the first one time out. Under
five judged conversations the tile falls back to the older reading and says so.
A conversation still waiting shows as unjudged, never as unanswered.

Hovering a tile gives its last-24-hours figure where it has one; Answered shows
a count ("2 of 3") rather than a percentage, because over a single day a
percentage swings by whole points per conversation. Revenue and Cost have no
separate day figure — both are read over the window already on screen.

## Why this is the right way

| Rule | Why it works | Source |
|---|---|---|
| Take the provider's reported cost over a locally derived one | OpenRouter returns the cost field as "The total amount charged to your account", alongside `cost_details.upstream_inference_cost` — "The actual cost charged by the upstream AI provider". A local re-derivation cannot know either | [OpenRouter: usage accounting](https://openrouter.ai/docs/use-cases/usage-accounting) |
| A price re-derived from token counts is wrong whenever caching applies | OpenAI bills reused prompt tokens at "the model's reduced cached-input rate for reused tokens, discounted up to 90%", reported separately in the response's usage details | [OpenAI: prompt caching](https://developers.openai.com/api/docs/guides/prompt-caching) |
| Meter tool calls per call, and record failures too | The MCP specification puts rate limiting on the server — servers "MUST … Rate limit tool invocations" — and asks clients to "Log tool usage for audit purposes". A ledger that only recorded successes would be neither | [MCP specification: tools](https://modelcontextprotocol.io/specification/2025-06-18/server/tools) |
| Store sub-cent amounts at sub-cent precision | Every honest per-call figure here is a fraction of a cent; rounding on the way in is how a real day of spend becomes `$0` | Mechanism, this page |

## Limits and open questions

- **You cannot break spend down by provider.** The ledger records the model,
  not the vendor behind it, so a "how much went to Anthropic" question has no
  answer in the product today.
- **You cannot yet see spend per agent run in the token ledger.** MCP rows
  carry the run that executed them; token rows carry only a free-form
  conversation id, so an agent's model bill is grouped by conversation rather
  than by run.
- **Rows flagged `estimated` are guesses, and the fallback rate is
  deliberately high.** A model outside the catalogue is priced pessimistically
  on purpose — under-charging a customer for a model nobody priced is the worse
  error — so an estimated row is an upper bound, not a measurement.
- **Two older screens still sum the deducted-cents column** and therefore
  under-report projects whose calls are mostly sub-cent. The Spend tile and the
  Usage view rebuild list price instead. If two spend figures disagree, that is
  the reason.
- **Savings is an estimate and is labelled as one.** It multiplies answered
  conversations by an industry-default support ticket cost. It is not your
  support cost, and Docsbook has not measured yours.
- **Own-key spend is invisible as money.** Those calls show volume, model mix
  and token counts, and `$0`. What they actually cost you is on your provider's
  bill.
- **The reports and the retention window are not the same length.** The panel
  never shows more than 30 days of usage, matching where reader analytics ends.
  The AI ledger itself is kept for **90 days** — the extra margin exists so a
  disputed bill can still be reconstructed — and is pruned daily. MCP call rows
  are currently not pruned at all, which is why the per-tool view is all-time.
- **Under question: "Savings" and "Revenue" are models, "Cost" is a
  measurement.** What is verifiable is the ledger: which model ran, what the
  provider charged, what left the balance. What is not verifiable from this
  data is whether an answered question would otherwise have become a support
  ticket, or whether a reader who used the chat would otherwise not have
  bought. Read the two money-in figures as rankings between readers, never as
  cash.

## Which plan

The reader-facing assistant, agent runs and automatic translations are the
capabilities that spend money on Docsbook's provider key, and they are the
paid ones. Everything else on this page — the ledgers, the breakdowns, the
model picker, bringing your own key, MCP — is available on every plan, and MCP
in particular has no plan gate at all: money is the only limit. Current plans
and rates are on the [pricing page](https://docsbook.io/pricing).

## Where to look

1. **Spend over time, next to your traffic** — the Spend tile on the
   [analytics overview](./overview.md).
2. **What the money went on** — the Usage view: AI by surface, category and
   model; MCP by tool and class; events priced but not charged. Windows are
   24 hours, 7 days and 30 days.
3. **What your chat was asked and what it cost** — the **Chat** row in the
   admin sidebar; open a conversation for its transcript and its own
   cost breakdown.
4. **From an agent** — `get_ai_usage` over
   [MCP](../../reference/mcp-tools.md).

## Related

- [Analytics overview](./overview.md) — the Spend tile and how it behaves under filters
- [How measurement works](../how-measurement-works.md) — retention and where the data lives
- [Tracked events](./events.md) — the chat events behind these conversations
- [AI chat](../../ai-chat/chat.md) — choosing a model and a provider
- [How AI translations work](../../translation/ai-translations.md) — the other thing that spends this balance
- [Webhooks](../../reference/webhooks.md) — being told you are approaching a limit instead of finding out
