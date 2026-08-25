---
title: "Pro, Business, Growth, and Scale Plans Overview"
description: "What Docsbook's paid plans unlock — AI chat and SEO run on every plan; Pro adds your own custom domain, translations, advanced AI chat config, and a larger AI budget; Business adds webhooks, bring-your-own API keys, and semantic search on top, plus higher usage limits. Growth mirrors Pro and Scale mirrors Business, each with a bigger monthly AI budget and more project seats."
---

# Pro, Business, Growth, and Scale Plans

<!-- TODO(docs-sync): src/lib/plan-marketing.ts (the app's single source of truth for
     plan feature lists) now defines only Free/Pro/Business, and the new
     src/utils/paddle/resolvePriceId.ts notes explicitly that "pro_plus/growth/scale
     are not real plans." plan-marketing.ts also dropped the per-plan
     "AI budget equal to plan price" marketing line entirely. This page's title, intro,
     Plan Comparison table, and the "What PRO (and Growth) Add", "Business/Scale-Only
     Features", "Higher Usage Limits on Business and Scale", "Growth and Scale", and
     "Project Seats" sections all still describe a five-plan Growth/Scale ladder and need
     a structural rewrite (headings and a table column removed), not a line edit — left
     for manual review. The "How to Pay" section and closing CTA further down already
     correctly describe only Pro/Business and do not need this rewrite. Separately, every
     $59/$159 figure on this page is also stale: src/utils/constants.ts PRICING now has
     proMonthly=$85 (proYearlyMonthly=$59), businessMonthly=$200 (businessYearlyMonthly=
     $140), and ANNUAL_DISCOUNT_PERCENT is 30, not 20 — verified via git log, PRICING
     landed in 678adea (2026-08-24), predates even the prior docs reconciliation. Fold
     that correction into the same rewrite. -->

Docsbook has five plans. Free is free forever — and it already includes reader-facing AI chat (on a $0.15 monthly AI budget, with your choice of AI model) and full SEO / GEO / AEO. Pro is a monthly subscription that adds your own custom domain, translations, advanced AI chat configuration (custom system prompt, chat hooks), search & feedback analytics, and a much larger AI budget. Business is a separate, higher tier: it includes everything in Pro plus a set of Business-exclusive capabilities — webhooks, bring-your-own API keys (for both AI chat and translations), semantic search, hosted API reference, and UTM analytics — on top of higher usage limits. Growth and Scale sit above Business: each carries every Business capability, with a larger monthly AI budget and more project seats, for teams whose usage has outgrown Business.

A subscription is bought once per **account**, not per project. It grants a number of project **seats**: a project is paid while it holds one, and you can move a seat to a different project at any time. Free projects are unlimited on every plan.

## Plan Comparison

| Feature | Free ($0) | Pro | Growth | Business | Scale |
|---------|------|------|------|------|------|
| Public repositories | Unlimited | Unlimited | Unlimited | Unlimited | Unlimited |
| Paid project seats | 0 | 1 | 5 | 3 | 15 |
| GitHub sync | ✅ | ✅ | ✅ | ✅ | ✅ |
| Branding & themes | ✅ | ✅ | ✅ | ✅ | ✅ |
| Custom domain | ❌ | ✅ | ✅ | ✅ | ✅ |
| AI chat | ✅ $0.15/mo budget | ✅ $59/mo budget | ✅ $349/mo budget | ✅ $159/mo budget | ✅ $899/mo budget |
| AI translations (15 languages) | ❌ | ✅ | ✅ higher limit | ✅ higher limit | ✅ highest limit |
| Full SEO / GEO / AEO (sitemap, OG, JSON-LD) | ✅ | ✅ | ✅ | ✅ | ✅ |
| Analytics period | 24h | 7 days | 30 days | 30 days | 30 days |
| Private docs (password / SSO) | ❌ | ✅ | ✅ | ✅ | ✅ |
| Bring your own AI/translation API key | ❌ | ❌ | ❌ | ✅ | ✅ |
| Webhooks | 0 | 0 | 0 | 25 | 25 |
| Free trial | — | 7 days | — | 14 days | — |

## On Every Plan (including Free)

### AI Chat

A chatbot trained on your documentation runs on **every plan**, Free included. Plans differ by the monthly **AI budget**, not by a feature switch — Free gets $0.15/month, and every paid plan includes an AI budget equal to its price: Pro $59, Business $159, Growth $349, and Scale $899 (the largest of all). Choosing which model runs your chat on Docsbook's key is available on **every plan, including Free** — the model's price comes out of your AI budget. Bringing your own provider and API key (OpenRouter, OpenAI, Gemini, Anthropic), so the provider bills you directly, is a **Business/Scale-only** capability; see [Business/Scale-Only Features](#businessscale-only-features) below.

### SEO / GEO / AEO

Meta tags, sitemap.xml, OpenGraph, Twitter cards, JSON-LD (WebSite, Organization, FAQ), canonical URLs — available on **every plan**, Free included. Each language version is indexed separately.

## What PRO (and Growth) Add

Growth includes everything below that Pro does — same features, larger AI budget, more project seats.

### 1. Automatic Translation

Translate to **15 languages**: English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish, Dutch.

Business and Scale include a higher monthly translation limit than Pro/Growth.

**How to set up:** [Translation Guide](./translation.md)

### 2. Advanced AI Chat Configuration

Custom AI chat system prompt, chat hooks (pre / post / streaming), and the AI chat analysis dashboard.

### 3. Larger AI Budget

Pro raises the monthly AI budget from Free's $0.15 to $59; Business goes to $159, Growth to $349, and Scale to $899 — the largest budget of any plan. Each of those matches what the plan costs. The budget belongs to the account and is shared across every paid project on it.

### 4. Extended Analytics

Free shows the last 24 hours. Pro shows 7 days; Growth, Business, and Scale show 30 days of views, visitors, top pages, referrers, and search queries — plus search & feedback analytics.

### 5. Private Docs

Switch a workspace from public to **private**, then require a password and/or your own SSO/OIDC
identity provider (Google Workspace, Microsoft Entra ID, or Okta) before anyone but the owner can
read it. Optionally restrict SSO sign-in to a single email domain. **How to set up:** [SSO Setup](./sso.md)

### 6. Your Own Domain

Use `docs.yourcompany.com` instead of `docsbook.io/yourname/repo` — a branded URL, better for SEO
(the authority accrues to your domain, not ours), with free SSL. **How to set up:** [Domain Guide](./custom-domain.md)

It was Business-only until 10.08.2026. It's the first thing a site owner wants, so it
now starts at Pro.

## Business/Scale-Only Features

These capabilities are exclusive to the **Business** and **Scale** plans — Pro and Growth do not include them:

- **Webhooks** — subscribe to workspace events (content indexed, translations, chat activity, and more). Free, Pro, and Growth have no webhook slots; Business and Scale get up to 25 per workspace.
- **Bring your own AI/translation API key** — configure your own provider, API key, and model for AI chat and/or translations (separate keys for each), instead of using Docsbook's shared quota.

## Higher Usage Limits on Business and Scale

On top of the Business/Scale-only features above, Business and Scale also raise the numeric limits shared with Pro/Growth:

- AI chat — higher monthly request limit than Pro/Growth (Scale is the highest of all)
- Translations — higher monthly limit than Pro/Growth (Scale is the highest of all)

## Growth and Scale

Growth and Scale sit alongside Pro and Business as separate plans with larger AI budgets and more project seats:

- **Growth** ($349/month) — the same feature set as Pro, with 5 project seats and a $349/month AI budget. For teams that have outgrown Pro's usage limits but don't need the Business-only capabilities.
- **Scale** ($899/month) — the same feature set as Business, with 15 project seats and a $899/month AI budget, the largest of any plan. For teams that have outgrown Business's usage limits.

## Project Seats

Your subscription is bought once per **account** and grants project seats — 1 on Pro, 3 on Business, 5 on Growth, 15 on Scale. A project is paid only while it holds a seat, and you assign or release seats yourself from the Usage tab in workspace settings.

- Free projects are unlimited on every plan — every project carries the "Powered by Docsbook" badge, on every tier.
- Moving a seat to a different project is the normal case, not an exception. A project that just gave up a seat has to wait an hour before taking one again, and seat changes are capped at 10 per month per account.
- Releasing a seat drops that project to Free immediately — its custom domain and private-docs gate stop applying.
- Need more projects than your plan includes? You can buy extra seats, up to twice your plan's allowance.
- If you downgrade or cancel, the oldest seats are kept and the newest are released, so your long-lived production docs stay paid.

## Usage Budget

Every plan's monthly AI budget is a hard ceiling — once it runs out, usage simply pauses until the next cycle. You're never billed above your plan's price.

You can also cap a single spend source. From the Usage tab, set an optional per-cycle ceiling on each of Readers (AI Chat), Admin & AI Agent, AI Translations and Semantic Index — useful when one of them, typically translations or a re-index, could otherwise absorb the whole budget. The limit counts against your plan budget, and the source stops until the next cycle once it is reached; the other sources keep running. Leave a field blank for no limit, or set $0 to switch that source off. Every bar under **Spend by source** shows your limit next to the plan's own budget, so both numbers stay visible.

Usage is priced in money, not tokens: each call is charged at the real price the provider charges for the model that answered, plus a 150% markup. The model, its per-1M-token rate and the markup are all visible in your dashboard, so the amount deducted is one you can check yourself. From Pro you can switch models — a cheaper model makes the same budget go further — and on Business/Scale you can bring your own key and pay the provider directly, in which case we bill you nothing for usage.

## How to Pay

1. Open your workspace in the Float Widget
2. Click **Upgrade**
3. Pick Pro (7-day free trial) or Business (14-day free trial)
4. Paddle checkout opens (overlay)
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

You'll see a **Pro** or **Business** label in the Float Widget. New options open in Settings — translations, advanced AI chat config (custom prompt, hooks), your own custom domain, and a larger AI budget on Pro; webhooks, bring-your-own API keys, and semantic search additionally on Business.

## FAQ

**Q: How long until features activate?**

A: Instantly, as soon as Paddle confirms the payment (or the free trial starts).

**Q: Can I cancel Pro or Business?**

A: Yes, cancel anytime in your billing portal. The workspace downgrades to Free at the end of the billing period.

**Q: Is the paid plan per workspace?**

A: No. The subscription is bought once per account and grants project seats — 1 on Pro, 3 on Business, 5 on Growth, 15 on Scale. Each project you want paid takes one seat, and you can move a seat between projects. Buy extra seats (up to twice your plan's allowance) if you need more.

**Q: What happened to the old lifetime Pro plan?**

A: The one-time lifetime plan is no longer sold. Existing lifetime customers keep their plan and are not affected by this change.

<!-- widget:cta -->

## Pick a plan when you're ready

Pro starts with a 7-day free trial, Business with 14 days — no card charged until the trial ends.

[View pricing](https://docsbook.io/upgrade) · [Set up a custom domain](./custom-domain.md)

<!-- /widget -->

## What's Next

- [How to Set Up a Custom Domain](./custom-domain.md)
- [How to Enable Translations](./translation.md)
- [Managing Documentation](../getting-started/managing-docs.md)
