---
title: "Why we don't use Notion for docs — engineering lessons"
description: "A first-person take on why Notion stopped being a fit for product documentation — search, version control, hreflang, AI crawling, performance, and lock-in, with what we use instead."
---

# Why we don't use Notion for docs — engineering lessons

I used to put everything in Notion. Internal handbook, product specs, customer-facing FAQ, API examples, the runbook for the on-call rotation, the changelog, the half-finished onboarding guide that nobody read. One workspace, one search box, one set of permissions. It felt great for about eighteen months.

Then we tried to grow traffic to the docs. And then we tried to add a second language. And then a customer asked why the page they were reading was three releases behind the API. By the time I migrated everything off Notion, I had a list of mistakes I wish someone had handed me on day one.

This is that list. It is not a takedown — Notion is a genuinely good product for what it is built for. It is a post about the specific moment when "good wiki" stops being "good docs", and how to notice that moment before you have 400 pages and a sales team that needs the docs to actually rank.

## Where Notion still wins

Before the complaints, the honest part.

Notion is the best tool I have used for collaborative thinking. Strategy docs, meeting notes, RFCs in draft, product specs being argued over by four people in comments — Notion is the right answer. The block model, the database views, the inline databases, the linked mentions, the fact that anyone non-technical can edit without breaking anything — all of that is real and hard to replicate.

If your docs live entirely inside the company and never have to compete for a stranger's attention on Google, Notion is fine. If your audience is forty people who all have your Notion login, this post does not apply to you. Close the tab and go write something useful.

The rest of this post is about the moment the docs leave the building.

## 1. Search is two different problems and Notion solves one

Notion's internal search is excellent. Cmd+K, fuzzy match across titles, jump straight to the page. That is the search that engineers care about, and Notion built it well.

The search that *customers* care about lives on Google, ChatGPT, and Perplexity. And on that search, Notion is hostile by default. Pages load via JavaScript, the HTML is mostly empty until React hydrates, internal links go through `notion.so/<hash>` redirects, headings often render with non-semantic markup, and the URLs look like `notion.site/Getting-Started-9f8a3b2c1d4e`. Google can crawl it, but the SEO outcome is consistently worse than the same content as plain markdown on a normal domain.

The first time a competitor with objectively worse content outranked us because they wrote markdown and shipped a sitemap, I felt the lesson land. Customer-facing docs are an SEO surface. They need to be treated like one. A wiki is not an SEO surface.

## 2. Version control that is not version control

Notion has page history. It is not git. The difference matters more than I expected.

I cannot diff two versions of a doc in a code review. I cannot ask "what changed in the auth section between v1.4 and v1.5?" and get a clean answer. I cannot put a docs change in the same pull request as the code change it documents, so the docs are always slightly behind. I cannot ask a junior engineer to update the API reference as part of the same PR that ships the API, because the docs live in a different system with different permissions and a different mental model.

The result is documentation drift. The code ships on Monday, the doc gets updated on Thursday, and on Wednesday a customer reads the old version and files a support ticket. Multiply by every release. The fix is not "remind people to update Notion". The fix is to put the docs next to the code, so that "the code shipped but the docs did not" is something the diff tooling can yell at you about.

Once I had docs in a repo with PR templates, doc updates started being part of the definition of done, not an afterthought. That single workflow change did more for doc freshness than any tool.

## 3. Multilingual is not a feature, it is an architecture

We tried to internationalise our Notion docs once. The plan was reasonable: duplicate the workspace, translate, link from a language switcher. Within a month it was unmaintainable.

The real cost of multilingual docs is not the translation. It is the *coupling* between languages. When the English version changes, every translation is now stale, and you need a system that knows it. You need:

- A canonical source so translators know which version they are translating from.
- A way to mark a translation as out-of-date when the source moves.
- `hreflang` tags so Google knows the Spanish page is the Spanish version of the English page, not a duplicate.
- One URL per language with predictable paths (`/es/getting-started`, `/de/getting-started`).
- A way to publish a partial translation — some pages in five languages, others in two — without breaking the navigation.

Notion does none of this. You end up with five disconnected workspaces and a Google Sheet tracking what got out of sync. The Google Sheet wins for about three weeks and then everybody gives up.

If you ever plan to ship docs in more than one language, do not start in Notion. The migration cost grows linearly with page count and the pain grows superlinearly.

## 4. AI crawlers cannot read your wiki

This is the new one, and the one I underestimated.

By 2026, a meaningful share of "how does X work" questions never reach your website. The user asks ChatGPT, Claude, or Perplexity, and the answer is synthesised from whatever those models can see. Mintlify publicly reports that 45% of their docs traffic is now from AI agents. Our own numbers are smaller but moving the same direction.

For an AI crawler to cite your docs, it has to be able to *read* your docs. That means clean server-rendered HTML, semantic headings, a `sitemap.xml`, ideally an `llms.txt` listing the canonical content, and an `Allow` for the major AI user-agents in `robots.txt`. Notion gives you almost none of this. The HTML is JavaScript-heavy, there is no `llms.txt`, and the AI crawler answer-rate is empirically poor.

If you want to be cited in an answer engine, your docs need to look, to a crawler, like a documentation site. They cannot look like a SPA built around a database view.

## 5. The performance budget for docs is brutal

A docs page should feel instant. That is not a stylistic preference — it is a conversion lever. The user is debugging at 2am, they are already frustrated, every second of load time is a chance for them to give up and file a ticket instead.

Run a Notion-published page through Lighthouse. The numbers are not great. Largest Contentful Paint is usually in the 3–5 second range on a real cellular connection, Cumulative Layout Shift is noticeable because the React tree hydrates in waves, and Total Blocking Time is high because there is a lot of JavaScript to parse.

For an internal wiki nobody cares. For a customer-facing doc that has to compete with a thousand other tabs the user has open, it matters a lot. We saw bounce on docs pages drop materially when we moved to statically-rendered markdown. That is one of those numbers that, once you have seen it, you cannot unsee.

## 6. The lock-in is real and it compounds

Notion has an export. I have used it. The output is a folder of HTML or markdown files with mangled filenames, broken internal links pointing at `notion.so` URLs, embedded databases that flatten into unreadable tables, and image references that point at signed S3 URLs which expire. Exporting 400 pages and then fixing the export is a week of work.

Lock-in is not about whether the export button exists. It is about whether the exported data is structured enough to be useful in another tool without a port. By that test, Notion exports are weak. The longer you stay, the more pages you accumulate, and the higher the migration cost climbs. You only notice when you try to leave.

Markdown in a git repository has the opposite property. The "export" is `git clone`. You can move the directory to any other static site generator, any other docs platform, or just publish it as raw files. That portability is the single most underrated property a docs system can have. It does not feel valuable until the day you need it, and then it is worth everything.

## 7. Permissions, drafts, and the wiki-vs-docs split

The deepest problem is that wikis and docs are different products that happen to look the same in the editor.

A wiki is for *us*. It has drafts, half-finished pages, internal-only sections, pages where two team leads disagree in the comments, runbooks that should never be public, and an "archive" folder that is really just where things go to be forgotten. The permission model is granular because the audience is granular.

Docs are for *them*. There is one published version, no half-states, no drafts visible to readers, and no comments threads visible from the public URL. Drafts live in pull requests, not in the production tree. The permission model is binary — published or not — because the audience is the entire internet.

Notion is built for the first job and patched for the second. You end up with a workspace that mixes internal handbook pages and customer-facing API docs in the same tree, and one configuration mistake makes the wrong page public. I have seen this happen at three companies, and I almost did it myself.

The boundary between "wiki" and "docs" is worth making physical. Different system, different repo, different review workflow, different domain.

## What we use now

For internal stuff that needs comments, opinions, drafts, and inline databases — strategy docs, RFCs, meeting notes, the handbook — Notion is still the right tool. We did not stop using Notion. We stopped using it for the wrong job.

For customer-facing documentation, the docs live in a git repository, written in markdown, reviewed via pull requests, published as a static site. The setup is boring on purpose. The docs are next to the code, so they update in the same PR. The git history is the version history. The repository is the export. The CI runs link checking. The published site is server-rendered with proper headings, a sitemap, an `llms.txt`, and one URL per language.

Whether you use [Docsbook](https://docsbook.io), Docusaurus, Mintlify, VitePress, or roll your own with eleventy is a smaller decision than it looks. The bigger decision is the one before: are these docs for the team, or are they for the world? If they are for the world, get them out of the wiki and into a system that treats them like a product.

We built Docsbook because we wanted "git repo of markdown" to be five seconds away from "published documentation site with SEO, AI chat, fifteen languages, and analytics" — without a single CI step or `docusaurus.config.js`. That is the version of this story where we have a product to sell. It is also the honest path we walked. We tried Notion first. We tried Docusaurus second. We ended up writing Docsbook because we wanted the simplicity of Notion with the engineering properties of a real docs site, and nobody else had built it.

## The one principle worth keeping

If your docs need to be found by people who do not work at your company, they are an SEO and AI-discoverability product. Treat them like one. Put them in source control, render them as HTML, give every language a real URL, and make sure a crawler can read them without running your JavaScript.

A wiki is for the people who are already inside. Docs are for the people who are still outside, looking in. You only get one shot at that first impression, and it usually happens at 2am, on a phone, while the user is annoyed. Build for that user, not for the team meeting where the doc got written.

That is the lesson. Everything else is implementation detail.
