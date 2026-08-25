---
title: "Pro and Business Plans Overview"
description: "What Docsbook's paid plans unlock — AI chat and SEO run on every plan; Pro adds live auto translations, your own custom domain, and advanced AI chat config; Business adds premium support, privacy & access control, bring-your-own API keys, and semantic search on top, plus unlimited project seats."
---

# Pro and Business Plans

Docsbook has three plans. Free is free forever — and it already includes reader-facing AI chat (on a $0.15 monthly AI budget, with your choice of AI model) and full SEO / GEO / AEO. Pro is a monthly subscription that adds live auto translations, your own custom domain, advanced AI chat configuration (custom system prompt, chat hooks), full analytics and chat history, and a much larger AI budget. Business is the top tier: it includes everything in Pro plus a dedicated person from our team who helps you integrate Docsbook into your business, unlimited project seats, and a set of Business-exclusive capabilities — privacy & access control, bring-your-own API keys, semantic search, hosted API reference, and collaborators.

A subscription is bought once per **account**, not per project. It grants a number of project **seats**: a project is paid while it holds one, and you can move a seat to a different project at any time. Free projects are unlimited on every plan.

## Plan Comparison

| Feature | Free ($0) | Pro ($85/mo) | Business ($200/mo) |
|---------|------|------|------|
| Public repositories | Unlimited | Unlimited | Unlimited |
| Paid project seats | 0 | 1 | Unlimited |
| GitHub sync | ✅ | ✅ | ✅ |
| Branding & themes | ✅ | ✅ | ✅ |
| Live auto translations (15 languages) | ❌ | ✅ | ✅ |
| Custom domain | ❌ | ✅ | ✅ |
| AI chat | ✅ $0.15/mo budget | ✅ $85/mo budget | ✅ $200/mo budget |
| Full SEO / GEO / AEO (sitemap, OG, JSON-LD) | ✅ | ✅ | ✅ |
| Analytics period | 24h | 30 days | 30 days |
| Premium support (direct, personal) | ❌ | ❌ | ✅ |
| Privacy & access (password / SSO) | ❌ | ❌ | ✅ |
| Bring your own AI/translation API key | ❌ | ❌ | ✅ |
| Semantic search over your docs | ❌ | ❌ | ✅ |
| Webhooks | 0 | 25 | 100 |
| Free trial | — | 14 days | 14 days |

## On Every Plan (including Free)

### AI Chat

A chatbot trained on your documentation runs on **every plan**, Free included. Plans differ by the monthly **AI budget**, not by a feature switch — Free gets $0.15/month, Pro $85/month, and Business $200/month. Choosing which model runs your chat on Docsbook's key is available on **every plan, including Free** — the model's price comes out of your AI budget. Bringing your own provider and API key (OpenRouter, OpenAI, Gemini, Anthropic), so the provider bills you directly, is a **Business-only** capability; see [Business-Only Features](#business-only-features) below.

### SEO / GEO / AEO

Meta tags, sitemap.xml, OpenGraph, Twitter cards, JSON-LD (WebSite, Organization, FAQ), canonical URLs — available on **every plan**, Free included. Each language version is indexed separately.

## What Pro Adds

Everything in Free, plus:

### 1. Live Auto Translations

Translate to **15 languages**: English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish, Dutch. Docs are re-translated automatically whenever you edit a page, so no version goes stale.

**How to set up:** [Translation Guide](./translation.md)

### 2. Advanced AI Chat Configuration

Custom AI chat system prompt, chat hooks (pre / post / streaming), and the AI chat analysis dashboard.

### 3. Larger AI Budget

Pro raises the monthly AI budget from Free's $0.15 to $85 — matching what the plan costs. The budget belongs to the account and is shared across every paid project on it.

### 4. Extended Analytics

Free shows the last 24 hours. Pro shows a full 30 days of views, visitors, top pages, referrers, and search queries — plus search & feedback analytics, full chat history, and Google Search rankings.

### 5. Your Own Domain

Use `docs.yourcompany.com` instead of `docsbook.io/yourname/repo` — a branded URL, better for SEO
(the authority accrues to your domain, not ours), with free SSL. **How to set up:** [Domain Guide](./custom-domain.md)

## What Business Adds

Everything in Pro, plus:

### 1. Premium Support

A person on our team works directly with you to integrate Docsbook into your business and get you to the goal you bought it for — not a ticket queue.

### 2. Unlimited Project Seats

Pro is deliberately one paid project; Business removes that limit entirely, for teams running docs across multiple products.

### 3. Privacy & Access Control

Switch a workspace from public to **private**, then require a password and/or your own SSO/OIDC
identity provider (Google Workspace, Microsoft Entra ID, or Okta) before anyone but the owner can
read it. Optionally restrict SSO sign-in to a single email domain. **How to set up:** [SSO Setup](./sso.md)

## Business-Only Features

These capabilities are exclusive to the **Business** plan — Pro does not include them:

- **Premium support** — direct, personal help integrating Docsbook into your business.
- **Unlimited project seats** — Pro is capped at one paid project.
- **Privacy & access control** — password and/or SSO gating.
- **Bring your own AI/translation API key** — configure your own provider, API key, and model for AI chat and/or translations (separate keys for each), instead of using Docsbook's shared quota; we bill you nothing for usage on your own key.
- **Semantic search over your docs** — every section embedded so the AI chat finds the right passage by meaning instead of guessing from keywords.
- **Hosted, interactive API reference** — renders your OpenAPI/Swagger spec on its own page.
- **Changes impacts** — what a docs change did to traffic and answers afterward.
- **Collaborators** — invite your team into one live AI chat session.
- **More webhooks** — up to 100 per workspace, versus 25 on Pro.
- **Done-for-you setup** — migration to Docsbook, full branding setup, AI agents configured for your docs, and Slack & PR integrations set up for you.

## Project Seats

Your subscription is bought once per **account** and grants project seats — 1 on Pro, unlimited on Business. A project is paid only while it holds a seat, and you assign or release seats yourself from the Usage tab in workspace settings.

- Free projects are unlimited on every plan — every project carries the "Powered by Docsbook" badge, on every tier.
- Moving a seat to a different project is the normal case, not an exception. A project that just gave up a seat has to wait an hour before taking one again, and seat changes are capped at 10 per month per account.
- Releasing a seat drops that project to Free immediately — its custom domain and privacy gate stop applying.
- On Pro, need a second paid project? You can buy extra seats, up to twice your plan's allowance.
- If you downgrade or cancel, the oldest seats are kept and the newest are released, so your long-lived production docs stay paid.

## Usage Budget

Every plan's monthly AI budget is a hard ceiling — once it runs out, usage simply pauses until the next cycle. You're never billed above your plan's price.

You can also cap a single spend source. From the Usage tab, set an optional per-cycle ceiling on each of Readers (AI Chat), Admin & AI Agent, AI Translations and Semantic Index — useful when one of them, typically translations or a re-index, could otherwise absorb the whole budget. The limit counts against your plan budget, and the source stops until the next cycle once it is reached; the other sources keep running. Leave a field blank for no limit, or set $0 to switch that source off. Every bar under **Spend by source** shows your limit next to the plan's own budget, so both numbers stay visible.

Usage is priced in money, not tokens: each call is charged at the real price the provider charges for the model that answered, plus a markup. The model, its per-1M-token rate and the markup are all visible in your dashboard, so the amount deducted is one you can check yourself. On every plan you can switch models — a cheaper model makes the same budget go further — and on Business you can bring your own key and pay the provider directly, in which case we bill you nothing for usage.

## How to Pay

1. Open your workspace in the Float Widget
2. Click **Upgrade**
3. Pick Pro or Business — both start with a 14-day free trial
4. Paddle checkout opens (inline, on our own domain)
5. Enter card details, confirm

### Accepted Payment Methods

Visa, Mastercard, American Express, Apple Pay, Google Pay.

### Is Payment Secure?

Yes. Payments are processed by **Paddle** — the Merchant of Record. Docsbook never sees your card number. Paddle handles SSL, PCI DSS, EU VAT, and US sales tax.

### Refunds

Full refund within the first 30 days. Email support@docsbook.io.

## After Payment

1. **Payment processed** ✅
2. **Account gets its seats, and the project you checked out with takes one** ✅
3. **All features available immediately** ✅

You'll see a **Pro** or **Business** label in the Float Widget. New options open in Settings — translations, advanced AI chat config (custom prompt, hooks), your own custom domain, and a larger AI budget on Pro; premium support, privacy & access control, bring-your-own API keys, and semantic search additionally on Business.

## FAQ

**Q: How long until features activate?**

A: Instantly, as soon as Paddle confirms the payment (or the free trial starts).

**Q: Can I cancel Pro or Business?**

A: Yes, cancel anytime in your billing portal. The workspace downgrades to Free at the end of the billing period.

**Q: Is the paid plan per workspace?**

A: No. The subscription is bought once per account and grants project seats — 1 on Pro, unlimited on Business. Each project you want paid takes one seat, and you can move a seat between projects. On Pro, buy extra seats (up to twice your plan's allowance) if you need more than one.

**Q: What happened to the old lifetime Pro plan?**

A: The one-time lifetime plan is no longer sold. Existing lifetime customers keep their plan and are not affected by this change.

<!-- widget:cta -->

## Pick a plan when you're ready

Both Pro and Business start with a 14-day free trial — no card charged until the trial ends.

[View pricing](https://docsbook.io/upgrade) · [Set up a custom domain](./custom-domain.md)

<!-- /widget -->

## What's Next

- [How to Set Up a Custom Domain](./custom-domain.md)
- [How to Enable Translations](./translation.md)
- [Managing Documentation](../getting-started/managing-docs.md)
