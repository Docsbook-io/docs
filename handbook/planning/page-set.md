---
title: "Deciding the page set before you write a single page"
description: "Which pages a new documentation site needs, what each kind of page must contain, how folders become navigation, and why the FAQ and use-case pages count twice."
tldr: "Derive the page set from what the source offered, aim for 10–18 substantive leaf pages, and group them into folders by meaning — the folders become the navigation. Decide the whole list before writing: a page can only link to a neighbour it knows exists."
---

# Deciding the page set

The page set is decided in one sitting, before the first page is written, and it is derived from what the source actually offered rather than from a template. A row belongs in the plan only when there is real content behind it.

## Which pages should exist?

| Page or folder | Kind | Include it when |
|---|---|---|
| `README.md` / `index.md` | Hero, overview | Always — it is the selling front door |
| `getting-started.md` | Tutorial | Always |
| `concepts.md` or `concepts/` | Explanation | Always — it is the mental model |
| `features/<feature>.md` (3–6) | Benefit-first feature page | The source markets distinct capabilities |
| `guides/<task>.md` (2–5) | How-to | Concrete tasks exist |
| `use-cases.md` or `use-cases/` (1–4) | Job stories | Real audiences or scenarios are visible |
| `faq.md` | 6–10 questions and answers | Almost always — see below |
| `<domain>/` — `integrations/`, `security/`, `api/` | Cluster | The product has that area |
| `reference.md` / `api-reference.md` | Reference | An API, CLI or configuration surface exists |

Where you start depends on which route the input took:

| Source | Sections to start from |
|---|---|
| Repository with a README and code | Hero, getting started, concepts, `guides/`, `features/`, use-cases, FAQ, API reference |
| Marketing website | Hero, getting started, concepts, `features/`, `guides/`, use-cases, FAQ |
| An idea or a description only | Hero, getting started, concepts, `features/`, use-cases, FAQ |
| An existing documentation site | Mirror its structure, then add the missing page kinds and an FAQ or use-case page if it has none |

**Target 10–18 substantive leaf pages** where the source supports it. Scale down for a genuinely thin source: a well-scoped 8-page site beats 15 stubs. Never pad with empty placeholders — a stub is a promise the site does not keep, and a reader who opens two of them stops opening any.

## Why do folders matter more than they look?

Group the leaf pages under a handful of meaningful top-level folders. Those folder names are what the platform expands into the site's navigation sub-header, and that sub-header is what makes a site read as documentation rather than as a file listing. A flat list of five files does not sell, however good each file is.

## Which optional sections are worth adding?

Offer these once, as a multiple choice, before the crawl. Skipping is a valid answer. Each one produces three to five pages.

| Section | What it is | Why it earns its place |
|---|---|---|
| Competitor comparisons | `blog/<you>-vs-<competitor>.md` | "X vs Y" and "X alternative" are the highest-intent searches in most categories |
| Educational cluster | `learn/`, teaching the domain rather than the product | Top of funnel, with a soft action at the end; the strongest citation candidate on the site |
| Glossary and use-cases | `glossary/` for "what is <term>"; `use-cases/` per persona | Definition pages win featured snippets; use-case pages convert better than feature pages |
| Migration guides | `migrate-from-<competitor>.md` | Catches readers who are already leaving a competitor |

An educational cluster is worth more than its page count suggests because an engine does not ask your question once: Google describes AI Mode as "breaking down your question into subtopics and issuing a multitude of queries simultaneously on your behalf" ([Google, AI Mode update](https://blog.google/products/search/google-search-ai-mode-update/)), so a set of linked pages covering a subject answers more of that fan than a single page does.

If comparison or migration pages are chosen, confirm the competitor list — auto-detected from the source, with the reader free to add or remove names. **Never fabricate a competitor or a glossary term**: no evidence means skip the section and record the reason. Enrichment failing never blocks the publish; the core documentation still ships.

## Which page is worth writing most? Often not the one about your topic

The fan-out above has a planning consequence that is easy to miss, because it inverts the obvious order of work. If an engine answers one question by issuing many, then the URLs it cites are mostly answering the neighbouring questions rather than the one asked — roughly 70% of them, on one practitioner's account, with no published method behind the figure ([the neighbouring question](../evidence/claims.md#most-citations-come-from-the-neighbouring-question-not-from-yours)). The worked example was "how to brew coffee", where what got cited was water chemistry, extraction and taster protocols rather than any brewing guide.

**If that holds even roughly, the highest-value page in a plan is frequently not the page about your topic. It is the page about the thing a reader has to understand first.** The concept page that explains the model your product assumes, the page naming the constraint that makes the feature necessary, the comparison a reader needs before your feature means anything — these are the pages nobody writes, because they are not about the product and they do not look like documentation of it.

Two moves put it into a page set without waiting for the figure to be settled:

- **Write down the four or five sub-questions a reader must have answered to act on each page you planned, and mark which of them anything in the plan answers.** Answering one of five is the usual starting score. A sub-question nothing answers is a candidate row, and it is better evidenced than most rows on the list because your own plan implied it.
- **Prefer the prerequisite over another page on the same subject.** Where the choice is between a fifth feature page and the concept page the other four assume, the concept page covers more of the fan. This is the same argument the educational cluster is worth its page count for, and the corpus-level version of it — pillar and cluster completeness — is [Semantic SEO](../lenses/semantic-seo.md).

The figure is one account and must not be quoted to anybody as a forecast; the mechanism under it is Google's own published description of AI Mode. Plan against the mechanism.

## What must each kind of page be?

Four of these map onto the four needs Diátaxis names — "tutorials (learning), how-to guides (a task), reference (information), explanation (understanding)" ([Diátaxis](https://diataxis.fr/)) — and the reason to keep them apart is that a page mixing two of them serves neither. The full rulebook is in [writing rules](../writing/writing-rules.md); this is the shape each section commits to.

**Hero or index.** Opens with the product name and a one-line value proposition taken from the source. Three feature highlights, each a real detected capability. A "get started" action, plus one conversion action pointing at the call-to-action destination for the reader who is evaluating rather than installing. No marketing adjectives; describe specifics.

**Getting started (tutorial).** Prerequisites with specific versions at the top, a "what you will learn" line before step 1, then numbered steps where every step has a command or a UI action *and* its expected output. Ends in "Next steps", linking to concepts and to the first guide.

**Concepts (explanation).** No steps, no commands. Noun-phrase headings. Ends with links to the how-to guides that use these ideas.

**Guide (how-to).** The goal in the title, numbered steps, goal first. No background theory — link to concepts for that. Ends with "Related".

**Reference.** Tabular. Command, endpoint or parameter, then description, then example. Present tense, no narrative.

**Feature page.** The headline is the outcome the reader gets, not the feature name: "Never lose context between tools", not "Sync engine". The body is how it works, plus one piece of proof from the source. Ends with an action.

**Use-case page.** A concrete job story — who, the job to be done, the outcome — grounded in an audience the source actually addresses. [Jobs to be done](../lenses/jobs-to-be-done.md) is the reading that produces these.

**FAQ.** Six to ten questions an evaluating reader genuinely asks: the pricing model, the limits, privacy, supported tools, how it differs from the alternative. Each is an H2 question with a direct answer. The answers eliminate objections and do not hedge.

## How is the link graph wired?

At generation time, not afterwards:

- The index links to every top-level section.
- Every leaf page links back to the hero **and** to at least one sibling.
- Zero orphans. Every page ends with "Next steps" or "Related".
- Descriptive anchor text — "Read the concepts guide", never "click here".

This is the reason the full page list is decided before the first page is written: **a page can only link to a neighbour it knows exists.** [Internal linking](../lenses/internal-linking.md) covers what to do with the graph once the site has history behind it.

## Why do the FAQ and use-case pages count twice?

They carry the most liftable structure on the site. An answer engine quotes a passage — a paragraph, a list, a table row — rather than a page, which is what the GEO benchmark optimises for ([GEO, KDD 2024](https://arxiv.org/abs/2311.09735)), and a question with its own direct answer under it is the cleanest passage a documentation site produces. A numbered procedure is the second cleanest. That is why an FAQ is effectively mandatory even when the source has no explicit one: synthesise it from what the product plainly answers, and never from what it does not.

Docsbook's [answer-engine layer](../../aeo/README.md) turns that same Q&A into `FAQPage` markup and numbered procedures into `HowTo` markup. Two honest caveats about the markup specifically, neither of which changes the advice to write the content:

- **The FAQ rich result is gone.** Google narrowed it to well-known, authoritative government and health sites in August 2023 and removed it from Search in May 2026 ([Google Search Central, FAQ structured data](https://developers.google.com/search/docs/appearance/structured-data/faqpage)). Writing an FAQ to win a rich result is writing it for a result that no longer exists.
- **No markup is a requirement for AI surfaces.** Google states there are "no additional requirements to appear in AI Overviews or AI Mode, nor other special optimizations necessary" ([Google Search Central, AI features](https://developers.google.com/search/docs/appearance/ai-features)).

What remains true is the part that was always doing the work: the switch and the content go together, and flipping it on prose with no questions and no step sections produces nothing to lift. Write the questions your readers actually ask, in their words, each with a self-contained answer — see [writing for retrieval](../writing/retrieval.md) and [citation signals](../../geo/citation-signals.md).

## Related

- [Routing the input](./route-the-input.md) — what you are starting from, and the stage this decision sits in.
- [The four routes into creation](./sources.md) — the starting page set implied by each route.
- [Know the reader before you write the page](./know-the-reader.md) — the audit that tells you which of these pages the product actually needs.
- [Writing rules](../writing/writing-rules.md) — the per-page rulebook this plan hands over to.
- [Publishing what you wrote](./publishing.md) — turning the folder tree into navigation on a live site.
- [Claims](../evidence/claims.md) — the standing of the fan-out figure above, and the test that settles it for one site.
