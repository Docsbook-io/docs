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

Below the chart the cards break the same period down by page, referrer, device, AI crawler, outbound link and feedback.

| Card | Description |
|---|---|
| Top pages | Most-visited pages ranked by view count |
| Referrers | Where visitors came from (Google, GitHub, direct, etc.) |
| AI Views | Requests from AI crawlers (ChatGPT, Claude, Perplexity, Google-Extended and others) |
| CTA Clicks | Outbound links readers clicked to leave your docs (signup, pricing, repo, …) |
| Feedback | Thumbs up and down each page collected, most-disliked first |

**Online now** — a live count of readers active in the last five minutes — is not one of the six. It is a right-now number rather than a total over the period you picked, so it sits as its own chip beside the panel's title.

### Revenue

Revenue needs two settings, and reports nothing until it has both:

- your **Call To Action URL** decides *which* click counts as a conversion — a reader who left your docs for that domain;
- your **Average Product Price** decides what such a click is *worth*.

Both live in **Design → Branding**. Until both are filled in, the Revenue and Revenue/visitor tiles are switched off and say which one is missing. They deliberately never show `$0`: a missing price is not a price of zero, and a confident `$0` would read as "nothing sold" when nothing is actually being measured.

Once both are set, Revenue is simply the number of readers who reached your call-to-action page multiplied by your average price. A reader who clicks through five times counts once.

Matching is by domain, with `www.` treated as the same site. Other subdomains are not folded in — your docs usually live on one, and counting a click back into the docs as a sale would flatter the number.

### New and returning visitors

The Visitors chart draws two lines: readers seen for the first time, and readers coming back. Hover any point for the pageviews, pages per visitor, and the returning rate in that hour or day.

Because events are kept for at most 30 days, "new" can only mean *not seen in the window we can still read* — never "never seen before". The tooltip states the exact horizon it checked.

### Bounce rate and session time

A **bounce** is a visit of one page, under three seconds, with nothing else — someone who arrived and left without reading. It is a description, not a verdict; a reader who found their answer in one glance also bounces.

**Session time** averages how long visits lasted. Both are computed per visit, so a reader who comes back three times in a week contributes three visits.

If a period holds very few visits, the panel says so under the figures: percentages over a handful of visits swing by whole points per visit, and are a direction rather than a measurement.

### AI Views

The **AI Views** tab of the Referrers card charts one line per AI crawler instead of a single total, so you can tell which assistants are reading your docs and how that changes over time. The twelve busiest bots are charted, each labelled with the provider behind it, above the per-bot totals.

### CTA Clicks

The **CTA Clicks** card ranks every destination readers left your documentation for — your signup page, pricing, the repo, anything external — so you can see which call to action readers actually follow and from which page they follow it.

### Feedback

The **Feedback** tab of the same card ranks your pages by the thumbs readers gave them. Both vote widgets are counted together — the "was this helpful" rating at the foot of a page, and the thumbs on an AI answer given on that page — because the question it answers is which page readers approve of, not which button they pressed.

Rows are sorted by dislikes first: the page people voted down is the one to rewrite, while an upvoted page only confirms what already works. Both counts are always shown, zeros included.

## How to Open

1. Open any page of your documentation site.
2. Click the **Analytics** tab in the floating toolbar at the bottom.
3. The overview loads automatically with the last 24 hours selected.

## Time Ranges

Use the interval selector (top-right of the analytics panel) to switch views:

| Range | Plan required |
|---|---|
| 24H | Free |
| 7D | Pro |
| 30D | Growth / Business / Scale |

## Reading Referrers

Referrers are grouped by hostname. `(direct)` means the visitor typed your URL or came from a bookmark.

A spike in a specific referrer usually means someone shared your docs — great signal for which content resonates.

---

> **Start tracking your readers today.**
> [Connect your GitHub repo →](https://docsbook.io/connect)
