---
title: "Declare what a reader should do, then measure whether they did"
description: "Goals and funnels turn a docs site into something with an outcome: name the action that matters, order it into a route, and read where the route leaks."
tldr: "A goal is one action you want a reader to take — reach a page, fire an event, scroll to a section, leave for a host. A funnel is an ordered list of goals, and Docsbook counts a visit as reaching step N only if it hit steps 1 to N in that order. Both are matched retroactively against the history already recorded, so the numbers appear immediately."
---

# Goals and funnels

Pageviews cannot tell you whether the documentation worked. A goal is you
stating what "worked" means for your project; a funnel is you stating the route
to it. Everything below is then measured against those statements rather than
against a default somebody else chose.

## What you get

Name an outcome — `reached_pricing`, `copied_the_install_snippet`,
`left_for_signup` — and Docsbook reports how many **visits** completed it over
the window, with the daily series behind it, and (if you declared what one is
worth) what they were worth. String several into a route and you get a
step-by-step funnel that names the worst transition, not just the smallest
step.

New goals are matched **retroactively against the history already recorded**, so
a goal you declare today reports last week's numbers immediately instead of
starting from zero.

## The four kinds of goal

| Kind | Matches | Use it for |
|---|---|---|
| `page` | A page path | "They reached the pricing page" |
| `event` | One of the tracked `docs.*` events | "They copied a code block", "they asked the assistant" |
| `section` | A heading anchor scrolled into view, with or without the `#` | "They got as far down the page as the install steps" |
| `outbound` | A destination host they left for | "They went to your app, your repo, or signup" |

An `event` goal can be narrowed to one page with an optional scope, which is
what lets a single event be two different goals — "copied the quickstart
snippet" and "copied the auth snippet" are the same event on different pages.

## How it is built

**Counted per visit, never per event.** A `section` goal fires every time a
reader scrolls past that heading; counting events would report one person as
five conversions. Funnel *potential value* goes further and counts per
**person**, so a reader who walked the route twice contributes one reader's
worth rather than two.

**Order is enforced by comparing hit times, not by membership.** For each step,
Docsbook looks for the first hit at or after the previous step's hit. A reader
who landed on step 3 first and only later saw step 1 is correctly not counted as
having reached step 3.

**The conversion window bounds how long a later step still counts.** Leave it
empty and the visit itself is the window, which is the honest default for a docs
site. Set it, and it is clamped to the history that actually exists — a window
longer than retention describes conversions that can never be observed.

**Rates are suppressed on thin data.** A funnel's overall conversion rate is
withheld below **30 visits**, and each step is flagged `lowSample` when the step
before it had fewer than 30 — so a solid step 2 still quotes a rate while a thin
step 5 does not. Median and p90 time-to-convert are withheld below **5**
conversions, where the list of converters is the answer and a percentile is not.

**`leak_index` names the worst transition, not the smallest step.** The smallest
step is almost always the last one; the biggest proportional drop between two
adjacent steps is where the route actually breaks.

**Money stays off unless you switch it on.** A goal value of `0` is refused
outright — `null` and `0` are different claims, and only one of them belongs in
a revenue figure. Where no value is declared, money columns are blank rather
than `$0`.

### What the validator refuses, and what it only warns about

These are enforced identically whether you create a goal in the panel, over
[MCP](../../reference/mcp-tools.md), or through the assistant — one rule, so no
surface accepts what another rejects.

| Rule | Level | Reasoning it gives you |
|---|---|---|
| An `event` goal naming an event these docs do not emit | Refused | It could never fire, and a goal that never fires looks exactly like a goal with 100% drop-off |
| A goal value of `0` | Refused | `$0` reads as a measurement instead of an absent declaration |
| A funnel with fewer than 2 steps | Refused | With one step there is no transition to measure — that is a goal |
| A funnel step naming a goal that does not exist | Refused | A funnel silently dropping a step reports a *better* conversion rate than the real one |
| More than 8 steps | Refused | Split it in two, so each half has a denominator worth reading |
| More than 5 steps | Warning | Even at 60% per step, under 8% survives to the end |
| A single page as step 1 | Warning | Most docs readers arrive deep from search or an AI answer; a narrow entry excludes the majority of traffic before measuring anything |
| A funnel ending on a scroll or section view | Warning | It measures attention, not outcome |
| A goal name containing a path, id, `@` or a long number | Warning | Both a cardinality problem and a privacy one — goal names reach exports and chat replies |
| More than 6 live goals | Warning | Past six the list stops ranking and becomes a log |

Deleting a goal **archives** it rather than destroying it, because a funnel step
pointing at a vanished goal would otherwise take the step with it.

## The reports built on top

| Report | What it answers |
|---|---|
| Goals overview | Completions per goal over the window, plus the daily series |
| Funnel | Step-by-step completion, the share of the previous step that continued, top sources and countries at each step, and `leak_index` |
| Goal journeys | Everyone who completed one goal, and how long they took from first seen to converting |
| Goal visitors | Recent readers and which goals each completed |
| Visit outcomes | The success / dead-end / bounce / partial split for every visit, with no goal declared at all |
| Reverse funnel | Works backwards from visits that ended well: which entry pages lead to success, and in how many steps |
| Retention | W1/W4 return rate by weekly cohort |

**Time-to-convert is reported as median and p90, never a mean.** Time to convert
on a docs site is bimodal — readers who arrive ready, and readers who evaluate
for weeks — and the mean lands in the empty valley between the two modes,
describing a visitor who does not exist.

**The reverse funnel needs no hypothesis.** A declared funnel can only measure
the route you thought of; working backwards from successful visits reports the
route readers actually found, which is often one nobody designed. When that
route is real, the action is to promote its entry point in the navigation.

**Potential value is a readiness share, not a forecast.** Where a reader has
*not* converted, Docsbook can still rank them: it builds a profile of what
converters looked like before they converted — reading time, pages, and
crucially the pages converters open *more than everyone else* — and scores each
reader against it. A page opened by 80% of converters and 8% of everyone else
carries the finding; a page opened by 92% and 90% carries nothing. The profile
is only built at **5 or more converters** and carries at most **12**
discriminating paths.

## Why this is the right way

| Rule | Why it works | Source |
|---|---|---|
| Measure task completion, not traffic | "if users can't accomplish their target task, all else is irrelevant. User success is the bottom line of usability" — Nielsen & Budiu, 2001, reviewed 2021 | [NN/g: Success Rate](https://www.nngroup.com/articles/success-rate-the-simplest-usability-metric/) |
| Suppress rates on small denominators | The suppression floor is the same 30-visit floor every rate in the product uses; it is applied per step because a funnel's later steps are always the thinnest | [How measurement works](../how-measurement-works.md) |
| Steps must be ordered, not just present | An unordered "did they touch these pages" report cannot distinguish a journey from three unrelated landings — the same reason route analysis exists rather than a top-pages list | Mechanism, this page |
| Count outcomes per visit, value per person | A repeated scroll is one reader's intent expressed twice; summing it as revenue is how a funnel invents money out of a page refresh | Mechanism, this page |

## Limits and open questions

- **A visitor is a hashed IP.** Every count here inherits that: corporate NAT
  merges readers, mobile networks split them. Read five rows of goal visitors to
  learn who is evaluating you; do not read the total as a headcount. See
  [How measurement works](../how-measurement-works.md).
- **The source shown on a journey is last touch** and over-credits Direct.
  Treat it as a hint, never as attribution.
- **Retention cohorts are capped by 30-day history.** W4 needs a 30-day window
  to exist at all; on a 24-hour or 7-day period it is structurally zero and
  means nothing. There is no year-over-year view and there cannot be one.
- **Retention has no universally good direction.** High return is healthy for
  reference documentation and a failure for onboarding — the number cannot know
  which section it is describing.
- **Potential value is reasoned, not fitted.** Its weights are not calibrated
  against an observed base rate, so it ranks readers against each other honestly
  and must never be summed into a pipeline figure.
- **A funnel measures the route you declared.** If readers succeed by a path you
  did not describe, the funnel will report failure while the reverse funnel
  reports the truth. Read both.

## Related

- [How measurement works](../how-measurement-works.md) — the visit definition, the bot filters and the sample floors every number here inherits
- [Analytics overview](../tracking/overview.md) — conversion rate and revenue in the headline strip
- [Tracked events reference](../tracking/events.md) — the event names an `event` goal can match
- [MCP tools reference](../../reference/mcp-tools.md) — `create_goal`, `create_funnel`, `get_funnel`, `get_retention` and the rest
