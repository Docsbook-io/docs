---
title: "What Docsbook has shipped that cuts your support load"
description: "Every release that means fewer questions reach a human: the assistant, the questions it could not answer, dead ends, and the feedback a failed page leaves."
---

# What Docsbook has shipped that cuts your support load

Everything Docsbook shipped that moves one number: **Support load** — fewer questions reaching a human. On this axis, down is better.

Questions the docs answer are questions your inbox never sees. This is the Support load slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 04.09.2026

### Fixed

- The **Was this page helpful?** prompt no longer draws border boxes around itself or its Yes/No buttons, and no longer sits flush against the previous/next links below it. `Page Feedback`
- **Ask AI** on your own site no longer strands you with neither the toolbar nor the composer after you hid a live chat thread — pressing it now un-collapses the hidden conversation instead of racing a composer bar that can't mount while it's still open. It also always opens the same composer a plain reader gets, so pressing your own Ask AI button shows what a customer actually sees. `AI Chat`

## NEW - 03.09.2026

### Added

- Readers can rate a page from the page itself: a **"Was this page helpful?"** bar now sits at the end of the article, above the previous/next links, so the feedback that tells you which pages fail reaches you from phone readers too. The older thumbs up/down lived only in the right-hand panel, which a narrow screen never renders, so half your audience had no way to answer. On for every project, with its own toggle in Settings → Content next to the in-panel one. `Page Feedback`

## NEW - 02.09.2026

### Added

- Every action tool names the number it is bought to move — support load, organic traffic, AI citations, time to answer, conversion and eight more — in its own description, so an agent choosing between them is choosing an outcome. `MCP`
- The assistant can now read and write that tracker itself — `list_issues`, `get_issue` and `create_issue`, in the admin chat and over your MCP endpoint. Ask it to open an issue, add something to the backlog, or write down what an audit just found, and the finding outlives the conversation instead of ending with it. Filing needs a read-write token; reading does not. `MCP`

### Fixed

- Selecting a passage of text on an anonymous, pre-signup draft now surfaces the "Ask AI" popup, the same as it already did on a claimed site. `AI Chat`

## NEW - 01.09.2026

### Fixed

- The signed-out preview priced a chat conversation at $0.21-$0.41 while the Cost tile above it worked out to about a cent and a half. The rows are the figure an owner multiplies by their own traffic before deciding whether to switch the chat on, and they were eighteen times the truth. `AI Chat`

## NEW - 31.08.2026

### Added

- Each prompt watching a feed gets a chip on that toolbar — filled while it runs, hollow while it is paused, its last run in the tooltip — and clicking one opens the conversation the prompt has been having on its own, so you can see what it actually did rather than only that it is switched on. `Feeds`

### Improved

- Reviewing an AI-proposed change in `AI Chat` now shows each file's diff collapsed by default, so a multi-file proposal reads as a scannable list of files first instead of an unbroken wall of diffs, and the card itself now picks up your workspace's own accent color instead of a flat neutral background. `AI Chat`

## NEW - 30.08.2026

### Added

- Every new project now starts with **$1** of real credit, and a few minutes in a card offers **$5 more** to claim — yours to spend on AI chat, translations, MCP calls or an agent run, with nothing to pay until it runs out. It appears in the sidebar and as a strip across the top of `Billing`, and claiming it is one button. `Billing`
- `Billing` gained **Support us** beside **Add credit** — a monthly amount that tops the same project balance up each month, rather than a plan. It unlocks nothing and gates nothing; every dollar of it lands as credit you spend the same way. Cancel it whenever you like. `Billing`
- Every panel readout now has a guide of its own — `Conversations`, `Dialogs`, `Goals & funnels`, `Users`, `Live`, `Changes`, `Search rankings`, `Feeds`, the translation reports and the MCP cards included — instead of a three-line summary derived from its upgrade copy. `Dashboard`
- Hovering any line of the `Live` activity feed now offers to hand that one action to the assistant, and what it offers depends on what the reader did. A failed search or a page rated unhelpful gets **Fix it** — what in your docs caused it and what to change. A copied code block, a thumbs-up or a search result opened gets **Do more**, which works out what earned it and names the pages it is missing from. Everything else gets **Analyze**, for what that reader is doing and whether any of it needs you. `Live`
- An open conversation on the `Chat` page now has **Analyze**, which reads the transcript for the turn where it went wrong and separates the three causes that look alike: the answer is not in your docs, it is there and was not found, or it was found and reads badly. `AI Chat`
- The assistant's chat list now shows `Scheduled` and `Triggers` before you have any, each ending in a row that takes you to `Prompts` where a scheduled or event-fired chat is actually made. Both used to appear only once they already had runs in them. `AI Chat`
- Those two fold away and carry their count on the folded line, and a group you have nothing in yet starts folded, opening by itself the first time it runs. Your conversations are not one of them: they stay below, always open, headed by **New chat**. Typing in the search box opens a folded group that has a match in it. `AI Chat`
- A chat in that list can now be renamed, so a column of conversations that all open "Work out how to…" can be told apart at a glance. Clearing the name you gave it brings back the one taken from your first message. `AI Chat`
- Chats you keep coming back to can now be pinned, and pinning collects them into a `Favorites` group above everything else in the list. A pinned chat is never the one dropped when the list reaches the number of conversations this browser keeps. Names and pins live in the browser you set them in, like the conversations themselves. `AI Chat`
- The assistant can now search the web while it works with you, so an answer about anything outside your project — what a competitor charges, what a framework is currently called, whether a convention still holds — arrives with the pages it read rather than from memory. It searches on its own whenever a recommendation rests on the outside world, and you see the search happen in the thread, with the sources it found named by domain. `AI Chat`
- Search results are treated as a way to pick a source, not to quote one: before any figure, version or price from the web is written into your docs, the assistant opens the page itself. If the search cannot run, it says so instead of answering as though it had searched. `AI Chat`
- Each improvement the assistant recommends now carries what it is expected to gain: a range of extra search clicks, and beside it what that is worth per month. Both are computed from your own Search Console history and the value you have declared a visit to have, never written by the assistant, and hovering the row shows the arithmetic — impressions, clicks, the rate the page converts at today, and the rate pages at its position typically manage on your site. `AI Chat`
- Those figures say nothing they cannot support. A page already doing better than its position predicts shows how much traffic the change touches rather than a gain; a structure or settings recommendation carries no prediction at all, because neither changes how often a listing is clicked; and a page with too little search history shows an empty space rather than a zero. Every prediction is marked an estimate while the assumption behind it is reasoned rather than measured against what past changes actually did. `AI Chat`
- When the admin assistant genuinely cannot finish something, the turn now ends on a card that names what blocked it, what was already tried, and a message to us already written — one field to check and one click, instead of an apology and an empty support form to compose from scratch. `AI Chat`
- An open conversation on the `Chat` page now has **Improve** beside **Analyze**. Analyze reads the transcript for where it went wrong; Improve answers the other question — what to change in your docs so the next reader asking this does not need the chat at all, named at the right layer: a page that should exist, a link that should have connected two pages, or a retrieval problem no rewrite will solve. `AI Chat`
- The `Chat` page now has an **Open chat** button beside its title, which opens the actual reader-facing chat on your published docs — not the admin assistant this panel already offers on its own `AI Chat` tab. `AI Chat`
- Beside it, an **Impact** column says what running it typically moves and which way — support load, upkeep hours, manual watching, time to an answer, citations, markets, traffic, conversion — green for up and red for down, where down is the good one on anything that costs you. `Prompts`
- `Prompts` gained an **Impact** menu of its own beside **Filters**, for the prompts that move one particular thing — support load, upkeep hours, manual checks, time to an answer, citations, markets, traffic, conversion. It asks what you are trying to move rather than what a prompt is about, so a support inbox on fire collects the prompts that help with it whatever they are tagged and whether or not you have ever touched one. Picking two means either would help, not both at once, and every family carries the count it would leave. `Prompts`
- **Settings ▸ Chat** now has two model settings instead of one. **AI Visitors Chat Model** is what answers your readers; **Admin & AI Agent Model** is what runs the assistant in your dashboard — the one that reads your analytics, calls tools and edits your docs. Picking a stronger model for yourself and a cheaper one for your readers, or the reverse, is now one choice each. `AI Chat`
- All three pickers offer more models, cheap to expensive — GPT-4.1 nano, DeepSeek V3, Gemini 2.5 Flash and Pro, GPT-4.1 and Claude Opus 4.1 join the list, each with its price per 1M tokens beside it. `AI Chat`
- Six more of them: which numbers you already hold that nobody outside could obtain at any price, and which clear a privacy and contractual gate (`assess_research_assets`); whether a stranger would ever cite one of your pages, and which inbound links now arrive at something broken (`audit_linkability`); which repeated questions reach a person that a page would have closed, ranked by how many *different* people asked (`assess_support_deflection`); which third-party tools readers try to use you with and you never mention (`map_integration_demand`); what an evaluator on a named incumbent cannot find (`assess_competitor_switching`); and what shipped and stayed invisible (`audit_release_adoption`). `MCP`
- Forty-six worked example sentences for the new tools in the `MCP` catalog, including the chains — competitors' free offers into a buildable tool spec into the agent that ships the page, or a support question into the page that closes it. `MCP`
- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`
- Forty-two more worked examples in the `MCP` catalog, and ten existing prompts now call one of the new tools where it changes the answer — the unanswered-questions prompt now splits "the page is missing" from "the page exists and nothing can retrieve it", and the striking-distance prompt now says whether the page is simply the wrong shape for the query. `MCP`

### Changed

- The `Chat` page now leads with the two questions you open it with: what the assistant brought in, and what it cost. **Revenue** is what the readers who used it are worth, counted once per reader on the same scale `Goals & funnels` uses, with the tooltip keeping "reached your goal" apart from "part-way there". **Cost** sits beside it in red — what the chat actually billed, from the ledger, over the same window rather than a fixed week. `AI Chat`
- **Savings** keeps its place after them, because support cost avoided is worth seeing and is not the same money as either. It now says on its own tile that it is an estimate standing next to two measurements. The old **Earned** tile, which counted link follows rather than money, has gone; those clicks are still on the conversation rows. `AI Chat`
- The conversation table now opens with **Potential** and **Cost** ahead of **Time**, instead of at the far right behind six other columns where a narrow panel had to be scrolled to reach either. Potential is green, with the money reading it carries. `AI Chat`
- **Last seen**, **Completed at** and **Savings** are no longer shown by default in that table — the first repeats the order the table is already sorted in, the second reads the same on every row of the same reader, and the third is an estimate standing next to two measured columns. All three are one click away in the column picker, still sortable and still filterable. `AI Chat`
- **Assistant** in the draft's panel is where you rewrite a page, add one or change the wording, and **interactive mode** in its message box opens the site with the chat beside it and every block clickable, with a way back to the panel in the corner. `AI Chat`
- **New chat** now heads your conversations in the assistant's chat list, directly above them, instead of sitting at the very top of the column two groups away from the list it starts one in. It still answers to nothing that is folded. `AI Chat`
- The assistant's **Search chats** box is now set off by a line above and below it, so it reads as the thing narrowing the lists under it rather than as another row in them. `AI Chat`
- What `Scheduled` and `Triggers` are is now told by hovering the group's name, in both groups and whether or not you have anything in them. It used to be a paragraph inside the group that only appeared while the group was empty, so it was on screen exactly when there was nothing to explain and gone the moment it filled. `AI Chat`
- The `Docs assistant` card's eight tabs (Topics, Why they came, Searches, Lang, Links, Outcome, Feedback, Coverage gaps) each carry their own **Enable** now too, the same way every other tab on `Analytics` does, in place of one button covering the whole card. A workspace with plenty of outbound clicks and nothing yet on Coverage gaps meets the guide there and nowhere else. `Analytics`
- The `Chat` page now has one **Turn on** for the whole page rather than one over its four figures and a second over the conversations under them. The figures are the page's heading, not a card of their own, so they no longer carry a switch of their own — a button in a strip that height had more empty space around it than the strip had height. `AI Chat`
- The conversations list on `Chat` now fills the screen under those figures instead of stopping two thirds of the way down, so a project nobody has asked anything yet reads its whole explanation without scrolling to find the end of it. `AI Chat`
- The admin chat no longer draws a second floating top bar over the one already there. `AI Chat`
- The search, filters and column picker above the `Users` and Chat conversation tables are now a single row that stops growing as you add filters, and the period picker moved into it — the first row of data is that much closer to the top. `Analytics`
- The Chat page now reports your whole chat history rather than a single window, and its tiles and conversation list can no longer quote different periods. There is no interval picker: hover any tile to see that figure for the last 24 hours instead, shown as zeros on a quiet day rather than left blank. The interval pills stay on the framed card. `AI Chat`
- The conversation list now loads a page at a time instead of the whole history at once, so the Chat page opens at the same speed however long the assistant has been running. The footer says how many conversations are on screen and how many there are in all, and **Load more** fetches the next batch. `AI Chat`
- The conversations table on the Chat page now uses the pane's full width, matching the readers table, and its heading is gone — the sidebar row already says Chat. `AI Chat`
- The second built-in feed in `Feeds` is now **Reader events**, everything the people reading your docs did: pages read, searches run, questions asked of the AI and feedback left. It replaces **Unanswered questions**, which only filled up where an answer came up empty; those two event types are still one click away in the Workspace filter. `Feeds`
- Three feeds joined the built-in roster: **Translations** (every language generated, outdated or still needed), **Language events** (which languages readers switch the docs into) and **Chat events** (questions the AI assistant was asked, where it came up empty, which answers got a thumbs-down). `Feeds`
- Every button in the admin panel that starts the assistant on a ready-made prompt — an **Improve** on a reader, a goal or a funnel step, a **Run** in `Prompts`, an example on an `MCP` tool's page — now opens a new chat instead of adding a turn to whichever conversation you had open last. The one you were already having stays as you left it, and the new question is answered on its own rather than in the context of an unrelated one. `AI Chat`
- A recommendation is now one row instead of a paragraph: the change, how much it matters, the pages it touches as chips carrying the icon of what each one is, and the forecast on the right. The explanation moved to hover, and on a touch screen it stays under the title. Five recommendations that filled 789 pixels now take 565, so a set of seven can be compared without scrolling. `AI Chat`
- Recommendations are now grouped by the kind of work they are — page text, structure, and workspace settings — each under its own heading with a count, instead of naming the kind in small grey text at the end of the row. `AI Chat`

### Fixed

- The rename, pin and delete actions on a chat row are now reachable without a mouse. Tabbing to a row reveals them, and on a touch screen they are always there. Deleting a chat previously appeared on hover only, which no touch device and no keyboard could produce. `AI Chat`
- A conversation reopened from the assistant's chat list now shows the answers, not only the questions you asked. A long turn — a docs audit, a page generation — outgrew what the browser will store, and every save carrying the answer was refused while the one carrying the question alone had already gone through. Long passages inside a stored conversation are now shortened to fit, marked where they were cut, and the conversation you are having keeps its place ahead of older ones when the browser runs out of room. `AI Chat`
- The `Chat` page's **Answered** figure now actually fills in. Every visit read the transcripts, asked the model whether each conversation got a real answer, and then threw the verdicts away — so the same handful of conversations was re-read on every load and the column never moved past unjudged. Verdicts are now kept, and the reading builds up over a few visits instead of starting from nothing each time. `AI Chat`
- The `Docs assistant` card at the bottom of `Analytics` no longer renders as an empty box. A workspace whose readers had clicked links inside an answer but held no recorded conversations got a card with tabs across the top and nothing under them. Every tab is now always there, and a tab with nothing of yours in it says what would live there and why it is empty, over a faded sample of a filled report, with a **Fix it** that asks the assistant which kind of empty it is. `Analytics`
- `Outcome` on that card no longer reports a window with no conversations as `Answered 0 / Dead end 0 / Unrated 0`. Three zeros read as three measured failures; nothing measured now says so. And `Coverage gaps` says plainly when it is empty because nothing dead-ended, which is the best reading it has, instead of offering to fix a working assistant. `Analytics`
- The admin assistant no longer tells you the project you have open is not on Docsbook. It could reach that ending while its own tools were returning your pages and your commit history; when it does now, it is caught and the turn continues on the real project by name instead of offering to create the workspace you are already looking at. `AI Chat`
- Approving proposed changes in a review card now reliably applies them. The assistant previously had to retype every approved file's full text from scratch to commit it, and on a large batch it could refuse the whole thing rather than risk getting that copy wrong. Approved changes are now committed straight from the proposal you reviewed, so nothing is retyped and nothing is refused. `AI Chat`
- The proposed-changes panel is now readable in dark mode; its diff sat on a light background whatever theme you were using. `AI Chat`

### Improved

- The `Chat` page now loads several times faster. Two of its readouts each asked for the whole conversation history — resolving a reader and a value for every dialog, and pricing them — only to keep a single percentage from the answer. They now ask for that figure alone. The same two readouts at the bottom of `Analytics` got the same treatment. `AI Chat`

### Removed

- The **Make these applicable** button that appeared under an answer listing improvements is gone. `AI Chat`

## NEW - 28.08.2026

### Added

- The AI assistant is now a section of that panel, with the project already selected, instead of only an overlay on a docs page. `AI Chat`
- A **Getting started** checklist now sits at the bottom of the admin panel's sidebar, showing what your site still needs — its content, your branding, the AI chat, languages, your agent, your domain, and being findable. It ticks steps off as they are configured, collapses to a single row, and disappears once you are done. `Dashboard`
- The Users table now also prices the readers who have **not** reached your call to action, so a page of blanks becomes a ranked list of who to talk to next. A **Potential** figure is your average product price scaled by how much of a converting reader's path someone already matches: how long they have read, how many pages they opened, and how many of the pages that separate buyers from browsers they have been on. Hover a figure to see the comparison it was made against. `Analytics`
- Project cards on the Dashboard now show revenue beside visitors once a project has an average product price and a Call To Action URL set. `Dashboard`
- A language's Translations page now shows what its readers were worth as an **Earned** tile, priced from your Call To Action and Average Product Price, next to spend, savings and cache reuse. `Translations`
- Goals now show what the readers standing on them might still be worth. Each goal in `Analytics` ▸ Goals, and each step of a funnel, carries the potential revenue of the readers who got that far and have not converted yet, next to the completion counts; hovering a day on the chart shows the same figure per goal. It is your average product price scaled by how much of a converting reader's path each of them already matches, so a leak can be ranked by the money parked behind it rather than by its percentage alone. `Analytics`
- Chat conversations are now individually judged by AI on whether they actually answered the question, shown as its own column and rolled up into a more accurate Answered rate. `Analytics`
- The conversations table and the Journey view now show when a reader completed a goal and what they're worth. `Analytics`

### Changed

- `/chat` now takes you to the Dashboard. Links, bookmarks and a prompt typed before signing up all still work. `AI Chat`
- The Conversations table now shows one line per row, with a reader's country and device as icons beside their name and the site that referred them shown with its own favicon. Cost and Savings are their own columns, the topic column is labelled Topic, and a Time column shows how long the conversation ran and how long that reader has spent on your docs. `AI Chat`
- Opening a conversation now shows the transcript as a chat, with the reader's question and the assistant's answer as separate message bubbles, next to a panel with what's known about that reader — click it to see everything else they did, in `Feeds`. `AI Chat`
- `Feeds` now opens on **Select a feed**: a card for each feed with a line saying what it holds. Four are built in — All events, Unanswered questions, Reader feedback and Delivery trouble — so there is something to open before you have saved anything of your own. `Feeds`
- A language's sync state, coverage, source commit and any halt reason now live in a popover on the state chip, next to the switch and **Translate now** on one line. The 200px card that held them pushed "did this language pay off" below the fold. `Translations`
- The Signals and Turns columns in Chat's conversations table are hidden by default; they're still available from the column picker. `Analytics`
- The pricing tab now opens directly on the plan comparison, with your seat status and trial countdown shown there instead of in a separate card, and Usage and Contact Support one click away. `Pricing`

### Removed

- The low-credit pop-up no longer floats over the bottom-right of the assistant. It is the sidebar card above, which does not cover what you are reading and does not repeat what the sidebar already says. `AI Chat`

### Improved

- Reader avatars are now far less likely to give two different readers the same colour. The palette was built for eight chart series and collided constantly across a 25-row table; the colour is now generated per reader, and hard-to-tell-apart pairs drop from roughly 4% to under 2%. Affects `AI Chat`, `Analytics` and the Journey tab. `Analytics`
- A reader's browser now shows as its own mark beside their device, instead of being a word buried in a tooltip. `AI Chat`

### Fixed

- The estimated **Savings** figure in `AI Chat` now subtracts what those conversations actually cost to run, instead of ignoring your real spend — a workspace with real chat activity no longer sees it read as $0. `AI Chat`
- A reader's value in the goals table was counted once per goal rather than once per visit, so it read lower than the same money elsewhere in `Analytics`. Where no goal declares a value it now estimates from your average product price instead of showing a dash. `Analytics`
- **Earned** on a commit in `Changes` now sums exactly the figures the Users table prints for the same readers — a goal's declared value first, then your average product price — instead of a second, shorter calculation that ignored declared values and disagreed with the table its own explanation points at. `Changes`
- Savings in `AI Chat` no longer reads $0 for a real answer the reader didn't click through or rate — it now credits the AI's own verdict on whether the conversation was answered. `AI Chat`

## NEW - 26.08.2026

### Changed

- The doc toolbar's trigger is now an inverted pill, and its brand mark opens chat directly. `AI Chat`
- `More` in the project picker now opens the full project menu instead of revealing more rows in place. `AI Chat`

### Fixed

- The project picker in the chat header no longer grows past the screen with a long project list — it now caps its height with a pinned footer. `AI Chat`

## NEW - 25.08.2026

### Added

- Business plan adds Premium Support — a person on our team works directly with you to integrate Docsbook into your business. `Pricing`

## NEW - 24.08.2026

### Added

- A live chat bubble now appears for signed-in users everywhere — the `/chat` dashboard and any doc page you administer — to reach support directly. `Support`

### Changed

- Choosing which AI model answers your docs chat is now available on every plan, including Free — pick a cheaper or stronger model without upgrading, billed at that model's real price. `AI Chat`

### Fixed

- Cards that had nothing to show a signed-out visitor are now filled with sample data instead of an error or an empty state — goals and funnels, the commit list, chat conversations and their transcripts, repository folders, navigation and social links, and every language page. `Preview`

## NEW - 23.08.2026

### Added

- A `Lang` tab on the `Conversations` card in `Chat` shows which languages readers write in, each row with its flag, so a workspace serving several languages can see the split at a glance. `AI Chat`
- Every conversation in `Chat` — the dialog list, the sidebar, and the open conversation — now shows the flag of the language it was written in. `AI Chat`
- An `Average Product Price` setting under `Branding`. Together with your `Call To Action URL` it turns readers who click through to your sales page into a revenue figure. Set only one of the two and the revenue tiles stay switched off saying which half is missing, rather than reporting a confident `$0`. `Settings`
- The average product price can also be set from the assistant and over MCP, through `update_branding`. `MCP`
- Your workspace's background glow and accent color now carry into the AI chat panel too — full-screen and side-by-side — instead of stopping at the docs page's edge. `Theme Settings`
- Every language page opens on whether that language is keeping up — coverage split into current, fallen behind and never translated, when it was last written to, and which commit your docs stand at. `Translations`
- A button back to `Fullscreen` from the side-by-side chat, next to the project picker — shown only while the chat sits beside your docs. `AI Chat`

### Changed

- The `Top searches` tab on the `Conversations` card is now called `Searches`. `AI Chat`
- The standalone `Support` button beside the gear is gone. Support is reachable from the settings panel's own sidebar. `Docs`
- Project cards in the project picker show the connected repository's real GitHub avatar instead of a generic folder icon, and list your most recently used projects first. `AI Chat`
- `More` in the project picker now reveals two more rows at a time instead of the whole list at once, and relabels to `Load more` after the first press. `AI Chat`
- The project and conversation pickers in the chat header lost their border and background, with a bolder project name and tighter spacing. `AI Chat`
- The project picker in the chat header now leads with your repository's own GitHub avatar next to its name, and the name reads larger. `AI Chat`
- Settings now opens in one click from a gear icon in the chat header, instead of behind a menu. `AI Chat`
- The chat and change-history icons in the chat header now read in full color instead of muted. `AI Chat`

### Fixed

- Long project names and site paths no longer overflow their card in the project picker. `AI Chat`

### Removed

- Overage billing. AI usage now simply pauses once the plan's monthly budget is used up — never billed above your plan price. `Usage`
- The repository browsing list under `Connect a repository` in the project picker. `Start a new project` connects a new repo instead. `AI Chat`
- The `Try Docsbook` prompt grid that used to follow a finished setup checklist. `AI Chat`
- The centered "Docsbook" logo and wordmark shown above the composer on an empty conversation. The input stays exactly where it was. `AI Chat`
- The Docsbook logo and its menu from the chat header. Settings now opens in one click (see above); the connected repository, theme and sign out moved into the settings panel and the project picker. `AI Chat`
- The address bar above the side-by-side preview (page list, open in new tab, mobile width, reload). `Plan`, `Invite` and `Visit` sit there now instead, the same row the full-screen chat already showed. `AI Chat`

## NEW - 22.08.2026

### Added

- `Changes` now reports what Google did with the pages a commit touched: average position, impressions, clicks and click-through rate against the rest of the site, a daily chart with the commit marked on it, and a per-URL rank table. `Changes`
- A new `Dialogs` card lists every AI chat conversation individually — topic, funnel stage, answered/dead-end status, and estimated savings — open one to read the full exchange, its real cost, and how it compares to the topic's usual answer rate. `AI Chat`
- The `Conversations` card gets an `Outcome` tab — answered, dead-end, and unrated conversations at a glance, each opening straight into `Dialogs` pre-filtered. `AI Chat`
- Each conversation in `Dialogs` now shows what it actually cost to run, right next to its estimated savings. `AI Chat`
- `Select Chat` in the account menu lists every conversation in this project behind a search field, so a thread from last week is one query away instead of a scroll. `AI Chat`
- `Select Mode` in the account menu picks how the chat and your documentation share the screen: `Fullscreen`, `Sidescreen`, or `Preview` for the docs on their own. It sits on the doc toolbar's avatar too, so a chat you put away is always one click from coming back. `AI Chat`
- A `Changes` button sits beside the account control at the top of the chat, so the list of what was published to your docs is one click away from the conversation that wrote it. `AI Chat`
- `Interactive mode` sits next to `+` in the composer: turn it on and the docs open beside the chat with click-to-edit armed. Turning it off stops click-to-edit and leaves the docs where they are, so the page you were editing does not disappear behind the chat. `AI Chat`
- An `Invite` button now sits next to `Visit` in the chat toolbar, and split view gets a fullscreen toggle beside it. `AI Chat`
- `Get Support` now has a message form built in — the reply address is prefilled from your account and stays editable, and the message goes straight to us without opening a mail client. `Settings`
- `Needs attention` in the `Feeds` digest counts the events where a reader hit a wall — unanswered chat questions, dead-end searches, stale content and translations, usage limits — separately from routine activity. `Feeds`

### Changed

- The admin panel's sidebar now opens `Get Support` directly, replacing the old `Book a demo` link — booking a demo lives inside that tab now, alongside `Contact Us`. `Settings`
- The chat toolbar's site-link button now reads `Visit` with a leading external-link icon, instead of `Open website` as plain text. `AI Chat`
- The chat's top-left button shows the Docsbook mark instead of your avatar. It opens the same account menu, which names the account you are signed in as in its first row. `AI Chat`
- `Invite` in the chat toolbar is now a button with its label on it rather than a bare icon, so it is clear before you click that it adds someone to the workspace. `AI Chat`
- The `+` for a new conversation left the chat's top-left corner; `New chat` is the first row of `Select Chat` in the account menu, where it always was. `AI Chat`
- Every row in the `Conversations` card (topics, buying stage, coverage gaps, feedback) now opens straight into `Dialogs`, pre-filtered to that group. `AI Chat`
- `Chat` now opens into its own page from the sidebar, the same way `Settings` and `Feeds` do — `Dialogs` no longer sits beside `Conversations` as a separate card: it drops its own time range and filters (`Conversations` already covers the whole page) and loads older conversations automatically as you scroll. `AI Chat`
- The preview pane's address strip is now a compact pill: a page picker that names the page instead of showing the URL, with open-in-new-tab, mobile width and reload beside it, and `Copy link` moved into the picker's menu. `AI Chat`
- Mobile width in the preview now clamps the page to a real 430px card rather than emulating a phone, so what you check is the live page at that width. `AI Chat`
- The account avatar moved to the top-left of the chat, into the corner the conversation switcher, layout toggle and change-history buttons used to occupy: all three are named rows of its menu now, so nothing in the chat's chrome has to be recognised by its icon. `AI Chat`
- Standalone chat pages show the Docsbook mark and your project's name in the top-left corner instead of your avatar — the same account menu opens either way. `AI Chat`
- Every tag on a `Dialogs` row and on an open conversation's header — buying stage, outcome, docs gap — now carries its own colour instead of some falling back to plain grey. `AI Chat`

### Removed

- The `AI Usage` and `Chats Analysis` cards — the numbers now live inside `Conversations` and the new `Dialogs` card. `AI Chat`
- The separate button for hiding the chat: `Visit` already hands the page back to your documentation with the conversation still running, and `Select Mode` names that same state as `Preview`. `AI Chat`
- The project-switcher pill in the chat composer — pick a project from the new top-left menu instead. `AI Chat`

## NEW - 21.08.2026

### Fixed

- The example-prompt arrows in chat are now labelled "Previous / More example prompts", so they are no longer mistaken for a way back to earlier conversations. `AI Chat`
- A momentary limit on the AI provider is now retried, and falls back to a second key when one is configured; if it still fails you get a plain explanation instead of a raw provider error. `AI Chat`

### Changed

- An empty chat with no project selected now opens with your projects to pick from, and the connectable repositories under them. It used to open with the setup checklist, whose every step configures one specific site, so it asked you to brand, translate and publish a project you had not chosen yet. `AI Chat`
- The lists under the chat composer are set at a readable size and scroll with the page instead of inside their own box, so a long list is no longer cropped at an edge that looks like its end. The composer itself stays in the middle of the screen however long that list is. `AI Chat`

## NEW - 15.08.2026

### Changed

- AI chat answers now reveal word by word as they stream in, instead of a blinking caret. `AI Chat`

## NEW - 14.08.2026

### Added

- Ask the assistant what to improve and the answer is now a list you tick, not prose you re-type. Each row is one concrete change to one of your real pages, or the settings card that applies it; tick several and press `Apply` once, and they are all done in a single pass. Nothing is ticked for you, and what you leave unticked is never written. The list is drawn from the documentation skill that covers what you asked, what can be measured about your site, and the cards that exist — not from what the model already believed about the topic. `AI Chat`
- The first-day `Try Docsbook` cards now lead with filling in your docs and saving them to GitHub. `AI Chat`

### Changed

- AI chat answers are set in a tighter line-height. `AI Chat`

### Fixed

- Typing on `/chat` with projects but none selected no longer sends you into the create flow. `AI Chat`
- Asking for a change on the project you already have open no longer tries to create it again. `AI Chat`
- `Start new project` from a workspace subdomain no longer 404s, and the project switcher no longer doubles the organisation in its path. `AI Chat`

## NEW - 10.08.2026

### Added

- The empty chat now offers four ways to start — from a GitHub repo, from your website, from an idea, or from files and screenshots — and each one opens the create flow with that source already chosen, so you go straight to the one question it needs. `AI Chat`
- `Start a new project` is now always in the project menu, not only when a project is already open. `AI Chat`

### Fixed

- `Start from an idea` and the other build shortcuts used to start generating without ever asking what to build from, and named the result on their own. They now ask first. `AI Chat`

## NEW - 08.08.2026

### Changed

- In the full-screen chat, `Preview` is now `Open website` — it leaves the chat for the site, rather than naming a state you were already in. `AI Chat`
- The project switcher offers visitors without an account `Claim website` instead of `Sign up to connect a repo`. `AI Chat`

### Fixed

- Answers about paid features keep the plan requirement instead of describing the steps as if the feature were available on any plan. `AI Chat`
- The docs chat no longer invents integrations that do not exist, and admits when a topic is not covered. `AI Chat`

## NEW - 07.08.2026

### Added

- `Semantic Search` turns meaning-based answers on or off for your readers, shows when the index last updated, and keeps the rebuild controls in one place. `AI Chat`
- Ask the chat what to fix in your docs and the answer arrives as ranked recommendation cards, each opening a fresh chat that already knows the page and the problem. `AI Chat`
- A `Feedback` tab next to `CTA Clicks` ranks your pages by the thumbs readers gave them, most-disliked first, counting both the page rating and the votes on AI answers given there. `Analytics`
- A `Feedback` tab in the chat card shows which topics readers approve of and which they vote down. `AI Chat`
- `Search rankings` leads with four figures — impressions, clicks, average position and the queries you rank for — each with its own trend, and every query row carries the action to take on it. `SEO`

### Removed

- The `Pages` tab is gone. Its semantic graph now lives on as `Semantic Search` in `AI Chat`, its recommendations moved into the chat itself, and change history stays available where you already track it. `Dashboard`

### Fixed

- The semantic index now builds when you ask for it and keeps itself up to date as your docs change, instead of staying empty and leaving meaning-based answers falling back to keyword search. `AI Chat`

## NEW - 03.08.2026

### Fixed

- Pricing pages across the docs (blog comparisons, MCP reference, AI features overview, quick-start, branding guide) no longer show AI chat, SEO/GEO/AEO, or the MCP server as paid-tier features — they are free on every plan, including Free. Custom domain and white-label are now correctly attributed to Business (not Pro), and the Source-of-Truth content graph to Business (not Pro). `Docs`

## NEW - 02.08.2026

### Added

- Any change the assistant publishes can be undone from the chat: an undo button on the card that announced it, and a clock icon in the chat header listing recent changes with an undo beside each one. Undoing writes a new commit rather than rewriting history, so it shows up in the list itself and never discards a teammate's work. `AI Chat`

### Changed

- Ask AI on a draft is no longer capped at 3 messages before signing in: it now runs on a free daily AI credit, so short questions barely count while rewriting a long page uses more of it. `AI Chat`

### Fixed

- Asking a question on a docs site that has no AI chat connected now explains that in plain language instead of showing `HTTP 400`. `AI Chat`
- A draft message sent after the free AI credit runs out no longer disappears: it stays in the conversation with the explanation beneath it, instead of the chat looking as though nothing was sent. `AI Chat`
- The `Sign in` prompt on a draft now opens the sign-in window over your site, with GitHub, Google and email, instead of sending you straight out to GitHub. `AI Chat`

## NEW - 01.08.2026

### Added

- A blue `Upgrade` badge appears next to the account controls in the docs toolbar for free-plan workspaces. `AI Chat`
- The chat header's `GitHub` icon now shows a green dot when your GitHub account is linked, and clicking it opens a switcher listing your account and every organization you belong to — hover one to see its repositories and connect one as a new project. `AI Chat`
- Signing up now starts by asking what you do — founder, developer, technical writer, marketing, support — so the product can speak to your job rather than treat everyone the same. `Onboarding`
- A `Call To Action URL` field sets the one page your docs should drive readers to. Your AI chat points evaluating readers there, content generation writes pages towards it and can add it to your header as a button, and analytics counts conversations ending on that domain as reaching the goal. `Branding`

### Changed

- The chat's target page setting moved from `AI Chat` to `Branding` and is now called `Call To Action URL`, since it is your project's goal rather than a chat option. Anything you already set is unchanged. `Branding`
- A conversation you started before signing up carries over to your new project and reopens beside your documentation, so you can pick it up where you left off. `Onboarding`
- The docs toolbar's `Ask AI` button is now two icon buttons next to your avatar: `Chat` opens the full AI chat directly with the composer focused, `Editor` arms block-level editing with no chat needed. Pressing the active one returns the page to its normal state. `AI Chat`
- The conversation switcher left the docs toolbar — past chats are switched from the chat's own header, where a conversation is on screen to switch away from. `AI Chat`
- The `Invite` button in the chat header is now a plus-icon next to your account avatar, matching the header's other icon-only controls. `AI Chat`
- The account menu (theme, Integrations, sign out) and the `Workspace settings` gear moved from the chat input's footer to the header, next to your avatar. `AI Chat`
- The admin/reader mode toggle inside an open chat is gone — the mode now follows how you opened the chat (the admin toolbar starts the builder, a site chat widget starts reader mode). `AI Chat`
- The Docsbook mark in the docs toolbar is now the project switcher, so you can move between projects from any documentation page. `AI Chat`
- `Preview` in a chat opened from your documentation now puts the chat away and hands the page back to the doc underneath, instead of navigating and losing the conversation. `AI Chat`
- The full-screen/side-dock toggle appears once a conversation has something in it, since an empty thread has nothing to watch beside the page. `AI Chat`
- Bringing a hidden conversation back restores the shape you hid it from, full screen or side dock, rather than always reopening as a side dock. `AI Chat`

### Fixed

- A workspace's forced light or dark theme no longer loses to the system theme in the AI chat and other admin surfaces. `Branding`
- Reopening a past conversation no longer restores it as a chat you cannot see, and the docs toolbar no longer shows `Chat` as active while a plain documentation page is on screen. `AI Chat`
- The side-by-side view no longer opens with a strip of empty space above the page header and subheader. `AI Chat`
- A step the assistant never finished no longer spins forever when you reopen the conversation: it is marked as interrupted and tells you to send the message again. `AI Chat`
- A conversation cut short by a dropped connection stays usable, where before every following message failed. `AI Chat`
- Expanding a step in the assistant's trail now always shows what it ran on and what came back, instead of opening onto an empty panel. `AI Chat`
- Steps in the assistant's trail now name what they did and what they found, such as the traffic numbers they read, rather than repeating the name of the operation. `AI Chat`

## NEW - 31.07.2026

### Added

- A Docsbook-hosted project can now be moved into a GitHub repository you own, straight from the chat header: Docsbook creates the repository and copies every page across in one commit. Note that the public URL changes and the move is one-way. `AI Chat`
- A GitHub button in the chat header shows where a project's source lives, and connects an account when there is none. `AI Chat`

### Changed

- The chat header now shows the Invite panel on every plan, with sending gated to Growth, so you can see collaboration before buying it. Inviting by email and creating an invite link sit in one place. `AI Chat`
- The chat's close icon is now a labelled `Preview` button that leads to your documentation site. `AI Chat`

## NEW - 29.07.2026

### Added

- Ask AI now works on a draft before you sign in — 3 free messages, then a sign-in prompt to keep chatting and save your site. `AI Chat`

### Improved

- The semantic doc index is now described by what it actually does for you: it is the biggest single improvement to AI chat answer quality, the chat answers from the exact section with the page cited instead of inventing one, and replies come back faster. `AI Chat`

### Fixed

- The project picker no longer offers a visitor without an account a "Connect GitHub" action that could not apply to them. `AI Chat`
- The Semantic Graph card on a plan below Business now opens a page explaining the feature before sending you to the price table. `AI Chat`
- Unlock cards now quote the real numbers instead of stale ones: your monthly AI budget in dollars rather than a query count, 15 supported languages rather than "50+", and the actual chat model and MCP tool counts. `Billing`
- The chat feature is now called `AI Chat` everywhere in the admin panel, instead of switching between "AI Agent" and "AI Chat" between screens. `AI Chat`

## NEW - 28.07.2026

### Added

- Growth and Scale can now work in the AI chat together: see who from your team is in the chat, invite a teammate by email, and watch the same answer stream in for both of you instead of relaying it through Slack. `AI Chat`
- Seven new analyses answer real business questions: the routes readers walk, where they leak out of a funnel you declare, reverse funnels from successful visits, W1/W4 retention, searches that got results but no clicks, rage signals, and any headline metric plotted over time. `Analytics`
- Filters are now a searchable multi-select dropdown per dimension, offered only where the current view supports them, and language is filterable for the first time. `Analytics`
- Chat is now a unit of analytics: questions from one reader group into a conversation, clicks on links the AI cites are tracked, and new conversation and intent views show what readers ask and why. `AI Chat`
- Business plans can now build a semantic index over their docs, so readers' chat questions find the right page by meaning even when it shares no keywords, plus a relationship graph of how pages connect. `AI Chat`
- Your custom questions now appear as clickable suggestion chips when a reader focuses the chat input, and adding a skill swaps them for that skill's own example questions. `AI Chat`

### Removed

- The separate AI Spend card is gone from the AI Chat tab. What the assistant cost you now sits as an expandable line at the bottom of `Conversations`, so the tab leads with what the chat did for your business rather than what it billed. `AI Chat`

### Fixed

- Answers in the docs chat now cite the pages they came from. Citations were previously empty on every answer, so readers had no way to jump to the source. `AI Chat`
- Free workspaces no longer see a "credit almost gone" warning on their very first visit, before spending anything. `AI Chat`

## NEW - 27.07.2026

### Added

- Paid plans no longer hard-stop when the monthly AI budget runs out — usage continues as metered overage billed on top of the subscription, up to a monthly cap you set yourself (default $20/month) from the Limits tab in workspace settings. `Billing`
- Per-model AI spend view showing what each call cost at the provider's real price. `AI Chat`
- Per-language coverage shows, for every page in your docs, how many are translated and current, how many are behind, and how many have no translation at all — so you can tell at a glance whether a language is genuinely complete. `Translations`
- Choose which AI model answers your readers, from Pro upwards. `AI Chat`

### Fixed

- Documentation corrected across pricing, plans, AI chat, API, and analytics pages, which still described token budgets, per-workspace billing, and analytics windows that no longer match the product. `Docs`

## NEW - 24.07.2026

### Added

- A case studies page, including a real look at how Docsbook documents itself, plus an ROI calculator that estimates support-ticket savings from self-serve docs and AI chat. `Marketing`

### Removed

- The discontinued one-time lifetime plan is no longer offered anywhere, including in AI chat upgrade prompts. `Billing`

## NEW - 18.07.2026

### Changed

- AI chat is now available on every plan, including Free — plans differ by the monthly AI token budget, not by a feature switch. `AI Chat`
- The chat now shows an upgrade prompt in place of the plan badge when you approach your limit. `AI Chat`

## NEW - 17.07.2026

### Added

- Plan badge in the chat input footer shows your current plan and remaining free credits. `AI Chat`

## NEW - 14.07.2026

### Improved

- "Create docs from a website" now generates a foldered 8-page site (features, guides, use-cases, FAQ) instead of 5 flat pages — a stronger starting point and a real FAQ page for AI-answer citability. `AI Chat`

### Fixed

- "Ask AI" bubble on text selection now flips below the selection instead of overlapping it when there's no room above. `AI Chat`

## NEW - 05.07.2026

### Added

- New `Business` plan — everything included in `Pro`, with higher AI chat, translation, and webhook limits. `Billing`

## 0.26.5 - 29.06.2026

### Fixed

- Free-text questions in the onboarding AI chat now render a text field so you can type your answer — previously a question with no preset options left nowhere to respond. `AI Chat`
- Single-option prompts like "Type your website URL here" now open a real input instead of submitting a placeholder value, so sources (website or repo URL) are captured correctly. `AI Chat`
- Creating docs from just an idea no longer stalls with a "process did not complete" error — the underlying request was being rejected; the onboarding chat now runs through to a published site. `AI Chat`

### Improved

- The chat now shows honest progress while creating your docs (reading your site, writing docs, publishing) instead of sitting silent during generation. `AI Chat`

## 0.26.4 - 12.06.2026

### Added

- Separate credit cards for AI Chat, AI Translations, and Visitor AI Chat usage in admin dashboard — granular view of token spend by feature.

### Improved

- Progress bar in credit cards now shows remaining credits instead of usage percentage — better visibility of available budget in `AI Chat Credits` and `Visitors AI Chat Credits`

## 0.26.3 - 11.06.2026

### Fixed

- **Limits card:** "Usage by source" bars now show each category's share of *actual spend* instead of a tiny fraction of the full budget ceiling — so you can see at a glance where your tokens go (AI Chat readers vs. Admin vs. AI Translations) and what to optimize.
- **Usage attribution:** When a workspace owner uses the docs-chat widget, their token spend is now correctly charged to the "Admin & AI Agent" category instead of inflating the "Readers (AI Chat)" bar — giving an accurate picture of how much visitors actually cost.

## 0.26.0 - 11.06.2026

### Added

- New `/chat` page with full AI agent for docs: search, edit settings, publish changes, and get answers — all in one conversation interface.
- New-chat `+` button in `/chat` header to reset conversation without page reload.

## 0.25.1 - 08.06.2026

### Fixed

- **Accessibility**: Added `aria-label` to 4 icon-only buttons in the AI Chat mock on the landing page — screen readers and WCAG 2.1 AA compliance restored

## 0.23.0 - 03.06.2026

### Added

- **Analytics**: Exclude internal (founder/admin) traffic from Axiom with `INTERNAL_IPS` env allowlist — single source of truth in `src/utils/analytics/internal.ts` with consistent IP extraction across all six ingest points (`/api/axiom`, server pageview logger, `/api/vitals`, `/api/_axiom/web-vitals`, `/api/analytics/{cta,feedback}`)

## 0.21.2 - 25.05.2026

### Fixed

- Hero badge animation on Safari/iOS: `@property` conic-gradient is not supported in Safari; added CSS fallback via `border-beam-rotate` keyframe + `@supports` guard so the animated border renders correctly on all browsers

## 0.20.0 - 25.05.2026

### Added

- SEO content hub — 20 new long-tail GEO/AEO blog posts in `docs/blog/` targeting AI search citation (ChatGPT, Perplexity, Claude, Gemini) and high-intent developer queries. Covers comparisons (Docusaurus vs Docsbook 2026, AI docs platform comparison, free hosting comparison, docs as code vs managed), AI infrastructure (`llms.txt` complete guide, JSON-LD for documentation, MCP server for documentation, docs-skills for AI agents, how to get docs cited by ChatGPT, Perplexity citations for docs, multi-language documentation SEO, AI chat build vs buy), migrations (GitBook → Docsbook, Docusaurus → Docsbook), and practical guides (custom domain how-to, API documentation best practices 2026, documentation analytics, README → docs site, why README-only projects need a docs site, best docs platforms for startups 2026). `docs/blog/README.md` restructured into five sections: Foundations, SEO & AI search (GEO/AEO), AI features, Comparisons & migration, Practical guides

## 0.19.0 - 25.05.2026

### Added

- MCP visitor activity drill-down — two new tools on PRO+ (`get_top_visitors` and `get_visitor_activity`) let AI agents investigate what one specific anonymous visitor actually did end-to-end. `get_top_visitors` returns the most active anonymous visitors with a stable hashed `visitor_id`, pageview count, country, and first/last seen; pass that `visitor_id` to `get_visitor_activity` to get the full chronological event timeline (pageviews, page feedback, CTA clicks) with paths and event-specific details (vote, query, href, heading, …). `get_page_journeys` also returns the same `visitor_id` so journeys can be drilled into immediately. `visitor_id` is `sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0,16)` — stable across sessions for the same person within one workspace, but raw IPs never leave Axiom

## 0.18.1 - 25.05.2026

### Changed

- Bento feature cards on the landing page now link to their corresponding documentation pages instead of `/connect` — `AI Chat` → `/docs/ai/chat`, `SEO Optimization` → `/docs/content/features/seo`, `Web Analytics` → `/docs/analytics/tracking/overview`, `AI Translations` → `/docs/translation/ai-translations`, `User Feedback` → `/docs/content/features/feedback`. Smoother funnel (visitor reads about the feature first) and internal-linking SEO boost

## 0.18.0 - 24.05.2026

### Added

- Ask AI on text selection — when readers highlight a snippet inside the docs, a floating `Ask AI` bubble appears above the selection; one click sends the selected text to AI Chat as a ready prompt. Tooglable per-workspace (Content tab in admin and `show_ask_ai_on_selection` in MCP `update_ui_settings`). On by default. Reduces friction for "explain this paragraph" / "rephrase this" use cases and pushes AI engagement
- Mobile Outline drawer — on screens <1280px the right-hand "On this page" panel is now reachable via a floating button in the bottom-left corner that opens a slide-up sheet with the same heading list and actions (scroll to top, ask AI, copy markdown, edit on GitHub, page feedback); desktop layout unchanged
- Month-1 transparency Twitter thread draft at `marketing/twitter-threads/2026-05-month-1-transparency.md` — 11-tweet build-in-public post (genre reference: @levelsio / @marc_louvion) covering hook with revenue, three things that worked (lifetime PRO, MCP server, llms.txt auto-generation), three that didn't (cold email, paid ads, feature bloat), AI chat numbers, and what changes in month 2; placeholders for MRR/lifetime revenue/conversion, character counts inline, posting checklist included

### Changed

- Moved "Get Support" out of the admin sidebar — replaced the bulky "Help & Support" section with a subtle "Need help? Contact support" footer link pinned to the bottom of the settings modal sidebar, freeing vertical space
- Reordered and trimmed the floating admin toolbar — now 5 quick-access buttons (Analytics, AI Chat, AI Translations, Design, SEO) instead of 6; removed setup-once entries (Custom Domain, MCP Server) and surfaced SEO, which was previously only reachable via the settings modal

## 0.17.2 - 23.05.2026

### Added

- `get_doc_graph` now supports `format` parameter: `"toon"` (default) returns a compact text tree ~10x smaller than JSON with `@canonical/ref` syntax that LLMs parse natively; `"json"` preserves the previous full structured response for programmatic clients

## 0.17.1 - 23.05.2026

### Fixed

- Prevent race conditions in monthly usage limits for `AI Chat`, `Translations`, and `Reindex` — concurrent requests could each pass a stale pre-check and push counters past the plan limit (visible as `78/50` pages translated on Pro). Replaced check-then-act with atomic conditional `UPDATE ... RETURNING` in `batchTranslate`, `/api/ai-chat`, and the MCP `reindex` endpoint

## 0.17.0 - 23.05.2026

### Changed

- Fix system theme not applying correctly due to shared `localStorage` key across workspaces

## 0.16.3 - 23.05.2026

### Fixed

- Neutralize green styling on "Get Support" button in workspace settings sidebar — now matches the muted look of other navigation items

## 0.16.1 - 22.05.2026

### Added

- New `/start` page replaces the `LivePreviewExpanded` modal on "Start for free" — logo, GitHub URL input, Sign in with GitHub, email/Discord support links, social icons, hero-style shards background, cascade animations

## 0.15.1 - 22.05.2026

### Added

- Animated counter above the AI chat mock on the landing page, counting up over 6 seconds
- Figures on the `SocialProof` tabs of the landing page, including the 15 supported languages

## 0.15.0 - 22.05.2026

### Added

- `Get Support` tab in admin panel with email, Discord, and Twitter contacts
- Email support link in landing `Footer` for quick access to `support@docsbook.io`

## 0.14.0 - 20.05.2026

### Improved

- Follow-up question suggestions after each AI response in `AI Chat`
- Animated "Thinking…" indicator while AI is generating a response in `AI Chat`
- Share and Copy as Markdown buttons, plus a Report Issue option in `AI Chat`
- Smoother entrance animations on the `AI Chat` welcome screen
- Source of Truth automatically enabled for Enterprise workspaces in `AI Chat`

### Removed

- DeepSearch and References toggles from `AI Chat` — simplified to core Q&A

## 0.10.0 - 15.05.2026

### Improved

- Page feedback ratings moved into the Events section in `Analytics`

### Fixed

- AI chat responses now appear in `Chats Analysis` analytics

## 0.7.0 - 11.05.2026

### Added

- Custom background color support for individual header navigation links

## 0.5.0 - 10.05.2026

### Improved

- `Copy Page` button redesigned with modern styling and check icon feedback on copy

## Related

- [Full Docsbook changelog](../../CHANGELOG.md) — every release, on every axis
- [Changelogs by outcome](./README.md) — the other eleven numbers a release can move
- [Changelogs by panel section](../README.md) — the same releases, cut by where they landed

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
