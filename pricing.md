---
title: "Docsbook pricing: what costs money and what does not"
description: "Docsbook meters four kinds of AI work, plus machine crawling of your published site, against each project's own balance. Hosting, custom domains, human readers, search and GitHub sync are never metered."
---

# Docsbook pricing: what costs money and what does not

Docsbook meters **five** things, charged against the balance of the project that asked for them: four kinds of AI work, and machine crawling of your published site. Publishing the site, serving it to people, full-text search, GitHub sync and recording analytics are not metered — they do not move a balance. This page explains the mechanism; the current figures live on [the Docsbook pricing page](https://docsbook.io/pricing).

## What draws on a project balance

Four kinds of AI work spend a Docsbook project's balance. Each appears as its own row in **Spend by source** on the project's Limits card:

- **Readers (AI Chat)** — an AI answer given to a reader of your published documentation.
- **Admin & AI Agent** — an agent run you or a connected agent started, including metered MCP tool calls.
- **AI Translations** — translating a page into another language.
- **Semantic Index** — building the embeddings the AI chat retrieves from.

Machine crawling is the fifth, and it is the one thing on this page that is not AI work: see [What crawling costs](#what-crawling-costs) below.

Nothing else moves the balance. Hosting the site, a custom domain and its TLS certificate, people browsing, editors writing, GitHub sync, full-text search, branding and analytics are all unmetered, however much of them you use.

You can also cap any one of the four for the current cycle from the Limits card. A source that reaches its cap stops running until the next cycle, and a cap of $0 switches that source off entirely.

## Where to read the current prices

Read prices on [docsbook.io/pricing](https://docsbook.io/pricing), never here. That page is generated from Docsbook's billing constants on every request, so it cannot go stale; a price copied into a documentation page in Git can, and an assistant will keep quoting the stale copy for months after the real number changes. For the same reason this page names no plan price.

The machine-readable version of the same page is at [docsbook.io/pricing.md](https://docsbook.io/pricing.md). It is plain Markdown, so an agent or a crawler can read the prices without rendering HTML.

## What a project balance is

A **project balance** is the money attached to one Docsbook project, spent on the four kinds of AI work listed above. It is filled by your top-ups, and on a Pro project by the AI usage the subscription credits each month. Balances are per project, not per account: one project running out does not stop another, and money you topped one up with is never moved to another or taken back.

## How much free credit a new project gets

Every new project starts on Pro, with no card and **no time limit**, and that trial has an AI wallet of its own. The amount is on [docsbook.io/pricing](https://docsbook.io/pricing) — one figure, generated from the billing constants, so it cannot go stale here.

Three things are worth knowing about that wallet, because they are what make it a trial rather than a balance:

- **It is spent first**, ahead of anything you have topped the project up with. Free money goes before money you paid for.
- **It is what the trial IS.** There is no expiry date to miss: the trial runs until the wallet is empty, however long that takes. Subscribing does not forfeit the rest of it either — it is still spent before the month you paid for.
- **There is no card behind it**, so it cannot overspend. When the wallet is empty the project pauses and nothing is charged to anybody.

That wallet is the only credit Docsbook gives away. Everything after it is either a top-up you pay for or the monthly AI usage a Pro subscription includes.

## What happens when the free credit runs out

Subscribe and the project keeps Pro, with the month's AI usage credited to its balance — less whatever of the trial wallet you actually used, so the sample is not billed to you twice. A trial that never asked the AI anything is credited the full monthly amount.

Spend the wallet out without subscribing and **the project is paused**: it goes private, and the published docs stop being readable until it has a balance again. You are warned on the way there — at half the wallet, at three quarters, and again near the end — so the pause is never the first you hear of it. Nothing is deleted, your Markdown stays in your repository, and topping the project up or subscribing publishes it again exactly as it was.

## A plan on an organization

A plan can also sit on an **organization** rather than on one project. Every project filed into that organization is on the organization's plan, including the ones added afterwards, so a team buys once instead of once per site. A project is always on the best of what it has: its own subscription, its organization's, or its owner's — moving a project into a team can only ever raise what it may do, never lower it.

A new organization starts with **14 days of Pro**, and that is **one trial per account, ever**. Creating a second organization does not hand out a second trial — it is created on Free, and the dialog says so before you click, not after. A project created inside an organization has no separate wallet of its own either; it spends the organization's.

## The two plans, and which balance they fill

Both plans switch on the same things. What differs is **whose balance is topped up**, and it is the only question worth asking when choosing between them:

- **Pro is bought by a person.** It credits you, and covers a project you own.
- **Enterprise is bought for a repository, arranged with our team.** It credits **the project**, and everyone with access to that project spends that one balance — invite whoever you like, none of them needs a plan of their own. Buying it for a second repository means arranging it again, one repository at a time, so each keeps its own balance and a quiet project never pays for a busy one.

Pro's price is on [docsbook.io/pricing](https://docsbook.io/pricing); Enterprise has none published — reach out and we'll work out a number for your repository.

## How top-ups work

You name the amount when you top up a Docsbook project — there is a minimum and a maximum per payment, both on [docsbook.io/pricing](https://docsbook.io/pricing); for more than the maximum, top up twice. The amount lands on the balance of the one project you chose, not on the account.

Top-ups do not expire, and they are separate from the monthly AI usage a Pro subscription credits. If you want a recurring top-up on top of that, set up a monthly payment of your own on the billing screen — it tops the same balance up each month.

## What Docsbook charges for AI usage

Docsbook charges the AI provider's real price for the model that answered, **plus 70%**. The model, its per-1M-token rate and the markup are all shown in your dashboard, so the amount deducted is one you can check against the provider's own price list. Choosing a cheaper model makes the same balance go further.

Bringing your own provider API key is supported. When you do, you pay the provider directly and Docsbook bills you nothing for that usage.

## What MCP tool calls cost

Docsbook MCP tool calls are charged a flat price fixed before the call runs, independent of the size of the answer. Discovery calls — describing the server, finding a skill or a widget, listing your projects, creating one — are never metered. Reads, writes, analytics scans, and full agent runs each sit in their own price class.

The class and price of every tool is on its row in the **MCP** section of your admin panel and in the [MCP tools reference](./mcp/README.md). Every metered call also appears line by line in the project's Feeds panel — which tool, whether it worked, how long it took and what it cost.

## What crawling costs

AI and search crawlers — GPTBot, ClaudeBot, PerplexityBot, Googlebot and the rest — read a published documentation site far more heavily than people do: a bot walks every page, in every language you generate, and comes back to do it again. That is real serving work, and on a site of any size it is the largest thing a project costs to run, so it is metered like the AI work above.

What this means in practice:

- **Every plan includes a monthly crawl allowance**, and it is sized so that an ordinary site being discovered and re-read never reaches it. Being cited by ChatGPT or ranked by Google is the point of publishing; it is not something Docsbook asks you to pay for page by page.
- **Past the allowance, crawls are billed to the project's balance** at a flat rate per thousand pages served to bots.
- **A reader an AI assistant sends you is never a crawl.** ChatGPT-User, Perplexity-User and the rest fetch a page because a person asked for it — they are readers, and readers are unmetered.
- **Your project's Usage view** shows how many pages bots crawled this month, what that cost, and whether any crawls were refused.

When both the allowance and the balance are gone, crawlers are answered with `429 Too Many Requests` until the next month or your next top-up — and **only crawlers**. People reading your documentation, search, and the AI assistant are unaffected; a site never goes dark because a bot walked it too often.

## What happens when a project's balance runs out

When a Docsbook project's balance runs out, a metered call is refused **before it runs**. The refusal names which project ran out, what the call would have cost, what is left, and where to top that project up. Nothing is deleted and the documentation site stays online — readers keep browsing, search keeps working, GitHub sync keeps running.

Free discovery calls keep working too, so an agent connected over MCP can still find out what happened instead of failing silently.

The same applies to crawling: once the crawl allowance and the balance are both spent, bots are turned away and everyone else — readers, search, editors — carries on as before.

## Does anything refill on a schedule?

On a Pro project, yes: each paid month credits that month's AI usage to the project's balance. Nothing refills on a project that is not paying for one — the trial wallet is granted once and expires with the trial, and the free tier is granted nothing.

Top-ups never expire and are never part of a refill: they sit on the balance until you spend them, whatever happens to the plan.

## Can I leave, and what do I keep?

Your Markdown always stays in your own GitHub repository. Docsbook renders those files; it never stores your content in a proprietary format. Point another tool at the same repository and you keep every page, every image and every link — there is nothing to export first.

## Related

- [Docsbook FAQ](./faq.md) — cancellation, payment, data ownership and sync questions
- [Use cases](./use-cases.md) — what teams publish documentation to change
- [MCP tools reference](./mcp/README.md) — every tool, its parameters and its price class
- [AI usage and costs](./analytics/tracking/ai-usage.md) — where spend shows up in your analytics

<!-- widget:cta -->

## See what a project costs you

Create a project, publish it, and watch the balance while you use it. It starts on Pro with an AI wallet of its own and no time limit, and no card is asked for.

[Start free — no credit card](https://docsbook.io/start)

<!-- /widget -->
