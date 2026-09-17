---
title: "Choosing a lens: which reading your question and your evidence call for"
description: "The decision procedure that picks two to four readings out of fifteen — by the shape of the question and the evidence in hand, never by the topic word in the request."
tldr: "Route on the shape of the question and the evidence you actually have, never on the topic word in it. A lens earns its place only if it can find something no already-chosen lens can, and measured evidence beats inferred evidence at every level. Two to four readings is a run; five or more means the request was never scoped."
---

# Choosing a lens

An audit that runs every check produces a document nobody reads. An audit that runs one check produces a confident answer to a question nobody asked. This page is the decision procedure between those two failures: given what somebody asked and what evidence actually exists, which readings you take, in what order, and where their findings merge.

It is not a menu. It is the reasoning done before a single page is opened, and it holds three rules that every route obeys.

> **1. Route on the shape of the question and the evidence in hand — never on the topic word in it.**
> "Our SEO is bad" is not a route to an SEO lens. It is a symptom with at least four possible owners, and the word "SEO" is the least informative thing in the sentence.
>
> **2. A lens earns its place only if it can find something no already-chosen lens can.**
> Every reading below declares an exclusive claim. Two lenses whose claims overlap produce the same finding twice, at two severities, and the reader trusts neither.
>
> **3. Measured beats inferred, at every level.**
> This governs which reading runs first, which finding ranks higher, and which one wins when two disagree. A page failing on real traffic outranks the best-argued opportunity, always.

## Is this an audit at all?

Before routing anything, confirm the request is analysis. The test is the verb, not the topic.

| What is being asked | Where it belongs | Why not here |
|---|---|---|
| What is wrong, why did it change, what should we fix first | This section | — |
| Write this, rewrite this, restyle this, configure the site, declare a goal | [Writing](../writing/writing-rules.md) and [publishing](../planning/publishing.md) | An audit decides *which* page changes, never *what it says* |
| Build documentation that does not exist yet, migrate off another platform | [Planning a page set](../planning/page-set.md) | A page that does not exist cannot be audited |
| Make this keep happening, watch for it, alert us | [Automation](../automation/monitoring.md) | A finding you keep re-finding is a monitor, not an audit |

A request that spans two of these runs them in order and says so. A request that spans four was never scoped — ask which one comes first.

## What are the five passes, and where does writing start?

An audit is five passes, and the fifth is the only one that touches a file.

| Pass | What it produces | May it write? |
|---|---|---|
| 1. Locate | A shortlist of pages ranked by readers affected, each with its raw counts and the signal that put it there | No |
| 2. Diagnose | What is actually wrong on each, through the lenses this page selects | No |
| 3. Translate | The finding in the language of the business, worst first, evidence attached | No |
| 4. Check whether this has ever worked | A verdict on a comparable prior change, or a baseline because none existed | No |
| 5. Apply | The change, through the route the owner chose | Yes — and only after the gate below |

Passes 1 to 4 never touch a file. The crossing point is explicit, it belongs to the owner, and it is the only one. [Reading the numbers](./metrics.md) is the method for pass 1, [business translation](./business-translation.md) for pass 3, and [did it work?](./did-it-work.md) for pass 4.

## What shape is the question?

Five shapes, and each opens a different door. The shape is what the person wants to be true when the run finishes, not the words they typed.

| Shape | Sounds like | Opens with |
|---|---|---|
| **Diagnostic** | "Traffic dropped", "nobody converts", "why do readers leave" | Pass 1 in full. The numbers pick the lens; you do not. |
| **Triage** | "Audit our docs", "what should we fix first" | Pass 1, then the two or three lenses the shortlist's dominant signals point at. |
| **Conformance** | "Is our GEO set up", "check our internal linking", "are we trustworthy" | The one lens that owns it, plus pass 1 to say whether it matters here. |
| **Demand** | "What are we missing", "which pages should we write", "who else could use this" | The forward-reasoning lenses. Pass 1 only to demote anything already ranking. |
| **Expansion** | "Where else could we go", "should we do vertical X" | The terminal lens, and only once its named inputs exist. |

**A conformance question with no numbers behind it is the commonest misroute there is.** "Check our internal linking" gets answered with a graph report, the graph turns out to be fine, and the actual problem — that nobody arrives at the cluster in the first place — goes unexamined. Run pass 1 anyway, briefly, and say whether the lens they named is where their problem lives. If it is not, say that first, and then still answer the question they asked.

## What evidence do you have?

Evidence gates honesty, and a lens run above its tier produces fiction in a confident tone. Establish the tier once, state it once at the top as [reading the numbers](./metrics.md#degrading-honestly-what-you-can-produce-with-what-you-have) prescribes, and never re-raise it mid-report.

| Tier | You have | What runs at full strength |
|---|---|---|
| **T3 — connected workspace and search data** | Rankings, reader behaviour, routes, failed searches, assistant questions, goals and funnels | All of them |
| **T2 — behaviour, no search data** | On-site behaviour, searches, questions; no positions or impressions | Everything except the search-position half of search intent; semantic authority runs corpus-internally |
| **T1 — the files only** | A documentation folder, a repository, a public site | The corpus-shape and forward-reasoning lenses; anything traffic-dependent degrades or is skipped and said to be skipped |

The rule is: **skip loudly, never silently.** A lens that cannot run at your tier is named once, with what it would have added, and dropped. A lens that runs anyway on data it does not have is the single most expensive failure this procedure prevents.

## Which failure mode are you actually looking at?

A number says a page is failing. It does not say why, and the four reasons need four different fixes. Naming the mode is what decides between a detector and a lens.

| Mode | What it means | Where it goes |
|---|---|---|
| **Missing** | Nothing answers the question | A page to write, not a page to fix. Cross-check zero-result searches against unanswered assistant questions: a topic confirmed in both outranks a bigger count in either alone |
| **Unhelpful** | The page exists and does not answer | [Content detectors](./content-detectors.md) |
| **Unfindable** | The answer exists and readers never reach it | A title, a link or the navigation — never a rewrite. [User language](../lenses/user-language.md) or [internal linking](../lenses/internal-linking.md) |
| **Unserved** | A whole job, audience or workflow the product supports and the documentation addresses nowhere | [Demand gaps](./demand-gaps.md) — found by working forward from what the product can do, never backward from traffic |

Mislabelling is expensive: writing a new page when the real problem was the title costs a week and does not work. **Unserved** is the one nobody checks for, because its symptom is silence — a use case with no page has no impressions, no dead ends and no failing rank, so its absence is indistinguishable from success in every signal you have.

## The routing table

One row per reading. "Fires when" is a condition, not a topic: if the condition is not met, the lens does not load, however relevant its name sounds.

| Reading | Fires when | The finding only it produces | Tier of its output |
|---|---|---|---|
| [Demand gaps](./demand-gaps.md) (the capability map) | New site, thin numbers, or a shipped capability the documentation never framed as a job | A job, audience or workflow with no page at all — invisible in every number | Hypothesis |
| [Jobs to be done](../lenses/jobs-to-be-done.md) | Readers arrive and do not commit; a job is "covered" and still does not convert | The belief a reader must hold in order to switch, and the earliest rung no page carries | Mixed |
| [Semantic authority](../lenses/semantic-seo.md) | Pages rank shallowly across a whole topic, or the corpus mentions a field without owning it | A concept absent from the vocabulary entirely — there is no page to detect it on | Corpus-internal |
| [Search intent](../lenses/search-intent.md) | Impressions without clicks; a page ranks and the wrong readers arrive | A page that ranks and is the wrong *shape* for the question it ranks on | Measured, plus manual hypothesis |
| [Programmatic families](../lenses/programmatic-seo.md) | The same question repeats with one variable changed | A demand pattern visible only across a page family, never page by page | Mixed |
| [Free tools](../lenses/free-tools.md) | Readers ask "what will X be for my values"; pages carry manual worked examples | A reader need whose correct answer is a widget rather than a paragraph | Hypothesis |
| [Original research](../lenses/original-research.md) | The product generates data nobody outside it can obtain | First-party data the company is sitting on and has never published | Capability |
| [AI search and citability](../lenses/geo-ai-search.md) | Assistant crawlers are reading pages, or a question is being answered without a visit | The reader who got their answer and never arrived; the structurally uncitable page | Mixed |
| [Competitors](../lenses/competitors.md) | Evaluation-stage readers leave; a rival is named in the request or in reader questions | What the market documents that you do not — and what you own and undersell | Hypothesis, dated |
| [User language](../lenses/user-language.md) | Failed searches, unanswered assistant questions, or any "we have the page and nobody finds it" | The right page, unreachable because it is written in the company's words | Measured |
| [Content architecture](../lenses/content-architecture.md) | The corpus grew past the tree it was designed for; readers land and cannot orient | A defect present in no single page, visible only across all of them | Mixed |
| [Internal linking](../lenses/internal-linking.md) | Orphans, dead ends, or clusters that traffic never crosses between | Graph topology — islands, sinks, missing edges — that per-page checks cannot see | Mixed |
| [Trust and E-E-A-T](../lenses/eeat-trust.md) | Money, credentials or risk are involved; the documentation is correct and still not believed | A corpus that is factually right and not trusted | Mixed |
| [Backlinks and digital PR](../lenses/backlinks-digital-pr.md) | Asked about authority or links; or a linkable-asset candidate surfaced elsewhere | Whether anything here is worth citing, and which earned links are being wasted | Hypothesis, hard-capped |
| [Market expansion](../lenses/market-expansion.md) | Everything in the current market is understood and the question is "where next" | Which candidate market survives its gates, and what entering it costs in pages | Speculative, ending in a decision |

**The default set size is two to four.** One lens answers a conformance question. Two to four answer a triage. Five or more means the request was not scoped: say what you would cover in each of two runs, and ask which comes first. A fifteen-lens run is not thorough — it is a document that gets skimmed and filed.

## Does the order matter?

It does, and it is not cosmetic. A reading taken in the wrong position asks a question that an earlier one would have dissolved.

1. **Pass 1 first, always** — unless the tier says there are no numbers to read. It decides which lens is worth loading, and demotes anything already ranking.
2. **Cheapest reframers next.** [User language](../lenses/user-language.md) and [search intent](../lenses/search-intent.md) routinely turn "we need to write more" into "we need to rename three things". Running them after a content lens wastes the content lens.
3. **Corpus shape before corpus content.** [Content architecture](../lenses/content-architecture.md) and [internal linking](../lenses/internal-linking.md) change what "missing" means: a page written into a broken tree is a page nobody reaches.
4. **Measured lenses before inferred ones.** Everything traffic-fed runs before anything reasoned forward from capabilities.
5. **[Demand gaps](./demand-gaps.md) and the forward-reasoning lenses after the measured work**, so their queue is demoted against it rather than competing with it.
6. **[Market expansion](../lenses/market-expansion.md) last, and only if its inputs exist.** It consumes the capability map, the audience map, the competitor matrix, the vocabulary table and the asset ranking. Run without them, it is an opinion with a table around it.

## Where two readings touch

Lenses overlap at their edges by design. The overlaps are resolved here, so that a finding never appears twice.

| When two readings touch | Owner | What the other one does instead |
|---|---|---|
| A page is unreachable | [User language](../lenses/user-language.md) if the words are wrong; [internal linking](../lenses/internal-linking.md) if the edges are missing; [content architecture](../lenses/content-architecture.md) if the tree is wrong | Names the finding and cites the owner |
| A concept has no page | [Semantic authority](../lenses/semantic-seo.md) if it is absent from the vocabulary; [demand gaps](./demand-gaps.md) if it is a job with no page | Cites the other as an input |
| A rival is involved | [External checks](./external-checks.md) verify a specific claim; [competitors](../lenses/competitors.md) reads the market position | Neither restates the other |
| Anything recurring | [Automation](../automation/monitoring.md) | Every lens hands it over rather than proposing a manual re-run |

Deduplicate as the detectors already require: one line reported once, at the higher severity, naming both readings that found it. Then rank the merged queue by readers affected, with measured findings above hypotheses at equal size, and cut it to what a week holds. Five items is a plan; twenty is a backlog dump that gets ignored, and everything below the cut is one line with a count.

## Where does the change land?

Findings that survive the diagnosis and the prior-change check become edits. **Before writing anything, establish where the change should land.** If the owner has not already said, ask — this one question, with these three options.

| Route | What happens | When it fits |
|---|---|---|
| **Pull request** | A branch, the edits, and a description carrying the finding and its evidence | The documentation lives in a repository with review; anything touching prices, limits or claims about other companies |
| **Approve in chat** | The before and after shown per change, applied only on approval | A handful of changes, a person present, and no review process worth the ceremony |
| **Direct update** | Written straight to the source | The owner explicitly asked for it, the changes are mechanical, and they are reversible |

<!-- widget:callout type=warning -->

Do not guess this. A direct write into a repository somebody reviews is not a small mistake, and a pull request nobody wanted is a week of latency on a one-line fix.

<!-- /widget -->

[Publishing](../planning/publishing.md) covers the mechanics of each route; [from finding to change](../writing/from-finding-to-change.md) covers what a good change carries with it.

Then: one recommendation per page per run. Bundled changes make the next run unable to say which one worked.

## The four misroutes that actually happen

- **Routing on the topic word.** "SEO check" loads a search lens; the real defect is that the product's own term appears nowhere readers type. The cost is a quarter of title rewrites against a vocabulary mismatch.
- **Running a demand lens because the numbers were disappointing.** Small traffic is a reason to check the tier, not a licence to reason forward. The cost is a content programme built on inference while a measured failure sits unfixed.
- **Loading every lens because somebody said "full audit".** The cost is a report nobody finishes and a queue nobody can act on.
- **Answering the named lens and nothing else.** They asked about linking; linking is fine; you say so and stop. The cost is a correct answer to the wrong question, after which the reader concludes the audit found nothing.

## What makes a routing decision wrong

- **Never load a lens whose firing condition is unmet**, however precisely somebody named it. Say why it does not apply, and route to what does.
- **Never run a lens above its evidence tier.** Degrade it or skip it, and say which, once.
- **Never let a lens's own priority score cross runs.** Scores rank hypotheses inside one reading; the merged queue ranks by readers affected across all of them.
- **Never present a routing decision as a finding.** "We chose these three readings" belongs in one line at the top, not in the body of the report.
- **Never change route mid-run without saying so.** If pass 1 disproves the premise the question rested on, say that first, plainly, and then say what you ran instead.
- **Never let an opportunity outrank a measured failure.** Reasoning about who might arrive loses to a page that is demonstrably losing the readers who did.
- **Never invent a number to justify a route.** The evidence tier is a fact about the workspace, not a negotiating position.
- **The routing decision settles nothing about content.** It selects readings; [writing rules](../writing/writing-rules.md) still own every word that changes.

## Related

<!-- widget:cards plain cols=2 -->

- [Reading the numbers](./metrics.md) — pass 1, and the honesty tiers this procedure depends on {chart-line}
- [Reader behaviour](./behaviour.md) — the behavioural readings a shortlist points at {search}
- [Content detectors](./content-detectors.md) — the instrument for the unhelpful mode {file-text}
- [External checks](./external-checks.md) — the claims that decay with no commit behind them {globe}
- [Goals and funnels](./goals-and-funnels.md) — the owner's declared signal, and its own failure modes {target}
- [Demand gaps](./demand-gaps.md) — the reading for what has no page at all {network}
- [The lenses](../lenses/README.md) — all fourteen readings in full {book-open}
- [Routing the input](../planning/route-the-input.md) — the same question one level up: what kind of work was asked for {route}

<!-- /widget -->
