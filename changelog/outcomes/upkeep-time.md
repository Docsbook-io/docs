---
title: "What Docsbook has shipped that cuts docs upkeep time"
description: "Every release that cuts the time it takes to keep the docs true: writing, restructuring, staleness detection, and the agents that do that work for you."
---

# What Docsbook has shipped that cuts docs upkeep time

Everything Docsbook shipped that moves one number: **Upkeep time** — less time keeping the docs true. On this axis, down is better.

Work a person does by hand every week, handed to the agent instead. This is the Upkeep time slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG); an entry appears here whenever what it shipped moves this number, whichever part of the panel it landed in.

## NEW - 04.09.2026

### Added

- Two MCP tools that answer **"have we already tried this?"** before an agent proposes anything. `search_prior_work` searches your repository's issues and pull requests together and says what happened to each — still open, closed without merging, or merged — and `get_pull_request` opens one of them with the files it touched, the agent and run that opened it, the issues it came out of, what reviewers said, and, once it merged, the commit its effect can be measured on. `MCP`
- Fifty-four of the agent capabilities now run that check as their second step, so a recommendation arrives knowing whether this project already made that change and abandoned it. A pull request closed without merging is reported as a change your project rejected, never as a precedent for making it again, which is the reading that used to send the same idea round every quarter. `MCP`
- An **Agents** section in the admin panel: forty goals your project can pursue on its own, each one an ordered route of subagents rather than a single call, with what it is for, the number it is bought to move, and what a run costs before you arm it. Recurring documentation work you were doing by hand every week can now be handed to a schedule. `Agents`
- Arm one on a schedule you read as a sentence in your own clock: how often, which days, at what time, with the next run printed underneath in the same clock. The six presets it replaced were labelled in UTC, so checking one meant converting in your head, and "Tuesday and Thursday at nine" could not be asked for at all. `Agents`
- A **Runs** tab beside the catalog answers "did anything run last night, and did it hold up" of the whole project. That history used to be reachable only from inside one agent's settings, so the question could only be asked forty times. `Agents`
- Every station of an agent's run files what it found as a GitHub issue on your own tracker, so nobody has to read a transcript to learn what needs doing. The finding outlives the run that produced it: a person can pick it up, the diff that fixes it can reference it, and merging that diff closes it. `Issues`
- An issue an agent filed names that agent in its sidebar and opens its card from there, so "what wakes this thing, and what route is this station part of" is one click rather than a walk back through the panel. Beside it sit the run behind the finding, the other stations of the same route, the other issues that reference this one, and the pull request that closes it. `Issues`
- An MCP tool's page now lists the **agents that use it** — the cards whose route actually calls that tool, armed ones first, each with its own switch — so you can put a tool on a schedule from the page where you just read what a call costs, instead of hunting for it among forty agents. `MCP`
- Agents can now be armed to run every hour, not just once a day at the fastest. The schedule sentence gained an **Hourly** option that asks which minute past the hour rather than a time of day, for work that should not wait for tomorrow's run. `Agents`
- Pull Requests now opens with a short walkthrough on a first visit instead of landing straight on a live GitHub read, the same "Turn on" introduction Agents and Sources already carry. `Changes`

### Changed

- Reading an issue now tells you what came of it, not only what it says: the comments, the agent and the run that filed it, and the pull requests written against it. A hypothesis somebody wrote down and a hypothesis somebody actually tested read very differently, and the tracker was only showing you the first. `Issues`
- An agent's issue now opens on what it FOUND. Why the run happened, what earlier steps handed it, what happens to anything it writes and the raw call all moved into one collapsed block at the bottom, so deciding what to do about a finding no longer means scrolling past four headings about the machinery to reach it. `Issues`
- A run's transcript opens as its own table of contents, every station closed. Which stations ran, which held up and how long each took now fits on one screen instead of being spread over forty screens of prose. `Agents`
- Which sources an agent may read is one picker that says what an empty pick means, instead of a wall of toggles as tall as the number of sources you are not choosing. `Agents`
- **Start agent** now sits at the top of an agent's panel, beside Close, reachable from Overview as well as Runs, instead of only appearing once you switched to the Runs tab. `Agents`
- The trigger's "On a schedule / On an event / ..." control is now sized to match the detail underneath it, with the dividing line between them removed, so the two read as one card rather than two stacked controls. `Agents`
- The setup checklist now offers connecting your own coding agent — Claude Code, Cursor, Codex, or whichever one you already work in — right after the content interview instead of near the bottom of the list, so the one thing that lets you drive the rest of setup from your own tool over MCP gets found instead of skipped.
- Pressing **Improve** or **Analyze** anywhere in the panel — a reader row, a goal, a funnel step, a commit — now starts the agent that fits what you were looking at, carrying what was already on screen as that run's own instruction, and opens the run to watch live: a clock that keeps ticking while it works, and the instruction it started from shown apart from what it did. The button used to just copy that text to your clipboard, from when it opened a chat that no longer exists. `Agents`
- The price shown for an agent's route, and for one subagent call in it, now reads **up to** instead of a bare figure. It is still exact for the metered calls themselves, but a run also spends from your AI balance on the model turns it makes, which is billed separately and can push the real cost above the number shown. `Agents`
- The **Issues** walkthrough now runs over example issues instead of an empty tracker. A first visit shows what a filed finding looks like — the badge that marks one an agent opened on its own, the labels that say which kind of reader raised it, an open one beside a closed one — so the introduction argues for the section rather than reporting that there is nothing in it. The examples say they are examples and disappear the moment a real issue exists. `Issues`
- The **Pull Requests** walkthrough does the same: the queue behind it now shows example changes waiting for approval, each with the agent that opened it and the issues it came out of, plus the publish-automatically switch the walkthrough talks about. It used to introduce itself with "Nothing is waiting for you", which is exactly what it says on the day you have not armed anything yet. `Changes`

### Fixed

- A station with nothing to report no longer fails the whole run. On a project with no Search Console history and no in-doc searches, a station that correctly answered "there is no intent mismatch to explain here, and here is each check I could not make and why" was refused three times over and stopped the route, so an agent could not finish on exactly the projects it had least to invent about. `Agents`
- Issues an agent files carry their labels on GitHub again, and any label your repository does not have yet is created first. Without them the panel could not tell an agent's finding from something a person typed, so twenty findings opened with no run, no route and no sibling stations beside them. `Issues`
- Your MCP call log stops losing the first half of a session. A call that costs nothing is still a call, so `get_info`, `get_workspace`, `list_workspaces`, `create_workspace`, `find_skill` and `find_widget` (what an agent opens a session with) now appear in Feeds and in the tools table against the right project. `Feeds`
- A run whose hand-off went missing no longer spins for ever. The route is driven inside its own request, and anything still open is picked up within five minutes or reported as failed with the reason, so nobody has to watch a run to find out it stopped. `Agents`
- Translating a page now costs roughly a third of what it did. Translations run on GPT-5.6 Luna by default instead of GPT-4o mini, which is the same rewrite-this-prose job at $0.055/$0.22 per 1M tokens against $0.15/$0.60, so the same balance stretches over about three times as many pages and a language you were putting off is affordable now. Projects that had explicitly chosen a pricier model were moved with the default; the picker in **Settings ▸ Translations ▸ Translation Model** still offers every model, and the estimate shown before a run is priced on whichever one you pick. `Translations`
- Clicking the schedule's time no longer leaves it unclear what you are about to change. It is now the browser's own time control, in place of an invisible layer that gave no sign of which part a click had landed on. `Agents`

### Removed

- The **Prompts** section is gone. A prompt was text you copied into your own agent, so nothing in Docsbook could run it or tell you whether it ever ran; what it was reached for now lives where it can act — a goal on a schedule is an **Agent**, and "what can I say to this tool" is the one worked example on that tool's own page. Nothing you have to check by hand moved with it. `MCP`
- The **Generate Issues** button is gone from the Issues list. Asking for issues along a stage still works exactly as before — say it to the assistant, or arm the matching agent — the button was one way to compose that request, not a separate capability. `Issues`

## NEW - 03.09.2026

### Added

- Two new content widgets. **Tabs** put parallel versions of the same instruction — npm/pnpm/yarn, macOS/Windows, curl/Python — behind one switch, so a reader stops scrolling past two thirds of a page looking for their own variant; the panels are all in the page source and the switching is CSS-only, so every variant stays readable with JavaScript off and visible to crawlers. **Pricing** turns plans into cards a reader can choose between, or a plan table into a comparison matrix, so the shape of the choice is visible instead of being something the reader has to work out from a table. `Content Widgets`
- `list_content_widgets` now answers "does this page want a widget, and where?" before an agent picks one. Agents were reaching for the two widgets whose examples they had seen and leaving every other moment on the page as plain markdown. `MCP`

### Changed

- Pointing at a block in **interactive mode** now hands you the finished prompt instead of sending it off: it names the page, the section and the exact text it means, it is copied to your clipboard the moment it opens, and it stays editable if you want to add a constraint before you use it. Paste it into the agent that already works on your main branch and the rewrite lands as your own commit, reviewed where you review code — and arming the mode no longer opens anything over the page, so the doc you are pointing at stays the whole screen. `Editor`

### Fixed

- A documentation page's own `title` and `description` now reach the HTML head. Both were being ignored: the `<title>` was built from the body's H1 and the meta description from the first paragraph of the page, which on an index page shipped the widget's `{compass}` icon markers into the Google result. The brand was appended twice on top of that (`— Docsbook | Docsbook`), spending 22 of the title's characters on a repeat, and the JSON-LD `headline` named the page a third way, from the filename. Every page's search result and AI-assistant citation now says what the author wrote, on the apex domain and on custom domains alike. `SEO`
- The published documentation no longer gates features behind the retired Free/Pro/Business ladder. 235 plan labels across the guides, the AI layer, the reference and the analytics pages were telling readers — and any assistant quoting those pages to a buyer — that features already available to everyone required an upgrade. Pages now name what a feature actually consumes: assistant answers, agent runs, page translation and the semantic index draw on the project balance, while hosting, reading, search, GitHub sync, branding and event tracking do not. Unsourced figures went with them, and every price now links to the live pricing page rather than being copied into a page that cannot stay current. `Docs`

## NEW - 02.09.2026

### Added

- The MCP server's agent family is now **135 action tools**, one per step of documentation work rather than one per discipline. Ten verbs — observe, explain, discover, decide, plan, draft, measure, verify, learn, handoff — across fifteen subjects: your capability map, jobs to be done, topical authority, search intent, programmatic SEO, free tools, original research, AI search, competitors, reader vocabulary, content architecture, internal linking, trust, backlinks and market expansion. Ask for a step (`observe_link_graph`, `decide_next_market`, `draft_comparison_page`) instead of an audit, and get rows you can act on instead of a report. `MCP`
- Every action tool names the number it is bought to move — support load, organic traffic, AI citations, time to answer, conversion and eight more — in its own description, so an agent choosing between them is choosing an outcome. `MCP`
- The `draft_*` tools return the artifact itself — the page, the answer block, the link insertions, the outreach message — as markdown ready to apply, and name the call that applies it. They still write nothing themselves, so the whole family stays safe on a read-only token. `MCP`
- **Generate Issues** asks your assistant to look at the project and file what it finds, after two questions: which stage of work you want to be in — observe, understand, discover, decide, plan, execute, measure, verify, learn, coordinate — and which number you want moved. Asking is the point. With no stage named an assistant returns things to *build* every time, and a backlog with no Measure or Verify in it belongs to a team that never finds out whether the last thing it built worked; the pair you pick also selects the agents that already cover it, so the issues come from this project's own evidence rather than from general advice. `Issues`

### Changed

- **MCP agent pricing is now per tool, not per class.** An action tool is priced from the work it declares — how many families of evidence it reads, how many model round trips it may take, whether it leaves your site, whether it writes an artifact — so calls run **$0.0740 to $0.2450** instead of a flat $0.2500, and waits run about 20 s to 70 s instead of a blanket "30 s – 4 min". The narrow tools are now cheap enough to call in a loop. `MCP`
- The 44 previous audit-shaped tools (`audit_seo`, `map_capabilities`, `diagnose_traffic_drop` and the rest) have been replaced rather than renamed. The tools reference lists what took over each one; the four `run_docs_*` background jobs, `audit_geo` and the five `collect_*` collectors are unchanged. `MCP`
- The landing page now shows the real admin panel above the pricing card, in the same signed-out preview the anonymous draft ships, instead of hand-drawn mockups that drifted from the product they pictured. `Landing`

## NEW - 01.09.2026

### Added

- A **Sources** section in the admin panel — what your documentation is allowed to read from. It lists every kind of source Docsbook can read, from your own repository and website to Mintlify, GitBook, ReadMe, Notion, Zendesk, npm and two dozen more, with the ones you have connected lit and the rest offering a **Connect**. Connect one and asking the assistant to update the documentation or resolve drift starts by fetching it, instead of answering from memory: a repository hands back its files, a site hands back its pages. `Sources`

## NEW - 31.08.2026

### Improved

- The client picker on **MCP tools**, **Prompts**, and a tool's own install card now opens on an **Agent** tab by default — one prompt to copy for any agent that can read a playbook, instead of hunting your specific client among eight tabs first. The per-client tabs (Claude Code, Cursor, Codex, and the rest) are still there if you'd rather copy the exact command yourself. `MCP`

## NEW - 30.08.2026

### Added

- Every new project now starts with **$1** of real credit, and a few minutes in a card offers **$5 more** to claim — yours to spend on AI chat, translations, MCP calls or an agent run, with nothing to pay until it runs out. It appears in the sidebar and as a strip across the top of `Billing`, and claiming it is one button. `Billing`
- Your agent can now ask one question and get a checked answer back. Nineteen scenario tools each answer a single question about your docs — which pages are one edit away from traffic they already rank for (`audit_seo`), why traffic fell and what was ruled out (`diagnose_traffic_drop`), which pages you do not have yet (`find_content_gaps`), whether a change actually worked (`verify_change_impact`), whether answer engines can quote you (`audit_geo`), and fifteen more — each returning a structured answer instead of a paragraph to read. `MCP`
- Every finding carries the call that would fix it, so an audit hands straight over to `run_docs_create`, `run_docs_manage` or `run_docs_automate` without anyone translating it in between. All nineteen change nothing themselves and work with a read-only token. `MCP`
- Every tool in the `MCP` catalog now opens with worked example sentences of its own, where half of them previously showed only a line naming the tool and its arguments. The scenario tools, the background agents, goals and funnels, the assistant's own reports, semantic search and access control all gained three to five phrasings each, plus the chains that hand one tool's finding to the next. `MCP`
- The public prompt catalog gained two ways to browse them: **Audits & diagnosis**, for the sentences that ask what is wrong and what the fix would cost, and **Background agents**, for the ones that start work you come back to. `MCP`
- `write_docs` now takes an optional `intent`, so an agent editing your docs over MCP can record what the person asked for, and `get_change_history` hands it back along with any prediction attached to that commit. `MCP`
- An open conversation on the `Chat` page now has **Improve** beside **Analyze**. Analyze reads the transcript for where it went wrong; Improve answers the other question — what to change in your docs so the next reader asking this does not need the chat at all, named at the right layer: a page that should exist, a link that should have connected two pages, or a retrieval problem no rewrite will solve. `AI Chat`
- **Settings ▸ Chat** now has two model settings instead of one. **AI Visitors Chat Model** is what answers your readers; **Admin & AI Agent Model** is what runs the assistant in your dashboard — the one that reads your analytics, calls tools and edits your docs. Picking a stronger model for yourself and a cheaper one for your readers, or the reverse, is now one choice each. `AI Chat`
- Ten new scenario tools answer a question about your **business** rather than about your docs. What every product a buyer considers instead of yours gives away for free, and the need none of them serves (`map_competitor_free_offers`). Which reader question is answered by a working calculator or validator rather than by a paragraph, and whether it is an existing widget, a custom one, or something needing a service behind it (`design_free_tools`). Whether a repeating axis in your product justifies a generated page family, and whether a machine can keep that family correct (`plan_page_family`). `MCP`
- Forty-six worked example sentences for the new tools in the `MCP` catalog, including the chains — competitors' free offers into a buildable tool spec into the agent that ships the page, or a support question into the page that closes it. `MCP`
- Fourteen more scenario tools, one for each method already written in the skills catalog that no tool answered. Why the assistant cannot find an answer that IS on the page (`audit_retrieval`). Which settings are on and doing nothing, checked against the live site rather than the switch (`audit_site_config`). Which pages are really tables served as prose, with the widget from your own catalogue that fixes each (`design_page_widgets`). Which pages the last release made wrong (`diagnose_docs_drift`). `MCP`
- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`

### Changed

- The billing filters on the `MCP` tools list now lead with **Agent** instead of with the cheapest class. The strip scrolls sideways, so at most window widths its tail was off-screen — which put the one family that runs a whole job and hands you back a report where nobody saw it. Sorting the table by billing is unchanged. `MCP`
- Prompts calling a scenario or background-agent tool now show the **PRO** badge they always required. Around eighty-five of them were labelled free while the tool behind them was not. `MCP`
- `diagnose_intent_mismatch` was being quoted at the wrong price and the wrong wait, because both rate tables matched the bare word "intent" from an older, single-tool rule. It is an agent run and now says so — a caller told to expect a few seconds would have given up on something that takes minutes. `MCP`
- The `MCP` tool list was showing the previous build's catalog. Forty-five agent capabilities had shipped, deployed and were answering over MCP while the page listed 101 tools and the **Agent** filter showed only the four background runners — the list is cached hard because it changes only on deploy, and on a fixed address a stored copy was served without ever being rechecked. The request now carries the build that serves it, so a deploy can no longer be answered with the build before it. `MCP`
- **Assistant** in the draft's panel is where you rewrite a page, add one or change the wording, and **interactive mode** in its message box opens the site with the chat beside it and every block clickable, with a way back to the panel in the corner. `AI Chat`
- Three feeds joined the built-in roster: **Translations** (every language generated, outdated or still needed), **Language events** (which languages readers switch the docs into) and **Chat events** (questions the AI assistant was asked, where it came up empty, which answers got a thumbs-down). `Feeds`
- The `Tools` column in `Prompts` is now off by default too, alongside `Tags`. The chips named which endpoints the agent would reach for, and both questions you actually decide on — the price and the payoff — are computed from that same list, with the cost hover naming the dearest thing the prompt touches. Every tool is still listed in the row's card, and the column is one click away in **Columns**. `Prompts`

### Fixed

- The public skills catalog now spells names the way the rest of the product does — `SEO` and `GEO` rather than "Seo" and "Geo". `Skills`

## NEW - 29.08.2026

### Added

- Your agent can now hand a whole documentation job to Docsbook instead of doing it itself. `run_docs_analyze`, `run_docs_create`, `run_docs_manage` and `run_docs_automate` run the matching docs-skill on our side, against your workspace, with the full administrative toolset the skill was written for, and return a run id you read with `get_agent_run`. Work that takes minutes no longer has to fit in one request, and an assistant with no other Docsbook tools connected can still get an audit done. `MCP`
- `get_agent_run`, `list_agent_runs` and `cancel_agent_run` report a run's state and live progress, return its report and everything it changed once it finishes, and stop one that is still going. `MCP`
- Feeds now logs every MCP tool call made against your project alongside the project's own events, showing which tool an agent called, whether it worked, how long it took and what it cost, and filterable by the call's billing class. `Dashboard`

### Removed

- The Skills section of the admin panel, which listed an externally published catalog on its own release schedule and said nothing about your workspace. The catalog still ships and the assistant still opens skills by name. `Dashboard`

## NEW - 28.08.2026

### Added

- A **Getting started** checklist now sits at the bottom of the admin panel's sidebar, showing what your site still needs — its content, your branding, the AI chat, languages, your agent, your domain, and being findable. It ticks steps off as they are configured, collapses to a single row, and disappears once you are done. `Dashboard`

### Changed

- `MCP` and `Skills` are now rows of their own in the admin panel's sidebar, one click each, instead of pages nested inside an `Agents` section. `Dashboard`
- `MCP` and `Skills` now open on the first tool and the first skill instead of a page about the section, so what your agent can do here is on screen the moment you land. `MCP`
- Connecting your project is now the first step on every tool and skill page, with the one sentence to paste into your agent and the exact command for your client under it. It used to come after the step it makes possible, and on a skill it could be missing entirely. `MCP`
- Every tool and skill in the picker now carries an icon, so a list of eighty can be scanned rather than read. `MCP`
- Text, commands and example prompts on the `MCP` and `Skills` pages now scale up on a wide screen instead of staying at phone size. `MCP`
- Each skill's page still carries the example questions for that skill, next to one command to install it and one line to run it. `Skills`

### Removed

- The docs-subagents catalog is no longer browsable in the admin panel. Those agents are still installable from the `docs-subagents` package itself. `Dashboard`

## NEW - 26.08.2026

### Added

- Cards can now carry a body, their own call-to-action link, and a chosen number of columns or a compact horizontal layout, set on the widget marker. `Content Widgets`

### Fixed

- Russian-language pages now emit the FAQ and how-to markup that makes them eligible for rich results and AI answers, and a procedure written as a `stepper` widget is picked up as steps. Widget markers no longer leak into that markup. `SEO`
- A card whose text contains a link no longer breaks its own layout. `Content Widgets`

## NEW - 25.08.2026

### Fixed

- The Changes tab no longer stalls on busy repos — a stale per-run cap could stop it recording new commits once a repo shipped docs faster than it drained them. `Changes`

## NEW - 24.08.2026

### Fixed

- The MCP install commands, raw config and example questions are usable without an account, matching the public MCP page they mirror. `Agents`
- Opening an MCP tool or a skill no longer hides its catalog for the rest of the session — the breadcrumb goes back, and a failed catalog load retries when you reopen the page. `Agents`
- Plan names no longer appear to visitors who have no account, on tool descriptions, skill badges or example prompts. `Preview`

## NEW - 23.08.2026

### Added

- A `Widgets` gallery in settings shows every content widget your pages can render, each with a preview of the block it produces and a page describing the markdown it expects. `Settings`
- Any content widget can now be switched off for a project. Its comments stay in your files and every word between them still publishes; only the rich block is withheld. Switch it back on and every page that used it returns, with nothing to re-write. `Content Widgets`
- `Apply to a page` on a widget closes settings and turns on editing over your docs, offering that widget first on whichever block you pick. `Settings`

### Changed

- The live editor and the assistant now offer only the widgets a project has switched on, so neither can write markers that would not render. `Content Widgets`

## NEW - 22.08.2026

### Added

- `get_page_diff_impact` returns that same country, language and device breakdown, so an agent can tell a translation-shaped audience from a general rise in traffic. `MCP`
- The `Agents` tab has a new `MCP` page listing every tool this project's MCP server serves — read live from the server, so it is never a stale copy — with each tool's description, its arguments, and the sentences to say to a connected agent to make it fire. `Agents`
- The `MCP` page marks the four tools a client can reach with no token at all, so you can see what a reader of your docs could call, not just what you can. `Agents`
- `Needs attention` in the `Feeds` digest counts the events where a reader hit a wall — unanswered chat questions, dead-end searches, stale content and translations, usage limits — separately from routine activity. `Feeds`
- The `Agents` tab has a `Skills` page: every docs skill from the published catalog with its plan gate, install line, the sentences that trigger it, the MCP tools it calls, and its full instructions. `Agents`

### Changed

- The `Agents` tab now drills into a catalogue of every docs-subagents agent grouped by pipeline; picking one lists its ready-to-run prompts instead of a single shared MCP-connection card. `Agents`
- The `api` widget's playground now takes your workspace's colours instead of a fixed blue: the accent, buttons, focus rings and path parameters follow your brand, and the method chips stay readable on a dark or tinted page. `Widgets`
- Tool, agent and skill names across the `Agents` tab read as names (`Docs Planner`, not `docs-planner`), with the machine id kept verbatim under each title. `Agents`

### Fixed

- An `api` widget endpoint with no example no longer renders its form at half width, and a `### Response` block now sits beside the example it should be compared with instead of under the form. `Widgets`
- Documenting `Authorization` in an `api` widget's parameter table no longer renders it a second time as a required query field, which would have put the reader's key in the URL. `Widgets`

## NEW - 15.08.2026

### Fixed

- Widgets on a generated draft site no longer link to pages that were never created. `Draft`

## NEW - 14.08.2026

### Added

- Ask the assistant what to improve and the answer is now a list you tick, not prose you re-type. Each row is one concrete change to one of your real pages, or the settings card that applies it; tick several and press `Apply` once, and they are all done in a single pass. Nothing is ticked for you, and what you leave unticked is never written. The list is drawn from the documentation skill that covers what you asked, what can be measured about your site, and the cards that exist — not from what the model already believed about the topic. `AI Chat`

## NEW - 10.08.2026

### Fixed

- Switching tabs in the settings widget kept the previous tab's scroll position. `Settings`

## NEW - 07.08.2026

### Added

- A `recommendations` widget renders a marked list of findings as cards, ranked by how much each one is costing you. `Docs`

## NEW - 01.08.2026

### Added

- Editing a page can now add content, not just change it: hovering the seam between two blocks reveals a plus button that inserts a paragraph, heading, list, code block, quote, callout, table or content widget right there. `Block Editor`
- Your AI agent can now read a public web page and get it back as clean Markdown, so it can check your docs against a competitor's pricing, your own marketing site, or a link that may have gone dead. `MCP`
- Your AI agent can read and set the call-to-action page through `update_branding`, and sees it on every workspace it reads. `MCP`

### Changed

- The admin/reader mode toggle inside an open chat is gone — the mode now follows how you opened the chat (the admin toolbar starts the builder, a site chat widget starts reader mode). `AI Chat`

## NEW - 31.07.2026

### Added

- A new `Stepper` content widget renders headed sections as a numbered, connected sequence — for installation guides and multi-stage tutorials where order matters. `Content Widgets`
- Two new call-to-action content widgets close a page with the next step the reader should take: `cta` renders a heading and one or two buttons, and `cta-form` turns the primary action into a single field whose value is carried into the target URL. Both stay compact so a documentation page still reads as documentation. `Content Widgets`
- A [Content Widgets](../../content/features/widgets.md) page documents all six widgets, their markdown contract, and how to insert one from the block editor. `Documentation`
- Generated draft sites now close their selling pages with a call-to-action block, chosen from the widget catalog rather than a fixed list, so a newly shipped widget reaches generated sites automatically. `Site Generation`

## NEW - 29.07.2026

### Fixed

- Unlock cards now quote the real numbers instead of stale ones: your monthly AI budget in dollars rather than a query count, 15 supported languages rather than "50+", and the actual chat model and MCP tool counts. `Billing`
- The chat feature is now called `AI Chat` everywhere in the admin panel, instead of switching between "AI Agent" and "AI Chat" between screens. `AI Chat`

## NEW - 28.07.2026

### Added

- Your custom questions now appear as clickable suggestion chips when a reader focuses the chat input, and adding a skill swaps them for that skill's own example questions. `AI Chat`

## NEW - 27.07.2026

### Added

- Filling in a language translates only the missing and outdated pages; pages already up to date are skipped and cost nothing. `Translations`

## NEW - 24.07.2026

### Changed

- Webhook registration now requires the Business plan consistently, whether registered via the dashboard or an MCP agent. `Webhooks`
- `/llms.txt` and the shared preview image now describe Docsbook's current positioning instead of an outdated tagline. `SEO`

## NEW - 17.07.2026

### Added

- `/pricing.md` — a plain-markdown pricing page for AI agents to read directly. `Pricing`

## NEW - 14.07.2026

### Added

- `Copy page menu` card — independent toggles for each item in the `Copy page` dropdown (Skills.md URL, view as Markdown, and shortcuts for ChatGPT, Claude, Cursor, Windsurf, VS Code MCP). `Content`

## NEW - 05.07.2026

### Changed

- Upgrade page no longer shows specific AI-queries-per-month numbers that had drifted out of sync with actual limits. `Billing`

## 0.26.5 - 29.06.2026

### Improved

- Updated landing page feature names for clarity: "AI Agents", "Live Sync", "Auto Translations", "Auto Distribution". `Landing`

## 0.26.4 - 12.06.2026

### Improved

- **Buddy mode:** Converted `/buddy` from command to dedicated skill with isolated context — improves modularity and reduces main session token usage.
- **Agent daemon:** Enhanced reliability with revised `auto-commit.sh` lock handling and improved logging for task transitions.

## 0.26.3 - 11.06.2026

### Fixed

- **Usage attribution:** When a workspace owner uses the docs-chat widget, their token spend is now correctly charged to the "Admin & AI Agent" category instead of inflating the "Readers (AI Chat)" bar — giving an accurate picture of how much visitors actually cost.

## 0.26.2 - 11.06.2026

### Improved

- **Agent daemon:** Token diet for `spawn_session()` — now selects model by priority (P1 → Sonnet, P2/P3 → Haiku instead of fixed Sonnet) and adds bash pre-checks in merger role (skip if PR already merged or base=main). Selective directory copy by role (merger copies only `routines/` + `agents/branch-merger.md` instead of full context).

## 0.26.1 - 11.06.2026

### Fixed

- **Daemon:** Unreleased `agent:working` labels no longer hang forever — added reconcile sweep in `sweep_locks()` to auto-remove labels without live lock files; also fixed repo context (added `-R Docsbook-io/docsbook` to all gh-calls) and network hangs (wrapped git/gh in 20/30s timeouts)
- **Hooks:** `auto-commit-hook.sh` now removes stale lock files (>10 min) instead of skipping forever after crash

## 0.26.0 - 11.06.2026

### Added

- New `/chat` page with full AI agent for docs: search, edit settings, publish changes, and get answers — all in one conversation interface.
- `AdminCard` manifest system — all FloatWidget settings tabs now driven by a single `ADMIN_CARDS` registry, making tabs easier to add and test.
- `watch-issues.sh` script and local agent daemon for automated pipeline tasks.
- `code-scout` subagent — investigates code by problem description and creates GitHub Issues with technical context, so Buddy stays in orchestration mode without reading code directly.
- `qa-agent` now accepts a `FOCUS` parameter when called directly via Agent tool, enabling targeted testing without a full `/qa-plan` sweep.

### Fixed

- Agent pipeline `agent:working` lock now released automatically on any session exit (trap on EXIT in nohup subprocess) — no more manual lock cleanup after agent crashes.

## 0.25.1 - 08.06.2026

### Fixed

- **Skills**: Corrected the `npx install` link on the `/skills` page — now points to the correct `Docsbook-io/docs-skills` package

## 0.25.0 - 04.06.2026

### Added

- **Onboarding**: Interactive 7-step onboarding guide on first login to Docsbook — guided tour highlights key features in FloatWidget toolbar, adapts to user's plan (Free/PRO/PRO+/Enterprise), and remembers when dismissed with `hasSeenOnboarding` flag in `workspaces`
- **Admin**: Fix FloatWidget (toolbar) not appearing for authenticated repo owners after "Start for free" — added direct GitHub repo ownership check in `ensureWorkspaceIfMember()` so owners see the admin interface immediately
- **Skills**: SKILL.md schema preview on detail pages (`/skills/[name]`) — developers now see required/optional frontmatter fields, YAML example from the current skill, and copy-paste instructions before installing with `npx docs-skills install`

## 0.24.0 - 04.06.2026

### Fixed

- **Landing**: Fix `/skills` install command showing hardcoded "25 skills" — now uses dynamic `index.skills.length` (currently 36)

## 0.23.0 - 03.06.2026

### Added

- **Growth**: New `/enrich-audience` command for the first growth-reasoning team — reasons over `about/` + Axiom analytics and appends insights back into the product business-layer. Adds cross-artifact drift contract in `CLAUDE.md` + `AGENTS.md` (MCP ↔ docs-skills ↔ docs-subagents ↔ docs-claude-plugins dependency graph)

## 0.22.2 - 28.05.2026

### Changed

- Official documentation now served at `docsbook.io/docs` — middleware rewrites `/docs/*` internally instead of redirecting to `docsbook-io.docsbook.io`; canonical URLs, sitemap, JSON-LD, and all links updated across landing, admin, and MCP pages

## 0.22.0 - 28.05.2026

### Removed

- Removed server-side Source of Truth indexing — `get_doc_graph`, `read_doc_sections`, `reindex_doc_graph` and the 17 `doc_*` LSP-style MCP tools are gone. Graph search now runs locally via the [docs-claude-plugins](https://github.com/Docsbook-io/docs-claude-plugins) package (`/plugin install docs-sync@docs-claude-plugins`). Deleted `src/lib/source-of-truth.ts`, `src/lib/mcp/lsp-tools.ts`, the reindex REST route, the daily `stale-check` cron and the two smoke scripts

## 0.21.3 - 25.05.2026

### Fixed

- Mobile `/skills` and `/mcp` pages: added hamburger mobile menu to `Header` with full nav links, "Start for free" and "Log in" CTAs
- Mobile `/skills` top padding: reduced from `pt-28` to `pt-20` on mobile (consistent with `/mcp`)
- `SkillsInstallSelector`: install/use columns no longer stack on tablets — now `lg:grid-cols-2`
- `SkillInstallGuide`: install/use columns now split at `sm:` breakpoint for earlier two-column layout

## 0.21.1 - 25.05.2026

### Added

- Short marketing alias `docs.docsbook.io` for the product documentation — opens the same content as `docsbook-io.docsbook.io/docs/*` without redirect (URL stays clean in the browser). New `DOCS_ALIAS_SUBDOMAINS` map in `src/proxy.ts` rewrites `docs.docsbook.io/{path}` → `/docsbook-io/docs/{path}`; `/api/*` is passed through untouched, original subdomain URLs keep working.

## 0.20.2 - 25.05.2026

### Added

- UTM parameters on all internal CTAs leading from `/skills`, `/mcp`, `/docs` (Preview banner), and the blog to the landing page — every `/start` and `/connect` link now carries `utm_source` (`skills` / `mcp` / `preview` / `blog`), `utm_medium` (`nav` / `cta` / `banner`), and `utm_campaign` (e.g. `header_signup`, `mcp_start_free_top`, `preview_connect`, post slug for blog). New `src/utils/utm.ts` helper (`withUtm()`) wires the landing `Header`/`Footer` via an optional `utmSource` prop, the two inline CTAs on `/mcp`, and the `PreviewConnectBanner` on workspace pages. Blog post CTAs (`docusaurus_vs_docsbook`, `mintlify_vs_docsbook`, `gitbook_vs_docsbook`, `ai_search_documentation`, `documentation_seo_guide`, `how_to_host_docs_from_github`, `why_documentation_matters`) now tag their conversions per post. The landing page itself stays UTM-free so internal scroll-to-CTAs aren't mis-attributed

## 0.20.1 - 25.05.2026

### Changed

- Landing page positioning rewritten for AI crawlers — ChatGPT and Perplexity were describing Docsbook as a plain GitBook/Mintlify/Docusaurus alternative, missing the entire AI-Native layer. Hero H1 changed from "The AI Knowledge Platform" to "Docs from GitHub. For humans and AI agents." with concrete subtitle naming MCP, llms.txt, and 15 languages. New full-width "Built for AI agents" bento card with terminal mock (`claude mcp add`), MCP tool grid (`doc_outline`, `doc_search_text`, `read_doc_sections`, …) and client logos (Claude Code, Cursor, ChatGPT, Perplexity, Cline). New "AI Agents" social-proof tab with CTA to `/mcp`. `metadata.title`, `metadata.description`, JSON-LD `SoftwareApplication.featureList`, and FAQPage rewritten to surface MCP server, llms.txt, Source of Truth graph, Skills catalog, and updated pricing ($150 lifetime PRO / $59/mo PRO+) so AI search engines cite the current product correctly

## 0.20.0 - 25.05.2026

### Added

- SEO content hub — 20 new long-tail GEO/AEO blog posts in `docs/blog/` targeting AI search citation (ChatGPT, Perplexity, Claude, Gemini) and high-intent developer queries. Covers comparisons (Docusaurus vs Docsbook 2026, AI docs platform comparison, free hosting comparison, docs as code vs managed), AI infrastructure (`llms.txt` complete guide, JSON-LD for documentation, MCP server for documentation, docs-skills for AI agents, how to get docs cited by ChatGPT, Perplexity citations for docs, multi-language documentation SEO, AI chat build vs buy), migrations (GitBook → Docsbook, Docusaurus → Docsbook), and practical guides (custom domain how-to, API documentation best practices 2026, documentation analytics, README → docs site, why README-only projects need a docs site, best docs platforms for startups 2026). `docs/blog/README.md` restructured into five sections: Foundations, SEO & AI search (GEO/AEO), AI features, Comparisons & migration, Practical guides

## 0.19.0 - 25.05.2026

### Added

- MCP visitor activity drill-down — two new tools on PRO+ (`get_top_visitors` and `get_visitor_activity`) let AI agents investigate what one specific anonymous visitor actually did end-to-end. `get_top_visitors` returns the most active anonymous visitors with a stable hashed `visitor_id`, pageview count, country, and first/last seen; pass that `visitor_id` to `get_visitor_activity` to get the full chronological event timeline (pageviews, page feedback, CTA clicks) with paths and event-specific details (vote, query, href, heading, …). `get_page_journeys` also returns the same `visitor_id` so journeys can be drilled into immediately. `visitor_id` is `sha256(VISITOR_ID_SALT + repoFullName + ip).slice(0,16)` — stable across sessions for the same person within one workspace, but raw IPs never leave Axiom

## 0.18.0 - 24.05.2026

### Added

- Devices, Browsers and AI Visits analytics — new row of cards under Pages/Referrers in the Analytics tab. First card has tabs for `Devices` (Mobile/Desktop/Tablet) and `Browsers` (Chrome, Safari, Firefox, Edge, Brave, Arc, Vivaldi, Yandex…) with favicon icons. Second card lists AI crawler visits (GPTBot, ClaudeBot, PerplexityBot, Google-Extended, Bingbot, Applebot-Extended, Meta-ExternalAgent, CCBot, Bytespider, MistralAI-User and 12+ more) grouped by provider so you can see exactly which AI agents read your docs
- Sitelinks-friendly structured data on the landing — added `SiteNavigationElement` JSON-LD for 8 key sections (Quick Start, AI Features, MCP Server, Agent Skills, Documentation, FAQ, Blog, Changelog), an `ItemList` with top destinations, and `WebSite.hasPart` linking the main pages so Google has explicit signals for generating sitelinks under the docsbook.io result
- New sitemap entries — `/mcp` and `/skills` with priority `0.9`, plus `/connect` with `0.5`, so Google can discover and weigh these promo pages
- Simplified install/use guide on each skill page `/skills/[name]` — tabs for 7 AI clients (Claude Code, Cursor, Codex CLI, Windsurf, Cline, Gemini CLI, Copilot), two steps (Install + Use) with the command pre-filled for this specific skill, plus a runtime-discovery block via Docsbook MCP
- New opinion blog post `/blog/notion-for-docs-engineering-lessons` — first-person engineering essay on why Notion stops working as a docs system once docs leave the building (SEO surface vs internal wiki, version control drift, multilingual coupling, AI crawler discoverability, performance budget, export lock-in, wiki-vs-docs permission split) with a soft Docsbook pitch in the closing section; written for SEO ("notion for documentation") + outreach + objection handling
- Twitter teaser thread for Product Hunt launch at `marketing/twitter/ph-teaser-thread.md` — 9-tweet building-in-public thread (D-10 hook + 7 building-in-public tweets covering Anonymous MCP, llms.txt auto-discovery, TOON format, Docusaurus alternatives guide, attribution tracking, sitelinks JSON-LD, skills install UX + CTA), each tweet ≤280 chars, character counts inline, posting notes with UTM campaign `ph-teaser-twitter`

### Changed

- Moved "Get Support" out of the admin sidebar — replaced the bulky "Help & Support" section with a subtle "Need help? Contact support" footer link pinned to the bottom of the settings modal sidebar, freeing vertical space

### Fixed

- AI Skills cards in the admin no longer 404 on workspace subdomains — clicking a card now opens an in-place modal with the full `SKILL.md` (description, install snippets for 7 AI clients, keywords, MCP tools, GitHub link) instead of routing to `/skills/<name>` which only exists on `docsbook.io`. Landing-page behavior is unchanged

## 0.17.3 - 23.05.2026

### Changed

- Reworked landing header navigation — replaced old category dropdowns (AI, Analytics, Branding, Widgets, Translation) with 3 direct links (`AI`, `MCP`, `Skills`) plus 2 curated dropdowns: `Documentation` (Quick Start, Basics, Creating Docs, Custom Domain, AI Translations, FAQ) and `Blog` (all 5 posts)

## 0.17.1 - 23.05.2026

### Fixed

- Prevent race conditions in monthly usage limits for `AI Chat`, `Translations`, and `Reindex` — concurrent requests could each pass a stale pre-check and push counters past the plan limit (visible as `78/50` pages translated on Pro). Replaced check-then-act with atomic conditional `UPDATE ... RETURNING` in `batchTranslate`, `/api/ai-chat`, and the MCP `reindex` endpoint

## 0.16.0 - 22.05.2026

### Fixed

- Auth redirect loop after GitHub OAuth — stale `callbackUrl` cookie pointing at a subdomain `/connect` caused an infinite redirect cycle; NextAuth `redirect` callback now normalises any subdomain `/connect` → `docsbook.io/connect`

### Added

- Subscription management UI in `FloatWidget` pricing tab — shows current plan, subscription status, next billing date, and Manage subscription button linking to Paddle Customer Portal (Pro+ only)

## 0.15.0 - 22.05.2026

### Improved

- Search widget UX with breadcrumb paths and "Ask AI assistant" option in `Search Bar`

## 0.13.0 - 18.05.2026

### Added

- Documentation graph indexing for AI agents in `Source of Truth` (Enterprise)
- Source of Truth settings panel in `FloatWidget` (Enterprise)

## 0.11.0 - 16.05.2026

### Fixed

- Default theme now always applies when theme-switching widgets are disabled

## 0.10.0 - 15.05.2026

### Added

- Bring-your-own API key for OpenAI, Gemini, Anthropic, OpenRouter in `AI Agent` (Pro/Enterprise)

### Fixed

- AI Agent settings always shows 3 question input fields

## 0.2.0 - 08.05.2026

### Fixed

- AI Agent tab now loads with a single request instead of three

## Related

- [Full Docsbook changelog](../../CHANGELOG.md) — every release, on every axis
- [Changelogs by outcome](./README.md) — the other eleven numbers a release can move
- [Changelogs by panel section](../README.md) — the same releases, cut by where they landed

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: the entry goes in the general changelog, and the axis is read from its wording via src/lib/outcomes/axes.json. -->
