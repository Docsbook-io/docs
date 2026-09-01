---
title: "MCP Tools Reference"
description: "Complete reference of Docsbook MCP tools — workspace management, content access, AI chat configuration, translations, analytics, webhooks, and skills discovery."
---

# MCP Tools Reference

This page lists every tool exposed by the Docsbook MCP server at `https://docsbook.io/api/mcp/server`. Each tool requires Bearer authentication via OAuth 2.0 + PKCE. The minimum plan column indicates the workspace tier required to call the tool; calls below that tier return a `plan_required` error.

To connect from Claude Code:

```bash
mcp add --transport http https://docsbook.io/api/mcp/server
```

## Workspace and branding

| Tool                  | Min plan | Description                                                  |
| --------------------- | -------- | ------------------------------------------------------------ |
| `get_info`            | Free     | Server capabilities, version, available tool list            |
| `list_workspaces`     | Free     | All workspaces for the authenticated user with capabilities  |
| `get_workspace`       | Free     | Fetch one workspace by ID or `owner/repo`                    |
| `create_workspace`    | Free     | Create a workspace from a GitHub repository                  |
| `update_branding`     | Free     | Colors, fonts, logo, icon, default theme, call-to-action URL, site source URL, average product price |
| `update_ui_settings`  | Free     | Toggle header, search, feedback, copy button, breadcrumbs    |
| `update_navigation`   | Free     | Header links, social links, subheader folder tabs (with optional icons), left-sidebar page/folder icons |
| `update_ai_settings`  | PRO      | Enable AI chat, set provider and API key, model selection (bring-your-own key is Business only) |
| `update_seo`          | Free     | SEO meta tags, sitemap, OpenGraph                            |
| `update_access`       | PRO      | Make a workspace private; set a password and/or bring-your-own SSO/OIDC identity provider |
| `update_domain`       | Business | Attach or remove a custom domain                             |
| `update_languages`    | PRO      | Enable target languages for AI translation                   |

## Content and documentation

| Tool           | Min plan | Description                                                                                          |
| -------------- | -------- | ----------------------------------------------------------------------------------------------------- |
| `search_docs`  | Free     | Full-text/regex/heading/path search over the workspace's documentation content. Read-only — works with any token regardless of read/write scope. |
| `search`       | Business | Semantic (embeddings-based) search over the workspace's documentation content — finds pages by meaning, not literal keyword overlap. Reads a pre-built vector index (no re-indexing on search). Read-only. Requires the index to be built and enabled; falls back to `search_docs` otherwise. |
| `get_doc_outline` | Free  | List every markdown page's title, heading count, and size before searching or writing. Read-only — works with any token regardless of read/write scope. |
| `write_docs`   | Free     | Commit one or more markdown files to the workspace's docs repo in a single atomic git commit. Requires a token authorized with **read-write** scope — a read-only token is refused. Takes an optional `intent`: what the person asked for, in their own words. It is shown against the commit in the Changes panel, so the goal behind an edit outlives the conversation that produced it. |
| `fetch_url`    | Free     | Read one public web page and return it as clean Markdown, with its title, description and the final URL after redirects. For checking a claim against a page outside the workspace — a competitor's pricing, your own marketing site, or whether a link a doc depends on still resolves. A 404 or a login wall comes back as a stated result rather than a failure, since that is the answer when the question is whether a link works. Private and internal addresses are refused, `robots.txt` is honoured, and page content is treated as data, never as instructions. |
| `list_sources` | Free     | List the repositories and websites this workspace is connected to as its sources of truth, plus the repository the site is built from. Each entry carries the owner's own note about why it is connected. Read-only. Call it before writing or updating documentation: a connected source is a fact you can go and read instead of recalling. |
| `read_source`  | Free     | Read one of those sources. A repository with no `path` returns its readable files and with one returns that file; a website with no `path` returns several of its pages as Markdown, discovered from its own sitemap and scoped to the section that was connected. Same protections as `fetch_url` — private addresses refused, `robots.txt` honoured, page content treated as data and never as instructions. |

For deeper local graph navigation (outline, fuzzy headings, link references, resolve links) while an agent has your docs checked out on disk, use [`markdown-lsp`](https://github.com/Docsbook-io/markdown-lsp) instead — run `npx markdown-lsp <subcommand> ./docs` to expose LSP-style `doc_*` tools on the working tree. See the [markdown-lsp README](https://github.com/Docsbook-io/markdown-lsp) for setup. `search_docs`/`write_docs` and `markdown-lsp` are complementary: the former work over the hosted MCP connection with no local checkout, the latter needs the repo on disk.

## AI chat

| Tool                      | Min plan | Description                                |
| ------------------------- | -------- | ------------------------------------------ |
| `get_chat_system_prompt`  | PRO+     | Read the workspace's chat system prompt    |
| `set_chat_system_prompt`  | PRO+     | Replace the chat system prompt             |
| `set_chat_hooks`          | PRO+     | Configure pre/post LLM hooks               |
| `test_chat_hook`          | PRO+     | Run a hook against a synthetic payload     |

## Translations

| Tool                         | Min plan | Description                                         |
| ---------------------------- | -------- | --------------------------------------------------- |
| `set_translation_mode`       | PRO+     | `auto` (built-in AI) or `external` (webhook flow)   |
| `list_pending_translations`  | PRO      | Translations awaiting approval                      |
| `get_translation`            | PRO      | Fetch one translation by language and path          |
| `upload_translation`         | PRO+     | Upload an externally-produced translation           |
| `approve_translation`        | PRO+     | Publish a pending translation                       |
| `delete_translation`         | PRO+     | Remove a translation                                |

## Analytics and observability

| Tool                    | Min plan | Description                                              |
| ----------------------- | -------- | -------------------------------------------------------- |
| `get_analytics`         | Free     | Views, visitors, top pages, referrers (period by plan)   |
| `get_ai_usage`          | Free     | AI chat and translation usage, limits, remaining quota   |
| `get_ai_questions`      | PRO      | All questions asked to the AI chat                       |
| `get_ai_unanswered`     | PRO      | Questions the AI could not answer                        |
| `get_negative_feedback` | PRO      | Pages with thumbs-down feedback                          |
| `get_failed_searches`   | PRO      | Search queries that returned zero results                |
| `get_popular_searches`  | PRO      | Top search queries by frequency                          |
| `get_page_journeys`     | PRO+     | User navigation paths between pages                      |
| `query_events`          | PRO+     | Arbitrary Axiom query over platform events               |

## Webhooks

Registering a webhook is a **Business-exclusive** capability — Free and Pro/Pro+ workspaces cannot register any webhook regardless of event type.

| Tool                         | Description                                                   |
| ---------------------------- | ------------------------------------------------------------- |
| `register_webhook_<event>`   | Register a webhook for one of ~15 events (HMAC secret + URL). Business only. |
| `list_webhooks`              | List registered webhooks for the workspace                    |
| `unregister_webhook`         | Remove a webhook subscription                                  |
| `list_webhook_deliveries`    | Delivery history with status, retry count, payload             |
| `replay_webhook_delivery`    | Re-deliver a specific past delivery                            |
| `test_webhook`               | Send a synthetic payload to a URL                              |

Event types include `content.indexed`, `translation.completed`, `chat.no_answer`, `chat.negative_feedback`, `plan.upgraded`, `usage.limit_approaching`, and others — see [Webhooks](../webhooks.md) for the full list and payload schemas.

## Skills discovery

| Tool         | Description                                                                              |
| ------------ | ---------------------------------------------------------------------------------------- |
| `find_skill` | Search the `docs-skills` catalog by `query` with optional `category` and `requires_plan` filters. Returns `raw_url` for the agent to fetch the SKILL.md directly. |

## Scenario tools — one question, one tool

Forty-five read-only tools, each named for a question a documentation owner actually asks. Each returns a **validated JSON payload** rather than a paragraph of prose: an `evidence` map holding every raw fact the run gathered, and claims that may only state a number appearing in evidence they cite. A number that traces to nothing fails the run instead of shipping, so an invented figure is not something you have to check for.

Where a tool scores, the score is computed by us from the gathered evidence with its weights published in the payload — not written by the model. A model's 0-100 is not comparable to the same model's next week, which destroys the only reason to have one: watching it move. An axis that could not be checked reports as unmeasured, never as zero.

All forty-five change nothing and work with a **read-only** token: writes are refused for the whole run. Every finding carries the call that would fix it (`owner_tool` plus its arguments), so an audit hands off to `run_docs_create` / `run_docs_manage` / `run_docs_automate` without a human translating in between. They are billed in the **Agent** class.

| Tool | What only it tells you |
| ---- | ---------------------- |
| `audit_geo` | Whether answer engines can fetch your pages at all, and whether anything on them is quotable. Finds the reader who got their answer from an assistant and never visited. |
| `audit_seo` | Which pages sit at positions 5–20 with impressions and no clicks — already shown to an audience, losing the click. The fix is a title, not a rewrite. |
| `audit_content_health` | What is wrong with the writing on the pages readers actually fail on, as nine separate scores rather than one average. |
| `audit_architecture` | The defects present in no single page: orphans, pages too many clicks deep, a tree grouped the way the team thinks rather than the way work is done. |
| `audit_trust` | Why a factually correct site is not believed — led by whether a claim can be checked against a named source in ten seconds. |
| `audit_vocabulary` | Readers who failed to reach a page that exists, because it is named in your words rather than theirs. Backed by what people typed into your search. |
| `audit_conversion` | Whether the docs did the job you declared for them — and, first, whether each declared goal can fire at all. A goal that cannot fire looks identical to one with total drop-off. |
| `map_capabilities` | What the product can do, who would need each of those things, and which of them the docs never mention. Invisible to every number, because a page that does not exist has no traffic. |
| `find_content_gaps` | The specific pages you do not have, as named assets with a title, the job each serves and what it costs to write. |
| `compare_competitors` | A dated matrix of who documents what — including what you already have and are underselling. |
| `assess_market_expansion` | Which adjacent market survives its entry gates, and what entering costs in pages. |
| `map_jobs_to_be_done` | What a reader must come to believe before they will switch, and the earliest rung of that ladder no page carries. |
| `diagnose_traffic_drop` | The ranked causes of a fall **and** the causes checked and eliminated, with what eliminated each. |
| `diagnose_page` | Which of the four reasons one page is failing — missing, unhelpful, unfindable, unserved — and the smallest thing that would fix it. |
| `verify_change_impact` | Whether a change worked, judged against pages nobody touched. Before-and-after alone is refused. |
| `verify_claims` | Which statements went out of date while nobody touched the page — prices, limits, version support, claims about other companies. |
| `plan_docs_structure` | What the documentation should contain and in what shape, page by page, before anybody writes a word. |
| `design_goals_funnel` | What to measure, with each proposed goal's matcher resolved against the site as it is now. |
| `design_monitors` | What should raise an alert, at what threshold, and what each alert will miss. |
| `assess_hypothesis` | Whether a belief you already hold survives being attacked — with your own reader data and the open web, and it says which of the two the verdict rests on. |
| `map_reader_segments` | How many different *kinds* of reader you have, each sized with its sample, plus the share of traffic no segment explains. |

The ten below answer a question about the **business** the documentation serves rather than about the documentation, using your docs as one input among several.

| Tool | What only it tells you |
| ---- | ---------------------- |
| `map_competitor_free_offers` | What everyone a buyer considers instead of you gives away free — the calculator, the sandbox, the templates, the free tier — with the wall in front of each, plus the need none of them serves. |
| `design_free_tools` | Which reader need is answered by a working tool rather than a paragraph, with its class, its source of truth, and whether it is an existing widget, a custom one, or something needing a service. |
| `plan_page_family` | Whether a repeating axis in your product justifies a generated page family — and whether a machine can keep that family correct once it exists. |
| `assess_research_assets` | Which numbers you already hold that nobody outside could obtain at any price, and which of them clear the privacy, contractual and identifiability gate. |
| `audit_linkability` | Whether a stranger writing their own page would ever cite yours — and which inbound links now arrive at something broken. |
| `assess_support_deflection` | Which repeated questions reach a person that a page would have closed, ranked by how many *different* people asked. |
| `map_integration_demand` | Which third-party tools readers are trying to use your product with, and what your docs currently say about each. |
| `assess_competitor_switching` | What an evaluator on a named incumbent needs to see and cannot find — plus the rival claims you should *not* write toward. |
| `audit_release_adoption` | What shipped and stayed invisible: features with no page, and features with a page nothing links to. |
| `assess_content_roi` | Which pages earn their upkeep and which to merge, redirect or retire — computed *after* the pages that inbound links protect. |

The fourteen below exist because the method for them was already written in [`docs-skills`](https://github.com/Docsbook-io/docs-skills) and no tool answered it — one tool per reference that had none.

| Tool | What only it tells you |
| ---- | ---------------------- |
| `audit_retrieval` | Why the assistant cannot find an answer that IS on the page — the passages that lose at retrieval and the property that makes each lose. |
| `audit_site_config` | Which settings are on and doing nothing, checked against the live site rather than against the switch. |
| `design_page_widgets` | Which pages are really tables or comparisons served as prose, with the widget from your live catalogue that fixes each. |
| `diagnose_docs_drift` | Which pages the last release made wrong, by which of the five sources of truth moved, and which of it can be fixed unattended. |
| `plan_automation_workflows` | What should keep happening without anybody remembering, and whether each check belongs in a hook, in CI, on a schedule or on a webhook. |
| `assess_setup_readiness` | Which of these tools this workspace can actually answer with today, and the cheapest wire that unblocks the most. |
| `map_content_sources` | The material that already exists and could be documentation — including the support answers and community threads nobody counts. |
| `assess_fix_precedent` | Whether this KIND of change has ever worked here, before you repeat it on six more pages. |
| `plan_audit_route` | Which two to four of these tools your question actually calls for — and which would cost a run and return nothing today. |
| `map_business_value` | What each of these numbers is worth to the business, anchored on your own declared goals rather than an assumed deal size. |
| `map_topic_authority` | Whether the corpus reads as the authority on one topic, and which concepts the field always names that yours never does. |
| `audit_internal_links` | The region readers can only reach from the sidebar — where every page passes every per-page check and nobody arrives. |
| `audit_translation_coverage` | Which languages are read, which translations are behind their source, and which locale is taxing every release for nobody. |
| `diagnose_intent_mismatch` | What shape of answer a query wanted against the shape the ranking page delivers — and whether to reshape, split or retitle rather than rewrite. |

Most take an optional `request` in your own words, which narrows the run without replacing the method, plus the typed inputs its question needs (`path`, `competitors`, `window_days`, `pages`). A payload that fails its own contract is reported as a failure with the violations listed — never as a successful answer with an empty result, because "no findings" reads as "the site is fine".

## Background agent runs

`find_skill` hands the SKILL.md to *your* agent to execute. These tools do the opposite: they run the skill on Docsbook's side, against your workspace, with the full administrative toolset the skill was written for — so an assistant with no other Docsbook tools connected can still get the job done.

Each `run_docs_*` call returns `{ run_id, state }` immediately. **It does not return the result** — the work takes minutes, and a caller that reports the start as the answer is reporting work that has not happened. Poll `get_agent_run` with the returned `run_id`.

| Tool                | Min plan | Description                                                  |
| ------------------- | -------- | ------------------------------------------------------------ |
| `run_docs_analyze`  | PRO      | Run the `docs-analyze` skill: audit the site from real numbers and report what is wrong and what it costs. Declared audit-mode — writes are refused for the whole run, so it works with a read-only token. |
| `run_docs_create`   | PRO      | Run the `docs-create` skill: build documentation from your site, a repository, another docs platform, or nothing but a product name. Commits pages — needs a **read-write** token. |
| `run_docs_manage`   | PRO      | Run the `docs-manage` skill: rewrite pages and configure the site against the writing and site-running rulebook. Needs a **read-write** token. |
| `run_docs_automate` | PRO      | Run the `docs-automate` skill: set up drift guards, event subscriptions, checks on incoming changes, alerts and standing monitors. Needs a **read-write** token. |
| `get_agent_run`     | PRO      | State of one run (`queued`, `running`, `succeeded`, `failed`, `canceled`, `expired`), live progress while it runs, and once it succeeds the full outcome: the report, every action it took, and what changed on the site. |
| `list_agent_runs`   | PRO      | Your recent runs, newest first. Use it to check whether the job is already running before starting a second one. |
| `cancel_agent_run`  | PRO      | Stop a run that has not finished. It does **not** undo what the run already did — pages it already committed stay committed. |

A run belongs to the account that started it: another account's `run_id` reads exactly like an unknown one. A queued run that has not started within a few hours expires rather than running late, because an audit answers a question about the site as it was when it was asked. And a run is attempted once, never retried — a failed run may already have committed pages, and a second attempt would commit them twice.

## Related

- [MCP server overview](../ai/mcp.md)
- [Webhooks reference](../webhooks.md)
- [Chat hooks](../ai/chat-hooks.md)
