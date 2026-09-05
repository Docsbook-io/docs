---
title: "See what your documentation earns and which pages are dead"
description: "Docsbook analytics answer four owner questions: where readers come from, which pages they leave, whether they reach your call to action, and what it earned."
tldr: "Docsbook analytics answer four owner questions — where readers come from, which pages lose them, whether they reach the page that sells, and what that was worth. Reading the reports costs nothing against the project balance."
---

# Analytics & Insights

Docsbook records every page view, search, AI question and feedback vote on your documentation, and reports them as answers to questions an owner actually asks — not as a wall of counters. Reading these reports costs nothing against your project's balance; only AI answers, translations, agent runs and the semantic index spend it.

Four questions the reports below are built to answer, with the report that answers each:

| Question | Where it is answered |
|---|---|
| Where do my readers come from? | Sources card — referrers, channels, UTM, Google Search queries — in the [analytics overview](./tracking/overview.md) |
| Which pages are dead, and which hold people? | Pages and Headings tabs, plus the [read time report](./reports/read-time.md) |
| Did readers reach the page that sells? | Conversion rate and CTA Clicks in the [analytics overview](./tracking/overview.md) |
| What was that worth? | Revenue, once a Call To Action URL and an Average Product Price are set in [Branding](../design/style/branding.md) |
| Did they do the specific thing I care about? | [Goals and funnels](./reports/goals-and-funnels.md) — declare the outcome, and it is matched against history already recorded |
| Can I trust any of these numbers? | [How measurement works](./how-measurement-works.md) — what a visitor is, how bots and your own team are excluded, and what is deliberately not collected |

## Which pages are readers leaving without converting?

Open the **Pages** card of the analytics overview and switch its tab to **Exit**. The Exit tab names the last page of each visit, so the pages at the top of it are where readers stop — and every row carries both figures at once, how many visitors it brought and what they were worth. A page high on Exit and low on CTA Clicks is a page readers finish and leave.

Hovering a row gives its visitors, revenue, revenue per visitor and conversion rate; clicking the filter button narrows the whole dashboard to that page, so you can read one page end to end. See [Analytics overview](./tracking/overview.md) for every card and tab.

## What do readers do on the page, not just which page they opened?

Docsbook tracks the actions, not only the views: AI chat opens, questions asked, code blocks copied, outbound links clicked, sidebar navigations, language switches, and which headings were actually scrolled into view. Heading views concentrated at the top of a long page mean readers are not reaching the rest of it.

The full list, with what each event means, is the [tracked events reference](./tracking/events.md).

## Where are readers arriving from that you do not serve yet?

The **Countries** report and the reader map pair each country of origin with the share of its readers who landed on a page in a translated language. A country that sends readers and gets none of them onto a translation is a market you are paying to attract and then losing at the language barrier.

See [visitor countries report](./reports/countries.md), and [translation settings](../translation/settings.md) for turning a language on.

## In this section

<!-- widget:cards -->

- [How measurement works](./how-measurement-works.md) — cookieless visitor identity, two-layer bot filtering, the read-time clip, retention and privacy — the definitions every number below inherits
- [Tracking overview](./tracking/overview.md) — every figure, card and tab in the analytics panel, and what each one is not evidence of
- [Tracked events](./tracking/events.md) — all 36 `docs.*` events, what fires each one, and the payload it carries
- [AI usage and cost](./tracking/ai-usage.md) — what is metered, how a call is priced, and what your chat was asked and cost
- [Goals and funnels](./reports/goals-and-funnels.md) — declare what a reader should do, then measure whether they did
- [Read time](./reports/read-time.md) — how time-on-page is measured, and the clip the figure rests on
- [Countries and languages](./reports/countries.md) — where readers are, how reliably that is known, and which of them read a translation

<!-- /widget -->

## Related

- [Branding](../design/style/branding.md) — the Call To Action URL and Average Product Price that switch on conversion and revenue reporting
- [Webhooks](../reference/webhooks.md) — get told about a traffic drop or an unanswered question instead of checking for one
- [MCP tools reference](../reference/mcp-tools.md) — reading the same numbers from an agent
