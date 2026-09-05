---
title: "How Docsbook proves what it claims"
description: "The evidence rule every capability page in these docs follows: the mechanism in detail, a source you can open, and an explicit list of what is not proven."
tldr: "Every capability page here states what you get, how it is built, the evidence with a link to a primary source, and what is not proven. Claims we cannot source are marked Under question rather than quietly dropped."
---

# How Docsbook proves what it claims

Documentation platforms are sold with adjectives — advanced, intelligent, optimised. Adjectives are unfalsifiable, so they carry no information. These docs are written to a rule instead: **a capability page must let a sceptical engineer check us**. If a sentence cannot survive the question "says who?", it does not ship.

This page is the rule itself, so you can hold us to it.

## What every capability page contains

Each page under [SEO](./seo/README.md), [GEO](./geo/README.md), [AEO](./aeo/README.md), [Agent-ready content](./agent-ready/README.md), [AI chat](./ai-chat/README.md), [Analytics](./analytics/README.md) and [Translations](./translation/README.md) carries four blocks, in this order.

| Block | What it must contain | How to check it |
|---|---|---|
| **What you get** | The outcome in your terms — what appears on the page, in the panel, or in the API | Open your own site and look |
| **How it is built** | The mechanism at the level only someone who read the implementation could write: thresholds, order of preference, fallbacks, what happens on failure | Compare against the rendered HTML, the API response, or the exported data |
| **Evidence** | Each rule as *rule → why the machine or the reader behaves that way → a link to a primary source* | Open the link |
| **Limits** | What the feature does not do, what is not measured, what depends on a model version we do not control | Judge whether we left anything out |

A page with no limits block is a brochure, and brochures are believed less, not more.

## What counts as a source here

We rank sources, and the ranking is visible in how a claim is worded.

1. **Specifications and vendor documentation** — Google Search Central, schema.org, W3C, the IETF, the Model Context Protocol specification, the llms.txt specification, and the published documentation of the model providers involved. A claim resting on one of these is stated flatly.
2. **Peer-reviewed or preprint research with a stated method and sample size.** Stated with the method attached: "measured on 10,000 queries" tells you how far to trust it.
3. **Independent studies with published methodology.** Always attributed in the sentence — "X measured", never "it is known that".
4. **Vendor-reported results, including our own.** Labelled as vendor-reported. Our own internal measurements are labelled as ours.

Anything below that line is not evidence, and does not appear.

## What we deliberately do not claim

These are the claims a documentation vendor is expected to make, and the reason we do not make them.

- **No citation-rate lift.** Nobody can honestly promise that turning on a feature makes Perplexity or ChatGPT cite you N% more often. What has been measured in controlled work is narrower than the marketing version of it, and [GEO](./geo/README.md) says exactly what was measured and by whom.
- **No AI answer-accuracy percentage.** A number produced on our own corpus, with our own grader, is not evidence about your corpus. [AI chat](./ai-chat/README.md) describes what the pipeline does to stay grounded and what it measures, without inventing a score.
- **No ranking guarantees.** Search ranking is not a contract, and Google says so in its own documentation. [SEO](./seo/README.md) separates what is documented by Google from what is inference.
- **No compliance status we have not earned.** [MCP security](./agent-ready/mcp-security.md) states the current position and names what is not offered yet.

## "Under question" blocks

When a claim in these docs cannot be verified — the mechanism changed, the source turned out not to say what it was cited for, or nobody has published a measurement — we do not delete the sentence and we do not soften it into vagueness. It becomes an explicit block:

> **Under question.** *The claim.* What is verifiable: *the part that is.* What is not: *the part that is not, and why.* Treat it as a hypothesis until measured.

That block is a promise about our process: a claim we cannot support is visible to you rather than quietly removed.

## How these claims stay true

Documentation drifts away from a product silently, which is the failure mode Docsbook exists to fix — so the same machinery runs on these docs.

- Every user-facing change ships with an entry in the [changelog](./CHANGELOG.md), stating what the change was meant to buy, not just what moved.
- The changelog is projected into [per-outcome pages](./changelog/outcomes/README.md), so you can read the history of one outcome — AI citations, support load, organic traffic — rather than a flat list.
- Pages carry a visible last-modified date taken from the commit that changed them, so a stale page cannot pretend to be current. See [GEO](./geo/README.md).

## Found something wrong?

A claim on these pages that does not match what the product does is a defect, and we would rather hear it from you than have it sit there.

- Email [support@docsbook.io](mailto:support@docsbook.io) with the page and the sentence.
- Or say it in the [Docsbook Discord](https://discord.gg/baqUCdwrag).

## Related

- [Overview](./overview.md) — what Docsbook does, end to end.
- [Pricing](./pricing.md) — what is metered and what a project balance pays for.
- [FAQ](./faq.md) — cost, cancellation, sync, privacy and data ownership.
