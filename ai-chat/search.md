---
title: "Full-text search on your docs: how the index is built"
description: "What Docsbook's search index contains, how a query is parsed and ranked, what happens on a typo, and what a failed search tells you about a missing page."
tldr: "Docsbook indexes each page's plain text into Postgres full-text search, weighting titles above body and returning a highlighted snippet with the exact heading anchor. Reader search costs nothing. It has no typo tolerance — a misspelling returns nothing, and that miss is reported to you."
---

# Full-text search

Docsbook search is a Postgres full-text index over your pages, exposed as a search button in the header and a search box in the sidebar. It costs nothing per query — no model is called — and the queries that returned nothing are one of the two most useful signals your documentation produces.

## What you get

- **A search box in the header, the sidebar, or both.** Both can run at once; one is usually enough.
- **Results with a highlighted snippet** — a context window drawn from the page text around the match, not the first 200 characters of the page.
- **Deep links to the exact heading.** A match inside a section carries that section's real anchor, so the reader lands on the paragraph rather than at the top of a long page.
- **Translated pages first.** If the reader is on a translated locale, the translated row wins; untranslated pages still appear, so a half-translated site still searches whole.
- **A record of every search that returned nothing**, as a `search.no_results` webhook and a failed-searches report.

## How is the index built?

**Write-through on render, not on push.** A page enters the index when Docsbook renders it — after the response is sent, so indexing never delays the page. A translated page is indexed the same way when its translation is cached. There is nothing to rebuild by hand, and no reindex button.

The consequence is worth knowing: **a page nobody has opened since it was published is not in the index yet.** A brand-new site therefore searches thin until its pages have been visited once. Until any row exists at all, the search box falls back to matching filenames from the page list, so it is never empty-handed.

What goes into a row:

| Field | Contents |
|---|---|
| Title | Frontmatter `title`, else the page's H1, else the filename |
| Body | The page's plain text: frontmatter, heading markup, images, link syntax, fenced code blocks and inline markdown punctuation are stripped |
| Sections | One entry per `h2`/`h3`, carrying the heading's rendered anchor and its text, with `<pre>` blocks removed |
| Language | Empty for the original page, the locale code for each translation |

Search runs against a generated `tsvector` in which the **title carries weight `A` and the body weight `B`** — PostgreSQL's weight labels exist so that "words from different parts of a document [can be] weighted differently by ranking functions" ([PostgreSQL: Additional Text Search Features](https://www.postgresql.org/docs/current/textsearch-features.html)). That column is indexed with GIN.

## How is a query answered?

1. **Stopwords are stripped.** `websearch_to_tsquery` "combines unquoted text terms with the `&` (AND) operator" ([PostgreSQL: Controlling Text Search](https://www.postgresql.org/docs/current/textsearch-controls.html)), so a full sentence demands that the page contain every filler word too. A 45-word English stopword list is removed first, outside quotes only — so `"exact phrase"`, `OR` and `-word` still work.
2. **English queries are stemmed.** For English and untranslated content the query and the document are matched under the `english` configuration, which uses a Snowball stemmer that "reduce[s] common variant forms of words to a base, or stem, spelling" ([PostgreSQL: Dictionaries](https://www.postgresql.org/docs/current/textsearch-dictionaries.html)). Without it, a page that says "served" does not match a query that says "serve".
3. **Other languages use the stored index.** Non-English locales match against the stored `simple` vector, which "operates by converting the input token to lower case" and does not stem. English stemming rules applied to non-Latin text degrade to nonsense, so they are deliberately not applied.
4. **The English path normalises rank for length.** On English queries `ts_rank` runs with normalisation flag 1, which "divides the rank by 1 + the logarithm of the document length". Without it a 76 KB changelog that mentions every query term in passing outranks the short page that is actually about the question. The non-English path calls `ts_rank` with no normalisation flag, so on those locales a long page is not penalised for its length — see Limits.
5. **One row per page.** Original and translation collapse to a single result, preferring the reader's language, then rank. A title hit is promoted above body-only hits.
6. **The snippet is server-side.** `ts_headline` returns one fragment of 5–18 words around the match; the client re-highlights the terms.

## What happens on a typo?

**Nothing matches.** Docsbook search has no fuzzy matching, no trigram similarity and no edit-distance fallback. Stemming covers inflection — *serve* finds *served* — but not misspelling: *documnetation* finds nothing.

That is a deliberate trade rather than an oversight, and it comes with a compensating mechanism: **every zero-result query is reported to you.** The report is coalesced so one hunt is one signal, not one per keystroke:

- The browser waits **1.5 seconds** after the reader stops typing before reporting a miss, and flushes immediately if they close the dialog mid-hunt — measured on a live workspace, a reader typing one word paused 0.9–1.3 s between characters, which produced eight reports for one word before this existed.
- The server independently suppresses a miss that is a strict prefix extension of the previous one from the same reader inside a short window, because the endpoint is public and cannot assume any client debounced anything.

So `documnetation` reaching your failed-searches report is not a bug in search — it is search telling you a reader could not find the page, which is what you act on. Recurring misspellings are best fixed in your content, by naming the term the reader actually types.

## Where the search box goes

| Placement | Best for | Trade-off |
|---|---|---|
| Header button | First-time visitors, who look at the top bar first | Competes for space with your header links |
| Sidebar box | Readers who already navigate by the tree | Hidden on narrow screens where the sidebar collapses |

Turn the header button on in Float Widget → **Design** → **Header** → **Search button**. Turn the sidebar box on in Float Widget → **Design** → **Left Sidebar** → **Search in sidebar**. Both are free on every plan.

## Why this is the right way (evidence)

| Rule | Why it works | Source |
|---|---|---|
| Keep a lexical index even with semantic search available | Over 18 retrieval datasets, "BM25 is a robust baseline" in zero-shot settings while dense retrievers "often underperform" — your corpus is out-of-domain for any embedding model, and exact terms are what technical readers type | Thakur et al., 2021 — [BEIR](https://arxiv.org/abs/2104.08663) |
| Strip stopwords before the query reaches Postgres | `websearch_to_tsquery` ANDs unquoted terms, so one filler word absent from the page fails the whole match | [PostgreSQL: Controlling Text Search](https://www.postgresql.org/docs/current/textsearch-controls.html) |
| Stem English, do not stem other languages | The `simple` configuration only lowercases; Snowball stemmers are per-language and reduce variants to a stem | [PostgreSQL: Dictionaries](https://www.postgresql.org/docs/current/textsearch-dictionaries.html) |
| Normalise rank by document length (English path) | Flag 1 "divides the rank by 1 + the logarithm of the document length", so a long incidental mention cannot outrank a short page about the topic | [PostgreSQL: Controlling Text Search](https://www.postgresql.org/docs/current/textsearch-controls.html) |
| Weight the title above the body | Weight labels let ranking treat words from different parts of a document differently | [PostgreSQL: Additional Text Search Features](https://www.postgresql.org/docs/current/textsearch-features.html) |

The same index is one of the two retrievers behind [AI chat](./answer-quality.md#4-retrieval-runs-both-retrievers-every-time) — it is not a lesser fallback there either.

## Limits

- **No typo tolerance.** See above. If a misspelling matters for your audience, add the term to the page.
- **Code blocks are not searchable.** Fenced code is stripped before indexing, and `<pre>` blocks are removed from section text. A reader searching for a function name that appears only inside a code sample will not find it. Under question: the older docs claimed code blocks were indexed and "ranked below prose"; the indexer removes them outright.
- **Coverage depends on traffic, not on your repository.** A page enters the index on its first render. A published-but-never-opened page is missing from search results until somebody opens it.
- **We publish no latency figure.** English queries compute their `tsvector` at query time rather than reading the stored `simple` index, which means the English path does more work per query as a corpus grows. We have not published a benchmark, and we will not quote one until we have.
- **Length normalisation is English-only.** The English query path passes `ts_rank` normalisation flag 1; the path used for other locales calls `ts_rank` with no flag at all, which means no length normalisation. On a non-English site a very long page can therefore outrank a short page that is more precisely about the query. Under question until the two paths are reconciled.
- **Search is per project.** The index is scoped to one workspace; there is no cross-project search.
- **The failed-search signal is coalesced, not exact.** The first miss of a typing chain is what gets delivered to a live webhook, so the delivered query can be a shorter prefix of the one the reader settled on. The historical report recovers the settled query.

## Related

- [AI chat](./chat.md) — the assistant that uses this index as one of its retrievers.
- [Answer quality](./answer-quality.md) — how lexical and vector retrieval are merged.
- [Analytics: what readers searched for](../analytics/tracking/overview.md) — the queries that returned nothing.
- [Page feedback](./feedback.md) — the other signal that a page is missing or misnamed.
