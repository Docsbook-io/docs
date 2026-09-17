---
title: "Conversion: documentation that asks for the sale"
description: "How to decide what each page asks the reader to do: classify the monetisation model from real signals, apply its pattern, and never invent a price."
tldr: "Documentation is the highest-intent surface a product has, and most of it never tells the reader what to do next. Read the destination the owner already declared; if none is set, classify the monetisation model from observed signals — paid, free-first, open-source or sales-led — and apply that model's pattern. When the signals are ambiguous, choose free-first: it is the only pattern that is safe when the money story is unknown, because it never states a price."
---

# Conversion

Documentation is the highest-intent surface a product has: the reader is already trying to succeed with it. Most generated documentation wastes that. It explains the product perfectly, never tells the reader what to do next, never names the price, and never mentions that there is a free tier at all.

This is a **content** concern. It decides which pages exist, what each page's closing action is, and how the money story is told. It never invents prices, plans or limits, and it never touches billing configuration.

## Has the owner already declared where readers should go?

Find out before classifying anything. Most platforms have a field for the one page the documentation exists to drive readers to; read it first.

**When it is set, it wins over anything you infer.** The owner typed it. A pricing page you found by crawling is a guess about their funnel, and their answer is not.

- Every page's primary action points there, unless a page has an obviously better-matching destination already observed on the source — an internal next step, or an install command on an open-source install page.
- The classification below still runs. The declared destination tells you *where* to send the reader, not *how* the product makes money — though a destination that is a pricing page is itself a strong paid signal, and one pointing at a demo form is a strong sales-led signal.
- It belongs in the **header as a single button**, not only in prose. One such button, not several: a header with three buttons has no call to action at all.
- Do not restate it on every page or in every paragraph. One deliberate placement per page, at the point where the reader has just got what they came for.

**When it is not set**, derive it from the source. If the derivation is unambiguous — a single obvious pricing, signup or demo URL observed on the source — save it back, so the assistant, the header and every later generation use the same destination. If it is ambiguous, ask. A wrong destination saved as the project's goal is worse than an empty field.

## Which monetisation model is this?

Derive it from real signals only, never from what the product feels like.

| Signal | Where to look |
|---|---|
| A pricing or plans page, or a nav link to one | Site, sitemap, navigation |
| Currency amounts, "/mo", "/year", "per seat", "per user" | Page text |
| "Free plan", "free tier", "start free", "no credit card" | Page text, hero action |
| "Get a demo", "contact sales", "talk to us", "book a call" | Primary action text |
| An open-source licence plus an install command, with no payment surface anywhere | Repository, README |
| "Cloud" / "Managed" / "Enterprise" next to a self-host guide | Navigation, README |

Then pick exactly one:

| Model | Recognised by | The conversion job |
|---|---|---|
| **paid** | Visible prices and plans, a purchase or trial action | Make the price legible and the plan choice obvious |
| **free-first** | A free tier is the primary entry; paid tiers exist or are implied | Get the reader to start now; place the upgrade trigger where the limit is felt |
| **open-source** | Install or self-host is the primary path; a managed offer may exist | Reduce install friction, then present the hosted option as the "when you outgrow this" |
| **sales-led** | No public prices; a demo or contact form is the only action | Qualify and route to the demo, and never fabricate a price |

**When the signals are ambiguous or absent, choose free-first.** It is the only model whose pattern — a clear next action on every page — is safe when the money story is unknown, because it never states a price.

Record the classification and the signal it came from, and state it in the summary. A wrong guess must be visible and correctable, not silent.

If the classification is sales-led but the source clearly shows a self-serve signup, prefer free-first: the observable path beats the stated one.

## What does each model's pattern look like?

<!-- widget:accordion -->

### paid — the price must be findable in one click

- A **pricing page** with a plan comparison table (plan, price, who it is for, key limits), built **only** from prices found on the source. A plan whose price was not found says "contact sales" — never a guessed number.
- The hero states the entry price or the free-trial terms in the first screen of text.
- The FAQ answers, in this order: what does it cost, is there a free trial, what happens when I hit a limit, can I cancel, what counts as a seat.
- Every feature page names which plan the feature is on, where the source says so.

### free-first — the action ladder

The action escalates with reader intent.

| Page | The ask |
|---|---|
| Hero, concepts | "Start free — no credit card" |
| Getting started, guides | "Create your first <primary object>" |
| Feature pages | "Try <feature> on the free plan" |
| Use-cases | "Start with the <matching> setup" |

Name the free tier's real limits where the source states them. **A limit is the upgrade trigger** — mention it where the reader would hit it, in the guide that consumes the quota, not only on a pricing page. Generate a pricing page only if the source exposes paid tiers; otherwise fold the money question into the FAQ, answered honestly from the source.

### open-source — friction first, hosted second

- The hero's primary action is the install command; the secondary is the hosted offer, where one exists.
- A self-hosting guide, when the source documents deployment.
- A "self-host vs hosted" comparison — who each is for, what you operate yourself, what is included — built only from what the source states.
- **Never push the paid hosted option inside a tutorial.** The conversion happens on the comparison and in the FAQ.

### sales-led — qualify, then route

- One primary action everywhere, matching the wording the source itself uses.
- Use-cases carry the weight: each job story ends with the demo action framed for that segment.
- The FAQ answers the procurement questions the source supports — security, single sign-on, data residency, onboarding, support commitments. Never invent an answer; omit the question instead.
- **Never state or approximate a price.** "Pricing depends on team size — talk to sales" is the honest answer.

<!-- /widget -->

## Rules that hold for every model

1. **No dead ends.** Every page closes with a next-step or related section containing at least one internal link, and evaluation-stage pages carry one conversion action.
2. **One primary action per page.** Three competing asks convert worse than one clear one. Secondary links go in "Next steps", not as buttons.
3. **Benefit before mechanism.** A feature page headline is the outcome ("Ship docs without a deploy step"), not the component name ("Sync engine").
4. **Objections belong in the FAQ, answered flatly.** No hedging, and no "it depends" without the next sentence saying what it depends on.
5. **Never fabricate a commercial fact.** Prices, plan names, limits, service commitments, customer names, logos and counts come from the source or do not appear. A missing price is "contact sales"; a missing customer story is an omitted section.
6. **No hype adjectives.** Specifics convert; adjectives do not.
7. **The action links somewhere real.** Use a URL found on the source or an internal doc path. Never invent a route that was not observed.
8. **No call to action on reference pages.** A reader deep in a parameter table wants related links, not a pitch. A tutorial converts by working.

## Which pages does this add?

| Page | When | Content |
|---|---|---|
| Pricing | paid always; free-first if paid tiers exist | Plan comparison, what to pick, upgrade and downgrade rules |
| Use-cases | always | Job stories, each ending in the model's action |
| FAQ | always | Objection-killers, ordered by how early they block a purchase |
| Self-hosting | open-source with deployment docs | Install path, then the hosted comparison |

Whether a page should exist at all is a separate decision — see [The page set](../planning/page-set.md).

## Four traps that look solved and are not

These come from a real run against a product whose prices are public, where every rule above was already in place and the documentation still shipped wrong numbers.

**The pricing page is not where the crawler goes.** It is routinely absent from a sitemap index that lists blog, docs and legal — and a breadth-first crawl with a page budget fills up with blog posts before reaching it. Request the pricing and plans paths explicitly instead of hoping to discover them, and read them before anything else.

**Reading the pricing page is not the same as reading its prices.** The per-plan table is usually the *last* thing in the document, behind a volume slider and a feature matrix; the first currency amount on the page is typically an add-on, thousands of characters earlier. If you excerpt or summarise the page, anchor on the last amount, not the first, and confirm you can see every plan's number before writing a table. A page you fetched but whose prices you never saw looks exactly like a page with no prices — and produces a confident "contact sales" for a product that publishes a price.

**"No facts observed" is when invention is most likely, not least.** With nothing to copy, a page brief asking about pricing and limits reads as permission to answer from general knowledge, and what comes out is plausible and wrong — a free tier stated as 1,000 a month when it is 3,000. When no figures were observed the rule is absolute: no price, no quota, no seat count, no trial length. Describe the shape of the offer and link to the pricing page.

**A copied action link is usually a broken one.** A root-relative product path is correct on the product's own site and a 404 in documentation served from another domain. Rewrite those onto the source's origin, and leave internal doc links and anchors alone.

## What to write down

Report the classification and its evidence in this shape, so a wrong guess is correctable by whoever reads it next:

```text
Monetisation model: <paid|free-first|open-source|sales-led> (signal: <what proved it>)
Primary action:     "<text>" → <url or internal path>
Conversion pages:   pricing [or: skipped — no prices on source], use-cases, faq, …
Per-page closings:  <page> → <action>, …
Not stated (no source signal): <prices|limits|commitments|…>
```

An action nobody measured is an assumption. Declaring what a reader was supposed to do, and the ordered route to it, is covered in [Goals and funnels](../auditing/goals-and-funnels.md) — and a renamed anchor or a moved page leaves that measurement pointing at nothing, which looks exactly like readers refusing to convert.

## Related

<!-- widget:cards plain cols=2 -->

- [Writing rules](./writing-rules.md) — the dead-end rule and the one-action rule, in the context of writing any page. {file-text}
- [Goals and funnels](../auditing/goals-and-funnels.md) — measuring whether readers do the thing the page asks. {target}
- [From a finding to a change](./from-finding-to-change.md) — what to do when an audit reports that the documentation supports but does not sell. {wrench}
- [Reading the source](../planning/sources.md) — where the prices and limits on this page have to come from. {plug}

<!-- /widget -->
