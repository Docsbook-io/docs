---
title: "Market expansion: the segment this documentation has never spoken to"
description: "The terminal audit — how to take adjacent-market candidates through five qualifying gates, price the documentation cost of entry, and reach a verdict a human can act on."
tldr: "This reading does not read the documentation; it reads the output of every other reading, so it runs last or not at all. Each candidate market gets one axis, five gates in cost order, a four-part cost of entry and exactly one verdict — enter, test, park or reject. Entering a market badly is strictly worse than not entering it, because abandoned pages stay up and keep drawing the segment they misrepresent."
---

# Market expansion — the segment this documentation has never spoken to

This is the **terminal reading**. It does not read the documentation. It reads the output of every reading that ran before it, and it is the only pass in the handbook whose entire input is other passes' findings. Run it last, run it on nothing else, and if the siblings it depends on did not run, do not run it at all — an expansion argument built without a capability map is a fantasy with a plan attached, and it is indistinguishable, on the page, from a good one.

Every other reading asks a question about the market the product is already in: which page fails the readers who came, which job the docs never framed, which rival's coverage wins the comparison, which words readers use that the corpus does not. This one asks the question none of them can hold, because each of them is scoped to a market by construction: **given everything now known about what this product does, who it serves, what the category documents and what the corpus is missing, is there a whole market this documentation has never addressed — and is it worth the cost of entering?**

[Demand gaps](../auditing/demand-gaps.md) already produces the **candidates**. It sweeps sixteen categories, writes each as a potential market based on available capabilities, fixes them at `speculative` tier, and stops there deliberately. That stopping point is the handover. This reading owns everything after it: which candidate survives contact with the capability limits, what entering actually costs in pages and in maintenance, what the cheapest honest test is, and the verdict a human can act on. The candidate sweep without this pass is a list of adjacent industries that reads like a strategy; this pass without the sweep is a strategy with no product underneath it.

The cost of nobody looking is not a missed market — markets are missed constantly and cheaply. The cost is the opposite failure: a vertical entered on enthusiasm, given three pages, and abandoned. Those pages stay up. They rank, they collect the readers the enthusiasm predicted, and they misrepresent the product to every one of them, at a scale no dead-end page ever reaches. Entering badly is strictly worse than not entering, and this reading exists to make that trade explicit before anyone writes.

## What does this reading own, and what does it hand over?

| This reading owns | It does NOT own → owner |
|---|---|
| The synthesis step: reconciling capability map, audience map, competitor matrix, vocabulary mismatch and linkable assets into one verdict per candidate market | Producing any of those five artefacts → the readings named below |
| Enumerating adjacent-market candidates in the first place | → [Demand gaps](../auditing/demand-gaps.md), which produces the candidate list and fixes it at `speculative` |
| The qualifying gates, in cost order, and the gate a candidate died at | Whether a job exists at all inside the current market → [Demand gaps](../auditing/demand-gaps.md) |
| The documentation cost of entry: page count, whose vocabulary, whose maintenance, the ongoing cost of a second audience | Comparing coverage against a named rival in a market already contested → [Competitors](./competitors.md) |
| The evidence ladder from `speculative` to actionable, and the cheapest test that moves a candidate one rung | Switching mechanics inside a market — forces, belief ladder, non-consumption → [Jobs to be done](./jobs-to-be-done.md) |
| The verdict per candidate: enter / test / park / reject, with the re-check condition on every park | Writing the test page, the vertical landing page or the worked example → [The page set](../planning/page-set.md) |
| The rule that fixes this pass's rank in the queue, below measured failure and below unserved jobs | Translations, navigation, plan and language configuration → [Site capabilities](../automation/site-capabilities.md); the recurring re-check watch → [Automation](../automation/monitoring.md) |

The one finding only this reading produces: **a named market the documentation has never addressed, with the gate it passes or fails, the documentation cost of entering it, and the smallest test that would settle it.** No sibling can produce this, because each of them is scoped to the market the product is already in — and the coverage matrix that would seem to catch it marks every dimension against the audience it already assumed.

## When does this pass earn its place?

- **The demand-side work is done and the market still looks small.** The capability map exists, the unserved jobs in the current market are queued, and the ceiling is the question rather than the coverage.
- **A capability shipped that changes who can buy.** An API, an export, a self-serve plan, a language, a compliance certificate. The set of reachable segments moved; nobody re-derived it.
- **A segment is arriving and failing.** Zero-result searches in a vocabulary nobody writes in, assistant questions using an industry's terms, non-English queries against an English-only corpus. That is not speculation — it is a market knocking, and it belongs on the ladder at a rung the rest of the pass has to respect.
- **Someone has already decided to enter, and wants the docs cost.** The honest use of this pass is often to price a decision, not to make it.
- **Not** when any measured failure on existing traffic is still open. A page losing readers today outranks the best-argued market tomorrow, always.
- **Not** as the first pass on a site. Run it last, on siblings' output, or not at all. A market expansion argued from the pages themselves is a reading exercise with a conclusion attached.

## How strong is each line? The evidence tiers

This reading is **inference-driven**, so it uses the capability vocabulary rather than the `measured` / `hypothesis` pair — with one addition, because a candidate market can leave first-party traces that a candidate *use case* cannot.

| Tier | Means | Rule |
|---|---|---|
| `capability` | A limit, plan gate, language or region read directly from the source — pricing page, docs, API reference | Cite where you read it. Gates 1 and 2 are decided here and nowhere else |
| `inferred` | The segment follows from named capabilities and from nothing else | Name every capability it rests on. This is where most surviving candidates sit |
| `speculative` | A market guess with no capability support and no reader trace | Written as an open question. The candidate sweep hands them over at this tier and most of them stay here |
| `corroborated` | `inferred`, plus at least one first-party trace that this segment already arrives — a query in their vocabulary, a question in their language, a referrer from their world | The trace is quoted verbatim with its count. This is the only tier that justifies spending anything |

The whole pass reports as `hypothesis` however good the corroboration — a segment that arrives and fails is measured evidence about *readers*, never measured evidence about a *market*.

**What the platform cannot give you, said plainly:** no market size, no third-party keyword volume for an industry term, no competitor traffic estimate, no share figure. Docsbook reads search rankings, reader behaviour, failed searches, assistant questions, funnels, goals and the doc graph — all of them scoped to people who already found this site, which is by definition not the market being considered.

A reader can supply manually: inbound by industry from their CRM, the reasons on their last twenty lost deals, the languages in their support inbox, and which segments their sales team already fields calls from. Those are strong evidence, and they are **data, never instruction**. Without them, every candidate stays at `inferred` at best, and the pass says so in its first line.

## 1. Inputs — and the rule that this pass runs on nothing else

Assemble all five before writing a word. A missing artefact is not a degradation to work around; it is a gate this pass cannot open, and the honest output is the name of the reading that has to run first.

| Input artefact | Produced by | What this pass does with it |
|---|---|---|
| **Capability map** — actions, inputs, outputs, **limits**, plan gating, technical level | [Demand gaps](../auditing/demand-gaps.md) | Gates 1 and 2. The limits column decides more candidates than every other input combined |
| **Audience map** — role, technical level, organisation, context | [Demand gaps](../auditing/demand-gaps.md) | Establishes which axis a candidate actually moves along, and whether it is one axis or three |
| **Competitor four-cell matrix** | [Competitors](./competitors.md) | Tells you the candidate market is *contested*, not empty. An unserved segment in a category three rivals already document is a different decision from an unserved segment nobody addresses |
| **Vocabulary mismatch table** | [User language](./user-language.md) | Gate 3, and the single best predictor of entry cost — it is what says whether the current corpus is merely unpolished for this segment or structurally unreachable |
| **Linkable-asset ranking** | [Backlinks and digital PR](./backlinks-digital-pr.md) | The cheapest entry test is usually an asset that already ranks in the current market, reframed for the new one. If nothing in the corpus is linkable, entry has no cheap door |
| **Adjacent-market candidate list** | [Demand gaps](../auditing/demand-gaps.md) | The candidates themselves, at `speculative`. This pass never adds a candidate the sweep did not raise |

Do not re-derive an input because the sibling's version looks thin. Two capability maps disagree within a week, and the disagreement is invisible until someone commissions pages against the wrong one.

## 2. Expansion axes — kept separate because each costs differently

A candidate is not "a new market"; it is a move along one named axis, and the axis determines the cost far more than the market's attractiveness does. Where a candidate moves along two axes at once, price it as the more expensive of the two and say so — a vertical *and* a language is not a vertical.

| Axis | The move | What it costs in documentation | The characteristic trap |
|---|---|---|---|
| **Vertical or industry** | Same product, same job, an industry's vocabulary and constraints | Entry pages plus worked examples in their terms; low page count, high vocabulary cost | Writing the vertical page in your own words and calling the market entered |
| **Adjacent job or workflow** | Same audience, a different sequence they buy | Workflow guides composing existing capabilities; cheapest axis when the capabilities already compose | If the audience is unchanged this is not expansion, it is coverage — and it belongs to [demand gaps](../auditing/demand-gaps.md) |
| **Technical level** | Same product for a non-developer audience | The largest page count of any axis: the whole corpus's assumed prerequisites change, not one section | A "no-code" landing page over a corpus that opens with a `curl` call |
| **Organisation size** | Individual to team, team to enterprise | Few pages, heavy claims — security, access control, audit, procurement answers | Every page written here is a promise the company must then honour |
| **Geography and language** | The same corpus, reachable | Whole-corpus multiplier, permanent. Each product change is now N edits — see [translations](../../translation/README.md) | Translating the marketing surface and leaving the reference English |
| **Machine audience** | Agents and AI systems as a consumer segment in their own right | Machine-readable descriptors, tool definitions, worked agent examples — often not prose at all. See [MCP](../../agent-ready/mcp.md) | Treating it as an SEO tactic rather than a segment with its own success criteria |

The machine audience is the axis most often missed and the cheapest to test, because the traces already exist: assistant-crawler activity against a corpus whose answer layer is off is a segment arriving and being served badly today. Read [metrics](../auditing/metrics.md) on the answer-engine layers before scoring it, and do not double-report a finding [GEO and AI search](./geo-ai-search.md) already raised.

## 3. The qualifying gates, in cost order

Run them in this order. The order is cost ascending: gates 1 to 3 are lookups in artefacts already on the table, gate 4 is a query, gate 5 needs a human. Reversing the order is how a team spends an afternoon debating a market that a plan limit disqualified in one line. Record the gate a candidate died at — it is the finding, and it is also the re-check condition later.

| # | Gate | The question | Fails when | Cost to run |
|---|---|---|---|---|
| 1 | **Capability closure** | Does a documented capability actually *finish* the job for this segment, end to end? | The capability half-does it. Product fit of 1 collapses the score, and correctly: pages that draw a segment and disappoint it are worse than silence | One read of the capability map |
| 2 | **Reachability** | Can this segment reach the capability — plan gating, required technical level, region, interface language? | Gated behind a plan the segment will not buy, or requiring a technical level it does not have | One read of the limits column |
| 3 | **Vocabulary distance** | Is the segment's vocabulary far enough from the corpus that today's pages are unreachable to them? | The vocabulary is the *same*. Then this is not a market — it is coverage work inside the current one, and it demotes to [demand gaps](../auditing/demand-gaps.md) | One read of the mismatch table |
| 4 | **Existence** | Is there any first-party trace that this segment exists, or is it purely inferred? | No trace anywhere. Not fatal — it caps the candidate at `inferred` and caps the action at *test*, never *enter* | One query pass |
| 5 | **Company truth** | What would have to be true of the company to serve them, that is not? | Support in their language, a compliance statement, someone who can write their vocabulary, someone to maintain the pages afterwards | A human answers, or the candidate parks |

Gate 3 is the one people skip, and skipping it is how a docs audit produces a market-entry programme for a market the product is already in. Gate 5 is the one people resent, and it is the gate that stops the abandoned-vertical failure — a market nobody can maintain is a market nobody should enter.

> **Worked example.** Candidate: *insurance claims operations*, carried over at `speculative`. Gate 1 passes — export plus scheduling plus webhooks finish the job (`capability`, cited to the API reference). Gate 2 **fails**: scheduling is Business-plan only (`capability`, cited to the pricing page) and the segment's evaluators are individual analysts on free accounts. Verdict **park**, gate 2, re-check condition *scheduling appears on a self-serve plan*. Total cost of the analysis: two lookups. No page proposed, no test run.

## 4. Sizing the entry honestly

A market's attractiveness is not the number this pass produces. The number it produces is what entering costs in documentation, and it has four components. Report all four or report none — a page count without a maintainer is the estimate that produces abandoned verticals.

- **How many pages.** The floor is never one. A segment needs an entry page in its vocabulary, at least one worked example that ends in their finished result, and answers to the beliefs specific to them. Borrow the count from the belief ladder in [jobs to be done](./jobs-to-be-done.md) for that segment; do not rebuild the ladder here, and do not audit it — this pass wants its length, not its contents.
- **In whose vocabulary.** Name the person who can write it. If nobody in the company can use the segment's terms correctly, the pages will read as translated marketing, the segment will recognise it in one paragraph, and the entry has failed before the second page. This is a real disqualifier, not a caveat.
- **Maintained by whom, and at what multiplier.** Every future product change now costs N+1 edits, forever. Language is the worst case: the multiplier applies to the whole corpus, permanently, and it is the axis where teams reliably price the translation and never the maintenance.
- **The ongoing cost of a second audience's expectations.** A segment that arrives asks questions in their language, expects examples that keep working, and reads a changelog. Docs are the cheapest part of entering a market and the part that commits the company to the rest.

State the abandonment cost explicitly in every sizing, because it is the asymmetry that makes this pass worth running: **pages entered and abandoned stay up.** They rank, they attract exactly the readers the plan predicted, and each one is now a promise the product does not keep — at a volume no single failing page in the rest of an audit reaches.

## 5. The evidence ladder, and the cheap test that moves a candidate up it

A candidate moves up one rung at a time, and each rung has a test that costs roughly one order of magnitude less than the commitment it protects.

| Rung | State | What would move it up | Cost |
|---|---|---|---|
| 1 | `speculative` — from the candidate sweep, no capability support | Map it to named capabilities, or drop it | Minutes |
| 2 | `inferred` — capabilities named, gates 1 to 3 passed | Look for a first-party trace: queries in their vocabulary, questions in their terms, referrers from their world | One query pass |
| 3 | `corroborated` — a trace exists, quoted with its count | **One page**, in their vocabulary, on a capability that already works. Watch [impressions](../../mcp/analytics/get-search-rankings.md) and the [zero-result rate](../../mcp/analytics/get-failed-searches.md) against that vocabulary | One page |
| 4 | Tested — the page drew the segment and they got somewhere | **One worked example** ending in their finished result. Watch whether readers reach it and what the dead-end rate says on it | One example |
| 5 | Worth a programme | Hand to a human with the sizing above | Their decision, not this pass's |

Never skip from rung 2 to rung 5. The skip is the entire failure mode this reading exists to prevent, and it always looks justified at the time because the reasoning at rung 2 is genuinely sound — it is simply reasoning, and one page settles in a month what an argument cannot settle at all.

State the test's read-back window and its floor when you propose it. A vertical page judged on nine visits has told nobody anything; the floors in [metrics](../auditing/metrics.md) apply here unchanged.

## 6. The decision output — one verdict per candidate

Every candidate leaves this pass with exactly one of four verdicts, its reason, and either the gate it failed or the smallest next step. Nothing leaves undecided; "interesting" is not a verdict and it is how candidate lists become permanent.

| Verdict | Means | Must carry |
|---|---|---|
| **Enter** | Gates 1 to 5 pass and a test at rung 4 already succeeded | The sizing above, and the human who signed the maintenance |
| **Test** | Gates 1 to 3 pass, evidence at rung 2 or 3 | The one page or one example, its vocabulary, the metric read back and the window |
| **Park** | A gate fails on something that can change | The gate, and a **re-check condition** — concrete and observable |
| **Reject** | A gate fails on something that will not change | The gate, and the reason it is structural rather than temporary |

**Park is the most common verdict and the most abused.** A park without a re-check condition is a reject that nobody had the nerve to write, and it returns unchanged to every future run. The condition must be observable by someone other than its author: *scheduling reaches a self-serve plan*, *a second language ships*, *the answer layer is switched on*, *three questions in that vocabulary appear in one window*. A market that is wrong today is very often right after exactly one product change, which is why the condition matters more than the verdict.

## 7. Its place in the priority queue

Say this plainly in the report, in this order, because it is what stops this pass turning a documentation audit into a strategy offsite.

- **An expansion candidate never outranks a measured failure on existing traffic.** A page losing readers today has evidence; a market has an argument. It is not softened by the candidate being larger.
- **An expansion candidate rarely outranks an unserved job in the market the product is already in.** The unserved job rests on the same capability map and needs no new vocabulary, no new maintainer and no new promise. It is the cheaper half of the same idea, nearly every time.
- **At most one expansion candidate enters the week's five, and only at *test* size.** Everything else is one line with a count. A queue whose top three items are markets is a plan nobody will execute.

## What the report looks like

Hand back in this order, decision-ready, `hypothesis` labelled throughout:

1. **The inputs that were available**, and any sibling reading that did not run — stated first, because it bounds everything below.
2. **Candidates carried over** from the demand-gap sweep, with the axis each moves along.
3. **The gate table**: every candidate, the gate it reached, the tier it holds.
4. **Survivors with their sizing** — pages, vocabulary, maintainer, multiplier, abandonment cost.
5. **The verdict table**, with a re-check condition on every park.
6. **The one candidate**, at most, that enters the week's queue, at test size.

Then hand over and stop: the single test page to [the page set](../planning/page-set.md), named as one asset type and the reader question it closes; translations, navigation, plan and language configuration to [site capabilities](../automation/site-capabilities.md); the park re-check conditions to [automation](../automation/monitoring.md) as a watch, because a re-check nobody scheduled is a re-check nobody runs; the contested-market comparison to [competitors](./competitors.md); switching mechanics inside any market entered to [jobs to be done](./jobs-to-be-done.md). This pass writes nothing, and it decides nothing on its own authority — it hands a shortlist to a human.

## Traps

- **Never size a market.** No total addressable market, no revenue estimate, no share figure, no "roughly N companies". The platform cannot buy those numbers and this reading does not estimate them; a fabricated market size is the one output here that gets repeated in a board deck and never traced back.
- **Never attach a volume to an industry phrasing.** Search clusters carry no numbers anywhere in this handbook, and an industry vocabulary is a search cluster.
- **Never run this pass without its inputs.** Name the missing sibling and stop. A market expansion argued from the pages themselves reproduces whatever the pages already assumed about their audience, which is precisely the assumption under audit.
- **Never enumerate candidates here.** [Demand gaps](../auditing/demand-gaps.md) owns the sweep; adding a market this pass thought of on its own reintroduces the unsupported claim the `speculative` tier exists to contain.
- **Never characterise a rival's coverage of the candidate market.** That is [competitors](./competitors.md), and a claim about their docs is hearsay until [external checks](../auditing/external-checks.md) verifies it against their live page.
- **Never audit the belief ladder of a new segment here.** Borrow its length for the page count; [jobs to be done](./jobs-to-be-done.md) owns its contents, and running it twice yields the same gap at two severities.
- **Never promote `corroborated` to `measured`.** A segment arriving and failing is measured evidence about readers, never about a market.
- **Never propose entry without a named maintainer.** The unmaintained vertical is the failure this reading exists to prevent, and it is invisible at proposal time.
- **Never let a park stand without an observable re-check condition**, and never let an expansion candidate outrank a measured failure or displace more than one slot in the week's queue.
- **Do not report a machine-audience finding twice** when the answer-engine layer check in [metrics](../auditing/metrics.md) or [GEO and AI search](./geo-ai-search.md) already raised it. Merge at the higher severity and name both.
- **Do not treat a vocabulary that matches as a market.** Same words means same market, and the work demotes to coverage.

## Checklist before you call it done

- The pass ran last, and its first line names every input artefact it had and every sibling reading that did not run.
- Every candidate traces to the demand-gap sweep; none was invented in this pass.
- Each candidate is assigned exactly one primary axis, and multi-axis candidates are priced at the more expensive axis with that stated.
- Gates were run in cost order, and every candidate records the gate it reached.
- Every surviving candidate carries all four sizing components — page count, vocabulary owner, maintainer with multiplier, abandonment cost — or none is reported.
- Every candidate holds exactly one tier: `speculative`, `inferred` or `corroborated`, and every `corroborated` quotes its trace verbatim with a count.
- Every verdict is one of enter / test / park / reject; no candidate leaves undecided.
- Every park carries a re-check condition observable by someone other than its author.
- No market size, share, revenue figure or industry search volume appears anywhere in the output.
- At most one expansion candidate entered the week's queue, at test size, and no expansion item outranks a measured failure.
- Nothing was written: the test page went to whoever writes pages, configuration to whoever owns the site, re-check watches to automation.

## Related

- [Demand gaps](../auditing/demand-gaps.md) — the capability map, the audience map and the candidate sweep this reading consumes.
- [Competitors](./competitors.md) — whether the candidate market is contested or empty.
- [User language](./user-language.md) — the vocabulary mismatch that decides gate 3 and most of the cost.
- [Jobs to be done](./jobs-to-be-done.md) — the belief ladder whose length sets the page count.
- [Backlinks and digital PR](./backlinks-digital-pr.md) — the asset that is often the cheapest door into a new market.
- [Translations](../../translation/README.md) — the axis with the permanent multiplier.
