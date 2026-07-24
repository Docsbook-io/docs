---
title: "Pro and Business Plans Overview"
description: "What Docsbook Pro and Business unlock — AI chat and SEO run on every plan; Pro adds translations, advanced AI chat config, and a larger token budget; Business adds custom domain, white-label, webhooks, and bring-your-own API keys on top, plus higher usage limits."
---

# Pro and Business Plans

Docsbook has three plans. Free is free forever — and it already includes reader-facing AI chat (on a smaller monthly token budget) and full SEO / GEO / AEO. Pro is a monthly subscription that adds translations, advanced AI chat configuration (custom system prompt, chat hooks, MCP Source of Truth), search & feedback analytics, and a much larger AI token budget. Business is a separate, higher tier: it includes everything in Pro plus a set of Business-exclusive capabilities — custom domain, white-label, webhooks, and bring-your-own API keys (for both AI chat and translations) — on top of higher usage limits.

## Plan Comparison

| Feature | Free ($0) | Pro | Business |
|---------|------|------|------|
| Public repositories | Unlimited | Unlimited | Unlimited |
| GitHub sync | ✅ | ✅ | ✅ |
| Branding & themes | ✅ | ✅ | ✅ |
| Custom domain | ❌ | ❌ | ✅ |
| AI chat | ✅ smaller token budget | ✅ | ✅ higher limit |
| AI translations (15 languages) | ❌ | ✅ | ✅ higher limit |
| Full SEO / GEO / AEO (sitemap, OG, JSON-LD) | ✅ | ✅ | ✅ |
| Analytics period | 24h | 30 days | 30 days |
| Private docs (password / SSO) | ❌ | ✅ | ✅ |
| Hide "Powered by Docsbook" | ❌ | ❌ | ✅ |
| Bring your own AI/translation API key | ❌ | ❌ | ✅ |
| Webhooks | 0 | 0 | 25 |
| Free trial | — | 7 days | 14 days |

## On Every Plan (including Free)

### AI Chat

A chatbot trained on your documentation runs on **every plan**, Free included. Plans differ by the monthly **AI token budget**, not by a feature switch — Free gets a smaller budget, Pro and Business progressively larger ones. Business includes a higher budget than Pro. Bringing your own provider and API key (OpenRouter, OpenAI, Gemini, Anthropic) — with a custom model of your choice — is a **Business-only** capability; see [Business-Only Features](#business-only-features) below.

### SEO / GEO / AEO

Meta tags, sitemap.xml, OpenGraph, Twitter cards, JSON-LD (WebSite, Organization, FAQ), canonical URLs — available on **every plan**, Free included. Each language version is indexed separately.

## What PRO Adds

### 1. Automatic Translation

Translate to **15 languages**: English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish, Dutch.

Business includes a higher monthly translation limit than Pro.

**How to set up:** [Translation Guide](./translation.md)

### 2. Advanced AI Chat Configuration

Custom AI chat system prompt, chat hooks (pre / post / streaming), the MCP Source of Truth indexing graph, and the AI chat analysis dashboard.

### 3. Larger AI Token Budget

Pro raises the monthly AI token budget well above the Free allowance; Business raises it further.

### 4. Extended Analytics

Free shows the last 24 hours. Pro and Business show 7 / 14 / 30 days of views, visitors, top pages, referrers, and search queries — plus search & feedback analytics.

### 5. Private Docs

Switch a workspace from public to **private**, then require a password and/or your own SSO/OIDC
identity provider (Google Workspace, Microsoft Entra ID, or Okta) before anyone but the owner can
read it. Optionally restrict SSO sign-in to a single email domain. **How to set up:** [SSO Setup](./sso.md)

## Business-Only Features

These capabilities are exclusive to the **Business** plan — Pro/Pro+ does not include them:

- **Custom domain** — use `docs.yourcompany.com` instead of `docsbook.io/yourname/repo`. Branded URL, better for SEO, free SSL via Vercel. **How to set up:** [Domain Guide](./custom-domain.md)
- **White-label** — hide the "Powered by Docsbook" badge across all pages.
- **Webhooks** — subscribe to workspace events (content indexed, translations, chat activity, and more). Free and Pro have no webhook slots; Business gets up to 25 per workspace.
- **Bring your own AI/translation API key** — configure your own provider, API key, and model for AI chat and/or translations (separate keys for each), instead of using Docsbook's shared quota.

## Higher Usage Limits on Business

On top of the Business-only features above, Business also raises the numeric limits shared with Pro:

- AI chat — higher monthly request limit than Pro
- Translations — higher monthly limit than Pro

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
2. **Workspace plan upgrades** ✅ (Free → PRO or PRO+)
3. **All features available immediately** ✅

You'll see a **Pro** or **Business** label in the Float Widget. New options open in Settings — translations, advanced AI chat config (custom prompt, hooks, Source of Truth), and a larger token budget on Pro; custom domain, white-label, webhooks, and bring-your-own API keys additionally on Business.

## FAQ

**Q: How long until features activate?**

A: Instantly, as soon as Paddle confirms the payment (or the free trial starts).

**Q: Can I cancel Pro or Business?**

A: Yes, cancel anytime in your billing portal. The workspace downgrades to Free at the end of the billing period.

**Q: Is the paid plan per workspace?**

A: Yes. Billing is per workspace, so each workspace is upgraded separately.

**Q: What happened to the old lifetime Pro plan?**

A: The one-time lifetime plan is no longer sold. Existing lifetime customers keep their plan and are not affected by this change.

## What's Next

- [How to Set Up a Custom Domain](./custom-domain.md)
- [How to Enable Translations](./translation.md)
- [Managing Documentation](../getting-started/managing-docs.md)
