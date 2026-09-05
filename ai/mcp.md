---
title: "MCP server: run your documentation from a coding agent"
description: "Connect Claude Code, Cursor, Codex or any MCP client to Docsbook and read, write, measure and configure your documentation from inside the editor."
---

# MCP Server

The Docsbook MCP server is a remote Model Context Protocol server that exposes your documentation and its whole admin surface to an AI agent. Connect Claude Code or any MCP-compatible client to one endpoint and read your pages, commit changes, read analytics, and change settings without leaving the editor.

This page is the reference for what the server serves and what a call draws on. Every tool listed here is callable by any connected client; what a metered call costs is on the [Docsbook pricing page](https://docsbook.io/pricing) and on each tool's own row in your admin panel.

## What is the Docsbook MCP server?

The Docsbook MCP server exposes **309 tools** over the Model Context Protocol, an open standard for handing tools, resources and prompts to AI agents over a typed RPC interface. Of those tools, 18 are one-per-webhook-event registrations, 136 are action tools that each perform one step of documentation work on one subject and answer with a validated JSON payload, five are collectors that hand back the evidence those actions are built on with no judgement in it, four start and read background runs, two connect and configure a repository or website as a source of truth, two find and arm a standing agent on a schedule, event or connected repository's commits, and the rest are named tools covering workspace, content, chat, analytics and webhook operations.

## Endpoint

The Docsbook MCP server is served at one URL for every workspace and every client:

```text
https://docsbook.io/api/mcp/server
```

Authentication is OAuth 2.0 Authorization Code with PKCE. Bearer tokens are returned to the client and refreshed transparently. There is no per-project MCP URL to look up: the OAuth flow is scoped to the signed-in account, and the client picks the workspace afterwards.

## How do I connect my AI client to Docsbook?

Point your client at `https://docsbook.io/api/mcp/server` and complete the OAuth prompt in the browser. The Docsbook MCP server is a remote HTTP server with OAuth, so every modern MCP client connects to it with the same endpoint and no local process to run. The subsections below give the exact command or config file for each client.

You can also browse the catalog inside your own project: open the admin panel and pick `MCP` in the sidebar. The first time you open it the section offers a **Turn on** panel carrying the install command for your client, so you can connect before you read the catalog, and pressing it runs a short guide over the table itself. Behind it is a table of every tool the server serves right now, read live from the server rather than from a written-down copy, with each tool's billing class, price per call, how long a call typically stays open, and whether readers can call it without a token. Search it, narrow it with **Filters** — the billing classes, each printed with its own price — or sort by any column. Hovering a row opens a card with the rest of what there is to know about that tool: what it does, what a call costs and how long it typically stays open, how many arguments it takes and how many of them are required, how many worked examples call it, and — in your own project — what it has cost you so far and when you last called it, with the callable id in it ready to copy. Clicking a row opens that tool's own page, and the page has an address: the URL carries the tool, so you can refresh it, bookmark it, or send it to a colleague and land them on the same tool instead of back at a table of ninety rows. Everything on it is about that one tool. Its arguments are a form with a **Run** button that makes a real call against this project, and the button carries the price before the money moves. Under that is its **call history**, drawn by the same **Feeds** table you read everywhere else, narrowed to this one tool: one line per call, and expanding a row shows the call in full — what went in, what came back, who asked (your Run, an outside agent, a schedule, an event), how long it took, what it was priced at, and what actually left your balance. Below that is what runs it unattended: a schedule, an event, or one of your saved **Feeds**, so a call can watch a whole feed rather than a single event name, and each armed row shows what it already fires on so you never replace a run you set up earlier without seeing it. Last on the page are the **agents that use this tool** — the cards from the **Agents** section whose route actually calls it, armed ones first, each with its own switch, so you can put the tool on a schedule from the page where you just read what a call costs. Under them sits one worked example to copy into your own client; what runs from inside Docsbook is the call.

### Claude Code

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

The first call opens a browser tab for OAuth. After consent, the tools become available inside Claude Code.

### Cursor

Cursor has no `mcp add` command, but it accepts a one-click install link:

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=docsbook&config=eyJ1cmwiOiJodHRwczovL2RvY3Nib29rLmlvL2FwaS9tY3Avc2VydmVyIiwidHlwZSI6Imh0dHAifQ==
```

Or add the server to `~/.cursor/mcp.json` (or use **Settings → MCP & Integrations → New MCP server**):

```json
{
  "mcpServers": {
    "docsbook": {
      "url": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

Reload Cursor — OAuth opens in the browser on first use.

### Codex CLI

```bash
codex mcp add docsbook --url https://docsbook.io/api/mcp/server
```

Or edit the config directly — Codex stores MCP servers in `~/.codex/config.toml`:

```toml
[mcp_servers.docsbook]
url = "https://docsbook.io/api/mcp/server"
```

### Windsurf

Edit `~/.codeium/windsurf/mcp_config.json` and refresh the Cascade panel:

```json
{
  "mcpServers": {
    "docsbook": {
      "serverUrl": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

### Cline

Open **Cline → MCP Servers → Configure MCP Servers** and paste:

```json
{
  "mcpServers": {
    "docsbook": {
      "url": "https://docsbook.io/api/mcp/server",
      "transportType": "http"
    }
  }
}
```

### Gemini CLI

```bash
gemini mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

The default scope is the current project — add `--scope user` to install it globally. Or add it by hand to `~/.gemini/settings.json` (note the key is `httpUrl`; `url` there means SSE):

```json
{
  "mcpServers": {
    "docsbook": {
      "httpUrl": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

### GitHub Copilot (VS Code)

```bash
code --add-mcp '{"name":"docsbook","type":"http","url":"https://docsbook.io/api/mcp/server"}'
```

Or create `.vscode/mcp.json` inside your workspace, then enable the server from the Copilot Chat MCP picker (note the key is `servers`, not `mcpServers`):

```json
{
  "servers": {
    "docsbook": {
      "type": "http",
      "url": "https://docsbook.io/api/mcp/server"
    }
  }
}
```

### ChatGPT

ChatGPT supports remote MCP through **Connectors**, on ChatGPT's own paid plans. That requirement is OpenAI's, not Docsbook's.

1. Open **ChatGPT → Settings → Connectors → Advanced → Developer mode**.
2. Click **Create** and paste the URL: `https://docsbook.io/api/mcp/server`.
3. Authorize in the browser when prompted.

## What are the Docsbook MCP tools for?

The Docsbook MCP tools exist to make one of four things happen: more qualified readers arrive, more of them leave with what they came for, more buying-intent readers are carried forward by the assistant, and fewer questions reach a person. Everything below is grouped by which of those four it serves.

Your documentation is not a cost centre. It is a channel with three jobs: **get found** (by Google, and by the AI assistants your buyers now ask instead of Google), **convert the reader** (a visit that ends with nothing is a lost customer who never complained), and **prove what worked** (so the next edit is a decision, not a guess).

There are only four ways a docs tool makes money, and every tool below serves one of them:

| Lever | Mechanism | Core tools |
|---|---|---|
| **Acquisition** | More qualified readers arrive, from search and from AI answers | `update_seo`, `update_geo`, `update_aeo`, `get_search_rankings` |
| **Conversion** | More arriving readers leave with what they came for | `get_visit_outcomes`, `get_dead_end_pages`, `get_content_health`, `get_route_patterns` |
| **Sales** | The assistant carries buying-intent readers forward instead of just answering | `get_chat_intent`, `get_chat_conversations`, `set_chat_system_prompt`, `set_chat_hooks` |
| **Cost avoided** | Questions answered by the docs are questions not answered by a person | `get_ai_unanswered`, `get_failed_searches`, `get_search_zero_click`, `get_insights` |

A tool that serves none of these returns **context**, not a decision. `Pageviews: 12,340` is context. `31% of your readers left with nothing` is a decision.

### Getting found

| Tool | What it is worth |
|---|---|
| `update_seo` | Meta tags, sitemap, OpenGraph. Table stakes: without it, pages that deserve to rank cannot. |
| `update_geo` | Generative Engine Optimization — structures the page so an LLM can quote it *and attribute it to you*. The difference between being the source of an AI answer and being invisible inside one. |
| `update_aeo` | Answer Engine Optimization — shapes content into the direct-answer form AI assistants lift verbatim. |
| `get_search_rankings` | Real Google Search Console positions, plus the **"worth improving" set at position 5–20** — pages Google already shows that are not yet winning the click. Turns "we should do SEO" into a named page and a named query. Lags Google by ~2 days. |
| `get_analytics` (AI-bot breakdown) | Whether ChatGPT, Perplexity and Claude crawlers read you at all. A zero here means the GEO work is not landing — no crawl, no citation, no referral. |

Buyers increasingly ask an assistant before they ask a vendor. If the assistant answers from a competitor's docs, you never enter the shortlist and the loss appears in no dashboard.

### Not losing the reader

`get_visit_outcomes` is the headline number of the whole product: it classifies every visit as success / dead end / bounce / partial and reports the **dead-end rate** and **self-serve resolution rate**. A dead end is a reader who searched, asked the AI, or opened several pages — and still left with nothing. Everything below answers "…and where exactly?"

| Tool | What it is worth |
|---|---|
| `get_dead_end_pages` | The rewrite queue, ranked. Rows marked `terminal_success` are pages people leave from *because they got what they needed* — the tool protects your best pages from being "fixed". |
| `get_content_health` | One 0–100 score per page, combining dead-end exits with negative feedback. Replaces cross-referencing four reports by hand on a large doc set. |
| `get_rage_signals` | Pages re-entered 3+ times in one visit, A→B→A bounce-backs, repeated searches. Dead-end rate says a visit failed; this says *where*. Re-entry means the answer should be on that page and is not — the fix is restructuring, not new content. |
| `get_route_patterns` | The 2–4 page sequences readers actually walk, and how often each ends well. A frequent route that ends badly is a **navigation defect, not a page-quality problem** — rewriting those pages will not fix it. |
| `get_reverse_funnel` | Works backwards from successful visits: which entry pages lead to a good ending. Needs no hypothesis, so it surfaces the path readers found that you never designed. |
| `get_forward_funnel` | Completion of the route *you* declared, and which transition leaks. Your onboarding-completion rate. |
| `get_metric_timeseries` | Any headline metric by day — the only tool that answers "is this getting worse" and lines a change up against a release date. |
| `get_visits` | The evidence behind the rates: one reconstructed visit at a time. Use when a number is disputed, or to attach a real reader to a complaint. |
| `get_retention` | W1/W4 return rate by cohort. Direction depends on the section: high return is healthy for reference docs and a **failure** for onboarding. |

### Demand you are not serving

Every row here is a support ticket you can pre-empt by writing one page.

| Tool | What it is worth |
|---|---|
| `get_ai_unanswered` | Questions the assistant could not answer, in the reader's own words. The cheapest content plan there is. |
| `get_failed_searches` | Searches returning zero results — the same gap through a different door. |
| `get_search_zero_click` | Searches that returned results and got **no click**. The gap zero-result reports miss: search worked and the reader rejected every result, which points at **titles and summaries** — an order of magnitude cheaper to fix than page bodies. |
| `get_popular_searches` | What people look for most. Read against `get_content_health` on the same page: high demand + low health = your most expensive broken page. |
| `get_negative_feedback` | Pages with thumbs-down, ranked. The reader's explicit vote, no inference needed. |
| `get_insights` | The pre-combined digest — doc gaps, zero-result searches and disliked pages with impact estimates, in one call. Start here for "what should I fix this week". |

### Selling through the assistant

The chat is not a support widget. It is the only place where a prospect states their objection in plain language.

| Tool | What it is worth |
|---|---|
| `get_chat_intent` | Conversations split by **buying stage** — evaluation, pricing, integration, support, bug. Answers who is deciding whether to buy and what blocks the purchase. **Names the competitor** when readers mention one: competitive intelligence no page-level report can produce. |
| `get_chat_conversations` | Questions grouped by topic, with `click_through` — the share of conversations where the reader opened a cited page. A topic with buying intent and **no clicks is a sales leak**: the answer was correct and carried nobody forward. The unit is a conversation, not a question, because four questions from one stuck reader and one each from four readers give identical counts and opposite conclusions. |
| `set_chat_system_prompt` | Where the fix lands — turns the assistant from a librarian into a salesperson: qualify, handle the objection, route to a demo. |
| `set_chat_hooks` / `test_chat_hook` | Pre/post-LLM hooks: inject live context (pricing, availability, the reader's plan) or capture a lead the moment intent appears. |
| `get_ai_questions` | Verbatim question log — raw material for FAQ, onboarding email, objection handling. |

A pricing objection stated in your docs chat is worth more than a page view: the reader qualified themselves and told you exactly what stops them buying.

### Acting on the finding

Diagnosis without a fix is a report. These close the loop inside one connection.

| Tool | What it is worth |
|---|---|
| `search_docs` | Verbatim, citable sections — text, regex, heading or path modes. What an agent reads *before* editing so it changes the right lines. |
| `search` | Semantic (embeddings-based) search — finds a page by what it *means*, not what it literally says, using a pre-built vector index. Catches the natural-language question that phrases nothing like the page title. On every plan, and it always answers: a project with no index yet gets the same question answered by full text instead, and the reply says which engine ran (`mode`: `semantic` or `lexical`). Served without a token on your project's public endpoint, so a reader's agent can search your docs too. |
| `get_doc_outline` | Every page with title, heading count, size. Cheap orientation before a search or a write. |
| `write_docs` | Commits one or many markdown files in **one atomic git commit**. Turns analysis into a shipped change. |
| `fetch_url` | Reads one public web page as clean Markdown. The tool that lets an agent check a page against the world outside your workspace — a competitor's pricing, your own marketing site, or whether a link a doc depends on is still alive. |
| `get_change_history` | **Call before editing.** What was changed before and how the affected pages' traffic moved after — with raw before/after visit counts, `low_sample` and `pending` flags, and **no verdict on purpose** (a commit and a traffic move in the same week are not cause and effect). Without it, the same recommendation gets made forever with the same confidence. |
| `get_page_diff_impact` | **Call after shipping.** Did that edit actually help? Compares the pages a commit touched against the pages it did not, before and after — outcome mix, self-serve resolution, time to first value. The untouched pages are the control, and they are the point: docs traffic moves for reasons unrelated to your edit, so an improvement only counts if it beat the site trend. A change that merely matched it is reported as no effect, not as a win. Also breaks the visits down by country, reader language and device, each next to the same slice's move on the untouched pages — which is what turns "traffic went up" into a decision. Where you have set an average price and a call-to-action URL, it also prices the edit — conversions and revenue on the touched pages, before and after. |
| `update_navigation` | The fix for a defect `get_route_patterns` or `get_reverse_funnel` found — often cheaper and more effective than rewriting a page. |
| `find_skill` / `find_widget` | Discover a packaged capability — a workflow skill, an interactive widget — instead of writing one. |
| `list_issues` / `get_issue` / `create_issue` | The project's own GitHub issue tracker. Not every finding is a change you make in the same breath — `create_issue` is how one that is not gets written down instead of ending with the conversation. `list_issues` first, so a finding does not duplicate an issue already open. Filing needs a read-write token; reading does not. |

### Knowing without looking

A dashboard only works if someone opens it. A webhook works always. Registering a webhook costs one write call; each delivery it later makes is an outbound call from the Docsbook network.

| Event tool | What it is worth |
|---|---|
| `register_webhook_chat_no_answer` | The assistant just failed a reader — in Slack, in seconds, while they may still be on the page. |
| `register_webhook_search_no_results` | The same, for search. |
| `register_webhook_traffic_spike` / `_drop` | A spike is either a marketing win worth chasing or an incident driving people to troubleshooting. A drop after a release is a regression you would otherwise find next quarter. |
| `register_webhook_content_outdated` | Docs drifting from the product — the root cause of most bad AI answers. |
| `register_webhook_chat_negative_feedback`, `_feedback_received` | The reader's explicit complaint, routed to whoever owns that section. |
| `register_webhook_usage_limit_approaching`, `_overage_limit_reached` | Budget control — no surprise invoices. |
| `list_webhooks`, `unregister_webhook`, `list_webhook_deliveries`, `replay_webhook_delivery`, `test_webhook` | Operate the above: audit, retry, verify. |

### Reach and ownership

| Tool | What it is worth |
|---|---|
| `update_languages` | Enable a target language. Read alongside the country/language breakdown in `get_analytics`: **translate where the readers already are**, not where you hope they will be. |
| `set_translation_mode`, `upload_translation`, `approve_translation`, `list_pending_translations`, `get_translation`, `delete_translation` | The translation pipeline — automatic, or externally supplied with human approval. |
| `update_access` | Private workspace, password, or your own SSO/OIDC. Unblocks selling to companies whose procurement requires it. |
| `update_domain` | Docs on your own domain — the SEO authority accrues to **you**, not to a vendor subdomain. |
| `update_branding`, `update_ui_settings` | Your product, not a platform's. |

## The combinations that pay

No single tool above is the product. These loops are.

### Loop 1 — "Which page is costing me customers?"

```text
get_visit_outcomes      → the rate: 31% of visits end with nothing
get_dead_end_pages      → which pages those visits died on
get_rage_signals        → what the reader was trying to do there
get_change_history      → has this page been "fixed" before, and did it work?
search_docs → write_docs → ship the fix
get_page_diff_impact    → did the edited pages beat the pages you did not touch?
```

The rate alone is unactionable, the page list alone lacks a cause, and a fix without `get_change_history` repeats a failed edit with full confidence. The last step is what closes the loop: a site-wide trend line moves for a dozen reasons, so "the rate improved after my commit" is only evidence when the pages you edited improved *more than the ones you left alone*. Only the sequence produces a change you can defend.

### Loop 2 — "Is my navigation lying to readers?"

```text
get_route_patterns   → a frequent 3-page route that keeps ending badly
get_reverse_funnel   → the route successful readers actually take
update_navigation    → promote the working entry point
get_forward_funnel   → confirm completion on the declared route improved
```

A route that fails while its individual pages score well is a navigation defect — `get_content_health` would keep pointing at healthy pages forever.

### Loop 3 — "Where are the deals leaking?"

```text
get_chat_intent          → 40 pricing-stage conversations, a competitor named in 12
get_chat_conversations   → those topics have near-zero click_through
set_chat_system_prompt   → handle that objection, route to a demo
write_docs               → a comparison page that answers it once and for all
get_chat_intent (later)  → did the objection stop recurring?
```

The only loop in any docs product that starts at a stated objection and ends at a shipped answer. `click_through` is what separates "the assistant answered" from "the assistant sold".

### Loop 4 — "Am I visible to AI, and did it bring anyone?"

```text
update_geo + update_aeo   → structure content for citation
get_analytics (ai_bots)   → confirm crawlers are actually reading it
get_search_rankings       → track classic-search position alongside
get_analytics (referrers) → referrals arriving from AI assistants
get_visit_outcomes        → and whether those arrivals end in success
```

The last step is the one everybody skips. Traffic from an AI answer that dead-ends is worse than no traffic — you earned the visibility and burned the impression.

### The self-healing loop

Run Loop 1 on a schedule from CI:

```text
weekly:  get_content_health  → take the worst 3
         get_change_history  → skip anything already tried and failed
         search_docs → write_docs → open a PR
         get_page_diff_impact → report on the PR whether the edited pages
                                beat the untouched ones, or say they did not
```

Documentation that repairs itself and shows its work — "saw the problem" and "fixed the problem" without leaving the connection.

## Handing over the whole job

Every tool above answers inside the call that asked for it. Four do not, and that is the point of them.

Auditing a site, building one, restructuring it, or standing up the monitors that keep it honest is minutes of work — reading pages, reasoning over numbers, committing files. `find_skill` handles that by handing the SKILL.md to *your* agent, which only works if your agent is also connected here, has picked a workspace, and will spend twenty tool calls on it. These four run the skill on our side instead, against your workspace, with the full administrative toolset the skill was written for.

| Tool | What it is worth |
|---|---|
| `run_docs_analyze` | The full `docs-analyze` audit, run for you: what is wrong, judged from search positions, reader behaviour and your own goals — plus the gap no number shows, the audiences and use cases the docs never address. It is declared audit-mode, so it cannot change anything and works with a read-only token. |
| `run_docs_create` | The full `docs-create` pipeline: audit the product, decide the structure, write the pages, publish. From your site, a repository, another platform you are leaving, or a product name alone. |
| `run_docs_manage` | The `docs-manage` rulebook applied rather than quoted: pages rewritten, the site configured, goals and funnels declared. Use it when the request is a judgement ("make this good") rather than a value ("set the accent to #0f0"). |
| `run_docs_automate` | `docs-automate`, so the checks keep happening: drift guards, webhooks, CI checks, alerts and standing monitors. |

**Starting a job and reading its outcome are two separate calls.** A `run_docs_*` call returns `{ run_id, state: "queued" }` — never findings, never pages. `get_agent_run` returns the state, live progress while it runs, and once it has succeeded the report, every action the run took, and what changed. `list_agent_runs` finds a run id you lost; `cancel_agent_run` stops one that has not finished, without undoing what it already committed.

The three that write require a **read-write** token. `run_docs_analyze` does not, because it cannot write.

## Buying the evidence without the opinion

An audit does seven things in one call: gathers, normalises, interprets, judges, scores, ranks, recommends. Run the first two twice and you get the same answer, and anybody can redo them by hand and check. From `judge` onward the answer is the model's. Both halves used to be charged as one agent run, which meant the half you can verify was sold at the price of the half you have to trust.

Five **collectors** are the first half on its own, charged as a `probe` rather than as an agent run:

| Tool | What it hands back |
|---|---|
| `collect_page_text` | Your live pages as the wire actually serves them — status, title, meta description, headings, code blocks, and how many words of prose survive with no JavaScript engine — beside the size of the source we store for the same path. The gap between those two is the row: 8 000 characters in the repository arriving as 40 words is a page that is perfect to every check reading the source and unquotable to every assistant reading the page. |
| `collect_corpus_map` | Every page with its size, heading count and depth, the sections, the stubs, and how much of it navigation reaches. |
| `collect_assistant_questions` | What readers asked your docs assistant, verbatim, which of it went unanswered, the answer rate with its denominator, and the languages it arrived in. |
| `collect_traffic` | Who arrived, how the visits ended, which pages they ended on, and the 2–4 page sequences readers walk — four tables, kept apart. |
| `collect_onsite_search` | What readers typed into your own search box, what returned nothing, and what returned results and got no click — three tables, kept apart, because the first is a missing page and the second is a losing title. |

There is no model in the path, so there is nothing in them to disbelieve — and the payload proves it rather than claiming it. Every answer carries a **`reproduce`** block: the exact MCP calls and the arguments they were made with, per row. Run them yourself and you get the same record back, apart from the timestamp. Nothing an audit returns can offer that, because an audit's answer passed through a model.

What you do not get is a judgement. No findings, no scores, no ranking, no recommendation — those are what an action tool's price buys, and a collector that quietly included one would be an agent run at a fraction of the price.

**When the cheap one is the right one.** With no Search Console connected, `measure_intent_match` scores its ranking axes as unmeasured and still charges for the run; `collect_corpus_map` needs no search data, no traffic and no history at all, and hands back real rows on a site that went up this morning. The same applies when you want the numbers an action was built on before you decide whether to buy the reading of them.

**What is missing is said out loud.** A source that could not be read appears three times — in `skipped`, in `unavailable` with what having it would have added, and in its own `reproduce` row with the reason it failed. A rate with nothing to divide by comes back as `null` with the reason, never as a zero, and every rate carries its denominator.

## Reading the numbers honestly

Every analytics response from the Docsbook MCP server carries its own caveats in a `metrics` field. Three matter enough to repeat:

- **Visitors are hashed IPs.** Office NAT merges several readers into one; mobile networks split one reader into many. Report trends, never headcounts — `get_retention` is the most affected.
- **Rates are withheld below 30 visits**, and thin days are flagged `thin`. A 100% dead-end rate over four visits is noise.
- **`terminal_success` is not a failure.** A page people leave from after copying a snippet is the best page you have. Every ranking tool exempts these — do not re-introduce the mistake by hand.

## How do I search and edit docs content from an agent?

There are two ways to work with your documentation content from an agent, and which one you want depends on whether the agent has the repository on disk:

- **Hosted, via MCP tokens** — `search_docs` (read-only; works with any connected token regardless of its scope), `get_doc_outline` (read-only; lists every markdown page's title, heading count, and size before searching or writing), and `write_docs` (requires a token authorized with **read-write** scope; commits one or more files as a single atomic git commit). These run against the Docsbook-hosted repository directly, no local checkout needed.
- **Local, via `markdown-lsp`** — for an agent working directly on your checked-out files, [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) exposes richer LSP-style `doc_*` tools (outline, fuzzy headings, full-text, link references, resolve links) by running `npx markdown-lsp <subcommand> ./docs` on the agent's machine. See [Source of Truth](./source-of-truth.md) for the tool list and rationale.

Use `search_docs`/`write_docs` when the agent only has an MCP connection (no local checkout); use `markdown-lsp` when the agent already has the repo on disk and wants deeper graph navigation.

## What does a call to the Docsbook MCP server draw on?

Every metered call to the Docsbook MCP server comes off the **balance of the project the call is about** — the same balance a top-up funds and the rest of that project's AI work draws on. There is no separate meter for MCP, and no monthly quota of calls to plan around. Money is the only limit.

A call is charged a **flat amount, fixed before the call runs and independent of the size of the answer**. The same reporting call draws the same on a site with ten pages and one with ten thousand. What decides the amount is what serving the call makes the server do:

| Class | What the call makes the server do | Tools in it |
|---|---|---|
| Included | Nothing but a lookup | `get_info`, `find_skill`, `find_widget`, `find_tool`, `list_workspaces`, `get_workspace`, `create_workspace` |
| Read | Reads a row it already stores | A page, a setting or a registry row |
| Write | Changes stored state | `update_*`, `create_*`, `set_*`, `register_*` |
| Analytics | Scans the event store | Funnels, journeys, retention, feeds |
| Egress | Leaves the Docsbook network | `fetch_url`, `read_source`, `test_*`, `replay_*` |
| Probe | Gathers and normalises one family of facts, with no model in it | `collect_*` |
| AI | Calls a model to write, read or rank | `write_docs`, `search_docs`, `search`, `get_insights` |
| Agent | Runs a whole agent behind one call | The 135 action tools (`observe_*`, `explain_*`, `discover_*`, `decide_*`, `plan_*`, `draft_*`, `measure_*`, `verify_*`, `learn_*`, `handoff_*`), plus `audit_geo` and `run_docs_*` |

**An action tool is priced from the work it declares** — how many families of evidence it reads, how many model round trips it may take, whether it leaves your site, whether it writes an artifact — rather than one flat figure for the whole class. So a narrow observation draws a fraction of what a deep draft does, and its published wait (roughly 20 s to 70 s) differs the same way.

The current amount for every class and every individual tool is on the tool's own row in the **MCP** section of your admin panel, read live from the server rather than from a written-down copy, and on the [Docsbook pricing page](https://docsbook.io/pricing). This page deliberately quotes neither: a price copied into documentation is a price that goes stale without anyone noticing.

**Discovery is never metered.** Describing the server, finding a skill or a widget, listing your workspaces and creating one cost nothing — you should not be charged for the handshake, or for the call that creates the thing being billed.

**Which project pays is worked out from the call itself** — the workspace you named, the repository it is scoped to — and only ever a project you own. A call that names no project is served unmetered. A tool that goes on to do AI work draws for that work as well; the two add rather than replace each other.

**When the balance runs out**, a metered call is refused before it runs, and the refusal names which project ran out, what the call draws, what is left, and where to top that project up. Nothing is granted to a balance on a schedule, though you can set up a monthly payment of your own on the billing screen, which tops the same balance up each month. Free discovery keeps working, so your agent can still find out what happened.

**A call that fails is still charged** — the work happened, and the answer says so. A call the server never managed to run is not charged.

**You can read the calls line by line.** Every metered call appears in the project's [Feeds panel](../reference/webhooks.md#mcp-tool-calls-in-the-feed) — which tool, whether it worked, how long it took and what it drew — filterable by billing class. Calls that were about no single project (describing the server, listing your projects, creating one) belong to your account and appear in no project's feed; discovery calls leave no row at all.

Unauthenticated, repo-scoped access to a public documentation site is never metered.

## What a token is allowed to do

Access to the Docsbook MCP server is decided by the token, not by a tier. A token carries a **scope**, and the scope is the only thing that separates reading from writing:

- **Read-only** — every reporting, search and outline tool answers. `write_docs`, `create_issue` and the three writing `run_docs_*` runs refuse, and say why.
- **Read-write** — the same, plus committing pages, filing issues and changing settings.
- **No token at all** — on a repo-scoped endpoint (`docsbook.io/{owner}/{repo}/api/mcp/server`), `get_info`, `find_skill`, `find_widget` and `list_content_widgets` answer from the public catalog, and `search` answers over that site's own documentation — the one tool here that reads a project, because what it reads is the published site. It is refused on a private site, on a site whose plan has lapsed, on an endpoint not pinned to a site, and when the project has no AI balance left; it takes no project argument, so it can only ever read the site it is pinned to. Every other tool requires a valid Bearer token tied to a Docsbook account.

When a call is refused, the server returns a structured error naming the reason rather than a bare 403, so the agent can tell a reader what to fix. See [MCP Server — Trust & Security](./mcp-security.md) for the authentication flow and what the server stores.

## Related

- [MCP tools reference](../reference/mcp-tools.md) — every tool with its parameters.
- [Chat Hooks](./chat-hooks.md) — Configure pre/post-LLM hooks via MCP.
- [Docs Skills](./skills.md) — Discover SKILL.md files through `find_skill`, or have one run for you with `run_docs_*`.
- [Webhooks](../reference/webhooks.md) — Register event handlers from MCP, and verify their signatures.
- [Pricing](https://docsbook.io/pricing) — what a metered call draws on, generated from the live billing constants.
