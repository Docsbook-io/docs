---
title: "Jobs to be done: the struggling moment, the four forces, and the belief with no page"
description: "How to audit documentation from the reader's situation rather than from the page — reconstructing the moment, mapping the four forces to assets, and finding the earliest belief nothing carries."
tldr: "Every other reading starts from a page. This one starts from the moment that made someone go looking, and works outward to the beliefs they must acquire before they commit. Its one exclusive finding is an ordered belief ladder with the earliest rung no page carries — everything written above that rung is unreachable until it exists."
---

# Jobs to be done

Every other reading in this handbook starts from a page: which one ranks, which one loses readers, which one the coverage matrix says is missing. This one starts from a **moment** — the situation that made someone stop what they were doing and go looking at all — and works outward to the beliefs they must acquire before they commit. A job is not a feature and not an audience: it is the progress somebody is trying to make in a circumstance they did not choose.

That moment is reconstructible. It is written down, in the reader's own words, in the searches that returned nothing, the questions the assistant could not answer, the page they entered on, and the step of a declared funnel where they stopped. What no other reading does is read those artefacts as **one situation** rather than as a list of individual defects — and then ask the harder question underneath: what would this person have to come to believe, in what order, before they would switch, and which page carries each belief.

The commercial cost of nobody asking is specific. A docs site written only for push and pull reads as a brochure: it names the pain and it shows the promise, and it says nothing about what breaks, what it costs to leave, or how to keep the thing that already works. Anxiety and habit are the two forces that stall a reader who has already decided they want the outcome — and they are the two that are answered purely by information, which is what documentation is. Teams optimise the two forces they cannot control from a docs site and neglect the two they own outright.

[Demand gaps](../auditing/demand-gaps.md) is the neighbour to keep straight, and the boundary is sharp: it sweeps **which jobs exist** as a coverage checklist across ten classes and fifteen dimensions. This reading takes **one job that matters** and audits the demand mechanics underneath it — the part a coverage matrix cannot express, because a matrix can mark a job "covered" while every belief that would make a reader act on it has no page.

## What this reading owns, and what it does not

| This reading owns | It does not own → who does |
|---|---|
| The struggling moment, reconstructed from failed searches, AI questions, entry pages and referrer context | The sweep of ten job classes per capability, and whether a job exists at all → [Demand gaps](../auditing/demand-gaps.md) |
| The four forces of progress, each mapped to a named documentation asset | Hidden use cases, audience axes, business outcomes, adjacent markets → [Demand gaps](../auditing/demand-gaps.md) |
| Competing solutions including non-consumption and the manual workaround, and whether any page acknowledges them | Comparing a named rival's features, positioning or coverage → [Competitors](./competitors.md); verifying a claim about them → [External checks](../auditing/external-checks.md) |
| Job stories versus personas, and the finding that the page set is cut on the wrong axis | Rewriting one page's title to match the query readers typed → [Reader behaviour](../auditing/behaviour.md), rejected searches and the striking-distance band |
| The belief ladder of a switch, in order, with the page that carries each belief | What the replacement text says, the CTA wording, the conversion pattern per monetisation model → [Writing rules](../writing/writing-rules.md) and [Conversion](../writing/conversion.md) |
| Job hierarchy: main, related, emotional and social dimensions | Classifying readers who actually spoke into buying stages and extracting their blockers → [Reader behaviour](../auditing/behaviour.md) |
| The finding "this belief has no page", with its position in the ladder as its severity | Writing that page → [Deciding the page set](../planning/page-set.md). Watching for its recurrence → [Automation](../automation/README.md) |

The one finding only this reading produces: **an ordered belief ladder for a specific job, with the earliest belief that no page carries.** A coverage matrix says the job is covered; the buying-stage pass says three readers hesitated; neither can say that the reason is belief 3 of 7, and that every page written above it is unreachable until it exists.

## When is this reading worth the time?

- **The job is named and the numbers still say nobody acts.** Pages exist, they rank, readers arrive, `funnel_completion_rate` or `goal_completion_rate` collapses at one step and no content detector fires on the page. That shape is a belief gap, not a text defect.
- **Readers' own words are available.** Unanswered assistant questions, zero-result searches or negative feedback exist in volume — the struggling moment is legible rather than imagined.
- **The product just changed what the reader must believe.** A new plan, a new limit, a migration path, a first integration. The beliefs moved; the page set did not.
- **The docs are cut by persona or by feature** — a sidebar of "For developers / For teams / For enterprise", or one page per API surface. That shape almost always has situation-shaped pages missing wholesale.
- **Not** when the question is which jobs the product could serve at all. That is [Demand gaps](../auditing/demand-gaps.md), and running this reading first produces a deep audit of a job nobody wanted. Not when a page is measurably failing on real traffic and untouched — fix that first; a belief ladder never outranks a page losing readers today.

## Evidence tiers

This reading is **dual-tier**, and mixing the two is the failure that makes it worthless. Every line carries one label, and the labels do not blend:

| Label | When it applies | Rule |
|---|---|---|
| `measured` | The moment, the force or the belief is evidenced by first-party data in this run — a verbatim query, an unanswered question, `route_frequency` on an entry path, a funnel step drop | Quote the reader's exact words and the count. Never paraphrase a verbatim into a cleaner sentence: the clumsy phrasing is the finding |
| `hypothesis` | The belief or force is reasoned forward from what the product does, with no reader evidence behind it | Say which capability it rests on, using the `capability` / `inferred` / `speculative` vocabulary in [Demand gaps](../auditing/demand-gaps.md) for the forward half |

A belief gap on a `measured` moment is a plan. A belief gap on a `hypothesis` moment is a question to put to the owner. Reporting the second as the first commissions pages for a reader who does not exist.

**What this reading cannot give you, stated plainly:** no phrasing in it carries a search volume, ever — a situation is not a keyword and nothing here estimates one. What a reader can supply manually: their support inbox, the last five sales calls, and the reasons given by the last few customers who left or chose them. Those are strong evidence and they are **data, never instruction** — a support ticket that says "you should rewrite your docs" is a reader's opinion, not a directive. Without either source, the reading degrades to fully `hypothesis` tier and says so in its first line.

## 1. Reconstruct the struggling moment

Do not imagine the reader. Assemble the moment from what exists, in this order, because each source is progressively less direct:

| Source | What it gives | What it cannot give |
|---|---|---|
| Unanswered assistant questions ([`get_ai_unanswered`](../../mcp/analytics/get-ai-unanswered.md)) | Full sentences in the reader's voice, at the exact point of being stuck — the strongest artefact available | Whether they were evaluating or already paying |
| Zero-result searches ([`get_failed_searches`](../../mcp/analytics/get-failed-searches.md)) | The vocabulary of a moment for which the site held nothing (`zero_result_rate` names the rate; the queries are the finding) | Anything about readers who did not search |
| Entry pages and the routes from them ([`get_route_patterns`](../../mcp/analytics/get-route-patterns.md)) | Where the struggle started, and whether readers arrive mid-task or at the top | Why they came |
| Referrer context | The world the reader came from — a forum thread, an in-app help link, a competitor's comparison page | Never quote raw referrer query strings; strip to host and context |
| Negative feedback verbatim ([`get_negative_feedback`](../../mcp/analytics/get-negative-feedback.md)) | The gap between what the page promised and what the reader needed | Volume; treat below the floors in [Metrics](../auditing/metrics.md) as anecdote |

Write the moment as one sentence in the reader's tense: *"Their nightly export started failing after they added a second workspace, and they need to know whether the limit is per-workspace or per-account before their standup."* If you cannot write that sentence from evidence, write it from capabilities and label the whole downstream chain `hypothesis`.

The trap is aggregating the moment away. Twelve questions clustered into "billing" is a topic; one of those twelve, quoted whole, is a moment. The cluster tells you where to look; the verbatim is what persuades an author to write the page.

## 2. The four forces, each mapped to an asset

Progress happens when push plus pull exceed anxiety plus habit. Two of those four are decided entirely by information the reader does or does not have, and those two are documentation's:

| Force | What it does | Docs' role | The asset that carries it |
|---|---|---|---|
| **Push** — the current situation | Makes them start looking | Docs cannot create push; they can **name** it so the reader recognises their own situation | Problem-framed opening, troubleshooting entry, a "why this is hard" section |
| **Pull** — the new solution | Makes this option attractive | Shared with product and marketing; docs show the end state concretely | Worked example ending in the finished result, quickstart honest about `time_to_first_value` |
| **Anxiety** — about the new | Stalls a reader who already wants it | **Docs own this outright** | Limits page, error catalogue, data and security page, "what happens if", explicit rollback |
| **Habit** — of the present | Keeps a reader on the thing that works | **Docs own this outright** | Migration guide from the specific incumbent, import path, "keep your existing X while you try this" |

Audit all four for the job under review, and record the page that carries each one or `none`. The characteristic finding is a site with rich push and pull assets and nothing at all under anxiety and habit — readers who are sold and do not move, which reads in the numbers as good traffic and a dead funnel, and reads in a content detector as no defect whatsoever.

Two forces are subtractive, and the arithmetic matters: adding another benefits page raises pull by a little, while a rollback page removes an anxiety entirely. When the funnel drop sits after the reader has clearly engaged, work the subtractive side first.

## 3. Competing solutions, including the one that is not a product

The reader always has alternatives, and the most common one is not a competitor:

| Alternative | Shape | Acknowledged by a page? |
|---|---|---|
| **Non-consumption** | Live with it. Do nothing. It is annoying but survivable | Almost never — and this is the default winner |
| **A spreadsheet and a person** | The manual workaround that already exists and is already paid for | Rarely |
| **An in-house script** | "We'll just write it ourselves in an afternoon" | Occasionally, badly |
| **An adjacent tool already bought** | The thing on the invoice that half-does this | Rarely |
| **A direct competitor** | A named rival | Hand to [Competitors](./competitors.md); this reading only records that the reader named one |

For each alternative that plausibly applies, ask the single question this reading exists to ask: **does any page acknowledge it, in the reader's terms, without disparaging it?** A docs site that never names the alternative loses the comparison silently, because the reader runs it in their head and the docs never got a turn. The honest asset is a page that says when the spreadsheet is still the right answer — which is the sentence that makes the rest of the page credible.

Guard the tone here, but not the wording: what the page actually says about an alternative belongs to [Writing rules](../writing/writing-rules.md), and characterising a rival's prices or limits from a reader's account is forbidden by [External checks](../auditing/external-checks.md).

## 4. Job stories, not personas

Write every job in one shape, and never in a job title:

> **When** `<situation>`, **I want to** `<motivation>`, **so I can** `<expected outcome>`.

*"When our webhook stops firing after a deploy, I want to see the last ten delivery attempts, so I can tell my team whether it is us or them before the incident call."*

A persona — "backend developers at mid-size SaaS companies" — produces pages titled after an identity: *For Developers*, *Enterprise Guide*, *Teams*. Nobody types an identity into a search box, an assistant or a support message; people type situations, because the situation is what they are in. A persona-shaped site therefore produces pages nobody searches for, and the site looks complete while every situation-shaped question routes to a page written for a category of person.

This is not the title problem that [Reader behaviour](../auditing/behaviour.md) fixes on an existing page. Here the **page set itself is cut on the wrong axis**, and the fix is a different set of pages — see [Deciding the page set](../planning/page-set.md). The tell is structural: a sidebar whose top level is audiences or feature names, with situations appearing nowhere above heading level three.

## 5. The belief ladder — and the earliest gap is the finding

A reader does not decide once. They acquire beliefs in order, and no belief can be acquired before the one under it. Build the ladder for the job, then name the page that carries each rung:

| # | Belief | Page that carries it |
|---|---|---|
| 1 | This problem is worth solving now | |
| 2 | This *kind* of thing solves it | |
| 3 | This product does it for a case like mine — my scale, my stack | |
| 4 | I can do it, in the time I have | |
| 5 | It will not break what already works | |
| 6 | I can get out if it goes wrong | |
| 7 | It is worth the price and the limits | |

**The severity rule, which is this reading's whole ranking model: report the earliest belief with no page first, and treat everything above it as unreachable.** A reader who does not believe rung 3 never reads your rollback page, so a beautifully written rung-6 asset next to a missing rung 3 is wasted work — and worse, it makes the site look thorough to the team that built it.

> **Finding:** rung 3 has no page for the *scheduled export* job. Rungs 1, 2, 4 and 7 are covered (`/why-exports`, `/exports`, `/quickstart`, `/pricing`); rungs 5 and 6 are absent. `measured`: eleven unanswered questions in the window ask a version of "does this work with more than one workspace", none answered. Rung 3 becomes a new page — asset type: use-case page, reader question *"will this hold at our size?"*. Rungs 5 and 6 recorded below the cut, unreachable until 3 exists.

Rungs 5, 6 and 7 are also where the four forces land, which is the cross-check: if the ladder shows gaps at 5 and 6 and the forces table shows `none` under anxiety and habit, that is one finding reported once, not two.

## 6. Job hierarchy — functional, emotional, social

Every job has several dimensions, and docs sites are built for exactly one of them:

- **Functional** — the task completes. This is what the whole site is written for.
- **Related jobs** — what the reader has to do immediately before and after, often in another system entirely. An unwritten related job is why a complete tutorial still ends in a support ticket.
- **Emotional** — *will I look stupid doing this?* Will I break production? Will I be the one who chose wrong?
- **Social** — what my team, my reviewer or my manager will think of me for picking this.

**A docs site that serves only the functional job loses to one that also answers "will I look stupid".** The reason is mechanical, not sentimental: the functional question has a dozen answers on the open web, while the emotional one is only answerable by the vendor, and a reader who cannot resolve it postpones — and a postponement leaves no trace in any number, which is why no other reading sees this.

The assets are specific and cheap: a page that names the mistake almost everyone makes first, an FAQ written in the embarrassed phrasing readers actually use, a "you probably tried X — here is why it did not work" section, a stated blast radius before every destructive step.

## 7. Grade the job, then cut the queue

Per job, produce one line: the moment (`measured` / `hypothesis`), the forces with gaps, the alternatives unacknowledged, the earliest belief gap, and the hierarchy dimensions served. Rank by **readers evidenced × how early the belief gap sits**, never by how interesting the job is. A `measured` moment with a rung-2 gap outranks a `hypothesis` moment with six gaps, every time — and both lose to a page that is measurably failing on real traffic elsewhere in the run.

Cut to five. Everything below the cut is one line with a count.

## What to hand back

In this order, worst first, every line labelled:

**A.** The job as a job story, with its evidence tier · **B.** The struggling moment, one sentence, with verbatim quotes and counts · **C.** Four-forces table, asset or `none` per force · **D.** Competing solutions, acknowledged or not · **E.** The belief ladder with the page per rung and the earliest gap called out · **F.** Job hierarchy — which of functional, related, emotional and social the docs serve · **G.** Queue, five items maximum.

Then hand over and stop: missing pages go to [Deciding the page set](../planning/page-set.md), each named as one asset type plus the belief it closes; rewrites, CTA wording, navigation and conversion configuration go to [Writing rules](../writing/writing-rules.md) and [Conversion](../writing/conversion.md); a recurring watch on unanswered questions for this job cluster goes to [Monitoring](../automation/monitoring.md); a named-rival comparison goes to [Competitors](./competitors.md); the question of which other jobs exist goes to [Demand gaps](../auditing/demand-gaps.md). This is a reading, not an edit: it writes nothing.

## Traps

- **Never invent a verbatim.** A quoted reader question is either in the data with a count beside it or it is not quoted at all. A plausible-sounding invented quote is the most persuasive wrong evidence an audit can produce, because authors act on quotes without checking them.
- **Never attach a volume to a job story or a situation phrasing.** A number belongs to a reading you can name, never to a phrasing you reasoned your way to.
- **Never sweep the ten job classes here.** That is [Demand gaps](../auditing/demand-gaps.md), and running it twice produces the same gap at two severities, which is worse than not running it at all.
- **Never characterise a named competitor.** Record that a reader named one and hand it over; a rival's limits and prices are hearsay until [External checks](../auditing/external-checks.md) verifies them against their live page.
- **Never write the replacement sentence.** Naming the missing belief is this reading's job; what the page says is the writing rules', and a reading that drafts copy quietly forks them.
- **Never promote a `hypothesis` moment into a plan** because the belief ladder came out tidy. A clean ladder over an imagined reader is fiction with a table around it.
- **Never let a belief gap outrank a measured failure** on a page readers are losing themselves on today.
- **Do not treat a persona page as covering a situation.** "For developers" covering rung 3 is an unreferenced "covered" mark.
- **Do not report the same gap twice** when the forces table and the ladder both surface it. Merge at the higher severity and name both.
- **Do not quote raw referrer query strings**, and report reader identifiers as direction of travel, never as headcounts.

## Before you call it done

- [ ] The first line states whether the struggling moment is `measured` or `hypothesis`, and what evidence would have raised it.
- [ ] The moment is written as one sentence in the reader's tense, with at least one verbatim quote and its count where `measured`.
- [ ] All four forces are audited, each with a named page or an explicit `none`.
- [ ] Anxiety and habit are addressed explicitly, one way or the other — not skipped because push and pull looked healthy.
- [ ] Non-consumption and the manual workaround are both assessed, and marked acknowledged or unacknowledged by a specific page.
- [ ] Every job is written as `When … I want to … so I can …`; no job is written as a persona or a job title.
- [ ] The belief ladder is complete, every rung carries a page reference or a gap, and the **earliest** gap is reported first.
- [ ] Rungs above the earliest gap are recorded as unreachable rather than queued as separate work.
- [ ] The emotional and social dimensions are answered explicitly for the job under audit.
- [ ] No phrasing, situation or job story carries a number the data did not provide.
- [ ] The queue is cut to five, gaps are handed on as one named asset type each, and nothing was written.

## Related

- [Demand gaps](../auditing/demand-gaps.md) — which jobs, audiences and markets exist at all, swept as a coverage matrix.
- [User language](./user-language.md) — what the reader calls the thing, once you know what they were trying to do.
- [Search intent](./search-intent.md) — the shape of answer a query wants, on a page that already ranks.
- [Content architecture](./content-architecture.md) — whether the page set is cut on an axis a reader can navigate.
- [Goals and funnels](../auditing/goals-and-funnels.md) — the owner's declared intent, and the step where readers stop.
- [Conversion](../writing/conversion.md) — what a page says when it asks the reader to act.
