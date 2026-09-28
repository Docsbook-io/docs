---
title: "Docsbook Changelog"
description: "Release notes for Docsbook — new features, improvements and bug fixes to the AI-powered documentation platform, newest first."
layout: changelog
status: generated
version: "0.12"
---

# Product updates

New features, improvements and bug fixes in Docsbook — newest first. Each update has its own page; filter by type or by the part of the product it touches.

## 2026-09-28 — A front page that shows the product at work

The docsbook.io home page now opens on the Growth panel itself, walks a visitor through what the agent does from a brief to results, and ends where a project starts: one field and Generate.

### Improvements

- **A product tour sits right under the hero.** Five tabs (Visibility, Opportunities, Audit, Issues and Pull requests) show the real Growth screens, in light and dark, where a row of link cards used to be. `Website`
- **"How it works" is now a customer journey, not a feature list.** Six scrollable cards follow one product from a brief to a live site: you describe the product, the agent builds the site, puts your brand on it, writes every page, gets it found and cited, and keeps it growing on triggers. `Website`
- **The page ends where a project starts.** After the agents section, "What are we documenting?" takes a description, your website or a link to your Mintlify or GitBook docs and hands it to Generate, and the section above it gains a Get Started button. `Onboarding`

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
- **New SEO and GEO views show demand, mentions and competitors.** GEO adds **Prompt mentions**, **Prompt demand**, **Competitors**, **Competitor prompts** and **Competitor tactics**. SEO adds **Search demand**, **Google & Bing m
