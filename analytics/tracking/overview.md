---
title: "Analytics Overview"
description: "Track visitors, revenue, conversion rate, bounce rate and session time for your documentation, plus top pages, referrers and live online readers — privacy-first analytics with no third-party trackers."
---

# Web Analytics

Know exactly how many people read your docs and where they come from — without any third-party trackers.

## What You'll See

Six figures sit across the top of the panel. Click any of them to redraw the chart below — except Revenue, which has no chart of its own (it is conversions multiplied by a fixed price, so its line would be the conversion line with a different label).

| Metric | Description |
|---|---|
| Visitors | Distinct readers over the selected period, split into new and returning |
| Revenue | What those readers were worth — see [Revenue](#revenue) |
| Conversion rate | Share of visitors who clicked through to your Call To Action URL |
| Revenue/visitor | Revenue divided by visitors |
| Bounce rate | Share of visits that were one page, under three seconds, and nothing else |
| Session time | How long an average visit lasted |

Each one also shows how it moved against the period immediately before it. Green means the change is good news — which for bounce rate means going **down**.

Below the chart, four cards break the same period down. Each card holds several tabs:

| Card | Tabs |
|---|---|
| Pages | Pages, Headings, Entry, Exit |
| Sources | Referrers, Channels, UTM, Keyword |
| Audience | Devices, Browsers, Countries, Languages |
| Conversions | CTA Clicks, Feedback |
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

**Pages and Headings rank by two more figures**: `Views` and `Reading time`.
Those only mean something for a row that names a place in your docs, which is
why they are offered there and nowhere else — and they count only what happened
on that page. A reader who opened three pages gives each of them its own views
and its own seconds, rather than making all three look as busy as the busiest.
Reading time is averaged over the readers it was actually measured for; a page
with no measurements shows a dash, never `0`. It stays a **Pro** feature.

Hover a row for its visitors, revenue, revenue per visitor and conversion rate,
and for two buttons: one filters the whole dashboard by that value, the other
opens the page or site the row points at. **Details** at the foot of the card
opens the same numbers as a full table, where the filter is a tap away on a
phone.

### Filtering

Filtering by a row narrows **everything** — the other cards and the six figures
above the chart — so a country, a device or a referrer can be read end to end:
how many came, how well they converted, and which pages they read. Filters
stack, and each one is a chip above the cards that removes itself when clicked.

The tabs counted per event rather than per visit — Headings, Read Time, UTM,
AI Views, CTA Clicks and Feedback — cannot be filtered this way. They say so
above their rows while a filter is on, rather than showing unfiltered numbers
under a filtered heading.

**Online now** — a live count of readers active in the last five minutes — is not one of the six. It is a right-now number rather than a total over the period you picked, so it sits as its own chip beside the panel's title.

### Revenue

Revenue needs two settings, and reports nothing until it has both:

- your **Call To Action URL** decides *which* click counts as a conversion — a reader who left your docs for that domain;
- your **Average Product Price** decides what such a click is *worth*.

Both live in **Design → Branding**. Until both are filled in, the Revenue and Revenue/visitor tiles are switched off and say which one is missing. They deliberately never show `$0`: a missing price is not a price of zero, and a confident `$0` would read as "nothing sold" when nothing is actually being measured.

Once both are set, Revenue is simply the number of readers who reached your call-to-action page multiplied by your average price. A reader who clicks through five times counts once.

The same rule produces the revenue on every card row, so the cards and the
figures above them can never disagree about what a sale is. Until both settings
exist, the cards rank by visitors only and the metric control says which setting
is missing.

Matching is by domain, with `www.` treated as the same site. Other subdomains are not folded in — your docs usually live on one, and counting a click back into the docs as a sale would flatter the number.

### New and returning visitors

The Visitors chart draws two lines: readers seen for the first time, and readers coming back. Hover any point for the pageviews, pages per visitor, and the returning rate in that hour or day.

Because events are kept for at most 30 days, "new" can only mean *not seen in the window we can still read* — never "never seen before". The tooltip states the exact horizon it checked.

### Bounce rate and session time

A **bounce** is a visit of one page, under three seconds, with nothing else — someone who arrived and left without reading. It is a description, not a verdict; a reader who found their answer in one glance also bounces.

**Session time** averages how long visits lasted. Both are computed per visit, so a reader who comes back three times in a week contributes three visits.

If a period holds very few visits, the panel says so under the figures: percentages over a handful of visits swing by whole points per visit, and are a direction rather than a measurement.

### Keyword

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

### AI Views

The **AI Views** card charts one line per AI crawler instead of a single total, so you can tell which assistants are reading your docs and how that changes over time. The twelve busiest bots are charted, each labelled with the provider behind it, above the per-bot totals.

### Channels

The **Channels** tab groups visits by the *kind* of source — organic search,
social, referral, AI assistant, direct — when the question is which channel
works rather than which site. Hovering a channel names the three sites it
actually consists of, with their shares: "organic search" that is 96% Google and
one spread across five engines are different situations.

### CTA Clicks

The **CTA Clicks** card ranks every destination readers left your documentation for — your signup page, pricing, the repo, anything external — so you can see which call to action readers actually follow and from which page they follow it.

### Feedback

The **Feedback** tab of the same card ranks your pages by the thumbs readers gave them. Both vote widgets are counted together — the "was this helpful" rating at the foot of a page, and the thumbs on an AI answer given on that page — because the question it answers is which page readers approve of, not which button they pressed.

Rows are sorted by dislikes first: the page people voted down is the one to rewrite, while an upvoted page only confirms what already works. Both counts are always shown, zeros included.

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
  Keyword, Devices, Browsers, Countries and Languages, and CTA Clicks and
  Feedback. They answer different questions with different caveats — Entry names
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
  workspace. A teammate's view is unaffected, and clearing site data simply
  offers the guide again.
- **A tab that already has your rows in it is never covered.** It explains
  itself, so there is nothing for a panel over it to add.

Four readouts are switched on whole rather than per tab: the six figures at the
top, which have no tabs; **AI Views**, whose three tabs are one crawl stream
split by why the crawler came; and the two chat cards, which drop a tab entirely
when the window has no rows for it.

The sample figures are the ones the product tour uses, so what you see before
switching a tab on is the same thing you saw while trying Docsbook out.

## How to Open

1. Open any page of your documentation site.
2. Click the **Analytics** tab in the floating toolbar at the bottom.
3. The overview loads automatically with **Today** selected.

## Time Ranges

Use the interval switcher (next to the Online badge) to change the window:

| Range | Plan required |
|---|---|
| Now (live) | Free |
| Today | Free |
| Yesterday | Free |
| Last 24 hours | Free |
| Last 7 days | Pro |
| Last 30 days | Growth / Business / Scale |

Today and Yesterday are calendar days, not a rolling 24 hours — Today starts at midnight, so early in the day it covers less than Last 24 hours does.

**Now** puts the chart in live mode: the switcher shows a pulsing dot, and the chart and top figures refresh every 5 seconds with a per-minute view of the last hour. The rest of the page (the four cards below, and every other range) still refreshes every 30 seconds.

## Reading Referrers

Referrers are grouped by hostname. **Direct / None** means the visitor typed your
URL, came from a bookmark, or arrived from a link that stripped its referrer — on
most documentation sites it is the largest single row, which is why it is listed
rather than dropped.

Rows show the subdomain in grey and the domain in black, so a column of hosts
reads by the site behind them.

A spike in a specific referrer usually means someone shared your docs — great signal for which content resonates.

---

> **Start tracking your readers today.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
