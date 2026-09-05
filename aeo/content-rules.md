---
title: "Content rules for answer engines, and which ones we enforce"
description: "The numbered rules Docsbook writes documentation by, what each one does to the machine that answers with your page, and whether Docsbook enforces, checks or merely advises it."
tldr: "Ten rules, each with the retrieval behaviour that justifies it and the source that establishes it. Five are enforced by code — the chunk boundary, the heading anchor, the evidence-per-number check, generated prices, and the title and description precedence. Two are checked and reported. Three are advice the writing agents follow and nothing verifies afterwards."
---

# Content rules for answer engines

An answer engine never shows your page. It shows a passage from it, or a sentence rebuilt out of one, and the reader stops there. So the unit you are writing is the section, not the document — and the rules below are the ones Docsbook applies to sections, each with the mechanism it acts on and the source that establishes it.

Three things this page is not. It is not the markup layer — that is [Structured answers](./structured-answers.md). It is not the list of what raises citation odds once you are already retrieved — that is [Citation signals](../geo/citation-signals.md), which owns the measured effect sizes and the things not to do. This page is the writing rules and, for each one, an honest answer to the only question that matters when a vendor states a rule: *does your product actually do this, or is it telling me to?*

## What the three enforcement labels mean

| Label | What it means | What happens if you break the rule |
|---|---|---|
| **Enforced automatically** | Code does it, or refuses to ship output that breaks it | You cannot break it through Docsbook; the behaviour is not configurable |
| **Checked and reported** | Code measures it and shows you the result | Nothing changes on its own; you get a finding with the evidence under it |
| **Advised only** | An instruction the writing agents follow when they draft | Nothing verifies it afterwards, including when a human writes the page |

## The rules at a glance

| # | Rule | Enforcement |
|---|---|---|
| 1 | One page answers one job, in the shape that job takes | Advised only |
| 2 | Write the heading as the question the reader typed | Advised only |
| 3 | Every section must be readable with nothing above it | Enforced automatically |
| 4 | Heading levels are a contract, not a style choice | Advised only |
| 5 | The heading text owns its anchor — never write one by hand | Enforced automatically |
| 6 | The answer has to be in the bytes, before any JavaScript runs | Checked and reported |
| 7 | Every number in a claim names the thing that produced it | Enforced automatically |
| 8 | Prices, limits and versions are copied, never inferred | Enforced automatically (generated pricing pages) |
| 9 | The title and the description are written, not scraped off the H1 | Enforced automatically |
| 10 | A page nothing links to is a page nothing retrieves | Checked and reported |

---

## Rule 1 — One page answers one job, in the shape that job takes

A tutorial, an explanation, a how-to, a reference table and an FAQ are five different shapes, and mixing them produces a page that answers no question completely. When Docsbook generates a site it writes them as separate pages with separate briefs: explanation pages get noun-phrase headings and no commands, how-to pages get a title of the form "How to *accomplish specific goal*" and numbered goal-oriented steps with no background theory, reference pages get one table per group.

**What it does to an answering agent.** The engine is matching a question type to a passage type. A conceptual question retrieves badly against a page whose sections are imperative steps, and a procedural question retrieves badly against prose that explains why. The how-to shape has a second, mechanical consequence in Docsbook: a heading that starts "How to" followed by a numbered list of three or more steps is exactly what the `HowTo` detector reads, so writing the shape correctly also produces the markup — see [Structured answers](./structured-answers.md).

**Evidence.** Google's helpful-content self-assessment asks whether "the main heading or page title provide a descriptive, helpful summary of the content", and separately whether it "avoid[s] exaggerating or being shocking in nature" ([Google, creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)). A page title that names one job satisfies both by construction. The split into five shapes is Docsbook's own practice; no public source measures it.

*Advised only.* The shapes live in the page briefs the generator follows. Nothing checks a hand-written page against them.

## Rule 2 — Write the heading as the question the reader typed

Not "Rate limiting" but "What happens when I hit the rate limit?". Use the reader's words, not the internal noun for the subsystem.

**What it does to an answering agent.** It puts the query text inside the document. Retrieval scores the similarity between a question and a passage, and the cheapest way to raise that score is for the passage to contain the question. This is the same effect document expansion exploits deliberately: Nogueira et al. predict "which queries will be issued for a given document" and append them to it, reporting "state of the art in two retrieval tasks", with retrieval alone approaching the effectiveness of far more expensive neural re-rankers ([arXiv 1904.08375](https://arxiv.org/abs/1904.08375)). A question heading is that expansion, written by the person who already knows which question the section answers. In Docsbook it is also a detector input — an `###` heading ending in a question mark becomes a `Question` in `FAQPage` markup.

**Evidence.** [arXiv 1904.08375](https://arxiv.org/abs/1904.08375), plus the mechanism above. Note what no source supports: nothing published says a question heading wins you a featured snippet. Asked how to mark a page as one, Google answers "You can't. Google systems determine whether a page would make a good featured snippet for a user's search request, and if so, elevates it" ([Google, featured snippets](https://developers.google.com/search/docs/appearance/featured-snippets)).

*Advised only.* The writing agents phrase headings this way; nothing rewrites a heading you wrote.

## Rule 3 — Every section must be readable with nothing above it

A section that begins "As mentioned above, this defaults to 30 seconds" is unusable the moment it is separated from the paragraph it refers to — and it will be separated, on the first retrieval.

**What it does to an answering agent.** Docsbook indexes your docs at **heading granularity** by default: one embedded unit per section, not per page. Each unit's embedded text is prefixed with the section's full heading breadcrumb — `Billing > Refunds > Limits` — precisely because a section called "Limits" means something different under Webhooks than under AI chat, and the vector has to carry that. Units are capped at **6,000 characters**; a section longer than that is truncated, so a fact buried at the end of a very long section is not in the vector at all. At line granularity, paragraph blocks of 20 characters or fewer are dropped as noise.

**Evidence.** Retrieval granularity is a measured variable, and finer, self-contained units win. Chen et al. compare document, passage and sentence units against "propositions" — "atomic expressions within text, each encapsulating a distinct factoid and presented in a concise, self-contained natural language format" — and report that "indexing a corpus by fine-grained units such as propositions significantly outperforms passage-level units in retrieval tasks" ([Dense X Retrieval, arXiv 2312.06648](https://arxiv.org/abs/2312.06648)). The vendor-side version of the same finding, and the failure mode it produces in prose that does not name its own subject, is on [Citation signals](../geo/citation-signals.md).

*Enforced automatically* — for the half Docsbook owns. The breadcrumb prefix, the unit boundary and the cap are applied to every page with no setting to change them. The half you own is the prose: nothing can restore a subject you did not name.

## Rule 4 — Heading levels are a contract, not a style choice

Use H2 for a section, H3 for a question inside it, and do not skip a rank to get a smaller font.

**What it does to an answering agent.** Two things. The heading tree is what splits your page into the units of Rule 3, so a skipped level puts a section under the wrong parent and gives its vector the wrong breadcrumb. And Docsbook's FAQ detector reads exactly one shape: an H2 section whose H3 children are the questions, or any H3 ending in a question mark. An FAQ written with H3 sections and H4 questions produces no markup at all, silently — the commonest AEO failure we see.

**Evidence.** "Headings communicate the organization of the content on the page. Web browsers, plug-ins, and assistive technologies can use them to provide in-page navigation", and "Skipping heading ranks can be confusing and should be avoided where possible: Make sure that a `<h2>` is **not** followed directly by an `<h4>`" ([W3C WAI, headings](https://www.w3.org/WAI/tutorials/page-structure/headings/)).

*Advised only,* and this is a real gap: nothing in Docsbook warns you that you skipped a level or that your FAQ section matched nothing. Verify with a validator — see [Structured answers](./structured-answers.md).

## Rule 5 — The heading text owns its anchor; never write one by hand

Deep links, search results and AI citations all point at `page#anchor`. Every one of those anchors is derived from the heading text by the same library the renderer uses, and no other code is allowed to guess at one.

**What it does to an answering agent.** A citation whose anchor does not exist lands the reader at the top of a long page, having been promised a specific section. Nothing throws; the link is simply wrong. Docsbook computes anchors by calling `github-slugger`, which is what `rehype-slug` uses when the page is rendered, so the precomputed anchor and the rendered `id` cannot disagree. Before that was centralised, a hand-rolled slugifier was measured against this repository's own corpus: **1,386 of 21,827 headings — 6.3% — produced an anchor that was not the id on the page, and 263 came out as nothing but dashes.** 314 of the mismatches were on pure-ASCII headings ("Edge cases & errors" collapses one separator too many); the rest were non-Latin, where every heading of a Russian-language site collapsed to the same dead anchor.

**Evidence.** The measurement above is from this repository, not from a published study; treat it as our own number. There is no external source for it, and none is needed — the rule is that a string with an owner gets asked, not re-derived.

*Enforced automatically.* Anchors are computed in one place for every consumer.

## Rule 6 — The answer has to be in the bytes, before any JavaScript runs

If the prose only appears after a browser executes a script, an assistant fetching the URL receives a shell.

**What it does to an answering agent.** Nothing at all — which is the point. This failure is invisible to every check that reads your Markdown, because nothing is wrong with the Markdown. Docsbook's `audit_geo` fetches sampled pages without a JavaScript engine and asks whether at least **200 words** of body prose survive stripping the tags; below that the page is reported as a **critical** finding, on the reasoning that navigation labels, a cookie banner and a title tag alone can clear a lower bar. It runs the same check against named assistant user agents, so a CDN that serves a browser a page and an assistant a challenge shows up as a separate finding.

**Evidence.** Google's guidance for AI Overviews and AI Mode is explicit that the fix is textual content, not markup: "Making sure that important content is available in textual form", alongside "Ensuring that crawling is allowed in robots.txt" — and, in the same document, "You don't need to create new machine readable files, AI text files, or markup to appear in these features" ([Google, AI features](https://developers.google.com/search/docs/appearance/ai-features)). Perplexity describes `Perplexity-User` as visiting a page when a user asks a question, in order to "help provide an accurate answer and include a link to the page in its response" ([Perplexity, bots](https://docs.perplexity.ai/guides/bots)) — a fetch with no browser in it.

*Checked and reported.* Docsbook's own pages are server-rendered, so a Docsbook-hosted site passes this by construction; the check exists for the sites it audits.

## Rule 7 — Every number in a claim names the thing that produced it

A sentence containing a figure must be traceable to the observation that produced the figure — not to a plausible recollection of one.

**What it does to an answering agent.** A wrong number is the one error that survives correction: an assistant repeats it, and the repetition outlives your edit. Docsbook enforces this on everything its agent tools emit. Each finding carries `evidence_refs` pointing at named evidence entries, and the contract validator scans the finding's own text for digits: any number that does not appear in the evidence it cites is a violation, and the payload is sent back to the model to repair rather than returned to you. The only exemptions are the single digits 0–9 plus 10 and 100 — ordinals and small counts inside ordinary prose. The scoring is done by plain code over the gathered evidence, not by the model, because a 0–100 written by a language model is not comparable to the same number written by the same model next week.

**Evidence.** Google's helpful-content questions ask whether "the content present[s] information in a way that makes you want to trust it, such as clear sourcing, evidence of the expertise involved" ([Google, creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)). The measured version — that adding statistics and citing sources raises how much of a generated answer is attributed to you — is on [Citation signals](../geo/citation-signals.md), which owns those effect sizes.

*Enforced automatically,* for agent output. A number you type into a page yourself is not checked by anything.

## Rule 8 — Prices, limits and versions are copied, never inferred

Every price and every stated limit on a generated page is copied verbatim from source material read in that run. A plan whose price is not in the source is written as "Contact sales".

**What it does to an answering agent.** Pricing is the single most-quoted fact about a product and the one a reader acts on. An inferred "typical" price is indistinguishable from a real one once an assistant repeats it. Docsbook's generator carries the rule in the brief, and the anonymous pipeline goes further: if a crawl surfaced no prices at all, the pricing page is **not written**, on the reasoning that a pricing page with guessed numbers is worse than no pricing page.

**Evidence.** Google's structured-data policy requires that markup be "a true representation of the page content" and forbids marking up content not visible to readers ([Google, structured data guidelines](https://developers.google.com/search/docs/appearance/structured-data/sd-policies)); Google's AI-features guidance asks that "structured data matches the visible text on the page" ([Google, AI features](https://developers.google.com/search/docs/appearance/ai-features)). Neither says anything about invented prices — that part is Docsbook's own rule, and we state it as ours.

*Enforced automatically* for the generated pricing page, which is dropped rather than guessed. Elsewhere it is an instruction in the brief.

## Rule 9 — The title and the description are written, not scraped off the H1

Frontmatter `title` wins over the body H1, which wins over the filename. Frontmatter `description` wins over the first body paragraph.

**What it does to an answering agent.** The title and description are the two strings a machine reads before it reads anything else, and both have a failure mode that is invisible on the page. Deriving the title from the H1 means an author who edits frontmatter to control the search result changes nothing, and it lets the brand name be appended twice — burning a third of a search result's line on repetition. Deriving the description from the body means widget markup and the remains of a card list leak into what a reader is shown. Docsbook fixes the precedence in one place and truncates at a word boundary, cutting at a sentence end when one is available: **160 characters** for `<meta name="description">` and **400** for Open Graph and the JSON-LD `description`, both filled from the same authored string so the two can never disagree.

**Evidence.** "Snippets are primarily created from the page content itself", and Google recommends "unique descriptions for each page" ([Google, snippet](https://developers.google.com/search/docs/appearance/snippet)). For titles: write "descriptive and concise text", avoid "repeated or boilerplate text", and "brand your titles concisely" ([Google, title link](https://developers.google.com/search/docs/appearance/title-link)).

*Enforced automatically* for the precedence and the truncation. The **lengths are Docsbook's own budget, not a published limit** — see Limits.

## Rule 10 — A page nothing links to is a page nothing retrieves

Every page should be reachable from at least one other page, and every link on it should resolve.

**What it does to an answering agent.** Crawlers find pages by following links; a page that only exists in the sitemap is a page a crawler has one weak reason to fetch and no reason to consider important. Docsbook builds a link graph over the whole doc set and counts, per page, incoming links and unresolved links. A page with broken links or with zero incoming links is flagged in the doc-graph card with the fix offered as an action.

**Evidence.** Google's list of what actually helps a page appear in AI Overviews and AI Mode includes "Making your content easily findable through internal links on your website" ([Google, AI features](https://developers.google.com/search/docs/appearance/ai-features)).

*Checked and reported.* Nothing adds a link for you unless you ask an agent to.

## Limits and open questions

- **Half of the list does not stop you doing the wrong thing.** Rules 1, 2 and 4 are instructions the writing agents follow when they draft; Rules 6 and 10 are reported after the fact; Rule 8 is hard-enforced only on the generated pricing page. If you write a page by hand — or edit one an agent wrote — nothing in Docsbook checks it against this list. A linter that reports skipped heading levels and FAQ sections that matched no detector does not exist yet, and Rule 4 is the rule that fails most often and most silently.
- **The character budgets in Rule 9 are ours, not Google's.** Google publishes no character limit at all: "there's no limit on how long a `<title>` element can be", and the title link "is truncated in Google Search results as needed, typically to fit the device width" ([Google, title link](https://developers.google.com/search/docs/appearance/title-link)). The same is true of descriptions. 160 and 400 are the budgets this codebase uses, and the 50–60 character title target and 130–160 character description target in the generator's briefs are house style. Treat them as reasonable defaults, not as thresholds anything measures you against.
- **Under question: the thin-page threshold.** Docsbook's code computes a per-page verdict that calls a page "thin" below **120 words**, alongside "broken" and "orphan". The broken-link and orphan verdicts are surfaced; the thin verdict is computed, exported and unit-tested but is not currently painted on any panel, so in practice you will not be told a page is thin. The word minimums in the generator's briefs — 300 to 400 words depending on the page type — are house style with no published source behind those specific numbers. What is sourced is only the direction: Google asks whether content "provide[s] substantial value when compared to other pages in search results" ([Google, creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)).
- **Under question: whether question-form headings raise citation rate.** The retrieval mechanism in Rule 2 is real and sourced. What no public source establishes is a citation-rate lift from the heading form specifically, on any answer engine. Document expansion is measured on retrieval benchmarks, not on ChatGPT or AI Overviews. Treat Rule 2 as well-founded on retrieval and unproven on citation until somebody publishes the second measurement.
- **Rules 3 and 6 describe two different pipelines, and passing one says nothing about the other.** Rule 3 is Docsbook's own semantic index over your Markdown; Rule 6 is what an external assistant gets when it fetches your URL. A page can be perfectly chunked for your on-site search and invisible to ChatGPT, or the reverse. They share no code.
- **None of this is measured against outcomes for you.** Docsbook can tell you a page is orphaned, that a section matched no detector's shape, or that a fetch returned no prose. It cannot tell you that following these rules got you cited, and it does not claim to — see [Citation signals](../geo/citation-signals.md) on why one run proves nothing, and [How Docsbook proves what it claims](../evidence.md) for the standard these pages are held to.

## Related

- [AEO](./README.md) — what an answer engine needs from a page, and what the markup can still buy
- [Structured answers](./structured-answers.md) — the detectors these rules feed, and what a failure looks like
- [Citation signals](../geo/citation-signals.md) — the measured effect sizes, and the things not to do
- [GEO](../geo/README.md) — the TL;DR block, the visible date and the author line
- [SEO](../seo/README.md) — indexing, canonical URLs and crawlability, the stage before any of this
- [Search](../ai-chat/search.md) — the on-site retrieval the chunking rule feeds
- [Content widgets](../content/features/widgets.md) — the stepper and accordion regions the detectors understand
- [How Docsbook proves what it claims](../evidence.md) — the evidence rule these pages follow
