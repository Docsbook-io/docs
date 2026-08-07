---
title: "Pricing & Plans"
description: "Docsbook pricing — Free forever, Pro, Business, Growth, and Scale — with AI budgets, project seats, translations, and webhook limits broken down per plan. Growth mirrors Pro's capabilities and Scale mirrors Business's, each with a bigger monthly AI budget and more seats; Business/Scale add exclusive capabilities (custom domain, white-label, webhooks, bring-your-own API keys) on top of Pro/Growth."
---

# Pricing & Plans

Docsbook has five plans. A subscription is bought once per **account** and grants a number of project **seats** — a project becomes paid while it holds a seat, and you can move a seat between projects. Free projects are unlimited on every plan.

## Free

- $0 forever
- All basic features: branding, UI settings, navigation, basic analytics
- Reader-facing AI chat ($0.15/month AI budget)
- SEO / GEO / AEO tools — meta tags, sitemap, OpenGraph, JSON-LD
- No translations, no custom domain

## Pro

$59/month, 7-day free trial. Best for solo founders, indie devs, and small teams.

Everything in Free, plus:

- 1 project seat
- Auto-translation
- Advanced AI chat config — chat hooks, custom system prompt, your choice of AI model, chat analysis dashboard
- Search & feedback analytics
- $59/month AI budget
- Private docs — password-protect a workspace, or gate it behind your own SSO/OIDC identity provider
- Webhooks — none (see Business)

## Business

$159/month, 14-day free trial. Everything in Pro, plus a set of Business-exclusive capabilities, and higher usage limits — for teams and heavier usage.

- Everything in Pro
- 3 project seats
- Custom domain (`docs.yourcompany.com`) with free SSL — Business only
- White-label — hide "Powered by Docsbook" — Business only
- Bring your own AI chat and/or translation API key (with custom model) — Business only
- Webhooks — up to 25 per workspace — Business only
- $159/month AI budget, and higher translation limits than Pro

## Growth

$349/month. Includes every Business capability — auto-translation, advanced AI chat config (chat hooks, custom system prompt, your choice of AI model, chat analysis dashboard), search & feedback analytics, private docs (password/SSO), custom domain, white-label, webhooks, bring-your-own API keys, UTM analytics, hosted API reference, and the semantic doc index & relationship graph — plus 5 project seats and a $349/month AI budget. For teams on Pro who mainly need more AI usage headroom rather than the Business-only capabilities.

## Scale

$899/month. Same feature set as Business — custom domain, white-label, bring-your-own AI/translation API key, webhooks (up to 25) — plus 15 project seats and a $899/month AI budget, the largest of any plan. For teams on Business who need substantially more AI usage headroom.

## Limits Summary

| Feature                      | Free     | Pro     | Growth           | Business        | Scale          |
| ---------------------------- | -------- | ------- | ---------------- | ---------------- | -------------- |
| GitHub repositories          | ∞        | ∞       | ∞                | ∞                | ∞              |
| Paid project seats           | 0        | 1       | 5                 | 3                 | 15             |
| AI chat (reader-facing)      | ✅       | ✅      | ✅                | ✅                | ✅             |
| Custom domain                | ❌       | ❌      | ❌                | ✅                | ✅             |
| Private docs (password/SSO)  | ❌       | ✅      | ✅                | ✅                | ✅             |
| SEO / GEO / AEO               | ✅       | ✅      | ✅                | ✅                | ✅             |
| White-label                  | ❌       | ❌      | ❌                | ✅                | ✅             |
| Choose your AI model         | ❌       | ✅      | ✅                | ✅                | ✅             |
| Bring your own API key       | ❌       | ❌      | ❌                | ✅                | ✅             |
| Webhooks                     | 0        | 0       | 0                | 25                | 25             |
| Monthly AI budget             | $0.15    | $59     | $349              | $159              | $899           |
| Payment                       | —        | monthly/annual | monthly/annual | monthly/annual | monthly/annual |
| Overage billing               | ❌       | ✅      | ✅                | ✅                | ✅             |
| Per-source spend limits       | ❌       | ✅      | ✅                | ✅                | ✅             |

Pro/Growth and Business/Scale do **not** unlock the same set of features: custom domain, white-label, webhooks, and bring-your-own API keys are Business/Scale-exclusive. Growth mirrors Pro's feature set with a bigger AI budget and more seats; Scale mirrors Business's feature set with the largest AI budget and the most seats. See [AI Chat](../../ai/chat.md) and [Translations](../../ai/translations.md) for current limit numbers.

The AI budget is per **account** and shared across every paid project on it. If you need more projects than your plan includes, you can buy extra seats — up to twice your plan's seat allowance.

All monthly plans (Pro, Business, Growth, Scale) can also be billed annually at a 20% discount off the monthly price.

## Overage Billing

Paid plans (Pro, Business, Growth, Scale) don't hard-stop the moment your monthly AI budget runs out. Once the budget is exhausted, further usage is billed as overage — charged on top of your subscription — up to a monthly overage cap you control from the Limits tab in workspace settings (default $20/month). Overage charges are billed once your billing cycle closes; if you hit the cap, usage is blocked again until the next cycle (or you raise the cap). Free plan has no overage — usage stops at the free budget.

### Per-Source Limits

The same tab also accepts an optional per-cycle ceiling for each individual spend source — Readers (AI Chat), Admin & AI Agent, AI Translations, Semantic Index. A per-source limit is counted against the plan budget and overage together, so it answers "AI Translations must not cost me more than $3 this month" rather than capping only the overage portion. When a source reaches its limit it stops until the next cycle while the others keep running; a blank field means no limit, and $0 switches that source off entirely. Limits are shown as a marker on the matching bar under **Spend by source**, so the plan's budget and your own ceiling are both visible.

Usage is priced in money, not tokens: every AI call is charged at the real price the provider charges for the model that answered, plus a 150% markup. The model, its per-1M-token rate and the markup are all shown in your dashboard, so the amount deducted is one you can check. From Pro you can switch models — a cheaper model makes the same budget go further. On Business and Scale you can bring your own API key instead, pay the provider directly, and we bill you nothing for usage.

## Upgrade Paths

- **Free → Pro** — monthly subscription, 7-day free trial, instant activation
- **Free → Business** — monthly subscription, 14-day free trial, instant activation
- **Pro → Business** — upgrade anytime for higher limits
- **Pro ↔ Growth** — same feature set, Growth carries a larger AI budget and more seats
- **Business ↔ Scale** — same feature set, Scale carries the largest AI budget and the most seats
- **Pro/Business/Growth/Scale → Free** — cancel anytime via the Customer Portal

## Refund Policy

Full refund within 30 days, no questions asked. Contact [support@docsbook.io](mailto:support@docsbook.io).

## Related

- [Premium Features](../../guides/advanced/premium.md) — what each paid plan unlocks
- [AI Chat](../../ai/chat.md), [Translations](../../ai/translations.md), [Source of Truth](../../ai/source-of-truth.md)
