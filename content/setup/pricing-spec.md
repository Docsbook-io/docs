# Pricing Spec

## Plans

### Free
- $0 forever
- All basic features: branding, UI settings, navigation, analytics
- AI queries: 0/mo
- Translations: 0/mo
- No custom domain, no SEO, no AI chatbot

### Pro — $150 lifetime (one-time payment)
- Everything in Free
- AI chatbot: 200 queries/mo
- Translation: 50 translations/mo
- Custom domain
- SEO tools
- One-time payment, lifetime access
- Best for: solo founders, indie devs, projects with predictable usage

### Pro+ — $29/month (subscription)
- Everything in Pro
- AI chatbot: 2000 queries/mo
- Translation: 500 translations/mo
- White-label (hide "Powered by Docsbook")
- Source of Truth: knowledge graph index with deep search
- Best for: teams, agencies, brand-conscious customers, heavy usage

## Limits Summary

| Feature             | Free | Pro          | Pro+         |
| ------------------- | ---- | ------------ | ------------ |
| AI queries/mo       | 0    | 200          | 2000         |
| Translations/mo     | 0    | 50           | 500          |
| Custom domain       | ❌    | ✅            | ✅            |
| SEO                 | ❌    | ✅            | ✅            |
| White-label         | ❌    | ❌            | ✅            |
| Source of Truth     | ❌    | ❌            | ✅            |
| Payment             | —    | $150 one-time| $29/mo       |

## Grandfather Policy
Existing customers who paid the legacy $29 one-time Pro plan retain their Pro tier at no extra cost — their `plan='pro'` workspace is treated as lifetime Pro (matching the new Pro $150 lifetime tier). No action required from them.

Old "Enterprise" customers (`plan='enterprise'`) are migrated to `plan='pro_plus'` keeping all features.

## Failed Payments (Pro+ only)
When a Pro+ subscription payment fails:
1. Webhook `subscription.payment_failed` fires
2. Workspace is downgraded to `plan='free'` (aiEnabled=false, isPremium=false)
3. Email is sent to the workspace owner via Resend with a link to update their payment method via the Paddle Customer Portal

## Upgrade Paths
- Free → Pro: one-time Paddle checkout
- Free → Pro+: subscription Paddle checkout
- Pro → Pro+: subscription Paddle checkout (no proration — they keep their lifetime Pro and add Pro+ on top)
- Pro+ → Free: subscription cancellation via Customer Portal

## Technical Implementation
- Paddle products:
  - Pro: one-time price (`PADDLE_PRICE_ID_PRO`)
  - Pro+: monthly subscription price (`PADDLE_PRICE_ID_PRO_PLUS`)
- Webhook events:
  - `TransactionCompleted` → plan=pro (lifetime)
  - `SubscriptionActivated` → plan=pro_plus
  - `SubscriptionCanceled` → plan=free
  - `SubscriptionPaymentFailed` → plan=free + email
- DB columns added to `workspaces`: `paddle_subscription_id`, `paddle_customer_id`, `subscription_next_billed_at`, `subscription_status`
- Customer Portal URL: configured via `NEXT_PUBLIC_PADDLE_CUSTOMER_PORTAL_URL`
