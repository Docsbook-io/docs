---
title: "Reading documentation numbers without being confidently wrong"
description: "The window, the sample floors, the confounders and the honesty tiers that decide whether a documentation number means anything before you act on it."
tldr: "Pick one window and use it for every signal in the run. Report absolute counts beside every rate, and withhold the rate below the sample floor rather than inventing one. Most wrong documentation plans are not built on wrong numbers — they are built on real numbers read without their confounder, their denominator or their date."
---

# Reading the numbers

An audit that starts by reading pages produces a list of opinions. An audit that starts from what already happened — what readers searched for, where they gave up, which page a search engine already shows and nobody clicks — produces a shortlist you can rank. The numbers say **where** to look. They do not say what is wrong there; [the content detectors](./content-detectors.md) and [the behavioural readings](./behaviour.md) do that.

The failure this page exists to prevent is not arithmetic. It is a real number, correctly retrieved, quoted without the one fact that changes what it means — the window it came from, the size of the sample under it, the bots in it, or the definition that has since been changed. That produces a confident, expensive, wrong plan, and everyone in the room believes it because there is a number on the slide.

Read your platform's own definitions before quoting any figure from it. In Docsbook, [how measurement works](../../analytics/how-measurement-works.md) is that page: what a visitor is, how bots are excluded twice, where read time is clipped, and which percentages are suppressed rather than shown. Every number below inherits those definitions.

## What do you establish first, and in what order?

Four bodies of evidence, in this order, taking whichever are available:

1. **Search performance** — position, impressions, clicks, and the queries each page ranks for. Specifically: the pages sitting at positions 5 to 20 with impressions and no clicks. That band is the cheapest growth in the whole analysis, and [the striking-distance reading](./behaviour.md#which-pages-are-already-close-to-winning) is how to work it.
2. **Answer-engine signals** — whether the structured-data layers are switched on at all, and whether assistant crawlers are reading pages whose most citable structure is being withheld. See [what the answer-engine layers actually do](#what-do-the-answer-engine-layers-actually-do) below.
3. **Reader behaviour** — the outcome mix of visits, the pages readers gave up on, the routes they walked, the searches that returned nothing, the searches that returned results and got no click, and the questions the assistant could not answer.
4. **Conversion** — the goals the owner declared, and how the ordered route through them holds up step by step. This is the only signal in a run that measures the documentation against the owner's *own* stated intent, and the only one whose numbers can be wrong because a definition is wrong rather than because readers changed. [Goals and funnels](./goals-and-funnels.md) covers the checks that decide whether a goal number is about readers at all. Where nothing is declared, that is the finding: report it once, without an upsell, and read the routes readers actually walked instead.

Two scope limits apply before any of this. Search-performance analysis only applies to **public** pages — a private or internal documentation set has no impressions to read, and its absence of search data is not a finding. And every signal above is read, never written: nothing in this pass changes a page, a goal or a setting.

The output of this pass is a shortlist of pages or sections ranked by **readers affected**, each carrying the raw counts behind it and the signal that put it there — not a dashboard.

**If there is no history to rank** — a new site, a workspace connected last week, traffic below the floors in the table below — say so plainly and go to the demand-side reading instead of producing a ranked list out of nothing. [Demand gaps](./demand-gaps.md) is the pass that works forward from what the product can do, because a use case the documentation never addresses has no page, and therefore no impressions, no dead ends and no failing rank. Its absence is indistinguishable from success in every signal above. An audit built on four visits is worse than an audit that admits it has none.

## One window, stated once

Pick one period — 24 hours, 7 days, 30 days — and use it for every signal in the run. Seven days is the default for a weekly plan. Twenty-four hours is for checking a release and is almost always too thin to rank on. Mixing windows across sources invents trends that were never there: a 30-day search figure sitting next to a 7-day behaviour figure produces a "collapse" that is an artefact of the arithmetic.

Print the window and the total volume behind it as the first line of the report.

## Why is search data always older than it looks?

Search-performance data trails roughly two days behind and refreshes at most once a day. Whatever you are reading describes last week, not today.

- **Date every window *and* its as-of date.** "Positions for 4–31 July, as of 30 July" is a statement someone can check. "Our average position is 9" is not.
- **Never answer "how are we ranking today"** with anything but the most recent complete window plus its end date.
- **Do not force a refresh more than once a day.** The upstream source updates daily; a second pull returns the same numbers at extra cost.
- **If a page changed inside the window, say so.** You are judging the previous version of it.

## Sample floors: below which a percentage is a lie

A rate computed over a handful of events is not a small finding, it is a wrong one. Below the floor, report the absolute count and withhold the percentage.

| Signal | Floor | Below it |
|---|---|---|
| Any behavioural rate | ~30 visits | Report the absolute count; the percentage is withheld and must never be invented |
| A page's average position | Meaningful impressions | Report the impression count next to every position; never rank a queue on a position built from a handful |
| A rejected-search cluster | 2 separate visits | An observation, not a finding — do not rewrite anything for it |
| A buying-stage characterisation | 5 conversations | Quote the raw text as anecdote and say the volume does not support a conclusion |
| A blocker pattern | 3 independent conversations | As above |
| A competitor mention | 2 mentions | Log it; do not strategise against it |
| A call-to-action click-through | ~200 impressions | Statistical noise |
| A dwell percentile | ~30 pageviews | Noisy — exclude it and report the exclusion |
| A route or journey pattern | ~50 sessions | Not reportable |
| A question cluster | 5 questions | Too small; drop it and say so |

State the floor you used, and list what it excluded as a count. **Pages dropped silently read as pages that were fine.**

Two rules travel with the floors and apply above them as well. Every rate carries its absolute counts beside it. And every funnel rate carries the share of traffic that entered step one — a funnel is a hypothesis about a path most readers are not on, and a completion rate quoted without its coverage reads as a fact about the whole site.

## The confounders that bite hardest

- **Traffic is context, never a verdict.** Crawlers can be the overwhelming majority of raw pageviews, and behavioural metrics exclude bots while pageview counts do not. Use traffic to weight a queue, never to decide whether a page is healthy — and never put a pageview total next to a behavioural rate as if the two reconcile.
- **A high exit rate is not a problem on its own.** A page readers leave from *after succeeding* is a terminal success page. Recommending its rewrite makes the documentation worse. Always read exits next to the outcome mix, and never re-apply an exit penalty that a health score has already exempted.
- **One health score, two different jobs.** A composite score folds "readers gave up here" and "readers stayed and disliked it" into one number. Two pages at 45 need opposite work. Open the components and name the dominant signal, or flag the item as undecomposable and make its action a diagnostic rather than a rewrite. Never rank a queue on a composite score alone.
- **On-site search click-through and the search engine's click-through are different numbers.** One is readers using the search box inside the documentation; the other is the result page of a search engine. The fixes differ completely. Never quote one as the other.
- **Position is an average across everyone who searched**, mixing countries, devices and query variants. An average of 7 can be a steady 7, or a 3 and a 15 that need opposite fixes. Break the average down by query before recommending anything. And never verify a position by searching for it yourself — your own result is personalised and proves nothing.
- **Impressions are counted per query**, so one page appears many times. Sum per page before comparing pages, or a page ranking for twenty long-tail variants looks smaller than a page ranking for one. Never present impressions as an audience size.
- **A non-click is not automatically a failure.** A reader who got the answer out of the snippet leaves happy. For short factual queries — a default value, a port number, a limit — check whether the snippet already answered before proposing a title rewrite.
- **Zero results and zero clicks are opposite diagnoses.** Nothing returned means content is missing. Results returned and refused means content exists and does not look like the answer. Conflating them is the most expensive mistake available here.
- **Visitors are hashed identifiers.** Shared networks merge readers; mobile networks split them. Report direction of travel, never headcounts.
- **A buying stage is a classification, not a fact.** It is inferred from wording; nobody's billing record was consulted. Report it as what the reader was asking about — never as confirmed intent, never as pipeline.
- **Stage mix reflects who visits.** Documentation linked from an in-app help menu reads as support-heavy however well it sells. Establish where traffic enters before blaming the content.
- **An absent signal is not a clean bill.** No pricing conversations in a product that charges money means readers stopped asking, not that pricing is clear.

## Why is a before-and-after not evidence?

Documentation traffic moves for reasons that have nothing to do with you: a release, a conference, a seasonal cycle, someone else's blog post, a search engine's own update. A page you edited and a period in which the number rose are two facts, not a causal chain.

The comparison that carries weight is **edited pages against untouched pages, across both windows** — a control set inside your own corpus, moving under the same weather. Without one, the honest verdict is "cannot tell", and "cannot tell" is a real verdict rather than a soft failure. [Did it work?](./did-it-work.md) is the full method, including the four verdicts a comparison may return.

This is also why a baseline is written down **at the time of the change**, not reconstructed afterwards. Search effects take weeks; by the time anyone asks whether the rewrite worked, the numbers from before it are the only thing that could have settled the question, and nobody wrote them down.

## Degrading honestly: what you can produce with what you have

Say the availability gap **once, at the top**, in a sentence the reader can act on. Never sprinkle upgrade prompts through the report: a finding interrupted three times by what you would know if they paid you more is a finding nobody finishes reading.

| What you have | What you can produce | What to say |
|---|---|---|
| Search performance + per-page health + a ranked fix digest | The full queue: pages triaged by behaviour, cross-checked against concrete fixes that already carry impact estimates | Nothing missing. Name the period. |
| Per-page health only | A ranked page queue with **your own** impact reasoning: score × traffic, components separated, effort estimated by hand | Say the impact estimates are yours. The workspace's own ranked digest — which names specific unanswered questions and zero-result searches with impact already computed — would replace those estimates with measured ones, and add the *what to write* items this queue cannot see. |
| Search performance only, no behavioural data | A ranked rewrite queue for the striking-distance band, and a text-quality audit | Name what reader behaviour would have added: which pages people give up on, and whether the fix is the page or its title. |
| Neither | **Do not fabricate a queue.** A text-quality audit over the documentation, unranked, with every intent-related finding labelled a hypothesis | Say plainly that ranking by what readers actually did needs behavioural data this workspace does not collect; then say what that would give — a five-line weekly queue ordered by readers affected, each naming the fix and its expected effect — and what you can do today. |

In the bottom tier, keep facts and hypotheses visibly separated. "This title is 74 characters" is a fact. "This title is a label, not a search intent" is a hypothesis. A reader who cannot tell which is which discounts both. Where you need the primary keyword for a page and have no data for it, ask the owner and mark their answer as theirs.

**Never fabricate a position, an impression count or a query to fill a gap.** An invented number in a documentation report means somebody rewrites the wrong page, and the rewrite is measured against the invention.

## What do the answer-engine layers actually do?

Some platforms generate structured data behind opt-in switches that default to off. When they are off, a page still ships basic markup, but the most citable structure is withheld — and auditing frontmatter without checking the switches misses the biggest lever on the page.

| Layer | What it adds when on | Why it matters |
|---|---|---|
| Indexing | Base indexing signals, sitemap inclusion, meta reinforcement | Gets the page into the index at all |
| Authorship | A real person as author instead of the organisation | Engines weight authored content higher |
| Answer markup | Q&A and numbered procedures promoted into `FAQPage` / `HowTo` / speakable markup | Structured answers are the easiest thing on a page for an assistant to lift into an answer |

Rule of thumb: a site getting meaningful assistant-crawler traffic with the answer layer off is often the top finding of a whole run. But the switch and the content go together — enabling it over prose with no genuine question-and-answer or procedure in it produces nothing at best and invalid markup at worst. Flag the switch **and** check that the content supports it.

### What the markup layer does not buy

Two published positions bound what you may promise here, and both are worth carrying because the market sells the opposite.

- Google states that "There are no additional requirements to appear in AI Overviews or AI Mode, nor other special optimizations necessary", and that "You don't need to create new machine readable files, AI text files, or markup to appear in these features" ([Google Search Central, AI features and your website](https://developers.google.com/search/docs/appearance/ai-features)). Eligibility is the ordinary rule: the page is indexed, and a snippet is allowed.
- The FAQ rich result specifically is gone. Google narrowed it in August 2023 to well-known, authoritative government and health sites, and removed it from Search in May 2026 ([Google Search Central, FAQ structured data](https://developers.google.com/search/docs/appearance/structured-data/faqpage)).

So switch the answer layer on where the page genuinely carries questions and answers or a numbered procedure, because a self-contained, clearly delimited answer is the easiest unit to lift. Do not book a ranking, a rich result or a citation rate against it. [GEO](../../geo/README.md) and [AI search](../lenses/geo-ai-search.md) go into what is and is not established about being quoted.

## Related

<!-- widget:cards plain cols=2 -->

- [Choosing a lens](./choosing-a-lens.md) — which readings this evidence actually supports, and which to skip loudly {compass}
- [Behavioural readings](./behaviour.md) — dead ends, routes, rejected searches, the striking-distance band {search}
- [Content detectors](./content-detectors.md) — what is wrong with a page once a number has pointed at it {file-text}
- [Goals and funnels](./goals-and-funnels.md) — the declared signal, and the four checks before quoting it {target}
- [Saying it in business terms](./business-translation.md) — which conversions are honest, and the ones to refuse {scale}
- [How measurement works](../../analytics/how-measurement-works.md) — the definitions every figure above inherits {gauge}
- [Analytics](../../analytics/README.md) — the reports these numbers come from {bar-chart-3}

<!-- /widget -->
