---
title: "What Docsbook shipped that lifts conversion on docs"
description: "Every release that gets more readers to do the thing a page was written for: goals, funnels, calls to action, pricing clarity and the paths between them."
---

# What Docsbook shipped that lifts conversion on docs

Everything Docsbook shipped that moves one number: **Conversion** — more readers doing the thing the page was for. On this axis, up is better.

Readers who came to learn and left having started — the docs' real job. This is the Conversion slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 19.09.2026

### Added

- **`cards icons=inline`: the bordered card without the grid-paper band.** The icon sits in a small tile at the top of the body, so a hub of twelve doors is twelve icons over twelve titles rather than twelve grey rectangles, and a reader scans it in one pass. Combines with `horizontal` and `cols=`. `Content widgets`

### Improved

- **Adding credit now opens Paddle's checkout directly**, instead of landing on a page that asked which amount before it could get there. `Billing`

### Changed

- **The trial banner's "Upgrade plan" button now opens the Plan tab**, so you see the Pro/Enterprise choice before committing to either, instead of a checkout window opening straight away. `Billing`

### Removed

- **The "How the AI is billed" mechanics card is gone from the Plan screen.** It restated the trial, the allowance and the overage cap in a paragraph beside cards that already say each of those in fewer words. `Billing`

## NEW - 18.09.2026

### Added

- **A new organization starts with 14 days of Pro**, and that is one trial per account, ever. A second organization is created on Free, and the dialog says so before you click rather than after — so nobody plans a week of evaluation around a trial that was already spent. `Pricing`
- **Three new built-in feeds: Content gaps, Conversions, and Plan & usage.** Content gaps is where the assistant came up empty or a search returned nothing — the fastest signal of what your docs are missing. Conversions is every click that took a reader toward your product. Plan & usage is every plan change and usage-limit warning the workspace crossed. Content gaps and Plan & usage can each carry an alert, so you can get pinged in Slack or Discord the moment a reader hits a wall or a teammate nears a spend limit, instead of noticing it days later in the feed. `Feeds`
- **Billing has a settled home: Settings → Plan.** The same plan comparison and balance the Pricing tab shows, one tab away from Usage and Profile instead of a separate menu. `Pricing`

### Changed

- A project is now on the best plan it can reach — its own, its team's, or its owner's — so moving a site into a team that pays for Pro switches the paid capabilities on without buying anything again. `Pricing`
- **Paste as many addresses at once as you like** when connecting a source, one per line, with a preview of where each one will be filed before you commit. A project's docs are written from its repository *and* its pricing page *and* its API reference, and connecting them one dialog at a time is how a source list ends up with a single row in it. `Integrations`

### Fixed

- Making a documentation site private — behind a shared password or your own Google Workspace, Entra ID or Okta sign-in — is available on every plan, and the MCP tool that does it no longer tells you it needs an upgrade. It had been saying so after the gate came off, which sent people to a checkout for something their project already had. `Pricing`

### Removed

- **Upgrade project** and **Open documentation** are gone from the project switcher. The first named the wrong thing now that a plan is bought for you or for your team rather than for whichever project you happen to have open, and it opened the pricing tab that is one click away in the same panel; the second was a link out to a website inside a menu whose whole job is taking you to another of your projects. Creating a project, creating a team and moving this project into one took their place. `Organizations`

## NEW - 15.09.2026

### Added

- AI and search crawlers now draw on a monthly crawl budget instead of being served for free: every plan includes crawls at no cost (5,000 on Free, 100,000 on Pro, 500,000 on Enterprise), and anything past that is billed at $0.30 per 1,000 pages, so what a bot costs you when it walks every page in every language is a figure you can read and cap rather than an unexplained line on someone else's hosting bill. A reader that ChatGPT or Perplexity sends you is never counted as a crawl. `Pricing`
- Cards can now carry a **New**/**Beta** pill beside the title and a row of short tags under it, and their arrow can be set to appear only on hover — so a reader evaluating your models, plans or editions picks the right one straight off the grid instead of opening three pages to tell them apart. `Content`
- Three more blocks for a page that has to OPEN a site rather than continue one. A **hero** leads with the page's own heading, a lead line, a row of quick links and one prompt a reader can hand straight to their AI agent, so a first-time visitor either finds the three doors that matter or delegates the whole setup without reading a guide. A **showcase** gallery makes a screenshot the tile, so the customers and examples a landing page has to SHOW stop being described in a bullet list. And a **journey** lays a product's stages out side by side, so a reader can see which one they are in instead of scanning an index sorted by subsystem to guess. Between them a front page finally looks like your product rather than like the table of contents of a manual, and a reader evaluating you sees the customers you have instead of a bullet list claiming them. All three are ordinary markdown between two invisible comments, so the same file still reads correctly on GitHub. `Content`
- **The same tool now answers how the WORK is done, not only how the product works.** Ask `docsbook_assistant` how a page for a given search intent should be structured, what a quickstart owes its first screen, or what a passage needs before ChatGPT or Perplexity will quote it whole, and the answer comes back from Docsbook's own documentation handbook with the pages it drew on — so the shape of your page is something you can defend to whoever asks, instead of whatever your agent happened to believe about documentation. `MCP`
- **Three commands start the whole loop from one sentence about where you want the business to go**: `goal` to begin, `next` to pick the work up again, `learn` to go back and judge a change that shipped a fortnight ago. In a client that shows MCP commands they appear beside the tools, so nobody has to remember the order documentation work goes in or notice for themselves that a measurement fell due. `MCP`

### Changed

- **The free trial no longer expires.** Every new project still starts on Pro with a free AI wallet, but there is no fourteen-day clock on it any more: the project runs until that wallet is spent, however long it takes, so an evaluation you put down for three weeks is still there when you pick it up instead of having gone dark while nobody was using it. `Pricing`
- **A project that spends its free credit is now paused rather than left running.** When the wallet reaches zero with no subscription, the site goes private until it is topped up or subscribed — and you are warned at half the wallet, at three quarters and again near the end, so nobody meets the pause without having seen it coming. Nothing is deleted, and a top-up or a subscription publishes it again exactly as it was. `Pricing`
- **Enterprise now has a price and a checkout: $100/month for a repository.** No more contacting sales to find out what it costs. What it buys is the part worth knowing: the balance belongs to the PROJECT rather than to you, so everyone you invite spends that one balance without needing a plan of their own, and a team stops paying per person to work on one documentation site. Pro is unchanged at $20/month and is still bought by a person. `Pricing`
- The plans screen now lets you pick which repository Enterprise is bought for, and says in one line which balance each plan tops up, so nobody buys the wrong plan and finds out when a teammate is refused. `Pricing`

### Fixed

- Ask the connected assistant about a site you have not added to Docsbook yet — "here is my site, why are we not in Google, what do the AI assistants say about us" — and it now runs the whole audit before asking you to create anything: what people search for, who holds those results today, and what the competitors' docs cover that yours do not. The search, keyword and competitor tools need no project, so the answer arrives before the sign-up rather than after it. `MCP`

## NEW - 14.09.2026

### Added

- Opening a question, hypothesis, fact or goal on the Overview brief card now shows the GitHub issues and pull requests linked to it, right there in the read view, instead of leaving you to go dig through GitHub to see what work a line is actually attached to. `Overview`

### Changed

- A run that finds no declared goal on a project now states the default — be found through search engines and AI assistants — and gets on with the demand-ranked work, instead of filing a question and waiting for an answer that is the same on nearly every project. It still asks when a project gives a concrete reason to differ. `Agents`
- Every project now decomposes that one standing goal into directions and opportunities on its own, so an agent never has to ask what the docs are for and never invents a placeholder goal just to get started. `Agents`
- The Audits tab is now Opportunities: every row states the search, the competitor holding it today and what would beat them, and what winning it is worth — all in plain business words, with the call ids and readings that back each claim moved to a trace field the owner never has to open. `Overview`
- Every row on the Overview brief card — Questions, Hypotheses, Memory, Goals, Opportunities — now shows a short, plain-language label instead of its full raw text, so the whole list reads at a glance instead of forcing you to scan wrapped paragraphs to tell rows apart; opening a row still shows it in full. `Overview`

### Improved

- Opening a line on the Overview brief card — a question, a hypothesis, a fact, a goal or a reminder — now shows what it SAYS, wrapped and in full, instead of dropping you into a form where a three-sentence goal arrives as one clipped line you scroll sideways with the caret. Editing is a click in that view's footer, so reading what an agent has been told no longer costs a trip through the editor. `Overview`

## NEW - 13.09.2026

### Added

- `link_work` ties an issue, a pull request, a claim, a goal and a reminder into one thread, so the question "did this change work" is answered by the record itself instead of by somebody matching them up by hand. `MCP`
- A forecast about your docs now has to name which of the goals you declared it serves and quote the published finding its predicted size comes from, and an assistant that cannot is refused rather than warned, so the hour it spends goes on something you actually asked for instead of on whatever the first reading turned up. `MCP`
- A new **Audits** tab on the Overview brief card answers the question a goal cannot: how much organic traffic is actually on the table, and how much of it you have taken. An audit names one goal you declared, states the number that would count as reaching it, and lists the searches people make that your docs do not answer — each row with how many look for it, the reading that figure came from, and who ranks for it today. One line per audit beside your goals and claims, with the full opportunity table one click away, so how much of a goal is left is answered on the front page instead of on a screen of its own. `Audits`

### Improved

- Goals, Questions, What Docsbook knows and Reminders are now one card with four tabs — Questions, Memory, Goals and Reminders — each shown as an icon you hover for what it holds, so the two stores an agent reads through `list_memory` and `list_reminders` read on screen as one place instead of four, and an open question, a fact or an overdue reminder stands apart from a closed one by its own icon rather than a tab you had to pick first. `MCP`
- The project brief gains a Hypotheses tab beside Questions, Memory, Goals and Reminders, carrying the claim, its expected effect while it is open and its result once judged, with an overdue verdict flagged amber. `MCP`
- An agent working on your docs is now told to read the goals you declared before it reads a single number, and to go and find published work on the problem before it proposes a fix, so the change it brings you argues for something you asked for and cites where the idea came from instead of reading as a hunch. `MCP`
- The Hypotheses tab marks a claim that argues for no declared goal or quotes no source at all, so a forecast nobody could ever settle is visible at a glance rather than only after opening the row. `MCP`

### Fixed

- The readings that look outside your own docs — a search result, a competitor's page, a public profile — no longer fail with a supplier's product name and one of our own environment variables in the message. They answer in the same words as every other tool here (unavailable, timed out, rate limited, refused), so an agent can act on the answer instead of retrying a configuration problem it has no way to see, and the underlying diagnosis now goes to the operator who can actually fix it. `MCP`

## NEW - 12.09.2026

### Added

- Ask the new `docsbook` agent about anything in your documentation, in your own words, and it hands your coding agent a short set of instructions to carry out — what it found and what says so, the steps in order, what must not change, and how you know it worked — so the work happens in your own checkout in minutes instead of waiting on a run you cannot watch. `MCP`
- Every instruction says where its work lands: your checkout, one named Docsbook call you make yourself, or a decision only a person can take, so no step is quietly assigned to nobody. `MCP`
- `search_tool_calls` finds a past reading by what is inside it — a page it was about, a word in the answer, an error it returned — ranked so the calls actually about `/pricing` come above the fifty that merely mention it, and `get_tool_call` opens one whole. `MCP`
- Docsbook now remembers what is true about your project between sessions: `list_memory`, `add_memory`, `edit_memory` and `remove_memory` hold what these docs are FOR, what nobody has answered yet, and the facts, rules and preferences every agent otherwise works out again on every run — where your real pricing page is, words your product never uses, a section nobody may restructure — so the same question is not answered from scratch, and wrongly, twice. `MCP`
- `edit_goal` corrects a goal in place — its label, what one completion is worth, what it matches — where the only route before was deleting and recreating it, which broke every funnel that named it and reset the date you started measuring. `MCP`
- A **Goals** card on Overview holds what these docs are FOR, in your own words — the sentence every recommendation an agent makes about your documentation gets argued against, so a rewrite can be judged rather than only described. Declare nothing and the card says so, because an agent working on docs with no stated purpose is the finding. `MCP`
- Goals and questions can be closed: mark a goal met with the reading that showed it, answer a question and it keeps the answer, so an agent stops re-proposing work that is already done. An answer you later disagree with can be taken back. `MCP`
- Declaring a conversion goal is free on every plan and is matched retroactively, so a goal you name today already reports the weeks before today rather than starting a count from zero. `Analytics`

### Changed

- Every step says where its work lands: your own checkout, one named Docsbook call you make yourself, or a subagent worth handing it to. Steps in your checkout name the tools, so "look at what changed" arrives as `git log --since` rather than as a suggestion. `MCP`
- Editing a goal from the panel and editing one from an agent now go through the same rules, so a conversion goal one of them accepts and the other refuses is no longer possible. `Analytics`
- The **What Docsbook knows** card no longer prints the goal count as well — the Goals card owns it, so the same number cannot end up stated two different ways on one page. `MCP`
- Goals, Questions and What Docsbook knows now read like the Analytics cards: tabs for open and closed work, every line editable in a dialog instead of a two-line box, the full list with its evidence and its author behind Details, and the actions on whichever row you are pointing at. `MCP`

### Removed

- The forty-one `agent_<goal>` tools are gone from the MCP tool list, replaced by the single `docsbook` agent — of the forty-one, two had ever been called, because a list that long is not something a model chooses from. `MCP`
- The two goal tools added the same morning, `pursue_goal` and `capabilities_for_goal`, went with them: everything they answered is a field of the one `docsbook` answer, and three tools for one question is the problem this release exists to fix. `MCP`

## NEW - 11.09.2026

### Changed

- Every new project now starts on Pro for 14 days with an AI wallet of its own, and that wallet is the only credit we give away — the dollar a project used to be created with and the five dollars you could claim three minutes in are both gone. Whatever is left of the trial wallet ends with the trial; anything you topped up yourself is untouched. `Pricing`
- The first month you pay for credits Pro's AI usage less whatever of the trial wallet you actually spent, so a trial you used is not charged to you twice and a trial you never touched is credited in full. `Pricing`
- A card added during a trial no longer opens overage: overage now needs a subscription that has been successfully charged at least once, so nothing can run up a bill against a card that has never been billed, and the fortnight we told you was free cannot arrive as a line item later. `Billing`
- A project whose trial ends without a subscription is now granted no AI usage at all rather than a small monthly amount, which is what "paused until you upgrade" always said. Topping the project up still works and that money stays yours. `Pricing`

## NEW - 05.09.2026

### Added

- A **Run a full product audit** agent checks whether your docs can be found, believed and stand up against competitors' — fetchability, proof signals, the objection a reader stalls on, and whether the numbers on the page are still true — in one pass, and files what needs fixing as issues on your own repo instead of a report somebody has to run by hand. `Agents`
- Billing is a list of invoices now: what your next charge will be (an estimate you cannot pay early, because overage is still accruing into it), whether the invoice your project is running on has actually been paid, and every charge already taken — each subscription month, each top-up, and each settled overage charge as its own line rather than folded into a month it did not belong to. The old "This cycle" bar has gone; it summed an allowance, your credit and the overage cap into a number nobody is ever billed. `Pricing`
- Your project's 14-day trial now has $20 of AI usage of its own — enough to index a real docs site and let its assistant answer real questions before you decide. It is spent before anything you have paid for, it survives adding a card mid-trial (you are still charged only when the trial would have ended), and whatever is left of it ends with the trial. `Pricing`

### Changed

- Enterprise now promises full branding customization and content rewritten for SEO/GEO and sales as part of the engagement, alongside the existing turnkey setup and migration commitments already on the pricing page. `Pricing`
- The Pages, Referrers, Devices and CTA breakdown cards now default their ranking to Revenue the moment your workspace can measure it (an Average Product Price and a CTA URL set), instead of Visitors — and both that pick and the analytics period switcher now remember your last choice across visits. `Analytics`

### Fixed

- Overage can no longer be raised past $200 a cycle from anywhere — the Limits card, or the API behind it. The field accepted $500 while every sentence in the product promised $200, so the guarantee on the pricing page was one saved setting away from being untrue, and the card now names the ceiling instead of only refusing you after you type past it. `Pricing`
- A project whose last payment failed no longer keeps running up overage on the card that just declined. It spends the credit it already holds — that is yours — and the billing screen says plainly that settling the open invoice is what starts new usage again. Your docs site, its search and every published page stay online throughout. `Pricing`

## NEW - 04.09.2026

### Added

- An **Agents** section in the admin panel: forty goals your project can pursue on its own, each one an ordered route of subagents rather than a single call, with what it is for, the number it is bought to move, and what a run costs before you arm it. Recurring documentation work you were doing by hand every week can now be handed to a schedule. `Agents`
- Arm one on a schedule you read as a sentence in your own clock: how often, which days, at what time, with the next run printed underneath in the same clock. The six presets it replaced were labelled in UTC, so checking one meant converting in your head, and "Tuesday and Thursday at nine" could not be asked for at all. `Agents`
- The project switcher's menu gained an **Upgrade project** button in its pinned footer, opening the same pricing modal the trial banner and win-back notice already use, so upgrading a project no longer means first finding the billing tab. `Billing`

### Changed

- The Pro trial banner is one line now: how many days are left, when it ends, and what upgrading costs or what switches off if you don't — instead of a headline plus a paragraph explaining the same three facts. `Billing`
- Pressing **Improve** or **Analyze** anywhere in the panel — a reader row, a goal, a funnel step, a commit — now starts the agent that fits what you were looking at, carrying what was already on screen as that run's own instruction, and opens the run to watch live: a clock that keeps ticking while it works, and the instruction it started from shown apart from what it did. The button used to just copy that text to your clipboard, from when it opened a chat that no longer exists. `Agents`

### Fixed

- Your AI spend chart, per-model breakdown and the MCP `get_ai_usage` card now total what actually left your balance. A billing statement was reporting a figure it re-read from the row it had just rewritten instead of the one it started from, so a call that spent a real cent could log as $0.00 — across live projects the ledger was missing 17% of billed revenue, worse on the busiest one. Whatever a call's balance couldn't cover in full is now kept and collected on the next call that has money, instead of written off. `Billing`

### Removed

- The **Prompts** section is gone. A prompt was text you copied into your own agent, so nothing in Docsbook could run it or tell you whether it ever ran; what it was reached for now lives where it can act — a goal on a schedule is an **Agent**, and "what can I say to this tool" is the one worked example on that tool's own page. Nothing you have to check by hand moved with it. `MCP`
- The admin panel no longer shows a starting-credit or claimable-bonus card on a project's balance — new projects get a 14-day Pro trial instead of one-off dollar grants, so a card advertising cash that isn't offered anymore is gone too. `Billing`

## NEW - 03.09.2026

### Added

- Two new content widgets. **Tabs** put parallel versions of the same instruction — npm/pnpm/yarn, macOS/Windows, curl/Python — behind one switch, so a reader stops scrolling past two thirds of a page looking for their own variant; the panels are all in the page source and the switching is CSS-only, so every variant stays readable with JavaScript off and visible to crawlers. **Pricing** turns plans into cards a reader can choose between, or a plan table into a comparison matrix, so the shape of the choice is visible instead of being something the reader has to work out from a table. `Content Widgets`

### Fixed

- The published documentation no longer gates features behind the retired Free/Pro/Business ladder. 235 plan labels across the guides, the AI layer, the reference and the analytics pages were telling readers — and any assistant quoting those pages to a buyer — that features already available to everyone required an upgrade. Pages now name what a feature actually consumes: assistant answers, agent runs, page translation and the semantic index draw on the project balance, while hosting, reading, search, GitHub sync, branding and event tracking do not. Unsourced figures went with them, and every price now links to the live pricing page rather than being copied into a page that cannot stay current. `Docs`

## NEW - 02.09.2026

### Added

- The MCP server's agent family is now **135 action tools**, one per step of documentation work rather than one per discipline. Ten verbs — observe, explain, discover, decide, plan, draft, measure, verify, learn, handoff — across fifteen subjects: your capability map, jobs to be done, topical authority, search intent, programmatic SEO, free tools, original research, AI search, competitors, reader vocabulary, content architecture, internal linking, trust, backlinks and market expansion. Ask for a step (`observe_link_graph`, `decide_next_market`, `draft_comparison_page`) instead of an audit, and get rows you can act on instead of a report. `MCP`
- Every action tool names the number it is bought to move — support load, organic traffic, AI citations, time to answer, conversion and eight more — in its own description, so an agent choosing between them is choosing an outcome. `MCP`

### Changed

- **MCP agent pricing is now per tool, not per class.** An action tool is priced from the work it declares — how many families of evidence it reads, how many model round trips it may take, whether it leaves your site, whether it writes an artifact — so calls run **$0.0740 to $0.2450** instead of a flat $0.2500, and waits run about 20 s to 70 s instead of a blanket "30 s – 4 min". The narrow tools are now cheap enough to call in a loop. `MCP`
- The landing page now shows the real admin panel above the pricing card, in the same signed-out preview the anonymous draft ships, instead of hand-drawn mockups that drifted from the product they pictured. `Landing`

### Fixed

- Selecting a passage of text on an anonymous, pre-signup draft now surfaces the "Ask AI" popup, the same as it already did on a claimed site. `AI Chat`

## NEW - 30.08.2026

### Added

- `Analytics` gained a **Spend** figure right of Revenue: what this project's AI actually cost over the period on screen — reader chat, your own chat, translations, embeddings and MCP calls — with a chart of when it was spent and the billed calls behind each point. It needs no setup, it keeps working in a period nobody visited (an overnight translation run is a real bill with no reader behind it), and its arrow stays grey because spend has no good direction. `Analytics`
- Every panel readout now has a guide of its own — `Conversations`, `Dialogs`, `Goals & funnels`, `Users`, `Live`, `Changes`, `Search rankings`, `Feeds`, the translation reports and the MCP cards included — instead of a three-line summary derived from its upgrade copy. `Dashboard`
- Every tool in the `MCP` catalog now opens with worked example sentences of its own, where half of them previously showed only a line naming the tool and its arguments. The scenario tools, the background agents, goals and funnels, the assistant's own reports, semantic search and access control all gained three to five phrasings each, plus the chains that hand one tool's finding to the next. `MCP`
- The same **Improve** button now sits on every goal in `Goals & funnels` and on each step of a funnel, including beside the note that names where a route breaks, so a number that looks wrong is one click from an explanation of why. `Goals & funnels`
- **Improve** now sits on each of the six figures across the top of `Analytics` too, so a conversion rate that fell overnight is one click from an explanation that says what it was compared against and which direction is the good one for that particular figure. `Analytics`
- The assistant can now search the web while it works with you, so an answer about anything outside your project — what a competitor charges, what a framework is currently called, whether a convention still holds — arrives with the pages it read rather than from memory. It searches on its own whenever a recommendation rests on the outside world, and you see the search happen in the thread, with the sources it found named by domain. `AI Chat`
- Each improvement the assistant recommends now carries what it is expected to gain: a range of extra search clicks, and beside it what that is worth per month. Both are computed from your own Search Console history and the value you have declared a visit to have, never written by the assistant, and hovering the row shows the arithmetic — impressions, clicks, the rate the page converts at today, and the rate pages at its position typically manage on your site. `AI Chat`
- Beside it, an **Impact** column says what running it typically moves and which way — support load, upkeep hours, manual watching, time to an answer, citations, markets, traffic, conversion — green for up and red for down, where down is the good one on anything that costs you. `Prompts`
- `Prompts` gained an **Impact** menu of its own beside **Filters**, for the prompts that move one particular thing — support load, upkeep hours, manual checks, time to an answer, citations, markets, traffic, conversion. It asks what you are trying to move rather than what a prompt is about, so a support inbox on fire collects the prompts that help with it whatever they are tagged and whether or not you have ever touched one. Picking two means either would help, not both at once, and every family carries the count it would leave. `Prompts`
- Ten new scenario tools answer a question about your **business** rather than about your docs. What every product a buyer considers instead of yours gives away for free, and the need none of them serves (`map_competitor_free_offers`). Which reader question is answered by a working calculator or validator rather than by a paragraph, and whether it is an existing widget, a custom one, or something needing a service behind it (`design_free_tools`). Whether a repeating axis in your product justifies a generated page family, and whether a machine can keep that family correct (`plan_page_family`). `MCP`
- Six more of them: which numbers you already hold that nobody outside could obtain at any price, and which clear a privacy and contractual gate (`assess_research_assets`); whether a stranger would ever cite one of your pages, and which inbound links now arrive at something broken (`audit_linkability`); which repeated questions reach a person that a page would have closed, ranked by how many *different* people asked (`assess_support_deflection`); which third-party tools readers try to use you with and you never mention (`map_integration_demand`); what an evaluator on a named incumbent cannot find (`assess_competitor_switching`); and what shipped and stayed invisible (`audit_release_adoption`). `MCP`
- Forty-six worked example sentences for the new tools in the `MCP` catalog, including the chains — competitors' free offers into a buildable tool spec into the agent that ships the page, or a support question into the page that closes it. `MCP`

### Changed

- The `Chat` page now leads with the two questions you open it with: what the assistant brought in, and what it cost. **Revenue** is what the readers who used it are worth, counted once per reader on the same scale `Goals & funnels` uses, with the tooltip keeping "reached your goal" apart from "part-way there". **Cost** sits beside it in red — what the chat actually billed, from the ledger, over the same window rather than a fixed week. `AI Chat`
- Signing up to publish a draft now says what actually happens: the site stays exactly as it is and signing up makes it yours. It used to promise that your docs site would generate right after signup, to someone already looking at a finished one. `Dashboard`
- The account menu now opens on the wallet: what is left, what has been spent, **Add credit** and **Pricing**, above everything else in the menu. Billing used to be a row fourth down a list of links, shaped exactly like the changelog and documentation links either side of it. `Billing`
- The reader table's `Goals` column is gone: the goals a reader reached, with how long each took and what each was worth, now open in the hover of their `Completed at` cell, freeing the width that used to push `Last seen` off the right edge. `Analytics`
- `Completed at` now shows a reader's most recent goal completion on any page that is not already narrowed to a single goal, where it used to be blank. `Analytics`
- Read time, Visits, Pages and Time to goal now read at the same size as the columns beside them, and every column is wide enough for its own header. `Analytics`
- A pinned reader's goal chips in `Feeds` now say WHEN each goal was reached, so a conversion on the card points at the row in the stream underneath it. `Feeds`
- Every button in the admin panel that starts the assistant on a ready-made prompt — an **Improve** on a reader, a goal or a funnel step, a **Run** in `Prompts`, an example on an `MCP` tool's page — now opens a new chat instead of adding a turn to whichever conversation you had open last. The one you were already having stays as you left it, and the new question is answered on its own rather than in the context of an unrelated one. `AI Chat`
- `Analytics` no longer counts you and your team browsing your own docs as readers. Every figure that describes an audience — the dead-end rate, the funnel, the breakdowns, the headline and goals — now leaves your own visits out alongside bots. A workspace with no audience yet used to show visits, a bounce rate and a session time that were entirely its owner checking pages after a publish, which is the one reading that feels like a signal and is not. Your visits are not deleted, only kept out of the reader figures. `Analytics`

### Fixed

- Every other card that shows a sample behind its **Fix it** button — the docs assistant's tabs, `Goals & funnels`, and the rest sharing that same backdrop — no longer blurs it either, matching the `Translations` fix above. `Dashboard`

### Improved

- The `Chat` page now loads several times faster. Two of its readouts each asked for the whole conversation history — resolving a reader and a value for every dialog, and pricing them — only to keep a single percentage from the answer. They now ask for that figure alone. The same two readouts at the bottom of `Analytics` got the same treatment. `AI Chat`

## NEW - 29.08.2026

### Changed

- Feeds, Changes and Live now show the real page behind their upgrade gate rather than a drawing of it, so you can see what the feature actually does before paying for it. `Dashboard`
- Goals no longer ship a default funnel nobody declared, and the Journey tab now shows the same honest empty state as the rest of Goals until one exists. `Analytics`

## NEW - 28.08.2026

### Added

- A **Users** page in the admin panel lists every reader of your docs in one table: where they came from, what they read, which goals they reached and how long each one took them, and what that reader is worth. The same table now backs the User and Journey tabs of Goals, and each language's Translations page. `Analytics`
- The Users table now also prices the readers who have **not** reached your call to action, so a page of blanks becomes a ranked list of who to talk to next. A **Potential** figure is your average product price scaled by how much of a converting reader's path someone already matches: how long they have read, how many pages they opened, and how many of the pages that separate buyers from browsers they have been on. Hover a figure to see the comparison it was made against. `Analytics`
- Project cards on the Dashboard now show revenue beside visitors once a project has an average product price and a Call To Action URL set. `Dashboard`
- That page now also shows what a language cost beside who it reached: spent, saved, reused from cache and converted readers, on the same tile row as the audience figures. Reader counts alone cannot say whether a language paid off. Every tile in both rows explains itself on a `?`. `Translations`
- Narrowing a feed to one reader now puts a card above it saying who that reader is: their country, device, system and browser, the language they actually read in, the page they keep coming back to, how long they have spent reading your docs in total, the goals they have reached, and what they are worth today as well as what they might still be. A stream of pageviews under a pseudonym could not answer "who is this". `Feeds`
- Goals now show what the readers standing on them might still be worth. Each goal in `Analytics` ▸ Goals, and each step of a funnel, carries the potential revenue of the readers who got that far and have not converted yet, next to the completion counts; hovering a day on the chart shows the same figure per goal. It is your average product price scaled by how much of a converting reader's path each of them already matches, so a leak can be ranked by the money parked behind it rather than by its percentage alone. `Analytics`
- A commit in `Changes` now reads as a commit and is then measured: its labels, title, description and byline above ten indicators — readers, time reading, dead rate, CTA rate and AI citations measured, then score, earned, revenue, spent and steps to the CTA estimated — over a gallery of the files it touched. Picking a file re-points every number at that file alone. `Changes`
- The conversations table and the Journey view now show when a reader completed a goal and what they're worth. `Analytics`

### Changed

- Filtering the feed now offers each facet by name — **Add event**, **Add visitor**, **Add goal**, **Add status**, **Add destination**, **Search payload** — instead of one **Add filter** button that kept the choices a click out of sight. `Feeds`
- The Users table's **Spent** column is now called **Revenue**: in a panel of cost readouts the old name read as what a reader had cost you rather than earned you. An estimated figure is now labelled `est.` instead of carrying a leading `~`, which in a column of dollar amounts looked like a minus. `Analytics`
- Every goal in `Analytics` ▸ Goals now says what kind of thing it counts — a page view, a section, an event, or a click that leaves for another site — as an icon in the list and in the chart's tooltip, so a goal sitting at zero tells you where to look. `Analytics`
- A funnel step's tooltip now draws each top source with that site's own favicon and each top country with its flag, and groups referrers by site: one site linking in from four pages used to fill the list with four truncated copies of the same name and push a real source out of it. `Analytics`
- Goals and funnels can now be edited and removed from the card itself — hover a goal for its controls, with the funnel's beside its chips. Removing asks first and archives rather than erases, so what you have already measured is not rewritten and a funnel step built on that goal keeps working. `Analytics`
- The Journey view now leads with when each goal was reached — with a quick timeline of what led up to it — instead of listing every goal reached. `Analytics`
- The pricing tab now opens directly on the plan comparison, with your seat status and trial countdown shown there instead of in a separate card, and Usage and Contact Support one click away. `Pricing`

### Removed

- A language's cost row no longer ends on a bare count of converted readers — see the **Earned** tile above. `Translations`

### Fixed

- A reader's value in the goals table was counted once per goal rather than once per visit, so it read lower than the same money elsewhere in `Analytics`. Where no goal declares a value it now estimates from your average product price instead of showing a dash. `Analytics`
- Goal events in `Feeds` now carry their goal's colour. The tint only appeared for goals with a colour set by hand, which almost none have, so for most projects it silently never showed at all. `Feeds`
- **Earned** on a commit in `Changes` now sums exactly the figures the Users table prints for the same readers — a goal's declared value first, then your average product price — instead of a second, shorter calculation that ignored declared values and disagreed with the table its own explanation points at. `Changes`
- The tabs of a card you cannot use yet now switch. On a plan you have not bought, and in the signed-out preview, a card is shown over sample figures with the offer laid over it — but its own tabs were dead, so `Analytics` ▸ Goals showed one of its four views and hid Funnel, User and Journey behind a control that did nothing. Each view has its own sample data and can now be looked through before you decide. `Analytics`

## NEW - 26.08.2026

### Changed

- Setting a goal's match value is now a searchable picker of values the docs site has actually seen, with how often each occurred, instead of free text a typo can silently break. `Analytics`

## NEW - 25.08.2026

### Added

- Goals & Funnels' "Generate with AI" now creates the goals and funnels it proposes, instead of listing them for you to enter by hand. `Analytics`
- Business plan adds Premium Support — a person on our team works directly with you to integrate Docsbook into your business. `Pricing`

### Changed

- Live auto translations are now included on the Pro plan, not just Business. `Pricing`
- The admin Changes tab now leads with revenue, readers and every analytics list for the pages a commit touched, with a before/after compare toggle, instead of a bare score split across four tabs. `Changes`
- The Goals & Funnels card now shares Analytics' own card frame, and its empty tabs show a real, blurred preview of what you're setting up instead of a bare "no goals yet". `Analytics`
- Upgrading now opens checkout inline on our own domain instead of a new tab. `Billing`
- Revenue tiles that need setup are now clickable straight into that setup, instead of just greyed out. `Analytics`

### Removed

- The "$X of AI usage / month" line is gone from every plan's feature list on the pricing page — the AI budget itself is unchanged, only the copy. `Pricing`

## NEW - 24.08.2026

### Changed

- The plan table now opens on annual billing and quotes every column per month, so the cheaper option is the one that reads cheaper. `Pricing`

### Fixed

- Cards that had nothing to show a signed-out visitor are now filled with sample data instead of an error or an empty state — goals and funnels, the commit list, chat conversations and their transcripts, repository folders, navigation and social links, and every language page. `Preview`

## NEW - 23.08.2026

### Added

- `Analytics` now leads with six figures instead of four counts: visitors, revenue, conversion rate, revenue per visitor, bounce rate and session time, each showing how it moved against the period before it. `Analytics`
- An `Average Product Price` setting under `Branding`. Together with your `Call To Action URL` it turns readers who click through to your sales page into a revenue figure. Set only one of the two and the revenue tiles stay switched off saying which half is missing, rather than reporting a confident `$0`. `Settings`
- Every row of the analytics cards now carries revenue beside visitors, so you can see which pages, referrers, channels, countries, browsers and languages brought the readers who *bought* — not only the readers who came. One click switches all four cards between ranking by `Visitors` and by `Revenue`. `Analytics`
- Hovering a row shows its visitors, revenue, revenue per visitor and conversion rate, with buttons to filter by it or open it. `Details` on each card opens the same numbers as a full table. `Analytics`
- `Pages` and `Headings` can now be ranked by `Views` and `Reading time` as well as visitors and revenue, and each figure counts only what happened on that page — a busy visit no longer makes every page it touched look busy. `Analytics`
- `Feeds` can now filter by a single visitor or by whoever completed a goal — open a reader in `Analytics` and jump straight to everything they did in `Feeds`, or paste in an id by hand. `Feeds`

### Changed

- The analytics cards are now grouped as `Pages`, `Sources`, `Audience` and `Conversions`. Nothing was dropped — every existing tab moved into one of the four. `Analytics`

## NEW - 22.08.2026

### Added

- A new `Dialogs` card lists every AI chat conversation individually — topic, funnel stage, answered/dead-end status, and estimated savings — open one to read the full exchange, its real cost, and how it compares to the topic's usual answer rate. `AI Chat`

### Fixed

- The translation savings, visitor and conversion figures no longer render blurred on a paid plan. `Translation`

## NEW - 21.08.2026

### Added

- The pricing page now lists multiplayer chat under Growth and Scale, so the one capability a team is buying is visible before you subscribe. `Pricing`

### Changed

- An empty chat with no project selected now opens with your projects to pick from, and the connectable repositories under them. It used to open with the setup checklist, whose every step configures one specific site, so it asked you to brand, translate and publish a project you had not chosen yet. `AI Chat`

## NEW - 14.08.2026

### Added

- Ask the assistant what to improve and the answer is now a list you tick, not prose you re-type. Each row is one concrete change to one of your real pages, or the settings card that applies it; tick several and press `Apply` once, and they are all done in a single pass. Nothing is ticked for you, and what you leave unticked is never written. The list is drawn from the documentation skill that covers what you asked, what can be measured about your site, and the cards that exist — not from what the model already believed about the topic. `AI Chat`

### Fixed

- The `Compare all plans` table no longer overflows the Upgrade Plan modal, and that panel no longer mentions per-seat pricing. `Pricing`
- On a phone, the preview's Design settings had no route to pricing. `Settings`

## NEW - 10.08.2026

### Changed

- Custom domain and white-label now start on `Pro` instead of `Business`. Your own domain and your own brand are the first two things a site owner wants, so they no longer wait for the $159 tier. `Pricing`

### Fixed

- `Upgrade plan` did nothing when clicked on a chat with no project selected. `Billing`
- Plans on `/pricing` could not be bought: the upgrade CTAs dropped the plan you picked, and the two top tiers were sold with the wrong AI budget. `Pricing`

## NEW - 08.08.2026

### Added

- Enabling a language now asks you to confirm, showing how many pages will be translated, the estimated cost and your remaining budget. When the run does not fit, it says what share of your docs the budget covers and offers the upgrade. `Translations`

## NEW - 07.08.2026

### Added

- `CTA Clicks` shows how many readers left your docs through a link you placed there, with a trend chart and a ranked list of the destinations they clicked. `Analytics`
- A `Feedback` tab next to `CTA Clicks` ranks your pages by the thumbs readers gave them, most-disliked first, counting both the page rating and the votes on AI answers given there. `Analytics`

## NEW - 03.08.2026

### Fixed

- Pricing pages across the docs (blog comparisons, MCP reference, AI features overview, quick-start, branding guide) no longer show AI chat, SEO/GEO/AEO, or the MCP server as paid-tier features — they are free on every plan, including Free. Custom domain and white-label are now correctly attributed to Business (not Pro), and the Source-of-Truth content graph to Business (not Pro). `Docs`

## NEW - 01.08.2026

### Added

- A blue `Upgrade` badge appears next to the account controls in the docs toolbar for free-plan workspaces. `AI Chat`
- Your AI agent can now read a public web page and get it back as clean Markdown, so it can check your docs against a competitor's pricing, your own marketing site, or a link that may have gone dead. `MCP`
- A `Call To Action URL` field sets the one page your docs should drive readers to. Your AI chat points evaluating readers there, content generation writes pages towards it and can add it to your header as a button, and analytics counts conversations ending on that domain as reaching the goal. `Branding`

### Changed

- The chat's target page setting moved from `AI Chat` to `Branding` and is now called `Call To Action URL`, since it is your project's goal rather than a chat option. Anything you already set is unchanged. `Branding`
- A site built before signing up now keeps the call to action found on your own website, so the published project starts with a goal instead of a blank field. `Onboarding`

## NEW - 31.07.2026

### Added

- Two new call-to-action content widgets close a page with the next step the reader should take: `cta` renders a heading and one or two buttons, and `cta-form` turns the primary action into a single field whose value is carried into the target URL. Both stay compact so a documentation page still reads as documentation. `Content Widgets`

## NEW - 29.07.2026

### Changed

- Prices are no longer hidden from visitors who have not signed up: the full plan comparison is visible in a preview, and picking a plan opens the signup form. `Billing`
- Every sign-up prompt in a preview now opens the signup form where you are, rather than sending you to a page that asks you to sign in again and loses the preview you were exploring. `Preview`

### Fixed

- Paywall messages now name the tier you can actually buy, "Pro", instead of a "Pro+" plan that is not on the price list. `Billing`

## NEW - 28.07.2026

### Added

- Seven new analyses answer real business questions: the routes readers walk, where they leak out of a funnel you declare, reverse funnels from successful visits, W1/W4 retention, searches that got results but no clicks, rage signals, and any headline metric plotted over time. `Analytics`

### Changed

- Growth and Scale now include every Business capability — custom domain, white-label, webhooks, your own AI and translation keys, UTM analytics and API reference — which the higher-priced tiers were previously denied. `Pricing`
- Source of Truth and white-label are now Business features, and the pricing page, plan modals and AI upgrade prompts no longer advertise them at the Pro price. `Pricing`
- The homepage now leads with what your docs do for your revenue rather than the underlying tech, and the FAQ accordion is replaced by a gallery of live customer docs. `Landing`

## NEW - 27.07.2026

### Added

- Annual billing (20% off) is now wired end-to-end through checkout for Pro, Business, Growth, and Scale — the toggle appears in the pricing tab once Paddle annual prices are configured. `Billing`

### Fixed

- The `MCP Server` card in the `Integrations` tab now renders with its plan badge and upgrade footer instead of a bare blurred panel. `Integrations`
- Documentation corrected across pricing, plans, AI chat, API, and analytics pages, which still described token budgets, per-workspace billing, and analytics windows that no longer match the product. `Docs`

## NEW - 24.07.2026

### Added

- Anonymous drafts get a live split-screen chat + preview (or a full-screen preview at `/draft`), with a short trial of AI edits before you're asked to sign in. `Onboarding`
- Two new plans: Growth ($349/month) and Scale ($899/month), for teams that want deeper analytics, conversion tracking, and workflow features on top of the existing plans; annual billing on any paid plan now gets a 20% discount. `Pricing`

### Changed

- Business plan price corrected to $159/month everywhere — pricing page, FAQ, and machine-readable `/pricing.md` and `/llms.txt` now agree with the actual checkout price. `Pricing`
- Landing page copy reworded to lead with outcomes (traffic loss, AI vs Google attribution) instead of pricing gimmicks or raw tech specs. `Landing`
- Homepage copy and structured data now frame Docsbook around growth and conversion outcomes, not just docs hosting. `Landing`

### Removed

- The discontinued one-time lifetime plan is no longer offered anywhere, including in AI chat upgrade prompts. `Billing`

## NEW - 18.07.2026

### Changed

- The chat now shows an upgrade prompt in place of the plan badge when you approach your limit. `AI Chat`

## NEW - 17.07.2026

### Added

- `/pricing.md` — a plain-markdown pricing page for AI agents to read directly. `Pricing`

## NEW - 14.07.2026

### Added

- Partner demo workspaces — a temporary Pro trial can be granted and handed off to the client via a one-click claim link that transfers ownership. `Workspace`

## NEW - 05.07.2026

### Changed

- Upgrade page no longer shows specific AI-queries-per-month numbers that had drifted out of sync with actual limits. `Billing`

## 0.26.4 - 12.06.2026

### Improved

- **Buddy mode:** Converted `/buddy` from command to dedicated skill with isolated context — improves modularity and reduces main session token usage.

## 0.24.0 - 04.06.2026

### Added

- **Landing**: New `PricingSection` — 3-column plan comparison block (Free / PRO $150 / PRO+ $59/mo) placed on homepage between CtaBand and FAQ so founders can compare plans at a glance without reading paragraphs

## 0.23.0 - 03.06.2026

### Added

- **Analytics**: Exclude internal (founder/admin) traffic from Axiom with `INTERNAL_IPS` env allowlist — single source of truth in `src/utils/analytics/internal.ts` with consistent IP extraction across all six ingest points (`/api/axiom`, server pageview logger, `/api/vitals`, `/api/_axiom/web-vitals`, `/api/analytics/{cta,feedback}`)

## 0.22.3 - 30.05.2026

### Fixed

- Fix `/pricing` route returning 404 — now redirects to `/` instead of broken `pricing.docsbook.io` subdomain

## 0.22.0 - 28.05.2026

### Changed

- Updated `src/components/SourceOfTruthUpgradeModal.tsx` bullet from "100 reindexes/month" to "Local indexing via Claude Code"

## 0.21.3 - 25.05.2026

### Fixed

- Mobile `/skills` and `/mcp` pages: added hamburger mobile menu to `Header` with full nav links, "Start for free" and "Log in" CTAs

## 0.21.2 - 25.05.2026

### Fixed

- Mobile header: removed the second nav-links row on small screens — header now shows only logo + CTA button

## 0.20.2 - 25.05.2026

### Added

- UTM parameters on all internal CTAs leading from `/skills`, `/mcp`, `/docs` (Preview banner), and the blog to the landing page — every `/start` and `/connect` link now carries `utm_source` (`skills` / `mcp` / `preview` / `blog`), `utm_medium` (`nav` / `cta` / `banner`), and `utm_campaign` (e.g. `header_signup`, `mcp_start_free_top`, `preview_connect`, post slug for blog). New `src/utils/utm.ts` helper (`withUtm()`) wires the landing `Header`/`Footer` via an optional `utmSource` prop, the two inline CTAs on `/mcp`, and the `PreviewConnectBanner` on workspace pages. Blog post CTAs (`docusaurus_vs_docsbook`, `mintlify_vs_docsbook`, `gitbook_vs_docsbook`, `ai_search_documentation`, `documentation_seo_guide`, `how_to_host_docs_from_github`, `why_documentation_matters`) now tag their conversions per post. The landing page itself stays UTM-free so internal scroll-to-CTAs aren't mis-attributed

## 0.20.1 - 25.05.2026

### Changed

- Landing page positioning rewritten for AI crawlers — ChatGPT and Perplexity were describing Docsbook as a plain GitBook/Mintlify/Docusaurus alternative, missing the entire AI-Native layer. Hero H1 changed from "The AI Knowledge Platform" to "Docs from GitHub. For humans and AI agents." with concrete subtitle naming MCP, llms.txt, and 15 languages. New full-width "Built for AI agents" bento card with terminal mock (`claude mcp add`), MCP tool grid (`doc_outline`, `doc_search_text`, `read_doc_sections`, …) and client logos (Claude Code, Cursor, ChatGPT, Perplexity, Cline). New "AI Agents" social-proof tab with CTA to `/mcp`. `metadata.title`, `metadata.description`, JSON-LD `SoftwareApplication.featureList`, and FAQPage rewritten to surface MCP server, llms.txt, Source of Truth graph, Skills catalog, and updated pricing ($150 lifetime PRO / $59/mo PRO+) so AI search engines cite the current product correctly

## 0.19.0 - 25.05.2026

### Added

- MCP visitor activity drill-down — two new tools on PRO+ (`get_top_visitors` and `get_visitor_activity`) let AI agents investigate what one specific anonymous visitor actually did end-to-end. `get_top_visitors` returns the most active anonymous visitors with a stable hashed `visitor_id`, pageview count, country, and first/last seen; pass that `visitor_id` to `get_visitor_activity` to get the full chronological event timeline (pageviews, page feedback, CTA clicks) with paths and event-specific details (vote, query, href, heading, …). `get_page_journeys` also returns the same `visitor_id` so journeys can be drilled into immediately. `visitor_id` is `sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0,16)` — stable across sessions for the same person within one workspace, but raw IPs never leave Axiom

## 0.18.1 - 25.05.2026

### Changed

- Bento feature cards on the landing page now link to their corresponding documentation pages instead of `/connect` — `AI Chat` → `/docs/ai/chat`, `SEO Optimization` → `/docs/content/features/seo`, `Web Analytics` → `/docs/analytics/tracking/overview`, `AI Translations` → `/docs/translation/ai-translations`, `User Feedback` → `/docs/content/features/feedback`. Smoother funnel (visitor reads about the feature first) and internal-linking SEO boost

## 0.18.0 - 24.05.2026

### Added

- Signup attribution tracking — capture UTM parameters and referrer on landing pages, persist as first-touch cookie (`ds_attr`, 90 days), and write `signup_source` / `signup_medium` / `signup_campaign` / `signup_referrer` / `signup_landing_path` to `users` on GitHub OAuth signup so we can measure which channel (Twitter, HN, Product Hunt, dev.to, blog, organic, AI assistants) actually converts
- FAQ reply notebook for community comments at `docs/blog/faq-replies.md` — 32 ready-to-paste answers (TL;DR + Long versions) across 8 sections (General, Pricing, Competitors, AI, SEO, Tech, Security, Objections) for Reddit, X, IndieHackers, and HackerNews distribution
- Month-1 transparency Twitter thread draft at `marketing/twitter-threads/2026-05-month-1-transparency.md` — 11-tweet build-in-public post (genre reference: @levelsio / @marc_louvion) covering hook with revenue, three things that worked (lifetime PRO, MCP server, llms.txt auto-generation), three that didn't (cold email, paid ads, feature bloat), AI chat numbers, and what changes in month 2; placeholders for MRR/lifetime revenue/conversion, character counts inline, posting checklist included
- Twitter teaser thread for Product Hunt launch at `marketing/twitter/ph-teaser-thread.md` — 9-tweet building-in-public thread (D-10 hook + 7 building-in-public tweets covering Anonymous MCP, llms.txt auto-discovery, TOON format, Docusaurus alternatives guide, attribution tracking, sitelinks JSON-LD, skills install UX + CTA), each tweet ≤280 chars, character counts inline, posting notes with UTM campaign `ph-teaser-twitter`
- New blog comparison post `/blog/gitbook-vs-docsbook` — honest 2026 head-to-head against GitBook (~1900 words) covering TL;DR matrix, four reasons teams leave GitBook (per-editor pricing, vendor lock-in, migration cost, AI as commodity), side-by-side feature table, pricing math for three team sizes (solo / 5-person / 20-editor mid-market), 7-step migration path, an honest "when GitBook is the better choice" section, and a 6-question FAQ — targets the "GitBook alternative", "GitBook vs Docsbook", and "GitBook pricing 2026" SEO queries
- Rewrote `/blog/docusaurus-vs-docsbook` into a full "Docusaurus Alternatives in 2026" guide (2.7k words) — TL;DR decision matrix, four reasons teams leave Docusaurus, 9 alternatives compared (Docsbook, Mintlify, GitBook, ReadMe, Archbee, VitePress, Nextra, Starlight, MkDocs Material) with pros/cons/pricing/migration, a "how to choose" section with three decision questions, a step-by-step migration guide, and a 7-question FAQ — targets the "docusaurus alternatives" SEO query instead of the narrower 1:1 comparison

### Changed

- Pivoted pricing FAQ from one-time lifetime to subscription model — PRO now $19/month or $190/year, PRO+ stays $59/month or $590/year (annual saves 2 months)

## 0.17.4 - 23.05.2026

### Fixed

- Replaced broken `(#)` CTA links across 5 blog posts (`mintlify-vs-docsbook`, `docusaurus-vs-docsbook`, `why-documentation-matters`, `documentation-seo-guide`, `ai-search-documentation`) — all now point to `https://docsbook.io/start`
- Removed misleading "free for 14 days" copy in `mintlify-vs-docsbook` — Free plan is free forever; added note that the 14-day trial applies only to PRO+ ($59/month)

## 0.17.0 - 23.05.2026

### Changed (previous)

- Rename `MCP Server` to `MCP Source of Truth` in Pro+ pricing rows and add a hover `?` tooltip explaining the AI-coupled indexing graph

## 0.16.0 - 22.05.2026

### Added

- Subscription management UI in `FloatWidget` pricing tab — shows current plan, subscription status, next billing date, and Manage subscription button linking to Paddle Customer Portal (Pro+ only)
- `pricing-spec.md` in `docs/content/setup` — source of truth for the new billing model
- Two-option upgrade layout in `AiUpgradeModal` and `ProUpgradeModal` — side-by-side Pro lifetime vs Pro+ monthly cards

## 0.15.1 - 22.05.2026

### Added

- Animated growth counters in `CtaBand` — 4 stats (workspaces, pages indexed, countries, AI queries) count up over 6 seconds on scroll-into-view

## 0.15.0 - 22.05.2026

### Added

- Blog section in `docs` with 5 SEO-optimized posts for distribution — competitor comparisons (Mintlify, Docusaurus), AI search, documentation SEO guide

### Improved

- `llms.txt` now serves full product brief — pricing, features, audience, competitors

### Fixed

- GitHub icon removed from primary CTA button on `Landing Page`

### Security

- HSTS upgraded with `includeSubDomains` and `preload` directives

## 0.10.0 - 15.05.2026

### Fixed

- Paddle checkout modal now opens correctly

## 0.2.3 - 09.05.2026

### Improved

- SEO Optimization upsell card now shows as a centered overlay with pricing details

## 0.2.0 - 08.05.2026

### Improved

- Upgrade plan button styled with blue background for better visibility

## Related

- [Full Docsbook changelog](../../CHANGELOG.md) — every release, on every axis
- [Changelogs by outcome](./README.md) — the other eleven numbers a release can move
- [Changelogs by panel section](../README.md) — the same releases, cut by where they landed

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
