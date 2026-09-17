---
title: "Content architecture: the defect that lives between the pages"
description: "How to read a whole corpus as one object — the type census, tree shape, a front door per audience, the sequence to competence, and the split and merge tests that are not symmetrical."
tldr: "A corpus where every page passes its own audit can still fail the reader as a set. This reading counts the type mix, the depth and the entry points before it interprets anything, and every recommendation that moves a page comes with its redirect — a restructure that breaks URLs spends its own benefit on 404s."
---

# Content architecture

Every audit that finds something opens a page to find it. The [content detectors](../auditing/content-detectors.md) judge a page against the rules of its own type; the behavioural signals judge a page against what readers did on it; even the graph-wide checks — orphans, duplicate titles, translation parity — are per-page facts counted up. All of them share one blind spot: a corpus where every single page passes its own audit and the set still fails the reader.

That is the class this reading owns. A corpus that is 80% reference has a learning problem, and no reference page in it is guilty of anything — each is complete, neutral and correctly typed. A tree with one front door built for the audience the founders were serves that audience perfectly on every page. Three pages splitting one job are each individually well written. A branch with forty siblings contains forty good pages. There is no page to flag, so no page-level audit ever flags it, and the defect survives audit after audit indefinitely while the team congratulates itself on a clean report.

What it costs is the part nobody attributes to structure. Readers who cannot guess where anything lives fall back on search on every visit, and a docs site whose top route starts "landing → search" is paying for navigation it is not using. Readers who arrive mid-corpus meet a page written as step three of a sequence that exists nowhere, give up, and are recorded as a dead end on a page that is fine. An audience with no front door produces no failing signal at all, because nothing on the site ever matched what they would have typed — the same silence [Demand gaps](../auditing/demand-gaps.md) describes, arriving through the tree rather than through the product.

This reading takes the whole corpus as one object, states the shape it is actually in, and hands the fixes out. It counts, it reads, it reports, and it never moves a file or edits a navigation config.

## What this reading owns, and what it does not

| This reading owns | It does not own → who does |
|---|---|
| The distribution of page types across the whole corpus, and what a lopsided one does to a reader | Whether a given page obeys the rules of its own type → [Content detectors](../auditing/content-detectors.md), with severities |
| Tree shape: depth per branch, sibling counts, the one-child branch and the forty-child branch | Broken links, anchor text, orphan pages and the link graph → [Internal linking](./internal-linking.md) |
| Entry-point coverage per audience, audited against an audience map handed over, not re-derived | Which audiences and jobs exist at all → [Demand gaps](../auditing/demand-gaps.md) |
| Whether a path from first contact to competence exists as an actual sequence | What the next-step link on any one page should say → [Writing rules](../writing/writing-rules.md) |
| Page boundaries: the split test and the merge test, which are opposite fixes | Whether a page's concepts and entities are covered → [Semantic SEO](./semantic-seo.md) |
| Whether the hierarchy is guessable, and how to test that without running a study | The pitch a single page makes to a single query → [Search intent](./search-intent.md) and the striking-distance band in [Reader behaviour](../auditing/behaviour.md) |
| Top-level navigation as a claim about priority, collided with real entry data | The structure a NEW site is given → [Deciding the page set](../planning/page-set.md) |
| Restructuring cost and the redirect obligation on any move | Applying navigation, grouping, labels or redirects → [Site capabilities](../automation/site-capabilities.md) |

## When is this reading worth the time?

- **The corpus is above roughly 25 pages and grew by accretion** — a page per release, the tree never revisited. This is the default state of every docs site that survived two years.
- **Readers land deep and do not move.** Entry pages are spread across the corpus while the front door takes a minority of arrivals, or the most frequent route starts with the site's own search box.
- **A product the docs serve has an audience with no page addressed to it** — carried over from the demand-side reading, not discovered here.
- **The measurable work is done and the numbers are still flat.** Rewriting the same twelve pages harder does not fix a corpus whose shape is the problem.
- **A section keeps growing while the rest stands still** — the early sign that the tree has outgrown itself.
- **Not** when the site is under roughly 15 pages or was generated in the last week. Below that, shape is not a defect, it is a list, and the page set is [a creation decision](../planning/page-set.md). And **not** ahead of a page that is measurably losing readers today.

## Evidence tiers

This reading is mixed, and the two halves must stay visibly apart because one of them survives with no analytics at all.

| Half | Label | What belongs in it |
|---|---|---|
| The census | `measured` | Page counts by type, depth per branch, sibling counts, the entry-point inventory, the URL map. All of it is countable from the tree; none of it needs traffic. It stays a fact when the workspace has no history |
| The reading | `hypothesis` | What a distribution does to a reader, whether the sequence works, whether the naming is guessable, which page is doing three jobs. Inference, labelled as such |

Where audiences enter, they arrive with [Demand gaps](../auditing/demand-gaps.md)' tiers already on them — `capability`, `inferred`, `speculative` — and this reading carries those labels through rather than upgrading them. An entry point missing for a `speculative` audience is a `speculative` finding.

The collision rule: where real entry or route data clears the sample floors in [Metrics](../auditing/metrics.md), the number decides against the reading. A top-level item you judge central and the data shows nobody enters through is a finding about your judgement, not about the readers.

## 1. Build the census before you read anything

One row per page, and no analysis until the table is complete: path, depth, parent, sibling count at that level, page type, the audience it addresses, and whether it is an entry point (linked from the root or the top navigation). Count. Never estimate a distribution — "roughly two thirds reference" is exactly the invented number to avoid, and it is free to avoid.

Classify type by what the page actually does, never by its folder. A page under `/guides/` that lists every parameter is reference, and counting it as a how-to hides the real mix. A page you cannot classify at all is a page with no consistent goal or audience — that is a critical finding for [Content detectors](../auditing/content-detectors.md), so record it, hand it over, and exclude it from the mix rather than guessing a type to make the table tidy.

## 2. Read the type mix

The four types are the Diátaxis ones: tutorials for learning, how-to guides for a task, reference for information, explanation for understanding — four distinct needs and four corresponding forms ([Diátaxis](https://diataxis.fr/)). The mix is judged against **this product**, never against a golden ratio. An API-only product legitimately skews reference; the finding there is never the ratio, it is which of the other three types is missing entirely.

| Shape | What it does to a reader | Fix class | Owner |
|---|---|---|---|
| Reference above ~60%, few or no tutorials | Nobody can start. The docs answer questions only someone already competent knows how to ask; the product looks harder than it is | One tutorial per primary audience, and one explanation page carrying the mental model | [Page set](../planning/page-set.md) |
| Tutorials only | Unusable by anyone who already knows the product. Returning readers re-read a lesson to find one parameter, and end up in support | Extract the parameter tables into reference; extract the variant paths into how-tos | [Page set](../planning/page-set.md) plus splits from §6 |
| No explanation type anywhere | Every page says what to type and none says why. Readers cannot generalise, so every new task becomes a new support question | Concept pages for the two or three ideas the whole product rests on | [Page set](../planning/page-set.md) |
| No reference type | Competent readers cannot look anything up, so they read tutorials for facts and copy stale values out of prose | A reference surface for the API, CLI or config that exists | [Page set](../planning/page-set.md) |
| How-to only, no tutorial and no concepts | The corpus serves the person already inside the product and nobody outside it. Evaluation and onboarding happen in sales calls instead | One guaranteed path from zero, and the mental model behind it | [Page set](../planning/page-set.md) |
| Every type present, one page per type per topic | Correct. Say so and move on | none | — |

Report the mix as counts with the total, then one sentence of reading. The counts are `measured`; the reading is `hypothesis`.

## 3. Depth and breadth — what the tree does to a reader

| Shape | Reading | Fix class |
|---|---|---|
| Flat root, more than ~15 top-level items | Nothing is scannable, so readers stop scanning and start searching. Verify it: on-site search use per visit, and whether the top route begins at the search box | Group into a handful of sections. Navigation only — no URLs move |
| A branch with one child | Either a promise the corpus never kept, or grouping applied before there was anything to group | If the sibling pages are genuinely missing, a page-set decision. If not, flatten the branch |
| A branch with forty children | The section's own index is now a wall. Readers scroll it once and never again | Sub-group by job, and give the index page orientation rather than a link list |
| Depth beyond four levels | Anything at the bottom is effectively unreachable by browsing, whatever the sidebar shows | Promote; [Content detectors](../auditing/content-detectors.md) already flags depth as a per-page navigation defect, so report it once, at the higher severity, naming both |
| Depth wildly uneven across siblings — one branch at four levels, its neighbours at one | The tree encodes when the team wrote things, not what the reader is doing | Level the branches that carry comparable jobs |

Seven or so siblings stay scannable; past roughly fifteen the list stops being read. Neither number is a rule you enforce — they are the point at which you go and check the search and route data before recommending anything.

## 4. Entry points — a front door per audience

Take the audience map from [Demand gaps](../auditing/demand-gaps.md) as given. Deriving a second list of audiences here is the fastest way to make two readings disagree about who the product is for, and a reader who sees two lists trusts neither.

For each audience, three columns: is there a page that names them and their job; is it reachable in one click from the root; does it sequence them onward rather than ending. Most sites answer yes-yes-yes for exactly one audience — the one the founders were — and no-no-no for the rest.

> Audience map carries four: developer integrating the API (`capability`), platform team self-hosting (`capability`), non-technical owner evaluating (`inferred`), agency reselling (`speculative`). Entry coverage: 1 of 4. The root, the quick start and all six guides open with a code block. The evaluating owner has no page addressed to them anywhere, which is why no signal shows them failing — they never got far enough to fail.

Then collide it with data: which pages readers actually enter on, and in what proportion ([`get_route_patterns`](../../mcp/analytics/get-route-patterns.md) reports the routes, entry point first). An audience with a front door nobody enters through is a different finding from one with no door at all, and they need opposite work.

## 5. Progressive disclosure — is there a sequence at all?

Pick the primary audience, start at the root, and walk **only forward links** — no sidebar, no search, no back button. Record where you get to before the path forks with no guidance, or simply stops. That walk is the sequence the corpus actually offers; everything else is a sidebar the reader has to construct a curriculum from.

The failure this finds has one shape: every page is written as step three. Each assumes the reader arrived at the top, absorbed the vocabulary, and made the choices — and none of them says so, because prerequisites are a per-page rule that page-level audits check and pass when the page declares them. Declaring prerequisites correctly on forty pages still leaves a corpus with no order.

Output is an ordered path from first contact to competence, or the plain statement that none exists. The links that build it are writing and go to [Writing rules](../writing/writing-rules.md); the order itself is navigation and goes to [Site capabilities](../automation/site-capabilities.md).

## 6. Boundaries — split and merge are opposite, and the wrong call costs a rewrite

**Split test — one page doing three jobs.** All three must hold: the page contains sections belonging to more than one page type; its sections address readers at different competence levels; and where data exists, readers arrive on it from unrelated queries and leave at different anchors. Two of three is a page to watch, not a page to cut.

**Merge test — three pages doing one job.** All three must hold: from the titles alone, a reader cannot say which one answers their question; the pages share audience, type and job; and no one of them stands alone as a complete answer. Where search data exists, two URLs competing for the same query is the confirming evidence, and [Reader behaviour](../auditing/behaviour.md) calls it cannibalisation.

The asymmetry decides the default. A wrong split produces two thin pages and doubled maintenance — recoverable. A wrong merge deletes a URL, and with it every inbound link, ranking and citation pointing at it — not recoverable by editing. So **split on structural evidence, merge only with a number**.

> `/webhooks` covers what webhooks are, how to register one, and every payload field. Three types on one page, and the striking-distance band shows it ranking for both "what is a webhook" and "webhook payload schema" — two intents, one average position, neither served. Split into concept, how-to and reference. Contrast: `/billing`, `/billing-faq` and `/payments` all answer "how do I change my plan", none completely, and two of them rank for the same query. That is a merge, and it carries redirects.

## 7. Predictability — can a reader guess where it lives?

Take ten questions readers actually asked this site — failed searches, assistant questions, support threads. Never questions you wrote yourself: those measure your memory of the tree, not its guessability. For each, write down the section you would expect the answer in **before** looking. Then look, and score.

Below roughly seven hits in ten, the hierarchy is not guessable, and the corroboration is behavioural: on-site search used on most visits, and routes that begin at the search box rather than in the navigation.

What makes a tree guessable is naming, and three rules carry most of it. Sections are named for the reader's job, not the team that owns the feature — a "Platform" section named after an internal group is invisible to everyone outside it. No section is a product codename, because codenames are chosen by people who already know what is inside. Siblings are parallel in kind: all tasks, or all objects, never a mix, because a list that switches kinds mid-way stops being scannable at the switch.

## 8. Navigation as a claim about priority

The top level is a ranked assertion about what the product is about. Set it beside what readers actually come for — entry pages, the most frequent routes, the queries the site already ranks for — and where the two disagree, the number wins, provided it clears the sample floors in [Metrics](../auditing/metrics.md).

Two shapes recur. A top-level item with almost no entries occupying a prime slot, usually a feature the team was excited about at launch. And a top level ordered by build history or by internal team structure, where the first item is the oldest subsystem rather than the first thing anyone needs. Both are fixed by reordering and relabelling, which change no URLs and are the cheapest structural fix available.

Never reorder on raw pageviews: crawler traffic can be the overwhelming majority of them, and behavioural counts exclude bots while pageview totals do not — see [how measurement works](../../analytics/how-measurement-works.md) for which is which.

## 9. Scaling — and the redirect obligation on any move

The shape that works at 30 pages fails at 300, and the early signs arrive long before the failure. Watch for: new pages landing at the root because no existing branch fits them; one branch growing while its siblings stand still; sibling counts crossing fifteen; index pages that are bare link lists with no orientation; and the mix drifting toward reference as the product matures. At around 30 pages a flat tree is correct. Past roughly 100 it needs real sections with index pages that orient. Past roughly 300 it needs reference separated from narrative entirely, because the two are consulted in different ways and mixing them makes both harder to scan.

Then the rule that governs every recommendation above. **A reorganisation that changes URLs spends its own benefit on 404s** — every inbound link, every ranking, every bookmark and every URL an assistant has already cited. So: no structural recommendation leaves this reading without a URL map, old path to new, and a redirect for every page that moves. A move without a redirect is a defect being created, not a fix being applied. Prefer the changes that touch no URL at all — order, grouping, labels, index-page content — because they capture most of the benefit at none of the cost. Where URLs genuinely must change, move one section at a time and record `search_position` and `search_impressions` at the moment of the move, so the next run can tell a restructure that worked from one that quietly cost a quarter's rankings. [How indexing works](../../seo/indexing.md) covers what a redirect does to the canonical URL.

## What to hand back

In this order, `measured` census first so the readings that follow can be checked against it:

**A.** Census — page counts by type, depth per branch, sibling counts, entry-point inventory · **B.** Type-mix reading · **C.** Tree-shape findings · **D.** Entry coverage matrix per audience · **E.** The sequence to competence, or the statement that none exists · **F.** Split and merge queue, each with which test it passed · **G.** Guessability score, with the ten real questions quoted verbatim · **H.** Navigation versus demand, where data allowed the collision · **I.** Restructure plan with its URL map and redirect list.

Cut to five actionable items; everything below the cut is one line with a count. Then hand over: missing types, missing branches and missing front doors to [Deciding the page set](../planning/page-set.md); navigation order, grouping, labels and redirects to [Site capabilities](../automation/site-capabilities.md); the text of any split or merged page to [Writing rules](../writing/writing-rules.md); and any shape check worth repeating — a sibling count crossing its threshold, a page landing at the root — to [Monitoring](../automation/monitoring.md).

## Traps

- **Never estimate a distribution.** The census is countable and cheap; "about 80% reference" is an invented number in a reading whose whole authority is that it counted.
- **Never attach a traffic figure to a structural claim without its absolute count and window.** A shape finding dressed in a rate reads as measured when it is inference.
- **Never judge the type mix against a golden ratio.** The finding is an absent type, not a percentage that displeases you — an API product is meant to skew reference.
- **Never recommend a merge on shape alone.** A merge destroys URLs; it requires evidence that two pages compete, not an impression that they overlap.
- **Never propose a move without its redirect.** A restructure that breaks links pays for itself in 404s and is indistinguishable from vandalism to whoever linked in.
- **Never re-derive the audience map.** [Demand gaps](../auditing/demand-gaps.md) owns it. Two lists of audiences diverge on the first run and never reconcile.
- **Never report orphans, broken links or anchor text here** — [Internal linking](./internal-linking.md) owns them. A finding reported twice with two severities is worse than a finding not reported at all.
- **Never report a per-page type violation here** — [Content detectors](../auditing/content-detectors.md) owns it, with the severity table. This reading counts types; it does not judge one page against its type.
- **Never restructure a site that does not exist yet.** A new page set is [a creation decision](../planning/page-set.md), and second-guessing it here produces two conflicting structures.
- **Never run the guessability test on questions you wrote.** They measure your familiarity with the tree, and they always pass.
- **Never let a shape finding outrank a page measurably losing readers today.** Structure is the slow work; a failing page is this week's.
- **Do not mistake a small corpus for a broken one.** Fifteen pages with no sections is a correct shape, and recommending a hierarchy for it adds clicks and removes nothing.
- **Do not write anything.** No page, no navigation config, no redirect.

## Before you call it done

- [ ] A complete census exists — every page carries path, depth, sibling count, type and audience — and every count in the report traces to it.
- [ ] Type mix reported as counts with a total, judged against this product, with any absent type named.
- [ ] Pages that could not be classified are listed and handed to [Content detectors](../auditing/content-detectors.md), not assigned a type to tidy the table.
- [ ] Depth and sibling findings each name a fix class, and any depth finding already covered per page is merged rather than duplicated.
- [ ] Entry coverage audited against the audience map from [Demand gaps](../auditing/demand-gaps.md), with its tiers carried through unchanged.
- [ ] The forward-link walk was actually performed, and its result is either an ordered path or an explicit "no sequence exists".
- [ ] Every split names the three conditions it met; every merge carries a number, not an impression.
- [ ] The guessability test used ten real reader questions, quoted verbatim, with the score stated.
- [ ] Navigation-versus-demand collision either cites data above the sample floors or is stated as unavailable — never split the difference.
- [ ] Every recommendation that moves a page carries its old-to-new URL and a redirect, and a baseline is recorded before any move.
- [ ] Census labelled `measured`, every reading labelled `hypothesis`, and no shape finding placed above a measured page failure.
- [ ] Queue cut to five items, each with a named owner.

## Related

<!-- widget:cards plain cols=2 -->

- [Internal linking](./internal-linking.md) — the same corpus read as a graph: what is reachable, and from where. {git-fork}
- [Semantic SEO](./semantic-seo.md) — whether the concepts under the tree are covered, as opposed to where they sit. {network}
- [Search intent](./search-intent.md) — the page-type question asked one query at a time. {search}
- [Jobs to be done](./jobs-to-be-done.md) — why a persona-shaped tree produces pages nobody searches for. {target}
- [Content detectors](../auditing/content-detectors.md) — the per-page type rules this reading deliberately does not repeat. {list-checks}
- [Deciding the page set](../planning/page-set.md) — the structure a new site gets, before any of this applies. {layout-grid}

<!-- /widget -->
