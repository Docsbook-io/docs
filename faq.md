---
title: "Docsbook FAQ: cost, limits, sync and data ownership"
description: "Answers to what Docsbook costs, what happens when a balance runs out, who can read your site, how GitHub sync works, and what you keep if you leave."
---

# Docsbook FAQ: cost, limits, sync and data ownership

Questions are ordered by how early they block a decision: money first, then getting started, then how the product behaves once you are running.

## Cost and billing

### How much does Docsbook cost?

Docsbook meters four things, all of them AI work, charged against the balance of the project that asked for them:

- **Readers (AI Chat)** — an AI answer given to a reader of your documentation.
- **Admin & AI Agent** — an agent run you or a connected agent started.
- **AI Translations** — translating a page into another language.
- **Semantic Index** — building the embeddings the AI chat retrieves from.

Everything else is unmetered: hosting the site, a custom domain and its TLS certificate, readers browsing, editors writing, GitHub sync, full-text search, branding, analytics and MCP read calls. Current figures are on [docsbook.io/pricing](https://docsbook.io/pricing), which is generated from Docsbook's billing constants on every request — read prices there, not from a documentation page that can go stale. See [Pricing](./pricing.md) for the mechanism.

### Is there a free way to try Docsbook?

Yes. Generating a draft site needs no account and no credit card: paste a repository, a website URL or a sentence about your product at [docsbook.io/start](https://docsbook.io/start) and read the result before signing in. Every new project is then created with **$1.00** of balance, and a further **$5.00** can be claimed once the project is **3 minutes old**. Both are real credit against AI work.

### How do I start spending, and what does a top-up cost?

The $1.00 a Docsbook project starts with is spendable immediately — ask the AI chat a question and you will watch it move. Press **Claim** on the project's billing card once the project is 3 minutes old to add the **$5.00** welcome credit; nothing adds it on your behalf.

After that you name the amount yourself. The smallest single top-up is **$20.00** and the largest is **$5,000.00**; for more, top up twice. The money lands on the balance of the one project you chose. Nothing refills on a schedule — set up a monthly payment on the billing screen if you want a recurring amount.

### What happens when a project's balance runs out?

The documentation site stays online. Readers keep browsing, full-text search keeps working, GitHub sync keeps running, and nothing is deleted. What stops is metered AI work: the call is refused **before it runs**, and the refusal names which project ran out, what the call would have cost, what is left, and where to top that project up.

Free discovery calls over MCP keep working, so an agent can still report what happened rather than failing silently.

### Can I stop paying, and what happens to my documentation site?

There is nothing to cancel: you top a project balance up when you want to, and stopping means not topping it up again. Your documentation site stays online at `docsbook.io/{owner}/{repo}`, your Markdown stays in your own GitHub repository, and your settings — branding, navigation, layout — are preserved. Nothing is deleted.

If you set up a recurring monthly payment of your own, end it from the billing screen at [docsbook.io/chat](https://docsbook.io/chat).

### Do my files stay mine?

Yes. Your Markdown always lives in your own GitHub repository. Docsbook renders those files; it never stores your content in a proprietary format and there is nothing to export first. Point another documentation tool at the same repository and you keep every page, image and link.

### How do I pay for Docsbook?

Billing runs through Paddle, which is the merchant of record. Open the billing screen from the dashboard at [docsbook.io/chat](https://docsbook.io/chat) and top up the balance of a project — $20.00 at the smallest, $5,000.00 at the largest. Visa, Mastercard, American Express, Apple Pay and Google Pay are accepted.

### Is payment secure?

Yes. Payments are processed by Paddle as merchant of record, and Docsbook never sees your card number. The whole checkout runs on Paddle's own hosted flow.

### Can one account run several documentation sites?

Yes. One Docsbook account can own many projects, and each project carries its own balance. One project running out of balance does not stop another. Which project pays for a metered call is worked out from the call itself — the workspace you named, or the repository it is scoped to.

### Do you offer refunds?

Email [support@docsbook.io](mailto:support@docsbook.io) with your account address and what you paid for. Refunds are handled case by case through Paddle, which processed the payment.

### Are there discounts for organizations?

Email [support@docsbook.io](mailto:support@docsbook.io) to discuss it. There is no published organization discount to quote here.

## Getting started

### Do I need a GitHub repository to try Docsbook?

No. At [docsbook.io/start](https://docsbook.io/start) one field takes whatever you have — a website URL, a repository link, a PDF or screenshots, or a sentence about what you sell — and generates a draft site from it. You land on the draft's admin panel, with the documentation one click away, and can change branding, layout and SEO before creating an account.

GitHub is needed only to link an existing repository, or when you publish. Any sign-in method works: GitHub, Google, Apple, or email with a one-time code.

### What kind of repository does Docsbook need?

Any GitHub repository containing Markdown files. That can be a single `README.md`, a `docs/` folder, an API reference, or a flat pile of `.md` files — Docsbook builds the navigation from whatever structure is there.

### Do I need to configure anything in GitHub?

No. Authorise Docsbook through GitHub OAuth and it reads the repository files. There is no workflow file to add, no GitHub Action to install, and no webhook to register.

### What folder structure should I use?

Any structure works, because Docsbook builds the navigation tree from the folders it finds. A common shape:

```text
repo/
├── README.md
├── docs/
│   ├── getting-started.md
│   ├── api/
│   └── guides/
```

`README.md` at the root of a folder becomes that folder's landing page.

### Can I use `.markdown` instead of `.md`?

Yes. Docsbook reads both `.md` and `.markdown`. Files in other formats — `.txt`, `.rst`, `.adoc` — are not turned into pages.

### Do links between Markdown files work?

Yes. Relative links between Markdown files are resolved to the published URLs, so a link that works on GitHub works on the site. Write them the way you already do:

```markdown
[Concepts](./basics.md)
[Custom domain](../guides/advanced/custom-domain.md)
```

Anchors to headings inside a page (`./basics.md#indexing`) resolve as well.

### How do I add images to my documentation?

Put the image file in your repository — `docs/images/` is a common choice — and reference it with a relative path. PNG, JPG, GIF and WebP are all served.

```markdown
![Workspace settings with the API key field highlighted](./images/workspace-settings.png)
```

Alt text is what a screen reader and an AI crawler read, so describe what the image shows rather than naming the file.

### Can I use HTML in my Markdown?

Yes. Markdown allows inline HTML and Docsbook renders it. Plain Markdown is still the better default, because it survives being read in GitHub, in an editor, and by an agent over MCP.

### How do I switch between GitHub accounts and organizations?

Click the **GitHub button** in the top-right corner of the AI chat. It opens a switcher listing your signed-in account and every GitHub organization you belong to. A green dot on the button means GitHub is linked. Hover any account or organization — tap, on a touch screen — to see its repositories, and connect one as a new project from there.

### Can I move a Docsbook-hosted project to my own GitHub repository?

Yes, from the same GitHub button. Docsbook creates the repository on your account, copies every page into it in one commit, and points the project at it; your edits then commit straight to your repository.

Two consequences before you move: **the public URL changes**, and the previous hosted address stops working with no redirect, so update anywhere you have shared it. And **the move is one-way** — there is no button to move a project back onto Docsbook hosting.

## Publishing and sync

### How do I update my Docsbook documentation?

Edit the Markdown file and commit it to GitHub. The site picks the change up on the next visit — there is no build to trigger and no deploy to wait for. You can also edit in Docsbook's web editor or through an agent over MCP; all three land as commits in the same repository.

### How quickly does a Docsbook site update after a push?

On the next visit. Docsbook checks GitHub for new commits when the site is loaded and re-indexes what changed, so the page you open is built from the current repository state rather than from a cached build.

### Why has my Docsbook site not updated?

Work through these four, in order:

1. Is the commit actually on GitHub? Check the file on github.com.
2. Did you hard-refresh the browser (Ctrl+F5, or Cmd+Shift+R)?
3. Has a minute or two passed since the commit?
4. Does the file end in `.md` or `.markdown`? Other extensions are not indexed.

If all four are fine, email [support@docsbook.io](mailto:support@docsbook.io) with the repository and the commit.

### Does Docsbook site search work?

Yes. Every Docsbook site has built-in full-text search across all of its pages. Click the search icon in the header, or press Cmd+K on macOS and Ctrl+K on Windows and Linux.

### Is there a dark theme?

Yes. Light, dark and follow-the-system themes are all supported. The workspace owner picks the default in branding settings, and readers can switch it from the theme toggle in the header.

### How many concurrent visitors can a Docsbook site handle?

Docsbook sites are served from Vercel's CDN, which scales automatically. There is no visitor limit to configure and no traffic tier to buy.

## Access and privacy

### Who can see my Docsbook documentation?

By default, everyone: anyone with the link, people without a GitHub account, and search-engine crawlers. That is usually what you want, because a public site is what Google indexes and what an AI assistant can quote.

You can change it — see the next answer.

### Can I make my documentation private?

Yes. Switch the workspace to **private** and readers meet an unlock screen instead of your content, gated either by a shared password or by your own SSO identity provider. Structure, pages and the search index stay hidden until a reader unlocks it, and the owner always has full access.

See [Private docs: password and SSO](./guides/advanced/sso.md) for setup.

### Does a private GitHub repository make the published site private?

No. The two settings are independent. Docsbook reads the repository through the GitHub authorisation you granted, then serves the pages it built; who may read those pages is decided in Docsbook's own access settings, not by the repository's visibility.

### Is my documentation served over HTTPS?

Yes. Every Docsbook site is served over HTTPS through Vercel's CDN, and a custom domain gets its TLS certificate provisioned automatically.

### Can someone else edit my documentation through Docsbook?

Not unless you gave them access to the repository. Docsbook writes changes as commits to the repository the site is built from, so repository permissions decide who can change what.

### Who sees the float widget?

Only you, while signed in and viewing your own documentation. Readers see the documentation and nothing else — the float widget is not rendered for them at all.

## Custom domain

### How do I use my own domain for Docsbook?

Enter the domain in your workspace settings, add the CNAME record Docsbook shows you at your DNS provider, and wait for it to propagate. Docsbook provisions the TLS certificate itself.

Full walkthrough: [Custom domain setup](./guides/advanced/custom-domain.md).

### Should I use a root domain or a subdomain for docs?

A subdomain, usually — `docs.example.com`. It is a single CNAME record and it leaves your apex domain alone for the marketing site. A root domain works, and so do several subdomains pointing at different workspaces.

### Do I need to set up SSL myself?

No. Docsbook provisions and renews the TLS certificate for your custom domain automatically, at no extra cost and with nothing for you to configure.

### How long does DNS propagation take?

Usually 15 to 30 minutes, and up to 48 hours in the worst case. The delay is at your DNS provider, not at Docsbook — the domain starts serving as soon as the record resolves.

## Translations

### How do I translate my Docsbook documentation?

Open your workspace settings, select the target languages, and save. Docsbook translates the pages and serves each language on its own route. Translation is AI work, so it draws on the project balance.

Full walkthrough: [Translation guide](./guides/advanced/translation.md).

### Which languages does Docsbook support?

15: English, Spanish, French, German, Portuguese, Italian, Russian, Chinese, Japanese, Korean, Arabic, Hindi, Turkish, Polish and Dutch. Each language is served on its own route with the correct `hreflang` tags, so search engines index it as a separate page.

### How good is Docsbook's AI translation?

Good enough to publish for technical documentation, where the vocabulary is consistent and the sentences are short. Idioms, jokes and culture-specific examples are where it needs a human pass — read those pages before you announce the language.

### Do translations update when I update the original?

Yes. When the source page changes, Docsbook re-translates it, so a language version does not silently drift from the English.

### Can I edit a translation by hand?

Yes. Translations can be downloaded, corrected and uploaded back. Email [support@docsbook.io](mailto:support@docsbook.io) if you want the workflow walked through.

## AI and agents

### What is SEO, GEO and AEO, and why do they matter for docs?

SEO puts your documentation in Google's results. GEO — generative engine optimization — puts it in AI answers: Perplexity citations, ChatGPT Search, Google AI Overviews. AEO — answer engine optimization — adds the structured markup that featured snippets and voice assistants read.

Docsbook generates all three from your Markdown: meta tags, `sitemap.xml`, OpenGraph, canonical URLs, TL;DR blocks, a visible `dateModified`, author markup, FAQPage and HowTo JSON-LD, and speakable selectors. See [SEO](./content/features/seo.md), [GEO](./content/features/geo.md) and [AEO](./content/features/aeo.md).

### What are Docsbook skills?

Docsbook skills are `SKILL.md` files that teach an AI agent how to do documentation work. The catalog is four orchestrator skills, one per job: `docs-analyze` finds what is wrong, `docs-create` writes what is missing, `docs-manage` decides what a page should say, and `docs-automate` makes any of it recur.

Install them with `npx skills add Docsbook-io/docs-skills --skill '*'`, or let an MCP-connected agent discover them at runtime with `find_skill`. See [Docs skills](./ai/skills.md).

### Can an AI agent edit my documentation?

Yes. Docsbook's MCP server exposes 260 tools at `https://docsbook.io/api/mcp/server`, so Claude Code, Cursor or ChatGPT can read your pages, search them, change settings and commit new pages back. Writing requires a token authorised with read-write scope; a read-only token is refused.

See [MCP server](./ai/mcp.md) and the [MCP tools reference](./reference/mcp-tools.md).

## Migrating from another tool

### How do I migrate from GitBook to Docsbook?

Three steps:

1. **Export from GitBook.** GitBook can sync to a Git repository, or export Markdown as a `.zip`. Push the resulting `.md` files to a GitHub repository — any structure works.
2. **Connect the repository.** Paste `github.com/your-org/your-repo` at [docsbook.io/start](https://docsbook.io/start).
3. **Re-point your domain.** Remove the custom domain in GitBook, add it in Docsbook, and update the CNAME record. The TLS certificate is provisioned for you.

What carries over automatically: page structure, internal links (relative `.md` paths are resolved), images, GFM code blocks, headings and frontmatter. What you redo: branding, navigation links, and the AI chat's suggested questions. Side-by-side comparison: [GitBook vs Docsbook](./blog/gitbook-vs-docsbook.md).

### What happens to my docs if Docsbook shuts down?

Nothing is lost. Your Markdown files live in your own GitHub repository, in an open format, with their history. Point another tool at the same repository and you keep everything — there is no proprietary store to escape and no export to request.

## Support, legal and technical

### How do I contact Docsbook support?

Email [support@docsbook.io](mailto:support@docsbook.io), or ask in the [Docsbook Discord](https://discord.gg/baqUCdwrag). Include your project address — `docsbook.io/{owner}/{repo}` — so the answer can look at the right site.

### What should I do if something is broken?

Email [support@docsbook.io](mailto:support@docsbook.io) with three things: the page URL, what you expected, and what happened instead. A screenshot helps; the commit SHA helps more if the problem is about content that did not appear.

### Where can I see Docsbook product updates?

The [changelog](./CHANGELOG.md) records every shipped change and what it was meant to buy. Shorter announcements go to [twitter.com/docsbook](https://twitter.com/docsbook).

### What is Docsbook built with?

Next.js 16, React 19, TypeScript and Tailwind CSS on Vercel, with Postgres (Neon) and Redis behind it, Drizzle as the ORM, Paddle for billing, and the GitHub API for repository access. AI calls route through OpenRouter or your own provider key.

### Where is Docsbook data stored?

On Vercel's infrastructure and in Neon Postgres, hosted in the United States and other regions. Your documentation content itself stays in your GitHub repository — Docsbook stores the index it builds from it, not a second copy of your source of truth.

### Which Markdown parser does Docsbook use?

remark and rehype, through unified, with GitHub Flavored Markdown (GFM) supported. Navigation and link resolution use [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp), Docsbook's open-source documentation parser, and syntax highlighting uses Shiki.

### Is there a Terms of Service and a Privacy Policy?

Yes: [Terms](https://docsbook.io/terms) and [Privacy](https://docsbook.io/privacy). If a site breaks the terms, Docsbook contacts the owner first and normally gives a chance to fix it before anything else happens.

## Related

- [Pricing](./pricing.md) — what is metered, and what a project balance pays for
- [Quick start](./quick-start.md) — publish a documentation site, from source to public URL
- [Concepts](./basics.md) — every term used above, defined once
- [Use cases](./use-cases.md) — the jobs teams hire documentation for

<!-- widget:cta -->

## Still deciding?

Generate a draft from your own repository or website and judge the result before you sign in.

[Start free — no credit card](https://docsbook.io/start)

<!-- /widget -->
