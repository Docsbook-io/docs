---
title: "Docs analytics: traffic, AI visitors and revenue per page"
description: "See docs traffic, sources, countries and AI-assistant visitors in Docsbook, and turn a call-to-action URL and an average price into revenue per visitor."
---

# See who reads your docs and what they are worth

**Analytics ▸ Insights** shows who reads your documentation, where they came from and what they did — and, once you name the page that sells, what those readers were worth.

## What does the Insights tab show?

A row of figures sits over one chart that draws the figure you select. Above them are the **online** count (readers active in the last 5 minutes), the range switcher and **Open Live Map**.

| Figure | What it counts |
|---|---|
| **Visitors** | People who read the docs in the window, split into new and returning |
| **Revenue** | Conversions × your average product price |
| **Conversion rate** | Visitors who clicked through to your Call To Action URL ÷ visitors |
| **Revenue/visitor** | Revenue ÷ visitors |
| **Bounce rate** | Visits of one page, under 3 seconds, with nothing else |
| **Questions** | Questions readers asked the [AI chat](../ai-chat/README.md) |
| **Session time** | The average length of a visit |

The range runs from **Now** (a live, rolling hour) through **Today**, **Yesterday**, **Last 24 hours** and **Last 7 days** to **Last 30 days**. Today and Yesterday are UTC days.

Four cards under the chart break the same visits down:

- **Pages** — Pages, **Headings** (how far down a page readers scrolled), Entry and Exit; rank them by Visitors, Revenue, Views or Reading time
- **Sources** — Referrers, **Keyword** (what people typed into Google, from [Search Console](../seo/search-console.md)), Channels and UTM
- **Audience** — Devices, Browsers, Countries and Languages
- **Conversions** — **CTA Clicks** (readers who left the docs for pricing, sign-up or your app) and **Feedback** (votes per page)

**Filter by** any row to narrow the figures, the chart and all four cards to that page, country or source.

## How do I tell AI traffic from people?

Every figure on Insights counts people: crawlers are left out, and so are your own visits from the panel.

- **Sources ▸ Channels** gives people who clicked through from an answer in ChatGPT, Perplexity, Claude, Copilot or Gemini their own **AI assistant** channel, apart from Organic search, Social, Referral and Direct
- **Analytics ▸ GEO** lists the crawlers themselves — which assistant fetched which page, for live answers, indexing or training; see [AI visibility](../geo/ai-visibility.md)
- **Analytics ▸ Graph** colours a map of your docs by **AI Answers** (visits that arrived via an AI assistant) or **Training** (hits from AI training crawlers)

## How do I see revenue from my docs?

Name the page that sells and what a sale is worth, and **Conversion rate**, **Revenue** and **Revenue/visitor** switch on.

<!-- widget:stepper -->

### Set a Call To Action URL

Open **Settings ▸ General** and fill in **Call To Action URL**: your pricing, signup or demo page. A reader who clicks out of the docs to that host is a conversion, and **Conversion rate** appears.

### Set an Average Product Price

On the same tab, fill in **Average Product Price** — what one conversion is worth to you. **Revenue** and **Revenue/visitor** appear, and rows in the cards can be ranked by Revenue.

### Read the result

Back on **Analytics ▸ Insights**, Revenue is conversions × price and Revenue/visitor is revenue ÷ visitors. Filter by a page or a source to see what its readers were worth.

<!-- /widget -->

Until both are set, Revenue and Revenue/visitor show a dash and **Set up →**, never `$0`. From an MCP client, `update_branding` sets both (`cta_url`, `average_product_price_cents`).

## Follow one reader

**Activity ▸ Users** lists every reader as one row: a pseudonym, their country, the translation they read, where they came from, when they reached a [goal](./goals.md), and **Potential**.

- **Potential** — what a reader is worth on one scale: full value once they reached your Call To Action URL, and a share of it for everyone else, by how closely they follow a converter's path; it ranks readers and is not a revenue forecast
- **Filters** — **Close to converting**, **Came back** and **Reached no goal** find who to look at next
- **Open a row** to see everything that reader did, in order; **Improve** asks the agent where the docs are failing them

**Open Live Map** on Insights shows readers live on a world map: the page each one is on, how long they have been on the docs, and what they just did.

## What the agent reads from here

The [Docsbook agent](../agent/README.md) reads the same numbers when it works on your docs, and every screen can hand them to it:

- **Evidence** — visits, how they ended (success, dead end, bounce), the pages readers gave up on, and the routes they took
- **Improve on a row** — a page, a country, a source, a goal or a reader goes to the agent in the panel chat, numbers attached
- **Graph actions** — select a page on **Analytics ▸ Graph** for fixes such as **Get this page linked**, **Improve search ranking** or **Verify against code**
- **Dollar forecasts** — with both revenue settings set and Search Console data for the page, the agent's recommendations carry a monthly dollar estimate beside the extra clicks they expect; without the settings it never guesses a dollar figure

## FAQ

**Are visitor counts exact?** No. A reader is a salted hash of their IP address, so an office network can merge several people into one and a phone network can split one person; read the figures as trends.

**Why do my percentages carry a warning?** Under 30 visits in a window, a single visit moves a rate by whole points, so Insights says to treat them as a direction, not a measurement.

**What happens to analytics after the trial?** Recording never stops. If the 14-day Pro trial ends, or its balance runs out, with no plan behind it, Docsbook stops showing analytics until you subscribe or top up — your docs stay published. See [Plans and pricing](../plans-and-pricing.md).

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Goals and funnels](./goals.md) — Declare what a reader should do, and count who did {target}
- [You hear every reader](./README.md) — Feedback, failed searches, dead ends and the agent loops {message-square}
- [AI visibility](../geo/ai-visibility.md) — Which AI engines read and cite your docs {sparkles}
- [Google Search Console](../seo/search-console.md) — Queries, positions and clicks from Google {search}

<!-- /widget -->
