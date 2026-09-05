---
title: "What Docsbook has shipped that brings readers back"
description: "Every release that turns one visit into a habit: retention reporting, changelogs readers follow, feeds, and the pages a returning reader comes back to."
---

# What Docsbook has shipped that brings readers back

Everything Docsbook shipped that moves one number: **Repeat readers** — more readers coming back. On this axis, up is better.

One visit is a look; a second is a product someone is actually adopting. This is the Repeat readers slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 05.09.2026

### Changed

- The Pages, Referrers, Devices and CTA breakdown cards now default their ranking to Revenue the moment your workspace can measure it (an Average Product Price and a CTA URL set), instead of Visitors — and both that pick and the analytics period switcher now remember your last choice across visits. `Analytics`

### Fixed

- Feeds opened from a visitor pin (in Users, Analytics, Live or Chat) now shows a real breadcrumb back to wherever you came from, instead of the small × on the filter chip being the only way out. `Feeds`

## NEW - 04.09.2026

### Fixed

- Your MCP call log stops losing the first half of a session. A call that costs nothing is still a call, so `get_info`, `get_workspace`, `list_workspaces`, `create_workspace`, `find_skill` and `find_widget` (what an agent opens a session with) now appear in Feeds and in the tools table against the right project. `Feeds`

## NEW - 03.09.2026

### Fixed

- A project's carried balance survives the monthly rollover again. On 1 September the rollover replaced every carried balance with the retired plans' zero allowance: 399 projects held $200.73 in credit that every metered call refused as insufficient while the balance readout still showed the money. The rollover now keeps what is there (or tops it up to an allowance, if one ever returns), and the AI usage analytics and the MCP `get_ai_usage` card derive that rule instead of restating it, so what the card promises is what a call can spend. `Billing`

### Security

- `list_workspaces`, `get_workspace` and the fifteen `update_*` tools no longer return the raw workspace row. The project's live REST API key is replaced by `hasApiKey`, and the semantic index blob (95% of one answer, 2.1 MB across `list_workspaces`, which clients refused whole) by `hasSourceOfTruthGraph` plus `sourceOfTruthLastIndexedAt`, so an MCP client gets an answer it can act on and no transcript downstream of a call holds a working credential. `MCP`

## NEW - 02.09.2026

### Added

- The `draft_*` tools return the artifact itself — the page, the answer block, the link insertions, the outreach message — as markdown ready to apply, and name the call that applies it. They still write nothing themselves, so the whole family stays safe on a read-only token. `MCP`
- **Generate Issues** asks your assistant to look at the project and file what it finds, after two questions: which stage of work you want to be in — observe, understand, discover, decide, plan, execute, measure, verify, learn, coordinate — and which number you want moved. Asking is the point. With no stage named an assistant returns things to *build* every time, and a backlog with no Measure or Verify in it belongs to a team that never finds out whether the last thing it built worked; the pair you pick also selects the agents that already cover it, so the issues come from this project's own evidence rather than from general advice. `Issues`

### Changed

- Admin settings now open as a page everywhere on a documentation site — the settings gear, the account menu's settings rows and the language picker's "Activate languages" all navigate to the dashboard instead of throwing a full-height panel over the docs. An anonymous draft keeps its own page, so its unsaved work survives the trip. `Changes`

## NEW - 30.08.2026

### Added

- Five **collectors** in `MCP` hand back the evidence an audit is built on, without the opinion, at **$0.0040** a call against the audit's $0.25. `collect_page_text` fetches your live pages and reports what the wire actually serves — status, title, headings, and how many words survive with no JavaScript — beside the size of the source stored for the same path. `collect_corpus_map` maps every page with its size, depth and whether navigation reaches it. `collect_assistant_questions`, `collect_traffic` and `collect_onsite_search` return what readers asked, how their visits ended, and what they typed into your search box. `MCP`
- That makes the cheap one the right one more often than it sounds. With no Search Console connected, `audit_seo` still charges a quarter of a dollar to score its ranking axes as unmeasured, while `collect_corpus_map` needs no search data, no traffic and no history and returns real rows on a site that went up this morning. `MCP`
- Your agent can now ask one question and get a checked answer back. Nineteen scenario tools each answer a single question about your docs — which pages are one edit away from traffic they already rank for (`audit_seo`), why traffic fell and what was ruled out (`diagnose_traffic_drop`), which pages you do not have yet (`find_content_gaps`), whether a change actually worked (`verify_change_impact`), whether answer engines can quote you (`audit_geo`), and fifteen more — each returning a structured answer instead of a paragraph to read. `MCP`
- Hovering any line of the `Live` activity feed now offers to hand that one action to the assistant, and what it offers depends on what the reader did. A failed search or a page rated unhelpful gets **Fix it** — what in your docs caused it and what to change. A copied code block, a thumbs-up or a search result opened gets **Do more**, which works out what earned it and names the pages it is missing from. Everything else gets **Analyze**, for what that reader is doing and whether any of it needs you. `Live`
- Hovering a point on the traffic chart now offers **Analyze** beside the date, which accounts for that one hour or day: whether it is unusual at all against the days around it, and what a spike was actually made of, a crawler and a launch being identical in a visitor count. The chart is now reachable by keyboard as well, with the arrow keys walking between points. `Analytics`
- The `SEO`, `GEO` and `AEO` cards each gained the same pair, and Analyze reads your live pages rather than the switch: a setting that is on while the markup never renders is exactly what a green Active pill cannot tell you. `SEO`
- **Settings ▸ Chat** now has two model settings instead of one. **AI Visitors Chat Model** is what answers your readers; **Admin & AI Agent Model** is what runs the assistant in your dashboard — the one that reads your analytics, calls tools and edits your docs. Picking a stronger model for yourself and a cheaper one for your readers, or the reverse, is now one choice each. `AI Chat`

### Changed

- `Analytics` no longer counts you and your team browsing your own docs as readers. Every figure that describes an audience — the dead-end rate, the funnel, the breakdowns, the headline and goals — now leaves your own visits out alongside bots. A workspace with no audience yet used to show visits, a bounce rate and a session time that were entirely its owner checking pages after a publish, which is the one reading that feels like a signal and is not. Your visits are not deleted, only kept out of the reader figures. `Analytics`

### Fixed

- The admin assistant no longer tells you the project you have open is not on Docsbook. It could reach that ending while its own tools were returning your pages and your commit history; when it does now, it is caught and the turn continues on the real project by name instead of offering to create the workspace you are already looking at. `AI Chat`
- Large documentation pages no longer fail to render. A page over roughly 250KB could exhaust the renderer's memory and return an error instead of the page; those pages now render with syntax highlighting skipped rather than not at all. `Docs`

## NEW - 29.08.2026

### Added

- Your agent can now hand a whole documentation job to Docsbook instead of doing it itself. `run_docs_analyze`, `run_docs_create`, `run_docs_manage` and `run_docs_automate` run the matching docs-skill on our side, against your workspace, with the full administrative toolset the skill was written for, and return a run id you read with `get_agent_run`. Work that takes minutes no longer has to fit in one request, and an assistant with no other Docsbook tools connected can still get an audit done. `MCP`
- `get_agent_run`, `list_agent_runs` and `cancel_agent_run` report a run's state and live progress, return its report and everything it changed once it finishes, and stop one that is still going. `MCP`

### Changed

- Goals no longer ship a default funnel nobody declared, and the Journey tab now shows the same honest empty state as the rest of Goals until one exists. `Analytics`

## NEW - 28.08.2026

### Added

- The Overview's **Analytics** card now shows visitors with their curve for the week, how many readers are on the site right now, pageviews and AI questions. `Dashboard`
- A **Users** page in the admin panel lists every reader of your docs in one table: where they came from, what they read, which goals they reached and how long each one took them, and what that reader is worth. The same table now backs the User and Journey tabs of Goals, and each language's Translations page. `Analytics`
- Project cards on the Dashboard now show revenue beside visitors once a project has an average product price and a Call To Action URL set. `Dashboard`
- The conversations table and the Journey view now show when a reader completed a goal and what they're worth. `Analytics`

### Changed

- Project cards on the Dashboard now draw a curve of the last 7 days' visitors above the visitor count, so one glance shows which sites are alive. Views, AI questions and when you last opened a project appear on hover. `Dashboard`
- Filtering the feed now offers each facet by name — **Add event**, **Add visitor**, **Add goal**, **Add status**, **Add destination**, **Search payload** — instead of one **Add filter** button that kept the choices a click out of sight. `Feeds`
- The Journey view now leads with when each goal was reached — with a quick timeline of what led up to it — instead of listing every goal reached. `Analytics`
- The Analytics Visitors tile, its chart and every breakdown ranked by visitors now follow your workspace's own accent colour instead of a fixed blue. `Analytics`

### Improved

- Reader avatars are now far less likely to give two different readers the same colour. The palette was built for eight chart series and collided constantly across a 25-row table; the colour is now generated per reader, and hard-to-tell-apart pairs drop from roughly 4% to under 2%. Affects `AI Chat`, `Analytics` and the Journey tab. `Analytics`

### Fixed

- The estimated **Savings** figure in `AI Chat` now subtracts what those conversations actually cost to run, instead of ignoring your real spend — a workspace with real chat activity no longer sees it read as $0. `AI Chat`
- Filtering `Feeds` by a visitor now finds that reader's events. It searched only the events your docs dispatched — nearly all of which belong to the project rather than to any one reader — and answered "Nothing matches this filter" about readers who had been active all along. It now searches what that reader did on the site as well, across the whole window rather than the most recent few hundred events. `Feeds`
- The tabs of a card you cannot use yet now switch. On a plan you have not bought, and in the signed-out preview, a card is shown over sample figures with the offer laid over it — but its own tabs were dead, so `Analytics` ▸ Goals showed one of its four views and hid Funnel, User and Journey behind a control that did nothing. Each view has its own sample data and can now be looked through before you decide. `Analytics`

## NEW - 26.08.2026

### Fixed

- The settings panel and chat no longer open automatically over a fresh `/draft` or a `?preview=true` visitor's own site — they're one click away on the gear icon, and the guided tour still starts the first time you open it. `Preview`

## NEW - 24.08.2026

### Fixed

- Cards that had nothing to show a signed-out visitor are now filled with sample data instead of an error or an empty state — goals and funnels, the commit list, chat conversations and their transcripts, repository folders, navigation and social links, and every language page. `Preview`
- Sample figures shown to a signed-out visitor are blurred everywhere they appear, including the commit list and chat sidebar, so invented numbers can never be read as a site's real ones. `Preview`
- Opening an MCP tool or a skill no longer hides its catalog for the rest of the session — the breadcrumb goes back, and a failed catalog load retries when you reopen the page. `Agents`
- Plan names no longer appear to visitors who have no account, on tool descriptions, skill badges or example prompts. `Preview`

## NEW - 23.08.2026

### Added

- Any content widget can now be switched off for a project. Its comments stay in your files and every word between them still publishes; only the rich block is withheld. Switch it back on and every page that used it returns, with nothing to re-write. `Content Widgets`
- `Analytics` now leads with six figures instead of four counts: visitors, revenue, conversion rate, revenue per visitor, bounce rate and session time, each showing how it moved against the period before it. `Analytics`
- The visitors chart now splits new readers from returning ones, and its tooltip carries pageviews, pages per visitor and the returning rate for the hour or day under the cursor. `Analytics`
- `Bounce rate` and `Session time` are now reported per visit, so you can see how many readers arrive and leave without reading, and how long the rest stay. `Analytics`
- Every row of the analytics cards now carries revenue beside visitors, so you can see which pages, referrers, channels, countries, browsers and languages brought the readers who *bought* — not only the readers who came. One click switches all four cards between ranking by `Visitors` and by `Revenue`. `Analytics`
- Hovering a row shows its visitors, revenue, revenue per visitor and conversion rate, with buttons to filter by it or open it. `Details` on each card opens the same numbers as a full table. `Analytics`
- `Pages` and `Headings` can now be ranked by `Views` and `Reading time` as well as visitors and revenue, and each figure counts only what happened on that page — a busy visit no longer makes every page it touched look busy. `Analytics`
- `Feeds` can now filter by a single visitor or by whoever completed a goal — open a reader in `Analytics` and jump straight to everything they did in `Feeds`, or paste in an id by hand. `Feeds`

### Changed

- Visitors with no referrer are now a row of their own, `Direct / None`, instead of being left out of the referrer list. On most documentation sites they are the largest single source. `Analytics`

### Fixed

- Commits stopped showing up in `Changes`. The nightly collector walked only part of the projects it should have, so an active repository could go days without a single new entry while the run reported success. Every project is now collected on every run. `Changes`

### Removed

- The three summary tiles above the `Feeds` feed (all activity, needs attention, failed deliveries) — `failed` moved into `Add filter` under `Delivery status`. `Feeds`

## NEW - 22.08.2026

### Added

- `get_page_diff_impact` returns that same country, language and device breakdown, so an agent can tell a translation-shaped audience from a general rise in traffic. `MCP`
- `Search rankings` now opens with a one-click activation prompt when SEO, GEO and AEO are all off — showing what your rankings will look like and turning any of them on, free on every plan, instead of an empty tab. `SEO`
- The `Feeds` page opens on a digest of the range: all activity, events that need attention, and failed deliveries as three counters, plus a chip per event group with its count — every number is a one-click filter on the feed, and clicking it again clears it. `Feeds`
- `Needs attention` in the `Feeds` digest counts the events where a reader hit a wall — unanswered chat questions, dead-end searches, stale content and translations, usage limits — separately from routine activity. `Feeds`

### Changed

- `Visitor Countries` and `Language Countries` are one card with `Countries` and `Languages` tabs, sitting beside the reader map instead of under it — the same Countries/Languages split used to appear twice on the tab, once as map tabs and once as two separate tables. `Translation`
- The `Feeds` filter menu is a quarter of its old width and picks one facet at a time — events, delivery status, destination or a payload search — with the event list flat and searchable instead of split across nine headings. Each active filter now reads as its facet and count, and clicking it reopens that facet. `Feeds`

### Fixed

- The translation savings, visitor and conversion figures no longer render blurred on a paid plan. `Translation`

## NEW - 15.08.2026

### Changed

- The landing page's feature section now answers the four questions buyers actually ask, in the order they ask them: what the bill can do, what the docs return, whether you can act on that, and what it costs to leave. `Landing`

## NEW - 14.08.2026

### Changed

- Opening the language switcher on your own site before any language is enabled now offers to activate them and takes you to the translation settings, instead of reporting that none are added. Readers of your published docs still see the plain notice. `Translations`

### Fixed

- A visitor reading a preview of a repository that has no workspace yet gets their question answered instead of `Sign in to make changes`. `Draft`
- The draft chat showed the platform's own spending cap as if it were the visitor's. `Draft`
- The AI no longer offers a preview visitor the full 36-card owner library, or a working Account/Invite pair next to the locked one. `Draft`

## NEW - 10.08.2026

### Fixed

- A repository preview opened on a workspace subdomain returned a 404 when you sent a message. `Draft`
- Signed-out visitors editing a preview saw a raw `HTTP 401` instead of an invitation to sign in — and the sign-in button that replaced it was invisible against its own background. `Draft`

## NEW - 08.08.2026

### Changed

- The draft's blue button now says what a click does: `Claim website` while the generated site stands as built, `Save changes` once you have customised it. It was called `Publish`, which named an outcome a visitor without an account could not reach. `Draft`
- The project switcher offers visitors without an account `Claim website` instead of `Sign up to connect a repo`. `AI Chat`

## NEW - 01.08.2026

### Changed

- The docs toolbar's `Ask AI` button is now two icon buttons next to your avatar: `Chat` opens the full AI chat directly with the composer focused, `Editor` arms block-level editing with no chat needed. Pressing the active one returns the page to its normal state. `AI Chat`

### Fixed

- Reopening a past conversation no longer restores it as a chat you cannot see, and the docs toolbar no longer shows `Chat` as active while a plain documentation page is on screen. `AI Chat`

## NEW - 29.07.2026

### Changed

- Prices are no longer hidden from visitors who have not signed up: the full plan comparison is visible in a preview, and picking a plan opens the signup form. `Billing`

### Fixed

- The project picker no longer offers a visitor without an account a "Connect GitHub" action that could not apply to them. `AI Chat`

## NEW - 28.07.2026

### Added

- Seven new analyses answer real business questions: the routes readers walk, where they leak out of a funnel you declare, reverse funnels from successful visits, W1/W4 retention, searches that got results but no clicks, rage signals, and any headline metric plotted over time. `Analytics`
- Translation Activity is now a searchable table of your pages: each row shows whether a page changed in git and whether its translations followed, per language, with a retranslate button on the row. `Translation`

### Fixed

- Visitors, page views, top pages, referrers and events now exclude crawler traffic, which was up to 93% of pageviews on some sites. AI Visits remains the one card that reports bot volume. `Analytics`

## NEW - 27.07.2026

### Added

- Translation activity and spend breakdown. `Translations`
- Re-translate a single page or a whole language on demand, straight from the Translation Activity panel. `Translations`
- Translation Activity now reports how many pages have fallen behind your source content, and how many point at files that were renamed or deleted. `Translations`

### Fixed

- Subscribing now funds the AI budget on your account. Activation credited an unused balance, so a new subscriber could pay and still see an empty budget. `Billing`
- Translation docs no longer claim that pushing to GitHub re-translates changed pages on its own — it does not, and the new Translation Activity panel is how you catch pages up. `Docs`

## NEW - 24.07.2026

### Added

- A public Security & Privacy page explains how visitor analytics avoid PII, don't use tracking cookies, and can never link the same visitor across two different workspaces. `Security`

## 0.26.4 - 12.06.2026

### Added

- Separate credit cards for AI Chat, AI Translations, and Visitor AI Chat usage in admin dashboard — granular view of token spend by feature.

### Improved

- **Buddy mode:** Converted `/buddy` from command to dedicated skill with isolated context — improves modularity and reduces main session token usage.
- Progress bar in credit cards now shows remaining credits instead of usage percentage — better visibility of available budget in `AI Chat Credits` and `Visitors AI Chat Credits`

## 0.26.3 - 11.06.2026

### Fixed

- **Usage attribution:** When a workspace owner uses the docs-chat widget, their token spend is now correctly charged to the "Admin & AI Agent" category instead of inflating the "Readers (AI Chat)" bar — giving an accurate picture of how much visitors actually cost.

## 0.26.2 - 11.06.2026

### Improved

- **Agent daemon:** Token diet for `spawn_session()` — now selects model by priority (P1 → Sonnet, P2/P3 → Haiku instead of fixed Sonnet) and adds bash pre-checks in merger role (skip if PR already merged or base=main). Selective directory copy by role (merger copies only `routines/` + `agents/branch-merger.md` instead of full context).

## 0.26.0 - 11.06.2026

### Fixed

- Agent pipeline `agent:working` lock now released automatically on any session exit (trap on EXIT in nohup subprocess) — no more manual lock cleanup after agent crashes.
- `merger` now finds PRs by branch name `claude/issue-N` as fallback when `Closes #N` body search returns empty — eliminates false NEEDS_HUMAN blocks.

## 0.25.1 - 08.06.2026

### Fixed

- **Docs**: Removed internal operational files (`TWITTER_SETUP`, `outreach/`) from the public documentation sidebar — visitors no longer see private tooling pages

## 0.22.3 - 30.05.2026

### Fixed

- Fix `/pricing` route returning 404 — now redirects to `/` instead of broken `pricing.docsbook.io` subdomain
- Fix `/blog` and `/blog/:path*` returning 500 — now redirects to `docsbook.io/docs/blog` for marketer SEO entry-points
- Fix SEO/GEO/AEO toggles showing "Active" in anonymous mode — toggle now rolls back and shows an inline error when unauthenticated

## 0.22.2 - 28.05.2026

### Changed

- `docs.docsbook.io` and `docsbook-io.docsbook.io` now return `Disallow: /` in robots.txt so search engines index only the canonical `docsbook.io/docs` path

## 0.22.1 - 28.05.2026

### Fixed

- Fixed broken navigation on `docs.docsbook.io` alias — clicking any sidebar/inline link returned 404 because cached HTML carried the `/docs/` repo prefix while middleware rewrote it again. Added `x-docs-alias` header in `src/proxy.ts` and routed `basePath` to empty in `src/app/[user]/[repo]/[[...path]]/page.tsx` so links render as `/ai/mcp` instead of `/docs/ai/mcp`. Existing `docsbook-io.docsbook.io/docs/*` paths keep working unchanged

## 0.21.4 - 26.05.2026

### Chore

- Optimized Claude Code token usage with `claude-token-optimizer`: added Session Start Protocol, filled `.claude/QUICK_START.md`, `.claude/COMMON_MISTAKES.md`, `.claude/ARCHITECTURE_MAP.md` with project-specific content — auto-loaded tokens reduced from ~137k to ~121k

## 0.19.0 - 25.05.2026

### Added

- MCP visitor activity drill-down — two new tools on PRO+ (`get_top_visitors` and `get_visitor_activity`) let AI agents investigate what one specific anonymous visitor actually did end-to-end. `get_top_visitors` returns the most active anonymous visitors with a stable hashed `visitor_id`, pageview count, country, and first/last seen; pass that `visitor_id` to `get_visitor_activity` to get the full chronological event timeline (pageviews, page feedback, CTA clicks) with paths and event-specific details (vote, query, href, heading, …). `get_page_journeys` also returns the same `visitor_id` so journeys can be drilled into immediately. `visitor_id` is `sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0,16)` — stable across sessions for the same person within one workspace, but raw IPs never leave Axiom

## 0.18.1 - 25.05.2026

### Changed

- Bento feature cards on the landing page now link to their corresponding documentation pages instead of `/connect` — `AI Chat` → `/docs/ai/chat`, `SEO Optimization` → `/docs/content/features/seo`, `Web Analytics` → `/docs/analytics/tracking/overview`, `AI Translations` → `/docs/translation/ai-translations`, `User Feedback` → `/docs/content/features/feedback`. Smoother funnel (visitor reads about the feature first) and internal-linking SEO boost

## 0.18.0 - 24.05.2026

### Added

- Ask AI on text selection — when readers highlight a snippet inside the docs, a floating `Ask AI` bubble appears above the selection; one click sends the selected text to AI Chat as a ready prompt. Tooglable per-workspace (Content tab in admin and `show_ask_ai_on_selection` in MCP `update_ui_settings`). On by default. Reduces friction for "explain this paragraph" / "rephrase this" use cases and pushes AI engagement

### Changed

- Replaced legacy "Will the price increase?" answer with a price-lock guarantee for active subscriptions

## 0.17.2 - 23.05.2026

### Added

- `get_doc_graph` now supports `format` parameter: `"toon"` (default) returns a compact text tree ~10x smaller than JSON with `@canonical/ref` syntax that LLMs parse natively; `"json"` preserves the previous full structured response for programmatic clients

## 0.17.1 - 23.05.2026

### Fixed

- Prevent race conditions in monthly usage limits for `AI Chat`, `Translations`, and `Reindex` — concurrent requests could each pass a stale pre-check and push counters past the plan limit (visible as `78/50` pages translated on Pro). Replaced check-then-act with atomic conditional `UPDATE ... RETURNING` in `batchTranslate`, `/api/ai-chat`, and the MCP `reindex` endpoint

## 0.16.0 - 22.05.2026

### Fixed

- `ConnectPage` now redirects to sign-in when the session cookie is present but invalid/expired, preventing a broken `ConnectPicker` state

## 0.15.1 - 22.05.2026

### Added

- Before→After traffic animation in `BentoFeatures` analytics cell — visitors climb from 11 to 1,240 and page views from 34 to 8,900 in a 9-second loop

## 0.11.0 - 16.05.2026

### Added

- Header navigation links now translate to the active language

## 0.10.0 - 15.05.2026

### Fixed

- Subheader links navigate to correct translated pages when translations are active

## 0.3.1 - 09.05.2026

### Improved

- Sidebar folders auto-expand and scroll to active page on nested pages

## 0.2.0 - 08.05.2026

### Fixed

- AI panel no longer returns 403 when toggling DeepSearch/References

## 0.1.1 - 07.05.2026

### Fixed

- Pro plan features now accessible when workspace has an active Pro subscription
- Language switcher now visible to all visitors when enabled, even before languages are added

## Related

- [Full Docsbook changelog](../../CHANGELOG.md) — every release, on every axis
- [Changelogs by outcome](./README.md) — the other eleven numbers a release can move
- [Changelogs by panel section](../README.md) — the same releases, cut by where they landed

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
