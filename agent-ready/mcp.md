---
title: "MCP server: run your documentation from a coding agent"
description: "Connect Claude Code, Cursor, Codex or any MCP client to Docsbook and read, write, measure and configure your documentation from inside the editor."
tldr: "Docsbook's remote MCP server exposes 167 typed tools over one OAuth-protected endpoint. Since 2026-09-18 your own connected agent meets a small owner surface — orientation, reading your own docs, and giving a job to `docsbook_agent` — and delegates everything else (writing docs, translations, webhooks, settings, analytics) to that background worker instead of calling it directly. Calls are billed per call against the project's balance by billing class; discovery is free."
status: generated
version: "0.3"
---

# MCP Server

The Docsbook MCP server is a remote Model Context Protocol server that exposes your documentation and its whole admin surface to an AI agent. Connect Claude Code or any MCP-compatible client to one endpoint and read your pages, commit changes, read analytics, and change settings without leaving the editor.

This page is the reference for what the server serves and what a call draws on. Every tool listed here is callable by any connected client; what a metered call costs is on the [Docsbook pricing page](https://docsbook.io/pricing) and on each tool's own row in your admin panel.

## What is the Docsbook MCP server?

The Docsbook MCP server registers **167 tools** over the Model Context Protocol, an open standard for handing tools, resources and prompts to AI agents over a typed RPC interface. Not every tool is reachable by every caller — see the next section before you go looking for `write_docs` on your own token.

## Two surfaces, one endpoint (2026-09-18)

**Your own connected agent — the one that just completed the OAuth step above — meets a small, fixed surface, not the 167-tool catalog.** Orientation (`get_info`, `list_workspaces`, `get_workspace`), creating a project, reading your own documentation and Docsbook's own docs by meaning or by name, and the five tools that give a job to **`docsbook_agent`** and watch it (`docsbook_agent`, `docsbook_agent_status`, `docsbook_agent_tasks`, `docsbook_agent_reply`, `docsbook_agent_stop`). That is the whole of "manage the documentation" from your own token now.

**Everything else described on this page — writing documentation, translations, webhooks, settings, analytics beyond your own project's summary, the product's own accumulated memory — is performed by `docsbook_agent`, not called by you directly.** Describe the outcome in your own words ("improve the docs", "document this API", "why are readers not converting") and it plans the work, makes the calls itself, and reports back. The tool-by-tool sections below are still worth reading in full: they are `docsbook_agent`'s capability list, and knowing what it *can* do is how you know what to ask it for.

`docsbook_assistant` — the specialist that answers HOW a page should be structured, what a quickstart owes its first screen, how to write a passage an answer engine will quote whole — moved behind `docsbook_agent` the same day: it is read from inside a task now, not called on your own token. The same retrieval still answers reader questions instantly and for free on the public "Ask AI" chat at [docsbook.io](https://docsbook.io) and on the anonymous MCP endpoint's `search` — neither of those needs a token.

A narrow, separate slice of pure configuration (branding, navigation, the chatbot, translation mode, mention tracking) is reachable directly over REST by your workspace API key even though it is not on your MCP token's surface — see the [REST API reference](../rest-api/README.md) for that list.

**Why the surface narrowed.** Before 2026-09-18 every connected client met the same ~150 names: the reads, the writes, the settings, this project's accumulated memory and hypotheses. That assumed the caller was a coding agent holding the repository and the method — true of Docsbook's own background worker, false of the customer this endpoint is sold to. What moved behind `docsbook_agent` is MANAGEMENT — writing, configuring, measuring, and everything that carries method rather than content; the reads that answer "what does my own documentation say" stayed, because hiding those would protect nothing and break the one integration every customer already has.

## Endpoint

The Docsbook MCP server is served at one URL for every workspace and every client:

```text
https://docsbook.io/api/mcp/server
```

Authentication is an OAuth authorization-code flow with PKCE. The client receives one opaque Bearer token, which it presents on every call; no refresh token is issued and the token does not expire on its own, so rotation means revoking it in the panel and authorizing again. There is no per-project MCP URL to look up: the OAuth flow is scoped to the signed-in account, and the client picks the workspace afterwards. See [MCP server security](./mcp-security.md) for the flow, the scopes and the gaps.

## How do I connect my AI client to Docsbook?

Point your client at `https://docsbook.io/api/mcp/server` and complete the OAuth prompt in the browser. The Docsbook MCP server is a remote HTTP server with OAuth, so every modern MCP client connects to it with the same endpoint and no local process to run. The subsections below give the exact command or config file for each client.

You can also reach the server from inside your own project: open the admin panel, go to **Integrations ▸ Connectors** and open the **MCP server** card. MCP is a connector there like any other rather than a section of its own — pointing a client at this project is the one thing that section was ever opened for, and that is what a connector is. The card's page carries this project's endpoint, what the server exposes, and the direction data moves; the **Connect** button above the grid gives the install command for your client.

A single tool still has its own page, and the page still has an address: the URL carries the tool, so you can refresh it, bookmark it, or send it to a colleague and land them on the same tool. Everything on it is about that one tool. Its arguments are a form with a **Run** button that makes a real call against this project, and the button carries the price before the money moves. Under that is its **call history**, drawn by the same **Feeds** table you read everywhere else, narrowed to this one tool: one line per call, and expanding a row shows the call in full — what went in, what came back, who asked (your own client, an outside agent, a webhook delivery), how long it took, what it was priced at, and what actually left your balance. Under that sits one worked example to copy into your own client; what runs from inside Docsbook is the call, made by you or your agent — nothing here calls itself.

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

Every tool named from here down is `docsbook_agent`'s toolbox, not your own token's — give it the job and it makes these calls itself (see "Two surfaces, one endpoint" above). Reading the sections below tells you what to ask for, not what to call.

The Docsbook MCP tools exist to make one of four things happen: more qualified readers arrive, more of them leave with what they came for, more buying-intent readers are carried forward by the assistant, and fewer questions reach a person. Everything below is grouped by which of those four it serves.

Your documentation is not a cost centre. It is a channel with three jobs: **get found** (by Google, and by the AI assistants your buyers now ask instead of Google), **convert the reader** (a visit that ends with nothing is a lost customer who never complained), and **prove what worked** (so the next edit is a decision, not a guess).

There are only four ways a docs tool makes money, and every tool below serves one of them:

| Lever | Mechanism | Core tools |
|---|---|---|
| **Acquisition** | More qualified readers arrive, from search and from AI answers | `get_search_rankings`, `collect_ai_citability`, `write_docs` |
| **Conversion** | More arriving readers leave with what they came for | `get_visit_outcomes`, `get_dead_end_pages`, `get_content_health`, `get_route_patterns` |
| **Sales** | The assistant carries buying-intent readers forward instead of just answering | `get_chat_intent`, `get_chat_conversations`, `set_chat_system_prompt`, `set_chat_hooks` |
| **Cost avoided** | Questions answered by the docs are questions not answered by a person | `get_ai_unanswered`, `get_failed_searches`, `get_search_zero_click`, `get_insights` |

A tool that serves none of these returns **context**, not a decision. `Pageviews: 12,340` is context. `31% of your readers left with nothing` is a decision.

### Getting found

| Tool | What it is worth |
|---|---|
| *(no tool)* | Meta tags, sitemap, OpenGraph, TL;DR, author markup and FAQ/HowTo/speakable JSON-LD are emitted for every project automatically. There were `update_seo`, `update_geo` and `update_aeo` tools until 14 September 2026; they set flags that are now permanently on, so they were removed rather than left reporting changes they no longer make. |
| `collect_ai_citability` | Whether that markup is actually reaching the live pages, and whether an assistant can fetch and quote them at all — the question the three removed tools could never answer. |
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
| `list_tool_calls` | **Call before editing.** Every read made here is kept with the answer it gave, so any read tool is a snapshot instrument. This groups them into series — one tool on one page, heading, host, search query or the whole site, and a reading taken about a whole SET of phrases is filed under that set — and says which already have a second reading to compare against. Without it the same recommendation gets made forever with the same confidence, and a rewrite ships with no baseline to judge it by. |
| `compare_tool_calls` | **Call after shipping, for a change that was not a commit** — a setting, a language, the navigation, the assistant's prompt. Puts two readings of the same instrument side by side and reports every number that moved, what appeared, what went away, and how many fields did *not* move, which is the denominator. A percentage is `null` when the baseline was zero, never `∞`. **No verdict on purpose**: two readings a week apart are two facts, not cause and effect. |
| `search_tool_calls` / `get_tool_call` | Find a past reading by what is inside it — a page it was about, a word in the answer, an error it returned — ranked so the calls actually *about* a page beat the ones that merely mention it; then read one whole. |
| `list_memory` / `add_memory` / `edit_memory` / `remove_memory` | The project's brief between sessions: what these docs are FOR (`goal`), what nobody has answered yet (`question`), and the facts, rules and preferences every agent otherwise works out again on every run. Read it before deciding anything — the goals are what a recommendation gets argued against, and an owner's rule outranks an agent's reading of the site. Write back: anything the next session would re-derive, a `question` at the moment you would otherwise guess, and an answer onto one you closed. Visible and editable by the owner on the panel's Overview, so nothing here is an agent's private notes about somebody else's product. |
| `get_page_diff_impact` | **Call after shipping, for a change that WAS a commit.** Did that edit actually help? Compares the pages a commit touched against the pages it did not, before and after — outcome mix, self-serve resolution, time to first value. The untouched pages are the control, and they are the point: docs traffic moves for reasons unrelated to your edit, so an improvement only counts if it beat the site trend. A change that merely matched it is reported as no effect, not as a win. Also breaks the visits down by country, reader language and device, each next to the same slice's move on the untouched pages — which is what turns "traffic went up" into a decision. Where you have set an average price and a call-to-action URL, it also prices the edit — conversions and revenue on the touched pages, before and after. Called with no commit, it lists the commits it can measure. |
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
| `set_translation_mode`, `run_translation_pass`, `get_translation_status`, `upload_translation`, `approve_translation`, `list_pending_translations`, `get_translation`, `delete_translation` | The translation pipeline — `run_translation_pass` starts a real automatic catch-up run and `get_translation_status` reports each language's coverage before you spend on one, or bring translations in externally with human approval. |
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
list_tool_calls         → has this page been "fixed" before, and did it work?
search_docs → write_docs → ship the fix
get_page_diff_impact    → did the edited pages beat the pages you did not touch?
compare_tool_calls      → …and for a change that was not a commit, the same
                          reading before and after
```

The rate alone is unactionable, the page list alone lacks a cause, and a fix without `list_tool_calls` repeats a failed edit with full confidence. The last step is what closes the loop: a site-wide trend line moves for a dozen reasons, so "the rate improved after my commit" is only evidence when the pages you edited improved *more than the ones you left alone*. Only the sequence produces a change you can defend.

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
write_docs                → shape the passage an engine can lift
collect_ai_citability     → confirm the markup is really on the live page
get_analytics (ai_bots)   → confirm crawlers are actually reading it
get_search_rankings       → track classic-search position alongside
get_analytics (referrers) → referrals arriving from AI assistants
get_visit_outcomes        → and whether those arrivals end in success
```

The last step is the one everybody skips. Traffic from an AI answer that dead-ends is worse than no traffic — you earned the visibility and burned the impression.

### The self-healing loop

Run Loop 1 on a schedule from CI:

```text
weekly:  get_content_health  → take the worst 3, and this reading is
                                also the baseline for next week
         list_tool_calls     → skip anything already tried and failed
         search_docs → write_docs → open a PR
         get_page_diff_impact → report on the PR whether the edited pages
                                beat the untouched ones, or say they did not
         compare_tool_calls  → next week, this week's reading against
                                last week's, on the same pages
```

Documentation that repairs itself and shows its work — "saw the problem" and "fixed the problem" without leaving the connection.

## Prompt library

One request per lever above, in the words you would actually type — give any of these to `docsbook_agent` from Claude Code, Cursor or another connected client once OAuth is done:

- **Acquisition:** "Are AI assistants actually reading our docs, and where do we rank in Google for our own quickstart?" → `get_analytics` (AI-bot breakdown), `get_search_rankings`
- **Conversion:** "Which page is losing readers, and why?" → `get_visit_outcomes`, `get_dead_end_pages`, `get_rage_signals`
- **Sales:** "Pull every chat conversation where someone was comparing us to a competitor." → `get_chat_intent`
- **Cost avoided:** "What are people asking the docs assistant that it can't answer?" → `get_ai_unanswered`, `get_failed_searches`

Give any of these, plus `workspace_id`, to `docsbook_agent` rather than running the route yourself — it plans through the tools named above and calls them itself, and reports back what it did.

## Handing over the whole job

`docsbook_agent` starts a real background run and hands back a `task_id` to poll — `docsbook_agent_status` for one job, `docsbook_agent_tasks` for every job on the account, `docsbook_agent_reply` to answer a question it asks mid-run, `docsbook_agent_stop` to cancel it.

There used to be four narrower runners — `run_docs_analyze`, `run_docs_create`, `run_docs_manage`, `run_docs_automate` — retired 2026-09-12 along with `get_agent_run`, `list_agent_runs` and `cancel_agent_run`. For six days after that (2026-09-12 to 2026-09-18) nothing on this server ran unattended at all: the one agent, `docsbook_expert`, only ever advised, and you made every call yourself on your own token. `docsbook_agent` is what replaced it, and the direction reversed: describe the job in your own words — "improve the docs", "document this API", "why are readers not converting" — and it does the work itself rather than handing you steps to run. `find_skill` still hands over the long-form method when you want the whole rulebook a job draws on, rather than delegating it.

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

What you do not get is a judgement. No findings, no scores, no ranking, no recommendation — a collector that quietly included one would be a model run at a fraction of the price. For the judgement, give the job to `docsbook_agent`: it reads the rows, says what they mean, and what would make that reading wrong.

**When the cheap one is the right one.** `collect_corpus_map` needs no search data, no traffic and no history at all, and hands back real rows on a site that went up this morning — useful on exactly the projects where every analytics-shaped question answers "not enough data yet".

**What is missing is said out loud.** A source that could not be read appears three times — in `skipped`, in `unavailable` with what having it would have added, and in its own `reproduce` row with the reason it failed. A rate with nothing to divide by comes back as `null` with the reason, never as a zero, and every rate carries its denominator.

## Reading the numbers honestly

Every analytics response from the Docsbook MCP server carries its own caveats in a `metrics` field. Three matter enough to repeat:

- **Visitors are hashed IPs.** Office NAT merges several readers into one; mobile networks split one reader into many. Report trends, never headcounts — `get_retention` is the most affected.
- **Rates are withheld below 30 visits**, and thin days are flagged `thin`. A 100% dead-end rate over four visits is noise.
- **`terminal_success` is not a failure.** A page people leave from after copying a snippet is the best page you have. Every ranking tool exempts these — do not re-introduce the mistake by hand.

## How do I search and edit docs content from an agent?

There are two ways to work with your documentation content from an agent, and which one you want depends on whether the agent has the repository on disk:

- **Hosted, via MCP tokens** — `search_docs` and `get_doc_outline` are read-only and on your own owner surface: call them directly, with any connected token. `write_docs` is not: since 2026-09-18 it is reached only by giving `docsbook_agent` a job that writes, never by calling it yourself. These run against the Docsbook-hosted repository directly, no local checkout needed.
- **Local, via `markdown-lsp`** — for an agent working directly on your checked-out files, [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) answers richer graph questions (workspace outline, fuzzy heading search, full-text with context, incoming and outgoing links, link resolution) as commands the agent runs — `npx markdown-lsp <subcommand> ./docs` — or as a language server. It is not an MCP server and needs no token. See [Source of Truth](./source-of-truth.md) for the subcommand list and the rationale.

Use `search_docs`/`write_docs` when the agent only has an MCP connection (no local checkout); use `markdown-lsp` when the agent already has the repo on disk and wants deeper graph navigation.

## What does a call to the Docsbook MCP server draw on?

Every metered call to the Docsbook MCP server comes off the **balance of the project the call is about** — the same balance a top-up funds and the rest of that project's AI work draws on. There is no separate meter for MCP, and no monthly quota of calls to plan around. Money is the only limit.

A call is charged a **flat amount, fixed before the call runs and independent of the size of the answer**. The same reporting call draws the same on a site with ten pages and one with ten thousand. What decides the amount is what serving the call makes the server do:

| Class | What the call makes the server do | Tools in it |
|---|---|---|
| Included | Nothing but a lookup | `get_info`, `find_skill`, `find_widget`, `list_workspaces`, `get_workspace`, `create_workspace` |
| Read | Reads a row it already stores | A page, a setting or a registry row — the class an unclassified tool falls to |
| Write | Changes stored state | `create_*`, `update_*`, `set_*`, `delete_*`, `register_*`, `unregister_*`, `upload_*`, `approve_*`, `mark_*` |
| Analytics | Scans the event store | Funnels, journeys, retention, rankings, feeds, `query_events` |
| Egress | Leaves the Docsbook network | `fetch_url`, `read_source`, `test_*`, `replay_*`, the four tracker reads (`list_issues`, `get_issue`, `get_pull_request`, `search_prior_work`), and the vendor-backed scraping tools |
| Probe | Gathers and normalises one family of facts, with no model in it | `collect_*` |
| AI | Calls a model to write, read or rank | `write_docs`, `search_docs`, `search`, `get_insights`, `get_chat_intent` |
| Lens | One model pass over an evidence record it was handed, re-read from a single declared angle | Reserved (`lens_*`) — no tool is in this class today |
| Agent | Runs a whole agent behind one call | None today. The 135 action tools, the 41 `agent_*` goals, the four `run_docs_*` runners and `audit_geo` were in this class until 2026-09-12; their historical calls still price and report under it. `audit_geo` itself was renamed to `collect_ai_citability` and now bills as Probe — its evidence layer is code, not a model |

⚡ **Per-tool pricing inside the Agent class went with the action family.** While there were 135 of them, each was priced from the work it declared — how many families of evidence it read, how many model round trips it might take, whether it left your site — so a narrow observation drew a fraction of a deep draft. What remains in the class spans the band honestly, so it is priced at the band.

The current amount for every class and every individual tool is on the tool's own row in the **MCP** section of your admin panel, read live from the server rather than from a written-down copy, and on the [Docsbook pricing page](https://docsbook.io/pricing). This page deliberately quotes neither: a price copied into documentation is a price that goes stale without anyone noticing.

**Discovery is never metered.** Describing the server, finding a skill or a widget, listing your workspaces and creating one cost nothing — you should not be charged for the handshake, or for the call that creates the thing being billed.

**Which project pays is worked out from the call itself** — the workspace you named, the repository it is scoped to — and only ever a project you own. A call that names no project is served unmetered. A tool that goes on to do AI work draws for that work as well; the two add rather than replace each other.

**When the balance runs out**, a metered call is refused before it runs, and the refusal names which project ran out, what the call draws, what is left, and where to top that project up. Nothing is granted to a balance on a schedule, though you can set up a monthly payment of your own on the billing screen, which tops the same balance up each month. Free discovery keeps working, so your agent can still find out what happened.

**A call that fails is still charged** — the work happened, and the answer says so: a failed call comes back `ok: false` with `accepts` (the arguments that tool actually declares), `you_sent`, `missing_required`, and one `next` line naming the fix, so a wrong or misnamed argument reads as a shape to correct rather than as the tool being broken. A call the server never managed to run is not charged.

**You can read the calls line by line.** The project's **Agent** section reads them as the conversation they were: one continuous stream, broken only by the day, with each call on its own line saying what it was for, what it was called with and what came back — so you can tell whether an agent is changing anything without opening a single row. Clicking one unfolds the full result, the arguments it was given and who made the call. The same calls also appear in the [Feeds panel](../reference/webhooks.md#mcp-tool-calls-in-the-feed) when you want them as a filterable table instead, narrowed by billing class. Calls that were about no single project (describing the server, listing your projects, creating one) belong to your account and appear in neither; discovery calls leave no row at all.

**The Agent section is also where you set one running.** It offers a single prompt to paste into whichever AI agent you already work in, with a cadence to pick first — every hour, every four hours, every twelve, or once a day. The choice is written into the prompt itself, cron line included, so what you copy is complete on its own.

Unauthenticated, repo-scoped access to a public documentation site is never metered.

## What a token is allowed to do

Since 2026-09-18 the first gate is the **audience** — which surface your token meets at all, described above — and it is decided by who is connecting, not by a per-call scope: your own OAuth token is always `owner` and always meets the same sixteen names, whatever scope it carries.

- **Owner, read-only** — the orientation and read tools answer; giving `docsbook_agent` a job that would need to write anything is refused with the reason named, before the job starts.
- **Owner, read-write** — the whole owner surface: orientation, reading your own documentation and Docsbook's own docs, creating a project, and giving `docsbook_agent` a job (including one that writes).
- **`docsbook_agent` itself** — a token minted per task, scoped to the workspaces named in that task, meeting the full catalog described on this page minus four account-wide tools (`create_workspace`, `update_access`, `grant_repo_access`, `list_workspaces`) a task scoped to existing projects has no business reaching. This is not a token you hold yourself; it is what the background worker runs on while it carries out the job you gave it.
- **No token at all** — on a repo-scoped endpoint (`docsbook.io/{owner}/{repo}/api/mcp/server`), `get_info`, `find_skill`, `find_widget` and `list_content_widgets` answer from the public catalog, and `search` answers over that site's own documentation — the one tool here that reads a project, because what it reads is the published site. It is refused on a private site, on a site whose plan has lapsed, on an endpoint not pinned to a site, and when the project has no AI balance left; it takes no project argument, so it can only ever read the site it is pinned to. Every other tool requires a valid Bearer token tied to a Docsbook account.

When a call is refused, the server returns a structured error naming the reason rather than a bare 403, so the agent can tell a reader what to fix. See [MCP Server — Trust & Security](./mcp-security.md) for the authentication flow and what the server stores.

## Troubleshooting / FAQ

**Is the agents/MCP tooling still working?** Yes, and it changed direction twice. On 2026-09-12 the standing-agent engine described in older material — a scheduled agent that ran on its own, plus 135 action tools and 4 `run_docs_*` runners that only ever ran inside one — was retired in favour of `docsbook_expert`, a single tool that advised in one round trip and ran nothing. On 2026-09-18 `docsbook_expert` was itself removed and replaced by `docsbook_agent`, which runs the job rather than advising on it, and your own token's surface narrowed to sixteen names — see "Two surfaces, one endpoint" above.

**My client still lists `docsbook_expert` (or the older name `docsbook`) — did the connection break?** No, but those names no longer resolve to anything: `docsbook_expert` was removed, not renamed, on 2026-09-18. Reconnect the client so it reads the current tool list and sees `docsbook_agent`.

**A call was refused for an empty balance — what happened?** The refusal names the project, what the call draws, and what is left. Reconnecting or retrying will not fix it; top up the project's balance from the panel. Discovery calls (`get_info`, `find_skill`, listing and creating workspaces) are never metered and keep working regardless.

**Where do I go if a call is refused for a reason other than balance?** The server returns a structured error naming the reason — a missing scope on a read-only token, `NO_GITHUB_ACCESS` when Docsbook's own credential cannot reach a repository in your own GitHub account, or a private site. See [MCP server security](./mcp-security.md) for what each token scope can and cannot do.

**My call came back `ok: false` — what does that mean?** The tool ran and rejected what you sent it — almost always a missing or misnamed argument, not a broken tool. Compare the response's `accepts` list (the arguments that tool actually declares) against `you_sent` and `missing_required`, and follow the one `next` line; a call that still fails once it matches `accepts` is the one worth reporting to Docsbook.

## Related

- [MCP tools reference](../mcp/README.md) — every tool with its parameters.
- [Chat Hooks](../ai-chat/chat-hooks.md) — Configure pre/post-LLM hooks via MCP.
- [Docs Skills](./skills.md) — Discover SKILL.md files through `find_skill`, or give `docsbook_agent` the job and let it use one directly.
- [Webhooks](../reference/webhooks.md) — Register event handlers from MCP, and verify their signatures.
- [Pricing](https://docsbook.io/pricing) — what a metered call draws on, generated from the live billing constants.
