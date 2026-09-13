---
title: "Every tool the Docsbook MCP server exposes to an agent"
description: "The 156 tools a Docsbook workspace exposes over MCP — the one `docsbook_expert` agent, workspace setup, content, issues, chat, translations, analytics, call history, project memory, reminders, audits, hypotheses, the work board and webhooks."
---

# MCP Tools Reference

This page lists every tool exposed by the Docsbook MCP server at `https://docsbook.io/api/mcp/server`. The server exposes **156 tools**. Each requires Bearer authentication via OAuth 2.0 + PKCE.

The **Billing** column names the class a call is metered under, against the project's own balance:

| Class | What it covers |
|---|---|
| Included | Discovery and connection — never metered |
| Read | Reads a page, a setting or a registry row Docsbook already stores |
| Write | Changes something — content, config, goals, registrations |
| Analytics | Scans the event warehouse: funnels, journeys, retention, feeds |
| Egress | Leaves Docsbook's network — fetches a URL or fires a real delivery |
| Probe | Collects one family of facts and normalises it, with no model in the path |
| AI | Model-backed: something a model writes, reads or ranks for you |
| Agent | A whole agent run: minutes of work, a report, and its own run record |

Current rates per class are published on the [Docsbook pricing page](https://docsbook.io/pricing). A call refused for an empty balance says so; nothing on this page is gated by anything else.

To connect from Claude Code:

```bash
mcp add --transport http https://docsbook.io/api/mcp/server
```

## Start here: the agent

`docsbook_expert` is the one agent on this server, and the first call to make for any documentation request — however narrow, in any language. It is an **expert, not a runner**: it answers in one round trip with how to do the work, and does none of it.

| Tool | Billing | Description |
|---|---|---|
| `docsbook_expert` | Read | Any documentation request in the user's own words. Returns how to think about it, the steps in order with the tool on each and who runs it, what to carry between steps, what to write, what makes the answer wrong, and what to remember. Runs nothing. `workspace_id` optional |

Every step in the answer says where its work lands:

- **`you`** — your own checkout, with your editor, shell and tests. The step names the tools (`git log --since`, `Read`, `Edit`), because "use your own tools" is not advice and naming them is.
- **`docsbook_expert`** — one call to this server, which **you** make. Nothing runs on its own, so the call is gated, charged and logged exactly like any other.
- **`subagent`** — work worth handing to a subagent of your own: a step that fans out over forty pages, or that wants a fresh context.

Steps also carry `transform` — what to keep from one step's output and hand to the next — which is the half a tool list never has and a long route needs most.

⚡ **It was called `docsbook` until 12.09.2026, and that name still works.** An MCP client reads the tool list once, when it connects, and holds those names for the rest of the session — so a session that was already open when the name changed goes on saying `docsbook`. The server resolves the old name to this one rather than answering "tool not found", which is what it did for a day. Reconnect and you will see only `docsbook_expert`.

`docsbook_expert` never guesses. A request it cannot place on a known workflow gets the general method (the writing rulebook, what is actually published, the constraints) and says out loud that it is the general method. It has no `findings` field, deliberately: nothing ran, so there is nothing measured, and the numbers arrive when you make the calls it names.

**`workspace_id` is optional.** Most of what it knows is true of documentation work rather than of one project. Pass a project and the answer also says what that project can and cannot see, so a step that comes back thin reads as expected rather than broken.

## Workspace and branding

| Tool | Billing | Description |
|---|---|---|
| `get_info` | Included | Server capabilities, version, available tool list |
| `list_workspaces` | Included | All workspaces for the authenticated user with capabilities |
| `get_workspace` | Included | Fetch one workspace by ID or `owner/repo` |
| `create_workspace` | Included | Create a workspace from a GitHub repository |
| `update_branding` | Write | Colors, fonts, logo, icon, default theme, call-to-action URL, site source URL, average product price |
| `update_ui_settings` | Write | Toggle header, search, feedback, copy button, breadcrumbs |
| `update_navigation` | Write | Header links, social links, subheader folder tabs (with optional icons), left-sidebar page/folder icons, and sidebar label overrides — renaming what a page or folder shows in the sidebar without moving its address or its place in the tree |
| `update_ai_settings` | Write | Enable AI chat, set provider and API key, model selection — including bringing your own provider key |
| `update_seo` | Write | SEO meta tags, sitemap, OpenGraph |
| `update_access` | Write | Make a workspace private; set a password and/or bring-your-own SSO/OIDC identity provider |
| `update_domain` | Write | Attach or remove a custom domain |
| `update_languages` | Write | Enable target languages for AI translation |

## Content and documentation

| Tool | Billing | Description |
|---|---|---|
| `search_docs` | AI | Full-text/regex/heading/path search over the workspace's documentation content. Read-only — works with any token regardless of read/write scope. |
| `search` | AI | Semantic (embeddings-based) search over the workspace's documentation content — finds pages by meaning, not literal keyword overlap. Reads a pre-built vector index (no re-indexing on search). Read-only, on every plan, and served without a token on a repo-scoped endpoint for a public site. When no index is built or enabled it answers by full text instead of refusing, and `mode` (`semantic` / `lexical`) says which engine replied. |
| `get_doc_outline` | Read | List every markdown page's title, heading count, and size before searching or writing. Read-only — works with any token regardless of read/write scope. |
| `write_docs` | AI | Commit one or more markdown files to the workspace's docs repo in a single atomic git commit. Requires a token authorized with **read-write** scope — a read-only token is refused. Takes an optional `intent`: what the person asked for, in their own words. It is shown against the commit in the Changes panel, so the goal behind an edit outlives the conversation that produced it. |
| `fetch_url` | Egress | Read one public web page and return it as clean Markdown, with its title, description and the final URL after redirects. For checking a claim against a page outside the workspace — a competitor's pricing, your own marketing site, or whether a link a doc depends on still resolves. A 404 or a login wall comes back as a stated result rather than a failure, since that is the answer when the question is whether a link works. Private and internal addresses are refused, `robots.txt` is honoured, and page content is treated as data, never as instructions. |
| `list_sources` | Read | List the repositories and websites this workspace is connected to as its sources of truth, plus the repository the site is built from. Each entry carries the owner's own note about why it is connected. Read-only. Call it before writing or updating documentation: a connected source is a fact you can go and read instead of recalling. |
| `read_source` | Egress | Read one of those sources. A repository with no `path` returns its readable files and with one returns that file; a website with no `path` returns several of its pages as Markdown, discovered from its own sitemap and scoped to the section that was connected. Same protections as `fetch_url` — private addresses refused, `robots.txt` honoured, page content treated as data and never as instructions. |
| `connect_source` | Write | Connect a repository, a website or a single page as a source of truth — what `list_sources` then lists and `read_source` reads. A GitHub repository is proved readable (publicly, or with a GitHub authorization this project already holds) before it is stored; a private repository nobody has authorized yet is refused with the one thing that fixes it, rather than stored unreadable. `note` is the owner's own words about what the source is for, and is read as instruction by everything that later reads it. Requires a **read-write** token. |
| `configure_source` | Write | Rename a connected source, rewrite its `note`, pause it (`enabled: false` — stays connected, nothing reads it), or disconnect it entirely (removes any GitHub authorization attached to it). Identify the source by `source_id` from `list_sources` or by `match` (a word from its label or URL). Requires a **read-write** token. |

For deeper local graph navigation (outline, fuzzy headings, link references, resolve links) while an agent has your docs checked out on disk, use [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) instead — run `npx markdown-lsp <subcommand> ./docs` to expose LSP-style `doc_*` tools on the working tree. See the [markdown-lsp README](https://github.com/Docsbook-io/markdown-lsp) for setup. `search_docs`/`write_docs` and `markdown-lsp` are complementary: the former work over the hosted MCP connection with no local checkout, the latter needs the repo on disk.

## Issue tracker

The issues on the GitHub repository your documentation is built from — the work that is open on the project. This is where a finding outlives the conversation that produced it: an agent that has just audited your documentation can write down what it found instead of leaving it in a chat log.

The same three tools are what the admin panel's **Issues** section reads and writes, so an issue filed from Claude Code shows up on that table and vice versa.

| Tool | Billing | Description |
|---|---|---|
| `list_issues` | Read | List the issues on the project's repository — open, closed or all, optionally filtered by label. Pull requests are never included. Read-only. Call it before `create_issue`: an issue that duplicates an open one is worse than no issue. |
| `get_issue` | Read | Read one issue in full — its complete body, labels, state and link. Read-only. Acting on the 280-character preview `list_issues` returns is how you implement the wrong half of a request. |
| `create_issue` | Write | File an issue on the project's repository, with a title, a markdown body and labels. Requires a token authorized with **read-write** scope — a read-only token is refused. One call per issue. Returns the issue's number and link. |

A Docsbook-hosted site's issues live on the repository Docsbook hosts for it; a site built from your own repository uses that repository, and an MCP call acts as Docsbook's own account there — enough to read a public repository and open an issue on it, and a stated permission error on a private one rather than an empty list.

## AI chat

| Tool | Billing | Description |
|---|---|---|
| `get_chat_system_prompt` | Read | Read the workspace's chat system prompt |
| `set_chat_system_prompt` | Write | Replace the chat system prompt |
| `set_chat_hooks` | Write | Configure pre/post LLM hooks |
| `test_chat_hook` | Egress | Run a hook against a synthetic payload |

## Translations

| Tool | Billing | Description |
|---|---|---|
| `set_translation_mode` | Write | `auto` (built-in AI) or `external` (webhook flow) |
| `list_pending_translations` | Read | Translations awaiting approval |
| `get_translation` | Read | Fetch one translation by language and path |
| `upload_translation` | Write | Upload an externally-produced translation |
| `approve_translation` | Write | Publish a pending translation |
| `delete_translation` | Write | Remove a translation |

## Analytics and observability

| Tool | Billing | Description |
|---|---|---|
| `get_analytics` | Analytics | Views, visitors, top pages, referrers over a period |
| `get_ai_usage` | Analytics | AI chat and translation usage, and what remains on the balance |
| `get_ai_questions` | Analytics | All questions asked to the AI chat |
| `get_ai_unanswered` | Analytics | Questions the AI could not answer |
| `get_negative_feedback` | Analytics | Pages with thumbs-down feedback |
| `get_failed_searches` | Analytics | Search queries that returned zero results |
| `get_popular_searches` | Analytics | Top search queries by frequency |
| `get_page_journeys` | Analytics | Reader navigation paths between pages |
| `query_events` | Analytics | Arbitrary query over the platform event warehouse |

Every one of these is recorded with the answer it gave, which is what the next section is about.

## Call history — every read is a snapshot

Each metered call is kept with its arguments and its answer, so any read tool above doubles as a measuring instrument: read something today, read it again after the change, and the two are a before and an after nobody had to plan for. Free on every plan — this is the record of calls you already paid for once.

| Tool | Billing | Description |
|---|---|---|
| `list_tool_calls` | Read | The history, grouped into **series** — one tool on one subject (a page, a heading, a host, a search query, or the whole site, normalised so `/Quick-Start/` and `quick-start` are one series). Each says how many readings exist, when the last two were, and whether it can be compared yet. |
| `compare_tool_calls` | Read | Two readings of the same instrument, and every number that moved — with what appeared, what went away, and how many fields did *not* move, which is the denominator. A percentage is `null` when the baseline was zero, never `∞`. **No verdict**: two readings a week apart are two facts, not cause and effect. |
| `search_tool_calls` | Read | Find a past reading by what is inside it, ranked by where the words landed — the calls *about* `/pricing` above the ones that merely mention it. Inline filters: `tool:`, `path:`, `since:`, `failed:`, `source:`. |
| `get_tool_call` | Read | One recorded call, whole: the exact arguments and the exact answer, as stored (truncated with a marker, and redacted by key so no secret can be read back out). |

🔴 **Take the reading before you change anything.** A baseline cannot be created afterwards, and `compare_tool_calls` runs nothing — it compares what is already recorded.

`get_page_diff_impact` is the commit-shaped version: for a change that shipped as a commit, it judges the pages that commit touched against the pages it did not. Called with no `sha`, it lists the commits it can measure. It replaced `get_change_history`, which was removed on 2026-09-12 — that tool could only measure a change that arrived as a commit, and only in traffic.

## The project's brief: what it aims at, asks, and knows

What the docs are FOR, what nobody has answered yet, and what every agent otherwise works out again on every run. Free on every plan, and visible and editable by the owner on the admin panel's Overview, so nothing here is an agent's private notes about somebody else's product.

| Kind | What it holds | How a later run weighs it |
|---|---|---|
| `goal` | What these docs are for, in your words | The sentence a recommendation is argued against. Can be marked met |
| `question` | Something nobody here has answered yet | A thing to answer this run rather than guess. Can be answered |
| `fact` | True of the project and checkable | Will be re-checked; can go stale |
| `rule` | What to do or never do here | Outranks an agent's own reading of your site |
| `preference` | Taste — wording, tone, structure | Arguable; yields to a rule |

🔴 **A `goal` here is not an analytics goal.** `create_goal` records a thing a *reader* does that counts as a conversion, measured in visits and reported in Analytics ▸ Conversions. This one is the outcome your documentation exists for, and nothing counts it.

| Tool | Billing | Description |
|---|---|---|
| `list_memory` | Read | The whole brief, each line with its kind, who wrote it (`owner` or `agent`), what it rests on, and — for a goal or a question — whether it is still open. Comes with a one-line `gap` naming what is missing from the brief. Read it before deciding anything. |
| `add_memory` | Write | Record a goal, a question you would otherwise guess the answer to, or one claim the next session would re-derive. Not for findings that expire — a measurement records itself in the call history above. |
| `edit_memory` | Write | Correct a line **in place**, so the date the project first learnt it survives the correction — and **answer** a question or mark a goal met, with `resolution`. An empty `resolution` reopens one. |
| `remove_memory` | Write | Retire a line that stopped being true. Archived, never destroyed: a rule that simply vanished gets re-derived. Writing the same handle again brings the retired line back rather than starting a fresh one. |

⚡ An answered question keeps its answer beside it rather than disappearing — *"we already asked this, and here is the answer"* is what stops the next run asking again.

## Reminders: what the project promised to come back to

The brief above holds what stays true. This holds what is only true **later** — the reading that shows whether last week's rewrite worked and does not exist for another fortnight, a price that is right until Q4, a question you said you would answer. Free on every plan, and on the admin panel's Overview beside the brief.

The difference from the brief is *when it is read*, not what it holds: every memory line is read on every run, and a reminder is read **by its date**. It says nothing for the ninety days between being written and coming due.

| Kind | What it holds |
|---|---|
| `measure` | A change was made and its effect is not visible yet. Name the baseline in `because` — the change, and the `call_id` of the reading taken before it. |
| `recheck` | A fact with a known expiry: "beta until Q3", a price review, a version sunset. Written the day you learn the date, not the day it bites. |
| `followup` | A promise — a question somebody said they would answer, a decision deferred. What separates it from an open `question` is that somebody named a date. |

| Tool | Billing | Description |
|---|---|---|
| `list_reminders` | Read | What is **due now** by default — usually nothing, which is the cheap correct answer. Each row carries what to read (`check_with`), what it is judged against (`because`) and how late it is. `state: "all"` returns the whole schedule; `done` returns what past checks actually found. |
| `add_reminder` | Write | Promise to come back to something on a date. Say when with `in_days` rather than a date: the server does the arithmetic and answers with the absolute instant, so an agent that is unsure what today is cannot file a reminder into the past. |
| `edit_reminder` | Write | **Close** it with `outcome` — what the reading showed — or move its date rather than closing a check nobody ran. An empty `outcome` reopens one, because a reading taken against the wrong baseline has to be retractable. |
| `remove_reminder` | Write | Retire one that should never have been written, or whose subject is gone. Archived, never destroyed. |

🔴 **This is not a webhook.** Nothing fires and nobody is notified: a reminder is read when somebody asks what to do. For "tell us when something happens on the site", that is `register_webhook_*` below.

⚡ **"Nothing moved" is an outcome**, and the valuable one — it is what stops the same change being made again with the same confidence. Closing a reminder with what you found is how it gets finished; retiring one you actually checked destroys the finding, because a retired row and a completed one look identical to the next session.

## Audits: what there is to win, and how much of it is won

A goal says what counts as your documentation working. It does not say how much of it is on the table — so a change that works can still only be reported as a page that got better, never as a share of something. An audit is that missing number. Free on every plan, and its own **Audits** section in the panel.

One audit names one goal you declared, states in numbers what reaching it would take, and lists the searches, questions and jobs people actually have — one row each, with how many look for it, the reading that figure came from, what your docs have against it today and who ranks for it now. Claims are then drawn from that list rather than from whichever reading came up first, so a confirmed change reports the demand it took.

🔴 **An audit and the changes under it are judged separately, and they are allowed to disagree.** `edit_hypothesis` says whether one change did what it predicted; `edit_audit` says whether the goal moved. The sentence this exists to make sayable is the awkward one: every claim confirmed, and the target still short — which means the rows addressed a smaller share of the demand than anybody thought.

| Tool | Billing | Description |
|---|---|---|
| `list_audits` | Read | Every audit with its goal, its target and its rows, plus `progress`: how much demand is listed, how much of it anything is even pointed at, and how much has been won. Read it before writing a claim. |
| `add_audit` | Write | Open one. Needs `goal_key` — a goal you declared, checked against the ones that exist — and, for an assistant, `target` and `target_metric`. An audit with no target cannot come out short, and coming out short is the finding. |
| `add_audit_finding` | Write | Add one opportunity: `intent` in the words somebody types, `demand_value` with the `demand_source` it came from, `current` for what you have today, `competitor` for who holds it, and `action` from a closed list — create, rewrite, expand, structure, authority or none. |
| `edit_audit` | Write | Judge the audit with the target reading, move its review date, or correct it. `reached` means the goal moved, not that the changes under it were confirmed. |
| `edit_audit_finding` | Write | Correct a row, or drop one with the reason, so the next run reading the same demand does not re-propose it. |

🔴 **A demand figure is refused without a source you can open** — the `call_id` of the reading it came from, or a URL. A plausible number leaves no trace at all when it is invented, which a plausible link at least does.

🔴 **A search nobody could measure is left empty, never written as zero.** A zero reads as "nobody looks for this", travels into the decision to skip the row and is never revisited. `demand_note` is where "we tried and found no figure" goes, and `progress` reports how many rows are in that state beside every total, so a share computed over the rest is read as the upper bound it is.

⚡ **Nothing on a row says whether it was won.** That is the verdict on the claims pointing at it, and a second copy would disagree with the first inside a week. A rejection that named what to try next keeps the row in play rather than closing it as a loss.

## Hypotheses and the work board: whether the change worked

The brief holds what stays true and reminders hold what is true later. This holds the one thing neither did: **a claim that could turn out false**. Free on every plan, and on Overview as a Hypotheses tab beside the brief plus a four-column board.

It only works in one order — the claim first, the change second. `expected_effect` is written before the change and `result` after the reading, and once they are two columns of two different ages, a forecast can be told apart from a description written afterwards from the result. Nothing downstream can tell them apart otherwise, which is how a loop rots while every change still looks like it worked.

A claim also has to say what it is FOR and where it came FROM, so a change you make here can still be argued about in a fortnight. `kind` splits the two honest reasons to write one down: a **forecast**, written before the change to decide it, and a **reconstruction**, written about a change that already shipped so it stops reading as unmeasured. A forecast needs the whole chain — `goal_key` (a goal you declared, checked against the ones that exist), `because` (that goal is short, on this reading, and here is the cause), `source_url` with `source_claim` (a page outside your product and the one fact it reports) — and an assistant writing one without them is refused rather than warned. You writing one on your own panel is not: the refusal exists for what an unattended agent leaves behind, not for your own hunch.

| Tool | Billing | Description |
|---|---|---|
| `list_hypotheses` | Read | What this project believed and what it found out. `state: "due"` is the one to read first: a prediction, a change that shipped, and a date that has arrived with nobody having judged it. A `rejected` row is this project having already tried your idea and measured nothing. Read `kind` before citing a row as a prediction, and `counts.forecasts` to see how many of them were ever written in advance. |
| `add_hypothesis` | Write | Record the claim **before** making the change. A `forecast` takes the whole chain and is refused without it: `goal_key` the declared goal it argues for, `because` why that goal is short and what the cause is, `source_url` the page outside your product the idea came from — never this project's own pull request or commit, which is the change rather than its origin — `source_claim` the one fact that page reports, which is what `expected_effect` is sized from, and `baseline` the deciding reading as it stands right now — the figure, the tool, the call id and the date, taken **before** the change, because it is the one part of the claim that stops being obtainable once the change ships. Then `evidence` (the observation on this project), `expected_effect` (what that same reading should say afterwards, and by when) and `metric` (the reading that will decide it, the same tool and subject that produced the baseline). `baseline` and `expected_effect` are both refused without a number in them: "should help" agrees with any reading anybody later takes. Pass `kind: "reconstruction"` for a change that already shipped: it needs `because` and no source, because nobody read one. A row with no change attached stays `untested`. |
| `edit_hypothesis` | Write | Judge it — `result` is what was measured, with the denominator, and `verdict` is `confirmed` or `rejected`. Too early is not a verdict: move the date with `check_in_days` instead. An empty `verdict` retracts one. |
| `remove_hypothesis` | Write | Retire a claim that should never have been written, or whose subject is gone. Not how a tested one is finished — that is a verdict. |
| `link_work` | Read | Tie an issue, a pull request, a hypothesis, a memory line and a reminder together. Undirected and idempotent: linking A to B is the same fact as B to A, and writing it twice is one row. `write_docs` does the issue↔pull-request half for you when you pass `closes_issues`. |
| `unlink_work` | Read | Disconnect two things linked in error. A link to finished work is not stale — removing it makes a merged change unmeasurable again. |
| `get_work_board` | Egress | Every issue and pull request in the column its state earns: `planned`, `in_review`, `measuring`, `done`. Reads GitHub on request, so it is metered as egress rather than as a read. |
| `search_brief` | Read | One query over everything written down — memory, hypotheses and reminders, closed ones included. The pair of `search_prior_work`, which searches the repository instead. |

🔴 **"Nothing distinguishable" is `rejected`, not a missing verdict.** The claim predicted an effect and none appeared, and that is the most valuable row the store produces, because it is what stops the same change being made again with the same confidence.

🔴 **A merged change with nothing linked to it shows on the board as `unmeasured`** — the honest word for work nobody can say anything about afterwards. It looks like progress and is not, which is why the board names it rather than filing it under Done. Paying that debt (a claim written late, linked, with a reading dated) outranks starting anything new.

🔴 **A merged change with a claim and no reminder carries `needs_reminder`.** It is the quieter half of the same failure: the column says Measuring, the claim says it is being tested, and nobody is dated to come back and take the reading, so the check simply never happens. One `add_reminder` and one `link_work` pays it.

⚡ **A question can hold a merge.** Write it with `add_memory` as a `question` with `waiting_on: "owner_blocking"` and link it to the work, and a pull request that depends on it is opened and **not merged** until you answer — on a project set to merge automatically as well. The card shows as `blocked`, and the agent that wrote the change may not answer the question to unblock itself. Use it when a wrong answer would make the change wrong (which of two pages is real, whether a version is still supported); `waiting_on: "owner"` is the ordinary case, where the question is worth asking and the work goes ahead.

⚡ **`review_mode` says what happens to the next change you write**: `auto` merges it in the same call, `manual` opens the pull request and stops. Either way a pull request is opened; the mode decides only whether it lands. The owner sets it on the board.

## Webhooks

Registering a webhook costs nothing to keep; only the outbound deliveries and replays are metered, as egress.

| Tool | Billing | Description |
|---|---|---|
| `register_webhook_<event>` | Write | Register a webhook for one of the 18 typed events (HMAC secret + URL) |
| `list_webhooks` | Read | List registered webhooks for the workspace |
| `unregister_webhook` | Write | Remove a webhook subscription |
| `list_webhook_deliveries` | Analytics | Delivery history with status, retry count, payload |
| `replay_webhook_delivery` | Egress | Re-deliver a specific past delivery |
| `test_webhook` | Egress | Send a synthetic payload to a URL |

There are 18 typed events, among them `content.indexed`, `translation.completed`, `chat.no_answer`, `chat.negative_feedback` and `usage.limit_approaching` — see [Webhooks](./webhooks.md) for the full list and payload schemas.

## Skills discovery

| Tool | Billing | Description |
|---|---|---|
| `find_skill` | Included | Search the `docs-skills` catalog by `query` with optional `category` and `requires_plan` filters. Returns `raw_url` for the agent to fetch the SKILL.md directly. |

## Collectors — the evidence, without the reading of it

Five tools sit in a cheaper billing class of their own, **Probe**: `collect_page_text`, `collect_corpus_map`, `collect_assistant_questions`, `collect_traffic` and `collect_onsite_search`. They hand back normalised rows plus a `reproduce` block naming the exact calls behind every row — no model in the path, so there is nothing in them to disbelieve. Buy one when you want the numbers themselves rather than a reading of them.

`collect_ai_citability` sits beside them: it scores whether answer engines can fetch and quote your pages at all. Its evidence layer is code rather than a model — it crawls and does arithmetic — which is also why it bills as Probe rather than Agent. It was named `audit_geo` until 2026-09-12; the rename marks that it never ran a model, unlike the tools retired that day below.

## What used to run a model on Docsbook's own side

Until 2026-09-12, three kinds of tool ran work here instead of just answering a call, and all three are gone along with the engine behind them:

- **135 action tools** (`observe_link_graph`, `decide_next_market`, `draft_comparison_page`, one per verb × subject) each ran a model on our servers and answered with a validated payload. Nothing you could do with them became impossible — each ran on ordinary reads you can make yourself (`get_search_rankings`, `search_docs`, `read_doc`, thirty in all) — and what made them worth anything was never the running. It was knowing **which** reads, **in what order**, and **the trap in reading them**, which `docsbook_expert` now hands you directly, for free, in one call: ask it what you are trying to achieve and a step comes back naming the reads, the order, and the shape a good answer has. What you lose: those tools validated themselves — every digit in a claim had to appear in the evidence cited, so an invented figure failed instead of shipping. Nothing validates your own run; `docsbook_expert` gives you the shape of a good answer so you can tell whether one was followed.
- **Four background runners** (`run_docs_analyze`, `run_docs_create`, `run_docs_manage`, `run_docs_automate`) ran a skill on Docsbook's side against your workspace and handed back a `run_id` to poll with `get_agent_run`, `list_agent_runs` and `cancel_agent_run` — all seven gone. Every tool on this server now answers inside the call that asked for it: there is no job to start and no run to poll, which also removes the commonest way to misreport one (treating `{ run_id, state: "queued" }` as the answer).
- **Two standing-agent tools** (`find_agent`, `enable_agent`) armed a route that ran on its own, on a schedule, an event or a repository's commits — also gone, with the engine behind them. Nothing on this server starts work by itself. What that engine was for is served by what remains: `register_webhook_*` for "tell me when something happens" (your side decides what to do about it), your own agent holding your repository for "do the work once", and `docsbook_expert` for "what should I do about this" — which was the only part of a standing agent worth keeping, since it knew which tools, in what order, and how the answer goes wrong.

## Troubleshooting / FAQ

**Is the agents/MCP tooling still working?** Yes. On 2026-09-12 the standing-agent engine was retired — the 41 `agent_*` tools, the 135 action tools and the 4 `run_docs_*` runners are gone — and one agent remains: `docsbook_expert`, which advises rather than runs. Every other tool on this page still works exactly as documented.

**My client still shows the tool named `docsbook` instead of `docsbook_expert` — is that a problem?** No. An MCP client reads the tool list once, at connection time, and holds those names for the rest of that session. The server resolves the old name to the new one rather than refusing it. Reconnect your client to see `docsbook_expert`.

**A call was refused for an empty balance — what do I do?** The refusal names the project that ran out, what the call draws, what is left, and where to top up. Discovery calls (`get_info`, `list_workspaces`, `find_skill`, and the rest of the Included class above) keep working regardless, so your agent can still find out what happened and report it.

**Why does the tool count keep changing?** It reflects what actually runs. The server exposed more tools before 2026-09-12, when the 135 narrow action tools and the standing-agent tools were retired in favor of `docsbook_expert`; it currently exposes 156. `get_info` always reports the live count.

## Related

- [MCP server overview](../agent-ready/mcp.md) — connecting a client, the OAuth flow, and what the tools are for
- [Webhooks reference](./webhooks.md) — the 18 typed events and their payload schemas
- [API reference](./api.md) — the REST endpoint for asking your documentation a question
- [Chat hooks](../ai-chat/chat-hooks.md) — what `set_chat_hooks` configures
- [Analytics & insights](../analytics/README.md) — the reports the analytics tools read
