---
title: "Programmatic SEO: one question asked N times with one variable changed"
description: "How to tell a real page family from index bloat — finding a dimension with a machine-readable value list, applying the regeneration gate, sizing it, and running the swap test."
tldr: "A family is a repeating axis — integrations, error codes, SDK languages, regions — whose values come from a source of truth a machine can reread. Most documentation sites do not have one, and saying so is the more valuable half of this reading: an unviable family produces hundreds of near-identical pages that rot the moment the underlying list changes."
---

# Programmatic SEO

Every other reading in this handbook reads pages one at a time. It opens a page, judges it, scores it, and moves to the next. That is the correct way to find a bad page and the wrong way to find a missing *family*, because a family is not visible in any single page — it is visible only in the shape of the demand behind it. Forty people asking "how do I connect this to Postgres / MySQL / BigQuery / Snowflake" are asking one question with one variable changed, and a page-by-page reading sees four unrelated gaps of low individual weight, prioritises none of them, and never notices that the product's connector registry already lists thirty-one values of that variable.

This reading runs on the dimension, not the page. It asks whether the product carries a repeating axis — integrations, error codes, SDK languages, endpoints, model names, file formats, regions, framework combinations, plan tiers — whose values are enumerable from the product's own data, and whether that axis justifies a page family generated from a source of truth rather than written by hand. Just as often the honest finding is that it does not, and saying so is the more valuable half.

The failure this exists to prevent is expensive in both directions. Not building a viable family leaves the entire long tail of a real dimension unaddressed while the team rewrites the same twelve pages harder. Building an unviable one produces hundreds of near-identical pages that dilute the site's own search results, bury the concept pages in internal search, consume the crawler's attention on rows nobody was ever shown, and rot the moment the underlying list changes — because nobody remembers there are two hundred pages quoting a limit that moved. A rotted family is worse than no family: it is N pages asserting a wrong fact with the site's authority behind each one.

## What this reading owns, and what it does not

| This reading owns | It does not own → who does |
|---|---|
| Detecting a repeating dimension in the product and enumerating its values from a machine-readable source | Which concepts and entities the docs should cover at all → [Semantic SEO](./semantic-seo.md) |
| The regeneration gate: can a machine rebuild this family unattended | The intent behind any individual query → [Search intent](./search-intent.md) |
| The unique-value floor and the swap test for thin generated content | Where a family sits in the navigation tree and its depth → [Content architecture](./content-architecture.md) |
| Family sizing: whether N values justify a programme or four hand-written pages | Which jobs and audiences the product serves → [Demand gaps](../auditing/demand-gaps.md) |
| Index bloat, duplicate templates, near-identical titles, family pollution of internal search | Rewriting one member's title to move it from position 9 to 4 → [Reader behaviour](../auditing/behaviour.md), striking-distance band |
| Hub page, canonicalisation and pagination requirements for a family to be discoverable | Whether a value list on a marketing page is factually true → [External checks](../auditing/external-checks.md) |
| The pruning verdict on an existing family | Executing the prune, the redirects or the merge → [the apply gate](../writing/from-finding-to-change.md) |
| The family specification handed onward | Writing any page in the family → [Deciding the page set](../planning/page-set.md); the refresh trigger → [Automation](../automation/README.md) |

The overlap that must never happen: a member page that ranks at position 11 with impressions and no clicks is striking-distance work, reported once, there. This reading reports the family, not its individual rows.

## When is this reading worth the time?

- The product exposes a list the docs address in prose: "we support the major clouds", "connectors for popular tools", "a full set of error codes". Prose covering a list is the signature of a dimension nobody enumerated.
- Failed searches or unanswered questions repeat one phrasing with a different noun in the slot — the cheapest possible evidence that a dimension has demand.
- A family already exists and nobody has ever audited it. This is the most common real case, and the one where the reading returns a pruning verdict rather than a build plan.
- The product shipped a registry, a plugin system, an SDK matrix or a region list, and the docs gained one reference page listing the values.
- **Not when** the product has no repeating axis with a machine-readable source. Most documentation sites do not have one. Inventing a dimension to justify a programme is the failure this reading exists to prevent, and it is worse than skipping it, because the output looks like a plan and costs a quarter.
- **Not when** a measured failure is still open. A page losing real readers outranks any proposed family, every time.

## Evidence tiers

This reading is two-tiered by half. Proposing a new family is inference and uses the `capability` / `inferred` / `speculative` vocabulary from [Demand gaps](../auditing/demand-gaps.md); auditing an existing family reads real data and uses `measured` / `hypothesis`.

| Half | Tier vocabulary | Rule |
|---|---|---|
| Proposing a family | `capability` — the value list read directly from a registry, spec, config or package index, cited by path. `inferred` — the demand pattern, derived from repeated phrasings in failed searches or question clusters. `speculative` — a dimension nobody's data supports | The whole proposal half is `hypothesis`. Say so once, up front |
| Auditing an existing family | `measured` — membership counts, `search_impressions`, `organic_ctr`, entrances per member, over one stated window. `hypothesis` — the swap-test verdict, which is a reading of text | Never present a swap-test verdict as if it were traffic data |

The value list itself is never `inferred`. Either you read it from a source you can name, or the dimension does not exist for the purposes of this reading.

## 1. Find the dimension — enumerate, never guess

Look for the axis in the product's own data, not in the docs' table of contents. The docs are the artefact you are auditing; using them to enumerate the dimension guarantees you find exactly the values somebody already wrote about.

| Candidate dimension | Where its values are enumerable | Not a dimension when |
|---|---|---|
| Integrations, connectors | Plugin or connector registry, `integrations/` directory, connector config | The only list is a marketing page |
| Error codes | The error enum or constant table in source, the status-code map | Codes appear only inside prose |
| SDK languages | Published packages on their registries, per-language repository directories | A language is announced but unpublished |
| API endpoints | The OpenAPI or schema document | Routes are documented by hand and drift from the router |
| Model or provider names | The model registry or provider config constant | The list is a screenshot |
| File formats | The parser or exporter registry | Formats are named in a feature bullet |
| Regions, data centres | Infrastructure or deployment config | A region is on the roadmap |
| Framework combinations | The example-app directory, the CI test matrix | The combination has never been run |
| Plan tiers | Billing configuration, verified against the live pricing page by [External checks](../auditing/external-checks.md) | Tiers differ between billing and marketing — that is a finding, not a dimension |

**The rule that decides most runs: a dimension with no source of truth in the repository or an addressable API is not a dimension, it is a wish.** Write it down as `speculative`, state which source would settle it, and stop. Enumerating from a marketing page is the specific trap — marketing lists are aspirational, and a family generated from one produces pages documenting capabilities the product does not have, which is the single most expensive output an audit can produce.

Then compare the two counts, and read the gap in both directions:

> The docs name six integrations across three pages. The connector registry has thirty-one entries. The twenty-five unwritten values are the candidate family; the six hand-written pages are evidence that somebody has been maintaining this by hand and losing.

> The website lists forty integrations. The registry has twelve. Twenty-eight pages here would document things the product cannot do. The finding is a marketing-versus-product contradiction — hand it to [External checks](../auditing/external-checks.md) — not a family.

## 2. The regeneration gate — apply it before anything else

Nothing downstream matters if this fails, so run it second and abandon early. Five questions, all of which must answer yes:

1. Is the value list readable by a machine at a stable path or endpoint?
2. Does adding, renaming or removing a value change that source *first*, before anyone touches documentation?
3. Can each page's value-specific content be derived from structured data without a human writing a judgement per page?
4. Is there a named owner and a concrete trigger that reruns generation?
5. Does removing a value produce a redirect rather than a 404?

A family maintained by hand rots at N times the rate it was built, and the rot is invisible: a stale generated page is byte-for-byte indistinguishable from a healthy one, so no [content detector](../auditing/content-detectors.md) flags it and no reader reports it — they just act on the wrong limit. Any "no" here means the honest output is **hand-written pages, capped at the number the team will actually maintain**, handed on as ordinary gaps. That is a legitimate verdict and it is common.

## 3. Sizing — four values is four pages, not a programme

| Values | Verdict |
|---|---|
| 1–5 | Hand-written pages. The template, the generator and the refresh trigger cost more than writing five pages once |
| 6–15 | Borderline. Programmatic only if the gate passed **and** the per-value data is already structured. Otherwise hand-write the highest-demand values and put the rest in one table on one page |
| 16–100 | The band where a family pays for itself |
| 100+ | A family plus a hub strategy, and prune *before* generating — a value nobody asks about is index bloat that has not happened yet |

Never generate a cross-product because the arithmetic is impressive. Twelve frameworks by eight databases is ninety-six pages, and it is where index bloat is born. A combination earns a page only when the two values interact — a different install step, a different auth shape, a genuinely different failure — and generating the ones that do not is generating ninety pages that fail §4 by construction.

## 4. The unique-value floor — the swap test

**The test:** take a generated page, replace every occurrence of the variable with another value from the same dimension. If the page still reads correctly, it carries nothing but the template and has no reason to be indexed.

Each member must carry at least two of the following, and they must come from the source of truth rather than from prose:

- A code sample that would not run for another value.
- Value-specific limits, quotas, rate limits or version constraints.
- A value-specific failure mode with its actual message text.
- A step other values do not have — a different auth shape, an install that differs beyond a package name.
- Value-specific structured data prose cannot carry: supported fields, region latency, what the code actually means.

> `/integrations/slack`, `/integrations/discord`, `/integrations/teams`, each reading: "Connect X to receive notifications. 1. Open Settings. 2. Paste the webhook URL. 3. Save." Swap Slack for Discord and every sentence stays true. Three pages carrying one page of information. Verdict: one page with three tabs, plus the payload-shape table that genuinely differs between them.

If fewer than two hold for **most** values, the family collapses into one page with a table. Report that as the finding. Collapsing a would-be forty-page family into one good page is a better outcome than shipping forty, and it is the outcome roughly as often as the alternative.

This is also the shape search engines say they do not reward. Google's own guidance puts content made primarily to attract search visits outside what its systems seek to reward ([Creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)), and practitioners report bulk near-identical pages with no named expert as the biggest losers of recent core updates — one agency account puts 24% of top-10 pages out of the top 100 after the March 2026 update, concentrated in exactly that kind of page. Quote the mechanism, not that number: it comes from a single write-up with no published method ([Rush Agency field report, 2026](../evidence/sources.md#how-search-changed-in-2026-and-how-to-rebuild-for-ai-answers)).

## 5. Template shape and the variable surface

Specify which parts of the template are fixed and which are value-derived, because the boundary is what stops a generator producing duplicates.

- **Title carries the variable and the job**, never the variable and a category noun. "Slack integration" is a label forty of its siblings also wear; "Send build alerts to a Slack channel" is a page. This is the family-scale version of the title patterns in [Reader behaviour](../auditing/behaviour.md) — cite them, do not restate them.
- **Description is generated per value from value-specific data.** One description string repeated across forty pages is a duplicate-template signal to a search engine and a critical duplicate finding in [Content detectors](../auditing/content-detectors.md).
- **A value that cannot fill the value-derived slots does not get a page.** Generating a page with empty slots is how a family fills with thin members that later have to be pruned.

## 6. Hub, canonical, pagination

A family without a hub page is a set of orphans, and it will arrive as N high-severity orphan findings from the link detector, whose real fix is one page.

- **One hub** listing every member, linked from the navigation, and itself worth ranking for the category query. It is a page with a job, not an index.
- **Every member is self-canonical.** Never canonicalise a member to the hub — that de-indexes the family you just built. Never canonicalise near-identical members to one "best" member either; needing to is an admission the family failed §4. [How indexing works](../../seo/indexing.md) covers what a canonical does and how the sitemap is built.
- **Pagination on the hub only** when the list outgrows one page, every member stays within one click of the hub, and the sitemap carries the family as a section so a crawler reads the members as a set. Depth kills the tail of a family faster than anything else.
- **Members link back to the hub and to two or three siblings chosen by relatedness**, not alphabetically. Alphabetical sibling links are how the doc graph gains edges no reader ever walks — a broken journey in [Reader behaviour](../auditing/behaviour.md)'s terms, and a topology finding in [Internal linking](./internal-linking.md)'s.

## 7. Index bloat — detecting the cost in a corpus that already has one

| Symptom | Detection | What it costs |
|---|---|---|
| Near-identical titles | Group titles by their template skeleton with the variable stripped; flag skeletons with more than five members | Five near-identical rows in a result list means nothing gets chosen — the rejected-search pattern at family scale |
| Duplicate descriptions | Exact-match description strings across the corpus | A duplicate-template signal, and a critical finding in [Content detectors](../auditing/content-detectors.md) |
| Dead weight | Members with zero `search_impressions` across the whole window while the hub has impressions | The crawler's attention and the site's own authority spent on rows nobody was shown |
| Internal search pollution | Run the family's category term in the site search; count family members in the first ten results | A reader searching "webhook" gets ten connector pages and never reaches the concept page |

**Crawl budget itself is not observable from your own analytics, and pretending otherwise is inventing a number.** What is readable is search rankings, impressions, reader behaviour, failed searches and the doc graph; crawl statistics are not among them. The honest proxy is "members that have never received an impression". If the owner can supply a server-log sample or a crawl-stats export, say what it would add — which members the crawler visits and how often — and read it as supplied data. Without it, report the proxy and label it as the proxy.

## 8. Auditing a family that already exists

1. **Enumerate membership** from the URL pattern and the doc graph. State the count in the first line; an audit of "the integrations pages" without a number is not an audit.
2. **Pull per-member performance** over the one window the run already fixed. Split three ways: **earning** (impressions and clicks), **shown and refused** (impressions, no clicks — hand to the striking-distance band, do not fix it here), **never shown** (zero impressions).
3. **Sample the swap test** across five members drawn across the performance distribution, not the five best.
4. **Verdict per member**: keep · merge into the hub · prune with a redirect.
5. **Propose, never execute.** The redirect plan and the merge happen at [the apply gate](../writing/from-finding-to-change.md).

Two rules that stop this producing damage. **Never prune on zero impressions inside a window shorter than a full indexing cycle** — a member published three weeks ago is young, not dead, and pruning it destroys a page before it was ever tested. And **never prune a member serving a real customer segment on search numbers alone**: a connector used by four paying customers has no search demand and every reason to exist. Name it, state that the search data cannot judge it, and let a human decide.

> Family: 84 members under `/integrations/`. 61 have never received an impression in the window. 9 of 10 sampled members fail the swap test. Verdict: keep the 23 that earn, merge the rest into a hub table with per-connector configuration rows, redirect the 61. `measured` on membership and impressions, `hypothesis` on the swap-test share.

## 9. The family specification — the only artefact this reading produces

| Field | Content | Consumer |
|---|---|---|
| Dimension | The variable, its value list and the count | Page set |
| Source of truth | The exact path or endpoint the list is read from, and who owns it | Page set, automation |
| Template shape | Sections, marked fixed or value-derived | Page set |
| Unique-value contract | Which two of the five §4 items each member carries, and the rule that a value which cannot fill them gets no page | Page set |
| Hub page | Its URL, its own job, its links | Page set |
| Canonical and sitemap rules | Self-canonical members, family sitemap section | Writing and publishing |
| Refresh trigger | The event that reruns generation, and the behaviour on add, rename and remove | [Drift](../automation/drift.md) and [Events](../automation/events.md) |

## What to hand back

**A.** The dimension, its source of truth, and the gate verdict — pass, or fail with the reason. **B.** Sizing verdict and the resulting shape: programme, hand-written pages, or one page with a table. **C.** For an existing family: membership count, the three-way performance split with absolute counts, the swap-test sample and the pruning verdict. **D.** Index-bloat findings with the detection used for each. **E.** The family specification, or the explicit statement that no viable dimension exists.

Then hand over: the specification and the hub page to [Deciding the page set](../planning/page-set.md); the refresh trigger to [Drift](../automation/drift.md); canonical, sitemap and any redirect plan to [the apply gate](../writing/from-finding-to-change.md). This reading writes nothing and generates nothing.

## Traps

- **Never invent a value.** Every member traces to the source you read and named. A plausible-looking integration that does not exist becomes a page promising a capability the product does not have — the most expensive output available here.
- **Never attach a volume or a traffic forecast to a proposed family.** "40 pages × 200 visits" is the sentence that spends a quarter.
- **Never propose a family whose regeneration gate failed.** Hand-written pages, capped at what someone will maintain, is the honest answer and it is frequently the right one.
- **Never take a marketing page as the source of truth for a value list.** It is aspirational and it is an external claim; verifying it belongs to [External checks](../auditing/external-checks.md).
- **Never let a proposed family outrank a measured failure**, and never report a swap-test verdict with the weight of traffic data.
- **Do not rewrite an individual member's title for rank here.** That is the striking-distance band; reporting it in both places gets the same finding two severities.
- **Do not decide where the family sits in the tree** — [Content architecture](./content-architecture.md) owns placement. This reading names the hub and its members and hands the position over.
- **Do not map the concept space or characterise the intent behind member queries** — [Semantic SEO](./semantic-seo.md) owns the concepts, [Search intent](./search-intent.md) owns query shape. A family is one concept repeated, not a model of the concepts.
- **Do not generate or prune anything.** The prune is a proposal with counts, executed after the apply gate.
- **Do not fill a coverage claim with the family's size.** Eighty-four pages nobody was shown is not coverage; it is the finding.

## Before you call it done

- [ ] Exactly one dimension is named per family examined, with the path or endpoint its values were read from.
- [ ] The regeneration gate was answered on all five questions before any template, sizing or unique-value work.
- [ ] The value count is stated, and the sizing verdict follows the band table rather than ambition.
- [ ] The swap test was run on real page text, on a sample drawn across the performance distribution, and its verdict is labelled `hypothesis`.
- [ ] Where an existing family was audited: membership count, the three-way split with absolute counts on the single run window, and a per-member verdict of keep / merge / prune, unexecuted — and no crawl statistic quoted that nothing can read.
- [ ] Members below the impression floor for less than a full indexing cycle were excluded from pruning and the exclusion counted.
- [ ] The family specification carries all seven fields, or the report states plainly that no viable dimension exists.
- [ ] Nothing was written, generated or redirected; every handover names its owner.
- [ ] No finding duplicates a striking-distance, concept-space, query-intent or navigation finding owned by a neighbour.

## Related

- [Semantic SEO](./semantic-seo.md) — whether the concepts behind the dimension are covered at all.
- [Search intent](./search-intent.md) — what shape each member page has to be.
- [Content architecture](./content-architecture.md) — where the hub and its members belong in the tree, and what the sibling count does to a reader.
- [Internal linking](./internal-linking.md) — the hub-and-member edges, and what happens to a family with no inbound body links.
- [How indexing works](../../seo/indexing.md) — canonical URLs, the sitemap and what actually gets a page into an index.
- [Drift](../automation/drift.md) — keeping a generated family honest when the source list changes.
