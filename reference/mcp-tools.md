---
title: "Every tool the Docsbook MCP server exposes to an agent"
description: "The 136 tools a Docsbook workspace exposes over MCP — the one `docsbook` expert agent, workspace setup, content, issues, chat, translations, analytics, webhooks, standing automations and background agent runs."
---

# MCP Tools Reference

This page lists every tool exposed by the Docsbook MCP server at `https://docsbook.io/api/mcp/server`. The server exposes **136 tools**. Each requires Bearer authentication via OAuth 2.0 + PKCE.

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

`docsbook` is the one agent on this server, and the first call to make for any documentation request — however narrow, in any language. It is an **expert, not a runner**: it answers in one round trip with how to do the work, and does none of it.

| Tool | Billing | Description |
|---|---|---|
| `docsbook` | Read | Any documentation request in the user's own words. Returns how to think about it, the steps in order with the tool on each and who runs it, what to carry between steps, what to write, what makes the answer wrong, and what to remember. Runs nothing. `workspace_id` optional |

Every step in the answer says where its work lands:

- **`you`** — your own checkout, with your editor, shell and tests. The step names the tools (`git log --since`, `Read`, `Edit`), because "use your own tools" is not advice and naming them is.
- **`docsbook`** — one call to this server, which **you** make. Nothing runs on its own, so the call is gated, charged and logged exactly like any other.
- **`subagent`** — work worth handing to a subagent of your own: a step that fans out over forty pages, or that wants a fresh context.

Steps also carry `transform` — what to keep from one step's output and hand to the next — which is the half a tool list never has and a long route needs most.

`docsbook` never guesses. A request it cannot place on a known workflow gets the general method (the writing rulebook, what is actually published, the constraints) and says out loud that it is the general method. It has no `findings` field, deliberately: nothing ran, so there is nothing measured, and the numbers arrive when you make the calls it names.

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

## The 135 action tools were removed

Until 2026-09-12 this section listed 135 read-only tools — `observe_link_graph`, `decide_next_market`, `draft_comparison_page`, one per (verb × subject) — each running a model on our servers and answering with a validated payload. They are gone, and the reason is the same one that took the forty-one standing agents the same morning: **one of the 136 had ever been called.**

Nothing you could do became impossible. Each of them ran on ordinary reads you can make yourself — `get_search_rankings`, `search_docs`, `read_doc`, thirty in all — and what made them worth anything was never the running. It was knowing **which** reads, **in what order**, and **the trap in reading them**.

That is what `docsbook` now hands you, for free, in one call. Ask it what you are trying to achieve and a step comes back as:

> **Read what people actually type before they arrive** — `get_search_rankings`, `get_popular_searches`, `get_failed_searches`, `get_search_zero_click`
>
> - Read the demand from both sides: what search shows you for, and what readers type once they are here.
> - Classify each query by intent from its **wording**, not from the page it landed on — the landing page is what you are testing later, and using it here makes the analysis circular.
> - Answer with `queries`: one row per query, at most 30, each carrying `query`, `intent`, `volume`, `current_page`. `intent` is one of how_to / definition / comparison / error / price / reference / unclear.
>
> *Then carry forward only the queries with impressions and a position between 5 and 20 — those are the ones a rewrite can move.*

Your own agent then makes those calls, on your own token, at read prices. The method is the same method the removed tool followed; you are no longer paying for a second model to apply it.

**What you lose, stated plainly.** Those tools validated themselves: every digit in a claim had to appear in the evidence it cited, so an invented figure failed instead of shipping, and the scores were arithmetic rather than a model's opinion. Nothing validates your own run. What `docsbook` gives you instead is the shape a good answer has — the columns, the allowed values, the cap — so you can tell whether one was followed.

## Collectors — the evidence, without the reading of it

Five tools sit under the family in a cheaper billing class of their own, **Probe**: `collect_page_text`, `collect_corpus_map`, `collect_assistant_questions`, `collect_traffic` and `collect_onsite_search`. They hand back normalised rows plus a `reproduce` block naming the exact calls behind every row — no model in the path, so there is nothing in them to disbelieve. Buy one when you want the numbers themselves rather than a reading of them. `audit_geo` sits beside them and is the one survivor of the action family: its evidence layer is code rather than a model, and it scores whether answer engines can fetch and quote your pages at all.

## Background agent runs

`find_skill` hands the SKILL.md to *your* agent to execute. These tools do the opposite: they run the skill on Docsbook's side, against your workspace, with the full administrative toolset the skill was written for — so an assistant with no other Docsbook tools connected can still get the job done.

Each `run_docs_*` call returns `{ run_id, state }` immediately. **It does not return the result** — the work takes minutes, and a caller that reports the start as the answer is reporting work that has not happened. Poll `get_agent_run` with the returned `run_id`.

| Tool | Billing | Description |
|---|---|---|
| `run_docs_analyze` | Agent | Run the `docs-analyze` skill: audit the site from real numbers and report what is wrong and what it costs. Declared audit-mode — writes are refused for the whole run, so it works with a read-only token. |
| `run_docs_create` | Agent | Run the `docs-create` skill: build documentation from your site, a repository, another docs platform, or nothing but a product name. Commits pages — needs a **read-write** token. |
| `run_docs_manage` | Agent | Run the `docs-manage` skill: rewrite pages and configure the site against the writing and site-running rulebook. Needs a **read-write** token. |
| `run_docs_automate` | Agent | Run the `docs-automate` skill: set up drift guards, event subscriptions, checks on incoming changes, alerts and standing monitors. Needs a **read-write** token. |
| `get_agent_run` | Read | State of one run (`queued`, `running`, `succeeded`, `failed`, `canceled`, `expired`), live progress while it runs, and once it succeeds the full outcome: the report, every action it took, and what changed on the site. |
| `list_agent_runs` | Read | Your recent runs, newest first. Use it to check whether the job is already running before starting a second one. |
| `cancel_agent_run` | Read | Stop a run that has not finished. It does **not** undo what the run already did — pages it already committed stay committed. |

A run belongs to the account that started it: another account's `run_id` reads exactly like an unknown one. A queued run that has not started within a few hours expires rather than running late, because an audit answers a question about the site as it was when it was asked. And a run is attempted once, never retried — a failed run may already have committed pages, and a second attempt would commit them twice.

## Standing agents were removed

Until 2026-09-12 two tools here — `find_agent` and `enable_agent` — armed a route that ran on its own, on a schedule, an event or a repository's commits. They are gone with the engine behind them. Nothing on this server starts work by itself any more.

What that engine was actually used for is served by tools that remain:

- **"Tell me when something happens"** — `register_webhook_*` (the 18 typed events), which posts to your own endpoint. Your side decides what to do about it.
- **"Do the work once"** — the `run_docs_*` runs above, which you start.
- **"What should I do about this?"** — `docsbook`, which answers with the method, the steps and the tools, and leaves the running to you. That was the only part of a standing agent worth keeping: it knew which tools, in what order, and how the answer goes wrong.

## Related

- [MCP server overview](../agent-ready/mcp.md) — connecting a client, the OAuth flow, and what the tools are for
- [Webhooks reference](./webhooks.md) — the 18 typed events and their payload schemas
- [API reference](./api.md) — the REST endpoint for asking your documentation a question
- [Chat hooks](../ai-chat/chat-hooks.md) — what `set_chat_hooks` configures
- [Analytics & insights](../analytics/README.md) — the reports the analytics tools read
