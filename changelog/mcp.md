---
title: "What changed in the Docsbook MCP server, and when it shipped"
description: "Every release that touched the MCP server: the tools it serves, what each call costs, who may call them, and the outcome each tool is bought to move."
---

# What changed in the Docsbook MCP server, and when it shipped

Everything that shipped in **MCP**. This is the MCP slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

## NEW - 15.09.2026

### Added

- Install the Docsbook GitHub App on a repository and unattended runs can publish to it: an agent writing docs on a schedule no longer depends on somebody being signed in, which is why scheduled runs against repositories Docsbook does not host were refused outright. `MCP`

### Changed

- The MCP rate card is re-priced against a measured day of real agent use: Read $8, Write $20, Analytics $40, Egress $60, Probe $120, AI $300, Expert $400 per 1,000 calls, with discovery calls still free. The old card billed a project making 363 calls in a working day 56 cents, which said nothing true about what those calls cost to serve. `MCP`

### Fixed

- `write_docs` no longer reports that it closed an issue when it published straight to the branch without opening a pull request: the closing line only exists in a pull request body, so on that path nothing closed and the issues stayed open while every answer said otherwise. `MCP`

## NEW - 14.09.2026

### Changed

- `list_audits`, `add_audit`, `edit_audit`, `add_audit_finding` and `edit_audit_finding` are now `list_opportunities`, `add_direction`, `edit_direction`, `add_opportunity` and `edit_opportunity` — the old names still work. An assistant writing a technical sentence into a field the owner reads is now refused rather than let through. `MCP`

### Fixed

- `search_prior_work` answers again: GitHub's search API started rejecting queries that name neither issues nor pull requests, so every default call failed and told the caller to rephrase, which could never help. An assistant asking "have we already tried this" was getting nothing back and proposing work already done. `MCP`

### Removed

- The `update_seo`, `update_geo` and `update_aeo` tools are gone: with all three surfaces permanently on there is nothing for them to change, and an agent told "enabled" by a tool that did nothing would keep reporting work it never did. `MCP`
- Reminders — the `list_reminders`, `add_reminder`, `edit_reminder` and `remove_reminder` tools and their Overview tab — are gone. A hypothesis already carries `check_at`/`check_in_days`, its own date to come back and judge it, so a second, separate promise to remember was one more thing to write and one more place to check; writing the claim is now the whole fix. `MCP`

## NEW - 13.09.2026

### Added

- Write down what you expect a docs change to do BEFORE you make it, and Docsbook keeps the claim until its date: `add_hypothesis` records the forecast, `write_docs` attaches it to the change that tests it, and the verdict is recorded against it, so nobody has to reconstruct months later from memory whether a rewrite actually worked. `MCP`
- `link_work` ties an issue, a pull request, a claim, a goal and a reminder into one thread, so the question "did this change work" is answered by the record itself instead of by somebody matching them up by hand. `MCP`
- `search_brief` answers "have we already tried this" across everything written down about a project, rejected claims and their figures included, so the same rewrite is not shipped twice with the same confidence. `MCP`
- A question can now hold a merge: mark one `waiting_on: "owner_blocking"` and the change that depends on your answer is opened as a pull request and left unmerged until you give it, on projects that publish automatically too, so a page written on a wrong guess is caught before it is published rather than after a reader quotes it back to you. `MCP`
- A forecast about your docs now has to name which of the goals you declared it serves and quote the published finding its predicted size comes from, and an assistant that cannot is refused rather than warned, so the hour it spends goes on something you actually asked for instead of on whatever the first reading turned up. `MCP`
- A claim written after its change already shipped is marked as a reconstruction instead of counted as a prediction, so a project that has never once forecast a result stops reading as one whose every change worked. `MCP`
- `list_audits`, `add_audit`, `add_audit_finding`, `edit_audit` and `edit_audit_finding` let an agent build that opportunity table itself and rank what to write next by measured demand instead of by whichever reading came up first, so a week of unattended work goes on the keywords worth having. `MCP`
- `get_mentions` now carries each watched query's earlier checks beside today's, so whether a keyword moved up Google's results page or won a citation in its AI answer is read off the pair instead of remembered, and a ranking claim can be judged on its due date against the reading it started from. `MCP`

### Improved

- Goals, Questions, What Docsbook knows and Reminders are now one card with four tabs — Questions, Memory, Goals and Reminders — each shown as an icon you hover for what it holds, so the two stores an agent reads through `list_memory` and `list_reminders` read on screen as one place instead of four, and an open question, a fact or an overdue reminder stands apart from a closed one by its own icon rather than a tab you had to pick first. `MCP`
- The project brief gains a Hypotheses tab beside Questions, Memory, Goals and Reminders, carrying the claim, its expected effect while it is open and its result once judged, with an overdue verdict flagged amber. `MCP`
- An agent working on your docs is now told to read the goals you declared before it reads a single number, and to go and find published work on the problem before it proposes a fix, so the change it brings you argues for something you asked for and cites where the idea came from instead of reading as a hunch. `MCP`
- A claim about your docs now has to record the reading it starts FROM, not only the one it hopes for: Docsbook takes the before-figure with the same tool that will judge it, keeps it beside the forecast, and refuses a claim whose starting point or predicted size carries no number. So the verdict on a rewrite two weeks later is a comparison against a figure somebody wrote down, and nobody has to reconstruct from memory what the page was doing before an agent touched it. `MCP`
- The Hypotheses tab marks a claim that argues for no declared goal or quotes no source at all, so a forecast nobody could ever settle is visible at a glance rather than only after opening the row. `MCP`

### Fixed

- A claim written before its change no longer reports itself as already being tested: giving it a check date alone used to mark it `testing`, which made both the board and the due list say a change had shipped when nothing had. `MCP`
- "Have we already tried this" no longer answers "your search could not be parsed" when the real reason is that Docsbook cannot see the repository: GitHub returns the same code for a broken query and for one it will not run, and the two now read differently, so an agent stops rewording a question that was never the problem. `MCP`
- The readings that look outside your own docs — a search result, a competitor's page, a public profile — no longer fail with a supplier's product name and one of our own environment variables in the message. They answer in the same words as every other tool here (unavailable, timed out, rate limited, refused), so an agent can act on the answer instead of retrying a configuration problem it has no way to see, and the underlying diagnosis now goes to the operator who can actually fix it. `MCP`
- Writing a page to a Docsbook-hosted site no longer leaves it on a branch nobody looks at. When GitHub refuses the review pull request, the pages are published to the site anyway and the answer says the reviewable record is what went missing, instead of reporting an access failure over work that had already been committed. Sites that hold changes for human review still hold them, and the branch is named so nothing is lost. `MCP`
- A refusal from GitHub now names which permission was missing and whose credential it was, so an operator stops reconnecting a GitHub account that had nothing to do with it. `MCP`

## NEW - 12.09.2026

### Added

- A project with no GitHub repository is no longer turned away: Docsbook can work from your website, a single page, the docs already published here, or two sentences you type about your product, and it says which of those it used. `MCP`
- Ask the new `docsbook` agent about anything in your documentation, in your own words, and it hands your coding agent a short set of instructions to carry out — what it found and what says so, the steps in order, what must not change, and how you know it worked — so the work happens in your own checkout in minutes instead of waiting on a run you cannot watch. `MCP`
- Every instruction says where its work lands: your checkout, one named Docsbook call you make yourself, or a decision only a person can take, so no step is quietly assigned to nobody. `MCP`
- Every answer also comes as markdown, ready to paste into an issue or another session, so the plan does not have to be retyped for whoever picks the work up. `MCP`
- Every read your agent makes is now kept with the answer it gave, which turns any of them into a snapshot: read a page's traffic today, read it again after the rewrite, and `compare_tool_calls` tells you what moved — so "did that change work" stops being a matter of opinion and nobody has to remember to write a number down beforehand. `MCP`
- `list_tool_calls` groups everything ever read here into series — one tool on one page, heading, host or the whole site — and says which already have a second reading to compare against, so you find out what is measurable BEFORE you rewrite a page rather than after, when the baseline can no longer be taken. `MCP`
- `search_tool_calls` finds a past reading by what is inside it — a page it was about, a word in the answer, an error it returned — ranked so the calls actually about `/pricing` come above the fifty that merely mention it, and `get_tool_call` opens one whole. `MCP`
- Docsbook now remembers what is true about your project between sessions: `list_memory`, `add_memory`, `edit_memory` and `remove_memory` hold what these docs are FOR, what nobody has answered yet, and the facts, rules and preferences every agent otherwise works out again on every run — where your real pricing page is, words your product never uses, a section nobody may restructure — so the same question is not answered from scratch, and wrongly, twice. `MCP`
- A **Snapshots** card on Overview shows what has been measured on this project, how many of those readings have a second one to compare against, and a chart of readings per day — because reading something every Monday and reading twelve things on one afternoon in August are the same total and only the first lets you measure a change you make today. `MCP`
- A **What Docsbook knows** card puts that memory in front of you: every line with who wrote it, you or an agent, editable and retirable on the spot, so a recommendation built on something the system was told six weeks ago is something you can find rather than guess at. `MCP`
- `edit_goal` corrects a goal in place — its label, what one completion is worth, what it matches — where the only route before was deleting and recreating it, which broke every funnel that named it and reset the date you started measuring. `MCP`
- A **Goals** card on Overview holds what these docs are FOR, in your own words — the sentence every recommendation an agent makes about your documentation gets argued against, so a rewrite can be judged rather than only described. Declare nothing and the card says so, because an agent working on docs with no stated purpose is the finding. `MCP`
- A **Questions** card holds what nobody has answered yet. An agent writes down the thing it would otherwise have guessed — which of two install paths you actually recommend, whether a section may be reorganised — and you answer it in a line; the answer stays beside the question, so the next run reads it instead of guessing again. `MCP`
- Goals and questions can be closed: mark a goal met with the reading that showed it, answer a question and it keeps the answer, so an agent stops re-proposing work that is already done. An answer you later disagree with can be taken back. `MCP`
- A **Reminders** card on Overview holds what this project promised to come back to and what is due today, so a rewrite you made a fortnight ago gets looked at on the day it can finally be measured instead of whenever somebody happens to wonder — nobody has to keep a check like that in their head or on a calendar of their own. `MCP`
- `add_reminder` is the step the measurement loop never had: your agent records the change, the reading taken before it and the date to look again, in the same breath as making the change, so the effect of a change stops depending on anybody remembering to come back. Say when in days rather than a date and the server does the arithmetic, so a reminder cannot be filed into the past by an agent unsure what today is. `MCP`
- Ask your agent what to do about the docs and it now checks what is already due before it goes looking for something new — work that already has a baseline and a stated prediction beats a fresh idea that has neither, which means less time spent re-deciding what matters this week. `MCP`
- `edit_reminder` closes one with what the reading actually showed, and "nothing moved" counts: a recorded non-result is what stops the same change being made again next quarter with the same confidence. Reminders can be rescheduled rather than quietly cleared, and an answer taken against the wrong baseline can be reopened. `MCP`
- Reminders can be corrected, rescheduled and retired from inside the card as well as over MCP, so a check an agent scheduled for you is one you can move or throw away rather than one you have to live with. `MCP`
- A fact with a known expiry — an API in beta until Q3, a price under review, a version being sunset — can be recorded the day you learn the date, so the page that will be wrong then gets found then instead of by a reader. `MCP`

### Changed

- When Docsbook cannot start yet it answers with what it is missing and every way you could supply it, instead of telling you to go and configure a source. `MCP`
- The instructions your agent reads at connect time are a third shorter and reordered, so the parts that decide where a request goes now survive the 2 KB a client keeps — previously the half explaining how to route was cut off mid-sentence and never reached Claude Code at all. `MCP`
- A request Docsbook cannot place on an outcome — a narrow task like renaming a section, or a sentence in a language the outcome classifier does not read — no longer comes back as a list of outcomes and nothing else: it comes back with the writing rulebook Docsbook's own writers follow, what is actually published on your site, and the rules the edit must not break. `MCP`
- Asking Docsbook what to do is now one of the cheapest calls on the server and changes nothing, so an agent can ask before it knows whether the answer will help, on a read-only token and with no approval to wait for. `MCP`
- The `docsbook` agent is now an expert rather than a planner: ask it anything about your documentation and it answers with how to think about the request, the steps in order with the exact tool on each, what to carry from one step into the next, what the content has to do, what will make the answer wrong, and the rules worth keeping — and then your own coding agent does all of it. `MCP`
- Every step says where its work lands: your own checkout, one named Docsbook call you make yourself, or a subagent worth handing it to. Steps in your checkout name the tools, so "look at what changed" arrives as `git log --since` rather than as a suggestion. `MCP`
- Docsbook now knows what to do about requests that are not outcomes at all — what changed in the last week, add a page for this feature, we have no documentation, alert us when traffic falls, set the site up — each of which used to come back as a list of outcomes to choose from. `MCP`
- A request in Russian now reaches the same advice as its English twin. The outcome classifier reads English only, so anything else used to route nowhere; every workflow now carries the phrasings people actually use, in both languages. `MCP`
- `workspace_id` is optional on the agent, so an assistant that has not picked a project can still ask how the work is done. Name a project and the answer also says what that project can and cannot see, so a step that comes back thin reads as expected rather than broken. `MCP`
- Each answer names the published skill carrying the long-form method for that work, and the exact call that fetches it, instead of restating it. `Skills`
- Ask the `docsbook` agent what counts as success and it now has a workflow for it — read what is already declared, find what readers are trying to do, put one sentence to you, and only then declare it — instead of handing back a list of outcomes to choose from. `MCP`
- Every answer from the `docsbook` agent now opens with the two readings to take before recommending anything: what you declared counts as the docs working, and what your readers actually asked. Advice given without them is true about documentation and unfalsifiable about your site, and an empty answer to either is reported as a finding rather than skipped. `MCP`
- The **What Docsbook knows** card no longer prints the goal count as well — the Goals card owns it, so the same number cannot end up stated two different ways on one page. `MCP`
- Goals, Questions and What Docsbook knows now read like the Analytics cards: tabs for open and closed work, every line editable in a dialog instead of a two-line box, the full list with its evidence and its author behind Details, and the actions on whichever row you are pointing at. `MCP`
- Your snapshots are one card with a tab per group instead of two half-width lists, so the list of what has been measured here has room to grow as the project is worked on. `MCP`
- The one agent on the MCP server is now called `docsbook_expert`, and the old name `docsbook` still resolves to it. A client reads the tool list once when it connects and holds those names until it connects again, so anything already connected when the rename shipped went on asking for `docsbook` and was answered "tool not found" on the very call the server tells every client to make first. Reconnect and you will see only the new name. `MCP`

### Fixed

- Retiring a line Docsbook remembers and then writing the same one again no longer fails: the retired line comes back with the date your project first learnt it intact, and says that is what happened, where before it answered with a database error. `MCP`

### Removed

- The forty-one `agent_<goal>` tools are gone from the MCP tool list, replaced by the single `docsbook` agent — of the forty-one, two had ever been called, because a list that long is not something a model chooses from. `MCP`
- **Standing agents are gone.** The Agents section, the catalog of forty-one routes, the runs behind them, and the `find_agent` and `enable_agent` tools that armed one on a schedule, an event or a repository's commits — all removed. If you had one armed, it has stopped; the runs it already made are still in your issues and pull requests. `MCP`
- What a standing agent was for is still here in pieces you already own: `register_webhook_*` tells your own endpoint when something happens, the `run_docs_*` runs do a piece of work when you ask, and `docsbook` says what the work should be. The recurring part belongs to your own scheduler, which every agent connecting here already has. `MCP`
- The two goal tools added the same morning, `pursue_goal` and `capabilities_for_goal`, went with them: everything they answered is a field of the one `docsbook` answer, and three tools for one question is the problem this release exists to fix. `MCP`
- **The 135 action tools are gone too** — `observe_*`, `explain_*`, `discover_*`, `decide_*`, `plan_*`, `draft_*`, `measure_*`, `verify_*`, `learn_*`, `handoff_*`. One of the 136 had ever been called. Each ran a model on our servers over ordinary reads you can make yourself, so what they charged for was applying a method, not reaching anything you could not. `MCP`
- Ask the `docsbook` agent instead and the method comes back as part of the answer: which reads to make, in what order, what to carry from one into the next, and the trap in each — "classify each query by its wording, not by the page it landed on, because using the landing page here makes the analysis circular". Your own agent then makes those calls on your own token, at read prices. `MCP`
- Every step now also says what a good answer looks like — the columns each row must carry, the values a field is allowed to take, how many rows are worth having — so you can tell whether the method was followed. `MCP`
- Tools that CHANGE something now say so in their own description: write a page, change a setting, file an issue or arm an alert, and the tool tells your agent to ask `docsbook` what the change should be first — because the useful answer is often "not yet, this is thin, go and read X". Reading tools deliberately say nothing of the kind: reading is the consultation. `MCP`
- New workflow for the commonest request there is — changing a page that already exists. It starts by asking what readers were failing to get from it (searches that returned nothing, questions the assistant could not answer, pages voted down) rather than by editing, and it warns you when the page already ranks: change the body before the title, in separate commits, or you cannot tell which one moved it. `MCP`
- `collect_*` and `audit_geo` are their own family on the tool list now — the evidence tools, which gather in code with no model in the path and hand back the exact calls behind every row, so you can re-run them and get the same answer. `MCP`
- `get_change_history` is gone. It could only measure a change that arrived as a commit, and only in traffic, so turning on a language, re-ranking the navigation or fixing an answer the assistant kept getting wrong were all unmeasurable. The snapshots above measure any of them; the commit case keeps `get_page_diff_impact`, which still judges an edit against the pages nobody touched. `MCP`

## NEW - 11.09.2026

### Added

- Build a custom agent with your own allow-list of MCP tools and a plain-English pipeline prompt — it decides which tool to call next and in what order, so a new standing check doesn't wait on us shipping code for it. `MCP`
- Every MCP tool's own page now carries its own subagent — what wakes it, what happens to what it writes, its sources and its prompt — from the first time you open it, so a check you were keeping by remembering to look becomes something that monitors that one thing on a schedule, without building a whole agent first. `MCP`
- Read those checks from an agent, and choose what they watch, with `get_mentions` and `configure_mentions` — so a standing "are we still cited for this?" question stops being something anyone has to remember to look at. `MCP`

### Changed

- Agents — the built-in catalog and any you've built yourself — now live inside MCP instead of their own tab, each opening a full page with its trigger, review mode, sources and prompt rather than a modal. `MCP`

## NEW - 05.09.2026

### Added

- Any coding agent can now search your documentation through your project's public MCP endpoint without signing in — it asks a question in plain words and gets back the pages that answer it, so a machine reading your docs lands on the right page instead of the nearest word match. `MCP`
- Four new MCP tools put the whole drift-loop setup within reach of a coding agent instead of the panel only: `connect_source` and `configure_source` connect a repository or website as a source of truth and manage it, `find_agent` and `enable_agent` search this project's standing agents by outcome and arm one on a schedule, an event, or a connected repository's commits — so an agent asked to keep the docs in step with the code can now reach every step of that itself. `MCP`
- Each MCP tool's own page now shows what a successful call answers with, right below its Arguments — every field named and typed, so wiring up an integration no longer means calling the tool blind to find its shape. `MCP`
- The `update_navigation` MCP tool can now rename what the sidebar shows for any page or folder, so an agent can tell eight sections apart whose files are all called `README.md` and all render as "Introduction". The override changes the sidebar text only, never the page's address or its place in the tree, so no inbound link breaks and nothing is reordered, and the new label is still translated into every enabled language. `MCP`

### Changed

- Searching your docs by meaning is no longer behind a plan or a built index: `search` is on every project, and a project with no semantic index has the same question answered by full-text search rather than refused. A question someone's assistant asks of your docs now comes back answered instead of erroring, so it never has to reach your support inbox. `MCP`

### Fixed

- `list_workspaces` now warns when two of your projects resolve to the exact same live URL — a leftover from before project names were matched by case — and names which one is actually serving it, instead of showing both as equally live and leaving you to guess. `MCP`
- Every "Learn more" link in the panel, and the MCP address printed in `llms.txt` and `get-started.md`, now points straight at the page it names instead of redirecting through a retired address, so an assistant reading those files reaches the live page in one hop. `MCP`
- The MCP tool count quoted on the site and in `llms.txt` was one behind the server (309 against 310 actually registered) and is now read from the same source the server is. `MCP`

## NEW - 04.09.2026

### Added

- Two MCP tools that answer **"have we already tried this?"** before an agent proposes anything. `search_prior_work` searches your repository's issues and pull requests together and says what happened to each — still open, closed without merging, or merged — and `get_pull_request` opens one of them with the files it touched, the agent and run that opened it, the issues it came out of, what reviewers said, and, once it merged, the commit its effect can be measured on. `MCP`
- Fifty-four of the agent capabilities now run that check as their second step, so a recommendation arrives knowing whether this project already made that change and abandoned it. A pull request closed without merging is reported as a change your project rejected, never as a precedent for making it again, which is the reading that used to send the same idea round every quarter. `MCP`
- An MCP tool's page now lists the **agents that use it** — the cards whose route actually calls that tool, armed ones first, each with its own switch — so you can put a tool on a schedule from the page where you just read what a call costs, instead of hunting for it among forty agents. `MCP`
- A tool's **call history** is now the Feeds table narrowed to that tool, so what a call cost and what it answered read the same on the tool's page as they do in Feeds, and expanding a row still shows what went in and what came back. One log, one way to read it. `MCP`

### Changed

- The **MCP** tools table fits the panel again: every column is narrower, spend is one line instead of two, and each `agent_*` tool carries the icon of what it actually does rather than the same robot as the other fifty-three. A second dropdown narrows by **Impact** — what a tool moves — beside the one that narrows by what it costs, because those are two different questions. `MCP`

### Fixed

- Background documentation jobs run again. The health probe in front of them was measuring the router rather than the runner and read a 404 that is the design as "the runner is unreachable", refusing every job for three days. `MCP`

### Removed

- The **Prompts** section is gone. A prompt was text you copied into your own agent, so nothing in Docsbook could run it or tell you whether it ever ran; what it was reached for now lives where it can act — a goal on a schedule is an **Agent**, and "what can I say to this tool" is the one worked example on that tool's own page. Nothing you have to check by hand moved with it. `MCP`

## NEW - 03.09.2026

### Added

- Every MCP tool now has its own page at its own address: the URL carries the tool, so the page survives a refresh and can be bookmarked or sent to a colleague, instead of existing only for whoever happened to click the row. `MCP`
- Clicking a call in a tool's history opens the whole call: what went in, what came back, who asked for it (your own Run, a connected MCP client, a schedule, an event), how long it took, what it was priced at, and what actually left your balance. The price and the billed amount are shown as two figures on purpose, since a call costing less than a cent is charged and still bills $0.00, and either number on its own misreads. `MCP`
- A **Cost** column on that history, so you can see what a tool has been spending on this project without opening a single row. `MCP`
- `list_content_widgets` now answers "does this page want a widget, and where?" before an agent picks one. Agents were reaching for the two widgets whose examples they had seen and leaving every other moment on the page as plain markdown. `MCP`

### Security

- `list_workspaces`, `get_workspace` and the fifteen `update_*` tools no longer return the raw workspace row. The project's live REST API key is replaced by `hasApiKey`, and the semantic index blob (95% of one answer, 2.1 MB across `list_workspaces`, which clients refused whole) by `hasSourceOfTruthGraph` plus `sourceOfTruthLastIndexedAt`, so an MCP client gets an answer it can act on and no transcript downstream of a call holds a working credential. `MCP`

## NEW - 02.09.2026

### Added

- The MCP server's agent family is now **135 action tools**, one per step of documentation work rather than one per discipline. Ten verbs — observe, explain, discover, decide, plan, draft, measure, verify, learn, handoff — across fifteen subjects: your capability map, jobs to be done, topical authority, search intent, programmatic SEO, free tools, original research, AI search, competitors, reader vocabulary, content architecture, internal linking, trust, backlinks and market expansion. Ask for a step (`observe_link_graph`, `decide_next_market`, `draft_comparison_page`) instead of an audit, and get rows you can act on instead of a report. `MCP`
- Every action tool names the number it is bought to move — support load, organic traffic, AI citations, time to answer, conversion and eight more — in its own description, so an agent choosing between them is choosing an outcome. `MCP`
- The `draft_*` tools return the artifact itself — the page, the answer block, the link insertions, the outreach message — as markdown ready to apply, and name the call that applies it. They still write nothing themselves, so the whole family stays safe on a read-only token. `MCP`
- Every tool's page and the tools reference now carry a **per-tool price and wait**: the [MCP tools reference](../reference/mcp-tools.md) lists all 135 with what only that one tells you, what it costs, and how long the call is held open. `MCP`
- The assistant can now read and write that tracker itself — `list_issues`, `get_issue` and `create_issue`, in the admin chat and over your MCP endpoint. Ask it to open an issue, add something to the backlog, or write down what an audit just found, and the finding outlives the conversation instead of ending with it. Filing needs a read-write token; reading does not. `MCP`
- `generate_issues` runs issue generation as a background job, so it keeps working after you close the panel and can be started from Claude Code or Cursor without opening it at all. `MCP`
- The MCP tools table now carries an **Impact** column: which number each tool works on and which way that number is good news, so you can tell what a tool is for before you spend a call on it. No percentage — one call is a step inside a plan the table never reads, and a figure there would be a forecast rather than a fact. `MCP`

### Changed

- **MCP agent pricing is now per tool, not per class.** An action tool is priced from the work it declares — how many families of evidence it reads, how many model round trips it may take, whether it leaves your site, whether it writes an artifact — so calls run **$0.0740 to $0.2450** instead of a flat $0.2500, and waits run about 20 s to 70 s instead of a blanket "30 s – 4 min". The narrow tools are now cheap enough to call in a loop. `MCP`
- The 44 previous audit-shaped tools (`audit_seo`, `map_capabilities`, `diagnose_traffic_drop` and the rest) have been replaced rather than renamed. The tools reference lists what took over each one; the four `run_docs_*` background jobs, `audit_geo` and the five `collect_*` collectors are unchanged. `MCP`
- The MCP page's title bar now shows a **Connect MCP** button instead of a copyable project URL — it opens a guide with the exact command or config for your client. Every MCP URL shown in the admin panel now points at the shared `docsbook.io` endpoint rather than a workspace subdomain, matching how connecting actually works: authorization is scoped to your account, not to one project's URL. `MCP`

## NEW - 01.09.2026

### Added

- `list_sources` and `read_source` are served over your project's MCP endpoint, so a source you register means the same thing in Claude Code or Cursor as it does in the panel. Scenario tools that already read the outside world now reach your registered source instead of guessing at an address. `MCP`

## NEW - 31.08.2026

### Improved

- The client picker on **MCP tools**, **Prompts**, and a tool's own install card now opens on an **Agent** tab by default — one prompt to copy for any agent that can read a playbook, instead of hunting your specific client among eight tabs first. The per-client tabs (Claude Code, Cursor, Codex, and the rest) are still there if you'd rather copy the exact command yourself. `MCP`

## NEW - 30.08.2026

### Added

- Five **collectors** in `MCP` hand back the evidence an audit is built on, without the opinion, at **$0.0040** a call against the audit's $0.25. `collect_page_text` fetches your live pages and reports what the wire actually serves — status, title, headings, and how many words survive with no JavaScript — beside the size of the source stored for the same path. `collect_corpus_map` maps every page with its size, depth and whether navigation reaches it. `collect_assistant_questions`, `collect_traffic` and `collect_onsite_search` return what readers asked, how their visits ended, and what they typed into your search box. `MCP`
- Every collector answer carries a **`reproduce`** block: the exact calls and arguments behind each row, so you can re-run them yourself and get the same record. There is no model in the path, so there are no findings, no scores and nothing to take on trust — and an evidence figure that traces to no call fails the answer rather than shipping. `MCP`
- That makes the cheap one the right one more often than it sounds. With no Search Console connected, `audit_seo` still charges a quarter of a dollar to score its ranking axes as unmeasured, while `collect_corpus_map` needs no search data, no traffic and no history and returns real rows on a site that went up this morning. `MCP`
- A source a collector could not read is said out loud three times over — what was skipped, what having it would have added, and which call failed and why — and a rate with nothing to divide by comes back as unmeasured rather than as zero. `MCP`
- The `MCP` catalog gained a **Probe** billing class for them, priced between Egress and AI, and the filters, the price column and the typical-time column all carry it. `MCP`
- Your agent can now ask one question and get a checked answer back. Nineteen scenario tools each answer a single question about your docs — which pages are one edit away from traffic they already rank for (`audit_seo`), why traffic fell and what was ruled out (`diagnose_traffic_drop`), which pages you do not have yet (`find_content_gaps`), whether a change actually worked (`verify_change_impact`), whether answer engines can quote you (`audit_geo`), and fifteen more — each returning a structured answer instead of a paragraph to read. `MCP`
- Every number in those answers has to trace to evidence the run actually gathered, and one that traces to nothing fails the call rather than shipping. An invented figure is no longer something you have to check for. `MCP`
- Where a scenario tool scores your docs, the score is computed from that evidence with its weights published alongside it, so two runs are comparable; an axis that could not be checked reports as unmeasured rather than as zero. `MCP`
- Every finding carries the call that would fix it, so an audit hands straight over to `run_docs_create`, `run_docs_manage` or `run_docs_automate` without anyone translating it in between. All nineteen change nothing themselves and work with a read-only token. `MCP`
- Every tool in the `MCP` catalog now opens with worked example sentences of its own, where half of them previously showed only a line naming the tool and its arguments. The scenario tools, the background agents, goals and funnels, the assistant's own reports, semantic search and access control all gained three to five phrasings each, plus the chains that hand one tool's finding to the next. `MCP`
- The public prompt catalog gained two ways to browse them: **Audits & diagnosis**, for the sentences that ask what is wrong and what the fix would cost, and **Background agents**, for the ones that start work you come back to. `MCP`
- `MCP` now carries the same **Run now** / **Schedule** / **On event** buttons the `Prompts` toolbar has, asked tool-first: pick the tool, then pick from the prompts that call it. Each prompt shows the schedule or event it already has, so arming one never silently replaces a run you set up earlier, and putting a tool on a weekly schedule no longer means leaving the section to go and find its prompt. `MCP`
- `write_docs` now takes an optional `intent`, so an agent editing your docs over MCP can record what the person asked for, and `get_change_history` hands it back along with any prediction attached to that commit. `MCP`
- Ten new scenario tools answer a question about your **business** rather than about your docs. What every product a buyer considers instead of yours gives away for free, and the need none of them serves (`map_competitor_free_offers`). Which reader question is answered by a working calculator or validator rather than by a paragraph, and whether it is an existing widget, a custom one, or something needing a service behind it (`design_free_tools`). Whether a repeating axis in your product justifies a generated page family, and whether a machine can keep that family correct (`plan_page_family`). `MCP`
- Six more of them: which numbers you already hold that nobody outside could obtain at any price, and which clear a privacy and contractual gate (`assess_research_assets`); whether a stranger would ever cite one of your pages, and which inbound links now arrive at something broken (`audit_linkability`); which repeated questions reach a person that a page would have closed, ranked by how many *different* people asked (`assess_support_deflection`); which third-party tools readers try to use you with and you never mention (`map_integration_demand`); what an evaluator on a named incumbent cannot find (`assess_competitor_switching`); and what shipped and stayed invisible (`audit_release_adoption`). `MCP`
- `assess_content_roi` is the one that gives you permission to stop: which pages earn their upkeep, and which to merge, redirect or retire. It works out which low-traffic pages are protected by inbound links or assistant citations **first**, and never proposes retiring one of those — deleting a page something external points at spends a link profile that cannot be bought back. `MCP`
- Every one of the ten is read-only and comes back with a refusal list beside its answer: the tool candidates rejected with the test they failed, the datasets blocked with the specific blocker, the rival claims you should *not* write toward. A run with nothing refused did not look. `MCP`
- Forty-six worked example sentences for the new tools in the `MCP` catalog, including the chains — competitors' free offers into a buildable tool spec into the agent that ships the page, or a support question into the page that closes it. `MCP`
- Fourteen more scenario tools, one for each method already written in the skills catalog that no tool answered. Why the assistant cannot find an answer that IS on the page (`audit_retrieval`). Which settings are on and doing nothing, checked against the live site rather than the switch (`audit_site_config`). Which pages are really tables served as prose, with the widget from your own catalogue that fixes each (`design_page_widgets`). Which pages the last release made wrong (`diagnose_docs_drift`). `MCP`
- And ten more: what should keep happening without anybody remembering, and whether each check belongs in a hook or in CI (`plan_automation_workflows`); which of these tools your workspace can answer with at all, and the cheapest thing to connect (`assess_setup_readiness`); the material you already have that could be docs, support answers and community threads included (`map_content_sources`); whether this kind of change has ever worked here before you repeat it (`assess_fix_precedent`); which two to four tools your question actually calls for (`plan_audit_route`); what each number is worth to the business (`map_business_value`); whether the corpus reads as an authority or as a site that mentions a topic (`map_topic_authority`); the region readers can only reach from the sidebar (`audit_internal_links`); which languages are read and which translations are behind their source (`audit_translation_coverage`); and what shape of answer a query wanted against what the ranking page delivers (`diagnose_intent_mismatch`). `MCP`
- Forty-two more worked examples in the `MCP` catalog, and ten existing prompts now call one of the new tools where it changes the answer — the unanswered-questions prompt now splits "the page is missing" from "the page exists and nothing can retrieve it", and the striking-distance prompt now says whether the page is simply the wrong shape for the query. `MCP`

### Changed

- The billing filters on the `MCP` tools list now lead with **Agent** instead of with the cheapest class. The strip scrolls sideways, so at most window widths its tail was off-screen — which put the one family that runs a whole job and hands you back a report where nobody saw it. Sorting the table by billing is unchanged. `MCP`
- Prompts calling a scenario or background-agent tool now show the **PRO** badge they always required. Around eighty-five of them were labelled free while the tool behind them was not. `MCP`
- `diagnose_intent_mismatch` was being quoted at the wrong price and the wrong wait, because both rate tables matched the bare word "intent" from an older, single-tool rule. It is an agent run and now says so — a caller told to expect a few seconds would have given up on something that takes minutes. `MCP`
- The `MCP` tool list was showing the previous build's catalog. Forty-five agent capabilities had shipped, deployed and were answering over MCP while the page listed 101 tools and the **Agent** filter showed only the four background runners — the list is cached hard because it changes only on deploy, and on a fixed address a stored copy was served without ever being rechecked. The request now carries the build that serves it, so a deploy can no longer be answered with the build before it. `MCP`
- The seven billing filters on the `MCP` tools list are now one **Filters** button, the same control the `Prompts` toolbar carries. Six of them were switched off at any moment while taking the room that **Run now**, **Schedule** and **On event** now have; whichever classes you turn on stay on the line beside the button, each with its own way out, and the menu still prints each class's price. `MCP`
- Hovering a tool on that list now opens a card with everything its own page used to say: what it does, the price per call, the typical wait, how many arguments it needs and how many of them are required, how many worked examples call it, and — for your own project — what it has cost you and when it last ran. The callable id sits in it, ready to copy. `MCP`
- Clicking a tool row now opens the prompts that call it, which is what its green **Play** always did, instead of a page about the tool. Everything that page said is on the card above, and the sentences you can actually send are one click away rather than two. `MCP`
- The `MCP` section now opens with a **Turn on** of its own, and that panel carries the installer: pick your client from the chips, copy the command, then press the button to walk the tool table with a guide. Connecting your editor and meeting the catalog now happen in one place, instead of the install card sitting one click deeper on a single tool's page. `MCP`
- MCP calls are now charged to the balance of the project the call is about — the same balance a top-up funds. They were previously metered against your profile, which nothing tops up, so paying credited a row the billing never read. `MCP`
- Running out of balance now names which project ran out, what the call costs, what is left, and where to top that project up, instead of offering a tier to buy or a monthly reset to wait for. `MCP`

### Fixed

- An `MCP` scenario tool given a malformed piece of evidence now fails the call and says so, instead of crashing partway through scoring. `MCP`
- The public skills catalog now spells names the way the rest of the product does — `SEO` and `GEO` rather than "Seo" and "Geo". `Skills`

### Improved

- A scenario tool run now starts with exactly the tools its method needs already loaded, instead of spending its first round trips discovering them. Each of the 45 capabilities declares what it may call, the run is held to that declaration, and a capability that never said it goes outside your site does not go outside it. `MCP`

## NEW - 29.08.2026

### Added

- Your agent can now hand a whole documentation job to Docsbook instead of doing it itself. `run_docs_analyze`, `run_docs_create`, `run_docs_manage` and `run_docs_automate` run the matching docs-skill on our side, against your workspace, with the full administrative toolset the skill was written for, and return a run id you read with `get_agent_run`. Work that takes minutes no longer has to fit in one request, and an assistant with no other Docsbook tools connected can still get an audit done. `MCP`
- `get_agent_run`, `list_agent_runs` and `cancel_agent_run` report a run's state and live progress, return its report and everything it changed once it finishes, and stop one that is still going. `MCP`

### Changed

- The admin panel's MCP section is now one searchable, sortable table of every tool with its billing class and how much of your monthly allowance it buys, instead of a picker column showing one tool at a time. Tools you can compare are tools you can budget for. `MCP`
- Docsbook MCP tool calls are now billed **per call** against your account balance, at the flat price shown on each tool's row — fixed before the call and independent of how big the answer is. Discovery, connecting and creating a workspace stay free, a failed call says so, and a call we never ran is never charged. `MCP`
- Every MCP tool call now runs as a background job instead of inside the web request, so a tool can no longer be cut off by a request time limit and each call leaves its own durable record. Quick calls take a little longer in exchange. `MCP`
- Each row of the MCP tools table is now a single line, so the whole catalogue reads at a glance; the callable id stays on the tool's own page and on hover. `MCP`

## NEW - 28.08.2026

### Added

- The MCP server now offers a semantic `search` tool that finds documentation by what it means rather than its exact wording, reusing the workspace's existing vector index at no extra indexing cost. `MCP`

### Changed

- `MCP` and `Skills` now open on the first tool and the first skill instead of a page about the section, so what your agent can do here is on screen the moment you land. `MCP`
- Connecting your project is now the first step on every tool and skill page, with the one sentence to paste into your agent and the exact command for your client under it. It used to come after the step it makes possible, and on a skill it could be missing entirely. `MCP`
- Every tool and skill in the picker now carries an icon, so a list of eighty can be scanned rather than read. `MCP`
- Text, commands and example prompts on the `MCP` and `Skills` pages now scale up on a wide screen instead of staying at phone size. `MCP`
- Each skill's page still carries the example questions for that skill, next to one command to install it and one line to run it. `Skills`

## NEW - 23.08.2026

### Added

- The average product price can also be set from the assistant and over MCP, through `update_branding`. `MCP`

## NEW - 22.08.2026

### Added

- `get_page_diff_impact` returns that same country, language and device breakdown, so an agent can tell a translation-shaped audience from a general rise in traffic. `MCP`

## NEW - 21.08.2026

### Fixed

- `docsbook.io/<owner>/<repo>/api/mcp/server` now answers MCP clients that follow redirects. The redirect to your project dropped the request body, so a tool call arrived empty and the endpoint replied "Invalid JSON" instead of listing your tools. `MCP`

## NEW - 14.08.2026

### Fixed

- A `GET` to the MCP server routes is rejected outright instead of hanging until the request is killed. `MCP`

## NEW - 01.08.2026

### Added

- Your AI agent can now read a public web page and get it back as clean Markdown, so it can check your docs against a competitor's pricing, your own marketing site, or a link that may have gone dead. `MCP`
- Your AI agent can read and set the call-to-action page through `update_branding`, and sees it on every workspace it reads. `MCP`

## NEW - 31.07.2026

### Fixed

- Documentation edits made through a connected AI tool no longer report success while writing to an abandoned repository, on projects that were moved to their own GitHub. `MCP`

## NEW - 24.07.2026

### Changed

- MCP tool count claims corrected to the real number across the site and `/llms.txt`. `MCP`

## Related

- [Full Docsbook changelog](../CHANGELOG.md) — every release, across every section
- [MCP server](../agent-ready/mcp.md) — connecting an agent to your docs
- [MCP tools reference](../reference/mcp-tools.md) — every tool, its price and its wait
- [Changelogs by panel section](./README.md) — the same releases, cut by where they landed
- [Changelogs by outcome](./outcomes/README.md) — the same releases, cut by the number they move

<!-- Generated by scripts/changelog/split.mjs from docs/CHANGELOG.md. Do not edit by hand: add the entry to the general changelog with its component tag and rerun the script. -->
