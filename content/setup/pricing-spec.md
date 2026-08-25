---
title: "Pricing & Plans"
description: "Docsbook pricing — Free forever, Pro, and Business — with AI budgets, project seats, translations, and webhook limits broken down per plan. Pro adds live auto translations and a custom domain; Business adds premium support, unlimited seats, privacy & access control, bring-your-own API keys, and semantic search on top."
---

# Pricing & Plans

Docsbook has three plans. A subscription is bought once per **account** and grants a number of project **seats** — a project becomes paid while it holds a seat, and you can move a seat between projects. Free projects are unlimited on every plan.

## Free

- $0 forever
- All basic features: branding, UI settings, navigation, basic analytics
- Reader-facing AI chat ($0.15/month AI budget), with your choice of AI model
- SEO / GEO / AEO tools — meta tags, sitemap, OpenGraph, JSON-LD
- No translations, no custom domain

## Pro

$85/month ($59/month billed yearly), 14-day free trial. Best for solo founders, indie devs, and small teams.

Everything in Free, plus:

- 1 project seat
- Live auto translations — 15 languages, re-translated automatically on every edit
- Custom domain (`docs.yourcompany.com`) with free SSL
- Advanced AI chat config — chat hooks, custom system prompt, chat analysis dashboard
- Full analytics and chat history (30 days), Google Search rankings, conversions & funnels
- $85/month AI budget
- Webhooks — up to 25 per workspace
- Privacy & access control — see Business

## Business

$200/month ($140/month billed yearly), 14-day free trial. Everything in Pro, plus premium support and a set of Business-exclusive capabilities, for teams and heavier usage.

- Everything in Pro
- Premium support — a person on our team works directly with you to integrate Docsbook into your business
- Unlimited project seats
- Privacy & access control — password-protect a workspace, or gate it behind your own SSO/OIDC identity provider
- Bring your own AI chat and/or translation API key (with custom model)
- Semantic search over your docs, hosted interactive API reference, changes impacts, collaborators
- Webhooks — up to 100 per workspace
- $200/month AI budget

## Limits Summary

| Feature                      | Free     | Pro     | Business |
| ----------------------------- | -------- | ------- | -------- |
| GitHub repositories           | ∞        | ∞       | ∞        |
| Paid project seats            | 0        | 1       | Unlimited |
| AI chat (reader-facing)       | ✅       | ✅      | ✅       |
| Live auto translations        | ❌       | ✅      | ✅       |
| Custom domain                 | ❌       | ✅      | ✅       |
| Privacy & access (password/SSO) | ❌     | ❌      | ✅       |
| SEO / GEO / AEO               | ✅       | ✅      | ✅       |
| Choose your AI model          | ✅       | ✅      | ✅       |
| Bring your own API key        | ❌       | ❌      | ✅       |
| Webhooks                      | 0        | 25      | 100      |
| Monthly AI budget             | $0.15    | $85     | $200     |
| Payment                       | —        | monthly/annual | monthly/annual |
| Per-source spend limits       | ❌       | ✅      | ✅       |

Pro and Business do **not** unlock the same set of features: premium support, unlimited seats, privacy & access, bring-your-own API keys, and semantic search are Business-exclusive. See [AI Chat](../../ai/chat.md) and [Translations](../../ai/translations.md) for current limit numbers.

The AI budget is per **account** and shared across every paid project on it. On Pro, if you need more than one paid project, you can buy extra seats — up to twice your plan's seat allowance.

Both Pro and Business can also be billed annually at a 30% discount off the monthly price.

## Usage Budget

Every plan's monthly AI budget is a hard ceiling: once it's exhausted, AI usage simply pauses until the next billing cycle. You are never billed above your plan's price.

### Per-Source Limits

From the **Usage** tab in workspace settings, you can also set an optional per-cycle ceiling for each individual spend source — Readers (AI Chat), Admin & AI Agent, AI Translations, Semantic Index — counted against the plan budget. It answers "AI Translations must not cost me more than $3 this month." When a source reaches its limit it stops until the next cycle while the others keep running; a blank field means no limit, and $0 switches that source off entirely. Limits are shown as a marker on the matching bar under **Spend by source**, so the plan's budget and your own ceiling are both visible.

Usage is priced in money, not tokens: every AI call is charged at the real price the provider charges for the model that answered, plus a markup. The model, its per-1M-token rate and the markup are all shown in your dashboard, so the amount deducted is one you can check. On every plan, including Free, you can switch models — a cheaper model makes the same budget go further. On Business you can bring your own API key instead, pay the provider directly, and we bill you nothing for usage.

## Upgrade Paths

- **Free → Pro** — monthly subscription, 14-day free trial, instant activation
- **Free → Business** — monthly subscription, 14-day free trial, instant activation
- **Pro → Business** — upgrade anytime for premium support, unlimited seats, and Business-only capabilities
- **Pro/Business → Free** — cancel anytime via the Customer Portal

## Refund Policy

Full refund within 30 days, no questions asked. Contact [support@docsbook.io](mailto:support@docsbook.io).

## Related

- [Premium Features](../../guides/advanced/premium.md) — what each paid plan unlocks
- [AI Chat](../../ai/chat.md), [Translations](../../ai/translations.md), [Source of Truth](../../ai/source-of-truth.md)
