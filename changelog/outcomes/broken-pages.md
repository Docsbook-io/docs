---
title: "What Docsbook has shipped that fixes broken doc pages"
description: "Every release that leaves fewer pages broken or unreachable: dead links, orphan pages, failed builds, and the health checks that surface them early."
---

# What Docsbook has shipped that fixes broken doc pages

Everything Docsbook shipped that moves one number: **Broken pages** — fewer pages that are broken or unreachable. On this axis, down is better.

Claims and links that stopped being true — found before a reader finds them. This is the Broken pages slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 04.09.2026

### Fixed

- A station with nothing to report no longer fails the whole run. On a project with no Search Console history and no in-doc searches, a station that correctly answered "there is no intent mismatch to explain here, and here is each check I could not make and why" was refused three times over and stopped the route, so an agent could not finish on exactly the projects it had least to invent about. `Agents`
- Background documentation jobs run again. The health probe in front of them was measuring the router rather than the runner and read a 404 that is the design as "the runner is unreachable", refusing every job for three days. `MCP`
- The Pull Requests panel no longer reports "Nothing is waiting for you" while a real pull request sits open on GitHub. Listing pull requests reused the credential resolution built for committing, so a project without escalated GitHub write access read its queue from the wrong repository instead of its own. Reading the queue no longer needs write access at all. `Changes`

## NEW - 03.09.2026

### Fixed

- Showcase demos served on the apex path (`docsbook.io/[demo]`) now answer `llms.txt` and `llms-full.txt`, named after the demo rather than the account, and their translated pages open at `docsbook.io/[demo]/[lang]/…` with a canonical that points at itself, so an AI assistant can read and cite every public demo and search engines index its translations instead of following 112 sitemap entries into a noindex 404. `SEO`
- The generated changelog pages can be reached and read. All 21 were orphans with no inbound link and no way out, and three of their links resolved from the docs root while the page sits a level or two below it, so they 404'd. Each page now closes with links to the full changelog, the neighbouring cut and the product page it documents, and each cut has an index. `Changes`

## NEW - 02.09.2026

### Changed

- The setup checklist now opens with an audit instead of an interview: the first step files what is actually wrong with your generated draft as issues you can work through one at a time, rather than asking you what is missing before you have had a chance to find out.

## NEW - 31.08.2026

### Improved

- Reviewing an AI-proposed change in `AI Chat` now shows each file's diff collapsed by default, so a multi-file proposal reads as a scannable list of files first instead of an unbroken wall of diffs, and the card itself now picks up your workspace's own accent color instead of a flat neutral background. `AI Chat`

### Fixed

- Header navigation links on a docs site served at an apex path (like `docsbook.io/docs`) no longer 404 — they used to resolve against the site root instead of the site's own base path, so a link meant for that site could bounce through a subdomain that doesn't exist. `Changes`

## NEW - 30.08.2026

### Added

- Your agent can now ask one question and get a checked answer back. Nineteen scenario tools each answer a single question about your docs — which pages are one edit away from traffic they already rank for (`audit_seo`), why traffic fell and what was ruled out (`diagnose_traffic_drop`), which pages you do not have yet (`find_content_gaps`), whether a change actually worked (`verify_change_impact`), whether answer engines can quote you (`audit_geo`), and fifteen more — each returning a structured answer instead of a paragraph to read. `MCP`
- The public prompt catalog gained two ways to browse them: **Audits & diagnosis**, for the sentences that ask what is wrong and what the fix would cost, and **Background agents**, for the ones that start work you come back to. `MCP`
- The same **Improve** button now sits on every goal in `Goals & funnels` and on each step of a funnel, including beside the note that names where a route breaks, so a number that looks wrong is one click from an explanation of why. `Goals & funnels`
- An open conversation on the `Chat` page now has **Analyze**, which reads the transcript for the turn where it went wrong and separates the three causes that look alike: the answer is not in your docs, it is there and was not found, or it was found and reads badly. `AI Chat`
- An open conversation on the `Chat` page now has **Improve** beside **Analyze**. Analyze reads the transcript for where it went wrong; Improve answers the other question — what to change in your docs so the next reader asking this does not need the chat at all, named at the right layer: a page that should exist, a link that should have connected two pages, or a retrieval problem no rewrite will solve. `AI Chat`
- Six more of them: which numbers you already hold that nobody outside could obtain at any price, and which clear a privacy and contractual gate (`assess_research_assets`); whether a stranger would ever cite one of your pages, and which inbound links now arrive at something broken (`audit_linkability`); which repeated questions reach a person that a page would have closed, ranked by how many *different* people asked (`assess_support_deflection`); which third-party tools readers try to use you with and you never mention (`map_integration_demand`); what an evaluator on a named incumbent cannot find (`assess_competitor_switching`); and what shipped and stayed invisible (`audit_release_adoption`). `MCP`
- Fourteen more scenario tools, one for each method already written in the skills catalog that no tool answered. Why the assistant cannot find an answer that IS on the page (`audit_retrieval`). Which settings are on and doing nothing, checked against the live site rather than the switch (`audit_site_config`). Which pages are really tables served as prose, with the widget from your own catalogue that fixes each (`design_page_widgets`). Which pages the last release made wrong (`diagnose_docs_drift`). `MCP`
- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`
- Forty-two more worked examples in the `MCP` catalog, and ten existing prompts now call one of the new tools where it changes the answer — the unanswered-questions prompt now splits "the page is missing" from "the page exists and nothing can retrieve it", and the striking-distance prompt now says whether the page is simply the wrong shape for the query. `MCP`

### Changed

- `diagnose_intent_mismatch` was being quoted at the wrong price and the wrong wait, because both rate tables matched the bare word "intent" from an older, single-tool rule. It is an agent run and now says so — a caller told to expect a few seconds would have given up on something that takes minutes. `MCP`

### Fixed

- Approving proposed changes in a review card now reliably applies them. The assistant previously had to retype every approved file's full text from scratch to commit it, and on a large batch it could refuse the whole thing rather than risk getting that copy wrong. Approved changes are now committed straight from the proposal you reviewed, so nothing is retyped and nothing is refused. `AI Chat`

## NEW - 22.08.2026

### Fixed

- `www.docsbook.io` now redirects to the apex domain instead of showing a 404. `Marketing`

## NEW - 21.08.2026

### Fixed

- A link copied straight from GitHub's file view now opens on your docs domain instead of 404ing, so pasting `.../blob/main/README` works without hand-editing the path. `Docs`

## NEW - 14.08.2026

### Fixed

- `Start new project` from a workspace subdomain no longer 404s, and the project switcher no longer doubles the organisation in its path. `AI Chat`

## NEW - 10.08.2026

### Fixed

- Plans on `/pricing` could not be bought: the upgrade CTAs dropped the plan you picked, and the two top tiers were sold with the wrong AI budget. `Pricing`
- A repository preview opened on a workspace subdomain returned a 404 when you sent a message. `Draft`

## NEW - 07.08.2026

### Changed

- Each report in `Analytics Explorer` now renders in the shape its data means, so there is no chart-type menu to get wrong, and every row carries an icon you can scan for. `Analytics`

### Fixed

- Switching the doc language from inside a subfolder no longer leads to a 404 page. `Docs`

## NEW - 29.07.2026

### Fixed

- Clicking a page link inside an anonymous draft at `docsbook.io/draft` no longer redirects to a broken `draft.docsbook.io` subdomain. `Preview`

## NEW - 28.07.2026

### Added

- Content health merges the relationship graph, semantic index and findings into one card that names orphan pages, meaning-duplicates, broken links, unread pages and key hubs, each with a concrete next step. `Analytics`

## NEW - 17.07.2026

### Fixed

- A doc URL with different letter casing than the source file now redirects to the canonical URL instead of 404ing. `SEO`

## NEW - 14.07.2026

### Fixed

- Per-page social preview images on client doc sites, previously broken (404) on every page except the repo root. `Social Preview`

## 0.26.5 - 29.06.2026

### Improved

- The "Go to website" link after publishing now waits until your site is actually live, showing a brief "deploying" state instead of opening a page that 404s for the first few minutes. `Publishing`

## 0.22.3 - 30.05.2026

### Fixed

- Fix `/pricing` route returning 404 — now redirects to `/` instead of broken `pricing.docsbook.io` subdomain

## 0.22.1 - 28.05.2026

### Fixed

- Fixed broken navigation on `docs.docsbook.io` alias — clicking any sidebar/inline link returned 404 because cached HTML carried the `/docs/` repo prefix while middleware rewrote it again. Added `x-docs-alias` header in `src/proxy.ts` and routed `basePath` to empty in `src/app/[user]/[repo]/[[...path]]/page.tsx` so links render as `/ai/mcp` instead of `/docs/ai/mcp`. Existing `docsbook-io.docsbook.io/docs/*` paths keep working unchanged

## 0.18.0 - 24.05.2026

### Fixed

- AI Skills cards in the admin no longer 404 on workspace subdomains — clicking a card now opens an in-place modal with the full `SKILL.md` (description, install snippets for 7 AI clients, keywords, MCP tools, GitHub link) instead of routing to `/skills/<name>` which only exists on `docsbook.io`. Landing-page behavior is unchanged

### Removed

- Broken `SearchAction` from the landing JSON-LD — it pointed at `/search?q=`, a page that does not exist, sending a negative signal to Google instead of unlocking the Sitelinks Search Box

## 0.17.4 - 23.05.2026

### Fixed

- Replaced broken `(#)` CTA links across 5 blog posts (`mintlify-vs-docsbook`, `docusaurus-vs-docsbook`, `why-documentation-matters`, `documentation-seo-guide`, `ai-search-documentation`) — all now point to `https://docsbook.io/start`

## 0.16.0 - 22.05.2026

### Fixed

- `/connect` on a workspace subdomain now redirects to `docsbook.io/connect` instead of 404
- `ConnectPage` now redirects to sign-in when the session cookie is present but invalid/expired, preventing a broken `ConnectPicker` state
- Workspace redirect after sign-in always uses `APP_DOMAIN` instead of the request `host` header, preventing wrong subdomain redirects

## Related

- [Full Docsbook changelog](../../CHANGELOG.md) — every release, on every axis
- [Changelogs by outcome](./README.md) — the other eleven numbers a release can move
- [Changelogs by panel section](../README.md) — the same releases, cut by where they landed

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
