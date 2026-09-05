---
title: "Page feedback: what a thumbs-down can and cannot tell you"
description: "Add a one-click rating to every Docsbook page, see what it stores, where it surfaces, and how a thumbs-down becomes the next page you write — including what voluntary feedback is not evidence of."
tldr: "Readers rate a page with one click, and the vote is stored as an analytics event, a feedback.received webhook and — on a thumbs-down — a chat.negative_feedback webhook. Nothing personal is kept beyond a salted hash of the reader's IP. Feedback is voluntary, so it tells you where to look, not how good a page is."
---

# Page feedback

Page feedback in Docsbook is a **Was this page helpful?** control a reader answers with one click — no form, no email address, no account. The vote lands as an event against that page and as a webhook you can act on. Collecting it calls no model and costs nothing.

The rating is a **pointer**, not a score. This page is as much about what a thumbs-down does not prove as about how to collect one.

## What you get

- **A one-click rating on every page**, in one or two places, on every plan.
- **A vote that reaches your own systems immediately** — a `feedback.received` webhook, and a second `chat.negative_feedback` webhook on a thumbs-down, so a bad rating can land in your team's channel the moment it happens.
- **A per-reader trail.** In the visitor timeline the vote reads as "Rated the page helpful" or "Rated the page unhelpful", beside everything else that reader did, which is where a single vote becomes interpretable.
- **A queue that already knows what to do with it.** Two shipped agent routes start from negative feedback and from unanswered chat questions and end at a drafted page.

## What can a reader rate?

Three controls exist, and they are not the same measurement.

| | **Under the page** | **In the "On this page" panel** | **Under an AI answer** |
|---|---|---|---|
| What it rates | The page | The page | That one assistant answer |
| Where | At the end of the article, above the previous/next links | In the outline, below the table of contents | Beside each answer in the chat panel |
| Setting | **Rate this page** (Content tab) | **Rate Page** (Right Sidebar tab) | Part of [AI chat](./chat.md) |
| Default | **On** | Off | With the chat |
| On a phone | Shown inline | Behind the floating outline button, as a bottom sheet | Shown |
| Event it writes | `docs.page_feedback_up` / `_down` | The same | `docs.ai_like` / `docs.ai_dislike` |

The bar under the page is the one most projects want on. A reader reaches it by finishing the page, which is the moment they have an opinion; the outline control is seen only by a reader whose eyes are already on the right rail. The two page controls write into **one series** — they are two places to ask, not two metrics.

The AI-answer thumbs is a genuinely different series and carries different fields: the conversation id and the question that earned the vote, because a rating with only a path is a counter nobody can act on. **Report issue** in the answer's overflow menu writes the same dislike event.

**One vote per control, per page view.** After voting the buttons lock and a short thank-you replaces the question. The guard is per control, so a project with both page controls on can take two votes from the same reader on the same page — accepted deliberately: a reader who votes twice on purpose is telling you the same thing twice, and de-duplicating across surfaces would need shared state for no gain in signal.

## Turn page feedback on

Under the page (on by default):

1. Open your docs site while signed in.
2. Open Float Widget → **Settings** → **Content** tab.
3. Turn **Rate this page** on.

In the "On this page" panel:

1. Open Float Widget → **Settings** → **Right Sidebar** tab.
2. Turn **Rate Page** on.

Both are also settable from an MCP client with `update_ui_settings` (`show_content_feedback`, `show_page_feedback`).

## What is stored per vote

A page vote is deliberately thin. There is no free-text box on either page control, no session id and nothing a reader typed:

| Where it goes | What it carries |
|---|---|
| Analytics event | Event name (`docs.page_feedback_up` or `_down`), your project, the page path, the reader's IP and country. The direction is encoded in the **event name**, because the analytics dataset's schema rejects an unknown `vote` field outright |
| `feedback.received` webhook | `page_path`, `vote` (`up`/`down`), `comment` (always `null` from these controls), `country` — plus a visitor id |
| `chat.negative_feedback` webhook, on a down vote only | `session_id`, `page_path`, `type` (`thumbs_down`), `comment` |
| Visitor identity | A salted SHA-256 of the reader's IP scoped to your project, truncated to 16 hex characters. It is the same hash the rest of your analytics uses, so a vote can be joined to that reader's other events — and it is not reversible to an address |

Two behaviours are worth knowing because they change what your numbers mean:

- **Votes from your own team are excluded from analytics but still sent to your webhooks.** Internal traffic is skipped on the analytics write, on the grounds that you testing your own page is not a reader signal — but the owner should still be told a rating happened.
- **The `comment` field exists in the payload and is never filled by these controls.** It is there for a surface that collects one; today neither page control does.

An AI-answer vote stores its project, the page the reader was on, the conversation id and the question — no answer text, no reader identity beyond the same IP hash.

## What the owner sees

| Surface | What it shows | Plan |
|---|---|---|
| **Analytics → Feedback tab** | Thumbs up and down, in total and per page, top 20 rows sorted **dislikes first** — the downvoted page is the one to fix, the upvoted one only confirms what already works | Every plan |
| **Feeds / visitor timeline** | Each vote as its own event on a reader's trail, toned as a win or a problem | Every plan |
| **`feedback.received` and `chat.negative_feedback` webhooks** | The vote, at the moment it happens, to a URL of yours — signed and retried, unlike [chat hooks](./chat-hooks.md) | Every plan |
| **`get_negative_feedback` (MCP)** | Pages ranked by dislikes | Pro |
| **`get_ai_unanswered` (MCP)** | Chat questions that produced no answer — the other half of the same signal | Pro |

Registering a webhook is open on every plan; both the MCP path and the REST path check the same capability, and only three advanced events (traffic spike, traffic drop, MCP tool called) are separated out. Several MCP tool descriptions still announce these two events as Pro — that text is stale rather than the behaviour.

> **Under question — read the Feedback tab as the AI-answer series, not the page series.** The tab's totals and per-page rows are built from a query over `docs.ai_like` / `docs.ai_dislike`, the events the *AI answer* thumbs writes. The page controls write `docs.page_feedback_up` / `_down`, and no query behind that tab reads them. So a page vote today reaches your webhooks and the visitor timeline, and does not reach the Feedback tab's counts. `get_negative_feedback` has the same shape: its own code comment states that the page-level event is "not folded in here". Until this is corrected, treat the Feedback tab as a measure of assistant answers and use the event feed or a webhook for page votes.

## From a thumbs-down to the next page you write

A rating is not the finding. What makes it actionable is what sits next to it: the searches that returned nothing, the questions the assistant could not answer, and what the reader did after voting.

Two agent routes ship with that sequence already wired, both on Pro:

**Improve docs from user feedback** — suggested to run weekly. It reads the pages readers marked bad, then reads *what earlier fixes to those pages already did* before repeating one, then asks what job the reader was trying to finish, and only then edits. The change-history step exists because the version without it measured a page's health seconds after rewriting it, which is a number that cannot have moved yet.

**Fill gaps from assistant conversations** — suggested to run on the `chat.no_answer` event. It reads the questions the assistant could not answer, separates a documentation gap from a bad question, picks the one worth writing today, and drafts that page.

The prompts behind every **Improve** button in the panel carry the same four rules, and they are the rules to apply by hand too: judge every number against something and say what you compared it to; quote the pages and events you actually read; a metric you cannot read is missing, not zero; and stop at the diagnosis before editing anything.

Collecting a rating calls no model and is not metered. The agent routes above are model work and draw on your project balance — see the [pricing page](https://docsbook.io/pricing).

## Why this is the right way (evidence)

| Rule | Why it works | Source |
|---|---|---|
| Treat the rating as a pointer, never as a page's score | Voluntary review systems carry two self-selection biases — acquisition bias and underreporting bias, where "consumers with extreme, either positive or negative, ratings are more likely to write reviews than consumers with moderate product ratings" — which together "render the mean rating a biased estimator of product quality" | Hu, Pavlou & Zhang, 2017 — [On Self-Selection Biases in Online Product Reviews](https://aisel.aisnet.org/misq/vol41/iss2/8/), *MIS Quarterly* 41(2) |
| Expect almost nobody to vote, and do not read silence as approval | Observed across four long-running online communities with 63,990 participants and 578,349 posts, "less than 25% of actors made one or more posts", and the top 1% produced 74.7% of the content | van Mierlo, 2014 — [The 1% Rule in Four Digital Health Social Networks](https://pmc.ncbi.nlm.nih.gov/articles/PMC3939180/), *JMIR* (peer-reviewed observational study) |
| Do not conclude a page is bad from a low vote count alone | "Nonresponse can, but need not, induce nonresponse bias in survey estimates", and "there is no minimum response rate below which survey estimates are necessarily subject to bias" — a rate is not itself the problem | Groves, 2006 — [Nonresponse Rates and Nonresponse Bias in Household Surveys](https://academic.oup.com/poq/article/70/5/646/4084443), *Public Opinion Quarterly* 70(5) |
| Pair every rating with the behaviour around it before acting | Bias "occurs as a function of how correlated the survey variable is to the propensity to be measured" — so the question is not how many voted but whether the readers who vote differ *on the thing you are measuring*. A confused reader and a satisfied one do not press the button at the same rate | Groves, 2006 — [same paper](https://academic.oup.com/poq/article/70/5/646/4084443) |

The practical reading of those four rows: a page with ten thumbs-down is worth opening; a page with three thumbs-up is not evidence that it works; and a page with no votes at all is a page you know nothing about, not a page nobody disliked.

## Limits

- **The Feedback tab does not currently count page votes.** See the under-question block above. This is the one claim on this page a previous version of these docs got wrong, and it is stated here rather than quietly dropped.
- **A vote carries no reason.** Neither page control collects free text, so a thumbs-down tells you *that* something was wrong and never *what*. The AI-answer dislike is richer only because it carries the question.
- **Ratings are per view, not per reader.** A reader who returns tomorrow can vote again, and a project with both page controls on can take two votes from one reader on one page view.
- **Feedback is most informative on instructional pages** — tutorials and how-to guides, where a reader either finished the task or did not. On a parameter table, a rating tells you close to nothing.
- **We publish no benchmark of what a Docsbook feedback rate looks like.** No cross-customer distribution has been measured, so there is no "healthy" number to compare yourself against. The external sources above are about voluntary feedback in general, not about Docsbook sites.
- **A comment field is in the payload and nothing fills it.** If you build a surface that collects one, the webhook contract already has a place for it; out of the box it is always `null`.

## Related

- [AI chat](./chat.md) — the assistant whose answers carry their own, separate thumbs.
- [Answer quality](./answer-quality.md) — what happens to a question the assistant could not answer.
- [Full-text search](./search.md) — failed searches are the other signal that a page is missing or misnamed.
- [Web analytics](../analytics/tracking/overview.md) — check a page's traffic before you rewrite it on three votes.
- [Webhooks](../reference/webhooks.md) — `feedback.received` and `chat.negative_feedback` in full, signed and retried.
