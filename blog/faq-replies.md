---
title: "FAQ Reply Notebook — copy-paste answers for community comments"
description: "Internal notebook with ready-to-paste answers to the questions people keep asking about Docsbook on Reddit, X, IndieHackers, Product Hunt, and HackerNews. TL;DR for quick replies, Long versions for posts and threads."
---

# FAQ Reply Notebook

> **For internal use** — copy-paste replies for Reddit, X, IndieHackers, Product Hunt, HackerNews, and comments under competitor posts.
>
> **Format per question:** **TL;DR** (1–2 sentences, fits a tweet) + **Long** (3–5 sentences for threads and blog comments).
>
> **Tone:** honest founder voice. No marketing fluff, no "revolutionary AI-powered platform". Lead with the concrete thing it does, mention the trade-off, link the docs if relevant.
>
> **Source of truth for numbers and facts:** [README.md](https://github.com/Docsbook-io/docsbook/blob/main/README.md). If a number here disagrees with README, README wins — fix this file.

---

## 1. General

### What is Docsbook?

**TL;DR:** Docsbook turns a public GitHub repo into a documentation site in a few seconds. Paste `github.com/user/repo`, the site appears at `docsbook.io/user/repo`, and every push to main updates it automatically.

**Long:** It's a hosted docs platform aimed at people who want their docs to live as Markdown in GitHub — not in a proprietary CMS. There's no CI/CD to set up and no `docusaurus.config.js` to babysit. You get the docs site, a built-in AI chatbot trained on your content, AI translations to 15 languages with separate SEO indexing, full analytics, and an MCP server so AI agents can manage the workspace. Custom domain with free SSL is a Business-tier add-on. Free plan is real — not a trial.

---

### Who is it for?

**TL;DR:** SaaS founders, dev-tool teams, and OSS maintainers who want serious docs without spending two weeks on Docusaurus setup or $200+/month on GitBook.

**Long:** The sweet spot is a small team that already writes Markdown in GitHub and wants the published site, search, AI chat, translations, and analytics — without owning the infra. Teams that also want a custom domain or webhooks step up to Business. If you have a tech writer and a custom design system, Docusaurus is probably still better. If you have a 20-person docs team and enterprise SSO requirements, GitBook fits. Everyone in between is who Docsbook is built for.

---

### How long does it actually take to publish?

**TL;DR:** 5–30 seconds. Connect GitHub, point at a repo, the site is live. No build step, no deploy.

**Long:** First publish is the longest because we index the repo through the GitHub API. After that, every push to main updates the site within seconds — no GitHub Action, no Vercel deploy of your own to maintain. The indexing pipeline reads `README.md` and the `docs/` folder, parses with `markdown-lsp` (our open-source LSP parser, AST via unified+remark instead of fragile regex), and renders with shiki + rehype.

---

### Where does my content actually live?

**TL;DR:** In your GitHub repo. Docsbook reads from it but never writes back. Cancel anytime — your Markdown stays exactly where it was.

**Long:** This is the anti-lock-in story. Notion, GitBook, and Mintlify (mostly) own your content — to leave you have to export. With Docsbook, the source of truth is your repo. We cache and index, but we don't store the content authoritatively. Workspace settings (branding, AI config, domain, analytics) live in our Postgres; if you churn, those settings go away — your docs don't.

---

## 2. Pricing & plans

### How much does it cost?

**TL;DR:** Free forever for the basics. Pro is **$59/month** (AI chat, translations, SEO). Business is **$159/month** and adds custom domain, webhooks, bring-your-own API keys, and higher AI/translation limits.

**Long:** Free covers any public GitHub repo, branding, UI controls, navigation, 24h analytics, and base MCP tools. Pro ($59/month) adds AI chat, AI translations (15 languages), full SEO, and longer analytics windows (up to 30 days). Business ($159/month) includes everything in Pro plus a set of Business-exclusive capabilities: custom domain with free SSL, webhooks, bring-your-own AI/translation API key, and higher usage limits. Per-workspace billing, not per-seat.

---

### Is the Free plan a trial?

**TL;DR:** No. Free is forever. You can run a real public docs site on it with custom branding, navigation, theme, fonts — just no AI chat, no translations, no custom domain.

**Long:** I (Dan) made Free generous because I want OSS maintainers and indie hackers to actually use the thing without thinking about pricing. The paid plans exist for people who need AI features or a custom domain. If your repo is public and you just want a nice docs site, Free is everything you need.

---

### Why is Pro a subscription and not a lifetime deal?

**TL;DR:** We used to sell a one-time lifetime PRO plan; it's no longer offered to new customers, and existing lifetime customers are grandfathered. Current plans are subscriptions because AI chat, translations, and the MCP server carry ongoing inference and infrastructure cost.

**Long:** Docs are a living product now — the old flat lifetime price didn't scale with how much LLM inference a workspace actually uses. Pro ($59/month) and Business ($159/month) are subscriptions so we can keep AI/translation limits generous and keep shipping. If you bought the original one-time lifetime PRO before the move to subscriptions, you keep your original features forever at no extra cost — but that plan is retired and isn't sold anymore.

---

### What happens if I exceed AI request limits?

**TL;DR:** AI chat pauses until your next billing cycle — never billed above your plan price — or bring your own OpenAI / Anthropic / Gemini / OpenRouter key on Business, then it's free on our side.

**Long:** Every paid plan (Pro, Business, Growth, Scale) has a monthly AI budget, with higher-tier plans set higher. If you use it up, AI chat simply pauses until the next cycle instead of billing anything further. Business also lets you plug in your own API key in the AI settings and route requests through your provider — then we don't meter at all. Same applies to translations, which stay on the older request-count model for now.

---

### Is there a refund policy?

**TL;DR:** Yes — email me (dan@docsbook.io) within 30 days, no questions, full refund through Paddle.

**Long:** Trust matters more than any single sale. If Docsbook turns out not to fit your workflow, I'd rather refund than have an unhappy customer telling people not to use it. Paddle handles the refund mechanics, usually in a couple of business days.

---

## 3. Competitors

### How is this different from GitBook?

**TL;DR:** Same outcome (hosted docs site), ~$200/month cheaper, includes AI chat + AI translations in the price, content stays in *your* GitHub repo.

**Long:** GitBook starts at ~$8/user/month and serious teams end up paying $200+/month. AI features, translations, and analytics are paid add-ons. Content lives in GitBook's CMS — to leave, you export. Docsbook is $0 / $59 (Pro, AI + translations) / $159 (Business, adds custom domain, webhooks) per month, and your Markdown stays in your GitHub repo. The trade-off: GitBook has a richer WYSIWYG editor; we don't have one — you write Markdown.

---

### How is this different from Docusaurus?

**TL;DR:** Docusaurus is a React framework you self-host. Docsbook is a hosted product. 30 seconds vs. 2–3 days of setup + ongoing maintenance of a Node.js app.

**Long:** Docusaurus is fantastic if you want full control and have a team that enjoys owning the build pipeline, plugins, theme overrides, and a deployment target. Docsbook is for people who want the docs site without owning the framework. We also bundle search, AI chat, translations, and analytics, which are separate plugins/services in a Docusaurus setup. If you already shipped Docusaurus, don't migrate — it works fine. If you're starting today and don't need framework-level customization, Docsbook gets you there in seconds.

---

### How is this different from Mintlify?

**TL;DR:** Comparable feature set (hosted docs, AI), but Mintlify pushes you toward MDX in their structure. Docsbook reads plain Markdown from any GitHub repo and is generally cheaper.

**Long:** Mintlify is good — well-designed, well-marketed. Where we differ: (1) we work with any public GitHub repo that has Markdown in `README.md` or `docs/`, no project-specific config required; (2) per-workspace pricing, not per-seat, starting at $59/month vs. Mintlify's $150/month entry; (3) we expose a full MCP server with 61 tools, so AI agents can manage your workspace programmatically (read the doc graph, search by symbol, change branding, etc.). Their core docs experience is more polished out-of-the-box; ours catches up faster the more you customize.

---

### How is this different from Notion?

**TL;DR:** Notion is great for internal wikis. Bad for public docs — no real SEO, no AI chat trained on the content, no custom domain on most plans, and Google doesn't index it the way it indexes docs sites.

**Long:** I see a lot of teams using Notion as "docs" and then wondering why nobody finds them. Notion pages don't structure as docs (no proper heading hierarchy for SEO), don't expose `sitemap.xml`, don't have a built-in AI chat for visitors, and don't generate `llms.txt` for AI agents. Docsbook is built specifically for docs that need to be found — by Google, by ChatGPT, by Perplexity. Keep Notion for your internal wiki; put public docs somewhere built for it.

---

### How is this different from Readme.io?

**TL;DR:** Readme.io is API-docs-focused and expensive ($99–$3000/month). Docsbook is broader (any docs from any GitHub repo), much cheaper, and bundles AI + translations.

**Long:** If you have an OpenAPI spec and want polished API reference with try-it-now, Readme.io is built for that exact job and does it well. Docsbook is a more general docs platform — guides, references, blog posts, anything you can put in Markdown. If you need both, plenty of teams use Readme.io for API reference and Docsbook for the broader docs site.

---

## 4. AI chat & translations

### How does the AI chat work?

**TL;DR:** It's trained on *your* documentation only, not the open web. Visitors ask questions, it answers with citations to your doc pages.

**Long:** The flow is Search → Reading → Answer. The chatbot retrieves relevant sections from your indexed doc graph, then synthesizes an answer with the LLM, citing the pages it pulled from. You can configure suggested questions, the system prompt, pre/post LLM hooks, and the model provider (we default to OpenRouter `openai/gpt-4o-mini`, but you can plug in your own OpenAI / Anthropic / Gemini key). Streaming responses, full usage analytics, and a `get_ai_questions` MCP tool so you can see what your users are actually asking.

---

### Which AI providers can I use?

**TL;DR:** OpenRouter (default), OpenAI, Anthropic, Gemini. You can bring your own API key and pick any model the provider supports.

**Long:** Default is OpenRouter with `openai/gpt-4o-mini` because it's cheap and good enough for most docs Q&A. You override at the workspace level in AI settings — paste your key, choose model, done. Requests through your own key don't count against the monthly cap. This is also how you can route to a private/dedicated deployment if compliance requires it.

---

### How do AI translations work?

**TL;DR:** 15 languages (EN, ES, FR, DE, PT, IT, RU, ZH, JA, KO, AR, HI, TR, PL, NL). Each translated version gets indexed in Google as a separate page, with proper hreflang.

**Long:** You enable a language in the workspace, Docsbook generates the translation, and the translated version becomes a real page at `docsbook.io/[owner]/[repo]/[lang]/...`. Google treats each language as a distinct indexable URL — so you get separate SEO for each market. There's a language switcher in the sidebar or header (configurable), and we auto-detect the visitor's language with `franc`. Business gets a higher monthly translation cap than Pro. If you have your own translator workflow, set translation mode to `external` and push translations via the MCP tool or webhook.

---

### Can I review translations before they go live?

**TL;DR:** Yes — Pro and Business support a pending-approval queue. Translation lands as a draft, you approve via MCP (`approve_translation`) or the dashboard, then it publishes.

**Long:** This matters for languages where you have a native speaker on the team and want a sanity check before shipping. There's also `list_pending_translations` and `get_translation` MCP tools so an agent can pre-screen drafts and only surface the ones that look questionable.

---

## 5. SEO & AI discovery

### Does Docsbook generate `llms.txt`?

**TL;DR:** Yes. Every workspace gets `/llms.txt` and `/llms-full.txt` automatically, on every plan including Free. Platform-level too: `docsbook.io/llms.txt`.

**Long:** `llms.txt` is the emerging standard for telling AI agents (Perplexity, ChatGPT Search, Cursor, Cline) what your site is and how it's structured. We generate it from your doc graph — list of pages with titles and descriptions, in a format the AI clients actually parse. `llms-full.txt` is the same plus full content. Both work without configuration; they exist the moment your workspace is indexed. This is one of the reasons Docsbook content gets cited by AI search disproportionately well.

---

### What about regular SEO?

**TL;DR:** Built-in. Meta tags, OpenGraph, sitemap.xml, JSON-LD (WebSite, Organization, SoftwareApplication, FAQPage), canonical URLs, separate indexing per language. Free on every plan.

**Long:** Each page gets a proper `<title>`, `<meta description>`, OpenGraph image, and JSON-LD blocks for structured data. Sitemap is auto-generated and pings Google on update. Translations are exposed with hreflang. Custom domain (Business) plus the SEO setup means a Docsbook site behaves like a real docs site to Google, not a SPA. This is the main reason teams pick us over Notion for public docs.

---

### Will AI search engines actually cite my docs?

**TL;DR:** Yes if your content is well-structured and your `llms.txt` is solid — both of which Docsbook does by default. We see Docsbook-hosted docs cited regularly in Perplexity and ChatGPT Search.

**Long:** AI search citation depends on (1) being indexable (we handle that), (2) being structured so the model can extract concrete claims (heading hierarchy, code blocks, lists — your Markdown already does this), (3) having `llms.txt` (we generate it), (4) being authoritative for the topic (that's on you and how you write). On the technical side, Docsbook removes the usual blockers. For agents working against your repo directly, [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) adds LSP-style navigation (`doc_outline`, `doc_search_symbols`, `doc_resolve_link`, etc.) so they can navigate precisely instead of slurping raw HTML.

---

## 6. Technology & integrations

### What tech stack does Docsbook run on?

**TL;DR:** Next.js 16 on Vercel, PostgreSQL on Neon, Redis cache, Drizzle ORM. AI via OpenRouter/OpenAI/Anthropic/Gemini. Boring, fast, scales.

**Long:** Frontend is Next.js 16 App Router + React 19 + Tailwind 4 + shadcn/ui. Auth is `next-auth v5` with GitHub OAuth. Database is Neon serverless Postgres with Drizzle migrations. Markdown pipeline is `unified` + `remark-parse` + `remark-gfm` + `remark-rehype` + `rehype-pretty-code` + `shiki`. MCP server is `@modelcontextprotocol/sdk` 1.29 with full OAuth 2.0. Hosting is Vercel including custom domains, billing through Paddle, analytics through Axiom.

---

### Does it work with private repos?

**TL;DR:** Public repos work out of the box. Private repos via authenticated GitHub OAuth — same flow, we just need read access to the specific repo.

**Long:** When you connect GitHub, you grant access to the repos you want indexed. For OSS projects this is the public-repo flow with no extra scopes. For private repos, you authorize specific repos through the GitHub App and we read them with the user's token. We never store the content authoritatively — only the indexed graph and cache, which we can invalidate at any time.

---

### Can I use a custom domain?

**TL;DR:** Yes, on Business. Point a CNAME to Docsbook, we provision the SSL certificate, done. `docs.yourcompany.com` works in a few minutes.

**Long:** Custom domains run through Vercel's domain API. You add `docs.yourcompany.com` in the workspace dashboard or via the `update_domain` MCP tool, set a CNAME at your DNS provider, and Vercel issues the SSL cert automatically. We also proxy through `/docs-proxy/[[...path]]/` so the URL stays clean and analytics keep working.

---

### Is there an MCP server?

**TL;DR:** Yes — full OAuth 2.0 MCP server at `https://docsbook.io/api/mcp/server` with 61 tools for workspace management, branding, analytics, webhooks, and translations. For doc-graph search use [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) locally, not the hosted MCP.

**Long:** Connect the hosted MCP with `claude mcp add --transport http https://docsbook.io/api/mcp/server`. After OAuth, the agent gets tools across workspace management (create, branding, UI), AI chat (system prompt, hooks), translations (approve, upload, delete), analytics (questions, unanswered, failed searches), and webhooks (register, list, replay). For LSP-style doc-graph operations — outline, symbol search, link resolution, references — use [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) locally instead (`npx markdown-lsp <subcommand> ./docs`). It parses the repo on disk, which is faster and cheaper than going over the network.

---

## 7. Security, privacy & lock-in

### What happens to my data if I cancel?

**TL;DR:** Your Markdown stays in your GitHub repo. We delete workspace settings (branding, AI config, analytics) on request. No "export" required — your content was never ours.

**Long:** This is the structural difference from GitBook/Notion. With them, cancellation means an export ritual to get your content back. With Docsbook, your content was always in your repo — when you disconnect the workspace, your repo is unchanged. What we hold is workspace metadata in Postgres (which is what you're paying for), and analytics events in Axiom, both of which we delete on request.

---

### Where is the data hosted?

**TL;DR:** Vercel (global edge), Neon Postgres (US/EU regions), Redis cache, Axiom for logs. All US/EU infrastructure.

**Long:** Standard hosted-SaaS infra. Vercel handles HTTP and CDN globally. Neon is serverless Postgres, we run in their default region with point-in-time recovery. Redis is for caching the skills index. Logs and analytics go to Axiom. If you need a specific region commitment for compliance, talk to me — for now we deploy in the standard Vercel/Neon footprint.

---

### Is the source open?

**TL;DR:** Docsbook itself is closed-source. `markdown-lsp` (our parser) and `docs-skills` (the AI skills catalog) are open source on GitHub.

**Long:** The platform is closed but we OSS the parts that benefit the broader ecosystem. [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) is our LSP-style parser that turns Markdown into a structured doc graph — it powers local doc-graph search and is useful for anyone building docs tooling. `docs-skills` is a public catalog of 25 SKILL.md files for AI agents (`docs-analyze`, `docs-seo`, etc.) — works with Docsbook MCP and also standalone.

---

## 8. Objections & pushback

### "Why not just use Docusaurus, it's free?"

**TL;DR:** Docusaurus is free in dollars, not in time. Two days of setup + ongoing maintenance of a Node.js app costs more than a year of Docsbook Pro if you bill your own time.

**Long:** Docusaurus is great and I recommend it for teams that want full control. But "free" is the framework — you still need to host it, maintain the build, manage dependencies, add a search service (Algolia $$$), add analytics, add AI chat (custom), add i18n (custom), etc. The total cost of ownership over a year is meaningful. Docsbook trades the customization ceiling for setup time and bundled features. Both are valid choices.

---

### "$59/month for a docs site, that seems steep."

**TL;DR:** Compare it to what else is out there — GitBook, Mintlify, and Readme.io all start well above that for a comparable feature set. Free covers a real public docs site with no AI needed.

**Long:** I get the reaction at first glance. Compare it to GitBook ($200/mo for a real team), Mintlify ($150/mo+), Readme.io ($99/mo+) — all of which are subscriptions, same as us. Pro at $59/mo covers AI chat, translations, and SEO. Business at $159/mo is for teams that also want a custom domain, webhooks, or bring-your-own API keys. If you only need a public docs site with branding and no AI, Free is genuinely free forever.

---

### "Why GitHub-only? What if my source is in GitLab/Bitbucket?"

**TL;DR:** GitHub-only today. GitLab and Bitbucket are on the roadmap but not soon. If you have an active need, email me — that helps prioritize.

**Long:** Honest answer: GitHub covers ~90% of the OSS and dev-tool market we're aimed at, and supporting one provider deeply is better than supporting three providers shallowly. GitLab support is plausible because their API is similar; Bitbucket is harder. If GitLab support would unblock you, tell me — I keep a list and that's what moves features up.

---

### "How is this not going to get killed by GitHub adding native docs hosting?"

**TL;DR:** GitHub already has Pages and Wikis — neither is a real docs platform. Even if they shipped one, AI chat / translations / analytics / MCP / custom domain are the differentiators.

**Long:** GitHub Pages has existed for a decade and people still use Docusaurus, GitBook, Mintlify, Readme.io. Why? Because "static HTML hosting from a repo" is the easy 20% — the hard 80% is search, AI, i18n, SEO, analytics, custom domain UX, dashboard, billing for non-technical buyers. The risk isn't GitHub adding docs hosting; the risk is one of the existing players doing the AI + GitHub-native angle better. That's the bar we hold ourselves to.

---

### "Sounds great but I don't trust a one-person company with my docs."

**TL;DR:** Fair. Your content is in your GitHub repo, not in our database — so worst case (we disappear), you lose the hosted site, not your docs. Move them to Docusaurus in a day.

**Long:** This is the actual answer to "what if Docsbook goes away." Your Markdown is in your repo. Workspace settings are recoverable (we expose them via MCP and API). The site URL would break, but the content is untouched. Compare to GitBook/Notion where churn = export pain. The lock-in story is the structural reason small-vendor risk is lower here than with content-owning competitors.

---

## How to keep this notebook fresh

The hard part isn't writing the FAQ once — it's keeping it accurate as the product changes and as new questions come in from real conversations. Concrete options Dan can set up:

### Auto-pull real questions from production

- **MCP tools we already have:** `get_ai_questions`, `get_ai_unanswered`, `get_failed_searches`, `get_popular_searches`, `get_negative_feedback`. Run a weekly cron that pulls these for the `docsbook.io` workspace itself (since our own docs site is on Docsbook) — surfaces the questions our own visitors are asking but the AI couldn't answer, which is the highest-signal feedstock for new FAQ entries.
- **Script:** `scripts/faq-collect.ts` — calls those MCP tools, dedupes against existing questions in this file, posts a digest to Slack/Notion.

### Pull from social channels (needs MCP access)

- **Reddit MCP** — read comments on `r/SaaS`, `r/devops`, `r/programming` mentioning "GitBook", "Docusaurus", "Mintlify", "docs hosting". Real wild questions, not just our existing audience.
- **X/Twitter MCP** — same, but for tweets mentioning competitors or "docs site".
- **Discord/Slack** — if we have an instance, mine support questions. Doesn't exist yet.
- **HackerNews** — Algolia HN API is public, no MCP needed; a 50-line script catches every Docsbook/competitor mention.

### Build a `comment-reply` skill

A `.claude/skills/comment-reply/SKILL.md` that:
1. Takes input: comment text + target platform (Reddit / X / HN / IH).
2. Classifies which FAQ entry matches (or "no match").
3. Returns the TL;DR for X/HN-style platforms, the Long version for Reddit/IH, with platform-appropriate formatting.
4. If no match — drafts a new entry and proposes appending it to this file.

Useful as a CLI alias: `claude comment-reply "<paste comment here>" --platform reddit`.

### Build an `update-faq` skill

A weekly skill that:
1. Pulls new questions via `get_ai_questions` / `get_failed_searches`.
2. Diffs against this file.
3. For each unanswered cluster of >3 similar questions, drafts a new FAQ entry in this file's format and opens a PR.
4. Also flags entries where the *numbers* in README.md have drifted from what's quoted here.

### Manual upkeep checklist (in the meantime)

- [ ] Every release that changes pricing → update Section 2.
- [ ] Every new competitor mention in the wild → consider adding to Section 3.
- [ ] Every quarter → check README.md numbers against quoted numbers here.
- [ ] Every new MCP tool → reference it in Section 6 or "How to keep this fresh".

---

## Related

- [README — Docsbook product overview](https://github.com/Docsbook-io/docsbook/blob/main/README.md)
- [Public FAQ for users](../faq.md)
- [Docusaurus vs Docsbook](./docusaurus-vs-docsbook.md)
- [Mintlify vs Docsbook](./mintlify-vs-docsbook.md)
