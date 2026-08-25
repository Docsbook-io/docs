---
title: "MCP Server — Control Docsbook From Claude"
description: "Manage workspaces, branding, AI chat, translations, analytics, and webhooks from Claude Code over a standard MCP HTTP transport."
---

# MCP Server

Docsbook ships a Model Context Protocol (MCP) server. Connect Claude Code or any MCP-compatible client and manage every aspect of your docs without leaving the editor.

## What MCP is

The Model Context Protocol is an open standard for exposing tools, resources, and prompts to AI agents over a typed RPC interface. The Docsbook MCP server exposes 84 tools — 66 named tools plus one registration tool per webhook event — covering the full product surface.

## Endpoint

```text
https://docsbook.io/api/mcp/server
```

Authentication is OAuth 2.0 Authorization Code with PKCE. Bearer tokens are returned to the client and refreshed transparently.

## Install in your AI client

The Docsbook MCP server is a remote HTTP server with OAuth — every modern MCP client can connect to it using the same endpoint.

You can also browse the catalog inside your own project: open the admin panel, pick `Agents` in the sidebar, then `MCP`. It lists every tool the server serves right now — read live from the server rather than from a written-down copy — with each tool's description, its arguments, and example sentences to say to a connected agent.

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

ChatGPT supports remote MCP through **Connectors** (Pro / Business / Enterprise plans).

1. Open **ChatGPT → Settings → Connectors → Advanced → Developer mode**.
2. Click **Create** and paste the URL: `https://docsbook.io/api/mcp/server`.
3. Authorize in the browser when prompted.

## What the tools are for

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

| Tool | What it is worth | Min plan |
|---|---|---|
| `update_seo` | Meta tags, sitemap, OpenGraph. Table stakes: without it, pages that deserve to rank cannot. | Free |
| `update_geo` | Generative Engine Optimization — structures the page so an LLM can quote it *and attribute it to you*. The difference between being the source of an AI answer and being invisible inside one. | Free |
| `update_aeo` | Answer Engine Optimization — shapes content into the direct-answer form AI assistants lift verbatim. | Free |
| `get_search_rankings` | Real Google Search Console positions, plus the **"worth improving" set at position 5–20** — pages Google already shows that are not yet winning the click. Turns "we should do SEO" into a named page and a named query. Lags Google by ~2 days. | PRO |
| `get_analytics` (AI-bot breakdown) | Whether ChatGPT, Perplexity and Claude crawlers read you at all. A zero here means the GEO work is not landing — no crawl, no citation, no referral. | Free |

Buyers increasingly ask an assistant before they ask a vendor. If the assistant answers from a competitor's docs, you never enter the shortlist and the loss appears in no dashboard.

### Not losing the reader

`get_visit_outcomes` (PRO) is the headline number of the whole product: it classifies every visit as success / dead end / bounce / partial and reports the **dead-end rate** and **self-serve resolution rate**. A dead end is a reader who searched, asked the AI, or opened several pages — and still left with nothing. Everything below answers "…and where exactly?"

| Tool | What it is worth | Min plan |
|---|---|---|
| `get_dead_end_pages` | The rewrite queue, ranked. Rows marked `terminal_success` are pages people leave from *because they got what they needed* — the tool protects your best pages from being "fixed". | PRO |
| `get_content_health` | One 0–100 score per page, combining dead-end exits with negative feedback. Replaces cross-referencing four reports by hand on a large doc set. | PRO |
| `get_rage_signals` | Pages re-entered 3+ times in one visit, A→B→A bounce-backs, repeated searches. Dead-end rate says a visit failed; this says *where*. Re-entry means the answer should be on that page and is not — the fix is restructuring, not new content. | PRO |
| `get_route_patterns` | The 2–4 page sequences readers actually walk, and how often each ends well. A frequent route that ends badly is a **navigation defect, not a page-quality problem** — rewriting those pages will not fix it. | PRO |
| `get_reverse_funnel` | Works backwards from successful visits: which entry pages lead to a good ending. Needs no hypothesis, so it surfaces the path readers found that you never designed. | PRO |
| `get_forward_funnel` | Completion of the route *you* declared, and which transition leaks. Your onboarding-completion rate. | PRO |
| `get_metric_timeseries` | Any headline metric by day — the only tool that answers "is this getting worse" and lines a change up against a release date. | PRO |
| `get_visits` | The evidence behind the rates: one reconstructed visit at a time. Use when a number is disputed, or to attach a real reader to a complaint. | PRO+ |
| `get_retention` | W1/W4 return rate by cohort. Direction depends on the section: high return is healthy for reference docs and a **failure** for onboarding. | Business |

### Demand you are not serving

Every row here is a support ticket you can pre-empt by writing one page.

| Tool | What it is worth | Min plan |
|---|---|---|
| `get_ai_unanswered` | Questions the assistant could not answer, in the reader's own words. The cheapest content plan there is. | PRO |
| `get_failed_searches` | Searches returning zero results — the same gap through a different door. | PRO |
| `get_search_zero_click` | Searches that returned results and got **no click**. The gap zero-result reports miss: search worked and the reader rejected every result, which points at **titles and summaries** — an order of magnitude cheaper to fix than page bodies. | PRO |
| `get_popular_searches` | What people look for most. Read against `get_content_health` on the same page: high demand + low health = your most expensive broken page. | PRO |
| `get_negative_feedback` | Pages with thumbs-down, ranked. The reader's explicit vote, no inference needed. | PRO |
| `get_insights` | The pre-combined digest — doc gaps, zero-result searches and disliked pages with impact estimates, in one call. Start here for "what should I fix this week". | PRO+ |

### Selling through the assistant

The chat is not a support widget. It is the only place where a prospect states their objection in plain language.

| Tool | What it is worth | Min plan |
|---|---|---|
| `get_chat_intent` | Conversations split by **buying stage** — evaluation, pricing, integration, support, bug. Answers who is deciding whether to buy and what blocks the purchase. **Names the competitor** when readers mention one: competitive intelligence no page-level report can produce. | PRO+ |
| `get_chat_conversations` | Questions grouped by topic, with `click_through` — the share of conversations where the reader opened a cited page. A topic with buying intent and **no clicks is a sales leak**: the answer was correct and carried nobody forward. The unit is a conversation, not a question, because four questions from one stuck reader and one each from four readers give identical counts and opposite conclusions. | PRO |
| `set_chat_system_prompt` | Where the fix lands — turns the assistant from a librarian into a salesperson: qualify, handle the objection, route to a demo. | PRO+ |
| `set_chat_hooks` / `test_chat_hook` | Pre/post-LLM hooks: inject live context (pricing, availability, the reader's plan) or capture a lead the moment intent appears. | PRO+ |
| `get_ai_questions` | Verbatim question log — raw material for FAQ, onboarding email, objection handling. | PRO |

A pricing objection stated in your docs chat is worth more than a page view: the reader qualified themselves and told you exactly what stops them buying.

### Acting on the finding

Diagnosis without a fix is a report. These close the loop inside one connection.

| Tool | What it is worth | Min plan |
|---|---|---|
| `search_docs` | Verbatim, citable sections — text, regex, heading or path modes. What an agent reads *before* editing so it changes the right lines. | Free |
| `get_doc_outline` | Every page with title, heading count, size. Cheap orientation before a search or a write. | Free |
| `write_docs` | Commits one or many markdown files in **one atomic git commit**. Turns analysis into a shipped change. | Free |
| `fetch_url` | Reads one public web page as clean Markdown. The tool that lets an agent check a page against the world outside your workspace — a competitor's pricing, your own marketing site, or whether a link a doc depends on is still alive. | Free |
| `get_change_history` | **Call before editing.** What was changed before and how the affected pages' traffic moved after — with raw before/after visit counts, `low_sample` and `pending` flags, and **no verdict on purpose** (a commit and a traffic move in the same week are not cause and effect). Without it, the same recommendation gets made forever with the same confidence. | PRO |
| `get_page_diff_impact` | **Call after shipping.** Did that edit actually help? Compares the pages a commit touched against the pages it did not, before and after — outcome mix, self-serve resolution, time to first value. The untouched pages are the control, and they are the point: docs traffic moves for reasons unrelated to your edit, so an improvement only counts if it beat the site trend. A change that merely matched it is reported as no effect, not as a win. Also breaks the visits down by country, reader language and device, each next to the same slice's move on the untouched pages — which is what turns "traffic went up" into a decision. Where you have set an average price and a call-to-action URL, it also prices the edit — conversions and revenue on the touched pages, before and after. | PRO |
| `update_navigation` | The fix for a defect `get_route_patterns` or `get_reverse_funnel` found — often cheaper and more effective than rewriting a page. | Free |
| `find_skill` / `find_widget` | Discover a packaged capability — a workflow skill, an interactive widget — instead of writing one. | Free |

### Knowing without looking

A dashboard only works if someone opens it. A webhook works always. Registering any webhook is **Business-only**.

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

| Tool | What it is worth | Min plan |
|---|---|---|
| `update_languages` | Enable a target language. Read alongside the country/language breakdown in `get_analytics`: **translate where the readers already are**, not where you hope they will be. | PRO |
| `set_translation_mode`, `upload_translation`, `approve_translation`, `list_pending_translations`, `get_translation`, `delete_translation` | The translation pipeline — automatic, or externally supplied with human approval. | PRO / PRO+ |
| `update_access` | Private workspace, password, or your own SSO/OIDC. Unblocks selling to companies whose procurement requires it. | PRO |
| `update_domain` | Docs on your own domain — the SEO authority accrues to **you**, not to a vendor subdomain. | Pro |
| `update_branding`, `update_ui_settings` | Your product, not a platform's. | Free |

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

## Reading the numbers honestly

Every analytics response carries its own caveats in a `metrics` field. Three matter enough to repeat:

- **Visitors are hashed IPs.** Office NAT merges several readers into one; mobile networks split one reader into many. Report trends, never headcounts — `get_retention` is the most affected.
- **Rates are withheld below 30 visits**, and thin days are flagged `thin`. A 100% dead-end rate over four visits is noise.
- **`terminal_success` is not a failure.** A page people leave from after copying a snippet is the best page you have. Every ranking tool exempts these — do not re-introduce the mistake by hand.

## Searching and editing documentation content

There are two ways to work with your docs content from an agent:

- **Hosted, via MCP tokens** — `search_docs` (Free plan and up, read-only, works with any connected token regardless of its scope), `get_doc_outline` (Free+, read-only; lists every markdown page's title, heading count, and size before searching or writing), and `write_docs` (Free+, requires a token authorized with **read-write** scope; commits one or more files as a single atomic git commit). These run against the Docsbook-hosted repository directly, no local checkout needed.
- **Local, via `markdown-lsp`** — for an agent working directly on your checked-out files, [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) exposes richer LSP-style `doc_*` tools (outline, fuzzy headings, full-text, link references, resolve links) by running `npx markdown-lsp <subcommand> ./docs` on the agent's machine. See [Source of Truth](./source-of-truth.md) for the tool list and rationale.

Use `search_docs`/`write_docs` when the agent only has an MCP connection (no local checkout); use `markdown-lsp` when the agent already has the repo on disk and wants deeper graph navigation.

## Plan gating

Each tool declares a minimum plan. The server returns a structured error when a tool is called below the required tier.

| Plan | Available tool groups | What you can decide with it |
|---|---|---|
| Free | Workspace, branding, UI, navigation, traffic analytics (24h), `find_skill`, `find_widget`, `search_docs`, `get_doc_outline`, `write_docs` (with a read-write token), SEO/GEO/AEO | Whether readers arrive at all |
| PRO | + `get_search_rankings`, AI settings, languages, translations, private docs (`update_access`), demand gaps, **visit outcomes, dead-end pages, content health, route patterns, funnels, change history** | Which page is costing you customers, and whether the fix worked |
| PRO+ | + `get_insights`, `get_chat_intent`, `get_visits`, page journeys, top visitors, visitor drill-down, chat hooks, `query_events` | Who is deciding whether to buy, and what blocks the purchase |
| Business | + webhooks, `get_retention`, bring-your-own AI/translation API key | Long-run retention, and reacting without opening a dashboard |

## Related

- [MCP tools reference](../reference/mcp-tools.md) — every tool with its parameters and minimum plan.
- [Chat Hooks](./chat-hooks.md) — Configure pre/post-LLM hooks via MCP.
- [Docs Skills](./skills.md) — Discover SKILL.md files through `find_skill`.
- [Webhooks](../webhooks.md) — Register event handlers from MCP.
