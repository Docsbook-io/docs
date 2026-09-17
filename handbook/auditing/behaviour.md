---
title: "Reader behaviour: reading what people actually did in your docs"
description: "Dead ends, routes, question clusters, rejected searches, the striking-distance band, dwell, cohorts and buying stage — what each proves, and what it cannot."
tldr: "Behavioural readings answer what readers did, not what a page says. Each answers a different question, so pick the ones that can explain the failure you are chasing rather than running all of them. Every one reports absolute counts beside its rates, respects the sample floors, and quotes the reader verbatim wherever the reader's own words exist."
---

# Reader behaviour

These readings work on what readers did rather than on what the pages say. A page's text is available to anyone with an opinion; the routes people walked, the searches they abandoned and the questions the assistant could not answer are available only to you, and they are the part of an audit nobody can argue with.

Each reading below answers a different question. Pick the ones that can explain the failure mode you are chasing — [choosing a lens](./choosing-a-lens.md) is the decision procedure — rather than running all of them and producing a document nobody finishes. All of them obey the same discipline: absolute counts beside every rate, the [sample floors](./metrics.md#sample-floors-below-which-a-percentage-is-a-lie) respected, and the reader quoted verbatim wherever the reader's own words exist.

## Who left with nothing? Dead ends

A dead end is a visit where the reader demonstrably tried — searched, asked the assistant, or opened three or more pages — and produced no sign of getting what they came for. It is the closest thing to direct evidence that documentation is failing, and unlike bounce rate it never counts someone who never engaged in the first place.

1. **Establish the headline outcome mix** for the period, with raw counts. Too small a sample stops the analysis there; a fabricated percentage destroys trust in everything else in the report.
2. **Rank the pages readers gave up on**, ignoring anything flagged as terminal success. A page people leave from after succeeding is not a defect.
3. **Read the journeys, not just the counts.** For the top three, pull the individual visits that ended there. The step *before* the exit is usually the real problem: a reader who lands on billing, searches twice and leaves is telling you something different from one who arrives from the quick start and stops dead.
4. **Label each as missing, unhelpful or unfindable.** The three failure modes need three different fixes, and mislabelling is what makes an audit expensive.

The output is a ranked list of imperative fixes — "Rewrite /billing: 14 readers searched and left" — each carrying its evidence, not a dashboard of numbers.

In Docsbook this is [`get_visit_outcomes`](../../mcp/analytics/get-visit-outcomes.md) for the mix, [`get_dead_end_pages`](../../mcp/analytics/get-dead-end-pages.md) for the ranking, and [`get_page_journeys`](../../mcp/analytics/get-page-journeys.md) for the individual visits behind a row.

## Where do readers fall out? Routes and funnels

The classic funnel question, applied to documentation: 60% land on the quick start, 40% reach billing, 5% take the action. Where did the rest go?

Cluster the recurring multi-step paths readers actually walked ([`get_route_patterns`](../../mcp/analytics/get-route-patterns.md)) and compute how many reach a page that matters. Flag high-volume, low-completion paths. Also flag the **broken journey**: a transition the document graph implies — page A links to page B — that no session in the period took. That is usually an anchor-text problem rather than a content one.

Watch for the detour. When the top route is "landing → search → …", readers are bypassing the navigation, which is a discoverability finding about the sidebar and not about any page in the route.

Conversion pages are inferred from the graph plus action labels. If the site uses unusual labels, say so in the report rather than letting the inference pass silently. Where the owner has declared goals and an ordered funnel, read those instead — [goals and funnels](./goals-and-funnels.md) is the stronger signal and the one with its own failure modes.

## What are people asking? Question clusters

Group every question put to the assistant into themed topics, including the ones it **answered** — that is what makes this deeper than a gap list. For each cluster, check whether an existing page directly answers it.

| Coverage | Diagnosis | Fix |
|---|---|---|
| No page covers it | **Content gap** | A page to write, with a draft outline — see [the page set](../planning/page-set.md) |
| A page covers it well and the assistant missed it | **Retrieval failure** | Not content. The assistant's retrieval or its instructions — see [AI chat](../../ai-chat/README.md) and [writing for retrieval](../writing/retrieval.md) |
| A page covers it and answers well | Healthy | Note it and leave it alone |

Sorting by coverage × question count finds the highest-value retrieval fix in one step. The questions come from [`get_ai_questions`](../../mcp/analytics/get-ai-questions.md), and the ones that hit a wall from [`get_ai_unanswered`](../../mcp/analytics/get-ai-unanswered.md).

A retrieval failure diagnosed as a content gap is the expensive version of this mistake: you write a page that duplicates one you already have, and the assistant misses both.

## The page was right there: rejected searches

This is the failure no zero-result report will ever show. The reader typed a query, search worked, results appeared — and they read the titles and left without opening one. That points at eight words on a row, not at page bodies, and it is an order of magnitude cheaper to fix than writing anything.

1. **Collect the queries where results were returned and nothing was opened** ([`get_search_zero_click`](../../mcp/analytics/get-search-zero-click.md)). Group by meaning, not by exact string: "reset password", "forgot password" and "password recovery" are one query with three spellings, and splitting them hides the frequency that justifies the fix.
2. **Reconstruct what the reader saw.** Run the query yourself and write down the result list in order, with the exact titles. You are judging whether the right page's title, read cold in a list of five, looks like the answer.
3. **Diagnose exactly one of three.** **Wrong words** — right page, different vocabulary. **Wrong impression** — accurate, but it reads as jargon or a codename. **Genuinely absent** — nothing in that list answers it, which is a page to write rather than a title to rewrite.
4. **Check the snippet-answered case first.** A short factual query whose answer was visible without clicking is a quiet success, not a failure. Exclude it and say why.

**The principle:** a title is written in the reader's words, not the product's. Feature names are decided by people who already know what the feature does; queries are typed by people who do not. When the two disagree, the reader is right by definition. The rejected queries are that vocabulary, written down, with a frequency count attached — which is also the raw material for the [user-language reading](../lenses/user-language.md).

Patterns worth recognising:

| Pattern | Example fix |
|---|---|
| Query is a verb, title is a noun phrase | "Webhook Configuration Reference" → **"Send events to your server with webhooks"** |
| Title is the internal codename | "Atlas Sync" → **"Keep two workspaces in sync"** |
| Title states the concept, the reader arrives with the symptom | "Authentication Overview" → **"Fix 401 and 403 errors when calling the API"** |
| Bare noun that could mean anything | "Limits" → **"Rate limits, file size caps and how to raise them"** |
| Several near-identical rows, so nothing is chosen | "Billing" / "Billing FAQ" → **"Change your plan or payment method"** / **"Refunds, invoices and failed payments"** |
| Good title, boilerplate first line | Replace "This page describes the configuration options available." with the answer's first sentence |

A title that over-promises turns a non-click into a dead end, which is worse than the problem you started with. If the proposed title promises something the page does not deliver, the diagnosis was wrong.

## Which pages are already close to winning?

Pages at positions 5 to 20 have won the expensive part: crawled, indexed, judged relevant, shown to real people. What is missing is looking like the answer in a result list. Moving a page from 9 to 4 is a title and an opening paragraph; getting a new page to 9 is months.

1. **Pull the band** with position, impressions, clicks and queries, for a dated window ([`get_search_rankings`](../../mcp/analytics/get-search-rankings.md)).
2. **For each page, take the queries carrying the most impressions** — not the one the author had in mind — read the page, and answer in plain words: *is this page about that query?* Quote the query verbatim.
3. **Split into two piles. This is the step that saves the money.**
   - **Wrong intent** — the page ranks for something it does not answer. No rewrite will save it. The honest output is a content-gap note, and this page should stop competing for that query.
   - **Right intent, weak pitch** — the page genuinely answers and the result listing does not say so. This is the queue: cheap, low-risk, reversible.
   - A page whose queries split across both piles is trying to be two pages. Say so, instead of averaging it into one recommendation.
4. **Rank by impressions × the distance still to close to the top three**, not by position. A page at 15 with thousands of impressions beats a page at 6 with forty. Show the arithmetic, and break ties toward the smaller fix.
5. **For each queued page, produce three things**: a proposed title, a proposed description, and the one-sentence direct answer the first paragraph should open with. Never "improve the title". Putting the direct answer with its facts and figures in the first two paragraphs is also the part an engine is most likely to lift ([GEO, KDD 2024](https://arxiv.org/abs/2311.09735)); [writing for retrieval](../writing/retrieval.md) is how to shape it.
6. **Record the baseline** — position and impressions at rewrite time. Search effects take weeks, and without a written baseline the next run cannot tell a real improvement from a seasonal one.

Never change a page's URL or its subject: both forfeit the ranking this whole exercise is built on. And never promise a position. You can promise a better pitch to people already being shown the page; ranking is the search engine's decision.

Also worth catching here: **cannibalisation**, two URLs ranking for the same query and splitting the signal. Flag it; the merge decision belongs to a human.

## Is a long visit interest or confusion?

Five minutes on a page means two opposite things: careful reading of something that matters, or a reader who cannot work out what the page is telling them. The reliable disambiguator is negative feedback on the same page ([`get_negative_feedback`](../../mcp/analytics/get-negative-feedback.md)).

| Dwell | Negative feedback | Reading |
|---|---|---|
| Well above the site median | Any | **Problem**, high severity. They keep re-reading because something is not clear |
| Well above the site median | None | **Signal**, genuine interest. Consider expanding it; do not "fix" it |
| Well below the median | Any | **Problem**. Short and disliked |
| Around the median | Several | **Problem**, medium |
| Very low dwell, no feedback | — | Likely a title or discoverability problem rather than a content one |

The median is computed from this site, never from a global norm: every documentation set has its own attention pattern, and a reference corpus read in ten-second glances is not failing. Never recommend deleting a page on dwell time alone.

## Are the calls to action dead?

Two failure modes here: an action that gets impressions and few clicks, and a page that gets traffic and no outgoing clicks at all.

Compare each action's click-through against the median for the same label **on this site**. Flag where it falls well below with enough impressions to matter — the floor is around 200 impressions, below which this is noise. Revenue-bearing actions rank above informational ones.

A low rate can be entirely legitimate: an explanation page is not supposed to convert. When in doubt, report it as medium rather than high, and say what would settle it. The common shapes are: the action is buried or badly worded; the wrong action sits on the wrong page (a sign-up prompt on a page whose readers have already signed up); or the page is genuinely terminal and should either link onward or be redirected. [Conversion](../writing/conversion.md) covers what a working call to action looks like.

## Did the campaign land on the page it promised?

Campaign-tagged traffic arriving on a page that answers a different question bounces in seconds. Map tagged entries against landing pages and find where the promise and the page disagree: high bounce on a specific campaign, a campaign with traffic and no conversions, a campaign landing on a 404 or on the root. The successful ones matter too — say what made them work, so it can be repeated.

Never include raw referrer query strings in the report.

## Which kind of reader fails? Cohorts

Page-level analytics say which page does badly. Cohorts say which *kind* of reader fails, which is usually what product and marketing actually need.

Take the most active anonymous readers ([`get_top_visitors`](../../mcp/analytics/get-top-visitors.md)), pull each one's timeline ([`get_visitor_activity`](../../mcp/analytics/get-visitor-activity.md)), and cluster them into a handful of named behavioural patterns: a reader who visits pricing and leaves negative feedback without converting; one who repeatedly reads the same integration page without ever acting; one with wide coverage, long dwell and no negative signals.

Labels are descriptive and lowercase-kebab, never numeric — "pricing-bounce" tells somebody something and "cohort 3" does not. Report direction of travel, never headcounts: identifiers are anonymous and merge or split with the network. Never include user agents, IP addresses or referrer strings.

## Who is deciding, and what stops them? Buying stage

Every other reading answers "which page fails". This one answers "which reader fails, and at what point in deciding to pay". The same sentence about rate limits is a lost sale from someone evaluating and a support ticket from a customer; aggregated by topic the two are indistinguishable, and the pricing objection disappears into a cluster of API questions.

1. **Get the stage split first** — evaluating, asking about price, integrating, needing support — in counts and shares ([`get_chat_intent`](../../mcp/analytics/get-chat-intent.md)). The distribution is itself the first finding.
2. **Decide who the documentation actually serves.** If pre-purchase conversations are a small minority, this is a support surface rather than a sales surface, and that is a headline finding: the product is spending its highest-intent page real estate on people who have already paid. If a stage is absent entirely, say so and give the likeliest reason — an absent pricing stage in a product that charges money is a signal, not a clean bill.
3. **Extract the blocker, not the topic.** The question is never "what was this about"; it is *what did this reader need to know before they could stop hesitating, and did they get it*. Sort into **unanswered** (asked and hit a wall — the strongest evidence available), **answered badly** (an answer existed and did not settle it), and **answered but insufficient** (the fact is present, the reassurance is not).
4. **Name the missing page.** If one already covers the ground, the problem is framing or findability, and the fix is a rewrite rather than a new page.

Respect the floors: five conversations before characterising a stage, three independent conversations before calling something a blocker pattern. Below that, quote the raw text as anecdote and say the volume does not support a conclusion.

### The competitive pass, done separately and last

When a reader names another product mid-conversation, they have handed you what they are comparing you against, in their own words, at the moment of deciding. Record who, and in what context:

- **Comparison** — they are choosing, and a positioning page is missing.
- **Migration** — they have chosen and are blocked on mechanics. This is the highest-value context in the whole report.
- **Complaint** — a feature-gap report from someone who wanted to buy. Check whether the capability exists and is merely undocumented before escalating it to the roadmap.

Then record which page's absence left it unresolved.

Report only competitors readers actually named, never the ones the team worries about. **Never characterise a competitor's pricing, limits or features from these conversations.** A reader's description of a rival is hearsay, often stale and sometimes wrong. Record what the reader believes, attributed to the reader; verifying it is [an external check](./external-checks.md), and reading the market position is [the competitors lens](../lenses/competitors.md).

## Related

<!-- widget:cards plain cols=2 -->

- [Reading the numbers](./metrics.md) — windows, sample floors and the confounders every reading above inherits {chart-line}
- [Content detectors](./content-detectors.md) — what is wrong with the page a number pointed at {file-text}
- [Choosing a lens](./choosing-a-lens.md) — which of these readings this question and this evidence call for {compass}
- [Goals and funnels](./goals-and-funnels.md) — the owner's declared outcome, and why a zero there is ambiguous {target}
- [From finding to change](../writing/from-finding-to-change.md) — turning one of these findings into an edit somebody ships {pen-line}
- [Analytics](../../analytics/README.md) — the reports behind these readings {bar-chart-3}

<!-- /widget -->
