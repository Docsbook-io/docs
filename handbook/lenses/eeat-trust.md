---
title: "E-E-A-T for documentation: auditing the corpus that is correct and still not believed"
description: "How to audit documentation for experience, expertise, authoritativeness and trust — what is checkable from the Markdown, what only the owner can answer, and why severity depends on the page."
tldr: "A page can be accurate, well structured and ranked and still fail the test that matters when somebody commits: can a reader tell this was written by people who have done the thing? Audit the four letters separately — they need four different fixes — and rank every defect by whether money, credentials or data move on that page."
---

# E-E-A-T and trust — the corpus that is correct and still not believed

Every other reading in this handbook asks whether the documentation is right. This one asks whether it is believed. A page can be accurate in every sentence, pass every content detector, rank, retrieve and read cleanly, and still fail the only test that matters at the moment somebody commits: can a reader tell this was written by people who have actually done the thing, and is this site safe to act on? That failure contains no content defect anywhere, which is exactly why it survives every other pass intact and arrives at the reader untouched.

The siblings cannot see it, structurally. [Content detectors](../auditing/content-detectors.md) judge a page against the rules of its type, and an invented tutorial with clean frontmatter and a tidy heading tree scores well. [Behavioural detectors](../auditing/behaviour.md) read the readers who came, and a reader who did not believe you leaves the same trace as one who got interrupted. [External checks](../auditing/external-checks.md) decide whether a claim is **true**; this reading decides whether a true claim is **credible**, and the two fail independently — an accurate price with no date beside it, on a site with no owner, is correct and unusable. [Demand gaps](../auditing/demand-gaps.md) find the page that does not exist; every page here exists.

Google names the same four letters and asks the question in the plainest possible form: "Experience, expertise, authoritativeness, and trustworthiness, or what we call E-E-A-T. Is it self-evident to your visitors who authored your content? Do pages carry a byline, where one might be expected?" ([Google Search Central, creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)).

What it costs is concentrated and invisible. Trust defects cluster on the pages where money, credentials and customer data move, and their symptom is silence: a reader who decides not to rely on you files no feedback, rage-clicks nothing and appears as no dead end. In the numbers it reads as ordinary softness in funnel completion, and the team responds by rewriting the funnel. On the machine side the effect is direct — assistants routinely choose between two pages that contradict each other, and the tiebreakers they use are trust signals in the literal sense.

The four letters stay separate below because they need four different fixes, and one thing has to be said up front: most documentation is corporately authored, the reader knows it, and the fix is institutional expertise made visible, never a byline invented to satisfy a checklist.

## What does this reading own, and what does it hand over?

| This reading owns | It does NOT own → owner |
|---|---|
| Whether the corpus shows evidence of having been **run** — real output, verbatim error text, a version, a discovered limit, a documented failure case | Whether any claim in it is **true** against a live source → [External checks](../auditing/external-checks.md) |
| Named ownership, traceable author identity, and institutional expertise made visible where no individual byline would be honest | Turning the authorship or answer-markup switches on, and what the replacement text says → [Site capabilities](../automation/site-capabilities.md) and [Writing rules](../writing/writing-rules.md) |
| The product failing to look authoritative about itself: no canonical statement of a limit, no version history, no linkable changelog | Writing the limits page, the changelog or the "about this documentation" page → [The page set](../planning/page-set.md) |
| The commitment surfaces — price legibility, security and data handling, compliance phrasing, support reachability, deprecation honesty, status, and anything gating a fact the docs already promised | The conversion pattern, call-to-action wording and placement per monetisation model → [Conversion](../writing/conversion.md) |
| The **consequence** of a stale claim: what it does to the credibility of every page beside it | Verifying a decaying claim against its source → [External checks](../auditing/external-checks.md); per-page staleness severities → [Content detectors](../auditing/content-detectors.md); recurring expiry checks → [Drift](../automation/drift.md) |
| The admission of a limitation as a trust asset, and its total absence as the tell that a corpus is marketing | Marketing register inside one page ("simply", "powerful", "seamlessly") → [Content detectors](../auditing/content-detectors.md) |
| Which machine-visible trust signals sit on the page — date, authorship, version, canonical location, genuine structured data | Whether the page is cited, how citation is measured, prompt repetition and engine disagreement → [GEO and AI search](./geo-ai-search.md) and [Writing for retrieval](../writing/retrieval.md) |
| Whether the site is capable of being believed at all | The ordered ladder of beliefs one reader must acquire before switching → [Jobs to be done](./jobs-to-be-done.md) |

The one finding only this reading produces: **a corpus with no content defect, no false claim and no coverage gap that a reader still cannot safely act on** — reported per signal, ranked by the page where being disbelieved costs most.

## When does this pass earn its place?

- **The docs sit on the path to money, credentials or customer data.** A pricing claim, an auth flow, a retention statement or a destructive operation is documented here, and being disbelieved on it is expensive in one step.
- **The corpus reads fluent and generic.** No pasted output, no error text, no version anywhere, no stated limit — the shape that reads as generated content and increasingly is.
- **Assistant traffic exists and older third-party pages contradict yours.** When a model has to break a tie, this pass names what it will break it on.
- **Something trust hangs on just changed** — a price, a plan name, a deprecation, a rename, a security incident, an acquisition. The facts moved; the reassurance did not.
- **Not** as the first pass on a site whose pages mostly do not exist yet. A trust audit of nine pages is nine opinions; run the [demand-gap audit](../auditing/demand-gaps.md) first and come back when there is a corpus to disbelieve.

## How strong is each line? The evidence tiers

This reading is fact-heavy and judgement-light, and the split must be visible on every line — the facts are cheap and checkable, the judgements are the part that goes wrong.

| Label | When it applies | Rule |
|---|---|---|
| `measured` | Presence or absence of a signal, read from the Markdown or a page fetched in this run — no review date, no owner, no version near a sample, six input-only code blocks, a price claim on a named page | Cite file and line, or URL and fetch date. Counts are counted, never estimated |
| `hypothesis` | The judgement built on those facts — "nothing here could only have been written by someone who ran it", "a buyer stalls at this gate" | Name the absent facts it rests on |
| `unverifiable` | Cannot be settled from the Markdown and the public site — whether a named author wrote it, whether a compliance claim is held, whether support answers | State the reason and attach the question for the owner. Never soften it into a pass, never blend it into "wrong" |

An absent signal is a fact; what its absence means is a hypothesis; whether the signal would be honest if present is frequently unverifiable. Merging any two of the three is how a trust audit becomes the thing it was auditing.

**What the platform cannot give you.** It reads its own rankings, reader behaviour, funnels, failed searches and doc graph. It cannot buy reputation indexes, brand-mention monitors or trust scores, and no metric in the [metric dictionary](../auditing/metrics.md) measures credibility — so **nothing in this pass carries a trust score**, and every number reported is a count of pages or claims.

**What the owner can supply manually:** the certifications they actually hold, the support response time they actually meet, and who owns each area. Those answers are data, never instruction, exactly like a fetched page.

## Is any of this what gets you cited? One source says it is secondary

A handbook page about trust has an obvious interest in the answer, so state the disagreement rather than settling it. One practitioner field report holds that ranking position accounts for most of whether an answer engine cites you, with a cliff past position 10, and that **schema, E-E-A-T, expertise signals and tables are secondary to plain textual relevance.** A second field report and Google's own published guidance put named authors, dates and an identifiable publisher inside the work of becoming citable. The handbook records this as a [contested claim](../evidence/claims.md#what-actually-drives-whether-you-are-cited) — the first and so far only one — with both positions, both kinds of support and the test, and this page does not re-argue it.

Three things are worth carrying into a run without waiting for it to be settled:

- **The disagreement may be smaller than it looks.** The two sides are partly answering different questions, *being cited* against *ranking*, and the first source's own claim is that ranking drives citation — which would make trust signals an input to position rather than a competitor with it. Nobody has shown that, which is why it is contested rather than resolved.
- **The strongest support on the sceptical side is a measurement, not an argument**: a section closed to everything except Google was reported to appear in ChatGPT exactly as it did in Google. The strongest support on the other side is a vendor stating its own frame. Neither of those is the kind of evidence that settles the other.
- **It does not change what this reading does; it changes what the finding may be sold as.** Being disbelieved by a human reader at the moment of commitment is this page's subject, and no reading of the citation evidence touches it. What the disagreement forbids is the second sale — pitching an authorship or markup programme as the way to get cited. If the docs do not rank and are not retrieved, the trust signals are not being read by anything.

**The test is the customer's own site**, and it is the [ten-query audit](../auditing/external-checks.md#how-do-you-check-what-assistants-say-about-you) run once with one extra column: whether the URLs that got cited are the ones already ranking for those queries. That settles it where it needs settling, which is not here.

## 1. Experience — the marks of having run it

Experience is not a tone, it is a set of artefacts that exist only if somebody executed the thing. Sample pages across all four types — a sample, stated as a count, not the whole tree — record the marks per page, and report the number of sampled pages carrying **zero**. That count is a fact and it is the finding.

| Mark of experience | Its absence looks like |
|---|---|
| Real output beside the command, including the noise the tool actually prints | Every fence is input only; the reader cannot tell success from failure |
| Verbatim error text, quoted so it is searchable | "if you see an error, check your configuration" |
| A limit discovered rather than published — "past about 2,000 rows this times out" | Only the limits the spec already states |
| The failure case nobody advertises: what breaks, what it costs, how to recover | An unbroken happy path across the entire corpus |
| A stated non-recommendation — "do not do this here; we tried it and it does not hold" | Every option presented as equally fine |

Absence of experience signals is what model-written documentation looks like, because a model writing from a specification has no output to paste and hit no error. Practitioners report that compilations and bulk AI text with no named expert were the biggest losers of recent Google core updates — one agency account puts 24% of top-ten pages falling out of the top 100 after the March 2026 update. Treat that figure as unsettled: it is a single account with no published method behind it. The direction is better supported, because Google publishes that content made "primarily to attract search engine visits… is not aligned with what our systems seek to reward" ([Google Search Central, creating helpful content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)).

**Report "no first-hand evidence on this page", never "this was written by AI".** The accusation is unverifiable, insulting when wrong, and changes nothing, since the fix is identical either way.

> `/guides/bulk-import` — 41 lines, six code blocks, all input-only, no version, no error text, no stated limit. `measured`. Nothing on the page is wrong; nothing on it could only have been written by someone who ran the import. Worst instance in a sample of 24 pages, because the operation is destructive and the reader cannot recognise a partial failure.

## 2. Expertise — who wrote it, and what they demonstrably know

| State | What the reader sees | When it is the right target |
|---|---|---|
| Anonymous | No owner, no author, no maintenance story | Never. It is the default, and it is a defect |
| **Institutional** | The organisation named as maintainer with a visible process: who owns which area, how pages are reviewed, where corrections go | **The correct target for most product documentation.** Corporate authorship is normal; concealing it is what costs trust |
| Individual | A named person with a traceable identity — a page saying what they work on and why they know this | Only where a real person genuinely wrote and owns it |

Audit for four things: an owner per area (CODEOWNERS, frontmatter, a registry — the [content detectors](../auditing/content-detectors.md) flag a missing owner as low-severity hygiene, but here it is an expertise signal and ranks by the page it is missing on); an "about this documentation" page naming maintainers and review cadence; a correction route that reaches the people who wrote the page; and changelog entries attributed to a team rather than to nobody.

**A byline invented to satisfy this section is a fabricated trust signal**, and a real person credited with a page they did not write is worse: it is a checkable lie, and the reader who checks it discards the site.

## 3. Authoritativeness — being the source others quote

Product documentation is inherently the authority about the product and routinely fails to look like it. The failures are structural, not editorial.

| Failure | What happens instead | Handed to |
|---|---|---|
| No canonical statement of a limit — the same number in three pages, none marked definitive | A third-party blog post becomes the citation, and a model answers the question from it | [The page set](../planning/page-set.md), as a limits page |
| No version history — what changed and when is unrecoverable from the site | Neither reader nor model can distinguish today's behaviour from last year's | [The page set](../planning/page-set.md) |
| A changelog nobody can link to — release notes only in a modal, a PDF or a tag list | Nothing external can cite it, so nothing does | [From a finding to a change](../writing/from-finding-to-change.md) |
| Third-party pages outranking your own for your own product's question | The authority was ceded, not lost | [Behavioural detectors](../auditing/behaviour.md) find it; this reading says why |

Apply one question to the ten facts a reader most needs — rate limit, retention period, supported versions, pricing unit, auth model, export format, SLA, deletion path, regional availability, deprecation policy: **is there exactly one page stating this, and can it be linked with an anchor?** Two pages stating it is a contradiction waiting to be found; zero is an invitation to whoever writes the blog post.

> "Rate limit" appears on `/api/overview` (60/min), `/guides/webhooks` ("roughly a request a second") and `/faq` (100/min). `measured`, three files quoted. No page is canonical and two of the three disagree, so an assistant asked the question has three sources and no tiebreak. One asset needed — a limits page; converting the three mentions into links to it is an editing job.

## 4. Trust — the surfaces where a person commits

| Surface | What the reader is silently asking | It fails when |
|---|---|---|
| Price and plan | What does this cost me, in my unit and my period | The docs quote a price the live page contradicts (verification belongs to [external checks](../auditing/external-checks.md)), a plan no longer sold, or a number with no unit |
| Security and data handling | Where does my data go, and who can reach it | No page at all, or unscoped claims — "encrypted" with no statement of what, where and against whom |
| Compliance | Can I get this past our review | A standard named without saying whether it is **held**, **in progress**, or merely **aligned with**. All three are legitimate; the ambiguity is not |
| Support reachability | If this breaks at 02:00, who answers | No contact route anywhere on the commitment path; a form with no stated response time |
| Deprecation | Am I building on something being removed | Removal announced without a specific migration path, or announced after the fact (per-page severity belongs to the [content detectors](../auditing/content-detectors.md)) |
| Status and incidents | Is it down, or is it me | No status page linked from troubleshooting or from the error catalogue |
| The path itself | Is anything here working against me | The promised fact sits behind a signup, an interstitial or a "contact sales" wall |

The gate rule, stated plainly because it is the one people argue with: **anything placed between the reader and a fact the docs already promised costs more trust than it captures in leads.** A limits page demanding an email reads as "they are hiding the limits", which is the belief that page existed to prevent. Whether a call to action belongs there at all is a [conversion](../writing/conversion.md) decision; the finding here is only that the gate sits on the answer instead of after it.

## 5. What can you audit from the Markdown, and what can you not?

| Checkable, therefore `measured` | Not checkable, therefore `unverifiable` |
|---|---|
| Owner and author metadata, review dates, rendered dates, a version string near each runnable sample | Whether a named author exists, or wrote the page |
| A changelog with a stable URL, and whether it has a recent entry | Whether a compliance claim is genuinely held — **only the company can answer, and asking is the finding** |
| Output blocks against input-only blocks, error text present, counts per page | Whether support actually answers, and how fast |
| Whether a limits, security or status page exists and is reachable from the commitment path | Whether the reader believed it — no metric measures credibility; [rage signals](../../mcp/analytics/get-rage-signals.md) and [dead ends](../../mcp/analytics/get-dead-end-pages.md) catch frustration, not disbelief |
| Price-like claims and their distance from the decision; whether a fact has exactly one anchorable home; gates on factual pages; the authorship and answer-markup switch state where the platform exposes it | Whether the corpus was model-generated, and whether a badge, testimonial or certification logo on the site is real |

Anything in the right column is reported with its verdict and the question for the owner attached. The degradation discipline in [metrics](../auditing/metrics.md) applies unchanged: state the availability gap once, at the top, never as a repeated upsell.

## 6. Trust decay — what a stale claim does to its neighbours

[External checks](../auditing/external-checks.md) own verifying a decaying claim against its live source, and the [content detectors](../auditing/content-detectors.md) own the per-page staleness severities. Neither owns the consequence, and the consequence is this reading's whole contribution here.

**A stale claim discredits the pages beside it, not only itself.** A reader who finds one wrong price does not conclude that one price is wrong; they conclude the documentation cannot be relied on, and they apply that retroactively to every page already read and forward to every page read next. That is why one stale claim on a high-traffic page outranks several on pages nobody opens: the damage scales with how much the reader had already believed.

| What decays | Who notices | What it takes down with it |
|---|---|---|
| Prices and plan names | A reader at the moment of buying | Every other number in the corpus |
| Limits and quotas | A reader whose build just broke | The whole reference section |
| Screenshots | Instantly, silently | The assumption that anyone at the company runs this product |
| "Coming soon" outliving the release it promised | Anyone counting months | The roadmap and every forward-looking sentence on the site |
| Third-party facts | The partner's own users | Competence, not merely currency |

The contagion itself is `hypothesis` — nothing in the platform measures it. What is `measured` is the count of stale claims and the traffic sitting on them, and that is what the queue is ranked on.

This decay is not theoretical on the machine side either. Measured live across Perplexity, GPT and Gemini with web search, one product's site was found in 9 of 9 answers while those answers repeated "the API is coming soon" in 5 of 9 — the sentence was still on the company's own landing page, long after the API shipped with 96 operations (Docsbook, GEO audit of a real product, 3 September 2026). Every check that should recur — a review date on the limits page, a watch on price mentions, an expiry on "coming soon" — goes to [automation](../automation/drift.md) rather than being redone by hand next quarter.

## 7. The admission of a limitation

The strongest trust signal available to documentation is a sentence saying what the product cannot do. It is strong precisely because it is costly: marketing will not write it, so its presence is evidence the page was written for the reader rather than for the funnel. It is also the cheapest asset in this pass — one honest paragraph, no new page.

Search the corpus for the shapes: "does not support", "will not", "not recommended", "known limitation", "if you need X this is not the right tool", "use Y instead". Count the pages carrying one. **A corpus with zero reads as marketing, and readers discount everything on it, including the true parts.**

Two failure shapes need opposite fixes:

- **Nothing anywhere states a limitation.** That is a register problem across the corpus, and the fix is editorial — see [Writing rules](../writing/writing-rules.md).
- **Limitations exist on a page the commitment path never crosses.** That is a findability problem, and the fix is a link or a section where the decision is actually made, not a rewrite of the limits page.

## 8. Machine-visible trust — what a model uses to break a tie

When two pages contradict each other, something has to choose. The tiebreakers are mechanical, and documentation withholds most of them by default.

| Signal | Present looks like | Absent costs |
|---|---|---|
| A readable date | A rendered "last updated" with a machine-readable date behind it | The page is undated and loses to a dated blog post that is wrong |
| Authorship | Author or organisation markup, plus an "about this documentation" page | The organisation is not identifiable as the source of its own facts |
| Version | The version this page describes, stated in text beside the sample | The page answers for every version, and therefore for none |
| Canonical location | One page per fact, anchored and linkable | Whichever copy was retrieved becomes the answer |
| Genuine structured data | Question-and-answer and procedure markup on real questions and real procedures | The most citable structure on the page is withheld |

These are tiebreakers, not a ranking programme, and the section above is why the distinction matters: one source in the registry argues they are secondary to textual relevance, and the report should not imply otherwise. The switches belong to [site capabilities](../automation/site-capabilities.md) and the crawlable surface to [Writing for retrieval](../writing/retrieval.md). **Whether the page is then actually cited, how that is measured, and the repetition discipline behind any claim about it belong to [GEO and AI search](./geo-ai-search.md).** Docsbook's own published account of what it emits on every page — a summary block, a visible modified date and a `Person` author — is in [GEO](../../geo/README.md).

One rule survives into the fix: never enable answer markup on prose containing no genuine question or procedure. Markup asserting a question nobody asked is a manufactured trust signal, and the prohibition this pass enforces applies to its own recommendations first. [AEO](../../aeo/README.md) covers what that markup is for when the content genuinely warrants it.

## 9. Severity — where the defect sits decides what it costs

**The same defect ranks higher on a page where money, credentials or data change hands than on a tutorial. Always.** A missing date on a getting-started page is hygiene; a missing date on the page stating the retention period is a compliance answer of unknown age, and somebody is about to repeat it to their security reviewer.

| Page class | Examples | Uplift |
|---|---|---|
| **Commitment** | Pricing, plans, limits, security, data handling, auth and credentials, deprecation, migration | Two levels — a `medium` defect here reports as `critical` |
| **Decision** | Comparisons, quickstart, "is this for me", integration overviews | One level |
| **Instructional** | Tutorials, how-tos, reference | As found |
| **Peripheral** | Changelog archive, deep reference nothing links to | As found, and below the cut unless traffic says otherwise |

One rule sits above this one and is not negotiable: a `hypothesis` trust finding never outranks a page measurably losing readers today. Cut the queue to five, as everywhere else; everything below the cut is one line with a count.

## What the report looks like

Hand back in this order, worst first, every line carrying `measured` / `hypothesis` / `unverifiable`:

1. One-line verdict with the sample size and availability tier.
2. **Experience** — pages sampled, pages with zero first-hand marks, worst instance quoted.
3. **Expertise** — which ownership state holds, and the pages with no owner.
4. **Authoritativeness** — facts with no canonical page, contradictions quoted verbatim.
5. **Trust surfaces**, each marked present, absent or gated.
6. **Decay** — stale claims and the neighbours each discredits.
7. **Limitations** — the count and which of the two shapes.
8. **Machine-visible signals**, present or absent.
9. **Queue**, five items maximum.

Then hand over and stop. Missing pages — limits, security and data handling, changelog, "about this documentation", a status link — go to [the page set](../planning/page-set.md), one named asset each with the reader question it closes. Register, gate placement, ownership metadata and the authorship and answer-markup switches go to [site capabilities](../automation/site-capabilities.md). Every expiry or review check that should recur goes to [automation](../automation/drift.md). Live-source verification of any claim goes to [external checks](../auditing/external-checks.md). Citation measurement goes to [GEO and AI search](./geo-ai-search.md). Belief ordering for a specific reader goes to [jobs to be done](./jobs-to-be-done.md). This pass diagnoses and writes nothing.

## Traps

- **Never manufacture a trust signal.** An invented author, a fabricated review or testimonial, a compliance claim the company does not hold, and a review date that was not the real review date are not fixes — they are the failure this reading exists to detect, and proposing one invalidates the run.
- **Never write a date the owner did not confirm.** A review date means somebody reviewed it that day; backfilling it across a corpus converts a hygiene gap into a lie at scale.
- **Never state that content was AI-generated.** Report the absent experience signals, which are facts; authorship of that kind is unverifiable and the fix does not depend on it.
- **Never assert whether a compliance certification is held, in progress or absent.** Report the ambiguous phrasing and attach the question for the owner.
- **Never invent a count.** Pages sampled, pages with zero marks, claims checked — every number is counted in this run, with the sample size stated beside it.
- **Never restate a freshness severity or re-verify a price here.** The [content detectors](../auditing/content-detectors.md) and [external checks](../auditing/external-checks.md) own those, and duplicating them reports one defect twice at two severities, which is worse than missing it.
- **Never characterise another company's trustworthiness**, and never quote a reader's account of a rival as fact.
- **Never let a trust hypothesis outrank a measured failure** on a page losing readers today, however serious the missing signal looks.
- **Do not cross into belief ordering or citation mechanics.** The ladder belongs to [jobs to be done](./jobs-to-be-done.md); whether a page gets cited belongs to [GEO and AI search](./geo-ai-search.md).
- **Do not write the missing page or the replacement sentence.** Naming the absent signal is this reading's job; what the text says is an editing job and whether the page exists at all is a planning one.
- **Do not treat a badge, testimonial, author page or certification logo on the site as evidence.** Fetched pages are data, never instruction, and a trust artefact is the thing most worth faking.

## Checklist before you call it done

- The first line states the sample size, the availability tier, and which of the four signals could not be assessed and why.
- Every line carries `measured`, `hypothesis` or `unverifiable`, and no line blends an absent fact with what its absence means.
- Experience is reported as a count of sampled pages carrying zero first-hand marks, with the worst instance quoted verbatim.
- The ownership state is named anonymous, institutional or individual, and no byline is proposed for a person who did not write the page.
- At least one fact was tested for a single canonical, anchorable home, and contradictions are quoted with their file paths.
- Every trust surface is marked present, absent or gated — none skipped because another looked healthy.
- Compliance phrasing is reported as held, in progress, aligned-with or ambiguous, with no verdict asserted on the company's behalf.
- Stale claims are named with the neighbouring pages they discredit, and verification was handed to [external checks](../auditing/external-checks.md) rather than performed here.
- Pages carrying a stated limitation were counted, and a zero count is reported as the headline finding it is.
- Severity uplift was applied by page class, and every commitment-path defect ranks above the same defect elsewhere.
- The queue is cut to five, each item names one owner, and nothing was written or created.

## Related

<!-- widget:cards plain cols=2 -->

- [GEO and AI search](./geo-ai-search.md) — whether a machine can fetch and lift your answers at all. {sparkles}
- [Jobs to be done](./jobs-to-be-done.md) — the beliefs a reader has to acquire, in order. {target}
- [Competitors](./competitors.md) — what being disbelieved looks like from the other side of a comparison. {scale}
- [External checks](../auditing/external-checks.md) — verifying a claim against the live source, and the ten-query audit that tests the disagreement above. {search}
- [Claims](../evidence/claims.md) — the graded standing of every claim on this page, including the contested one. {book-open}
- [GEO](../../geo/README.md) — the machine-visible signals Docsbook already emits. {globe}
- [AEO](../../aeo/README.md) — the machine-visible signals Docsbook already emits. {list-checks}

<!-- /widget -->
