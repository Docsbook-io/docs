---
title: "What changed in the Docsbook MCP server, and when it shipped"
description: "Every release that touched the MCP server: the tools it serves, what each call costs, who may call them, and the outcome each tool is bought to move."
---

# What changed in the Docsbook MCP server, and when it shipped

Everything that shipped in **MCP**. This is the MCP slice of the [full Docsbook changelog](https://docsbook.io/docs/CHANGELOG).

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
