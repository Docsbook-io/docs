---
title: "Measure how long readers actually spend on each page"
description: "The read time report ranks the pages of your documentation by the time readers really spent on them, so a page that is opened often and read never stops hiding."
---

# Read Time Analytics

The read time report of your Docsbook documentation site measures how long readers spend on each page, not whether they opened it. A page can lead your views and still be abandoned in three seconds; read time is the figure that separates the two. Reading this report costs nothing against your project's balance.

## What it shows

| Metric | Description |
|---|---|
| Average read time | Mean time spent on a page per visit |
| Pages by engagement | Pages ranked from most to least read |

Reading time is averaged over the readers it was actually measured for. A page with no measurements shows a dash, never `0` — a zero would read as "nobody stayed" when the truth is "nothing was measured".

Read time is counted per page, not per visit: a reader who opens three pages gives each of them its own seconds, rather than making all three look as busy as the busiest.

## What does a page's read time tell me?

Read time is a comparison, not a verdict: it means something against the length of the page and the job the page does.

- **Low read time** on a complex page → content may be unclear, too long, or poorly structured.
- **High read time** on a short page → readers may be confused and rereading.
- **Consistent read time** across a tutorial → readers are progressing through it as intended.
- **Views high, read time near zero** → the page wins the click and loses the reader; its opening does not match the question that brought them.

Use this ranking to decide which pages to rewrite first.

## How to open the read time report

1. Open your docs site.
2. Float Widget → **Analytics** tab.
3. Select the **Read Time** view.

The same figure is available inside the main panel: the **Pages** and **Headings** cards can be ranked by `Reading time` as well as by visitors, revenue and views.

## Related

- [Analytics overview](../tracking/overview.md) — the Pages card this ranking lives in, and every other figure in the panel
- [Tracked events reference](../tracking/events.md) — heading views, which say how far down a long page readers get
- [Analytics & insights](../README.md) — the four questions these reports are built to answer
