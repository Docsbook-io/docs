---
title: "Search data: where it comes from"
description: "Docsbook reads Google Search Console for your docs with nothing to connect: which sites it covers, what syncs, how fresh it is, and how the agent uses it."
status: generated
version: "0.2"
---

# Search data: where it comes from

Docsbook reads Google Search Console for you, with no Google account to connect, and shows each query's clicks, views, CTR and position in **Analytics ▸ Insights**. The **Keywords** card breaks traffic down by search query.

## Which sites does it cover?

Docsbook reads a Search Console **domain property** for `docsbook.io`, which covers every subdomain, and keeps the rows whose URLs belong to your site.

| Where your site is served | Search Console data |
|---|---|
| `<owner>.docsbook.io/<repo>`, built from your GitHub repository | Read automatically |
| Its own `<name>.docsbook.io` address, hosted by Docsbook or set in **Settings ▸ General ▸ Site source** | Not read yet |
| Your [custom domain](../site/custom-domain.md), such as `docs.example.com` | Outside Docsbook's property |

For a custom domain, verify the domain in your own Search Console account to see its numbers there.

## What syncs, and how often?

Docsbook asks Google for two views of the same traffic and keeps both.

- **Queries** — each query Google names for your pages, per day and per page, with clicks, impressions and average position
- **Page totals** — the same numbers per page, including traffic behind queries Google withholds for privacy
- **30 days** — how much history is kept
- **About two days behind** — Google's own lag; a "data through" date shows how fresh the numbers are
- **Once a day at most** — a pull happens when the agent needs rankings, or when you press **Refresh** on the **Search rankings** card in the panel chat

Access is read-only. Docsbook never submits URLs, requests indexing or changes anything in Search Console.

## How to find the pages closest to page one

<!-- widget:stepper -->

### Open Analytics ▸ Insights

The page opens showing your top metrics.

### Go to the Keywords card

It lists each search query with clicks, impressions, CTR and average position.

### Sort by position, best first

Read down to the rows between `#5` and `#20` with many impressions. Google already shows these pages; a better title or first screen is what wins the click.

<!-- /widget -->

## What does the agent do with it?

The [Docsbook agent](../agent/README.md) uses the same rows to choose search changes and to judge them:

- **Picks the pages worth fixing** — queries at positions 5–20, already visible and not yet winning the click
- **Forecasts in clicks** — for a title, snippet, intent or first-screen change, it compares the page's CTR with what your other pages earn at that position and forecasts 25–50% of the gap, labelled an estimate
- **Learns from your site** — once five of your own changes have been measured, that band is replaced by what they actually achieved
- **Refuses to guess** — under 30 impressions in 28 days a page gets no forecast, never a zero
- **Judges the change** — Google's position, impressions and clicks for the page, before against after, with the day of the change left out
- **Explains drops** — the **Explain a traffic drop** [trigger](../agent/triggers.md) names the pages and sources that lost readers

## FAQ

<!-- widget:accordion -->

### Do I need to verify my site in Google Search Console?

No, for a site served at `<owner>.docsbook.io/<repo>`: Docsbook's own property already covers it. A custom domain needs verifying in your own account.

### Why are these numbers lower than Search Console's own totals?

Google leaves rare queries out of its query report for privacy, and the **Queries** and **Pages** views are built from the queries Google names. The agent's forecasts and before-and-after checks use the page-level totals, which include that traffic.

### Why don't I see yesterday's searches?

Google publishes Search Console data about two days late. The newest day shown is the one Google has closed.

<!-- /widget -->

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->
- [Search engines see you](./README.md) — Everything Docsbook does for SEO, and the agent's search loops {search}
- [Track AI citations](../geo/ai-visibility.md) — The same view for ChatGPT, Perplexity and Google's AI Overview {sparkles}

<!-- /widget -->
