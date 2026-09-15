---
title: "When the answer is a widget, not a paragraph: auditing documentation for free tools"
description: "How to spot reader needs that no amount of prose can close, classify them into tool classes, judge build cost honestly, and audit the tools you already shipped for correctness drift."
tldr: "Two questions decide it: does the answer change with the reader's own input, and is the reader doing arithmetic, transformation or lookup by hand? Both yes is a tool; anything else is a page. A stale tool outranks every other finding, because it produces a freshly computed wrong number the reader has no reason to doubt."
---

# Free tools — the reader whose answer is a widget, not a paragraph

Every other reading in this handbook assumes the fix is text: a better title, a rewritten section, a page that does not exist yet. This one is the only place where the honest finding is *no amount of writing solves this*. A reader who needs to know what their invoice will be at 47 seats on annual billing, whether their config file is valid, or what their cron string actually means on a Tuesday is not underserved by prose — they are served by prose, badly, forever, because the answer depends on a value only they hold.

The signature is already sitting in ordinary docs evidence and every other pass reads past it. A failed search with a number in it looks like a content gap. A page carrying nine hand-written worked examples looks like a thorough tutorial. A 300-row limits table with heavy dwell looks like an engaging reference. Each of those is a tool someone hand-rolled in Markdown and is now maintaining by hand, which is why the same page accumulates a tenth example every quarter and never gets shorter.

What it costs when nobody looks: the reader does the arithmetic themselves and gets it wrong, then arrives in support with a number nobody can reproduce; the writer keeps paying maintenance on a lookup table that a twenty-line calculator would own; and the single asset class most likely to be linked to, bookmarked and returned to never gets built. A page is read once. A validator is opened every time someone edits the file.

## What does this reading own, and what does it hand over?

| This reading owns | It does NOT own → owner |
|---|---|
| Finding reader needs whose correct answer depends on the reader's own input | Reader needs answerable in prose → [Demand gaps](../auditing/demand-gaps.md) |
| Classifying the need into a tool class and naming the data and logic that class requires | Writing the tool, the page or the scaffolding → [The page set](../planning/page-set.md) |
| The build-cost verdict, including "not worth it" with the reason | The tool page's title text, body copy, register and call to action → [Writing rules](../writing/writing-rules.md) and [Conversion](../writing/conversion.md) |
| Auditing tools that already exist: usage, reachability from the prose that describes the same problem, and correctness drift | Keeping a shipped tool in sync with the product's rules on a schedule → [Automation](../automation/monitoring.md) |
| Supplying the verbatim reader phrasings the tool page must be findable by | Whether the tool page ranks, and its title-versus-query mismatch → [Behavioural detectors](../auditing/behaviour.md) and [Search intent](./search-intent.md) |
| Naming which prose pages must link into the tool | Whether a widget already renders this shape → [Presentation](../writing/presentation.md) |
| Noting that a tool is the most citable asset class the docs can hold | Pursuing the citations → [Backlinks and digital PR](./backlinks-digital-pr.md). Hand the thread over; do not work it here |

A tool proposal that duplicates a content gap is worse than no proposal, because the same reader need arrives twice with two owners and two severities. If prose closes it, it is not this reading's finding.

## When does this pass earn its place?

- **The evidence carries parameters.** Failed searches, unanswered assistant questions or on-site queries that differ only by a value — plan name, seat count, region, version — are the direct fingerprint.
- **A page is visibly doing a machine's job.** Three or more worked examples with different inputs, a long lookup table, or a procedure whose every step is a transformation with no decision in it.
- **The product has rules readers must satisfy before anything works** — a config schema, a payload format, a naming constraint. A validator is the cheapest trust the docs can buy, and it is almost never built.
- **Support keeps reproducing the same arithmetic by hand.** Whoever answers "what will this cost me" for the fourth time is a calculator that has not been written down.
- **Not when** the docs have never been audited for the ordinary failures. A calculator on a site where the quick start dead-ends 14% of readers is a decoration bought with a quarter. Measured failures on real traffic outrank every candidate here, without exception.

## How strong is each line? The evidence tiers

This reading is **both tiers at once**, and mixing the two halves is how it starts inventing work.

**Detection is `measured`** where the signature comes from real data — a query count, a question count, an exit or repeat-visit figure on an existing tool page. Every candidate names the count of *distinct visits* behind it and quotes the reader verbatim. Below the sample floors in [metrics](../auditing/metrics.md), it is an observation, not a finding, and nothing gets built for it.

**The verdict is `hypothesis`.** "This need is tool-shaped" and "a tool would close it" are inferences. They are labelled as such and they never outrank a page that is measurably losing readers.

**Feasibility is graded separately**, because it is a claim about the product: `capability` — the logic, endpoint or dataset was read in this run, with a citation; `inferred` — it follows from capabilities read, and from nothing else; `speculative` — an assumption about what the product could expose. **A tool specified on `speculative` feasibility is not specified.** It is a request that someone build a service, and it goes to the owner as a question, not into a writing queue.

The platform reads search rankings, failed searches, assistant questions, reader behaviour, funnels and the doc graph. It cannot buy keyword volumes, backlink indexes or competitor traffic, so this reading never carries a volume, a link estimate or a "tools attract N times more links" figure. Where a manual input would raise the tier — the price and limit tables, the validation library, whether a public endpoint exists — ask the owner for it and label their answer as theirs.

## 1. Harvest the fingerprints

Five signatures, all of them living in evidence the other passes already pull. Run them together and count distinct visits, never string occurrences.

| Signature | Where it lives | What it looks like | Why prose fails |
|---|---|---|---|
| Parameterised question | [Assistant questions](../../mcp/analytics/get-ai-questions.md), [failed searches](../../mcp/analytics/get-failed-searches.md), [on-site queries](../../mcp/analytics/get-popular-searches.md) | "cost for 47 seats", "limit on the team plan", "is this timezone supported" — one stem, many values | Every value needs its own sentence; the page covers three and the reader has a fourth |
| Hand-rolled worked examples | Page text | Three or more examples differing only in inputs, growing over releases | The page is a lookup table with paragraphs between the rows |
| A table people want to filter | Page text plus behaviour | Long reference table, high dwell, repeat visits, on-site searches that land there and are then refined | Reading is scanning; the reader wants a `where` clause |
| Conversion written as instructions | Page text | A procedure whose steps are pure transformation — "take your v1 config, rename these six keys, move this block" | The reader executes a deterministic function by hand and makes typos |
| "Is mine valid / is mine affected" | Assistant questions, issue-shaped queries, feedback | "does this schema work", "will my URL break", "am I over the limit" | Only the reader's artefact answers it |

Group by meaning, not by string, exactly as rejected searches are grouped in the [behavioural detectors](../auditing/behaviour.md): "price for 40 users", "40 seat cost" and "how much for a team of forty" are one need with three spellings, and splitting them hides the frequency that justifies the build.

> `measured`: 31 distinct visits asked the assistant a question of the form "what does it cost for N users" across nine different values of N over 30 days; the pricing page states three tiers and one worked example. `hypothesis`: this is a calculator, and no rewrite of the pricing page closes it.

## 2. The tool-shape test

Two questions. Both must be yes, or it is a page and building a tool is a quarter spent on decoration.

**Q1 — does the answer change with the reader's own input?**

**Q2 — does the reader currently do arithmetic, transformation or lookup by hand?**

| Q1 | Q2 | Verdict |
|---|---|---|
| yes | yes | **Tool.** Specify it |
| yes | no | The lookup already exists and works. A page, possibly a better-formatted one |
| no | yes | The arithmetic has one answer. Publish the answer, or write the missing page |
| no | no | A page. Stop here |

Then one gate that kills more candidates than either question: **can the reader already get this from the product itself, in fewer steps than the tool would take?** If the answer is visible in the product after login, the tool is only worth building for the reader who has not signed up — which is a legitimate and often excellent reason, but it must be said out loud, because it changes who the tool is for and therefore what it must not require.

Before specifying anything, check the live widget catalogue ([presentation](../writing/presentation.md) covers what is available). If a widget already renders a filterable comparison or a parameterised block, the finding is a configuration, not a build, and its cost drops by an order of magnitude.

## 3. Tool classes, their data, and what each is worth

| Class | The question it closes | What it needs | Where the requirement usually breaks |
|---|---|---|---|
| **Validator** | "Is my file, payload or name valid?" | The product's own validation rules, as a library, schema or endpoint | The rules live only inside a server the reader cannot reach. Highest trust and lowest effort *when* the rules are already extractable; a reimplementation that disagrees with the server is worse than nothing |
| **Calculator** | "What will this cost, size or consume for my numbers?" | The price, limit or quota table as versioned data | Hardcoded prices. It silently becomes a price claim that decays — the same decay [external checks](../auditing/external-checks.md) governs |
| **Converter or formatter** | "What is mine in the other format?" | A deterministic mapping. No product data at all | Almost nothing. Cheapest to build, most linkable, weakest route back into the product |
| **Generator** | "Give me a config, schema, snippet or regex for my case" | Templates plus the product's current option list | The option list drifts and the generated file stops loading. Highest conversion of the set: output is pasted straight into the product |
| **Checker or auditor** | "Point at my site or repo and tell me what is wrong" | A fetcher, a rate limit, and an abuse story | Nobody owns the running cost. Strongest link magnetism, highest operating burden |
| **Playground** | "Let me try a real call before I commit" | A live endpoint, anonymous or sandbox credentials, a quota | A playground that demands a login before it computes is a sign-up wall in a tool's clothing, and readers say so publicly |
| **Comparison or decision table** | "Which plan, region, SDK or method do I need?" | A dataset the team already maintains | Cheapest input-dependent asset in the list, and the one most often left as static prose |

For each candidate, answer the ownership question in one line: **where does this logic live today, and can a page reach it?** That answer, not the class, decides feasibility.

## 4. Build-cost honesty, and when to say no

Per candidate, record: the source of truth for its logic; whether a static page can reach that source; how often the source changes; who owns the tool when it breaks; what it outputs when it is stale.

Four kill rules, and writing "not worth it" against them is a finding, not a failure of nerve:

- **No named source of truth.** "We will hardcode the current values" is how a calculator quotes a price that ended two quarters ago.
- **The data moves faster than anything that updates it.** A dataset that changes weekly with no automation behind it is a wrong-answer machine with your logo on it. Either the sync is part of the specification and goes to [automation](../automation/monitoring.md), or the tool is not specified.
- **The output would be read as a commitment** — a quote, a compliance verdict, a legal limit. That is the owner's decision, not a docs queue item.
- **An operating burden nobody accepted** — a rate limit, an abuse surface that fetches arbitrary URLs, credentials in a browser.

A stale page states a fact the reader can doubt and date. A stale tool produces a freshly computed, wrong number the reader has no reason to question, then pastes it into a budget. That asymmetry is why correctness drift is the highest severity this reading can issue.

## 5. What the specification contains

Whoever builds the tool receives exactly this, per tool — anything missing is guessed later, wrongly:

- The reader question, **verbatim**, with the count of distinct visits behind it and the window.
- Inputs: name, type, valid range, unit, default.
- The computation or rule, and the **named source of truth** it must read, with its tier.
- Outputs, their units, and the sentence the tool should print alongside the number so the reader can check it.
- The **worked default** — a pre-filled realistic case that produces a meaningful answer before the reader types anything. An empty tool is a blank form, and a blank form reads as work.
- What it must refuse to answer, and what it says instead. A tool that guesses outside its range is the fastest way to lose the trust the tool was built to earn.
- The sync requirement — what updates it, how often, and what happens if that stops.
- The prose pages that must link into it, by path, from the doc graph.

## 6. Distribution — an unfound tool is a feature nobody uses

Four requirements, all of them cheap and all of them routinely skipped.

1. **Its own indexable URL.** A tab inside an existing page or a modal cannot be linked to, cited or ranked, and this is the asset class whose entire upside is being linked to.
2. **A plain-language title matching how the need is typed.** Supply the verbatim phrasings from the harvest; whoever writes the page writes the words. Never coin a phrasing this reading reasoned its way to, and never attach a volume to one.
3. **The worked default**, as above — the tool must be useful in the first second.
4. **A route back into the product**, and inbound links from every prose page describing the same problem. That last one is the check that fails most: the tool ships, and the three pages that describe the problem in prose never mention it exists.

## 7. Auditing the tools already there

Three questions, in this order. The first outranks everything else in this reading.

| Check | How | Severity when it fails |
|---|---|---|
| **Correctness drift** | Take three inputs whose correct answer you can derive from a source of truth **read in this run**, run them through the live tool, compare | **Critical.** A tool answering wrong is quoted, screenshotted and repeated. Report it above every content finding in the run |
| **Reachability** | From the doc graph, list every page describing the same problem and check each for a link to the tool | High. An orphan tool is the normal state, not the exception |
| **Usage and outcome** | Traffic and repeat visits on the tool page, and whether visits terminate there or continue | Medium. High repeat visits with no onward route is a working tool with no call to action |

Verify the tool against the live source with the same discipline [external checks](../auditing/external-checks.md) sets for price claims: a URL, a date, and "unverifiable" as its own verdict rather than blended into "wrong". Never mark a tool wrong from memory.

## 8. Ranking and the cut

Rank candidates by **distinct readers behind the signature × feasibility × route back into the product**, multiplied, for the same reason [demand gaps](../auditing/demand-gaps.md) multiplies: any single 1 collapses the score, and it should. A high-demand tool whose logic has no reachable source of truth is not a cheap tool, it is a promise. Correctness drift on an existing tool enters the queue above every new build.

Cut to five. Everything below the cut is one line with a count.

## What the report looks like

Handed back in this order:

1. **Existing-tool failures**, correctness drift first, then reachability, then dead-ended usage — `measured`, with counts and the window.
2. **Tool-shaped needs found**, each with its verbatim reader evidence, distinct-visit count, class, and feasibility tier.
3. **Rejected candidates**, with which of the two test questions they failed and which sibling reading owns them instead. This list is the proof the reading was applied rather than performed.
4. **A queue of at most five specifications**, to whoever builds pages and tools.
5. **Page copy, titles, calls to action, and the inbound links from prose pages**, to whoever writes.
6. **The sync requirement per tool**, to [automation](../automation/monitoring.md).
7. **The citation and link thread**, named and untouched — to [backlinks and digital PR](./backlinks-digital-pr.md).

## Traps

- **Never propose a tool when the answer does not depend on the reader's input.** That is a page, and a widget for it is a quarter spent on decoration that a paragraph would have closed.
- **Never invent a number.** No usage figure, no search volume, no link count, no "interactive assets earn N times more citations". There is no third-party volume or backlink data here at all; count distinct visits in the workspace's own evidence and stop there.
- **Never specify a tool whose logic rests on `speculative` feasibility.** Take it to the owner as a question about what the product can expose, never into a writing queue as work.
- **Never write the tool, the page, its title text or its call to action.** A one-file HTML calculator is still a write, and the copy belongs to whoever owns the page.
- **Never restate a title-versus-query mismatch as a tool finding.** If the right page exists and reads wrong in a result list, that belongs to [search intent](./search-intent.md) and the [behavioural detectors](../auditing/behaviour.md), and reporting it twice at two severities is exactly what a duplicated reading costs.
- **Never claim a link, citation or PR outcome for a proposed tool.** Name that the asset class is citable, hand the thread to [backlinks and digital PR](./backlinks-digital-pr.md), and drop it.
- **Never let a tool proposal outrank a measured failure on real traffic**, and never let a `hypothesis` tool-shape verdict inherit the confidence of the `measured` count that produced it.
- **Do not treat a stale tool as a low-severity page issue.** It computes a fresh-looking wrong answer that the reader has no reason to doubt.
- **Do not propose a playground when the product has no anonymous or sandbox access path.** A tool that requires a login before it answers is a conversion gate, and it will be described as one in public.

## Checklist before you call it done

- Every candidate carries a verbatim reader phrasing and a count of distinct visits, inside the run's single stated window.
- Candidates below the sample floors in [metrics](../auditing/metrics.md) are reported as observations and specify nothing.
- Both tool-shape questions were answered explicitly per candidate, and rejected candidates are listed with the question they failed and the sibling that owns them.
- The product-already-answers-this gate was applied, and any tool kept for pre-signup readers says so.
- Every candidate names its class, its source of truth, and a feasibility tier of `capability` / `inferred` / `speculative`.
- No specification rests on `speculative` feasibility.
- Each specification names inputs, computation, outputs, worked default, refusal behaviour, sync requirement and inbound links.
- Existing tools were tested against a source of truth read in this run, with three inputs each, and drift is reported above every other finding.
- Reachability was checked against the doc graph, not from memory.
- The queue is cut to five, with everything below it as one line and a count.
- Detection is labelled `measured`, verdicts `hypothesis`, and no proposal is ranked above a measured failure.
- No volume, link estimate or usage figure appears that the data did not supply.

## Related

- [Demand gaps](../auditing/demand-gaps.md) — the needs that prose does close, and the capability-to-job chain behind them.
- [Original research](./original-research.md) — the dataset a tool often queries, and how to make it publishable.
- [Backlinks and digital PR](./backlinks-digital-pr.md) — why a tool is the most linkable thing documentation can hold.
- [Presentation](../writing/presentation.md) — the widgets already available before anything is built.
- [External checks](../auditing/external-checks.md) — verifying a tool's answers against the live source of truth.
