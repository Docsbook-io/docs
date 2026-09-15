---
title: "Know the reader before you write the page: the product audit"
description: "Who enters, how they enter, who they compare you to, and how the product makes money — the four answers that decide what a documentation set contains."
tldr: "Documentation that reads like a file dump was written before anyone asked who it is for. Establish the segments, entry paths, competitors, monetisation model, call-to-action destination and brand signals first — each with its evidence tier, each absence recorded."
---

# Know the reader before you write the page

Documentation that reads like a file dump is almost always documentation written before anyone asked who it is for. This stage answers four questions, and every one of them changes the output: **who enters, how they enter, who they compare you to, and how the product makes money.**

It is a reading stage. It reports; it does not rewrite the product. The only files it may write are the plan and additive, marked blocks inside a private product source-of-truth.

It is also the stage where you find out what the product currently *claims*, which is not always what it does. That matters beyond the documentation: assistants mostly paraphrase a product's own site, including the parts that have gone stale. In one live audit across Perplexity, GPT and Gemini with web search, the product's site was found in 9 of 9 answers and those answers repeated "the API is coming soon" in 5 of 9 — while the API was live with 96 operations, and a price sat on the landing page (Docsbook, GEO audit of a live product, 3 September 2026). A sentence nobody has updated is a sentence being read aloud to buyers.

## In what order do you trust what you find?

Reason in this order, and never present a lower tier as a higher one:

1. **Existing analysis reports.** If a previous run left findings on disk, reuse them rather than re-deriving them.
2. **The source itself** — the site, the repository, the documentation being migrated. This is the strongest ground for claims about the product.
3. **Real analytics**, when a workspace with history is connected. This is the only tier that can tell you which entry path people actually use; see [analytics](../../analytics/README.md).
4. **Reasoned simulation**, only where no data can exist yet — a channel that launched last week, a competitor's unshipped roadmap.

Label every simulated claim as simulated, in the finding and in any prose that comes out of it. A reader has to be able to tell a measured claim from a reasoned guess. When in doubt, label it simulated and lower the confidence.

## Who are the buyers, actually?

For each segment the source addresses, write down:

- **The job to be done**, in the reader's words rather than the product's.
- **Where they already are** — the forums, communities and search phrasings they use. This is what the top-of-funnel pages have to match.
- **The buying trigger** — the event that turns a browser into an evaluator.
- **The entry path they actually use**, which is often not the one the marketing site assumes.

Two or three real segments beat five invented ones. A persona the source does not address is a fabrication. [Jobs to be done](../lenses/jobs-to-be-done.md) is the full reading behind this list, and [user language](../lenses/user-language.md) is how you get the wording right rather than approximating it.

## Every way in, and how good each one is

List every path a reader can arrive by — organic search, a repository README, a package registry, a shared link, an agent or MCP client, a documentation link from inside the app, a comparison article. For each one, record:

- The actual sequence of steps from first touch to first value.
- The friction in it: a term that appears nowhere on the landing page, a step that assumes a tool the reader does not have.
- A coverage score, 0–100%, for how well the documentation supports that path today.
- What would measure it, so a later audit can pick it up — see [did it work](../auditing/did-it-work.md).

If the product declares an entry funnel or a positioning rule anywhere in its own knowledge base, **read it first and treat it as a hard constraint.** No page you propose may contradict it.

## What does the product let people finish?

A segment list says who arrives. It does not say what the product lets them finish, and a plan built only on segments produces a page per feature — which is exactly how generated documentation ends up as a file dump with better headings.

Before deciding the structure, walk the chain once: **capability → job → user → workflow → outcome.** Translate every feature into the action it performs ("webhook" becomes "start a process the moment something happens"), then ask which jobs that action finishes, for whom, and what the result is worth. Combinations matter more than individual capabilities: *API plus filtering plus export* is six different use cases for six different audiences, and each of them types something different into a search box.

This is what the mandatory use-case page and the FAQ get written from, and it is what stops a plan from covering only technical intent while nobody who is merely problem-aware ever finds the product. [Demand gaps](../auditing/demand-gaps.md) is the full method — the job classes, the audience axes, the coverage matrix and the scoring. Reach for it when the plan needs more than two or three use-case pages, or when the product's capabilities clearly serve audiences the source never addresses. Its one hard rule applies with full force here: **a capability the source did not show does not exist**, and no page may be planned for it.

## Who is the product measured against?

- Who the source itself names, and who the segments actually compare it against. These differ more often than not.
- What changed recently: pricing, a feature that closed a gap, a new entrant.
- The counter-arguments a reader arrives with.

Every price, feature and limit must trace to a cited source or be written as an open question. Never a fabricated number. **A competitor comparison built on stale facts is worse than none** — it is the page a prospect forwards to the competitor. [Competitors](../lenses/competitors.md) covers how to keep those facts fresh, and [`crawl_competitor_docs`](../../mcp/research/crawl-competitor-docs.md) reads a rival's documentation without you doing it by hand.

## What does the monetisation model require the site to do?

Classify from real signals — a pricing page, the repository licence, the product description — and then let the classification decide the shape of the site.

| Model | What the documentation must carry |
|---|---|
| Open source, no paid tier | A contribution path, an install matrix, no call-to-action ladder |
| Free tool with a paid upgrade | The limits of free stated clearly, one honest upgrade page, an upgrade action at the moment the limit is felt |
| Self-serve SaaS | A pricing page, a plan comparison, an activation path per plan, an action on every leaf page |
| Sales-led | Use-case and proof pages, "book a demo" as the terminal action, no invented pricing |

Guessing here is expensive in both directions: a call-to-action ladder on an open-source project reads as spam, and a missing one on self-serve SaaS leaves money on the table. If the signals conflict, ask. [Conversion](../writing/conversion.md) turns the classification into the actual pattern on the page.

## Where does the call to action point?

If the project declares a single destination its documentation exists to drive readers to, that destination beats anything you would infer from the source, and it belongs in the site header as a filled button.

Read it **before the first page is written**. Every hero and every "Next steps" block depends on it, so discovering it after generation means rewriting every page.

## Brand signals

Collect these with their source. Record a missing one as missing — never as a guess.

| Signal | Where it comes from |
|---|---|
| Accent or theme colour | `<meta name="theme-color">`, CSS custom properties on `:root` (`--accent`, `--primary`, `--color-primary`), or the dominant non-neutral hue of the logo |
| Colour scheme | Background luminance; a theme-toggle element means prefer following the system setting over pinning a scheme |
| Logo versus icon | **Different fields.** The logo is the horizontal wordmark in the header; the icon is the square favicon. A favicon in the logo field hides the product name. If there is only a favicon and no wordmark, leave the logo empty and rely on the name plus the icon. |
| Font | Only when the site's CSS explicitly names a web font |
| Social links | GitHub, X, Discord, LinkedIn, YouTube, Slack — usually in the footer markup, not the header |

Never invent a colour. Palette derivation, contrast checking and how these get applied to a live site belong to [presentation](../writing/presentation.md); this stage only collects.

## What to ask when the source cannot answer

Ask only what the source did not already tell you. One question at a time, reacting to each answer before the next, reflecting back what you heard after each block.

- **Product** — name, one-liner, source of truth, maturity: pre-launch, early, growing or scaled.
- **Goals** — onboarding, support deflection, search traffic, AI citability, sales enablement, education, developer reference, trust and compliance. Take a one-line success measure for each chosen goal, and surface the goals they did not volunteer.
- **Audience** — propose two or three roles from what you read rather than asking cold, then confirm each one's entry point, current knowledge, job to be done, and what success looks like.
- **Funnels** — for each confirmed role, a three-to-five step path from entry to success. Where a top-of-funnel goal is chosen, the awareness pages are about the problem space, not about the product.

**The last two are not report prose — they are the definitions the site gets measured by.** The goals and the funnel written here are declared against the live site at publish time ([goals and funnels](../auditing/goals-and-funnels.md), and the reports they feed in [analytics](../../analytics/reports/goals-and-funnels.md)). Write them so that step is possible: a goal is one thing a reader does that something observable can match — a section they reach, an action they take in the page, a destination they leave for — and a funnel is those goals in the order they happen, starting broad and ending on the thing that changes revenue. A goal phrased as an internal aspiration ("build trust") cannot be declared, and a funnel that starts at the index page describes a reader almost nobody is.

Cap the first plan at five to seven must-ship pages. No team ships more than that, and a plan nobody finishes is a plan nobody trusts.

## What the audit produces

A plan document, in this shape:

```markdown
# Documentation plan — <product>

## Product
<one-liner, maturity, source-of-truth links, monetisation model>

## Goals
- <goal> — <one-line success measure>

## Segments & funnels
### <Segment>
- Entry: …
- Funnel: Awareness → Evaluation → Activation → Retention
- Friction: …
- Pages needed:
  - <slug> — <purpose> — <goal it serves>

## Competitors
| Name | How we are compared | Fact | Source / open question |

## Information architecture
<top-level nav, one bullet per section, with the segment it serves>

## Content backlog (prioritised)
| # | Page | Type | Segment | Goal | Priority | Effort |
Priority: P0 ship first, P1 next, P2 nice to have. Effort: S / M / L.

## Brand signals
| Signal | Value | Source | or: absent |
```

Then say the short version out loud: the top three must-ship pages and the next step. Five lines, not the document.

## Writing back into a private source-of-truth

When the product keeps its own knowledge base — a README plus a specs tree, a product-marketing file, any Markdown base — this stage may append what it learned, so the next run starts from richer ground.

- **Fill explicit blanks first.** A placeholder line marked as empty is replaced with content under it; that is the cleanest case.
- **Append, never overwrite.** Sections holding human prose get a new marked subsection beneath them. Existing lines are not edited.
- **Mark every generated block** so a human can audit it, trust it or delete it:

  ```markdown
  <!-- BEGIN docsbook:product-audit · <lens> · <ISO-date> · evidence:<measured|mixed|simulated> -->
  … generated content …
  <!-- END docsbook:product-audit -->
  ```

- **A re-run replaces its own previous block**, matched by the marker, rather than stacking duplicates. Human prose between markers is never touched.
- Never write outside the source-of-truth directory, and never touch product code or published documentation from this stage.

## How you know the audit is done

- Segments, entry paths and competitors each recorded with an evidence tier, and every simulated claim labelled as simulated.
- A stated entry funnel or positioning rule, where one exists, was read first and is contradicted by nothing in the plan.
- The capability → job → user chain was walked at least once, and every planned use-case page traces to a capability the source actually showed.
- The monetisation model was classified from real signals, and the shape of the site follows from it.
- The call-to-action destination was resolved before generation started.
- Brand signals recorded with their sources, and absences recorded as absences.
- Every number, price and competitor fact traces to a source or is written as an open question.
- Writes into a private source-of-truth are additive, marked, and a re-run replaced its own block.

## Related

- [Routing the input](./route-the-input.md) — the stage before this one, and the pipeline it belongs to.
- [Deciding the page set](./page-set.md) — what this audit's answers turn into.
- [Jobs to be done](../lenses/jobs-to-be-done.md) and [demand gaps](../auditing/demand-gaps.md) — the deeper readings behind segments and capabilities.
- [Conversion](../writing/conversion.md) — the on-page pattern the monetisation model selects.
- [Goals and funnels](../auditing/goals-and-funnels.md) — where the goals written here get declared and measured.
