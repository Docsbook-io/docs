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

A: No. The Free plan ($0) includes unlimited public repositories, GitHub sync, and full design customization. PRO ($150 lifetime) adds a custom domain, AI chat, translations, SEO, and more. PRO+ ($59/month) adds white-label, higher AI/translation limits, and Source of Truth.

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

**Q: Do I need to configure anything in GitHub?**

A: No. Connect your account via OAuth — Docsbook gets access to your public repos.

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

A: Everyone on the internet. Your site is fully public.
- People without a GitHub account
- Search engine bots (Google, Bing)
- Anyone

This is expected — you want everyone to see your documentation.

---

**Q: How does this relate to a private GitHub repo?**

A: Even if a GitHub repo is private, documentation on Docsbook is open.

(Private repos are not yet supported.)

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

## Paid plans (PRO & PRO+)

**Q: What is PRO?**

A: A one-time lifetime purchase ($150) per workspace with:
- Custom domain
- AI chat (200 requests/month)
- AI translations (50/month, 15 languages)
- SEO (meta tags, sitemap, OpenGraph, JSON-LD)
- Extended analytics (7/14/30 days)

**Q: What is PRO+?**

A: A monthly subscription ($59/month) per workspace. Includes everything in PRO, plus:
- White-label (hide "Powered by Docsbook")
- Higher AI limits (2000 requests/month)
- Higher translation limits (500/month)
- Source of Truth (doc graph for AI agents)

---

**Q: How much does it cost?**

A: Free $0 forever. PRO $150 one-time (lifetime). PRO+ $59/month.

---

**Q: How do I pay?**

A: Click "Upgrade" in the Float Widget → checkout opens via Paddle.

Accepted: Visa, Mastercard, AmEx, Apple Pay, Google Pay.

---

**Q: Is payment secure?**

A: Yes. Payments are processed by Paddle (the Merchant of Record). Docsbook never sees your card number.

---

**Q: Is there a refund?**

A: Yes, full refund within the first 30 days. Contact support@docsbook.io.

---

**Q: Will the price increase?**

A: PRO is $150 lifetime — once you buy it, the price for your workspace never changes.

---

**Q: Can I buy PRO for multiple workspaces?**

A: Yes — billing is per workspace. Each workspace is upgraded separately.

---

**Q: Are there discounts for organizations?**

A: Contact support@docsbook.io for special arrangements.

---

## Domains

**Q: How do I use my own domain?**

A: PRO feature. Guide: [Custom Domain Setup](./guides/advanced/custom-domain.md)

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

PRO and PRO+ customers get priority.

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

## Don't see an answer to your question?

Write to [support@docsbook.io](mailto:support@docsbook.io) — we're happy to help.

---

**Next:**
- [Quick Start](./quick-start.md)
- [Core Concepts](./basics.md)
- [Creating Documentation](./guides/getting-started/creating-docs.md)
