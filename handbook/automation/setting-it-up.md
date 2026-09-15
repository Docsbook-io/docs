---
title: "Setting up automation: the interview that comes before the first switch"
description: "Why every automation starts with five questions rather than a menu, how to offer options instead of a recommendation, and what to state about a monitor before you install it."
tldr: "Never install an automation before asking what went wrong, what should happen next time, who acts on it, how often is too often, and what must never happen automatically. Then offer two or three options with what each catches, what it costs and how it fails — and state the blind spot, the failure mode and the noise estimate before writing a file. An alarm that fires for everyone always is an alarm nobody reads by the third day."
---

# Setting up automation

Everything automated here exists because someone would otherwise have to remember. Documentation falls behind the code, a translation goes stale, a page slips off the first page of results, the assistant starts failing on a topic — and nobody notices until a reader does.

But automation that watches the wrong thing is worse than none. It produces noise, the noise trains everyone to ignore the channel, and the next alert — the one that mattered — is ignored with it. That is the single reason this page opens with questions instead of a feature list.

The sequence is five steps, and the first two of them write nothing at all:

| Step | What it does | What it may change |
|---|---|---|
| 1. Interview | Asks what you actually want watched | Nothing |
| 2. Design | Proposes the setup with its costs and its failure modes | Nothing |
| 3. Install | Writes workflow files, registers handlers, changes settings | Only what was agreed |
| 4. Prove | Fires a test through the real path and reports what happened | Nothing new |
| 5. Hand over | Names what runs, what it misses, and how to turn it off | Nothing |

## Why not just install the thing that was asked for?

Because the named request is usually the symptom. "Block pushes that change code without docs" is almost always a team that wants a pull request opened with the change already made; "alert us on traffic drops" is usually a team that wants to know about one section falling, not about a holiday weekend.

The interview costs three minutes and it is the difference between an automation that survives a quarter and one that gets muted in a week.

**Rules for running it:** one question at a time, reacting to each answer before asking the next. Skip anything the request already answered. Never open with a catalogue of what the platform can do — that turns a diagnosis into shopping.

## The five questions

### What went wrong that made you ask?

The most useful question and the one most often skipped. A concrete incident — "we shipped a rename and the docs said the old name for a month", "a customer quoted a price we changed in March", "our chat kept saying it didn't know about SSO" — names the trigger better than any menu.

If the answer is abstract ("we want better docs hygiene"), push once for the last time it actually hurt. If nothing comes back, that is a real answer too: there is no incident to design against, and the honest recommendation is usually a single cheap CI check plus one monitor, not a suite.

### What should happen when it happens again?

These five responses differ by an order of magnitude in trust and in cost. Put them on the table explicitly rather than choosing one on the asker's behalf:

| Response | What it means | What it costs |
|---|---|---|
| **Tell someone** | A message into a channel or an inbox | Cheapest. Does nothing on its own; someone must act |
| **File it** | An issue in the tracker, in the normal triage flow | Survives being ignored for a week. Needs someone to triage |
| **Propose a fix** | A pull request with the change already made | Highest value per incident, needs review, and needs the change to be safely derivable |
| **Fail the check** | A red pull request or a blocked push | The only one that genuinely prevents the problem. Also the only one that can stop a colleague's work at a bad moment |
| **Fix it silently** | Applied with no human in the loop | Reserve for mechanical, reversible changes. Never for prices, claims about other companies, or anything outward-facing |

Most requests that arrive as "block it" actually want "propose a fix". Ask.

### Who acts on it, and where do they already look?

An alert into a channel nobody reads is a channel nobody reads. Find the surface the team already uses — a chat channel, the issue tracker, the pull request itself, an inbox — and put it there.

Never create a new surface for an automation, and never route to two surfaces "so it definitely gets seen": duplicate alerts halve the attention each one gets.

Get the **owner** as well. An alert nobody owns is an alert everybody assumes someone else is handling.

### How often is too often?

Ask before installing, not after the first noisy week. Five values, and a monitor missing any of them will be noisy:

- **The threshold.** What size of change is worth a message? A five-place ranking drop on one page is noise; the same drop across a whole section is not.
- **The floor.** Below what volume should it stay quiet regardless of what the percentage says? [Monitors and alerts](./monitoring.md) carries the defaults.
- **The cadence.** Immediate, daily digest, or weekly? Most signals here move slowly and a digest beats an interrupt. Reserve immediate for things that are broken right now.
- **Quiet hours and days.** A weekend alert on a metric that moves weekly is pure cost.
- **The stop rule.** How many times can this fire about the same thing before it stops repeating itself?

### What must never happen automatically?

Ask this as its own question rather than inferring it, and name the candidates out loud:

- Pushing to a shared or public remote.
- Opening or merging a pull request.
- Changing anything readers see without review.
- Blocking a push or failing a build.
- Sending anywhere outside the team.
- Touching prices, plans, limits, or claims about other companies.

Whatever comes back is a hard constraint on everything installed in this run, and it belongs in the handover so the next person knows.

## Offer options, not a recommendation

Two or three concrete setups, each with three lines: **what it catches**, **what it costs**, **how it fails**. Never a single take-it-or-leave-it, and never everything the platform can do at once.

```
Three ways to catch the rename problem. Pick one, or tell me what to change.

(a) Pre-push drift check — warn only
    Catches:  a renamed symbol whose docs page still says the old name, before it ships
    Costs:    a few seconds on every push; occasional false positives you dismiss
    Fails:    silently, if the search index is down — you get a warning line, not a block

(b) Pull-request check
    Catches:  the same drift, plus malformed frontmatter and broken internal links
    Costs:    a CI job per PR; a red check when it finds something
    Fails:    loudly and in the right place, but only for changes that go through a PR

(c) Weekly drift digest into your issue tracker
    Catches:  accumulated drift across the whole repo, including what (a) and (b) missed
    Costs:    one issue a week, which someone has to triage
    Fails:    quietly — a week where nothing is filed looks the same as a week with no drift,
              unless we file an explicit "nothing found" note

Most teams with your shape start with (b) and add (c) after a month.
```

That last line is a recommendation, and it is welcome — **after** the options, not instead of them.

## What has to be said before anything is installed

Before writing a file, state five things and get agreement on them:

| | What to state |
|---|---|
| **The trigger** | The exact event or schedule, and the threshold with the sample floor under it |
| **The action** | What happens, and whether a human is in the loop before anything changes |
| **The blind spot** | What this setup will miss. Every monitor has one, and an unstated blind spot reads as full coverage |
| **The failure mode** | What happens when the source is unreachable, the plan gate refuses, or the event never fires. Silence must never be indistinguishable from health |
| **The noise estimate** | Roughly how often this will fire given the current numbers |

The noise estimate is the one that saves the channel. If the honest answer is "several times a day", the threshold is wrong, and this is the moment to fix it rather than the moment to install it and find out.

## What can actually be installed

| Route | What it is | Where it is described |
|---|---|---|
| **Drift** | Docs falling behind code, the live site, a pricing page, or any other source of truth | [Drift](./drift.md) |
| **Measurement drift** | A content change that broke what a goal matches, or shipped something no goal measures | [Drift](./drift.md) |
| **Events** | Something happens on the platform and a handler reacts | [Events and handlers](./events.md) |
| **CI** | A check on every pull request, or a guard before every push | [CI checks and repository hooks](./ci-checks.md) |
| **Monitors** | A standing watch over search, answer-engine, reader-behaviour or funnel signals | [Monitors and alerts](./monitoring.md) |
| **Tuning loops** | A recurring pass that adjusts something from real failure signal | [Monitors and alerts](./monitoring.md) |

Install what the interview settled on and nothing else. An extra "while I was here" automation is a change nobody signed off on, and it is the first thing that gets blamed when the channel goes noisy.

Keeping a capability *configured* is automation; deciding what a capability should be set to in the first place is [Site capabilities](./site-capabilities.md).

## How do you know it works?

An automation that was installed but never fired is indistinguishable from one that is broken.

- **Fire a test through the real path** — the event, the workflow, the alert — and confirm it arrived where it was supposed to. Not that the send returned success: that it landed.
- **When a dependency is not live yet** — an event the platform does not emit, a channel not yet connected — say so explicitly and leave what you wrote in place. A handler that exists before its event does is useful the moment the event ships; a handler deleted because registration failed has to be rebuilt from scratch.
- **Surface any secret exactly once**, and say where it must be stored.
- **Never claim a feature is on because the write that enabled it succeeded.** Check the thing that actually observes it — the rendered page, the delivery log, the feed.

## The handover

One message, and it names five things: what now runs, on what trigger, with what threshold; where it reports and who owns it; what it will not catch; what you must still do by hand (store a secret, connect a channel, merge the workflow branch); and **how to turn it off**.

That last one is not a courtesy. An automation nobody knows how to disable gets worked around instead, and the workaround is always worse than the automation.

## When the answer is "don't automate this yet"

Recommending against a setup is a real outcome of the interview, not a failure of it. Two cases come up constantly:

- **It has happened once.** A single incident is not a pattern, and a monitor built for it will mostly report nothing. Note what to watch for, and set it up if it recurs.
- **The underlying thing is broken, not drifting.** Automating a notification about a page that is simply wrong postpones fixing the page. Fix the page first — that is an [audit](../auditing/README.md) — and add the monitor afterwards.

## Traps

- **Nothing is installed before the interview.** Even when the request names the exact automation, confirm the trigger, the destination and the threshold.
- **A public, outward-facing action always needs consent** — pushing to a shared remote, opening a pull request on someone else's repository, sending to a channel, posting anywhere a third party sees it. The local half is safe; the outward half is asked for by name, with the target named.
- **Never block a developer's push by default.** Warn. Blocking is opt-in and set explicitly in the repository's own configuration.
- **Never fail loudly on a plan gate or an unreachable dependency, and never fail silently either.** Record it, keep what was already written, and continue with the rest of the run.
- **Never fabricate a command, a URL, a version or a limit** in generated content or generated configuration. Ground every concrete claim in the diff, the repository's own metadata, or the existing page. When unsure, link the source instead of guessing.
- **Never hardcode a credential in a generated file.** Reference a stored secret by name, and generate a fresh signing secret per registration.
- **Never alert on a sample too thin to mean anything.** Every threshold carries a volume floor.
- **Never delete a partially written file when a later step fails.** It is useful the moment the dependency lands.
- **One automation per problem.** Two monitors watching the same signal produce two alerts and half the trust.

## Related

- [Drift](./drift.md) — the guards for documentation falling behind its source of truth.
- [Monitors and alerts](./monitoring.md) — thresholds, volume floors, and when to remove a monitor.
- [Events and handlers](./events.md) — what the platform emits and how to react to it.
- [CI checks and repository hooks](./ci-checks.md) — the checks that run before a reader sees anything.
- [Site capabilities](./site-capabilities.md) — what each setting gives a reader, and when it is worth turning on.
- [Auditing](../auditing/README.md) — finding what is wrong now. A monitor is worth creating once you have found the same thing twice.
