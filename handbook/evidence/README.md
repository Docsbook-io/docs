---
title: "Evidence: what this handbook knows, and who says so"
description: "Every claim in the handbook is graded established, contested or hypothesis, and each one names the sources under it — vendor documentation, a study, a named framework, a practitioner report, or our own measurement."
tldr: "Claims are graded in three tiers. Established means a vendor, a specification, a peer-reviewed study or our own measurement stands under it and you may state it to a customer. Contested means real evidence points both ways. Hypothesis means it is plausible and widely repeated but not settled — quote the mechanism, never the number."
---

# Evidence

Most documentation advice arrives as assertion. This handbook grades it instead, because the expensive mistakes in this field are not wrong facts — they are confident ones.

"Add an `llms.txt` and Google will cite you" and "answer the question in the first two paragraphs" are both things practitioners say with the same certainty. One of them is contradicted in writing by Google; the other is supported by a peer-reviewed study. A handbook with one voice for both is worse than no handbook, because it launders a webinar into a commitment somebody spends a sprint on.

## The two registries

<!-- widget:cards cols=2 -->

- [Claims](./claims.md) — the knowledge itself, graded, each with the mechanism, the sources, a test you can run on your own site, and what being on the wrong side of it costs. {scale}
- [Sources](./sources.md) — the references, each with what it actually says, verbatim, and the date we last opened it. {book-open}

<!-- /widget -->

## How a claim is graded

| Standing | What it means | What you may do with it |
|---|---|---|
| `established` | A vendor's own documentation, a published specification, a study with a stated method, or our own dated measurement stands under it | State it to a customer. Quote the source after it. |
| `contested` | Real evidence points both ways, and the disagreement is itself the useful thing to say | Present both sides. The disagreement is the finding. |
| `hypothesis` | Plausible, widely repeated, not settled | Quote the **mechanism**, never the number. Run the test on the customer's own site and quote that instead. |

The grading is enforced rather than promised: a claim cannot be marked `established` unless a source at least as strong as a study or a vendor's own page is actually cited under it. Without that rule, a registry becomes a way to launder a talk into a fact by giving it an identifier.

## How strong a source is

| Kind | What it is | What it settles |
|---|---|---|
| Vendor documentation | The platform's own published page | "Does X work on this platform" — the platform is the one deciding |
| Standard | A specification or open proposal | What a format **is**. Says nothing about whether anyone honours it |
| Research | A study with a stated method, archived or peer-reviewed | Generalises to your site only as far as its own sample does |
| Framework | A named, published method | Not evidence that it works; evidence that it has a definition — which is what stops four people meaning four things by "reference page" |
| Field report | A practitioner's account — a talk, a write-up, our notes from one | Dated and attributable. Never enough on its own for a number said out loud to a customer |
| Our own measurement | A number we took, on a stated date, against a stated subject | Strong about that subject, silent about everyone else |

## Why every source carries a date

The date is when somebody actually opened the page and saw the line quoted from it — not when they remembered it, and not when the model was trained.

Two entries are why the field exists. Google's FAQ rich result was narrowed in 2023 and then removed from Search in May 2026, so any advice to add `FAQPage` markup was correct, then decorative, then wrong, without changing a word. And one vendor's crawler documentation moved host between two fetches in a single afternoon. **A citation with no date is a claim that the web is static.**

## What is deliberately not in here

House rules with no source outside our own opinion — "a rate with no denominator is not a finding", for instance — are not filed as claims. Filing them would mean either an unsourced claim or a citation invented to satisfy the field, and both teach a reader that the whole registry is decoration. They live in the handbook's method pages instead, stated as what they are: how we work.
