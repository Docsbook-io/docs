---
title: "Turning a documentation finding into something a business will act on"
description: "The shape a finding has to take before anyone acts on it: what to fix, why this one, who fixes it, and the one number that will say it helped."
tldr: "A finding nobody acts on was written for the wrong reader. Every line of a report answers four questions — what to fix, why this one, who fixes it, how we will know it helped — said in the reader's terms rather than the metric's, with absolute counts beside every rate and a named owner at the end. Five items is a plan; twenty is a backlog dump that gets ignored."
---

# Translating numbers into something a business acts on

A finding nobody acts on was written for the wrong reader. A report's job is not
to prove that the analysis happened; it is to make one person able to decide
what to do on Monday.

This page is about the last step of an audit — the translation. The readings
themselves live elsewhere: [metrics](./metrics.md) and
[behaviour](./behaviour.md) for what readers did,
[content detectors](./content-detectors.md) for what is wrong with the text,
[goals and funnels](./goals-and-funnels.md) for what the owner said should
happen, and [did it work?](./did-it-work.md) for whether the last change
helped.

## What shape does a finding have to take?

Every line answers four questions: **what to fix, why this one, who fixes it,
how we will know it helped.**

```
Period: last 7 days · 1,240 visits · source tier: full (behaviour + ranked digest)

#1  /billing/invoices — health 31/100 (readers giving up dominates; 3 dislikes)
    Why now:   412 readers, 58 gave up here — the largest single loss in the set
    Effort:    M (rewrite of one section, no new page)
    Effect:    dead-end rate on this page 14% → under 8% within two weeks
    Owner:     the billing docs owner — rewrite brief, after the journeys are read

#2  "sso saml setup" — unanswered 23×, zero results 11× (two independent signals agree)
    Why now:   no page exists; workspace impact: high
    Effort:    L (new page)
    Effect:    the query stops appearing in unanswered questions within one release
    Owner:     whoever owns the authentication docs

#3  /quickstart — health 44/100 (dislikes dominate; 9 of 11 votes negative)
    Why now:   highest-traffic page in the set; a correctness problem, not a gap
    Effort:    S (accuracy pass on two steps)
    Effect:    assistant satisfaction on this page recovers above the warning line
    Owner:     the quickstart owner

Not this week: 14 further pages below the cut, all under 40 visits in the period.
Excluded as noise: 6 pages scoring badly on fewer than 5 events.
```

The `source tier` line on the header is part of the finding, not decoration:
it says how much data the run actually had, which is what stops a thin week
being read as a strong result — see [metrics](./metrics.md).

The rules behind that block:

- **Absolute counts next to every rate.** "14%" is unarguable and unactionable;
  "58 of 412 readers" is neither.
- **Effort as S/M/L, with the reason in parentheses.** The reason is what stops
  an L being negotiated down to an S in a meeting.
- **The effect line names one number and a horizon.** Two numbers is a wish.
- **Every line ends with a named owner**, or with an explicit "nobody obvious
  owns this — here is the work in one sentence". A line without an executor is
  not a plan, it is a complaint.

**Five items is a plan. Twenty is a backlog dump that gets ignored.** Everything
below the cut is one line with a count, so the reader can see that it was
considered and set aside rather than missed.

## How do I say it in the reader's terms rather than the metric's?

| Instead of | Say |
|---|---|
| "dead_end_rate 14%" | "58 of 412 readers left this page without getting what they came for" |
| "position 8.4, CTR 0.6%" | "1,840 people saw this page in search results this month and 11 clicked. The title they saw shares no words with what they typed." |
| "zero_click_rate elevated" | "readers searched, saw your pages listed, and opened none of them — the titles are not reading as the answer" |
| "content_health 31/100" | "on this page, readers giving up is what drives the score, not disliked answers — so it needs a rewrite of the section they give up in, not a correctness pass" |
| "funnel completion 8%" | "4,000 sessions walked quick start → features → billing; 320 took the action at the end" |
| "12% of conversations are pricing-stage" | "14 of 118 conversations were people asking what it costs before deciding — and the assistant had nothing to answer 9 of them with" |

The pattern in every row is the same: replace the ratio with the two counts it
came from, and say what the reader was trying to do when the number was
recorded.

## Quote the reader

A query in someone's own words moves an author more than any aggregate, and
they can verify it without rerunning the analysis. Wherever a reader wrote
something — a search, a question to the assistant, a piece of feedback — quote
it verbatim, with the count of separate visits behind it.
[User language](../lenses/user-language.md) is the fuller reading; here the
quote is simply the cheapest way to make a number believable.

## Which conversions must you refuse?

- **Never convert findings into money, pipeline, or deflected support tickets
  on the owner's behalf.** Deflection counts a reader who gave up the same as
  one who got help. If the owner wants a figure, ask *them* for their cost per
  ticket and label the result as their assumption.
- **Never restate a buying-stage count as intent or revenue.** It is a count of
  conversations classified from text.
- **Never restate someone else's impact estimate in your own units.** Pass it
  through as given, and label your own estimates as yours.
- **Never present impressions as an audience size.** They are counted per
  query.
- **Never promise a search position.** You can promise a better pitch to people
  already being shown the page — which is a different and much more defensible
  claim, because impressions, average position and click-through are three
  separate failures wearing one word, and only the third is a pitch problem
  ([Google Search Central, core updates](https://developers.google.com/search/updates/core-updates)).

## Measured or hypothesis, on every line

Findings backed by data carry the dated window and the numbers behind them.
Findings without carry **`hypothesis`** and say what the missing data would have
settled. Keep the two visibly separated — a reader who cannot tell which is
which discounts both.

"This title is 74 characters" is a fact. "This title is a label, not a search
intent" is a hypothesis. Length, duplication, missing frontmatter, heading
skips, missing alt text and orphan pages are all verifiable from the text alone
and stay facts even with no analytics at all.

## Where does the machine format go?

Underneath. Structured findings exist so that a tool can consume them — the
`action` and `constraints` fields are instructions for a program, not prose for
a person. Never paste that JSON into a reply as "the report": a wall of
`"severity": "high"` reads as a system error and buries the one line that
mattered.

When a person asked, answer the way an editor would: the worst problem first,
in plain language, with the before and after, and an offer to apply the fixes.
If the surface can render changes for approval, that is the answer; the machine
format stays under it.

```json
{
  "file": "docs/api/authentication.md",
  "line": 2,
  "severity": "critical",
  "rule": "position-5-20-no-clicks",
  "confidence": "measured",
  "evidence": {
    "window": "2026-07-01..2026-07-29",
    "query": "how to authenticate api requests",
    "position": 8.4,
    "impressions": 1840,
    "clicks": 11
  },
  "found": "Ranks at 8.4 for 'how to authenticate api requests' — 1,840 people saw this result and 11 clicked. The title shown to them is 'Authentication', which shares no words with what they typed.",
  "suggestion": "title: 'How to authenticate API requests | Product' (52 chars, matches the query the page already ranks for). The page is already visible; only the click is missing.",
  "action": "rewrite_title",
  "constraints": { "max_length": 60 }
}
```

## Related

- [From finding to change](../writing/from-finding-to-change.md) — what happens
  to a line of this report once someone accepts it.
- [Did it work?](./did-it-work.md) — the run that comes back and checks the
  effect line you promised.
- [Choosing a lens](./choosing-a-lens.md) — deciding which reading produces the
  findings in the first place.
- [Analytics](../../analytics/README.md) — where the numbers on the left-hand
  side of the translation table come from.
- [Evidence](../evidence/README.md) — the same measured-or-hypothesis
  distinction, graded across the whole handbook.
