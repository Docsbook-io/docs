---
title: "Documentation Analytics: What to Track in 2026"
description: "Most docs analytics show pageviews and stop. This is the practical guide to documentation metrics that actually matter — failed searches, AI questions, negative feedback, and what each tells you."
---

# Documentation Analytics: What to Track

Pageviews lie. Top pages by views tell you which pages are popular, not which pages are useful. The metrics that actually move documentation quality are different.

This is the working set we ship to Docsbook customers.

## TL;DR

The five metrics that change behavior:

1. **Failed searches** — what users tried to find and could not
2. **AI questions with no answer** — same signal, conversational form
3. **Negative feedback (👎)** — pages where the user actively reported failure
4. **Page journeys** — what users do before bouncing or converting
5. **Top failed pages** — pages that get traffic but get the worst feedback

Pageviews and bounce rate are background context, not action drivers.

## Failed searches: the highest-leverage metric

A failed search is a user who knew exactly what they wanted, typed it, and your docs returned nothing.

Every failed search is a content gap with a known title. The user told you what to write.

In Docsbook, `get_failed_searches` returns the list ordered by frequency. The top 10 in any given month usually map directly to the next 10 docs pages you should write.

Examples we have seen across customer docs:

- "how to revoke an api key"
- "rate limit headers"
- "what happens when my plan expires"
- "self-hosted deployment"
- "delete account"

Each one is a documentation backlog item with a search-query-shaped title.

## AI questions with no answer

If you run an AI chat on your docs, log the questions where the AI returns a hedged or empty answer. Same signal as failed searches, often with more context.

`get_ai_unanswered` in Docsbook MCP returns these. The pattern: users ask things, the LLM cannot find a confident answer in your content, you see what was asked.

Difference from failed searches: AI questions tend to be longer, more contextual, and reveal user mental models.

Failed search: "stripe webhook"

AI question: "I keep getting 401s on my Stripe webhook even after I added the signing secret. What am I doing wrong?"

The AI question is gold for content design.

## Negative feedback

A thumbs-down on a docs page is a user who read the page and concluded it did not help. This is the rarest and most valuable signal.

`get_negative_feedback` in Docsbook MCP returns the pages and the optional written feedback.

What to look for:

- A page that gets 10+ pageviews per 👎 is performing fine
- A page that gets 2–3 pageviews per 👎 is broken — rewrite
- A page that gets 0 pageviews has no signal, ignore

## Page journeys

Where users go after a page tells you whether the page closed the question or kicked the user to a different page.

`get_page_journeys` in Docsbook MCP returns common multi-page paths.

Patterns to look for:

- **Bounces from quick-start** — your quick-start is too long, or your CTA is wrong
- **Loop between two pages** — users are confused about which one applies
- **Pageviews → search → exit** — the page led the user to question more, then they failed to find it

## What pageviews are good for

Pageviews are background context. They tell you scope, not health.

A page with 10,000 pageviews/month and a 4% negative-feedback rate is more urgent than a page with 100 pageviews/month and a 10% negative-feedback rate. Volume × failure rate = total bad UX.

## What bounce rate is good for

Bounce rate from documentation is often misleading. A bouncing user might be a happy user who read the answer and left. Or a frustrated user who saw the page and immediately closed the tab.

To disambiguate, use:

- Time on page (low + bounce = bad, high + bounce = OK)
- Scroll depth (no scroll + bounce = bad)
- Feedback widget interaction

## What we have stopped tracking

- **Average session duration** — too noisy, conflated with idle browser tabs
- **Pages per session** — high pages-per-session can mean users are searching unsuccessfully
- **Geo distribution at the page level** — useful for translation planning, not for content quality

## Cohorts that matter

Three slices:

### New vs returning

New users hit your quick-start. Returning users hit your reference. Different pages, different success criteria.

### Logged in vs anonymous

Logged-in users are deeper in the funnel. Their bounce signals are stronger.

### Referrer source

Direct, search, AI search (perplexity.ai, chat.openai.com, claude.ai), social. Each cohort has different intent. AI-search referrals are often the deepest-intent traffic.

## Track AI search referrals separately

In Docsbook analytics, filter referrers by:

- `perplexity.ai`
- `chat.openai.com`
- `claude.ai`
- `gemini.google.com`

This is the AI distribution channel from the user's side. Track conversion from these referrers separately — they often convert better than Google traffic.

## What to do with the data

A working monthly ritual:

1. Pull failed searches, AI unanswered, negative feedback (3 queries, 5 minutes)
2. Group by topic — multiple queries about "X" mean one missing page
3. Pick the top 3 by frequency × revenue impact
4. Write the missing pages
5. Re-check next month

This is the highest ROI loop in documentation. Each iteration turns a known content gap into a search-engine-indexed page that AI search can cite.

## Related reading

- [Documentation SEO guide](./documentation-seo-guide.md)
- [AI chat for documentation: build vs buy](./ai-chat-for-documentation-build-vs-buy.md)
- [How to get docs cited by ChatGPT](./how-to-get-docs-cited-by-chatgpt.md)

---

Docsbook ships failed-searches, AI-questions, and negative-feedback analytics on PRO, with page journeys on PRO+. [See it on your docs →](https://docsbook.io/start)
