---
title: "Demand gaps: finding the readers who never arrived"
description: "The audit that runs backwards from what the product can do, because a use case with no page has no traffic — and its absence looks exactly like success."
tldr: "Every other audit reasons about readers who came. This one starts from what the product can do, derives who could want that, and then asks the docs to account for each one — because a use case with no page has no impressions, no rank, no dead ends and no rage signals. The whole audit is hypothesis evidence, and a page measurably failing on real traffic outranks its best-scored opportunity every time."
---

# Demand gaps — the readers who never arrived

Every other audit reasons about readers who came: what they searched, where
they gave up, which page they bounced from. None of them can see the reader who
never arrived, because nothing on the site matched what they would have typed.
A use case with no page has no impressions, no rank, no dead ends and no rage
signals — it is invisible in every number the rest of an audit trusts, and
**its absence looks exactly like success.**

So this audit runs the other way round. It starts from **what the product can
do**, derives who could want that and why, and then asks the docs to account
for each one. Its output is not "this page is broken"; it is "this audience,
this job and this workflow have no page at all" — handed to whoever decides
which pages exist ([page set](../planning/page-set.md)), never written here.

The chain is fixed, and skipping a link is how audits produce feature lists
instead of demand:

> **Capability → Job → User → Workflow → Outcome → Market → Content**

## When is this audit worth running?

- **The docs are new, or the workspace has no history.** The measured readings
  have nothing to rank; this is the only honest input.
- **Everything measurable was already fixed and the numbers are still small.**
  Rewriting the same twelve pages harder does not create demand that no page
  addresses.
- **The product shipped capabilities the docs never framed as jobs.** Common
  after an API, an export, a webhook or an integration lands with one reference
  page and nothing else.
- **Not** as a substitute for a measured finding. A page failing on real
  traffic outranks the best-scored opportunity here, every time. When both are
  available, [choosing a lens](./choosing-a-lens.md) decides the order.

## Evidence tiers — the one thing that keeps this honest

This audit produces inference, and inference is how audits start inventing
products. Label every line with the tier it actually holds, and never present a
lower tier as a higher one:

| Tier | Means | Rule |
|---|---|---|
| `capability` | Read directly from the source — docs, README, API reference, changelog, pricing page | Cite where you read it |
| `inferred` | Follows from one or more capabilities, and from nothing else | Name the capabilities it rests on |
| `speculative` | A market or audience guess with no support in the source | Written as an open question, never as a plan |

The whole audit is `hypothesis` evidence in the labelling described under
[business translation](./business-translation.md). Say so once, up front. **A
capability the source did not show does not exist** — not in a use case, not in
a search cluster, and above all not in a page this audit asks someone to write.

## 1. Capability map — actions, not feature names

Extract what the product does, then translate every feature name into the
action it performs. A feature list is not a capability map, and it cannot be
turned into a job:

| Written as a feature | Written as a capability |
|---|---|
| API endpoint | Get the data programmatically, on your own schedule |
| Export | Move results into another system |
| Webhook | Start a process the moment something happens |

Record per capability: **action · inputs · outputs · limits · how often it is
used · what it depends on · what it connects to · technical level required**.
Limits and dependencies are not decoration — a capability gated behind a plan
the target audience will not buy is not an opportunity, and half the scoring
later turns on that line.

## 2. Jobs — what the capability lets someone finish

For each capability, write jobs in one shape:

> User has **[problem]** → uses **[capability]** → gets **[outcome]**.

Sweep all ten classes per capability rather than stopping at the obvious one.
The obvious job is usually the one the docs already cover, which makes it the
least valuable output here:

**Find** (people, companies, records, documents, events, signals) · **Analyse**
(compare, classify, score, diagnose) · **Monitor** (watch for change, alert,
detect, recur) · **Extract** (collect, export, enrich, transform, normalise) ·
**Automate** (remove a repeating manual step) · **Discover** (new objects,
trends, opportunities) · **Verify** (validate, audit, catch anomalies) ·
**Predict** (signals, intent, likely change) · **Build** (a tool, dashboard,
agent, pipeline or dataset on top) · **Operate** (run it as infrastructure
inside an existing process).

A class with no plausible job is a legitimate answer. Write "none" and move on;
padding all ten is how a coverage matrix fills with fiction.

The sweep is the method; reading a job properly — the forces on the person, the
language they use for it — is [jobs to be done](../lenses/jobs-to-be-done.md).

## 3. Hidden use cases — what combinations unlock

The jobs the docs already name are rarely where the growth is. Combine:

> Capability A + Capability B + audience C = candidate use case

*API + filtering + export*, for one product, is lead generation, research,
enrichment, dataset construction, monitoring and internal analytics — six use
cases, six audiences, six sets of search phrasings, and typically one reference
page serving all of them badly.

Per candidate record: the capabilities it rests on, **how obvious it is from
the docs today** (obvious / implied / invisible), who it serves, and the
outcome. Invisible ones with real capability support are the point of the whole
audit.

## 4. Audience map — four axes, not a job title

Cut the same product four ways; the same person appears on all four, and the
axis that changes the docs most is usually the technical one:

- **Role** — developer, engineer, founder, marketer, sales, recruiter, analyst,
  researcher, product manager, operations, agency, consultant, creator, data
  scientist, AI engineer, platform team.
- **Technical level** — non-technical, technical non-developer, developer,
  data/ML specialist, whole engineering team.
- **Organisation** — individual, startup, SMB, agency, enterprise, research
  body, media.
- **Context** — internal tool, customer-facing product, research, automation,
  analytics, infrastructure, experimentation.

Per audience: the job they want done, why this product rather than nothing,
which capabilities they actually need, the result they walk away with. An
audience the source addresses nowhere and no capability serves is
`speculative` — record it as an open question, not as an audience. Writing for
the one you keep is [know the reader](../planning/know-the-reader.md).

## 5. Business outcomes — what the product does versus why anyone pays

Translate every capability into a result someone would defend in a budget
conversation: time saved · cost removed · manual work removed · revenue ·
conversion · leads · retention · risk reduced · research accelerated · better
decisions · automation · wider coverage · faster detection of change · data
that did not exist before · a new product made possible · better customer
experience.

The gap between the two columns is the finding. Docs that only ever answer
*what it does* leave the buyer to derive *why it is worth paying for*, and most
of them do not bother.

## 6. Workflows — the whole run, not a single call

A capability is a step; people buy the finished sequence.

> Trigger → Action → Processing → Output → Business result

*New event → collect the data → enrich it → classify it → push it to the CRM →
sales acts on it.* Mark which workflows the docs already describe end-to-end,
and which are assemblable from documented capabilities but written nowhere.
**The second list is usually the highest-value content in the entire audit:**
every step exists, and no page says they compose.

## 7. Integrations and ecosystem

Name the systems this product can sit inside: CRM · databases · spreadsheets ·
BI · chat · email · webhooks · automation platforms · warehouses · cloud
infrastructure · AI systems · agents · retrieval pipelines · internal tools ·
customer-facing apps.

**Never write a potential integration as an existing one.** An unbuilt
integration is recorded as *potential integration / ecosystem opportunity*, and
a page for it may only describe what is actually possible today with the
documented capabilities.

## 8. AI and automation surface

Ask one question of the whole product: **can it act as a data source, a tool,
an action, or an infrastructure layer for an AI system?** Then check each of:
agents · retrieval · model context · tool calling · structured output for
machine consumers · autonomous workflows · research · enrichment ·
classification · extraction · summarisation · monitoring agents ·
assistant-driven search.

Products with an API and structured output almost always have this surface and
almost never document it. It is also the one gap where the missing asset is
often not prose — a machine-readable descriptor, a tool definition, a worked
agent example. ([Agent-ready docs](../../agent-ready/mcp.md) is the surface
itself.) One caution when the proposed asset is a catalogue of capabilities:
a long list of named tools is not a set a calling model picks from. Measured on
Docsbook's own MCP call ledger on 2026-09-12, 1 of 136 action tools had ever
been called, and every call from outside the founding team landed on one of
five names — so the asset that closes this gap is usually a worked route into
the few capabilities that matter, not an exhaustive index of all of them.

## 9. Intent — the same use case at six depths

One use case needs different pages at different depths. Tag each:
**problem-aware** (they have the pain, not the vocabulary) · **solution-aware**
(they know the category) · **product-aware** (they are looking at products) ·
**technical** (API, SDK, implementation) · **commercial** (price, limits,
comparison) · **learning** (how to do it at all).

Most docs sites cover technical intent thoroughly and everything above it not
at all, then wonder why nobody arrives before the evaluation stage. Matching a
page to the depth it serves is [search intent](../lenses/search-intent.md).

## 10. Search clusters — how the job gets typed

Per use case, write the phrasings a reader would actually use. Not the product
name — someone who knows the product name is already found. Group into:
**category** · **problem** · **job** · **tool** · **alternative** ·
**integration** · **tutorial** · **comparison** · **API/developer** ·
**industry** · **persona**.

These are candidate phrasings, not volumes. **Never attach a number to one.**
If real search data exists in the same run, cross-check the clusters against
it: a cluster the product already ranks for is a page to sharpen, not a page to
write, and it demotes straight into the ordinary striking-distance work
described in [external checks](./external-checks.md).

## 11. Coverage matrix

One row per dimension, one mark per row, and a page reference for anything
marked covered. Unreferenced "covered" is the failure mode this table exists to
prevent:

| Dimension | Covered | Partial | Missing |
|---|---|---|---|
| Core capabilities | | | |
| Basic use cases | | | |
| Advanced use cases | | | |
| User personas | | | |
| Business outcomes | | | |
| Workflows | | | |
| Integrations | | | |
| Automation | | | |
| AI use cases | | | |
| Industry use cases | | | |
| Tutorials | | | |
| Examples | | | |
| Troubleshooting | | | |
| Comparisons | | | |
| Migration | | | |

## 12. Gaps — a named asset, never "more content"

"Needs more content" is not a finding anyone can act on. Every gap names **one
asset type** and **the reader question it closes**: tutorial · use-case page ·
integration guide · industry page · persona page · API example · workflow guide
· comparison page · migration guide · case study · benchmark · template ·
dataset · interactive tool · FAQ entry · troubleshooting article.

> Missing: integration guide, *"how do I get this into our warehouse
> nightly?"* — rests on the export and scheduling capabilities; no page
> composes them.

## 13. Adjacent markets

Check whether the same capabilities serve a category the product never
addressed: sales · marketing · recruiting · research · finance · security ·
operations · support · product · analytics · data · AI · media · education ·
agencies · consulting.

Write every one as **potential market based on available capabilities**,
`speculative` tier, with the capabilities named. A market claim that outruns
the product ends up on a landing page, and then in a sales call. Deciding which
of them is worth serving — and what it costs in translation and maintenance —
is [market expansion](../lenses/market-expansion.md).

## 14. Priority

Score each use case 1–5 on four axes and multiply:

> **Opportunity Score = Demand × Product fit × Commercial value × Content
> opportunity**

- **Demand** — how likely it is that people are already looking for this.
- **Product fit** — how well today's capabilities actually finish the job.
- **Commercial value** — how much the outcome is worth to whoever gets it.
- **Content opportunity** — how much a page would unlock that nothing currently
  does.

The multiplication is the point: any single 1 collapses the score, which is
correct. High demand on a job the product half-does produces a page that draws
readers and disappoints them, and that is worse than no page. Two guards on the
arithmetic:

- **Product fit is scored from the capability map, never from ambition.** It is
  the axis that keeps this audit from commissioning documentation for features
  that do not exist.
- **A score is a sort order, not a forecast.** It ranks hypotheses against each
  other. It never outranks a page that is measurably failing on real traffic,
  and it never gets reported as if it were measured.

Cut to what a week holds, like every other queue: five items is a plan, twenty
is a backlog dump. Everything below the cut is one line with a count.

## 15. What the report contains

Report in this order, worst gap first, `hypothesis` labelled throughout:

**A.** Capability map · **B.** Use cases the docs already make explicit ·
**C.** Hidden use cases · **D.** Audience map · **E.** Jobs to be done ·
**F.** Business outcomes · **G.** Workflow opportunities · **H.** AI and
automation opportunities · **I.** Content gaps · **J.** Search and discovery
opportunities · **K.** Priority queue — 10–20 opportunities, each with
audience, problem, solution, outcome, the capabilities it rests on, the named
content asset, and its score.

Then hand the queue over. This audit writes nothing.

## Traps

- **Never invent a capability.** Every job, workflow, market and proposed page
  traces to something read in the source. This is the single rule the whole
  audit stands on.
- **Never present a potential integration, market or audience as an existing
  one**, in the report or in any page it produces.
- **Never attach a number to a search cluster.** These are phrasings, not
  volumes, and a fabricated volume is how a whole quarter gets spent on the
  wrong cluster.
- **Never let an opportunity score outrank a measured failure.** Real traffic
  beats reasoning about traffic.
- **Never write the pages here.** Gaps go to whoever owns the page set, with
  the evidence attached; this audit stays an audit.
- **Do not score product fit on a capability the target audience cannot
  reach** — plan gating, a required technical level, a regional limit. A
  blocked capability is fit 1, not fit 5.
- **Do not fill the coverage matrix to look thorough.** "Missing" is a finding;
  a padded "covered" row hides one.

## Before you hand the queue over

- The whole audit is labelled `hypothesis` once, up front, and every line
  carries `capability` / `inferred` / `speculative`.
- Every capability is written as an action with inputs, outputs and limits — no
  bare feature names.
- All ten job classes were swept per capability; empty classes recorded as
  empty rather than padded.
- Hidden use cases name the capabilities they rest on and how visible they are
  in today's docs.
- Audiences cut on all four axes; any audience with no capability behind it
  marked `speculative`.
- At least one workflow assemblable from documented capabilities but described
  nowhere is identified, or its absence is stated.
- The AI and automation question is answered explicitly, one way or the other.
- Search clusters carry no numbers, and any cluster the product already ranks
  for is demoted to existing-page work.
- The coverage matrix is complete, with a page reference behind every
  "covered".
- Every gap names one asset type and the reader question it closes.
- The priority queue is scored on all four axes, cut to five actionable items,
  and handed over unwritten.

## Related

- [Jobs to be done](../lenses/jobs-to-be-done.md) — reading a job properly once
  the sweep has named it.
- [Market expansion](../lenses/market-expansion.md) — what to do with an
  adjacent market you decide to serve.
- [Search intent](../lenses/search-intent.md) — matching a page to the depth of
  the question that reaches it.
- [Page set](../planning/page-set.md) — where the priority queue goes, and how
  a gap becomes a commissioned page.
- [Choosing a lens](./choosing-a-lens.md) — when demand gaps outrank a measured
  reading, and when they do not.
