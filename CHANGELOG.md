---
title: "Docsbook Changelog"
description: "Release notes for Docsbook — new features, improvements and bug fixes to the AI-powered documentation platform, newest first."
layout: changelog
status: generated
version: "0.11"
---

# Product updates

New features, improvements and bug fixes in Docsbook — newest first. Each update has its own page; filter by type or by the part of the product it touches.

## 2026-09-25 — The end of a trial is clear, and an Inbox story for your front page

When a trial or its credit runs out, the panel says so plainly and offers a way back in. Front pages get a widget that shows the agent reporting in.

### New releases

- **A new closing-section widget shows a Slack thread over the agent's Inbox**, with reports written as emails that switch with a click. The conversation stays in your Markdown, so it is indexed and translated like the rest of the page. `Content`

### Improvements

- **When the trial ends or its credit runs out, the Overview's AI card, Activity and the Graph are locked** like the rest of analytics, over sample figures, and nothing new is collected. `Pricing`
- **A trial whose credit is spent now offers "Buy access — $20/mo"** instead of "Get Free" at $0. The charge and the month's AI allowance start the same day. `Pricing`

## 2026-09-24 — One screen to start, and runs you can start, watch and stop

Creating a site is now one field and a Generate button that hands the writing to the agent. Every trigger has a Run now button that takes you to the live run, and a run can be stopped from there.

### New releases

- **Starting with Docsbook is one screen: describe your product, paste a link or pick a repository, and press Generate.** The multi-step form is gone, for new visitors and signed-in owners alike. The field takes a description, your website, a link to existing Mintlify or GitBook docs, or a GitHub repository, and you can attach files or a screenshot. Templates sit underneath if you want a starting structure. A newcomer describes the product first and signs up at Generate, and the project finishes creating on return. `Onboarding`
- **Pressing Generate hands the site to the agent, and you watch it write.** You land on **Activity ▸ Agent runs** with the creation run already working. It writes in the language of your description, attachments or website, from the first page to the sidebar labels. It fills in the branding, product brief, support email and call to action it learned, and with no template picked it designs the structure itself. Existing documentation is moved over whole, up to 300 pages at a time, with links between pages rewritten and other tools' components (steps, tabs, callouts, accordions) turned into Docsbook widgets. It never links readers out to the docs it was built from. `Onboarding`
- **A new one-time trigger, Generate docs from your repository, extends the docs in your own repository without rewriting them.** It starts only when you pick a repository and press Generate, adds what is missing and leaves your existing files alone. Importing a repository from the sidebar in one click still runs nothing. `Agents`
- **Every trigger dialog has a green Run now.** It starts the trigger once and takes you straight to that run's live trace. It works on a trigger you have never saved, without switching it on. Switching a trigger on or off moved to an **Active / Off** card that saves at once, and clicking a trigger card opens its settings. `Agents`
- **Stop a running task from its trace, and see what it has cost so far.** The Cost column used to stay empty until a run finished, and chat turns showed no cost at all. Tasks can also run for about 18 minutes instead of being cut off at five, and your Stop and the budget still apply at every step. `Agents`
- **Every tool your owner MCP token can reach is now a REST endpoint too.** Reads are `GET /api/v1/{tool}`, changes are `POST`, and the API reference lists every tool with its price. `API`

### Improvements

- **The Overview's agent card says Online only while a run is actually open**, and clicking it opens that run. When nothing is running it reads Idle and opens Triggers. While an agent works, an **Agent is running** row appears in the panel's sidebar and, for admins only, at the bottom of your docs sidebar. `Panel`

### Bug fixes

- **Triggers fire again.** For about a day and a half, no project event reached anything: armed triggers didn't run, webhook alerts and feed rows weren't written, and a new project's first "Generate docs" run never started. Events are delivered again, and a failed webhook no longer stops triggers from firing. `Agents`

## 2026-09-24 — Private stays private, and nothing is charged without asking

A private site is now closed on every door around the page, teammates can work in the panel you invited them to, and the balance stops at zero unless you choose to refill it.

### New releases

- **Auto-recharge, off by default.** Nothing is charged beyond your plan automatically any more: when the balance reaches zero the AI stops and the site keeps serving. To keep the AI running, switch on auto-recharge under **Settings ▸ Usage ▸ Balance**: when the balance falls below a threshold you set, your subscription's card is charged the amount you pick, at most $200 in any 30 days. **Top up** on the same card opens a small amount picker that goes straight to checkout. `Pricing`
- **Pro can now be paid yearly: $200 a year instead of $240.** The $20 of AI usage still arrives every month. `Pricing`
- **A private site can be served on its own custom domain**, with its own sign-in gate there. Password and SSO work on that domain, a collaborator signs in with their Docsbook account and comes back already let in, and search engines are told not to index what an admitted reader sees. `Privacy & access`

### Improvements

- **AI costs a fraction of what it did.** Chat answers, translations and search indexing are billed at twice the model provider's price, and agent runs at twice what the provider actually billed for each step. Most MCP and API calls now cost cents per thousand instead of dollars, and very cheap calls no longer read as "$0.0000". `Pricing`
- **A Free site is hosting only.** While a project's analytics are locked (the trial is over and nothing is paid or topped up), Docsbook stops recording its readers and bots, instead of collecting data nobody can open. The site, its search and your domain keep working, and recording resumes when you subscribe or top up. `Pricing`
- **An AI assistant fetching your page is metered as a crawl ($0.30 per 1,000 past your plan's allowance) and is never refused.** A person who clicks through from an AI answer is still a free reader. `Pricing`

### Bug fixes

- **A private site's content is closed everywhere the page itself is closed.** Its Markdown copy, search, AI chat, `llms.txt`, sitemap, link previews, social cards and folder listings all follow the site's gate. Switching a site to private also clears copies already cached along the way. `Privacy & access`
- **Only the repositories you connected are read through your GitHub App installation.** Installing the Docsbook App on "All repositories" to connect one no longer lets any Docsbook site read your organization's other private repositories. `Privacy & access`
- **Teammates, invitees and organization admins can use the project panel, not only its creator.** Accepting an invite let you open the project, but every screen inside answered "Workspace not found". Viewers can now see the panel, editors and admins can change the project, and billing, spend limits and keys stay with the owner. `Privacy & access`

## 2026-09-24 — Graph: watch agents, AI engines and readers move through your docs

The documentation map is now its own page that shows, within seconds, which agent, AI engine or reader is touching which page, and Activity is sorted by who came.

### New releases

- **Graph is its own row in the sidebar, and it opens live.** Every time an agent touches your docs (your panel chat, your site's assistant, MCP clients, tasks and triggers, the REST API) and every time a reader moves between pages, the move is drawn on the map within seconds. Bots reading your published docs show too, split into crawlers, AI answers, indexing and training. Click a walker in the feed to frame every page it touched, **Replay** it, or **Follow** the newest touch. The old **Analytics ▸ Graph** link lands here. `Brain`
- **Activity is grouped by who came: Agent, AI, People and Crawlers**, then Chat, Publishing, Billing and All, and it opens on **Agent ▸ Agent runs**. **AI** splits AI engines by why they came, **People** holds humans only, and every bot row names the bot, its provider and what it came for. `Analytics`
- **AI engines fetching your docs now show up in Analytics ▸ GEO, with a new AI mentions tab.** A bot runs no JavaScript, so fetches by ChatGPT and other assistants were almost never recorded. Docsbook now records them itself, and **AI mentions** draws them as three lines (answers, indexing, training) above the prompts checked against answer engines. `GEO`
- **Search from outside is answered by the docs agent.** Your own agent calling `search_project_docs` gets the pages and an answer in a few seconds instead of up to a minute. An anonymous caller on your public MCP server gets the pages found, with no AI call billed to you. Tool names and arguments are unchanged. `MCP`

### Improvements

- **The Graph stays still while you look.** Hovering only highlights, a click selects without shaking the map, and a **Live** switch turns the lighting off while the feed keeps logging. On a phone the activity panel is a bottom sheet. `Brain`
- **Empty Analytics and Activity tabs show a dimmed preview of what they will look like, plus a Fix it button** that hands the question to the assistant, instead of a grey sentence. `Analytics`
- **The Goals, Funnel and Journey tabs are redesigned around your accent colour.** One line sums every goal until you pick a row, a headline gives the week-over-week trend, and goals rank by **Reached**, **Rate** and **Potential**. `Analytics`

### Bug fixes

- **"Online" and Visitors count people only.** Bots, scripts and your own visits showed as readers online, and a reader going from A to B and back to A lost the return. `Analytics`

## 2026-09-24 — Docs that read like a product site

Edit a page without AI, API reference pages you can try in place, a blog and front-page widgets, a changelog page, tabs in the header, and a proper phone menu.

### New releases

- **Edit a page directly, with no AI.** Interactive mode has **Edit with AI**, which writes an instruction for the agent, and **Edit directly**: change a block's Markdown in place, move, duplicate or delete it, change its type, or add a widget. It saves as an ordinary commit and uses no model. Picking a block opens an inspector in the chat's corner, with AI actions as a grid of icons that you can **Run now** or **Run in background**. `Content`
- **API and MCP reference pages lay out like Stripe's.** Description, inputs and outputs sit on the left; example input in cURL, JavaScript or Python and example output sit on the right and stay in view. **Try it** turns the inputs into a form and sends a real request. `Content`
- **Put a blog and a product front page on your docs.** `layout: landing` drops the sidebar and page chrome. `stories` makes a grid of post cards with category filters, `story` opens a post, and `quote` shows a pull quote. `cards feature`, a pricing widget with a Monthly/Annual switch and a `compare` table, a larger hero title and closing sections round out a front page. `Content`
- **A changelog page as a timeline.** Add `layout: changelog` to a page and its `## YYYY-MM-DD — Title` sections render as releases, with filters by type and area. Each release gets its own address, so it can be linked, indexed and cited on its own. `Content`
- **Tabs in the header, tab groups, and any page as a tab.** A **Tabs in header** preset puts your section tabs in the centre of the header on desktop, replacing **Centered**. Several tabs can collapse into one dropdown tab without moving files, and Subheader Folders can pick any page, not only a top-level folder. `Docs site`
- **Separate dark-theme icon and logo.** A dark icon on a dark site no longer sits in a light frame you couldn't control. Created from your website, Docsbook picks up both versions. `Docs site`
- **An MCP button in the chat.** Readers get one-click install in Cursor, VS Code or Claude Code, your site's MCP address and a ready prompt, and you get the same for your account-wide server. The **Copy page** menu stays about copying and opening the page. `MCP`

### Improvements

- **On your own docs you get one chat.** The corner button answers the way readers' chat does until you turn on Interactive mode, then becomes the admin chat with its tools. Ask AI, selected text and search all open that same panel, and a new button on code blocks asks it to explain that block. `AI chat`
- **Premium is an accent haze, and the header is transparent.** A landing front page gets a full hero in your accent colour, other pages a quieter band, and the header's blur fades in on scroll. Widgets, code and tables sit on a see-through surface instead of solid plates. `Docs site`
- **Phones get a full-height menu**, with your logo, tap-sized rows and a theme switch. Search collapses to an icon, the outline opens as a bottom sheet, and nothing makes the page scroll sideways. `Docs site`
- **Reading pages load about a third less JavaScript.** Only owners load the panel code, and a page carries only the icons it shows. `Docs site`
- **Every crawler may read your site, and custom domains get language links.** `robots.txt` no longer turns away a default list of crawlers; it names only the bots you switch off. A translated page on your own domain now points search engines to its other languages. `SEO`

### Bug fixes

- **Reading fixes.** The sidebar keeps the page you are reading open and in view, a folder shown as a section tab no longer appears again in the main sidebar, and a page pushed straight to GitHub no longer shows as missing for up to half an hour. `Docs site`
- **Themes and links hold up.** A reader's "System" theme follows the device on every site, a very pale accent stays visible in light theme, and View as Markdown, Copy Skills.md URL and the chat's Visit link go to real addresses on custom domains and domain roots. `Docs site`

## 2026-09-23 — Analytics as ranked lists, and an Audit of every rule

Every Analytics tab that answers "which page, which query, which engine" is now one ranked list with a view switch. The documentation rules are one Audit list, and Activity is grouped by subject.

### New releases

- **Analytics ▸ Audit is one list of every documentation rule, ranked by priority.** The rules used to be spread over eleven cards on four tabs, so "what should we fix first" had no single answer. Search, a topic filter and status chips sit above a fixed #1-to-#N rank. Rules that can be counted are checked automatically, every verdict cites a reading taken on your project, and **Run audit** hands a topic to the agent to judge the rest. `Analytics`
- **SEO, GEO, Socials, Feedback and Chat are each one ranked list with a View switch.** The KPI tiles, charts and summary cards are gone. Each tab has one toolbar (search, period, source, sort) over rows with a fixed rank, so the page or query at the top is the one to look at first. `Analytics`
- **New SEO and GEO views show demand, mentions and competitors.** GEO adds **Prompt mentions**, **Prompt demand**, **Competitors**, **Competitor prompts** and **Competitor tactics**. SEO adds **Search demand**, **Google & Bing mentions**, **Competitors**, **Competitor queries** and **Competitor tactics**, where the agent records which rules the winning pages follow. `SEO`
- **Feedback moved to Analytics and ranks pages by total reactions**, with a **Votes** view of every vote. **Activity ▸ Chat** gains a **Rating** column. `Analytics`
- **Activity ▸ Searches shows every search run over your docs**, from the public MCP server, your token, the API, agents and the chats, with who ran it and how many hits came back. The site's own search box has its own tab, **Search box**. `Analytics`
- **An organization's Activity shows all its projects in one place**, with a Project column, instead of one project's panel at a time. `Panel`

### Improvements

- **Activity's long strip of tabs is grouped into a few dropdowns, and every tab is a ready-made view.** The **Add filter** menus and saved lists are gone, every event tab uses the same table as **Agent runs**, and links you already shared still open the same tab. `Panel`

## 2026-09-23 — Teams share their owner's balance, and Free sites stay up

An organization now spends its owner's balance and can be handed over from its Danger Zone. People join a team, not a single project. After the trial, a Free site stays published, with analytics locked until you pay.

### New releases

- **Move a project into a Docsbook organization, or hand an organization to another member, from Danger Zone.** **Transfer to Organization** is the first card in a project's Danger Zone. A team's own Danger Zone has **Transfer Organization**: pick a member and confirm, and from then on the team's projects spend the new owner's balance. `Panel`

### Improvements

- **An organization's projects spend its owner's balance.** Organizations held no money of their own, so a team showed $0 while its owner had credit, and its projects were refused for lack of funds. Top-ups land on the owner's account, the organization's Usage page shows it, and the plan still comes from the organization. `Pricing`
- **Inviting someone gives them access to the team or account, not to one project.** Existing project collaborators were moved to the team or account that owns the project, and invite links already sent still work. `Privacy & access`
- **After the trial, a Free site stays public.** Sites are no longer made private when unpaid, and sites that were paused have been restored. Analytics are shown as samples with a **Get access** button, and the same lock applies when an API token, the MCP server or the agent asks for the numbers. `Pricing`
- **Moving a Docsbook-hosted project to your GitHub goes through the Docsbook GitHub App**, with no personal token. For an organization, the App creates the repository and copies your docs; for a personal account, the repository is transferred to you. The dialog shows, for each destination, whether the App is installed, with **Install** and **Check again**. `Integrations`

### Bug fixes

- **Private repositories with the Docsbook GitHub App installed are no longer reported as missing**, and a project created from a private repository starts as a private site instead of publishing everything in it. `Sources`
- **An invite opened while signed in to the wrong account has a Switch account button** that brings you back to the same invite. `Onboarding`
- **Bot crawls count toward the monthly crawl allowance as the pricing page describes.** Monthly totals weren't being settled, and Amazon's search crawler wasn't counted as a crawler. `Pricing`

## 2026-09-23 — Faster pages, and links you can see

Doc pages come from a cache and start loading when a reader hovers a link. Links in an article carry the icon of the page they lead to, and the top of the page is tighter.

### New releases

- **Links in an article are bold, with an accent underline and the target page's icon.** If the linked page has an icon under Sidebar Icons, the link shows it, so a reader can tell where it goes before clicking. `Content`
- **Top-level sidebar folders can collapse.** Turn on **Collapsible Top-Level Folders** (Customize ▸ Left sidebar) and each first-level folder becomes a row with a chevron that opens by itself around the current page. `Docs site`

### Improvements

- **Doc pages open faster.** Page content is cached for the whole site instead of fetched from GitHub on every view, and it updates when you publish. Hovering, focusing or tapping a link starts loading that page. `Docs site`
- **The top of the page is tighter.** **Copy page** and **Ask AI** sit beside the title, breadcrumbs sit closer to it, and the TL;DR is a subtitle under the title. `Docs site`
- **The AI assistant answers only on sites that have a Docsbook project behind them.** A public repository nobody has set up gets a short explanation instead of an AI answer. `AI chat`

### Bug fixes

- **The floating Ask Docs button is on by default** for new projects and on published sites. `AI chat`
- **Chat citations and the subheader's Overview tab go to your site's real address.** On custom domains and custom addresses, citations led to a 404 and Overview did nothing on any page but the home page. `AI chat`

## 2026-09-23 — Agents search first, write short, and run where you can see them

Your MCP tools are named after your product, search finds text by meaning, the agent writes short paragraphs with blocks between them, and Triggers work across a whole organization.

### New releases

- **Your public MCP server and its tools are named after your product.** Every project's server used to be called `docsbook` with a tool called `search`, so an agent with several servers couldn't tell whose docs were behind it. It's now `<slug>-docs`, with `search_<slug>_docs`, `read_<slug>_doc` and `get_<slug>_doc_outline`. Your token's tools are `search_project_docs`, `read_project_doc`, `get_project_doc_outline` and `ask_project_docs`, and the old names still work. `MCP`
- **Search finds sections worded differently.** With search by meaning on, `search_docs` combines exact-word and meaning matches, and connected agents are pointed to it first instead of browsing page by page. The index catches up with a commit within minutes, including one pushed straight to GitHub. `MCP`
- **The agent writes short paragraphs with blocks between them.** A line or two per paragraph, code or a widget between them, identifiers in inline code, a link where a concept is first named. `write_docs` returns a style review that flags long paragraphs and walls of text without changing the page. `Agents`
- **Triggers for a whole organization, on one screen.** On the owner dashboard, **Yours** lists the triggers switched on across every project, each tagged with its project, and **Discover** shows the catalogue. `Agents`
- **You can see which triggers are running.** A running card is highlighted, shows a spinner, sorts first and opens its run in Activity. The Triggers row in the sidebar shows how many are running. `Agents`
- **A new project's first run matches what you gave it.** With a website, **Generate docs from your site** reads it and your attachments and rewrites the template about your product. Without one, **Generate docs from your brief** works only from your description, trims the template to fit and lists what's missing as questions instead of guessing. The report lands in your Inbox. `Onboarding`

### Bug fixes

- **The Stop button in the admin chat stops the answer.** Clicking it while a reply was streaming did nothing. `AI chat`
- **The agent can read the site's own repository as a source**, instead of retrying a failed read until it gave up mid-task. `Sources`

## 2026-09-22 — A new project that already looks like a product

Templates became full sites with their own look, landing pages got new widgets, and a docs site loads with its branding from the first paint.

### New releases

- **38 templates, each with real pages, real widgets and its own look.** The original 32 went from a handful of plain pages to about ten each, and six new ones are for businesses that are not software: hotel, restaurant, salon and spa, clinic, fitness studio and home services. Each sets its own theme, fonts, accent, header and footer, and its card is a screenshot of the site you will get. Nothing in them invents a fact: prices, hours and addresses are marked blanks for you to fill in. `Onboarding`
- **New landing-page widgets.** `bento` lays out feature cards of different widths led by screenshots, `logos` is a customer strip, cards can carry their own colour, and `lineup` compares plans, models or editions at a glance. The `journey` widget now runs down the page on a vertical rail, with no edits needed. `Content`

### Bug fixes

- **A docs site no longer flashes a plain white page before its branding loads.** Your colours, theme and fonts arrive with the first paint. `Docs site`
- **Pages inside a top-level `api/` folder open on hosted sites and custom domains.** They returned 404 while your sitemap and `llms.txt` listed them. `Docs site`
- **A language with uploaded translations is served even if its switch was never turned on**, and the language picker is hidden when there is nothing to pick. `Translations`
- **`llms-full.txt` loads on large sites.** It could time out on sites with thousands of pages; it now builds in seconds and says so when it is cut short. `GEO`

## 2026-09-22 — One agent, in the panel and on your own pages

The admin chat works on your live docs, applies what you ask it to, and refreshes the page under it. Both chats show what they are doing while they work.

### New releases

- **Point at any block on your own docs and the instruction lands in the admin chat.** Interactive mode is a button in the admin chat (and on your site's card in Overview). Pick a block, choose an action, and the instruction appears unsent, so you can add what you meant. The header, sidebar, footer and page buttons can all be selected, with about thirty actions such as reorder, badge, translate and recolour. Readers never see any of it. `AI chat`
- **Asking the admin chat for an edit makes the edit.** A request like "rephrase this" used to end with "Proposed 1 change" and nothing changed. The change is now published or opened as a pull request, following **When a change goes live**, with a link under the answer. `AI chat`
- **Your page updates under the chat without a reload.** Change an icon, the navigation or the branding from the admin chat, and the page behind it re-renders while your conversation stays put. `AI chat`

### Improvements

- **You can see what the chat is doing while it works.** The waiting line names the tool that's running, a run of tool calls folds into one line such as "Explored with 5 tools", and the admin chat streams its answer word by word, holding still once the first line reaches the top so you can read. `AI chat`
- **The admin chat suggests a next step after every answer**, has copy, like and dislike buttons, and starts fresh when you close it or switch project, so one project's conversation no longer follows you into another. `AI chat`
- **Reply and Write in the Inbox open the admin chat**, with the letter quoted and unsent for Reply. `Inbox`

### Bug fixes

- **The owner's Custom Questions appear in the reader's chat.** They were set in the panel but never reached the chat readers open. `AI chat`
- **An instruction from the admin chat always runs on the project you're looking at.** A project number the model made up, or a word that matched another project's name, could send the work elsewhere. `AI chat`
- **The admin chat's website reader respects robots.txt and can't be pointed at internal addresses.** `Privacy & access`

## 2026-09-22 — Triggers that know the job, and every agent run on record

Ready-made jobs lead the Triggers screen and wake when their input changes. Every agent run can be inspected step by step, and alerts go to more places.

### New releases

- **Triggers opens with ready-made jobs that already know what to ask.** Dozens of cards, grouped as Write, Audit, Answer, Report and Translate: write release notes, sweep for broken links, check whether AI engines cite you, keep reference pages in step with your OpenAPI spec or MCP tools, and more. Most wake when their input changes (your docs are re-indexed, a payment arrives, a question goes unanswered) rather than on a calendar. `Agents`
- **One translation trigger per language.** Fifteen cards, each with a prompt tuned to that language, so you can see at a glance that Japanese is running and Korean isn't. `Translations`
- **Activity ▸ Agent runs lists every call of the Docsbook agent.** Tasks, admin-chat turns, readers' questions, MCP and API clients and automations each get a row with status, duration, tool calls, tokens and cost. Open one for a step-by-step trace. Your arguments and tool output aren't stored. `Agents`
- **More places to send alerts.** Integrations ▸ Chat & alerts adds Discord, Microsoft Teams, PagerDuty and email (which delivers nothing until a confirmation link is clicked). A new **content.indexing_failed** alert tells you when your docs could not be indexed. `Integrations`
- **Hand a finished project to its owner, knowledge included.** `create_claim_link` and `revoke_claim_link` manage claim links over MCP. A project given away this way takes its memory entries and audit verdicts to the new owner; your organization-wide knowledge and skills stay with you. `MCP`

### Improvements

- **The agent runs on the model you picked in the panel.** The setting was saved but never used, so every task ran on a fixed default. Background tasks also use your own AI key when you have one. `Agents`
- **Your MCP client can reach every tool.** Tools for branding, navigation, domain, languages, translations and page writing now appear in the tool list, and the ones kept off it run through the listed `call_tool`, since Claude Code, claude.ai and Cursor only call listed tools. `MCP`

### Bug fixes

- **An MCP client or the chat can no longer attach a new project to someone else's repository.** A repository you can't prove is yours is now hosted by Docsbook as a separate site. `Privacy & access`
- **An agent task that hit its step limit or deadline reports "expired", not "succeeded".** `Agents`

## 2026-09-22 — Your site's address, access and skills in Settings

Your site's address is now a setting, Access has a card for each thing you control, and skills tell the agent how to work and where.

### New releases

- **Choose your site's address in Settings ▸ General ▸ Site source**, for any project, without renaming anything on GitHub. The old address redirects, and canonical links, the sitemap and `llms.txt` follow. `Panel`
- **Settings ▸ Access has a card for each thing you control**: **Collaborators**, **Privacy & Access** (password and SSO), **Source repository** (whether the GitHub repository is public), **Search engines** (whether Google can list the site) and **AI engines** (whether ChatGPT and others can read it). `Privacy & access`
- **Set your docs' original language in Settings ▸ General ▸ Default Language**, on any plan. Wherever the panel said "Original", it now names the language. `Translations`
- **Skills: write how your agent should work, and choose where each applies.** Open a skill to edit it full-screen, then tick where it runs (public docs chat, admin chat, public MCP, admin MCP) and, optionally, for which roles or people. A new skill runs only in the admin surfaces until you tick a reader-facing one, and skills are shared across all projects of an organization or account. Agent instructions live on **Settings ▸ Prompts**, and the tab once called "Models & Search" is now **Agent**. `Agents`

### Improvements

- **Credit belongs to your account, not to each project.** Credit you add can be spent by every project you own, and existing project balances were moved there. Credit on one project could fail with "insufficient balance" on another. `Pricing`
- **The account menu is organized into labelled sections**: Accounts, My profile, Organizations, Shared with me and Invitations, with a cog on every row. Owners and admins can rename an organization and set its icon, and switching project or organization keeps you on the same section and tab. `Panel`

## 2026-09-21 — Settings in a dialog, and a panel for the whole team

Settings now opens over the page you were on, the same dialog works for a single project or for everything an organization owns, and the log becomes one readable Activity table.

### New releases

- **Settings opens as a dialog on top of the section you were on.** It used to replace the panel's content, so checking a setting meant losing your place. It has its own menu with an icon on every row, and the long pages are split into shorter ones: General, Domain & API and Danger Zone for the project, and separate pages for the chat's prompts and its models. `Panel`
- **The same Settings dialog works on an organization or owner dashboard.** Usage, Access, Profile and Support open straight away, and project pages ask which project first. Buy Pro once for a team or a GitHub owner and it covers every project under it. `Panel`
- **Invite people into a GitHub organization or your personal space, not only into a Docsbook team.** The access covers the projects you keep under that owner, never someone else's projects under the same name. `Privacy & access`
- **Leave a Docsbook team, or delete one that holds no projects**, from Settings ▸ Danger Zone. If you are the last owner, leaving hands ownership to the next full-access member. `Panel`
- **Move a project's repository to another GitHub account or organization.** The Move Project dialog checks whether the move can work before you pick, gives the exact reason and a link to fix it when it can't, and publishing follows the repository to its new address. `Sources`
- **Give a project to someone with a one-time claim link.** Whoever opens it becomes its sole owner. `Panel`
- **Logs is now Activity, with one log format everywhere.** One line per event, with exact time, source, outcome, project and cost. A row opens beside the log, ↑/↓ step through events, and the sparkle in an event's detail asks the panel chat about that event. `Feeds`

### Improvements

- **One breadcrumb on an owner dashboard replaces four project pickers.** Picking a project opens it on the section you were reading. `Panel`
- **Every Customize card has an icon, and a search box finds any setting**, down to one switch inside a group of five. `Panel`
- **"When a change goes live" is one Auto-merge switch**, on by default. Turn it off and changes wait for your review. `Changes`

### Bug fixes

- **The Issues list scrolls inside its own area again**, instead of scrolling the whole panel with the sidebar and header. `Issues`

## 2026-09-21 — Triggers, a memory for the agent, and one chat panel

The Agent section becomes Triggers, a grid of everything that can wake your agent. The agent gets one folder where it keeps what it knows, and the reader's and owner's chats become the same branded corner panel.

### New releases

- **Triggers replaces the Agent section.** One grid shows everything that can start work: events from connected apps, schedules (hourly, daily, weekdays, monthly and more) and the Docsbook agent itself, which works on its own at a frequency you can see and change. `Agents`
- **Events inside Docsbook can wake the agent too**: a reader rating a page down, the chat failing to answer, a payment, the index finishing a rebuild. Each is a card whose switch asks what the agent should do. `Agents`
- **The agent keeps one folder of what it knows per organization, GitHub owner or personal account.** Tell the panel chat a fact about your product and it writes it down; ask what it knows and it answers from the folder. It never hands over the whole folder at once. `Agents`
- **The chats can ask a clarifying question**, with the options as buttons. The panel chat also changes settings with the real tools and tells you what changed. `AI chat`
- **Readers get an honest "I don't know" and somewhere to go next.** Add a **Support Email** in Settings ▸ General, and when your pages don't answer a question the chat sends the reader there. It never makes up an address. `AI chat`
- **`find_tool` on your MCP server finds the tools that aren't in the list**, such as settings, alerts, goals and the agent's folder, with a project owner's token. `MCP`

### Improvements

- **The reader's chat and the panel chat are one panel.** Both open into the docked corner panel with the cursor in the input, with your project's name and icon in the header and a small "Powered by docsbook.io" underneath. `AI chat`
- **Luna is the default model for the reader chat, and the model list is current**, with GPT-5, Gemini 3.1, DeepSeek V3.2, Claude Sonnet 5 and Opus 5, and cheaper options such as Qwen3.7 Flash and Mistral Small. `AI chat`

## 2026-09-21 — Analytics with no switches, a catalog of rules, and one trial per account

Every Analytics card shows your data or a sample straight away, search and AI reports can be fed from engines Docsbook doesn't read itself, and the trial now belongs to you rather than to each project.

### New releases

- **Analytics and Activity have no more "Turn on" buttons.** Every card loads your data straight away. `Analytics`
- **Report what Docsbook can't read itself.** With your project API key, push daily search numbers from Bing, Yandex, DuckDuckGo or a rank tracker, record the checks you run in ChatGPT, Claude or Perplexity, and record posts about your docs on Reddit, X, Facebook and LinkedIn in a new **Socials** tab. `SEO`
- **A catalog of 299 documentation rules, each linked to the published source behind it.** Every rule is one plain sentence with its source's icon, a rule quotes its source only where the quote was found word for word, and a rule reads **Not checked** until it has actually been judged. `Analytics`
- **A partner program: earn 50% of the subscription of anyone you bring to Docsbook.** The Referral page in Settings has your link and who came through it, and the **Powered by Docsbook** badge on your published site is your partner link too. `Pricing`
- **One Pro trial per account, covering every project you create.** Days are counted from the first time you open a project, not from sign-up, and the trial's AI credit is shared by all your projects. When the credit runs out the AI stops and the site keeps serving. Reactivating a project or receiving one as a gift doesn't start a second trial. `Pricing`

### Improvements

- **Doc pages are about a third lighter.** Editing markup is only sent when editing is possible, and closed sidebar folders carry their links without the styling, so crawlers still find every link. `SEO`
- **Crawlers may read the Markdown copy of your pages.** `robots.txt` allows it, and `llms.txt` lists each page's Markdown address beside its web address. `GEO`
- **Bringing your own AI or translation key is an Enterprise feature**, and each locked card says which plan unlocks it. A daily safety limit on AI spend keeps a runaway loop or a leaked key from using up the month in minutes. `Pricing`

### Bug fixes

- **The Plan page no longer shows "Get Free" and $0 when subscribing would charge your card today.** It shows the real price and **Subscribe — $20/mo**, with a confirmation that you are billed today. `Pricing`

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
- **A collaborator invite now links straight to the docs, not only to the sign-in-gated accept page.** Deciding whether to join a project used to mean creating an account first and looking around after; the invite email now also opens the documentation site itself. `Panel`
- **The trial-wallet warnings this page promises now actually fire.** A trial without an expiry date (running since 15 September) never triggered its 50%, 75% and 90% notices — a field-name mismatch made every one of them silently read as not running a trial at all, for the five days between shipping and this fix. `Pricing`
- **The Feedback tab in Logs now shows the same empty state as every other tab on the strip when there is nothing to show**, instead of a plainer placeholder of its own. Its **Fix it** action now opens the admin chat directly. `Feeds`

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
- A header link now has a **New tab** toggle, so you can keep readers on the current tab for a link that used to force a new one open (and vice versa) instead of that always being decided by whether the URL is external. `Content`

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

- **Organizations**: make a team in one click, invite someone once for access to every project in it, and buy a single plan for the whole team instead of per project. `Panel`
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
- Audits became **Opportunities**: a flat, ranked list of searches you don't win yet, each with the competitor holding it today and what winning it would be worth. `Panel`

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
- Goals, Questions, Memory and Reminders became one card with four tabs; Issues and Pull Requests became another. `Panel`

## 2026-09-12 — One consulting agent instead of 176 tools

The MCP surface was rebuilt around one agent that hands back the steps, the tool for each and what would make the answer wrong — and it now remembers your project between sessions.

### New releases

- The MCP surface was rebuilt around one consulting agent — **`docsbook_expert`**, with a build partner **`docsbook_assistant`** — replacing 41 standing-agent routes and 135 narrow action tools. Ask it anything about your docs and it hands back the steps, the exact tool for each, and what would make the answer wrong. `MCP`
- Docsbook now remembers facts about your project between sessions (`list_memory`/`add_memory`), and keeps every past reading so a rewrite can be measured against a real baseline instead of a guess. `MCP`

### Improvements

- A project with no GitHub repository is no longer turned away — Docsbook can work from your website, a single page, or a couple of sentences about your product. `MCP`
- The Doc Graph now draws immediately from cache instead of waiting on a similarity query, and its Meaning edges are measured between pages rather than spent entirely on one long page's own headings. `Brain`

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

- Inviting a teammate to a project's AI chat was permanently failing with "temporarily unavailable." `AI chat`

## 2026-09-05 — Invoices you can read, and changes that score themselves

Billing became a real invoice list with staged overage warnings, every pull request scores its own outcome, and semantic search is on for every plan.

### New releases

- Billing is now a real invoice list — what's owed next, whether the current invoice is paid, every past charge as its own line — with five staged overage warnings (75/85/90/95%/cap) and matching webhooks. `Pricing`
- Every pull request now scores itself out of 100 — readers served, reach, cost to run, edit quality — with the movements behind it, so whether a merged change worked stops depending on somebody remembering to check. `Changes`
- The Doc Graph gained read-depth coloring, a Dead ends overlay, and now shows the open pull requests and issues already touching a page you click. `Brain`

### Improvements

- Semantic search (`search`) is on every project now regardless of plan, so a question an assistant asks of your docs is answered instead of refused. `MCP`
- The docs were reorganized by capability — SEO, GEO, AEO, agent-ready content, chat, analytics, translations — each page stating how the feature is built and what isn't proven yet. `Content`

### Bug fixes

- Overage could be pushed past the $200 cap the pricing page promised; a project on a declined card kept accruing new overage instead of spending down its existing credit. `Pricing`

## 2026-09-04 — Check prior work first, and AI markup cut to +70%

Agents now ask "have we already tried this" before proposing anything, and the markup on AI usage dropped from +900% to +70% of the provider's price.

### New releases

- Two tools answer "have we already tried this" before an agent proposes anything (`search_prior_work`, `get_pull_request`), and fifty-four capabilities now run that check first. `MCP`

### Improvements

- AI usage markup cut from the provider's real price **+900%** to **+70%**, in the same dashboard breakdown. `Pricing`

### Bug fixes

- The AI-spend ledger had been under-reporting by 17%, because it read a balance from the row it had just rewritten instead of the one it started from. `Pricing`

### Removed

- Removed the **Prompts** section — a prompt you used to copy-paste into your own tool is now either a scheduled Agent or the one worked example already on a tool's own page. `MCP`

## 2026-09-03 — A page and a history for every MCP tool

Each tool has its own address with every call it served — cost, latency, input and output — and the project row stopped leaking through tool answers.

### New releases

- Every MCP tool now has its own page and address, with full call history — cost, latency, what went in and what came back. `MCP`

### Improvements

- Page feedback ("Was this page helpful?") now shows on mobile, where the old sidebar version never rendered. `Content`

### Bug fixes

- `list_workspaces`/`get_workspace` and fifteen `update_*` tools stopped returning the raw project row, including a live API key and a 2.1MB semantic-index blob. `MCP`
- A billing-rollover bug had zeroed 399 projects' carried balances while still showing the money as available; page titles and meta descriptions were being built from the wrong source. `Pricing`

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
- Contextual **Improve**/**Analyze** buttons landed across Analytics, Users, Chat and Changes, so any number on screen can hand itself to the assistant. `AI chat`
- Every empty panel card now shows sample data with a guided "Turn on" walkthrough instead of a blank box. `Panel`
- MCP calls became billed per call in the background against your project balance, with the whole catalogue browsable as one searchable, filterable table. `MCP`
- A public content-widget gallery, each block switchable off per project; the interactive API-reference widget now follows your brand's colors. `Content`

## 2026-07-31 — July: private sites, new plans and a chat API

The month in one release — password and SSO-protected sites, Growth and Scale plans, real Search Console rankings and a public REST endpoint for a project's AI chat.

### New releases

- Anonymous, no-account docs generation at `docsbook.io/create` — paste a URL, a repo or an idea and get a live draft with AI chat before signing up; signing in publishes it exactly as it stands. `Onboarding`
- Workspaces can be made private, behind a password or your own SSO (Google Workspace, Microsoft Entra ID, Okta). `Privacy & access`
- Two new plans, **Growth** ($349) and **Scale** ($899), plus 20%-off annual billing on every paid plan. `Pricing`
- Analytics Explorer replaced the raw event feed: charts, click-to-filter facets, funnels, retention, and bot-traffic filtering — crawlers had been up to 93% of pageviews on some sites. `Analytics`
- **Translation Activity**: per-page, per-language coverage and staleness, with one-click re-translation of just what changed. `Translations`
- Multiplayer AI chat on Growth/Scale — a teammate sees the same answer stream in live, instead of a relay. `AI chat`
- A public REST endpoint, `POST /api/v1/chat`, for calling a project's AI chat from your own backend. `API`

### Improvements

- AI usage is billed in real dollars against a per-plan monthly budget, with metered overage instead of a hard stop when it runs out. `Pricing`
- Real Google Search Console rankings landed in SEO & GEO, with no OAuth needed on a `*.docsbook.io` subdomain. `SEO`
- The semantic doc index — meaning-based chat answers with page citations — shipped for Business-and-up plans. `AI chat`

## 2026-05-01 — Docsbook launches

Docsbook launched in May 2026 as a documentation site generated straight from a GitHub repository: hosting, theming, translations, an SEO panel, and an MCP server for AI-assisted editing.

### New releases

- **The admin AI chat** (`/chat`) arrived in June, with full read/write access to a project's docs. `AI chat`
- **Sign-in beyond GitHub** — Google, Apple and email. `Onboarding`
- **The first pricing plans.** `Pricing`
