---
title: "Drift: catching documentation that has fallen behind its source of truth"
description: "The five kinds of drift, which of them can safely be fixed automatically and which may only ever be proposed, and the guard that catches a rewrite quietly breaking what measures it."
tldr: "Drift is the gap between what the docs say and what is true, and it has five different sources of truth — code, the live site, another company, the docs themselves, and the goals that measure them. Only code-to-docs and measurement drift are safely automatable end to end; a wrong price or a claim about another company is always proposed, never rewritten. The measurement kind is the one that fails with no error at all."
---

# Drift

Drift is the gap between what the docs say and what is true. It has several sources, and they need different guards, because "true" means a different thing in each.

| Source of truth | What drifts | How it is caught |
|---|---|---|
| **Code** | A renamed symbol, a changed signature, a removed flag, a new required argument | Diff-triggered, on push or in CI |
| **The live site** | A price, a plan name, a limit, a feature that shipped or was withdrawn | Scheduled, against the public page |
| **Another company** | A partner's API, a competitor's limit, an external link | Scheduled, and on a known breaking change |
| **The docs themselves** | A translation behind its source, a page nobody has reviewed, a leftover promise | Scheduled, on an age threshold |
| **What the docs are measured by** | A goal pointing at an anchor a rewrite renamed; a funnel step on a page that moved; new content nothing measures | Diff-triggered, on the same push as the content change |

Only the first and the last are genuinely automatable end to end. The rest produce **proposals** — a wrong price or a claim about another company is never rewritten without a human. That boundary comes from [how a finding becomes a change](../writing/from-finding-to-change.md) and it holds here without exception.

## Code to docs

The one route where an automated rewrite is defensible: both sides are in the repository, the diff says exactly what changed, and the change is reviewable before it ships.

### The pipeline

1. **Clean up first.** Remove any leftover working directories from previous runs before doing anything else. They are always garbage, and a stale one produces a confusing partial result.
2. **Offer the hook once.** On the first run, offer to install a [pre-push hook](./ci-checks.md) so this happens by itself. On later runs, do not ask again.
3. **Detect what changed.** Compute the diff against the remote merge-base. **If no non-documentation files changed, exit cleanly** — this is the common case and it must be fast and silent. Detect also whether the docs live in a regular folder or a submodule; the apply step differs.
4. **Check the search dependency is reachable.** Semantic search over the docs is what makes this route work at all. If it is unreachable, **abort with one clear line — never block the push silently.**
5. **Cluster the changed files** into semantic groups, each with a hypothesis about which documentation might have drifted. On failure, fall back to grouping by top-level directory.
6. **Search per cluster, in parallel isolated working directories.** Each search returns candidate pages with a confidence score.
7. **Rewrite only above the confidence threshold** — 0.6 is a sane default. Below it, report the candidate rather than editing it.
8. **Curate before applying.** One pass over all the proposed edits together: resolve conflicts between clusters, normalise style, drop speculative edits, and — critically — **verify that every concrete claim is grounded in the diff, the repository's own metadata, or the existing page.** A generated install command that appears nowhere in the repository is the exact failure this step exists to catch.
9. **Apply atomically.** For a regular folder: apply, stage, amend the commit. For a submodule: apply in the submodule, commit there, **ask before pushing to its remote**, and only then fast-forward and amend the parent.
10. **Clean up** unconditionally on success or a no-op; **keep the working directories on a failure or a pending consent**, so the state can be inspected.
11. **Report** as structured output: status, commits, pending pushes, and anything needing human review.

### What makes this route go wrong

- **Warn, do not block, by default.** Exit non-zero only when the repository's own configuration explicitly asks for it.
- **Never amend an empty edit list.** "No doc edits needed" and exit.
- **Cap the diff** passed to the clustering step — 50 KB is a sane default — and truncate larger ones with a note rather than silently.
- **Cap how much of a page one pass may rewrite.** Forty per cent is a sane default. An edit beyond that is not a drift fix, it is a rewrite, and it needs a human.
- **A timed-out cluster is skipped and logged**, never a reason to abort the others.
- **Pushing to a submodule's remote is a public action.** The local commit needs no consent; the push is asked for by name, with the SHA, the remote and the branch stated. Only a CI configuration set deliberately may override that.
- **No fabricated commands, URLs, versions or limits.** When unsure, link the README rather than guessing the install line.

## The live site to docs

The docs quote a price, a plan name, a quota. The live page changes. Nobody updates the eleven mentions scattered through the documentation.

Schedule this against the **live public page**, not a constants file — the whole value is that one side of the comparison is what a customer actually sees. The comparison method, the four verdicts and the traps live in [external checks](../auditing/external-checks.md); the automation's job is only to run it on a schedule and route the result.

Natural triggers:

- Immediately after any pricing or packaging change — the run that pays for the whole thing.
- Before a launch or a campaign that drives people into the docs.
- Quarterly as a floor. Quotas and limits drift more quietly than headline prices, because nobody announces them.

The cost of skipping it is not only a stale page. Measured live across Perplexity, GPT and Gemini with web search on one real product: the brand's site was found in 9 of 9 answers, and those answers repeated "the API is coming soon" in 5 of 9 and "no pricing published" in 3 of 3 — while the API was live with 96 operations and the price sat on the landing page (Docsbook GEO audit, 3 September 2026). A stale sentence does not sit quietly on your site; it gets recited back to your buyers by machines.

**The output is always a proposal, never an applied edit.** A wrong number in the docs may mean the live page changed without a decision anyone signed off, and an automatic rewrite erases the evidence of that.

## The outside world to docs

Claims about third parties decay with no commit on your side, no failing test and no incident. Nothing in your own workflow will ever surface it, which is exactly why it needs a schedule.

Run it quarterly as a floor, and on a trigger when a partner ships a breaking change — that run is scoped to the one vendor and is much faster than a sweep. The verification method, the verdicts, and the rule that **unverifiable is its own verdict** are in [external checks](../auditing/external-checks.md).

Route the result as a proposal. Where the check finds a dead external link, that fix is mechanical enough to propose as a pull request. Where it finds a contradicted claim about another company, it is a sentence for a human to approve.

## The docs to what measures them

This is the drift class with no external source of truth, and the only one that fails without producing a single error. Nothing breaks. No link 404s, no test goes red, no page contradicts anything.

A goal declared against `#pricing` keeps drawing its chart after a rewrite renamed that heading to `#plans-and-pricing` — and the chart draws a flat line at zero, which reads *exactly* like readers refusing to convert. The owner then spends a quarter rewriting a page that was never the problem, and the audit that told them to does not know it was wrong either.

Anchors are unusually easy to break this way. Measured across 21,827 headings in one repository, 6.3% of generated anchors did not match the id the renderer actually emitted, and 263 collapsed to nothing but hyphens; on a clean English corpus of 2,968 headings it was 1.7%, concentrated on the most-used page, where every step of a quickstart missed because of an em dash (Docsbook corpus measurement, 5 September 2026). Nothing failed in any of those cases. The links simply led nowhere.

The rule worth automating is one sentence: **a goal is a claim about a page that still exists, and content changes without asking the goal.**

### When does this need to run?

On the same push as the content change, not on a schedule. This is a diff-triggered guard for the same reason the code route is: the diff says exactly what moved, and the fix is cheapest in the minute the author still remembers why they moved it.

A typo does not need it. Five kinds of change always do:

| What the diff did | What it can break |
|---|---|
| Renamed, removed or re-anchored a heading | Every section goal on that anchor drops to zero |
| Moved, merged, renamed or deleted a page | Every page goal and every funnel step on that path |
| Restructured navigation or internal links | The route still exists and nobody walks it any more |
| Added, removed or re-pointed a call to action | The macro goal now measures a destination nobody clicks |
| Shipped a new page, section or conversion action | Nothing breaks — the new thing is simply unmeasured, which is the more common case by far |

Note the shape of that last row. **Two different checks live here and only one of them is a repair:** whether what is declared still resolves, and whether what just shipped is measured at all. A guard that only does the first will run clean forever on a site that is slowly ceasing to measure anything it builds.

### The check itself

Reading what is declared is free on every plan — the results are the paid part, and this guard does not need them, which is what makes it safe to run on every push regardless of tier.

1. Read the declared goals and funnels, with what each one matches.
2. Resolve every matcher against the docs **as the diff leaves them**: does the anchor exist on a page, does the path resolve without a redirect, is the outbound host still the one the calls to action point at, is the event still emitted from the page the goal is scoped to.
3. Report an unresolvable matcher as a **measurement defect**, never as a conversion problem. Naming it as reader behaviour is the failure this guard exists to prevent, and it is worse than having no guard at all.
4. Ask the additive question against the diff: did this change ship something a reader is supposed to *do*, that no goal names?

### Routing what it finds

**Propose; never re-point a matcher automatically.** Re-pointing produces one series that spans a definition change, and a series that has silently changed meaning is the same failure as a funnel that silently drops a step — the number stays plausible and stops being comparable. The proposal carries the date, so whoever accepts it knows where the comparison restarts.

The additive half is a **suggestion, not a finding**, and the asymmetry is worth saying out loud: declaring a new goal costs nothing and loses nothing, because matching is retroactive — a goal declared today arrives with its history already filled in. There is no "we will add it once we have data". The data is already there.

Both halves belong to whoever owns the declaration; [goals and funnels](../auditing/goals-and-funnels.md) covers what a good one looks like, and the [goals and funnels reports](../../analytics/reports/goals-and-funnels.md) are where the numbers are read afterwards. The reading and the guard must not be run by the same automation: something that both changes what is measured and reports on the result can be trusted at neither.

**Warn, do not block.** A stale goal is not worth stopping a push over, and a guard that blocks on measurement gets disabled within a week — after which nothing catches the class at all.

## The docs to themselves

Age-based and parity-based drift, which needs no external source at all:

- **Stale pages.** A page untouched past a threshold — a shorter one for the pages everyone reads, a longer one for the rest. The event carries the page; the handler files it into normal triage.
- **Translations behind their source.** A translation more than a set number of days behind its source is flagged, and past a larger threshold the page itself should carry an outdated-content banner until it is caught up. A stale translation is worse than none, because it is trusted.
- **Leftover promises.** A "coming soon" past its date, a past date presented as a future one, a TODO left in a published page.

These are the cheapest automations available and the ones most worth having, because nothing else will ever surface them. Docsbook emits all three as typed events — `content_outdated`, `translation_outdated` and `translation_needed` — so the schedule is the platform's rather than yours; see [registering a content-outdated webhook](../../mcp/alerts/register-webhook-content-outdated.md) and [translation-outdated](../../mcp/alerts/register-webhook-translation-outdated.md), and [translations](../../translation/README.md) for what parity means.

Route them as filed issues rather than messages: they are not urgent, and they need to survive being ignored for a week.

**Deprecated content is flagged for a banner and a migration path — never for deletion, automatic or otherwise.**

## Related

- [Setting up automation](./setting-it-up.md) — the interview that decides which of these routes you actually want.
- [CI checks and repository hooks](./ci-checks.md) — where the diff-triggered guards run.
- [Monitors and alerts](./monitoring.md) — thresholds and volume floors for the scheduled half.
- [Events and handlers](./events.md) — what the platform emits, and how a handler should react.
- [External checks](../auditing/external-checks.md) — the comparison method behind the site and third-party routes.
- [Goals and funnels](../auditing/goals-and-funnels.md) — what a matcher is, and who owns the declaration.
