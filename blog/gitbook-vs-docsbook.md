---
title: "GitBook vs Docsbook: pricing, lock-in and migration"
description: "GitBook and Docsbook compared on how each one charges, where your content actually lives, what AI you get, and what the migration between them costs."
---

# GitBook vs Docsbook: pricing, lock-in and migration

GitBook is the documentation platform of choice for Zoom, FedEx, Nvidia, and a long tail of mid-market and enterprise teams. It looks polished, has a comfortable WYSIWYG editor, and the AI Search feature actually works.

So why do teams go looking for a GitBook alternative?

Because two years into a GitBook contract most teams notice the same three things: the bill scales with every new editor on the team, content lives inside GitBook's database rather than in their repo, and the platform that promised to handle their docs forever now has to be migrated away from.

This post is the honest comparison. We make Docsbook, so we'll tell you when it wins. But GitBook is a real product with real strengths, and there are teams it fits better than us. We'll tell you which.

## TL;DR — Decision matrix

| | **GitBook** | **Docsbook** |
|---|---|---|
| **Best for** | Mid-market and enterprise teams with budget and dedicated docs owners | Indie hackers, startups, OSS, and teams whose source of truth is GitHub |
| **Setup** | Hours to a day | 5 seconds |
| **Pricing model** | Per site per month, plus a fee per collaborating user | Pay-as-you-go balance per project, spent on AI usage |
| **Where the current price lives** | [gitbook.com/pricing](https://www.gitbook.com/pricing) | [docsbook.io/pricing](https://docsbook.io/pricing), generated live on every request |
| **Source of truth** | GitBook's database (Git Sync is an add-on) | Your GitHub repo, period |
| **AI chat** | Built-in (AI Search) | Built-in, metered against the project balance |
| **Multi-language** | Add-on, limited | 15 languages, each indexed separately for SEO |
| **MCP server** | None | Yes, OAuth 2.0, used by Claude Code and Cursor |
| **llms.txt** | Not built-in | Auto-generated platform-wide and per workspace |
| **Vendor lock-in** | High — content in their DB | None — your repo stays canonical |
| **Custom domain** | Paid | Supported, with automatic SSL |
| **Footer credit** | Removable on the top tier | A "Powered by Docsbook" link in the footer, on every site |

If you only read one row: GitBook is priced and built for a team that has a docs owner and a budget line. Docsbook is priced and built for a team where the docs live in `docs/` next to the code and nobody wants to own a separate docs system.

## Why teams leave GitBook

Four reasons show up in every churn conversation we have with new Docsbook customers migrating off GitBook.

### 1. The bill grows with the number of people who edit

GitBook's price has two axes. Read from its own pricing page on 2026-09-03, [gitbook.com/pricing](https://www.gitbook.com/pricing) lists Free at $0 per site/month with one user, Premium at $65 per site/month plus $12 per user/month, Ultimate at $249 per site/month plus $12 per user/month, and Enterprise on request. Readers cost nothing — the per-user fee applies to people who collaborate on content inside the GitBook app.

That shape has a consequence worth naming plainly: every additional colleague who might fix a typo adds a recurring line to the bill. It is a coherent model — it funds the WYSIWYG editor, the change-request flow and the sales team — but it prices the thing most product teams want more of, which is more engineers touching the docs.

Docsbook does not charge per editor and does not sell tiers. Each project carries its own balance, and the balance is spent on AI usage; publishing the site, hosting it, serving a custom domain and every page a reader opens draw nothing from it. Anyone on your GitHub team can edit the underlying Markdown, because the editor is the one they already use. Current numbers are on [docsbook.io/pricing](https://docsbook.io/pricing).

### 2. Vendor lock-in is real

GitBook's Git Sync is an add-on, and even with it enabled, the canonical source is GitBook's database. If you stop paying, your content does not stay where you can keep working on it.

We have seen this play out the same way three times: a team decides to leave, exports their content, and discovers that the export is a ZIP of Markdown files that doesn't match the structure of their repo, with image links pointing at GitBook's CDN. Migration is not a button. It is a project.

Docsbook is the inverse model. Your Markdown sits in your GitHub repo. We index it, render it, and ship it. If you stop paying, the docs are still right there in `docs/` — what you lose is the hosted site, the AI chat, and the translations. The asset stays yours because it never moved.

### 3. The migration off Docusaurus or off Markdown is half the cost

If your docs are currently in a `docs/` folder of Markdown files (which is where most engineering teams keep them), getting onto GitBook means either pasting them into GitBook's editor or wiring up Git Sync and hoping the import handles your front matter, custom components, and image paths.

Most teams underestimate this. GitBook's editor is a block-based editor, not a Markdown editor — so MDX components, callouts written as `:::note`, and tables that work fine in Markdown either render slightly wrong or need to be redone.

Docsbook reads your Markdown as-is. If `README.md` and a `docs/` folder work on GitHub, they work on Docsbook in 5 seconds. Frontmatter, GFM tables, code fences, image links — all rendered without any reformatting.

### 4. AI search is a checkbox, not a moat anymore

In 2024, AI Search was the reason to pay GitBook. In 2026 every serious documentation platform has it. The question is no longer "do you have AI" — it is "how much does AI cost on top of the editor seat I'm already paying for, and where does my AI traffic come from."

Docsbook meters AI in dollars against the project's balance rather than gating it behind a tier, so the question "which plan has AI" does not arise. The MCP server is included, which means Claude Code and Cursor users read and edit your docs directly, and `llms.txt` and `llms-full.txt` are published automatically at the platform level and per workspace.

That last part matters more than it looks. Mintlify measured 30 days of traffic across the documentation sites it hosts — roughly 790 million requests — and reported that AI coding agents accounted for **45.3% of all requests**, with Claude Code at 25.2% and Cursor at 18.0% ([The state of agent traffic in documentation](https://www.mintlify.com/blog/state-of-ai), published 3 April 2026). Its follow-up measurement put the agent share at **66% of traffic in July 2026** ([The state of docs traffic: a 2026 midyear report](https://www.mintlify.com/blog/state-of-docs-traffic), published 29 July 2026). That is one vendor's fleet, not the whole web — but it is the largest published measurement of agent traffic to documentation, and the direction is not subtle.

## Side-by-side feature comparison

| Feature | GitBook | Docsbook |
|---|---|---|
| Setup time | Hours to a day | 5 seconds |
| Free entry | $0 per site/month, one user (gitbook.com/pricing, read 2026-09-03) | Publishing a site costs nothing; AI usage is metered against a balance |
| Source of truth | GitBook DB (Git Sync optional) | GitHub repo |
| Editor | WYSIWYG block editor | Markdown in your repo |
| AI chat | AI Search, varies by plan | Included, metered in dollars against the project balance |
| AI translations | No | 15 languages, separate SEO indexing |
| MCP server | No | Yes — workspace, branding, analytics, search and content-graph tools |
| llms.txt | No | Yes, platform and workspace |
| Source-of-truth content graph for AI agents | No | Yes |
| Custom domain | Paid | Supported, with automatic SSL |
| Custom branding | Paid | Colours, fonts, logo, light and dark |
| Footer credit | Removable on the top tier | Not removable — every site carries a "Powered by Docsbook" footer link |
| Multi-language | Add-on, limited | 15 languages built in |
| Analytics | Built-in, basic | Built-in, with the full event stream |
| Webhooks | Limited | HMAC-signed events for content, traffic, search and chat |
| Pricing model | Per site plus per collaborating user | Pay-as-you-go balance per project |
| Vendor lock-in | High | None |

## How do the two pricing models actually compare?

They cannot be compared as two numbers, because they meter different things — and that difference is the whole decision.

| | GitBook | Docsbook |
|---|---|---|
| What you pay for | A site, plus every person who edits it | AI usage, against a balance held per project |
| What grows the bill | Hiring someone who might fix a typo | Asking the assistant more questions |
| What costs nothing | Readers | The site, its hosting, its domain, and every page view |
| Where the current number lives | [gitbook.com/pricing](https://www.gitbook.com/pricing) | [docsbook.io/pricing](https://docsbook.io/pricing) |

Two consequences follow. On GitBook, the cheapest docs team is a small one, so the model quietly discourages the thing most engineering orgs want — more engineers editing docs. On Docsbook, the cheapest docs team is one whose readers find the answer on the page rather than asking the assistant, so the model rewards writing the page.

Do the arithmetic against your own team size on the vendor's own page. This post deliberately publishes no worked example: GitBook's numbers change, ours are generated per request, and a table of both would be wrong within a quarter of publishing. [docsbook.io/pricing](https://docsbook.io/pricing) is regenerated from the live pricing constants on every request, which is why it is the only number worth quoting back to us.

## Migration path: GitBook → Docsbook

If you're considering moving, here's the realistic path. We've watched this run several times.

1. **Export from GitBook.** Use GitBook's space export to get your content as Markdown. Expect to fix image paths and any block-editor weirdness manually — count on a half day to a day depending on how many custom blocks you used.
2. **Drop the files into a `docs/` folder in any GitHub repo.** Public or private. If you don't have a repo, create one.
3. **Paste the repo URL into Docsbook.** Site goes live in 5 seconds at `docsbook.io/owner/repo`. Verify everything renders.
4. **Connect your custom domain.** Point DNS at Docsbook to serve `docs.yourcompany.com` with automatic SSL.
5. **Enable AI chat and translations.** Optional but cheap to turn on. Most teams turn them on the same day.
6. **Set up redirects on the old GitBook domain.** Use Cloudflare Workers, Netlify, or a redirect service to send `*.gitbook.io/yourspace/*` to the new paths.
7. **Cancel GitBook.**

The whole thing is usually a one- or two-day project. The longest part is fixing block-editor quirks in the exported Markdown, and that's a one-time cost.

## When GitBook is actually the better choice

We'd rather you stay on GitBook than buy Docsbook and be disappointed. Here are the cases where GitBook genuinely fits better.

- **Your docs editors are non-technical.** GitBook's WYSIWYG editor lets product managers, support leads, and writers contribute without learning Markdown or Git. If half your editors don't know what a pull request is, GitBook is the right tool.
- **You need real-time co-editing.** GitBook supports live multi-user editing in the browser. Docsbook does not — your collaboration model is "git push".
- **You need branched workflows with change requests inside the editor.** GitBook's change-request UI is mature. Docsbook leaves this to GitHub PRs, which is the right call if your editors are engineers and the wrong call if they aren't.
- **You are buying for an enterprise team that requires SOC 2 Type II, SAML SSO, and a dedicated CSM.** GitBook has all of this packaged. Docsbook is moving in that direction but isn't there yet.
- **You're already on GitBook, your team is happy, and the bill is acceptable.** Migration cost is real. If the current setup works, don't fix what isn't broken.

If none of the above apply to you, Docsbook is almost certainly the better fit.

## FAQ

**Is Docsbook open source?**
No, but your content is. Your Markdown lives in your GitHub repo and you can stop paying for the hosted site at any time without losing access to a single page.

**Does Docsbook support private repos?**
Yes. You authorize Docsbook to read a private repo, and the published site can also be private or public depending on your settings.

**Can I keep editing in GitBook and mirror to Docsbook?**
You can, but it defeats the point. Pick one source of truth. If GitBook is yours, stay on GitBook. If GitHub is yours, come over.

**What happens to my SEO if I migrate?**
Set up 301 redirects from every old GitBook URL to the matching Docsbook path. Search engines follow a 301 and carry the ranking signals across; a path you forget to redirect is the one that loses traffic. Docsbook emits per-page meta tags and JSON-LD by default, so the new pages are not missing markup the old ones had — but no platform can promise you a ranking, and this one does not.

**Does Docsbook have AI search like GitBook?**
Yes. AI chat is trained on your own docs, and its cost is metered in dollars against the project's balance rather than gated behind a tier. You can also bring your own API key — OpenRouter, OpenAI, Anthropic or Gemini — and pay the provider directly instead.

**Can I customize the look and feel?**
Yes. Logo, favicon, accent colours for light and dark, Google Fonts, and per-component visibility toggles — search bar, copy button, edit-on-GitHub link, AI chat button and the rest. The one thing you cannot switch off is the small "Powered by Docsbook" link in the page footer: it renders on every Docsbook site, unconditionally.

## The honest bottom line

GitBook is a great product for a specific audience: mid-market and enterprise teams who want WYSIWYG editing, live collaboration, and don't mind paying per editor.

Docsbook is a good product for a different audience: teams whose docs already live in GitHub, who do not want their content inside a vendor's database, and who would rather pay for what the AI actually does than for the number of people allowed to edit.

If you are the first audience, GitBook is the right call. If you are the second, Docsbook is the better fit — and the deciding factor is not the price today but which number grows when the team does.

[Start free — no credit card](https://docsbook.io/start)

## Next steps

- [Migrating from GitBook to Docsbook](./migrating-from-gitbook-to-docsbook.md) — the export, the import and the redirect list
- [Docusaurus alternatives in 2026: 9 platforms compared](./docusaurus-vs-docsbook.md) — the wider field, if GitBook is not your only candidate
- [AI documentation platforms compared](./ai-docs-platform-comparison.md) — the AI feature matrix across four managed platforms
- [Custom domain for documentation](./custom-domain-for-docs-howto.md) — the DNS and SSL steps for `docs.yourcompany.com`
