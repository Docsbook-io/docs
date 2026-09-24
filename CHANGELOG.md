---
title: "Docsbook Changelog"
description: "Release notes for Docsbook — new features, improvements and bug fixes to the AI-powered documentation platform, newest first."
layout: changelog
status: generated
version: "0.10"
---

# Product updates

New features, improvements and bug fixes in Docsbook — newest first. Each update has its own page; filter by type or by the part of the product it touches.

## 2026-09-20 — Watch an agent task while it works

Every action a documentation task takes is now a line on a live timeline, private repositories open and stay private, and the panel finds your GitHub repositories and organizations the moment you sign in.

### New releases

- **The sidebar lists your GitHub repositories, not only the projects you have already made.** Pick one and the new-project form opens with it chosen, so connecting a repository is a click on the repository itself instead of a trip through a second picker. `Panel`
- **Your GitHub organizations show up the moment you sign in**, whether or not anything has been filed into them yet, so a new account can open the company it works under instead of only its own profile. `Panel`
- **You can watch a documentation task work, step by step, while it is still working.** A run takes minutes, and the only sign of life was one line of progress that the next one overwrote, so "what is it doing right now" had no answer anyone could check and an assistant asked it would describe what an agent probably does. Every action a task takes is now a line in an ordered timeline you can follow as it happens: the pages it reads, the pages it writes, the translations it runs, how long each took and whether it worked. `Agents`
- **Anyone can see the documentation work done on a public project, with no account and no token.** The project's own endpoint now answers what the agent has been doing on it, so a reader deciding whether your docs are maintained can look instead of guess. It shows the work and not the business: what you asked for, what the agent reported back to you, your analytics and your settings are not in it, and a private project's work stays private. `MCP`

### Improvements

- **Starting a documentation task now tells you it can be watched live and asked about while it runs**, instead of only pointing at a status check. The tool that hands a job over used to read like a script to wait; it now names the live timeline and lets you send the agent a question mid-run rather than only after it asks you one. `Agents`
- **Agent runs are billed for the work they did, not for how long they took.** A run that read four pages no longer costs what a run that rewrote the site costs, and a run waiting on your answer no longer bills you for the wait. Pricing is per token with the session fee kept for the per-run machinery; the previous monthly free-run allowance is gone, since under a token meter a free run has no size. `Agents`
- **The admin chat resolves your project itself, instead of asking first.** Opening it used to start with a dropdown of every workspace you can reach — your own, your organization's, anyone's you collaborate on — before it would take a question. It now picks the project from what you say in the message, or the one you already have open, and shows which one it picked; the corner button is a plain icon now, since everyone who can see it is already signed in as the admin. `AI chat`
- **Visit Website moved from the panel's header to its sidebar.** It is a plain row now, sitting just above the account and organization switcher at the bottom of the sidebar, instead of a highlighted button in the top-right corner. `Panel`
- **The Spend tile is off Analytics' headline strip.** The row now reads Visitors, Revenue, Conversion rate and the rest, without it. `Analytics`
- **Turning on the autonomous growth agent now needs this project's own paid plan, not trial credit.** It runs hourly and unwatched, which made it the fastest way to burn through a trial's free sample; its settings dialog now makes the business case for what it actually does, and sends you to the Plan page instead of arming it if you try to turn it on without a subscription. `Pricing`
- **Three Analytics reports moved to the tab that answers their question.** AI Views — which assistants and crawlers fetch your docs — sat on the Insights tab, three scrolls below the human-traffic cards it was being compared against and one tab away from the report on whether an AI answer actually names you; the two now sit together. The docs-assistant conversation breakdown sat at the foot of the page-traffic report; it now lives on the Chat tab, beside the KPI tiles that already summarised the same conversations. The per-reader table (who came, when, what they read) moved out of Analytics into Logs. `Analytics`

### Bug fixes

- **A private site whose repository Docsbook hosts is now actually private everywhere.** Switching visibility to Private closed the site behind an unlock screen, but if Docsbook hosts your documentation's repository for you, that repository could still sit open on GitHub — readable and cloneable by anyone, outside your own GitHub account entirely. Going private now closes that repository too, and refuses the change with a reason if it can't. A site built from your own GitHub repository was never affected: Docsbook has never changed your repository's visibility either way. `Privacy & access`
- **Documentation kept in a private repository now opens.** Granting the Docsbook GitHub App was enough to let Docsbook publish to a repository but never to read one, so a private project sat on "your docs are deploying" and its AI answered as though the pages did not exist. Docsbook now reads with the installation you granted, and a private site serves without anyone handing over a personal access token. `Sources`
- **A repository Docsbook cannot read now says so, and names what would fix it.** It used to report the project as having no documentation at all, so an assistant asked about your docs confidently said there were none, and you went looking through your pages instead of at the one access setting that was wrong. `MCP`
- **Granting Docsbook access to an organization now takes effect straight away.** The switcher only knew about organizations that already held a project, so re-granting access on GitHub looked like it had done nothing. Docsbook asks GitHub directly now, and a fresh grant is on screen at the next sign-in instead of after a wait. `Onboarding`
- **An empty repository list now says which of the two things is wrong** — no GitHub connected, or a sign-in that cannot see private repositories — and offers the one button that fixes it. Most of a company's repositories are private, so "nothing here" used to read as a grant that had failed. `Panel`
- **The Assistant, Analytics, Customize and Settings shortcuts on the doc toolbar now open beside your doc instead of replacing it.** Clicking one used to leave the page you were reading and load the dashboard in its place, so getting back meant the browser's back button. Each shortcut opens in its own tab now, and the doc you were reading stays exactly where you left it. `Panel`
- **A conversation started from the floating Ask Docs button now stays docked to the corner it opened from**, as a small widget-style card (a full-width sheet on mobile), for the rest of that conversation. It used to hand off to the same full-viewport view every other entry point uses the moment you sent your first message. Every other way to open chat — the header's Ask AI, a pending search or outline query, the admin toolbar, `?chat=1` — is unchanged. `AI chat`
- **The install link every agent task uses to enable its live timeline can no longer be taken over by a project name.** That link reached the install script by a coincidence of routing rather than by design; a project created with that exact name would have silently broken every agent task's step-by-step timeline afterward, with nothing anywhere saying why. That name is now reserved and can never belong to a project, the same way a handful of other system paths already are. `Agents`
- **A collaborator invite now links straight to the docs, not only to the sign-in-gated accept page.** Deciding whether to join a project used to mean creating an account first and looking around after; the invite email now also opens the documentation site itself. `Collaboration`
- **The trial-wallet warnings this page promises now actually fire.** A trial without an expiry date (running since 15 September) never triggered its 50%, 75% and 90% notices — a field-name mismatch made every one of them silently read as not running a trial at all, for the five days between shipping and this fix. `Pricing`
- **The Feedback tab in Logs now shows the same empty state as every other tab on the strip when there is nothing to show**, instead of a plainer placeholder of its own. Its **Fix it** action now opens the admin chat directly. `Logs`

## 2026-09-20 — A translated site, translated all the way through

The menu, the buttons, the metadata search engines read and the AI panel now follow the reader into their language, so a French page no longer sits inside an English site.

### Improvements

- **A project paying with its own translation key is no longer stopped when the shared pool runs out.** Bringing your own key is the product's answer to an exhausted shared quota, and it now holds at every step of a translation run rather than only at the last one. `Translations`
- **`llms.txt` names the languages a site publishes**, and shows what a translated address looks like, so an assistant asked "is there documentation in German" can answer from the one file it is pointed at. `SEO`

### Bug fixes

- **A translated page is now that language all the way through.** The menu, the breadcrumbs, the buttons in the header, the subheader tabs and the AI panel's suggested questions were staying in the original language next to a fully translated article — a French page with an English sidebar. They are translated now, and a reader stops having to navigate a site in a language they did not choose. `Translations`
- **A translated page now tells search and AI engines what it says, in the language it says it in.** Its title, its description, its social card and its structured data were all still English under a French URL, so an assistant asked about your French page quoted the English sentence and a search result listed the English one. All of them are taken from the translated page itself. `Translations`
- **Ask Docs and the language picker speak the reader's language.** Both were English on thirteen of the fifteen languages we offer, on sites that were otherwise fully translated. The rest of the furniture — "Updated", the theme picker, the menu and AI-panel controls — is translated too. `Translations`
- **A page in Arabic reads right-to-left**, and a screen reader is now told which language it is reading instead of announcing every translated page as English. `Translations`
- **Publishing one new page no longer sends the whole site's menu back to the original language** while it waits for the next translation run. `Translations`
- **A project reached at a differently-capitalised address is no longer treated as a different project**, which used to cost it its translated menu without anything looking broken. `Translations`

## 2026-09-19 — An Overview that answers "is everything all right?"

The panel opens on four cards again — the live site, the commit it serves, the agent and what the AI engines did this week — and the sidebar tells projects and organizations apart at a glance.

### New releases

- **The panel opens on an Overview again** — first row in the sidebar, four cards, no scrolling: which site is live and on what address, the commit it is serving and who pushed it, whether the agent is armed, what the AI engines did this week, and whether readers arrived. The question "is everything all right with my docs" is now answered by looking, not by opening four sections. `Panel`
- Your site's card carries the last commit's message, its short hash and its author, so **"did my push go live?" stops being a trip to GitHub**. `Panel`
- A new **Edit** button beside Visit opens your documentation in edit mode with nothing else on screen — click a block and change it, no chat rail taking half the window. `Panel`
- The **+** beside Domains goes straight to setting up your own domain, instead of a line of text telling you that you have not got one. `Panel`
- Each project now wears **its own icon** in the panel's project switcher — in the list and on the open project alike — so telling six sites apart is a glance instead of a read. A project that has set no icon gets a folder. `Panel`

### Improvements

- The Overview's AI card splits crawler traffic into **AI answers, Indexing and Training**, so "an assistant read us while answering somebody" is no longer averaged in with "a model swept us for training data". `Analytics`
- A reading that could not be taken now shows as a dash rather than a zero, and a week-on-week figure with no previous week to compare against shows no percentage at all — **nothing on this page is a number nobody measured**. `Analytics`
- **The bottom of the sidebar names the organization you have open**, not your own account, so the one label on screen agrees with the row ticked inside the menu. `Panel`
- **An organization's dashboard keeps that same organization switcher at the bottom** instead of turning into a static name, and its sidebar header now lists that organization's projects — so the panel answers "which project" and "which organization" in the same two places wherever you are. `Panel`
- A header link now has a **New tab** toggle, so you can keep readers on the current tab for a link that used to force a new one open (and vice versa) instead of that always being decided by whether the URL is external. `Design`

## 2026-09-19 — A new project in about a second

Creating a site runs no AI any more: pick one of 32 templates, paste your website for branding or import a repository, attach what you already have — and the site is readable the moment it exists.

### New releases

- **Creating a project now happens on your dashboard, under the team it belongs to**, instead of on a screen of its own: your repositories on the right, the sidebar still on the left, so you can see which owner the new site is being filed under before you make it. If you have no repository — or no GitHub at all — **New repository** is the first row and we host one for you. `Onboarding`
- **Creating a project runs no AI and finishes in about a second**: pick from 32 hand-written templates (API reference, on-call runbook, help centre, contributor guide, blank), paste your site's address for instant branding, or import a GitHub repository (searched across your organizations, nothing written into it) — the site is readable the moment it exists, and writing with AI is still one screen away when you want it. `Onboarding`
- **Template cards show the site they make.** Each one draws a live preview from the template's own pages — the navigation, the headings, where the tables and code blocks fall — and names every page it will write, so you can tell an API reference from a help centre without creating either. The last tile opens the whole catalogue, searchable. `Onboarding`
- **Attach what you already have while creating**: documents become pages, and screenshots you take on the spot are committed to your repository as images you can drop into any page. Both optional, several at a time, removable before you press Create. `Onboarding`
- New content blocks — a **stats** band, a **hero** with buttons and a code panel, cards with **New**/**Beta** pills, and a full **footer** — so a docs homepage can read as a product page instead of a table of contents. `Content`
- Drop a folder of PDFs, Word docs, Markdown or plain text into a new or existing project and each file becomes a searchable, answerable page (Integrations ▸ Files). `Integrations`

### Improvements

- The new-project form carries **no instructions to read** — every block is one word and an ⓘ, so the explanation is there when you want it and out of the way when you do not. `Onboarding`
- **Signing up asks you nothing.** There is no questionnaire between creating an account and using the product any more: you land in your panel, with the new-project form already open and your repositories in front of you, so the first thing you do here is the thing you came to do. `Onboarding`
- **Name your project as you create it, and see the address it buys.** The field checks the name while you type and shows the site's address under it, so you find out that a name is taken before you press Create rather than after — and a name you chose is never quietly turned into another one. `Onboarding`
- **Start free** opens sign-up on the page you were reading instead of taking you off it. `Onboarding`
- The integrations you want wired up are now picked while creating the project, from the same catalogue the panel shows. `Integrations`

## 2026-09-19 — Agents you write, arm and hear back from

Write an agent with its own prompt, wake it on a saved feed or a GitHub event, and have every finished run reported to Slack, Discord or a webhook in the agent's own words.

### New releases

- **Write your own agent.** New agent in the Agent section gives it a name, an icon, a line about what it buys you and — the point — its own prompt, so the one job peculiar to your project stops being something you remember to do by hand. `Agents`
- **Arm a job on a saved feed**, so an agent runs when a class of log lines matches rather than only on a clock or one named event: save the filter in Logs, pick it under Runs, and nobody has to watch the stream. `Agents`
- **A job can now be woken by your GitHub repository, and it actually goes off.** Pick the repository under Runs ▸ Connected app — the list is what you granted Docsbook, not every repo you own — and the agent runs when commits land, a pull request merges, a release is published, a spec file changes, an issue gets a label or somebody opens a discussion. Until now a card could sit switched on and watching for weeks while nothing ever asked GitHub. `Agents`
- **An agent job can now report where you already work.** Tick the Slack channel, Discord channel or webhook in its settings and every finished run arrives there, so nobody has to open the panel to find out whether the night's pass did anything. `Agents`
- **Ask the Docsbook agent to set all of this up.** It can now see what your project runs, write a new agent with its own prompt and trigger, save a feed to arm it on, point its report at a channel, and hand you the one link that connects GitHub or Slack when the job needs an app you have not attached. `MCP`

### Improvements

- Agent jobs now switch on from the card itself, and their settings are one short dialog: what you want done — with what to measure and what a good result looks like already drafted for you — an optional line of your own, and what sets it off: a schedule, or something that happens on your site, like a reader marking a page unhelpful. `Agents`
- **A trigger that cannot fire now says so, instead of looking like a quiet week.** Its settings show when it was last checked, when it last woke the agent and what went wrong if anything did — and arming it on a repository your GitHub account has not granted is refused on the spot rather than saved as a card that can never go off. `Agents`
- An agent you switch on **stays under Discover with its switch on** rather than vanishing from the tab you turned it on in, so the press you just made is still on screen to confirm. `Agents`
- **A notifier now says what it sends, and lets an agent write it instead.** Tick a job under Written by and your Slack or Discord channel gets the agent's own two sentences rather than a field dump nobody reads. `Feeds`
- **An agent that finds work now does some of it in the same run.** Filing an issue is a note for what is left over, not the end of the pass, and a figure it could not read is a line in its report rather than a reason to leave the page unwritten — so a morning's run comes back with a change to look at, not only a list of things somebody should do. `Agents`

### Bug fixes

- A job whose work runs in the background reported `{"task_id":"…","status":"queued"}` to your channel every morning while the write-up it produced minutes later went nowhere. The report now waits for the run and carries what the agent wrote, and the card stops showing the start of its last run forever. `Agents`
- A Slack hook serving three feeds appeared three times in a job's destination picker with no way to tell which to tick. One destination is now one choice. `Agents`
- The Autonomous agent card showed two glows at once, a spectrum-cycling sweep and a separate accent one — it's now a single accent glow in the top-left corner. `Agents`

## 2026-09-19 — The Inbox becomes a conversation

Every letter has a reply box that puts the project's agent on the thread, and the mailbox stopped filling up with notices that a job simply ran.

### New releases

- **The Inbox is a conversation now.** Every letter — a run that failed, an audit that came due, a question the agent wrote — has one reply box under it, and sending your answer puts the project's agent on the whole thread: it answers you in the same letter, and does the work when you ask it to, so deciding something no longer means leaving the mailbox to go and do it. `Inbox`
- **Write a letter of your own** from the Inbox: a subject, what you want done, and the agent picks it up there. The panel needed no second chat window for this. `Inbox`

### Improvements

- A thread you have already read comes back **unread the moment the agent answers into it** — and stays read when the turn was yours, so the mailbox never nags you about your own sentence. Archived letters and bringing one back still work as before. `Inbox`
- Letters are written in Markdown throughout, so headings, lists, links and code read the same whoever wrote them. `Inbox`
- The unread count in the sidebar is a plain number rather than a coloured pill — which also fixes it being invisible on projects with no accent colour set. `Inbox`
- **Your mailbox stopped reporting that the machine ran.** A job that finishes well no longer writes "…finished" into the Inbox — on an hourly agent that was twenty-four unread notifications a day, with the one letter that mattered buried under them. What arrives now is a run that FAILED, a reading that came due, or a letter the agent chose to write you in its own words. Whether a pass went off is still on its own row in Agent, where it is a fact to look up rather than something to dismiss. `Inbox`

## 2026-09-19 — MCP, feeds and integrations, tightened

Docsbook's own manual moved to the address people type, MCP tools gained plain REST endpoints, every feed became a tab in Logs, and a batch of GitHub and Integrations rough edges is gone.

### New releases

- `read_doc` and `get_doc_outline` are public over MCP now, and **Connect MCP** is one item in every published page's Copy menu — so a reader's agent can open the exact page a search returned instead of guessing from its title. Docsbook's own manual is readable the same way. `MCP`
- Read-only tools on your MCP owner surface now have their own `GET /api/v1/<tool>` endpoint, and a narrow set of settings tools (branding, navigation, the chatbot, translation mode, mention tracking) their own `POST` — no MCP client, no wrapping args object. `MCP`
- New **AI crawler activity** feed: every page an AI or search crawler fetched from your docs, each row priced at the real crawl rate rather than a generic per-visit figure — proof of what's actually paying for your citations. `Feeds`
- A **Live** toggle on the feed pauses its own re-polling, for reading a fast-moving feed without rows shifting under you. `Feeds`

### Improvements

- **Docsbook's own manual now lives at the address people type** — `docsbook.io` serves it directly instead of bouncing to `/docs`, so a link you paste, a canonical URL and a result in search all point at the same page. A site Docsbook hosts for you moved with it, from `docsbook.io/<project>` to `<project>.docsbook.io`, and its old links redirect there; a site you publish from your own repository keeps the address it had. `SEO`
- A long, multi-topic question is now searched part by part and the results fused, instead of being averaged into one point that lands between all of them. `MCP`
- Every feed — built-in presets, your saved lists, New list — is now a tab right next to Chat and Feedback in Logs, with no separate Activity tab to open first. `Feeds`
- Opening Logs for a whole organization with no project picked now merges every project's feed into one list, labelled by project, instead of asking you to open one project at a time. `Feeds`
- Integrations' catalogue of 2,500+ apps now shows up as cards right in the grid instead of behind a search screen, and connecting one of them no longer fails at the authorization window. `Integrations`
- A connector switched off for the whole deployment now names the piece that is missing, instead of reporting the app directory as the cause on a card that does not use it — so the person who can switch it on is told what to switch on. `Integrations`
- Integrations opens straight on Discover now, and the Skills tab is gone — one screen, no tab to pick between what's connected and what could be. `Integrations`

### Bug fixes

- The public MCP endpoint had been silently dropping three of its ten advertised tools; the support widget meant for us was leaking onto published docs. `MCP`
- The tool catalog at docsbook.io/mcp had silently narrowed to 16 tools instead of the real ~162, and several tool pages documented a REST call that would 404; both now reflect what actually runs. `MCP`
- Connecting GitHub from Integrations could open a window with no app selected instead of GitHub's own install screen — it now always goes straight there. `Integrations`
- A GitHub app you had **already installed** stayed invisible to the project, because GitHub only reports a first install and says nothing when you grant access a second time. **I have finished** now asks GitHub which installations are yours and attaches them, so granting access once is enough and nobody has to guess why the card still says not connected. `Integrations`
- Opening an issue or pull request covered the whole panel, sidebar and header included, instead of just replacing the list you opened it from — it now swaps only that section's body, the same way an MCP tool's own page already does. `Issues`
- That same issue or pull request then stayed on screen when you switched sections, so Analytics or Settings never appeared under it. An open record is the page of the section you opened it from — switch away and you get the section you switched to, come back and it is still there. `Issues`

### Removed

- The Change Log button and the per-section release-note pages it opened are both gone — this single page is now the whole changelog. `Changes`

## 2026-09-18 — Organizations, and one grid of integrations

Make a team in one click and buy one plan for all of its projects, see everything a project is wired to in one grid, and let pages carry a review status an agent can respect.

### New releases

- **Organizations**: make a team in one click, invite someone once for access to every project in it, and buy a single plan for the whole team instead of per project. `Organizations`
- **Integrations** is now one grid of everything a project is wired to — 14 built-in connectors plus 2,500 more by search, several accounts per service, and 29 occasions that can wake an agent. `Integrations`
- Issues and pull requests are now one list, filterable with GitHub's own syntax, each row carrying the outcome it claims to move and how much of that claim actually landed — plus a comment box that puts the assistant to work on the thread. `Issues`
- Documentation pages can now carry a status — `draft` → `review` → `approved` → `locked` — so an agent knows which pages are actually signed off before it builds on them; only a person, through `set_doc_status`, can approve or lock one. `MCP`
- Three new built-in feeds (Content gaps, Conversions, Plan & usage) and a Skills gallery for installing or writing your own agent playbooks. `Feeds`

## 2026-09-15 — A crawl budget, and a trial that runs until its wallet is spent

AI and search crawlers now draw on a monthly budget, the free trial ends when its AI wallet does rather than on a date, and Enterprise got a self-serve price.

### New releases

- Two new content blocks: **callout** for the one sentence a reader must not miss, and a **code group** that tabs one example per language instead of stacking four. `Content`
- A floating **Ask Docs** button, and a landing-page mode for your home page — hide the sidebar and outline and let the content run full width. `Content`
- `docsbook_assistant` (renamed from `ask_docsbook`) is now reachable over plain REST as well as MCP, and can also answer questions about Docsbook itself, not only your own docs. `MCP`

### Improvements

- AI and search crawlers now draw on a monthly crawl budget (a free allotment on every plan, then $0.30 per 1,000 pages) instead of being served for nothing, with usage shown in the panel and a `usage.limit_approaching` webhook to match. A reader an AI assistant sends you is never counted. `Pricing`
- The free trial no longer expires on a clock: a project runs on Pro until its AI wallet is actually spent, then pauses — with warnings at 50%, 75% and 90% — instead of quietly going dark. `Pricing`
- Enterprise now has a self-serve price, **$100/month per repository**, with the balance owned by the project rather than by one person. `Pricing`

### Bug fixes

- Connecting the MCP server for the first time led to a 404 instead of sign-in; SEO/GEO markup wasn't reaching two-thirds of projects because the switch that controlled it is gone — both are on by default now. `MCP`

## 2026-09-14 — SEO, GEO and AEO on for every project

Canonical URLs, sitemaps, JSON-LD, TL;DRs and FAQ markup ship by default with nothing to switch on, and audits became a ranked list of searches you do not win yet.

### New releases

- A new **Agent activity** view shows every call an agent has made, read as a conversation, with one-click scheduling from hourly to daily. `Agents`
- Audits became **Opportunities**: a flat, ranked list of searches you don't win yet, each with the competitor holding it today and what winning it would be worth. `Overview`

### Improvements

- SEO, GEO and AEO markup now ship on by default for every project — canonical URLs, sitemap, JSON-LD, a TL;DR, FAQ/HowTo markup — with nothing to switch on. `SEO`

### Removed

- Removed the Reminders tools and tab — a hypothesis already carries its own check-in date — and the now-redundant `update_seo`/`update_geo`/`update_aeo` tools. `MCP`

## 2026-09-13 — Translations on your own pipeline, and forecasts on every change

Docsbook watches for pages that fall behind and hands the translating to whatever you register, and a docs change can carry a forecast that is checked against the result later.

### New releases

- A docs change can now carry a forecast (`add_hypothesis`) with a verdict recorded against it later, so "did that rewrite actually work" is answered by the record instead of by memory. `MCP`
- A pull request can be held for your decision when it touches a question you haven't answered yet, even on projects that publish automatically. `MCP`

### Improvements

- Translations moved off Docsbook's own AI budget by default: Docsbook watches for pages that fall behind and hands the actual translating to whatever you register over a `translation.needed` webhook. `Translations`
- Goals, Questions, Memory and Reminders became one card with four tabs; Issues and Pull Requests became another. `Overview`

## 2026-09-12 — One consulting agent instead of 176 tools

The MCP surface was rebuilt around one agent that hands back the steps, the tool for each and what would make the answer wrong — and it now remembers your project between sessions.

### New releases

- The MCP surface was rebuilt around one consulting agent — **`docsbook_expert`**, with a build partner **`docsbook_assistant`** — replacing 41 standing-agent routes and 135 narrow action tools. Ask it anything about your docs and it hands back the steps, the exact tool for each, and what would make the answer wrong. `MCP`
- Docsbook now remembers facts about your project between sessions (`list_memory`/`add_memory`), and keeps every past reading so a rewrite can be measured against a real baseline instead of a guess. `MCP`

### Improvements

- A project with no GitHub repository is no longer turned away — Docsbook can work from your website, a single page, or a couple of sentences about your product. `MCP`
- The Doc Graph now draws immediately from cache instead of waiting on a similarity query, and its Meaning edges are measured between pages rather than spent entirely on one long page's own headings. `Doc Graph`

## 2026-09-11 — Custom agents and AI Mentions

Build an agent from your own allow-list of tools, and check on a schedule whether Google's AI Overview, Google and Bing name your docs for the questions you care about.

### New releases

- Build a custom agent from your own allow-list of MCP tools and a plain-English prompt. `MCP`
- **AI Mentions**: ask Google's AI Overview, Google's results page and Bing whether they name your docs for the questions you care about, checked on a schedule instead of by hand. `GEO`

### Improvements

- The free trial gained its own $20 AI wallet, spent before anything you've paid for; a card added mid-trial is only charged once the trial would have ended. `Pricing`

### Bug fixes

- Fixed a week-long gap, from 4 September, where AI spend stopped reaching the usage ledger entirely. `Feeds`

## 2026-09-08 — Team chat invites work again

A one-line fix for teammates who could not be invited into a project's AI chat.

### Bug fixes

- Inviting a teammate to a project's AI chat was permanently failing with "temporarily unavailable." `AI Chat`

## 2026-09-05 — Invoices you can read, and changes that score themselves

Billing became a real invoice list with staged overage warnings, every pull request scores its own outcome, and semantic search is on for every plan.

### New releases

- Billing is now a real invoice list — what's owed next, whether the current invoice is paid, every past charge as its own line — with five staged overage warnings (75/85/90/95%/cap) and matching webhooks. `Pricing`
- Every pull request now scores itself out of 100 — readers served, reach, cost to run, edit quality — with the movements behind it, so whether a merged change worked stops depending on somebody remembering to check. `Changes`
- The Doc Graph gained read-depth coloring, a Dead ends overlay, and now shows the open pull requests and issues already touching a page you click. `Doc Graph`

### Improvements

- Semantic search (`search`) is on every project now regardless of plan, so a question an assistant asks of your docs is answered instead of refused. `MCP`
- The docs were reorganized by capability — SEO, GEO, AEO, agent-ready content, chat, analytics, translations — each page stating how the feature is built and what isn't proven yet. `Documentation`

### Bug fixes

- Overage could be pushed past the $200 cap the pricing page promised; a project on a declined card kept accruing new overage instead of spending down its existing credit. `Pricing`

## 2026-09-04 — Check prior work first, and AI markup cut to +70%

Agents now ask "have we already tried this" before proposing anything, and the markup on AI usage dropped from +900% to +70% of the provider's price.

### New releases

- Two tools answer "have we already tried this" before an agent proposes anything (`search_prior_work`, `get_pull_request`), and fifty-four capabilities now run that check first. `MCP`

### Improvements

- AI usage markup cut from the provider's real price **+900%** to **+70%**, in the same dashboard breakdown. `Billing`

### Bug fixes

- The AI-spend ledger had been under-reporting by 17%, because it read a balance from the row it had just rewritten instead of the one it started from. `Billing`

### Removed

- Removed the **Prompts** section — a prompt you used to copy-paste into your own tool is now either a scheduled Agent or the one worked example already on a tool's own page. `MCP`

## 2026-09-03 — A page and a history for every MCP tool

Each tool has its own address with every call it served — cost, latency, input and output — and the project row stopped leaking through tool answers.

### New releases

- Every MCP tool now has its own page and address, with full call history — cost, latency, what went in and what came back. `MCP`

### Improvements

- Page feedback ("Was this page helpful?") now shows on mobile, where the old sidebar version never rendered. `Page Feedback`

### Bug fixes

- `list_workspaces`/`get_workspace` and fifteen `update_*` tools stopped returning the raw project row, including a live API key and a 2.1MB semantic-index blob. `MCP`
- A billing-rollover bug had zeroed 399 projects' carried balances while still showing the money as available; page titles and meta descriptions were being built from the wrong source. `Billing`

## 2026-09-02 — GitHub issues inside the panel

Your repository's issues, with an action per row and the same tools over MCP — and per-tool pricing cheap enough to call in a loop.

### New releases

- **Issues**: the GitHub issues on your repository, inside the admin panel, with a Start/Audit/Verify action per row and `list_issues`/`get_issue`/`create_issue` over MCP. `Issues`

### Improvements

- MCP agent pricing moved from a flat $0.25/call to per-tool pricing ($0.074–$0.245), cheap enough to call in a loop. `MCP`

## 2026-09-01 — Sources: what your docs may read from

Connect GitHub, your website, Notion, Zendesk and two dozen more by pasting an address.

### New releases

- **Sources**: what your docs are allowed to read from — GitHub, your website, Notion, Zendesk and two dozen more — connected by pasting an address, one row per connection. `Sources`

## 2026-08-31 — August: analytics around revenue, and drafts before sign-up

The month in one release — analytics rebuilt around revenue, feeds turned into a real event and webhook system, and a live draft site before you have an account.

### New releases

- Analytics was rebuilt around revenue: six headline figures (visitors, revenue, conversion rate, revenue per visitor, bounce rate, session time), and every breakdown — Pages, Referrers, Channels, Countries, Languages, Devices — rankable by Revenue as well as by Visitors, plus a live "Now" mode. `Analytics`
- Feeds became a real event and webhook system: saved lists, per-tool and per-event filtering, notifiers you attach to any list, a Usage breakdown of what AI and MCP spend actually went on, and CSV/JSON/NDJSON export. `Feeds`
- Sign-up was rebuilt around instant drafts: paste a URL, a repository or a sentence and watch a real site build live, with its own admin panel before you have an account. `Onboarding`
- Translations gained a page per language: coverage, staleness, cost, and a reader map by country; a push that changes a page now re-translates it automatically within your budget. `Translations`

### Improvements

- Every commit now scores itself out of 100 the day it lands — readers served, reach, cost, edit quality — with SEO position and before/after cost tracked alongside it. `Changes`
- Contextual **Improve**/**Analyze** buttons landed across Analytics, Users, Chat and Changes, so any number on screen can hand itself to the assistant. `AI Chat`
- Every empty panel card now shows sample data with a guided "Turn on" walkthrough instead of a blank box. `Panel`
- MCP calls became billed per call in the background against your project balance, with the whole catalogue browsable as one searchable, filterable table. `MCP`
- A public content-widget gallery, each block switchable off per project; the interactive API-reference widget now follows your brand's colors. `Content Widgets`

## 2026-07-31 — July: private sites, new plans and a chat API

The month in one release — password and SSO-protected sites, Growth and Scale plans, real Search Console rankings and a public REST endpoint for a project's AI chat.

### New releases

- Anonymous, no-account docs generation at `docsbook.io/create` — paste a URL, a repo or an idea and get a live draft with AI chat before signing up; signing in publishes it exactly as it stands. `Onboarding`
- Workspaces can be made private, behind a password or your own SSO (Google Workspace, Microsoft Entra ID, Okta). `Privacy & Security`
- Two new plans, **Growth** ($349) and **Scale** ($899), plus 20%-off annual billing on every paid plan. `Pricing`
- Analytics Explorer replaced the raw event feed: charts, click-to-filter facets, funnels, retention, and bot-traffic filtering — crawlers had been up to 93% of pageviews on some sites. `Analytics`
- **Translation Activity**: per-page, per-language coverage and staleness, with one-click re-translation of just what changed. `Translations`
- Multiplayer AI chat on Growth/Scale — a teammate sees the same answer stream in live, instead of a relay. `AI Chat`
- A public REST endpoint, `POST /api/v1/chat`, for calling a project's AI chat from your own backend. `API`

### Improvements

- AI usage is billed in real dollars against a per-plan monthly budget, with metered overage instead of a hard stop when it runs out. `Billing`
- Real Google Search Console rankings landed in SEO & GEO, with no OAuth needed on a `*.docsbook.io` subdomain. `SEO`
- The semantic doc index — meaning-based chat answers with page citations — shipped for Business-and-up plans. `AI Chat`

## 2026-05-01 — Docsbook launches

Docsbook launched in May 2026 as a documentation site generated straight from a GitHub repository: hosting, theming, translations, an SEO panel, and an MCP server for AI-assisted editing.

### New releases

- **The admin AI chat** (`/chat`) arrived in June, with full read/write access to a project's docs. `AI chat`
- **Sign-in beyond GitHub** — Google, Apple and email. `Onboarding`
- **The first pricing plans.** `Pricing`
