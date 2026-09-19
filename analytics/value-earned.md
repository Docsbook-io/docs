---
title: "What your documentation earned"
description: "Docsbook values the outcomes your docs produce — an AI-referred reader is worth more than a search click, and a citation is worth more than either — and sets the total against what your agents cost. Attributed value, not revenue."
---

# What your documentation earned

Every other number in Docsbook tells you how much of something happened. This one tells you **what it was worth** — and puts it next to what the work cost, so the two can be read in one glance.

## Why a visit is not a visit

A documentation site gets readers from very different places, and treating them as one number hides the only thing worth knowing.

Somebody who clicked a Google result is usually already your user, looking up a flag. Somebody an AI assistant sent is in the middle of deciding: they asked a question, and the engine picked your docs as the answer. And being **named in the answer itself** is different again — that is not one reader, it is a standing recommendation served to everyone who asks that question, whether or not any of them click.

So Docsbook values them differently:

| Outcome | Roughly worth |
|---|---|
| A visit from classic search | the baseline |
| A visit an AI assistant sent | many times the baseline |
| A citation — an engine naming your docs in its answer | more than either |
| A reader clicking through to your product | the most of all |
| An answer your on-site AI assistant gave | a deflected support conversation |

The exact rates are published with the figures on [docsbook.io/pricing](https://docsbook.io/pricing) and returned alongside every total in the API, so you can always see the arithmetic rather than being handed a number.

## What is deliberately worth nothing

- **A click you paid for.** Its worth is already on your ad invoice. Counting it here would let a project raise its "earned" figure by spending money, which would make the number useless for the one thing it is for.
- **Your own navigation, your own tooling, and SEO crawlers** you do not serve.
- **A search that found nothing.** Zero, never negative: a gap in your docs is a real finding, and the total should not fall when Docsbook learns something true about your site.

**Crawlers are not zero.** An AI crawler reading your pages is worth a little — it is how a citation becomes possible later. It is not worth what a reader is worth, and Docsbook does not pretend otherwise.

## If you have declared what a conversion is worth

If you have set a value on a goal, **your figure wins** for that outcome. You know what a signup is worth to you; Docsbook does not, and counting both would double every conversion on your site.

Setting it to zero counts as an answer, not as leaving it blank.

## Against what it cost

The same view shows what your agent runs cost over the window — runs, how many were included in your plan, and what actually left a balance — and the two together:

- **Net** — value produced minus what it cost.
- **Ratio** — how many times over the work paid for itself. When you have spent nothing yet, there is no ratio, and Docsbook says so instead of printing an infinity.

## Read this number honestly

🔴 **This is attributed value, not revenue.** It is what the outcomes your documentation produced are worth at Docsbook's published rates. It is not money that arrived, it is not a forecast, and it does not belong in a row next to your actual receipts.

What it is good for is comparison: this month against last, this channel against that one, and the work against its cost. Those are the questions it answers honestly, and they are the reason it exists.

## Where to find it

- **In your panel** — alongside spend on the project's analytics.
- **Over the API** — `GET /api/analytics/value?workspaceId=<id>&days=<n>`, which returns the counts, the rate card and the comparison together.

If part of it cannot be read — the event warehouse is unreachable, or citations have never been configured — the response **names the missing part** rather than quietly returning a smaller number.

## Related

- [Docsbook pricing](../pricing.md) — what costs money, including what an agent run costs and who pays for it
- [AI usage and costs](./tracking/ai-usage.md) — where spend shows up in your analytics
- [How measurement works](./how-measurement-works.md) — how Docsbook decides who a reader is and where they came from
