---
title: "Read time: how long readers really spend on each page"
description: "How Docsbook measures time on page — segments, the 300-second clip, the three-second floor — and why the number is trustworthy in a way naive time-on-page is not."
tldr: "Docsbook emits a read-time segment each time a reader leaves a page, clips every segment at 300 seconds before summing, and averages by segment count. The clip is not cosmetic: without it, a sweep of 11,176 real sessions inflated total read time roughly thirtyfold."
---

# Read time

A page can lead your views and be abandoned in three seconds. Read time is the
figure that separates the two — and it is the figure most analytics tools get
wrong, in a way that is invisible until you look at the raw numbers.

## What you get

Every page of your documentation carries an average read time, and the Pages and
Headings cards can be ranked by it. A page with no measurements shows a **dash,
never `0`** — a zero would read as "nobody stayed" when the truth is "nothing was
measured".

Read time is counted **per page, not per visit**: a reader who opens three pages
gives each of them its own seconds, rather than making all three look as busy as
the busiest.

Reading this report costs nothing against your project's balance, and it is
available on every plan.

## How it is built

**A segment, not a stopwatch.** The tracker starts a clock when a page opens and
reads it when the reader leaves it — on `pagehide`, on in-site navigation to
another page, and on `visibilitychange → hidden` on iOS, where `pagehide` is
unreliable. Each reading emits one `docs.read_time` event carrying that stretch
of seconds, and **resets the clock**. A reader who hides the tab and comes back
therefore produces two segments rather than one double-counted stretch.

**Segments under 3 seconds are never emitted.** Below that, a reader passed
through; recording it would add noise to a page's mean without adding a reading.

**Delivery is by beacon.** Read time, heading views and exits go through
`navigator.sendBeacon` to a same-origin endpoint, batched at up to 100 events
per beacon, because the ordinary logging transport debounces for two seconds
over `fetch` and does not survive a tab close. Every collector is idempotent: it
returns only the events it has not already sent, so an iOS hidden-flush followed
by a real exit does not double-count, and a page restored from the back/forward
cache can flush again.

**Every segment is clipped at 300 seconds before anything sums it.** This is the
number the whole report rests on. The emitter keeps counting while a desktop tab
sits in the background, and on a calibration sweep of **11,176 real sessions
across 7 workspaces**: 40 individual segments exceeded two hours, the 99th
percentile was **81,342 seconds** — 22 hours — and summing raw segments inflated
total read time from a true **42,160 seconds to 1,268,422**, roughly thirtyfold.

**The clip is defined once, in one module with no imports, and re-exported to
everything that quotes a time figure** — the per-page average, the visit
summary, the chat table's "time on site" column, the goals layer and the MCP
tools. A second, more generous definition of "time on site" one column away from
the first is exactly how two numbers about the same reader start disagreeing.

**The average divides by segment count, not by visit count.** A reader who tabbed
away and back contributes two segments to one visit; averaging by visit would
credit that visit twice.

**Bots are excluded by the same User-Agent filter the rest of the dashboard
uses**, so a page's read time reconciles with its view count. The behavioural
crawler gate — a visit with no JavaScript-emitted event is a crawler whatever its
User-Agent claims — needs full session reconstruction and is applied in the visit
layer instead; see [How measurement works](../how-measurement-works.md).

## What a page's read time tells you

Read time is a comparison, not a verdict: it means something against the length
of the page and the job the page does.

| Shape | Likely reading | Move |
|---|---|---|
| Low read time on a complex page | Unclear, too long, or badly structured | Restructure before rewriting |
| High read time on a short page | Readers are rereading, not enjoying | Clarify the paragraph they are stuck on |
| Consistent read time across a tutorial | Readers are progressing as intended | Nothing |
| Views high, read time near zero | The page wins the click and loses the reader | Its opening does not match the question that brought them |

Pair it with heading views: read time says how long they stayed, heading views
say how far down they got. A long read time concentrated in the first two
headings is a reader stuck, not a reader engaged.

## Why this is the right way

| Rule | Why it works | Source |
|---|---|---|
| Exit-time events must go by beacon, not a debounced `fetch` | Beacon requests "are guaranteed to be initiated before page is unloaded and are allowed to run to completion" | [W3C Beacon API](https://www.w3.org/TR/beacon/) |
| Listen on `pagehide`, and additionally on visibility change | `unload` "is still unreliable, so avoid using it unless absolutely necessary"; `pagehide` "fires in all cases where the `unload` event fires" and also on bfcache entry | [web.dev: bfcache](https://web.dev/articles/bfcache) |
| A page that keeps counting while hidden is measuring the wrong thing | The Page Visibility API exists because developers "have been designing web pages as if they are always visible" | [W3C Page Visibility Level 2](https://www.w3.org/TR/page-visibility-2/) |
| The best-practice target is foreground time | GA4 defines user engagement as "the amount of time someone spends with your web page in focus" | [GA4: User engagement](https://support.google.com/analytics/answer/11109416) |
| A per-page reading beats a session-derived one | Universal Analytics computed a session without engagement hits on the last page as "The time of the first hit on the last page - the first hit on the first page" — the final page, the one the reader chose to end on, contributes nothing | [Universal Analytics: session duration](https://support.google.com/analytics/answer/1006253) |
| A dash beats a zero | A confident `0` on an unmeasured page is indistinguishable from a measured abandonment, and only one of those is actionable | Mechanism, this page |

That last row is the whole reason Docsbook emits its own exit event rather than
inferring time from the gap between pageviews. The last page of a visit — the
one the reader stopped on, which is usually the one you most want to judge — is
precisely the page a gap-based measurement cannot see.

## Limits and open questions

- **Read time is clipped, not gated on visibility.** On desktop, a background tab
  keeps accruing seconds until the 300-second clip stops it. The error therefore
  has a known direction (upward) and a known bound (300 seconds per segment),
  which is why it is usable — but it is **not** the same measurement as a
  focus-gated engagement time, and this page does not claim it is. If your
  readers habitually park documentation in a background tab, treat the figure as
  an upper bound.
- **A page open for longer than five minutes in one stretch is recorded as five
  minutes.** For a long tutorial that a reader genuinely works through, this
  understates. The clip trades a bounded understatement on rare long reads for a
  thirtyfold overstatement on idle tabs.
- **Under question: "average read time" is not "average attention".** What is
  verifiable is the mechanism above — segments, the floor, the clip, the
  divisor. What is not verifiable from this data is whether the reader was
  looking at the screen. No web analytics product can measure that, and none
  should imply it.
- **Readers with JavaScript disabled, and crawlers, contribute no read time at
  all.** Their pageviews still count, so a page crawled heavily can show a high
  view count against a thin read-time sample.
- **Thirty days is the whole history.** There is no long-term read-time trend to
  draw.

## How to open the read time report

1. Open your documentation site.
2. Float Widget → **Analytics** tab.
3. Rank the **Pages** or **Headings** card by `Reading time`.

`Reading time` is offered on Pages and Headings only. It means something for a
row that names a place in your documentation and nothing for a row that names a
country or a browser, so it is offered there and nowhere else.

## Related

- [How measurement works](../how-measurement-works.md) — the clip, the beacon path and the bot filters in full
- [Analytics overview](../tracking/overview.md) — the Pages card this ranking lives in
- [Tracked events reference](../tracking/events.md) — heading views, which say how far down a long page readers get
- [Goals and funnels](./goals-and-funnels.md) — measuring what the visit achieved, not only how long it lasted
