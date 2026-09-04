---
title: "Read the analytics panel of your documentation site"
description: "What each figure, card and tab in the Docsbook analytics panel measures, what it is not evidence of, and which decision about your documentation it supports."
---

# Web Analytics

The Docsbook analytics panel reports who read your documentation, where they came from, which pages held them, whether they reached the page you are selling, and what your project spent on AI over the same window. It runs on your own site with no third-party trackers, and reading it costs nothing against your project's balance.

## What each figure answers

Every figure on this page exists to settle one question about your documentation. The table below maps the question to the figure; the sections after it say what each figure measures and — as importantly — what it is not evidence of.

| Your question | The figure that answers it |
|---|---|
| Is anybody outside my team reading this? | Visitors, with your own team's visits excluded — see [Who counts as a visitor](#who-counts-as-a-visitor) |
| Are they arriving and bouncing straight off? | Bounce rate and Session time |
| Do they reach the page that sells? | Conversion rate, and the CTA Clicks card |
| What was that worth? | Revenue and Revenue/visitor, once Branding has both settings |
| What is this documentation costing me? | Spend, read straight off the billing ledger |
| Which pages are dead, and which hold people? | The Pages card, ranked by Views or Reading time |
| Are AI crawlers reading the docs at all? | The AI Views card, one line per crawler |

## What you will see

Seven figures sit across the top of the panel. Click any of them to redraw the chart below — except Revenue, which has no chart of its own (it is conversions multiplied by a fixed price, so its line would be the conversion line with a different label).

| Metric | Description |
|---|---|
| Visitors | Distinct readers over the selected period, split into new and returning |
| Revenue | What those readers were worth — see [What did the documentation earn?](#what-did-the-documentation-earn) |
| Spend | What this project's AI cost over the same period — see [What is the documentation costing?](#what-is-the-documentation-costing) |
| Conversion rate | Share of visitors who clicked through to your Call To Action URL |
| Revenue/visitor | Revenue divided by visitors |
| Bounce rate | Share of visits that were one page, under three seconds, and nothing else |
| Session time | How long an average visit lasted |

Each one also shows how it moved against the period immediately before it. Green means the change is good news — which for bounce rate means going **down**. Spend's arrow is grey in both directions, because spend has no good direction to point in.

Below the chart, four cards break the same period down. Each card holds several tabs:

| Card | Tabs |
|---|---|
| Pages | Pages, Headings, Entry, Exit |
| Sources | Referrers, Channels, UTM, Keyword |
| Audience | Devices, Browsers, Countries, Languages |
| Conversions | CTA Clicks, Feedback, Searches |
| AI Views (full width) | AI crawler requests over time, and per bot |

At the very bottom of the page, two more cards — "What readers asked" and
"Where the answers led" — break down your AI chat's own conversations
(topics, why readers came, top searches, languages, outbound links, and the
answered/dead-end/unrated split) over this same range. See
[AI Usage & Cost Statistics](./ai-usage.md) for what each tab shows; unlike
the cards above, rows here don't filter the rest of the dashboard.

Each card picks its tab from a dropdown rather than a row of tabs: four or five
tabs never fit a half-width card, and the row they used to sit in scrolled
sideways inside a card that also scrolls down.

Every row on the first three cards carries **both** figures: how many visitors it
brought and how much revenue they were worth. The control on the right of the
card says which figure the list is ranked by — click it to switch, and every
card switches with it. Two bars are always drawn behind each row: blue is
whatever the list is ranked by, rose is always the money.

**Pages and Headings in the Docsbook analytics panel rank by two more figures**: `Views` and `Reading time`.
Those only mean something for a row that names a place in your docs, which is
why they are offered there and nowhere else — and they count only what happened
on that page. A reader who opened three pages gives each of them its own views
and its own seconds, rather than making all three look as busy as the busiest.
Reading time is averaged over the readers it was actually measured for; a page
with no measurements shows a dash, never `0`.

Hover a row for its visitors, revenue, revenue per visitor and conversion rate,
and for two buttons: one filters the whole dashboard by that value, the other
opens the page or site the row points at. **Details** at the foot of the card
opens the same numbers as a full table, where the filter is a tap away on a
phone.

### Filtering the dashboard by a row

Filtering by a row narrows **everything** — the other cards and the visitor
figures above the chart — so a country, a device or a referrer can be read end
to end: how many came, how well they converted, and which pages they read.
Filters stack, and each one is a chip above the cards that removes itself when
clicked. Spend is the exception: a filter cuts *visits*, and an AI answer or a
translation job is not a visit, so Spend keeps showing the whole project's bill.

The tabs counted per event rather than per visit — Headings, Read Time, UTM,
AI Views, CTA Clicks, Feedback and Searches — cannot be filtered this way. They
say so above their rows while a filter is on, rather than showing unfiltered
numbers under a filtered heading.

**Online now** — a live count of readers active in the last five minutes — is not one of the seven. It is a right-now number rather than a total over the period you picked, so it sits as its own chip beside the panel's title.

### What did the documentation earn?

Revenue in the Docsbook analytics panel needs two settings, and reports nothing until it has both:

- your **Call To Action URL** decides *which* click counts as a conversion — a reader who left your docs for that domain;
- your **Average Product Price** decides what such a click is *worth*.

Both live in **Design → Branding**; see [Branding](../../design/style/branding.md). Until both are filled in, the Revenue and Revenue/visitor tiles are switched off and say which one is missing. They deliberately never show `$0`: a missing price is not a price of zero, and a confident `$0` would read as "nothing sold" when nothing is actually being measured.

Once both are set, Revenue is the number of readers who reached your call-to-action page multiplied by your average price. A reader who clicks through five times counts once.

The same rule produces the revenue on every card row, so the cards and the
figures above them can never disagree about what a sale is. Until both settings
exist, the cards rank by visitors only and the metric control says which setting
is missing.

Matching is by domain, with `www.` treated as the same site. Other subdomains are not folded in — your docs usually live on one, and counting a click back into the docs as a sale would flatter the number.

### What is the documentation costing?

**Spend** is what left this project's balance over the same period: the AI calls
your readers made in chat, the ones you made in the panel, translations,
embeddings, and MCP calls billed against the project. Click it and the chart
redraws as a cost line; each point names the billed calls behind it.

It needs no settings — unlike Revenue, it is read straight off your billing
ledger. That also makes it the one figure here whose `$0` is a real reading
rather than a gap, so a period the panel could not read the ledger for says so
instead of showing zero. Calls that ran on your own API key are counted and cost
nothing.

Because it does not come from visits, Spend stays meaningful in a period nobody
visited — a translation run overnight is a real bill with no reader behind it,
and that is usually the most useful thing this tile has to show you. Look for a
cost spike that no visitor spike explains.

Nothing you add to your balance is netted off this figure: it counts money going
out, so a top-up does not make it dip.

### Who counts as a visitor?

Two kinds of visit are left out of every reader figure on this page: bots, and
**you and your team browsing your own docs**.

The second one matters most on a young project. Before this, a workspace with no
audience yet still showed visits, a bounce rate and a session time — all of them
you, checking your own pages after a publish. That is the one reading that feels
like a signal and is not, and it is exactly when you are most likely to act on
it.

So a number here that is lower than you expected, or zero on a workspace you have
been opening all week, is the report answering honestly: nobody outside your team
has read this yet. Your own visits are not deleted, only kept out of the reader
figures.

### New and returning visitors

The Visitors chart draws two lines: readers seen for the first time, and readers coming back. Hover any point for the pageviews, pages per visitor, and the returning rate in that hour or day.

Because events are kept for at most 30 days, "new" can only mean *not seen in the window we can still read* — never "never seen before". The tooltip states the exact horizon it checked.

### Bounce rate and session time

A **bounce** is a visit of one page, under three seconds, with nothing else — someone who arrived and left without reading. It is a description, not a verdict; a reader who found their answer in one glance also bounces.

**Session time** averages how long visits lasted. Both are computed per visit, so a reader who comes back three times in a week contributes three visits.

If a period holds very few visits, the panel says so under the figures: percentages over a handful of visits swing by whole points per visit, and are a direction rather than a measurement.

### Which Google queries is the site found by?

The **Keyword** tab of the Sources card is the one list that does not come from
your visitors: it comes from Google Search Console. An impression that never
became a click cannot be seen by anything running on your docs site, so this tab
shows what Google saw — the queries you rank for, with position, impressions,
clicks and click-through rate.

Connect Search Console in the SEO tab first. The numbers lag about two days
(Google's own schedule) and the tab states the day they run through. Revenue
here is an **estimate** — clicks multiplied by your site-wide revenue per
visitor — and is labelled and drawn as one, because a modelled figure should
never look like a measured one.

### Which AI crawlers are reading the docs?

The **AI Views** card charts one line per AI crawler instead of a single total, so you can tell which assistants are reading your docs and how that changes over time. The twelve busiest bots are charted, each labelled with the provider behind it, above the per-bot totals.

### Channels

The **Channels** tab groups visits by the *kind* of source — organic search,
social, referral, AI assistant, direct — when the question is which channel
works rather than which site. Hovering a channel names the three sites it
actually consists of, with their shares: "organic search" that is 96% Google and
one spread across five engines are different situations.

### Did readers reach the page that sells?

The **CTA Clicks** card of the Docsbook analytics panel ranks every destination readers left your documentation for — your signup page, pricing, the repo, anything external — so you can see which call to action readers actually follow and from which page they follow it.

### Which pages did readers vote down?

The **Feedback** tab of the same card ranks your pages by the thumbs readers gave them. Both vote widgets are counted together — the "was this helpful" rating at the foot of a page, and the thumbs on an AI answer given on that page — because the question it answers is which page readers approve of, not which button they pressed.

Rows are sorted by dislikes first: the page people voted down is the one to rewrite, while an upvoted page only confirms what already works. Both counts are always shown, zeros included.

### What are readers searching for that isn't there?

The **Searches** tab of the same card ranks what readers typed into your on-page search box, one row per query, with how often it found something and how often it came back empty. A query can carry both counts at once — the same words sometimes resolve and sometimes come back with nothing.

A query with no results is the reader telling you, in their own words, what the docs should cover: check whether a page answering it already exists under a different name, and if not, that is the next page to write. Unlike the other cards, Searches has no metric menu to re-rank by — these rows are counted per search event rather than per visit, so there is no revenue figure to sort on the way Pages and Sources offer.

## A report you have no data for yet

A report with nothing in it teaches nothing, so a tab that has none of your own
rows yet does not render empty. It renders over **sample figures**, faded, with
its own icon in the middle of it and **Enable <em>Tab</em>** under it — Enable
Headings, Enable Channels, Enable Feedback — and one line saying what that
particular list answers.

The whole card is the button. Pressing anywhere on it runs a short guide inside
that card, over those same sample figures: each step names something on the card
by the label printed on it, says how to read it — including what the figure is
*not* evidence of — and names the move it leads to. Finishing or skipping the
guide switches that tab to your own numbers.

Four things worth knowing about it:

- **It is per tab, not per card and not per page.** Pages, Headings, Entry and
  Exit are four switches, not one, and so are Referrers, Channels, UTM and
  Keyword, Devices, Browsers, Countries and Languages, and CTA Clicks, Feedback
  and Searches. They answer different questions with different caveats — Entry names
  one page per visit while Pages credits every page a visit touched — and each
  gets the explanation that is actually about it. A site with plenty of
  referrers and no tagged campaign meets the guide on **UTM** and nowhere else.
- **The tab strip stays live under it.** Switching tabs on a covered card moves
  to that tab's own switch and its own description — and off the switch
  entirely if that tab has rows of yours. Looking through the tabs before
  turning any of them on is the expected first move.
- **It gates nothing.** Every figure on this page was collected the whole time
  regardless — the switch only decides which of two presentations of the same
  report you are looking at, and it is remembered in your browser, per
  workspace. A teammate's view is unaffected, and clearing site data offers
  the guide again.
- **A tab that already has your rows in it is never covered.** It explains
  itself, so there is nothing for a panel over it to add.

Four readouts are switched on whole rather than per tab: the seven figures at
the top, which have no tabs; **AI Views**, whose three tabs are one crawl stream
split by why the crawler came; and the two chat cards, which drop a tab entirely
when the window has no rows for it.

The sample figures are the ones the product tour uses, so what you see before
switching a tab on is the same thing you saw while trying Docsbook out.

## How to open the analytics panel

1. Open any page of your documentation site.
2. Click the **Analytics** tab in the floating toolbar at the bottom.
3. The overview loads automatically with **Today** selected.

## Time ranges

Use the interval switcher (next to the Online badge) to change the window:

| Range | What it covers |
|---|---|
| Now (live) | The last hour, per minute, refreshed while you watch |
| Today | The current calendar day, from midnight |
| Yesterday | The previous calendar day, whole |
| Last 24 hours | A rolling day back from now |
| Last 7 days | A rolling week back from now |
| Last 30 days | A rolling month back from now |

Thirty days is the longest window there is, because events are kept for 30 days and nothing older survives to be charted.

Today and Yesterday are calendar days, not a rolling 24 hours — Today starts at midnight, so early in the day it covers less than Last 24 hours does.

**Now** puts the chart in live mode: the switcher shows a pulsing dot, and the chart and top figures refresh every 5 seconds with a per-minute view of the last hour. The rest of the page (the four cards below, and every other range) still refreshes every 30 seconds.

## Reading referrers

Referrers are grouped by hostname. **Direct / None** means the visitor typed your
URL, came from a bookmark, or arrived from a link that stripped its referrer — on
most documentation sites it is the largest single row, which is why it is listed
rather than dropped.

Rows show the subdomain in grey and the domain in black, so a column of hosts
reads by the site behind them.

A spike in a specific referrer usually means someone shared your docs, which tells you which page was worth sharing.

## Related

- [Tracked events reference](./events.md) — every event behind these figures, and what each one means
- [AI usage & cost statistics](./ai-usage.md) — the chat conversations behind the Spend figure
- [Read time report](../reports/read-time.md) — how the Reading time ranking is measured
- [Visitor countries report](../reports/countries.md) — the Countries tab as its own report, with the reader map
- [Branding](../../design/style/branding.md) — the Call To Action URL and Average Product Price that switch Revenue on
