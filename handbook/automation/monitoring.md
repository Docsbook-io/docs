---
title: "Monitors and alerts: when a standing watch is worth installing, and how to tune it"
description: "How to design a threshold with a volume floor under it, which docs signals are worth a standing monitor, what every alert must carry, and when a monitor should be removed."
tldr: "A monitor is a standing question asked on a schedule, and it is worth creating once you have answered the same question twice by hand — not before. Every threshold needs four parts: the signal, what it is compared against, a volume floor below which it stays quiet, and a cadence matching how fast the number actually moves. A monitor that has never fired and one that fires every week without anyone acting are both broken."
---

# Monitors and alerts

A monitor is a standing question asked on a schedule. It is worth creating **once you have answered the same question twice by hand**, and not before: a monitor built for a single incident mostly reports nothing, and a channel that mostly reports nothing gets muted.

Everything here reads the same numbers an audit reads, and the confounders and sample floors in [metrics](../auditing/metrics.md) apply in full. A monitor that ignores them is a machine for producing confident false alarms on a schedule.

## How do you design a threshold?

Four parts, and a monitor missing any of them will be noisy:

1. **The signal.** One number, named, from one source.
2. **The comparison.** Against what — last week, the trailing median, the rest of the site? **A change compared against nothing is not a signal.** Traffic moves for reasons that have nothing to do with the docs, and a monitor that alerts on any movement alerts on holidays and launches. Where a site-wide trend can be subtracted, subtract it.
3. **The volume floor.** Below what sample does it stay quiet regardless of what the percentage says? This is the single most important field and the one most often left out.
4. **The cadence.** Immediate, daily, or weekly — matched to how fast the underlying number actually moves. Search data lags roughly two days and refreshes daily; alerting hourly on it is pure noise.

### Sensible volume floors

Unless the site's own volume argues otherwise:

| Signal | Stay quiet below |
|---|---|
| Any behavioural rate | ~30 visits in the window |
| A page's search position | Meaningful impressions — never alert on a position built from a handful |
| A rejected-search cluster | 2 separate visits |
| A question cluster | 5 questions |
| A route or journey pattern | ~50 sessions |
| An action's click-through | ~200 impressions |
| A dwell percentile | ~30 pageviews |
| A tuning pass | 5 combined signal items |

### The confounder that ruins traffic alerts

A traffic monitor that fires during a search engine's core update rollout is worse than no monitor, because it prompts exactly the wrong action. Google's own guidance is to "wait at least a full week after a core update completes before analyzing your site in Search Console", to avoid "quick fix" changes, and to avoid "making changes to content that's already performing well" ([Google Search Central, core updates](https://developers.google.com/search/updates/core-updates)). Build the rollout window into the monitor as quiet time, or the alert will arrive precisely when acting on it does the most damage.

When something does drop, the first split is diagnostic rather than corrective: impressions, average position and click-through rate separately, before and after the date. Fewer impressions means lost coverage, a worse position means lost ranking, and flat impressions with falling clicks usually means an answer is sitting above you — three different problems that look identical as "traffic dropped", with three different fixes.

## What is worth monitoring?

### Search and answer engines

| Watch | Trigger worth alerting on | Notes |
|---|---|---|
| Position on the pages that matter | A sustained drop across a **section**, not a single page | One page moving five places is normal variance. Compare against the site's own trend |
| The striking-distance band | A page entering it with real impressions | This is an opportunity alert, not a failure alert — route it to the work queue, not to a channel |
| Impressions with near-zero clicks | A page crossing the threshold and staying there for a full window | The title is usually the fix |
| Indexing and answer-markup switches | Any of them turning **off** | Rare, high-impact, and otherwise invisible |
| Assistant-crawler traffic | Meaningful crawler volume while the answer layer is off | The highest-value single alert in this whole section |

Never alert on a position taken from a single day's data, and never present lagged data as current. [How search works](../../seo/how-it-works.md) and [GEO](../../geo/README.md) cover what these numbers mean.

### Reader behaviour

| Watch | Trigger | Notes |
|---|---|---|
| The outcome mix of visits | The share of visits ending with nothing rising against the trailing period | The closest thing to a health metric the docs have |
| A page readers give up on | A page entering the top of the list and staying | Route it with the journeys attached, or the alert is unactionable |
| Searches returning nothing | A query crossing a repetition threshold | Feed the gap queue rather than alerting a person |
| Questions the assistant could not answer | A cluster forming above the floor | Same |
| Answers rated badly | A concentration on one topic | Distinguish "the page is wrong" from "retrieval missed it" before routing |

**Do not alert on a rising exit rate.** Pages readers leave from after succeeding are terminal success pages, and a monitor that flags them is a monitor recommending the rewrite of the best pages on the site. [Reader behaviour](../auditing/behaviour.md) has the full set of readings.

### Funnels and conversion

| Watch | Trigger | Notes |
|---|---|---|
| Completion of the paths that end somewhere that matters | A high-volume path's completion falling | Needs the volume floor; a path with ten sessions has no completion rate |
| The primary action's click-through | Falling well below the site's own median for the same label | The baseline is per-site, never global |
| A page with traffic and no outgoing clicks | Appearing and persisting | It might be genuinely terminal — check before treating it as broken |
| Campaign traffic bouncing | A campaign's landing page underperforming its peers | Only meaningful while a campaign is live |

Before trusting any of these, check that the matcher still resolves: [drift](./drift.md) covers why a goal reading zero is more often a measurement defect than a conversion problem.

### Freshness and correctness

The cheapest monitors to run and the ones nothing else will ever surface: stale pages, translations behind their source, leftover promises, prices against the live page, third-party claims against their sources. All are scheduled, all route to filed issues rather than messages, and all are described in [drift](./drift.md).

## Which of these does Docsbook fire by itself?

Several of the rows above exist as typed events you can subscribe to rather than schedules you have to build. Docsbook emits 18 of them; registering a webhook costs nothing against the project's balance, and the [Feeds panel](../../reference/webhooks.md) shows every event the workspace produced **including the ones no alert was watching** — which is how you find out what your docs actually emit before deciding what to be notified about.

| What you want watched | The event to subscribe to |
|---|---|
| A sharp fall in traffic | [`traffic_drop`](../../mcp/alerts/register-webhook-traffic-drop.md) |
| A sharp rise | [`traffic_spike`](../../mcp/alerts/register-webhook-traffic-spike.md) |
| Searches that returned nothing | [`search_no_results`](../../mcp/alerts/register-webhook-search-no-results.md) |
| A query becoming unusually popular | [`search_popular`](../../mcp/alerts/register-webhook-search-popular.md) |
| Questions the assistant could not answer | [`chat_no_answer`](../../mcp/alerts/register-webhook-chat-no-answer.md) |
| Answers rated badly | [`chat_negative_feedback`](../../mcp/alerts/register-webhook-chat-negative-feedback.md) |
| Page feedback left by a reader | [`feedback_received`](../../mcp/alerts/register-webhook-feedback-received.md) |
| A page crossing a staleness threshold | [`content_outdated`](../../mcp/alerts/register-webhook-content-outdated.md) |
| A translation falling behind its source | [`translation_outdated`](../../mcp/alerts/register-webhook-translation-outdated.md) |
| Usage approaching the plan's limit | [`usage_limit_approaching`](../../mcp/alerts/register-webhook-usage-limit-approaching.md) |

The thresholds on this page still apply to every one of them. A platform event tells you *when something happened*; it does not decide for you whether that something was above the floor, compared against anything, or worth a person's attention. [Events and handlers](./events.md) covers the registration mechanics and the things that fail silently.

## What does an alert have to contain?

An alert that says a number moved costs the reader a context switch to learn nothing. Every one carries:

- **The number, its absolute counts, and its window.** "Dead ends on /billing: 14 of 45 visits, last 7 days, up from 6 of 51" — not "dead-end rate up 15%".
- **What it is compared against**, and whether the site-wide trend was subtracted.
- **A link to the page or the report.**
- **One sentence on what to do next**, or the name of whoever decides.
- **A stop rule.** How many times this will repeat about the same thing before going quiet.

## Tuning loops

A tuning loop is a recurring pass that *changes* something based on accumulated failure signal, rather than only reporting it. Two are worth running.

### The assistant's instructions

Monthly, or three weeks after the last pass.

1. **Collect the failure signal** — the answers readers rated badly and the questions the assistant could not answer, over a fixed window. Keep the question, the answer, and any free-text reason. In Docsbook these are [`get_ai_unanswered`](../../mcp/analytics/get-ai-unanswered.md) and [`get_negative_feedback`](../../mcp/analytics/get-negative-feedback.md).
2. **Require a floor.** Below about five combined items, stop and say there is not enough to tune on. Never speculate a cluster into existence.
3. **Cluster by topic** — three to eight groups, each with a label, a count, up to three sample questions, and one sentence on the inferred failure mode.
4. **Distinguish the two failure modes first.** A topic no page covers is a content gap and needs a page written ([deciding the page set](../planning/page-set.md)); a topic a page covers well that the assistant never surfaces is a retrieval problem, and that is what this loop fixes. Tuning instructions to compensate for missing content produces an assistant that confidently answers from nothing.
5. **Propose a minimally invasive change.** Keep every existing voice, persona and refusal rule intact; add explicit guidance for the top three to five clusters. Keep the result short — long instructions degrade answer quality, so compress before showing.
6. **Show a before-and-after diff**, annotated so each changed chunk maps to the cluster that motivated it.
7. **Apply only on an explicit yes.** Writing [the system prompt](../../mcp/settings/set-chat-system-prompt.md) replaces the instructions for every conversation on the site; it is a destructive write and it is never automatic. Accept yes, no, or edit — and on edit, loop back to the diff.
8. **Report** what was applied, when, and when to run this again.

[AI chat](../../ai-chat/README.md) covers what the assistant reads and how the answers are produced.

### Translations

Enable auto-translation once and it keeps up on its own; the loop is about what auto-translation does not cover.

- **Validate the language set against what the platform actually supports** before writing anything, and check the plan gate before the first write — enabling half a configuration and then failing is worse than not starting. The supported set and the gate are on [`update_languages`](../../mcp/settings/update-languages.md).
- **Notify on batch completion** where someone reviews translations; skip the notification entirely where nobody does, rather than creating a channel for it.
- **Watch parity, not just completion.** A batch that completed is not a translation that is current — the parity rules are in [content detectors](../auditing/content-detectors.md), and [translations](../../translation/README.md) covers how Docsbook decides a page is behind.
- **Record the configuration where agents will read it.** A managed section in the repository's agent-context file, replaced by marker rather than rewritten, so the next session knows which languages exist and how they are produced.

## When should a monitor be removed?

Say this out loud at handover, and act on it the moment you see it:

- **It has never fired.** Either the threshold is wrong or the problem does not exist here. Both mean it should change or go.
- **It fires every week and nobody acts.** The threshold is too tight, or the alert is unactionable. Fix it or remove it; leaving it is what teaches people to ignore the channel.
- **The underlying thing was fixed structurally.** A monitor for a class of problem the architecture no longer permits is pure noise with an air of diligence.

## Related

<!-- widget:cards plain cols=2 -->

- [Setting up automation](./setting-it-up.md) — the interview that sets the threshold, the destination and the quiet hours before anything is installed. {settings}
- [Events and handlers](./events.md) — registering, verifying and proving the delivery path. {zap}
- [Drift](./drift.md) — the scheduled freshness and correctness monitors, in full. {git-compare}
- [Metrics](../auditing/metrics.md) — the confounders and sample floors these thresholds inherit. {chart-line}
- [Reader behaviour](../auditing/behaviour.md) — what the behavioural signals mean before you alert on them. {search}
- [Analytics](../../analytics/README.md) — where the numbers come from. {bar-chart-3}

<!-- /widget -->
