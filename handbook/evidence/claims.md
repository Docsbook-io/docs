---
title: "Claims: what is established about documentation, what is contested, and what is just repeated"
description: "Twenty-four graded claims about AI search, trust, page shape, speed and reading a traffic drop — each with its mechanism, its sources, a test you can run on your own site, and what being wrong about it costs."
tldr: "Each claim carries a standing. Established means you may state it to a customer with the source after it. Hypothesis means quote the mechanism and never the number — run the test on the customer's own site instead. The three claims most likely to save a wasted quarter are that no markup makes a page eligible for AI Overviews, that FAQ markup buys nothing since May 2026, and that blocking AI training is a different robots line from blocking AI search."
---

# Claims

Each entry is one piece of knowledge with the reference attached: what is true, why, who says so, how to check it on your own site, and what it costs to be on the wrong side of it. The grading is explained in [Evidence](./README.md); the references are in [Sources](./sources.md).

## AI search and citation

### There is no markup that makes a page eligible for AI Overviews

**Established** · [Google — AI Features and Your Website](./sources.md#google--ai-features-and-your-website), [Google — crawlers overview](./sources.md#google--crawlers-user-agents-overview)

There is no file, markup or schema that makes a page eligible for Google's AI Overviews or AI Mode. The eligibility rule is the ordinary one: the page is indexed and allowed to show a snippet.

**Why** Google states it on the page it publishes about exactly this question, and states it twice — no additional requirements, and no new machine-readable files, AI text files or markup.

**Test it** Take a page you want cited and check the two things that actually gate it. Is it indexed — impressions in your search-rankings report, or Search Console's URL inspection? Is a snippet allowed — grep the head and the HTTP headers for `nosnippet`, `max-snippet:0`, `noindex`? If both pass, the eligibility question is closed and the problem is the content.

**Cost of being wrong** A quarter spent on GEO markup that Google says in writing does nothing, while the page that was blocked from snippets stays blocked.

> Google publishes that no special markup or AI file is needed for AI Overviews — a page just has to be indexed and allowed a snippet. So the work is the content and the crawlability, not a new file.

### llms.txt is a proposal, not an engine requirement

**Established** · [The /llms.txt file](./sources.md#the-llmstxt-file-v2), [Google — AI Features](./sources.md#google--ai-features-and-your-website)

`llms.txt` is an open proposal. It is genuinely used by tools that consume documentation, and no major search engine documents it as an input.

**Why** The specification is a personal proposal with a version history; Google separately publishes that no AI text file is needed. Both can be true — it is a convention among consumers, not a ranking surface.

**Test it** Whether anything fetches yours is a log question, not an opinion. Look for requests to `/llms.txt` by the assistant user agents in your access logs over 30 days. Zero fetches after a month is the answer for your site.

**Cost of being wrong** Either a wasted afternoon, or — the commoner and more expensive direction — an `llms.txt` sold to an owner as the reason they will be cited, with nothing to show when they are not.

> llms.txt is worth having and worth about an afternoon. It is a convention some tools read, not something Google counts — anyone selling it as the GEO deliverable is selling you the cheap half.

Docsbook generates both files for every workspace automatically; see [llms.txt](../../geo/llms-txt.md).

### llms.txt can live at a subpath, not only at the root

**Established** · [The /llms.txt file](./sources.md#the-llmstxt-file-v2), [our measurement of a vendor serving it at a subpath](./sources.md#what-we-measured-ourselves)

Look for `llms.txt` at the documentation path as well as the domain root. The specification covers subpaths, the most specific file wins, and real sites use that.

**Cost of being wrong** You report "you have no llms.txt" to somebody who has one. An invented gap is worse than a missed one, because it is the one they will quote back at you.

### Blocking one bot is not blocking the rest

**Established** · [OpenAI](./sources.md#openai--crawlers-and-user-agents), [Anthropic](./sources.md#anthropic--does-anthropic-crawl-data-from-the-web), [Perplexity](./sources.md#perplexity--crawlers), [Google](./sources.md#google--crawlers-user-agents-overview)

Every major vendor runs separate agents for training, for their search index, and for a fetch a user triggered, and blocking one does not block the others: OAI-SearchBot / GPTBot / ChatGPT-User, Claude-SearchBot / ClaudeBot / Claude-User, PerplexityBot / Perplexity-User, Googlebot / Google-Extended.

**Why** Each vendor documents the split, OpenAI states the independence outright, and Google states that Google-Extended affects neither inclusion in Search nor ranking.

**Test it** Read `robots.txt` verbatim — never from memory, the agent lists change on the vendors' own release cycles — and put each rule in one of three columns: training, search index, user-triggered. A site that blocks a search-index agent while expecting citations is the usual accident.

**Cost of being wrong** Either invisibility nobody chose, from a search agent blocked by a line meant to stop training; or a promise that "we blocked the AI crawlers" that the user-triggered agent walks straight through.

> Blocking AI training and staying visible in AI answers are the same robots file and different lines in it. Every vendor documents separate agents for the two, so this is a decision you can actually make rather than a trade you have to accept.

### A fetch a user triggered is not governed by robots.txt

**Established** · [Perplexity](./sources.md#perplexity--crawlers)

Perplexity documents that `Perplexity-User` generally ignores robots rules, because a person asked for the page.

**Cost of being wrong** You tell an owner their content is walled off from assistants when a user asking a direct question still reaches it — and you plan a content strategy around a wall that is not there.

### What gets lifted is a passage, not a page

**Established** · [GEO, KDD 2024](./sources.md#geo-generative-engine-optimization), [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

An answer engine lifts a passage — a paragraph, a list, a table row — not a page. A page that only makes sense read whole has nothing in it to quote, however well written it is.

**Why** It follows from how the engines assemble an answer, it is what the GEO study optimises, and it is what practitioners report seeing lifted.

**Test it** Take the ten questions your readers actually ask and, for each, try to find one passage on your site that answers it completely with the paragraph above it deleted. The count of questions with no such passage is the finding.

> Assistants quote a paragraph, not a page. The practical version of "optimise for AI" is: for each real question, one self-contained answer that survives being read alone.

How to write that way is [Writing for retrieval](../writing/retrieval.md).

### One question becomes a fan of many

**Established** · [Google — AI in Search](./sources.md#google--ai-in-search-going-beyond-information-to-intelligence), [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

Google's AI Mode breaks a question into subtopics and issues a fan of queries at once, so the page that gets used is the one covering the whole fan rather than the one matching the typed words.

**Test it** Write down the five sub-questions a reader would need answered to act on your main one, then check which of the five your page answers. Answering one of five is the usual starting score.

**Cost of being wrong** You keep tuning a page against the exact query and it keeps losing to a longer page that happened to answer the four neighbouring questions too.

### Content-side optimisation does move AI visibility — by an unknown amount

**Hypothesis** · [GEO, KDD 2024](./sources.md#geo-generative-engine-optimization)

The study found up to 40% more visibility in generative-engine responses from content changes, with the effect varying a lot by domain.

**Why it is only a hypothesis for you** A real study with a stated method, but a benchmark rather than your site. "Up to" and "varies across domains" are doing heavy lifting, and none of it was measured on documentation specifically.

**Test it** Fix a question set, record verbatim what each engine answers today with the date and the sources it names, make one change, and re-ask the same set after two weeks. Never quote the 40% as your forecast — quote your own before-and-after.

**Cost of being wrong** A number from a paper repeated as a promise. The owner remembers the 40%, you remember the "up to", and the review goes badly.

> There is one peer-reviewed study on this and it found up to 40% more visibility from content changes, varying widely by domain. That is enough to justify trying it on a few pages and not enough to promise a number.

### Engines repeat your own mistakes back to your buyers

**Established** · [our GEO audit of a real product](./sources.md#what-we-measured-ourselves), [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

Assistants mostly paraphrase your own site, including the parts that are out of date. A landing page that still says the API is "coming soon" produces assistants that say the API is coming soon, long after it shipped.

**Why** Measured directly on a real audit: engines found the site in 9 of 9 answers and repeated "API — coming soon" in 5 of 9 while the API was live with 96 operations.

**Test it** Ask the engines about your product by name and grade what comes back by content, not by whether you were named: accurate, outdated, partly wrong, absent. The outdated bucket is usually a sentence still sitting on your own site.

> Before buying visibility, check what the engines already say — they usually repeat your own stale sentence back to your buyers, and deleting that sentence is free.

### Measure what was said, not whether you were named

**Established** · [our GEO audit](./sources.md#what-we-measured-ourselves), [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

Measure what the engines say, verbatim and dated, not whether your brand appeared. A mention that carries a wrong price or a dead feature is worse than an absence.

**Why** Presence is a rate; wording is a finding you can act on. Measured directly: a site was named in 9 of 9 answers — a perfect presence score — while those same answers told buyers the API was not built yet.

**Test it** Ten real queries from Search Console, asked conversationally, answers pasted in verbatim with engine and date, each graded accurate / outdated / partly wrong / absent, plus the page it should have come from.

**Cost of being wrong** A citation-rate dashboard that goes up while the thing being cited is wrong.

## Trust and authorship

### E-E-A-T starts with whether anyone can tell who wrote it

**Established** · [Google — helpful, reliable, people-first content](./sources.md#creating-helpful-reliable-people-first-content)

E-E-A-T is Experience, Expertise, Authoritativeness and Trustworthiness, and Google asks plainly whether it is self-evident who wrote the page and whether it carries a byline where one would be expected.

**Test it** Open your five most important pages and answer Google's own question on each: could a first-time reader say who wrote this and why they would know? Anonymous documentation is the normal state, not a scandal — but it is a lever nobody has pulled.

> Google's own guidance asks whether a reader can tell who wrote the page. On most documentation the answer is no, and a named author with a real credential is one of the cheapest trust signals available.

### Content built primarily to rank is not what Google rewards

**Established** · [Google — helpful, reliable, people-first content](./sources.md#creating-helpful-reliable-people-first-content)

Google states that content made primarily to attract search visits is not what its systems seek to reward.

**Cost of being wrong** A programme of pages written to a keyword list, which is the exact shape that the March 2026 update is reported to have cleared out of the top 100.

### Bulk AI content with no named expert is the losing side

**Hypothesis** · [practitioner field report](./sources.md#the-field-as-practitioners-report-it), [Google — helpful content](./sources.md#creating-helpful-reliable-people-first-content)

Compilations and bulk AI text with no named expert are reported as the biggest losers of recent core updates — one agency account puts 24% of top-10 pages falling out of the top 100 after the March 2026 update, concentrated in exactly that kind of page.

**Why it is only a hypothesis** The direction matches Google's published guidance about people-first content. The specific figure is one agency's account with no published method behind it.

**Test it** You do not need the industry number. Split your own pages into "has a named author and something first-hand" and "does not", and compare their position trend across the update date.

**Cost of being wrong** Quoting 24% as fact to a customer who looks it up and finds one webinar behind it. Quote the mechanism, which is well supported; do not quote the number.

## The shape of a page

### There are four kinds of documentation page, and mixing them serves none

**Established** · [Diátaxis](./sources.md#diátaxis--a-systematic-framework-for-technical-documentation)

Tutorial, how-to, reference, explanation — four different reader needs. A page that mixes them serves none of them well.

**Test it** Label each of your top 20 pages with exactly one of the four. The ones you cannot label are the rewrite queue, and they are usually the pages with the worst visit outcomes.

**Cost of being wrong** A rewrite that "improves" a reference page by turning it into a tutorial has solved a different problem and broken the page for everyone who arrived to look one thing up.

### Put the answer in the first two paragraphs

**Established** · [GEO, KDD 2024](./sources.md#geo-generative-engine-optimization), [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

Put the direct answer, with the facts and figures in it, in the first two paragraphs. It is what a reader in a hurry needs and it is the only part an engine is likely to lift.

**Why** Two independent lines converge: the study that optimised for generative engines, and the practitioner account of what is and is not quoted. Neither costs anything to follow.

**Test it** Delete everything below the second paragraph of a page and ask whether the reader's question is answered. On most documentation it is not, because the first two paragraphs are throat-clearing about what the feature is.

> The first two paragraphs are the whole page as far as a hurried reader and an answer engine are concerned. Most docs spend them introducing themselves.

### The page has to be the shape that already ranks

**Hypothesis** · [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

A page has to be the same shape as whatever currently ranks for the query — a comparison, a list, a how-to. A product page competing against a comparison page loses on format before content is considered.

**Why it is only a hypothesis** Widely reported by practitioners, with a named worked example. A strong heuristic, not a published rule.

**Test it** Open the top five results for the query and write down what kind of page each is. If four of five are comparisons and yours is a product page, that is the finding — and it is checkable in ten minutes.

See [Search intent](../lenses/search-intent.md) for the full reading.

## Structured data

### FAQ markup buys no rich result any more

**Established** · [Google — FAQPage structured data](./sources.md#faq-faqpage-structured-data)

Google narrowed the FAQ rich result to authoritative government and health sites in August 2023, and removed it from Search in May 2026.

**Cost of being wrong** A sprint adding `FAQPage` schema across a corpus for a result that no longer exists — and it is still recommended constantly, which is why this claim is worth carrying.

> Skip the FAQ schema. Google removed the FAQ rich result from Search in May 2026; the markup is now maintenance with no upside.

## Speed

### Google's responsiveness thresholds are concrete, and measured in the field

**Established** · [web.dev — Interaction to Next Paint](./sources.md#interaction-to-next-paint-inp)

INP at or below 200 ms is good, above 500 ms is poor, assessed at the 75th percentile of real field page loads — not at your laptop's.

**Test it** Field data at the 75th percentile, never a lab run. A docs site is read on conference wifi and on phones, and that is the tail the threshold is measured on.

**Cost of being wrong** "The site is fast", measured on a developer machine, while the readers it was built for are in the poor bucket.

### The three-seconds-costs-23% figure is not yours to quote

**Hypothesis** · [practitioner field report](./sources.md#the-field-as-practitioners-report-it), [web.dev — INP](./sources.md#interaction-to-next-paint-inp)

A page slower than three seconds is reported to lose about 23% of its traffic.

**Why it is only a hypothesis** A widely repeated practitioner figure with no published method attached. The direction is not in doubt and Google publishes its own thresholds; this particular number is not something to put in a proposal.

**Test it** Use the published thresholds instead. Measure your own INP and LCP at the 75th percentile and report which bucket you are in. That is defensible; the 23% is not.

## Topical authority

### Clusters of linked pages beat single pages — by an unverified multiple

**Hypothesis** · [practitioner field report](./sources.md#the-field-as-practitioners-report-it), [Google — AI in Search](./sources.md#google--ai-in-search-going-beyond-information-to-intelligence)

Covering a subject as a cluster of linked pages rather than one page is reported to produce substantially more traffic and substantially more mentions in AI answers — one agency account gives +46% traffic over six months and 3.2× the AI mentions.

**Why it is only a hypothesis** The mechanism is well supported: fan-out means an engine is issuing many sub-queries, and a cluster answers more of them. The specific multipliers come from one practitioner account with no published method.

**Test it** Pick one subject you cover with a single page. Write the three sub-questions it does not answer as three linked pages, and compare that subject's impressions against an untouched subject as the control, over eight weeks.

**Cost of being wrong** Quoting +46% as a forecast. Quote the mechanism — the engine asks many questions at once, so the site that answers many of them gets used — and let the customer's own control set produce the number.

See [Semantic SEO](../lenses/semantic-seo.md) and [Internal linking](../lenses/internal-linking.md).

## Reading a drop

### Do not rewrite during a core update

**Established** · [Google — core updates](./sources.md#google-searchs-core-updates-and-your-website), [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

Wait at least a full week after the rollout completes before analysing, and do not make drastic changes. Google explicitly advises against quick fixes and against touching content that is already performing.

**Why** Google publishes this advice directly, and adds that recovery can take several months for its systems to confirm.

**Test it** Split the drop before you act on it: impressions, average position and CTR separately, before and after the update date. A CTR-only drop with flat impressions is a snippet or an AI-answer problem, not a ranking one — and the fix is different.

**Cost of being wrong** The classic: a panic rewrite during a rollout, after which nobody can tell what the update did and what the rewrite did, and the baseline is gone for good.

> Google's own guidance is to wait a week after the rollout finishes and to avoid quick fixes. The useful work during a rollout is diagnosis, not surgery.

### "Traffic dropped" is three different failures

**Established** · [Google — core updates](./sources.md#google-searchs-core-updates-and-your-website), [practitioner field report](./sources.md#the-field-as-practitioners-report-it)

Fewer impressions means you lost coverage. Worse position means you lost ranking. Flat impressions with falling CTR means you are shown and not clicked — usually an answer above you. Each has a different fix.

**Cost of being wrong** Rewriting pages to fix what was a CTR collapse caused by an AI answer occupying the first screen. The content was never the problem and the rewrite cannot show it.

[Metrics](../auditing/metrics.md) has the full reading.

## Two that generalise beyond search

### A big catalogue is not a set anyone chooses from

**Established** · [our own call ledger](./sources.md#what-we-measured-ourselves)

A long list of named capabilities is not a set a calling model — or a reader — picks from. Measured on this product: 1 of 136 tools had ever been called, and every call from outside the founding team landed on one of five names.

**Why** The failure is silent on both sides. The model answers from the few names it can see, and nothing in the logs distinguishes a near miss from a correct answer, so it does not get reported and does not get fixed.

**Test it** Read your own call ledger by name, not in aggregate. A long tail of zeroes is the finding; a healthy total hides it.

**Cost of being wrong** Building the hundred-and-thirty-seventh capability instead of one route into the thirty that already exist.

### Generated anchors drift from rendered ones, and nothing fails

**Established** · [our corpus measurement](./sources.md#what-we-measured-ourselves)

Any link built by generating an anchor from a heading will drift from the anchor the renderer actually emits, and nothing fails when it does — the link just leads nowhere. Measured here: 6.3% of 21,827 headings in one repository, 1.7% on a clean English corpus.

**Why** Two independent slug generators cannot agree for long. Punctuation and non-ASCII are where they part first — an em dash or an ampersand is enough, and in JavaScript `\w` and `\b` are ASCII, so a Cyrillic heading can collapse to a single hyphen.

**Test it** Generate the anchor for every heading with your own code, render the same corpus, and diff the two sets. If you have never done it, assume single-digit percent and check the most-used page first.

**Cost of being wrong** Deep links in search results and AI answers that land at the top of the page instead of the section — invisible to every test, visible to every reader.
