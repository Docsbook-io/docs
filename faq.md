---
title: "Docsbook FAQ"
description: "Answers to common questions about Docsbook — GitHub sync, pricing, custom domains, AI chat, translations, private repos, and migrating from other docs tools."
---

# Frequently Asked Questions (FAQ)

## General Questions

**Q: What is Docsbook?**

A: Docsbook transforms your GitHub documentation into a published site in 5 seconds. Connect your GitHub repository and you're done.

---

**Q: Do I need to pay to get started?**

A: No. The Free plan ($0) includes unlimited public repositories, GitHub sync, full design customization, reader-facing AI chat (on a $0.15 monthly AI budget), and full SEO / GEO / AEO. Pro (monthly, 7-day free trial) adds translations, advanced AI chat configuration (custom prompt, hooks), your choice of AI model, search analytics, and a $59/month AI budget. Business (monthly, 14-day free trial) includes everything in Pro plus custom domain, white-label, webhooks, bring-your-own API keys, semantic search, and higher usage limits.

---

**Q: What kind of repository do I need?**

A: Any public GitHub repository with markdown files. This can include:
- README.md
- Project documentation
- Instructions
- API reference
- Any markdown files

---

**Q: Are private GitHub repositories supported?**

A: Currently only public ones. Private repos are planned for the future.

---

**Q: Do I need a GitHub repo to try Docsbook?**

A: No. At [docsbook.io/create](https://docsbook.io/create) you can generate a draft site from a website URL or just a text idea, then browse and customize it as a real docs site before creating an account. The draft is built to sell, not only to explain: pages close with a call to action, and if your source publishes prices you also get a pricing page — built only from the figures found on your own site, never guessed. GitHub is only needed if you want to link an existing repo, or once you're ready to publish (any sign-in method works — GitHub, Google, Apple, or email).

---

**Q: Do I need to configure anything in GitHub?**

A: No. Connect your account via OAuth — Docsbook gets access to your public repos.

---

**Q: What is SEO / GEO / AEO, and why does it matter for docs?**

A: Classic SEO puts your docs in Google. GEO (Generative Engine Optimization) puts them in AI answers — Perplexity citations, ChatGPT Search, Google AI Overviews. AEO (Answer Engine Optimization) adds structured markup so voice assistants and featured snippets can pull directly from your content.

Docsbook generates all three automatically: TL;DR blocks, FAQPage and HowTo JSON-LD, `dateModified`, author markup, and speakable selectors. One toggle in the dashboard — no manual work.

---

**Q: What are Docsbook skills?**

A: Skills are AI-agent instructions (`SKILL.md` files) for documentation tasks: audit structure, write missing sections, check SEO, enable translations, track analytics gaps.

Install them locally with `npx docs-skills install`, or let any MCP-connected agent discover and use them at runtime via `find_skill()`. There are 52 skills across seven categories: analysis, creation, observability, automation, publishing, planning, and growth.

---

**Q: What happens to my docs if Docsbook shuts down?**

A: Nothing is lost. Your Markdown files always live in your own GitHub repository — Docsbook renders them, it never stores your content in a proprietary format. Point another tool at the same repo and you keep everything.

---

## Usage

**Q: How do I update my documentation?**

A: Update the files in GitHub — the site syncs automatically.

1. Edit the `.md` file
2. Commit to GitHub
3. Open the Docsbook site
4. See the updates

---

**Q: How quickly does documentation update?**

A: On your next visit:
1. You visit the site
2. Docsbook checks GitHub for new content
3. Shows the latest version

Typically: instantly.

---

**Q: Why hasn't my site updated?**

A: Check:
1. Is the commit actually in GitHub? (Check on github.com)
2. Did you refresh the browser? (Ctrl+F5)
3. Has 1-2 minutes passed?
4. Is the file extension `.md`?

---

**Q: What folder structure should I use?**

A: Any. We recommend:
```
repo/
├── README.md
├── docs/
│   ├── getting-started.md
│   ├── api/
│   └── guides/
```

But any other structure works too.

---

**Q: Can I use `.markdown` instead of `.md`?**

A: Yes, both extensions work.

---

**Q: Do links between files work?**

A: Yes! Use:
```markdown
[Link](./path/to/file.md)
[Link to folder](../folder/file.md)
```

They are automatically converted to proper URLs.

---

**Q: What about images?**

A: Put them in a folder (e.g., `docs/images/`) and reference them:
```markdown
![Description](./images/screenshot.png)
```

PNG, JPG, GIF, WebP are supported.

---

**Q: Can I use HTML?**

A: Markdown supports HTML, so yes:
```html
<div>Regular HTML</div>
```

But we recommend plain markdown.

---

## Access & Security

**Q: Who can see my documentation?**

A: By default, everyone on the internet — your site is fully public.
- People without a GitHub account
- Search engine bots (Google, Bing)
- Anyone

This is expected for most docs — you want everyone to find and read them.

On Pro and Business, you can switch a workspace to **private** and require a password or SSO
sign-in before anyone but the owner can view it. See [Managing Your Docs](/guides/getting-started/managing-docs) for setup.

---

**Q: How does this relate to a private GitHub repo?**

A: Even if a GitHub repo is private, documentation on Docsbook is open by default.

(Docsbook still reads from the GitHub repo either way — private repos are supported for the
source. If you also want the *published docs site* to require sign-in, use the private-workspace
setting above; that's independent of the GitHub repo's own visibility.)

---

**Q: Is my documentation secure?**

A: Yes, HTTPS (SSL) and Vercel CDN are used.

---

**Q: Can someone edit my documentation through Docsbook?**

A: No, that's not possible. Editing can only be done in GitHub.

---

**Q: Who sees the Float Widget (control buttons)?**

A: Only you, when logged in. Other people see only the documentation.

---

## Paid plans (Pro & Business)

**Q: Is Docsbook a subscription?**

A: Yes. Pro and Business are monthly subscriptions, billed per account via Paddle — one subscription grants project seats, and each project you want paid takes one. Free stays free forever — no card required. You can cancel or downgrade at any time from the Float Widget.

We moved off the old one-time lifetime model because docs are a living product: AI chat, translations, and the MCP server all require ongoing infrastructure (LLM tokens, indexing, hosting). A subscription lets us keep shipping and keep limits high.

---

**Q: What is Pro?**

A: An account subscription — **$59/month**, 7-day free trial, with 1 project seat. Includes:
- AI chat trained on your docs, on a $59/month AI budget
- AI translations to 15 languages
- Full SEO (meta tags, sitemap, OpenGraph, JSON-LD)
- Extended analytics (7 days instead of 24h)
- Advanced MCP tools — chat hooks, custom system prompt, translation management
- Your choice of AI model for reader-facing chat

Custom domain, white-label, webhooks, bring-your-own API keys, and semantic search are **not** included in Pro — see Business below.

---

**Q: What is Business?**

A: An account subscription — **$159/month**, 14-day free trial, with 3 project seats. Everything in Pro, plus a set of Business-exclusive capabilities:
- Custom domain (`docs.yourcompany.com`) with free SSL
- White-label (hide "Powered by Docsbook")
- Webhooks — up to 25 per workspace
- Bring your own AI chat and/or translation API key (with custom model)
- Semantic search — the biggest single improvement to AI chat answer quality (finds the right section by meaning, answers from it with the page cited rather than inventing one, and replies faster). Turn it on in **AI Chat → Semantic Search**; the index re-syncs on every doc commit
- A $159/month AI budget, and higher translation limits than Pro

---

**Q: How much does it cost?**

A: Free $0 forever. Pro $59/month (1 project seat). Business $159/month (3 seats). Growth $349/month (5 seats). Scale $899/month (15 seats). Billed per account, not per project.

---

**Q: What happens if I cancel?**

A: Your subscription stays active until the end of the current billing period — no immediate cutoff.

After it ends, every project that held a seat drops to **Free**:
- The site stays online at `docsbook.io/owner/repo` (forever, unless you move the project to your own GitHub — that changes the address)
- Your custom domain stops resolving (revert DNS or re-upgrade — Business only)
- Translations, white-label, and webhooks turn off; AI chat and SEO keep running on the Free AI budget
- All your content stays in GitHub — nothing is deleted
- Settings (branding, navigation, UI) are preserved — re-upgrading restores everything

There is no lock-in: your docs live in your GitHub repo.

---

**Q: Is there a refund?**

A: Yes. **30-day money-back guarantee** on the first payment, no questions asked. Email [support@docsbook.io](mailto:support@docsbook.io) and we refund within 1–2 business days.

---

**Q: I bought the old PRO lifetime plan. What happens to me?**

A: Grandfathered. The one-time lifetime PRO plan is no longer sold to new customers — Pro and Business are subscription-only today. If you bought PRO as a one-time purchase before we moved to subscriptions, your workspace keeps its original features forever at no extra cost — exactly as promised. No downgrade, no surprise bill.

You can still upgrade your lifetime workspace to Pro ($59/month) or Business ($159/month) if you want the newer capabilities like custom domain, white-label, or webhooks.

---

**Q: How do I migrate from GitBook?**

A: Three steps. Most teams finish in under 30 minutes.

1. **Export from GitBook** — GitBook lets you sync to a Git repo, or export as Markdown / `.zip`. Push the resulting `.md` files to a GitHub repository (any structure works — flat, `docs/` folder, nested, whatever).
2. **Connect to Docsbook** — paste `github.com/your-org/your-repo` on [docsbook.io](https://docsbook.io). Your site goes live in seconds.
3. **Re-point your domain** — in GitBook, remove the custom domain. In Docsbook Business, add `docs.yourcompany.com` and update DNS (one CNAME). SSL is provisioned automatically.

What carries over automatically: page structure, internal links (relative `.md` paths are resolved), images, code blocks (GFM), headings, frontmatter.

What you'll redo: branding (colors, logo, fonts — 5 minutes in the Float Widget), navigation (header links, social links), AI chat suggested questions.

Pricing: GitBook starts at ~$8/user/month and scales fast with team size. Docsbook is **flat $59/month per account** for Pro (translations, larger AI budget, advanced AI chat config — AI chat and SEO are already free), or $159/month for Business (adds custom domain, white-label, webhooks, and 3 project seats instead of 1) — regardless of team size. Most teams save $200+/month switching. See the full comparison: [GitBook vs Docsbook](./blog/docusaurus-vs-docsbook.md).

Stuck? Email [support@docsbook.io](mailto:support@docsbook.io) — we help with migrations for free.

---

**Q: How do I pay?**

A: Click "Upgrade" in the Float Widget → checkout opens via Paddle.

Accepted: Visa, Mastercard, AmEx, Apple Pay, Google Pay.

---

**Q: Is payment secure?**

A: Yes. Payments are processed by Paddle (the Merchant of Record). Docsbook never sees your card number.

---

**Q: Will the price increase?**

A: If prices change, **your existing subscription is locked in**: you keep your current rate for as long as you keep the subscription active. You'll only see a new price if you cancel and re-subscribe later.

---

**Q: Can I buy Pro or Business for multiple workspaces?**

A: Yes, and you don't need a second subscription. One subscription covers your whole account and grants project seats — 1 on Pro, 3 on Business, 5 on Growth, 15 on Scale. Each project you want paid takes a seat, and you can move a seat between projects at any time. If you need more, you can buy extra seats up to twice your plan's allowance.

---

**Q: Are there discounts for organizations?**

A: Contact support@docsbook.io for special arrangements.

---

## Domains

**Q: How do I use my own domain?**

A: Business feature. Guide: [Custom Domain Setup](./guides/advanced/custom-domain.md)

TL;DR:
1. Enter domain in Settings
2. Update DNS (add CNAME)
3. Wait 30 minutes
4. Done.

---

**Q: Which is better: root domain or subdomain?**

A: We recommend a subdomain:
```
✅ docs.example.com (recommended)
✅ example.com (also works)
✅ guide.example.com (multiple can be used)
```

---

**Q: Do I need SSL (HTTPS)?**

A: Docsbook sets it up automatically via Let's Encrypt. Free and no action required on your part.

---

**Q: How long does DNS propagation take?**

A: Usually 15-30 minutes, up to 48 hours maximum.

---

## Translations

**Q: How do I translate documentation?**

A: PRO feature. Guide: [Translations](./guides/advanced/translation.md)

TL;DR:
1. Open Settings
2. Select languages
3. Click Save
4. Docsbook translates in minutes

---

**Q: What languages are supported?**

A: 15 languages: English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish, Dutch.

---

**Q: How good is AI translation?**

A: Good for technical documentation. May need editing for idioms and cultural references.

---

**Q: Will translations update when I update docs?**

A: Yes, automatically.

---

**Q: Can I edit translations?**

A: Yes, you can download and edit manually. Contact support@docsbook.io.

---

## Support & Issues

**Q: How do I contact support?**

A: Email: [support@docsbook.io](mailto:support@docsbook.io)

Pro and Business customers get priority.

---

**Q: Is there Docsbook documentation?**

A: Yes, you're reading it. See the other sections.

---

**Q: What should I do if something is broken?**

A: Write to support@docsbook.io with a description of the issue.

---

**Q: Where can I see updates?**

A: Follow [twitter.com/docsbook](https://twitter.com/docsbook) for product updates and incident reports.

---

## Technical Questions

**Q: What is Docsbook built with?**

A: Next.js 16, React 19, TypeScript, Tailwind CSS 4, Vercel, Neon Postgres, Paddle (billing), GitHub API.

---

**Q: Where is data stored?**

A: On Vercel (servers in the US and other countries) and Neon Postgres.

---

**Q: What markdown parser is used?**

A: Remark + Rehype. GitHub Flavored Markdown (GFM) is supported.

---

**Q: Does site search work?**

A: Yes. Docsbook has built-in full-text search across every page. Click the search icon in the header or press Cmd+K / Ctrl+K to open it.

---

**Q: Is there a dark theme?**

A: Yes. Light, dark and system-follow themes are all supported. Workspace owners pick the default in the branding settings; readers can switch via the theme toggle in the header.

---

**Q: How many concurrent visitors can it handle?**

A: Vercel scales automatically.

---

## Legal

**Q: Is there a Terms of Service?**

A: Yes, see [Terms](https://docsbook.io/terms).

---

**Q: What about a Privacy Policy?**

A: Yes, see [Privacy](https://docsbook.io/privacy).

---

**Q: What if I violate the rules?**

A: We'll reach out to you. Usually we give a chance to fix things.

---

<!-- widget:cta -->

## Don't see an answer to your question?

Write to us and we're happy to help — or just try it and see for yourself.

[Email support](mailto:support@docsbook.io) · [Start free](https://docsbook.io/connect)

<!-- /widget -->

---

**Next:**
- [Quick Start](./quick-start.md)
- [Core Concepts](./basics.md)
- [Creating Documentation](./guides/getting-started/creating-docs.md)
