---
title: "AI spend changelog"
description: "Everything Docsbook shipped that shows or lowers what the models cost you — usage records, per-call billing, quotas and overage."
---

# AI spend changelog

Everything Docsbook shipped that moves one number: **AI spend** — less money burnt on model calls. On this axis, down is better.

Sees where the model budget actually goes before the invoice does. This is the AI spend slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 03.09.2026

### Added

- Clicking a call in a tool's history opens the whole call: what went in, what came back, who asked for it (your own Run, a connected MCP client, a schedule, an event), how long it took, what it was priced at, and what actually left your balance. The price and the billed amount are shown as two figures on purpose, since a call costing less than a cent is charged and still bills $0.00, and either number on its own misreads. `MCP`
- A **Cost** column on that history, so you can see what a tool has been spending on this project without opening a single row. `MCP`

## NEW - 02.09.2026

### Added

- The `draft_*` tools return the artifact itself — the page, the answer block, the link insertions, the outreach message — as markdown ready to apply, and name the call that applies it. They still write nothing themselves, so the whole family stays safe on a read-only token. `MCP`
- Every tool's page and the tools reference now carry a **per-tool price and wait**: the [MCP tools reference](./reference/mcp-tools.md) lists all 135 with what only that one tells you, what it costs, and how long the call is held open. `MCP`
- The assistant can now read and write that tracker itself — `list_issues`, `get_issue` and `create_issue`, in the admin chat and over your MCP endpoint. Ask it to open an issue, add something to the backlog, or write down what an audit just found, and the finding outlives the conversation instead of ending with it. Filing needs a read-write token; reading does not. `MCP`
- The MCP tools table now carries an **Impact** column: which number each tool works on and which way that number is good news, so you can tell what a tool is for before you spend a call on it. No percentage — one call is a step inside a plan the table never reads, and a figure there would be a forecast rather than a fact. `MCP`

## NEW - 01.09.2026

### Changed

- The account menu's wallet is two plain rows now — **Billing** (opens the same top-up screen) and **Usage** (the per-model spend breakdown) — rather than a standalone balance row and then a bespoke balance card; the sidebar's own low-balance notice is still what warns when a project is running low. `Dashboard`

### Fixed

- The signed-out preview priced a chat conversation at $0.21-$0.41 while the Cost tile above it worked out to about a cent and a half. The rows are the figure an owner multiplies by their own traffic before deciding whether to switch the chat on, and they were eighteen times the truth. `AI Chat`

## NEW - 31.08.2026

### Removed

- The **Usage** button has left the feed's toolbar. The breakdown itself has not moved: **See usage** on the sidebar balance card still opens it. It is about the whole project over a window, while every other control on that row acts on the feed in front of you. `Feeds`

## NEW - 30.08.2026

### Added

- The `MCP` catalog gained a **Probe** billing class for them, priced between Egress and AI, and the filters, the price column and the typical-time column all carry it. `MCP`
- `Analytics` gained a **Spend** figure right of Revenue: what this project's AI actually cost over the period on screen — reader chat, your own chat, translations, embeddings and MCP calls — with a chart of when it was spent and the billed calls behind each point. It needs no setup, it keeps working in a period nobody visited (an overnight translation run is a real bill with no reader behind it), and its arrow stays grey because spend has no good direction. `Analytics`
- Every new project now starts with **$1** of real credit, and a few minutes in a card offers **$5 more** to claim — yours to spend on AI chat, translations, MCP calls or an agent run, with nothing to pay until it runs out. It appears in the sidebar and as a strip across the top of `Billing`, and claiming it is one button. `Billing`
- The sidebar card can be dismissed outright, unlike the low-balance warning beside it, which still only folds to a single row. Dismissing it costs you nothing: the same bonus stays claimable on the billing screen. `Dashboard`
- `Billing` gained **Support us** beside **Add credit** — a monthly amount that tops the same project balance up each month, rather than a plan. It unlocks nothing and gates nothing; every dollar of it lands as credit you spend the same way. Cancel it whenever you like. `Billing`
- Every finding carries the call that would fix it, so an audit hands straight over to `run_docs_create`, `run_docs_manage` or `run_docs_automate` without anyone translating it in between. All nineteen change nothing themselves and work with a read-only token. `MCP`
- The public prompt catalog gained two ways to browse them: **Audits & diagnosis**, for the sentences that ask what is wrong and what the fix would cost, and **Background agents**, for the ones that start work you come back to. `MCP`
- `Feeds` gained a **Usage** button that swaps the live stream for the sum: what this project's money went on over a window, dearest first, as three tables — every AI answer, translation and indexing run by model, every MCP tool call by tool, and every event by type. A price on one row at a time was never a column anybody could add up. `Feeds`
- Pick a window of **24 hours**, **7 days** or **30 days**, and export what you are looking at: the breakdown itself as a spreadsheet, with each line's cost as a number you can sum and a column saying whether it was charged, or the raw events behind it bounded by the same window. `Feeds`
- **See usage** on the balance card in the sidebar now opens that breakdown. It used to open the billing screen, which answers a different question with the same word: a balance says how much is left, never what took it. **Top up**, beside it, still goes to billing. `Dashboard`
- Every prompt in `Prompts` now shows what one run is worth, in a **Cost** column: the MCP calls it makes plus the model turns around them, so a prompt costing a fraction of a cent is told apart from one costing a quarter of a dollar before you put it on an hourly schedule. `Prompts`
- Beside it, an **Impact** column says what running it typically moves and which way — support load, upkeep hours, manual watching, time to an answer, citations, markets, traffic, conversion — green for up and red for down, where down is the good one on anything that costs you. `Prompts`
- Both are estimates of what prompts of that kind do, and both say so when you hover them: neither is a reading off your own workspace, and the cost hover breaks the figure into the calls and the turns it is made of. `Prompts`
- All three pickers offer more models, cheap to expensive — GPT-4.1 nano, DeepSeek V3, Gemini 2.5 Flash and Pro, GPT-4.1 and Claude Opus 4.1 join the list, each with its price per 1M tokens beside it. `AI Chat`
- **Usage** is now a row in **Settings**, so what the project spent — AI calls, MCP calls and logged events, over 24 hours, 7 or 30 days — is somewhere you can go and look, rather than only a button inside `Feeds` or a link on a low-balance warning. `Billing`
- `assess_content_roi` is the one that gives you permission to stop: which pages earn their upkeep, and which to merge, redirect or retire. It works out which low-traffic pages are protected by inbound links or assistant citations **first**, and never proposes retiring one of those — deleting a page something external points at spends a link profile that cannot be bought back. `MCP`
- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`

### Changed

- The `Chat` page now leads with the two questions you open it with: what the assistant brought in, and what it cost. **Revenue** is what the readers who used it are worth, counted once per reader on the same scale `Goals & funnels` uses, with the tooltip keeping "reached your goal" apart from "part-way there". **Cost** sits beside it in red — what the chat actually billed, from the ledger, over the same window rather than a fixed week. `AI Chat`
- **Savings** keeps its place after them, because support cost avoided is worth seeing and is not the same money as either. It now says on its own tile that it is an estimate standing next to two measurements. The old **Earned** tile, which counted link follows rather than money, has gone; those clicks are still on the conversation rows. `AI Chat`
- The conversation table now opens with **Potential** and **Cost** ahead of **Time**, instead of at the far right behind six other columns where a narrow panel had to be scrolled to reach either. Potential is green, with the money reading it carries. `AI Chat`
- The billing filters on the `MCP` tools list now lead with **Agent** instead of with the cheapest class. The strip scrolls sideways, so at most window widths its tail was off-screen — which put the one family that runs a whole job and hands you back a report where nobody saw it. Sorting the table by billing is unchanged. `MCP`
- The seven billing filters on the `MCP` tools list are now one **Filters** button, the same control the `Prompts` toolbar carries. Six of them were switched off at any moment while taking the room that **Run now**, **Schedule** and **On event** now have; whichever classes you turn on stay on the line beside the button, each with its own way out, and the menu still prints each class's price. `MCP`
- Hovering a tool on that list now opens a card with everything its own page used to say: what it does, the price per call, the typical wait, how many arguments it needs and how many of them are required, how many worked examples call it, and — for your own project — what it has cost you and when it last ran. The callable id sits in it, ready to copy. `MCP`
- Your project's balance now has a row of its own at the bottom of the sidebar, with the amount spelled out in money and a **Top up** button on it, and pressing anywhere on the row opens the top-up screen. It used to be a small dial carrying no figures at all, whose numbers appeared only on hover — which a phone cannot do. `Billing`
- The account menu now opens on the wallet: what is left, what has been spent, **Add credit** and **Pricing**, above everything else in the menu. Billing used to be a row fourth down a list of links, shaped exactly like the changelog and documentation links either side of it. `Billing`
- The `Docs assistant` card's eight tabs (Topics, Why they came, Searches, Lang, Links, Outcome, Feedback, Coverage gaps) each carry their own **Enable** now too, the same way every other tab on `Analytics` does, in place of one button covering the whole card. A workspace with plenty of outbound clicks and nothing yet on Coverage gaps meets the guide there and nowhere else. `Analytics`
- MCP calls are now charged to the balance of the project the call is about — the same balance a top-up funds. They were previously metered against your profile, which nothing tops up, so paying credited a row the billing never read. `MCP`
- Running out of balance now names which project ran out, what the call costs, what is left, and where to top that project up, instead of offering a tier to buy or a monthly reset to wait for. `MCP`
- MCP spend now appears as its own row in `Spend by source`, so the balance no longer drops further than "spent" can account for. `Dashboard`
- The `Tools` column in `Prompts` is now off by default too, alongside `Tags`. The chips named which endpoints the agent would reach for, and both questions you actually decide on — the price and the payoff — are computed from that same list, with the cost hover naming the dearest thing the prompt touches. Every tool is still listed in the row's card, and the column is one click away in **Columns**. `Prompts`

### Fixed

- `Outcome` on that card no longer reports a window with no conversations as `Answered 0 / Dead end 0 / Unrated 0`. Three zeros read as three measured failures; nothing measured now says so. And `Coverage gaps` says plainly when it is empty because nothing dead-ended, which is the best reading it has, instead of offering to fix a working assistant. `Analytics`

### Improved

- A scenario tool run now starts with exactly the tools its method needs already loaded, instead of spending its first round trips discovering them. Each of the 45 capabilities declares what it may call, the run is held to that declaration, and a capability that never said it goes outside your site does not go outside it. `MCP`
- The `MCP` tool table's search box and billing-class filters now stay on one line at every width, instead of the chips dropping onto a second row above the table. `Dashboard`

## NEW - 29.08.2026

### Added

- Feeds now logs every MCP tool call made against your project alongside the project's own events, showing which tool an agent called, whether it worked, how long it took and what it cost, and filterable by the call's billing class. `Dashboard`

### Changed

- The admin panel's MCP section is now one searchable, sortable table of every tool with its billing class and how much of your monthly allowance it buys, instead of a picker column showing one tool at a time. Tools you can compare are tools you can budget for. `MCP`

## NEW - 28.08.2026

### Added

- The AI budget now names the one way to remove its ceiling: on Business you run the AI on your own OpenRouter, OpenAI, Gemini or Anthropic key, and pay us nothing for tokens. `Limits`
- The MCP server now offers a semantic `search` tool that finds documentation by what it means rather than its exact wording, reusing the workspace's existing vector index at no extra indexing cost. `MCP`
- The admin panel's sidebar now warns you before your AI allowance runs out: a small card above **Getting started** showing the share left, when the cycle resets, and a way through to your usage or a plan. It appears at a quarter left, again at a tenth, and once more when nothing is left, and closing it keeps it quiet until one of those actually happens. `Limits`
- That page now also shows what a language cost beside who it reached: spent, saved, reused from cache and converted readers, on the same tile row as the audience figures. Reader counts alone cannot say whether a language paid off. Every tile in both rows explains itself on a `?`. `Translations`
- A language's Translations page now shows what its readers were worth as an **Earned** tile, priced from your Call To Action and Average Product Price, next to spend, savings and cache reuse. `Translations`

### Changed

- The admin panel's sidebar now shows which plan the project is on next to a bar for how much of this cycle's AI allowance is gone. The exact spend, in dollars, and the days left before it resets are on hover. `Dashboard`
- The Conversations table now shows one line per row, with a reader's country and device as icons beside their name and the site that referred them shown with its own favicon. Cost and Savings are their own columns, the topic column is labelled Topic, and a Time column shows how long the conversation ran and how long that reader has spent on your docs. `AI Chat`
- **Spend by source** is now one row per source — its name, what it has spent, one bar and one percentage — instead of four coloured tiles, and every source is listed whether or not it has spent anything, so you can see where money can go before it goes there. Colour now means only one thing: amber as a source nears its own limit, red once it reaches it. `Limits`
- The Users table's **Spent** column is now called **Revenue**: in a panel of cost readouts the old name read as what a reader had cost you rather than earned you. An estimated figure is now labelled `est.` instead of carrying a leading `~`, which in a column of dollar amounts looked like a minus. `Analytics`
- A language's sync state, coverage, source commit and any halt reason now live in a popover on the state chip, next to the switch and **Translate now** on one line. The 200px card that held them pushed "did this language pay off" below the fold. `Translations`
- Each commit in a language's commit ledger now also shows what translating it into that language cost and which AI model did the work, next to the author's GitHub avatar. Opening a page's patch now says whether you are looking at the source revision or the translation. `Translations`
- Every locked feature across the admin panel now shows as a soft, see-through preview of the real thing with one button that unlocks it, in place of blurred figures and padlock overlays. `Billing`
- The pricing tab now opens directly on the plan comparison, with your seat status and trial countdown shown there instead of in a separate card, and Usage and Contact Support one click away. `Pricing`

### Removed

- The **Webhooks** card is gone from Usage. It counted your webhooks against a limit that no longer exists. `Limits`
- A language's cost row no longer ends on a bare count of converted readers — see the **Earned** tile above. `Translations`

### Fixed

- Your plan now shows in the admin panel's sidebar even when there are no usage figures to draw a bar from. `Dashboard`
- The estimated **Savings** figure in `AI Chat` now subtracts what those conversations actually cost to run, instead of ignoring your real spend — a workspace with real chat activity no longer sees it read as $0. `AI Chat`

## NEW - 25.08.2026

### Changed

- Upgrading now opens checkout inline on our own domain instead of a new tab. `Billing`

### Removed

- The "$X of AI usage / month" line is gone from every plan's feature list on the pricing page — the AI budget itself is unchanged, only the copy. `Pricing`

## NEW - 24.08.2026

### Changed

- The plan table now opens on annual billing and quotes every column per month, so the cheaper option is the one that reads cheaper. `Pricing`

## NEW - 23.08.2026

### Added

- Every commit in `Changes` now carries one 0-100 score, with the four areas behind it: readers served, reach, cost to run and edit quality. Each area shows its own number, how much of the total it counts for, and how much data stands behind it. `Changes`
- `Changes` now puts the cash figures up front: what re-translating the edited pages cost, what readers asking the chat cost either side of the commit, and total AI spend. `Changes`
- Your docs now follow your commits: on the `Auto` translation mode, a push that changes a page re-translates it in every enabled language without being asked, within your existing budget and provider limits. `Translations`
- Every language page opens on whether that language is keeping up — coverage split into current, fallen behind and never translated, when it was last written to, and which commit your docs stand at. `Translations`
- Each language can be switched on and off from its own page, with the same cost confirmation you get in settings. `Translations`

### Changed

- The `Limits` tab is now called `Usage`. `Usage`
- `Changes` opens on the answer instead of on the charts. The score, what moved and what it cost come first; every measurement behind them is one `The measurements behind this score` toggle away, with nothing removed. `Changes`

### Removed

- Overage billing. AI usage now simply pauses once the plan's monthly budget is used up — never billed above your plan price. `Usage`

## NEW - 22.08.2026

### Added

- Every commit in `Changes` now shows what it cost: AI spend for the week before and the week after in dollars and percent, the share readers' own questions account for, cost per visit, and what re-translating the edited pages cost — with the sections served free from cache priced out. `Changes`
- A new `Dialogs` card lists every AI chat conversation individually — topic, funnel stage, answered/dead-end status, and estimated savings — open one to read the full exchange, its real cost, and how it compares to the topic's usual answer rate. `AI Chat`
- Each conversation in `Dialogs` now shows what it actually cost to run, right next to its estimated savings. `AI Chat`
- Every language you translate into now has a page of its own under `Translations` — pick it from the sidebar to see how many readers arrive from that language's countries in the first place, how many of them actually read in it, where it landed and where it missed, what they read, and what the language has cost against a human translator. `Translation`
- The `MCP` page marks the four tools a client can reach with no token at all, so you can see what a reader of your docs could call, not just what you can. `Agents`
- `Needs attention` in the `Feeds` digest counts the events where a reader hit a wall — unanswered chat questions, dead-end searches, stale content and translations, usage limits — separately from routine activity. `Feeds`

### Changed

- Every row in the `Conversations` card (topics, buying stage, coverage gaps, feedback) now opens straight into `Dialogs`, pre-filtered to that group. `AI Chat`
- The sidebar's plan usage meter is now clickable anywhere on the card, not just the `Manage` link, and highlights on hover to show it. `Billing`

### Removed

- The `AI Usage` and `Chats Analysis` cards — the numbers now live inside `Conversations` and the new `Dialogs` card. `AI Chat`

## NEW - 15.08.2026

### Changed

- The landing page's feature section now answers the four questions buyers actually ask, in the order they ask them: what the bill can do, what the docs return, whether you can act on that, and what it costs to leave. `Landing`

## NEW - 14.08.2026

### Changed

- The landing page's first screen states what Docsbook is and what it costs. `Landing`

### Fixed

- The draft chat showed the platform's own spending cap as if it were the visitor's. `Draft`
- A new workspace can use its free AI budget straight away instead of hitting an empty-balance notice before its first question. `Billing`
- The Limits panel no longer reports a brand-new wallet as out of budget. `Billing`

## NEW - 10.08.2026

### Fixed

- `Upgrade plan` did nothing when clicked on a chat with no project selected. `Billing`
- Plans on `/pricing` could not be bought: the upgrade CTAs dropped the plan you picked, and the two top tiers were sold with the wrong AI budget. `Pricing`

## NEW - 08.08.2026

### Added

- Enabling a language now asks you to confirm, showing how many pages will be translated, the estimated cost and your remaining budget. When the run does not fit, it says what share of your docs the budget covers and offers the upgrade. `Translations`

### Fixed

- AI spend is billed at the rate your plan states. A rounding floor inflated the cost of small requests. `Billing`

## NEW - 07.08.2026

### Added

- Per-source spend limits let you cap what one source may spend each cycle, so AI translations or the semantic index can never eat the whole budget. Each bar under `Spend by source` now shows your limit next to the plan's own. `Limits`
- A `recommendations` widget renders a marked list of findings as cards, ranked by how much each one is costing you. `Docs`

## NEW - 29.07.2026

### Improved

- Every paid feature in the plan comparison now carries a question-mark tooltip explaining what it buys your business, in plain language rather than capability names. `Billing`

### Changed

- Prices are no longer hidden from visitors who have not signed up: the full plan comparison is visible in a preview, and picking a plan opens the signup form. `Billing`

### Fixed

- Long feature explanations in the plan comparison no longer get cut off at the edge of the Business column. `Billing`
- The feature unlock cards no longer advertise plans and features that do not exist: there is no "Starter" tier, DeepSearch was removed long ago, and Custom Questions is free on every plan rather than Pro. `Billing`
- Unlock cards now quote the real numbers instead of stale ones: your monthly AI budget in dollars rather than a query count, 15 supported languages rather than "50+", and the actual chat model and MCP tool counts. `Billing`
- Extra usage is now described the way it is actually billed, in dollars against your monthly spend limit, instead of a per-query price that was never charged. `Billing`
- Paywall messages now name the tier you can actually buy, "Pro", instead of a "Pro+" plan that is not on the price list. `Billing`

## NEW - 28.07.2026

### Removed

- The separate AI Spend card is gone from the AI Chat tab. What the assistant cost you now sits as an expandable line at the bottom of `Conversations`, so the tab leads with what the chat did for your business rather than what it billed. `AI Chat`

### Fixed

- Free workspaces no longer see a "credit almost gone" warning on their very first visit, before spending anything. `AI Chat`

## NEW - 27.07.2026

### Added

- Paid plans no longer hard-stop when the monthly AI budget runs out — usage continues as metered overage billed on top of the subscription, up to a monthly cap you set yourself (default $20/month) from the Limits tab in workspace settings. `Billing`
- Annual billing (20% off) is now wired end-to-end through checkout for Pro, Business, Growth, and Scale — the toggle appears in the pricing tab once Paddle annual prices are configured. `Billing`
- Per-model AI spend view showing what each call cost at the provider's real price. `AI Chat`
- Translation activity and spend breakdown. `Translations`
- Per-language coverage shows, for every page in your docs, how many are translated and current, how many are behind, and how many have no translation at all — so you can tell at a glance whether a language is genuinely complete. `Translations`
- Filling in a language translates only the missing and outdated pages; pages already up to date are skipped and cost nothing. `Translations`
- Live progress while a translation run is going, including why a run stopped early when it hits your budget or the provider's quota. `Translations`
- Translation spend is now shown next to how many page sections were reused from cache instead of re-translated. `Translations`

### Changed

- One subscription now covers several projects through project seats instead of being bought per workspace. `Billing`
- AI usage is measured in money rather than tokens, so your plan's monthly allowance and every charge are shown in dollars. `Billing`
- Every paid plan now includes an AI budget equal to its price: Pro gives $59 of AI usage a month, Business $159, Growth $349, and Scale $899. `Billing`
- AI usage is now charged at the provider's real model price plus 150%, replacing the previous 20% markup. A Pro budget covers roughly 15,000 answers a month on the default model, and switching to a cheaper model makes it go further. `Billing`

### Fixed

- Subscribing now funds the AI budget on your account. Activation credited an unused balance, so a new subscriber could pay and still see an empty budget. `Billing`
- Documentation corrected across pricing, plans, AI chat, API, and analytics pages, which still described token budgets, per-workspace billing, and analytics windows that no longer match the product. `Docs`

## NEW - 24.07.2026

### Added

- Two new plans: Growth ($349/month) and Scale ($899/month), for teams that want deeper analytics, conversion tracking, and workflow features on top of the existing plans; annual billing on any paid plan now gets a 20% discount. `Pricing`

### Removed

- The discontinued one-time lifetime plan is no longer offered anywhere, including in AI chat upgrade prompts. `Billing`

## NEW - 18.07.2026

### Changed

- AI chat is now available on every plan, including Free — plans differ by the monthly AI token budget, not by a feature switch. `AI Chat`

### Fixed

- Monthly AI token budgets now reset correctly at the start of each billing period. `Billing`

## NEW - 06.07.2026

### Added

- Optional `auth_header` field when registering a webhook, sent verbatim as the `Authorization` header on every delivery — for receivers that require their own bearer token. `Webhooks`

## NEW - 05.07.2026

### Added

- New `Business` plan — everything included in `Pro`, with higher AI chat, translation, and webhook limits. `Billing`

### Changed

- `Pro+` renamed to `Pro`; the one-time `Lifetime` plan is no longer sold (existing lifetime customers are unaffected). `Billing`
- Upgrade page no longer shows specific AI-queries-per-month numbers that had drifted out of sync with actual limits. `Billing`

## 0.26.4 - 12.06.2026

### Added

- Separate credit cards for AI Chat, AI Translations, and Visitor AI Chat usage in admin dashboard — granular view of token spend by feature.

### Fixed

- Zero credits shown for newly created workspaces in `Token Budget` — `ensureWorkspace` now seeds the initial monthly token balance on creation.

### Improved

- **Buddy mode:** Converted `/buddy` from command to dedicated skill with isolated context — improves modularity and reduces main session token usage.
- Progress bar in credit cards now shows remaining credits instead of usage percentage — better visibility of available budget in `AI Chat Credits` and `Visitors AI Chat Credits`

## 0.26.3 - 11.06.2026

### Fixed

- **Limits card:** "Usage by source" bars now show each category's share of *actual spend* instead of a tiny fraction of the full budget ceiling — so you can see at a glance where your tokens go (AI Chat readers vs. Admin vs. AI Translations) and what to optimize.
- **Usage attribution:** When a workspace owner uses the docs-chat widget, their token spend is now correctly charged to the "Admin & AI Agent" category instead of inflating the "Readers (AI Chat)" bar — giving an accurate picture of how much visitors actually cost.

## 0.26.2 - 11.06.2026

### Improved

- **Agent daemon:** Token diet for `spawn_session()` — now selects model by priority (P1 → Sonnet, P2/P3 → Haiku instead of fixed Sonnet) and adds bash pre-checks in merger role (skip if PR already merged or base=main). Selective directory copy by role (merger copies only `routines/` + `agents/branch-merger.md` instead of full context).

## 0.26.0 - 11.06.2026

### Added

- `LimitsCard` in admin dashboard — unified token budget view with per-workspace usage breakdown.

## 0.22.0 - 28.05.2026

### Changed

- Replaced the admin Source of Truth card in `src/components/mcp/SourceOfTruthControls.tsx` — the reindex usage counter (`/100`) and Reindex button are gone, replaced by a promo card with the install command and a link to the docs-claude-plugins repository

## 0.21.4 - 26.05.2026

### Chore

- Optimized Claude Code token usage with `claude-token-optimizer`: added Session Start Protocol, filled `.claude/QUICK_START.md`, `.claude/COMMON_MISTAKES.md`, `.claude/ARCHITECTURE_MAP.md` with project-specific content — auto-loaded tokens reduced from ~137k to ~121k

## 0.18.0 - 24.05.2026

### Added

- New opinion blog post `/blog/notion-for-docs-engineering-lessons` — first-person engineering essay on why Notion stops working as a docs system once docs leave the building (SEO surface vs internal wiki, version control drift, multilingual coupling, AI crawler discoverability, performance budget, export lock-in, wiki-vs-docs permission split) with a soft Docsbook pitch in the closing section; written for SEO ("notion for documentation") + outreach + objection handling
- New blog comparison post `/blog/gitbook-vs-docsbook` — honest 2026 head-to-head against GitBook (~1900 words) covering TL;DR matrix, four reasons teams leave GitBook (per-editor pricing, vendor lock-in, migration cost, AI as commodity), side-by-side feature table, pricing math for three team sizes (solo / 5-person / 20-editor mid-market), 7-step migration path, an honest "when GitBook is the better choice" section, and a 6-question FAQ — targets the "GitBook alternative", "GitBook vs Docsbook", and "GitBook pricing 2026" SEO queries

## 0.17.2 - 23.05.2026

### Fixed

- Paginate MCP `get_doc_graph` to avoid hitting the MCP response token limit on large repos (previously a single 110k+ character JSON line blew past the limit and made the tool unusable in Claude). Added `page`/`page_size` (default 50), `path_prefix`, `include_headings`, `include_relations`, and `include_github_urls` flags; relations are only emitted on `page=1` to save bytes

## 0.17.1 - 23.05.2026

### Fixed

- Prevent race conditions in monthly usage limits for `AI Chat`, `Translations`, and `Reindex` — concurrent requests could each pass a stale pre-check and push counters past the plan limit (visible as `78/50` pages translated on Pro). Replaced check-then-act with atomic conditional `UPDATE ... RETURNING` in `batchTranslate`, `/api/ai-chat`, and the MCP `reindex` endpoint
- Roll back the reserved reindex slot when `fetchAndIndexRepo` fails so transient errors no longer eat the monthly quota

## 0.17.0 - 23.05.2026

### Changed (previous)

- Add a Pro+ badge next to `Reindex Usage` that opens the Source of Truth promo modal on click

## 0.16.0 - 22.05.2026

### Changed

- Rework billing model — Pro is now $150 lifetime one-time payment, Pro+ replaces Enterprise as $29/mo subscription with white-label and Source of Truth
- Existing `pro` workspaces (legacy $29 one-time) grandfathered as lifetime Pro at no extra cost

### Added

- Subscription management UI in `FloatWidget` pricing tab — shows current plan, subscription status, next billing date, and Manage subscription button linking to Paddle Customer Portal (Pro+ only)
- `pricing-spec.md` in `docs/content/setup` — source of truth for the new billing model

## 0.2.3 - 09.05.2026

### Improved

- Translation tab layout — usage card moved above country stats

## 0.2.0 - 08.05.2026

### Added

- Per-plan monthly translation quotas with usage tracking and progress bar

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
