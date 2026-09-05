---
title: "Every tool the Docsbook MCP server exposes to an agent"
description: "The 309 tools a Docsbook workspace exposes over MCP — workspace setup, content, issues, chat, translations, analytics, webhooks, standing agents and background agent runs."
---

# MCP Tools Reference

This page lists every tool exposed by the Docsbook MCP server at `https://docsbook.io/api/mcp/server`. The server exposes **309 tools**. Each requires Bearer authentication via OAuth 2.0 + PKCE.

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
| `connect_source` | Write | Connect a repository, a website or a single page as a source of truth — what `list_sources` then lists, `read_source` reads, and an agent armed with `enable_agent` watches. A GitHub repository is proved readable (publicly, or with a GitHub authorization this project already holds) before it is stored; a private repository nobody has authorized yet is refused with the one thing that fixes it, rather than stored unreadable. `note` is the owner's own words about what the source is for, and is read as instruction by everything that later reads it. Requires a **read-write** token. |
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

## Action tools — one step of the work, one tool

135 read-only tools. Each is **one action on one subject**, not a whole discipline: `observe_link_graph` reports the edges between your pages, `decide_next_market` picks one market and says why not the others, `draft_comparison_page` writes the page. A caller picks a step, not a department.

The family is a cross of three axes, and every tool declares its position on all three:

- **The verb** decides the shape of the answer and what the run refuses.
- **The domain** decides the subject and the evidence it reads.
- **The outcome** — support load, organic traffic, AI citations, time to answer, conversion and eight more — is the number that tool is bought to move, and it is named in the tool's own description.

| Verb | Answers with | Refuses |
| ---- | ------------ | ------- |
| `observe_*` | What is there, with the source of every row | To recommend anything |
| `explain_*` | The mechanism behind it, not a correlation restated | A story it cannot point at a step of |
| `discover_*` | What is missing, named specifically enough to build | "More content about X" |
| `decide_*` | One choice, with every rejection and its reason | Returning a ranked list instead of a decision |
| `plan_*` | An ordered sequence whose first step is a call | Planning past the first thing that could invalidate it |
| `draft_*` | The artifact itself, ready to apply | Handing back a brief and calling it a draft |
| `measure_*` | A scorecard computed by us, comparable run to run | Writing a score, or filling a gap with a zero |
| `verify_*` | A verdict against a control, with "too early" allowed | Reaching for "confirmed" on a window too short |
| `learn_*` | A transferable rule and where it stops applying | A lesson with no boundary |
| `handoff_*` | The exact call, its arguments and the acceptance check | Work whose acceptance test it cannot state |

Each returns a **validated JSON payload** rather than a paragraph of prose: an `evidence` map holding every raw fact the run gathered, and claims that may only state a number appearing in evidence they cite. A number that traces to nothing fails the run instead of shipping, so an invented figure is not something you have to check for.

Where a tool scores — the fifteen `measure_*` tools, one per domain — the score is computed by us from the gathered evidence with its weights published in the payload, not written by the model. A model's 0-100 is not comparable to the same model's next week, which destroys the only reason to have one: watching it move. An axis that could not be checked reports as unmeasured, never as zero.

**All 135 change nothing** and work with a **read-only** token: writes are refused for the whole run. Every one of them bills in the **Agent** class. That includes `draft_*`, which produces the page or the block and names the call that would apply it (`run_docs_create` / `run_docs_manage`) rather than applying it itself. Every row carries that call, so an analysis hands off without a human translating in between.

**Each one is priced from the work it declares** — how many families of evidence it reads, how many model round trips it may take, whether it leaves your site, whether it emits an artifact — so a narrow observation costs a fraction of a deep draft rather than every action carrying one flat agent figure. The wait differs the same way, and the typical wait is listed per tool below. Each tool's current price is shown against it in the panel and on the [Docsbook pricing page](https://docsbook.io/pricing).

### Product & capability map

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_capability_inventory` | One row per capability your product actually exposes, beside the page that documents it — and the blank where no page exists. | ~41 s |
| `explain_capability_confusion` | The mechanism behind readers asking for something the product already does — the exact wording, placement or absence that makes an existing capability invisible. | ~45 s |
| `discover_undocumented_capabilities` | Capabilities that exist in the product and appear nowhere in the docs, each named specifically enough to write a page from tomorrow. | ~45 s |
| `decide_capability_priority` | One capability to document next, with every serious alternative listed and the reason each lost. | ~26 s |
| `plan_capability_page_set` | The set of pages one capability actually needs — and, as importantly, the pages it does not — in the order they should be written. | ~39 s |
| `draft_capability_matrix` | A finished capability matrix page — every capability, its state, its plan gate and its page link — in markdown ready to commit. | ~52 s |
| `measure_capability_coverage` | A repeatable scorecard of how much of the product the documentation actually covers, on five axes that are fixed by different people. | ~45 s |
| `verify_capability_claims` | For each capability the docs claim, a verdict on whether the product still does that — with the source that settles it. | ~52 s |
| `handoff_capability_backlog` | The capability work packaged for whoever runs it next: the exact call, its arguments, and how they will know it worked. | ~20 s |

### Jobs to be done

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_reader_jobs` | The jobs readers stated in their own words — from assistant questions and searches — grouped, counted, and quoted verbatim. | ~32 s |
| `explain_job_abandonment` | Where one job stops being completable, and the mechanism that stops it — the step, the missing prerequisite or the sentence readers hit before they leave. | ~42 s |
| `discover_unserved_jobs` | Jobs your product can serve and your documentation addresses nowhere — reasoned forward from capability to reader, because a job served nowhere leaves no trace to measure. | ~48 s |
| `decide_primary_job` | The one job this documentation should be organised around, with the rival jobs named and the cost of each rejection stated. | ~32 s |
| `plan_job_journey` | The ordered page sequence that carries one job from first contact to done, with the gaps in that sequence marked. | ~33 s |
| `draft_job_walkthrough` | The walkthrough page itself, written end to end for one job, with every prerequisite stated and every step verifiable. | ~55 s |
| `measure_job_completion` | A scorecard of whether readers with a job actually finish it — entry, continuation, dead ends, declared outcomes and returning. | ~39 s |
| `verify_job_now_served` | Whether the pages written for a job actually changed what readers do — before, after, window, control, verdict. | ~36 s |
| `learn_job_patterns` | The rule behind the jobs your docs serve well, stated so it transfers — and the boundary past which it stops holding. | ~32 s |

### Topical authority

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_topic_inventory` | Every topic this corpus covers, with how many pages carry it, how deep the deepest one goes, and how many pages link to it. | ~32 s |
| `explain_authority_shortfall` | Why this corpus reads as a site that mentions a topic rather than the site about it — with the specific absence that produces the impression. | ~39 s |
| `discover_missing_entities` | The entities a topic requires that this corpus never names — the concepts, tools, formats and failure modes a reader expects a real source to know about. | ~39 s |
| `decide_topic_cluster_focus` | The one topic cluster to build next, with the rivals named and the reason each was rejected. | ~32 s |
| `plan_topic_cluster` | The hub and its spokes: every page the cluster needs, what each one owns, how they link, and the order to write them in. | ~33 s |
| `draft_topic_hub_page` | The hub page itself, written: the definition, the map of the sub-topics, and the links that make the cluster a graph. | ~46 s |
| `measure_topical_depth` | A repeatable score for whether the corpus reads as an authority on its topics — definition, coverage, relations, evidence and connectedness. | ~36 s |
| `verify_cluster_effect` | Whether a cluster you built actually earned anything — rankings, arrivals or citations — against a control and a stated window. | ~36 s |
| `learn_authority_wins` | The rule behind the topics this site did win — what those pages had that the others did not, and where the rule stops applying. | ~32 s |

### Search intent

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_query_intents` | The queries this site is found by, sorted into the intent each one carries — how-to, definition, comparison, error, price, reference. | ~32 s |
| `explain_intent_mismatch` | Why a page that ranks loses the reader anyway — the specific gap between the shape of the question and the shape of the page. | ~36 s |
| `discover_intent_gaps` | Intents readers demonstrably arrive with that no page on this site is shaped to answer. | ~36 s |
| `decide_page_shape` | What ONE page must be — tutorial, how-to, reference, explanation or comparison — given the intents that actually reach it, with the rejected shapes named. | ~26 s |
| `plan_intent_coverage` | The ordered set of pages that would cover the intents this site attracts, each one shaped for exactly one of them. | ~30 s |
| `draft_intent_matched_opening` | The rewritten title, description and first screen of a page, matched to the intent it actually ranks for — written out, ready to apply. | ~39 s |
| `measure_intent_match` | A scorecard of how well the pages readers are shown match the intents they arrived with, on five axes computed from observations. | ~36 s |
| `verify_intent_fix` | Whether an intent-driven rewrite actually changed clicks or engagement — with a control and the search-data lag accounted for. | ~36 s |
| `handoff_intent_rewrites` | The intent rewrites packaged as calls: which page, what to change it to, and the query the change has to win. | ~20 s |

### Programmatic SEO

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_page_families` | The URL patterns on this site that already repeat over an axis, with how many members exist and how many the axis actually has. | ~26 s |
| `explain_thin_family_pages` | Why the generated members of a family underperform — the field that is empty, identical or invented across most of them. | ~36 s |
| `discover_scalable_patterns` | Repeating search patterns this product could answer at scale — the axis, the query template, and the unique fact each member would carry. | ~48 s |
| `decide_family_worth_building` | One verdict on whether a proposed family should be built, with the alternatives named and the kill condition stated up front. | ~30 s |
| `plan_family_rollout` | The rollout: which members ship first, what data feeds them, what the guardrails are, and where the checkpoint is. | ~42 s |
| `draft_family_template` | The template itself — the page skeleton, the per-member variables, and two fully rendered example members. | ~58 s |
| `measure_family_coverage` | A scorecard per family: how much of the axis is covered, how distinct the members are, how well they are linked, and how current their facts are. | ~32 s |
| `verify_family_indexation` | Whether the generated members are actually reachable and indexed — fetched live, with the ones that are not named individually. | ~45 s |
| `learn_family_thresholds` | The threshold, on this site, above which a generated member earns anything — stated as a rule with the cases behind it. | ~32 s |

### Free tools

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_tool_demand` | The requests readers already make that are shaped like a tool — calculate, convert, validate, generate, check — quoted and counted. | ~32 s |
| `explain_tool_underuse` | Why an existing free tool is not used — the entry point, the friction or the mismatch that stops readers reaching or finishing it. | ~45 s |
| `discover_tool_ideas` | Free tools this product could credibly host, each with the query it would answer and the data that makes it possible. | ~48 s |
| `decide_tool_to_build` | One tool to build, the rest rejected with reasons, and the maintenance cost of the chosen one stated before anybody starts. | ~39 s |
| `plan_tool_launch` | The launch: where the tool lives, what links to it, what it hands the reader afterwards, and how its success will be judged. | ~33 s |
| `draft_tool_page` | The tool's page, written: what it does above the fold, the worked example, the method it uses, and the next step — plus the embed spec for the widget itself. | ~58 s |
| `measure_tool_pull` | A scorecard of what a tool actually pulls in — arrivals, completion, onward movement, links earned and standalone readability. | ~32 s |
| `verify_tool_traffic` | Whether launching the tool changed anything measurable — against a control, over a stated window, with a verdict that can be "too early". | ~32 s |
| `handoff_tool_build` | The tool specified for whoever builds it: inputs, rules, outputs, edge cases, and the acceptance check it must pass. | ~29 s |

### Original research

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_own_data_assets` | The data this product already holds that nobody outside can compute — what it covers, how far back it goes, and whether it can be published at all. | ~41 s |
| `explain_research_ignored` | Why a published study earned no citations — the missing method, the unquotable format, or the absent claim somebody could have repeated. | ~48 s |
| `discover_research_questions` | Questions your own data could answer that nobody else can, each with the cut of data that would answer it and the audience that would repeat it. | ~45 s |
| `decide_research_to_publish` | One study to run, with the rejected questions named and the honest risk stated: what happens if the answer is boring. | ~30 s |
| `plan_research_release` | The release: the cut to run, the method to state, the artifacts to publish, and the cadence that makes it repeatable next year. | ~33 s |
| `draft_research_report` | The report itself: the headline claim in one quotable sentence, the numbers with their denominators, the method, and the limits. | ~68 s |
| `measure_research_citations` | A scorecard of how citable the published research actually is — quotable claim, stated method, reachable data, dating and machine readability. | ~45 s |
| `verify_research_claims` | Whether each published number still holds when the same cut is re-run — with the discrepancies named individually. | ~39 s |
| `learn_research_formats` | The rule behind which of your published pieces got repeated — the format, the claim shape or the release pattern — and where it stops applying. | ~39 s |

### GEO / AI search

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_assistant_answers` | What answer engines currently say about this product, and which source they used to say it — quoted, dated, and with the questions that produced it. | ~46 s |
| `explain_citation_absence` | Why this documentation is not the source an assistant cites — the specific property of the page that makes it unquotable. | ~48 s |
| `discover_quotable_atoms` | The self-contained passages this corpus should have and does not — one question, one complete answer, quotable without its neighbours. | ~39 s |
| `decide_geo_surface_priority` | Which machine surface to fix first — page shape, llms.txt, structured data, feeds or crawler access — with the rest ranked and rejected. | ~39 s |
| `plan_geo_surfaces` | The ordered work on machine surfaces, each step with the setting or the page it touches and the check that proves it landed. | ~39 s |
| `draft_answer_blocks` | The quotable passages themselves — question, complete answer, source and date — written to be lifted whole and still be correct. | ~55 s |
| `measure_ai_visibility` | A scorecard of how present this product is in answer engines — presence, accuracy, attribution, freshness and share of the questions covered. | ~48 s |
| `verify_citation_gain` | Whether GEO work changed what assistants say — the same questions asked before and after, with the answers compared verbatim. | ~45 s |
| `learn_citation_patterns` | The rule behind which of your pages get quoted — the shape, the position of the answer, the dating — with its boundary. | ~45 s |

### Competitors & market gaps

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_competitor_docs` | What a named competitor's documentation actually contains — sections, page types, what they document that you do not — fetched and dated. | ~46 s |
| `explain_switching_objections` | The specific objection an evaluator forms while reading both sets of docs — and the page and sentence of yours that forms it. | ~48 s |
| `discover_market_gaps` | Needs neither you nor the named competitors serve — with the evidence that somebody has the need and nobody answers it. | ~52 s |
| `decide_positioning_wedge` | The one comparison this product should invite, with the comparisons it should decline and the reason each was declined. | ~33 s |
| `plan_comparison_pages` | The set of comparison pages worth having, what each must contain to be credible, and the order to write them in. | ~39 s |
| `draft_comparison_page` | The comparison page itself, written from fetched evidence — every claim about the other side dated and sourced, including the ones where they win. | ~58 s |
| `measure_competitive_coverage` | A scorecard of how your documentation stands against named competitors on the surfaces evaluators actually open. | ~48 s |
| `verify_competitor_claims` | Whether the claims your pages make about competitors are still true today — each one re-fetched, with the stale ones named. | ~42 s |
| `learn_competitor_moves` | What changed on the competitors' side since the last look, and the pattern behind the changes — stated as what to watch next. | ~42 s |

### User language

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_reader_vocabulary` | The words readers actually type and ask, verbatim and counted, beside the word your documentation uses for the same thing. | ~29 s |
| `explain_term_misses` | Why a reader's word returns nothing — and which of the two very different causes it is: a concept named differently, or a concept absent entirely. | ~36 s |
| `discover_missing_synonyms` | The alternative names for concepts you already document that appear nowhere in the corpus — each with the page that should carry it. | ~32 s |
| `decide_canonical_terms` | One canonical name per concept, with the rejected names kept as synonyms rather than deleted, and the reason for each choice. | ~30 s |
| `plan_terminology_migration` | The ordered plan for rolling a naming decision through the corpus, including the pages that must not change and why. | ~30 s |
| `draft_glossary_entries` | The glossary entries themselves — each concept defined in one sentence a newcomer can use, with its synonyms and the page that owns it. | ~52 s |
| `measure_vocabulary_alignment` | A scorecard of how far the corpus's language is from its readers' — coverage of their terms, consistency of ours, and how much of it search resolves. | ~32 s |
| `verify_renaming_effect` | Whether adding the readers' words actually reduced the failures — the same searches before and after, with a control. | ~32 s |
| `handoff_term_changes` | The naming work packaged as calls: which page, which word becomes which, and the search that must stop failing afterwards. | ~20 s |

### Content architecture

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_corpus_shape` | The shape of the corpus as it is: sections, depth per branch, page sizes, and how much of it the declared navigation actually reaches. | ~26 s |
| `explain_navigation_failure` | Why readers cannot find things — the specific mismatch between the tree you declared and the routes readers actually walk. | ~42 s |
| `discover_orphan_pages` | Pages nothing links to and pages readers reach and cannot leave — the two ends of the corpus that are invisible from inside the tree. | ~32 s |
| `decide_structure_model` | The organising principle this corpus should use — by job, by product area, by page type, or by audience — with the rejected models and their costs. | ~36 s |
| `plan_restructure` | The move list: which page goes where, in what order, with every URL change and the redirect it requires stated as its own line. | ~39 s |
| `draft_navigation_tree` | The navigation itself, written out — the full tree with labels in the reader's words, ready to apply. | ~42 s |
| `measure_findability` | A scorecard of whether a reader can get from where they land to what they need — reachability, depth balance, orientation, entry points and search fallback. | ~39 s |
| `verify_restructure_effect` | Whether a restructure helped — the same findability and behaviour measures before and after, with redirects checked and a control section. | ~45 s |
| `learn_structure_lessons` | The rule behind the sections of this corpus that work — how they are grouped, how deep they go, how they open — and where it stops applying. | ~32 s |

### Internal linking

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_link_graph` | The corpus as a graph: which pages link to which, how many edges each has in and out, and which pages the graph treats as hubs. | ~29 s |
| `explain_unreachable_pages` | Why a page is unreachable in practice — the missing edge, the link nobody follows, or the anchor text that gives no reason to click. | ~36 s |
| `discover_missing_links` | Pairs of pages that discuss the same entity and do not link to each other — each with the sentence where the link belongs. | ~39 s |
| `decide_hub_pages` | Which pages become hubs — the ones everything else points at — with the candidates that were rejected and why. | ~30 s |
| `plan_linking_pass` | The linking pass: which pages get edited, in what order, how many links each gains, and the rule that stops it becoming link spam. | ~30 s |
| `draft_link_insertions` | The exact edits: for each page, the sentence as it will read after the link is inserted, with the anchor text and the target. | ~46 s |
| `measure_graph_health` | A scorecard of the link graph — connectedness, hub concentration, cluster crossing, anchor quality and how many pages depend on navigation alone. | ~36 s |
| `verify_link_effect` | Whether an internal linking pass changed anything — arrivals to the linked pages, dead-end rate, and rankings, against a control. | ~36 s |
| `handoff_link_edits` | The link edits packaged per page as calls, with the acceptance check stated as an arrival or an inbound count. | ~20 s |

### Trust (E-E-A-T)

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_trust_signals` | What credibility material the pages actually carry — authors, dates, sources, numbers with denominators, worked examples, stated limits — page by page. | ~32 s |
| `explain_disbelief` | Why a reader does not believe a page that is factually correct — the unsourced number, the unstated limit, or the claim only you make. | ~45 s |
| `discover_unsourced_claims` | Every claim on the commercially important pages that carries no source, no denominator and no date — listed individually. | ~35 s |
| `decide_evidence_standard` | The proof each class of claim must carry before it may be published — decided once, with the rejected standards and their costs. | ~29 s |
| `plan_trust_upgrade` | The ordered work that brings the pages up to the evidence standard, starting with the pages trust is actually spent on. | ~30 s |
| `draft_evidence_blocks` | The rewritten claims themselves — each with its source, its denominator, its date, and the limitation stated beside it. | ~55 s |
| `measure_trust` | A scorecard of believability on five axes — verifiability first, because it is the one a competitor cannot copy in an afternoon. | ~45 s |
| `verify_claim_freshness` | Whether each dated or numeric claim is still true today — re-checked against its source, with the stale ones named individually. | ~48 s |
| `learn_trust_objections` | The recurring objection pattern across everything readers doubted — stated as a rule about what this audience needs proved. | ~32 s |

### Backlinks & digital PR

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_inbound_mentions` | Who currently references this product in public, what they say, and whether the reference is a link, a mention or a quotation. | ~42 s |
| `explain_unlinkable_pages` | Why nobody links to a page — what it lacks that a person writing about this subject would have needed. | ~45 s |
| `discover_link_targets` | Specific places that would plausibly reference this product — each with the page they would link to and the reason they would bother. | ~51 s |
| `decide_linkable_asset` | The one asset to build for references — data, tool, definition or argument — with the rejected options and why they lose. | ~39 s |
| `plan_outreach_sequence` | The outreach plan as ordered rows: who is approached, in what order, with what, and the stopping condition. | ~42 s |
| `draft_outreach_pitch` | The message itself, written per target — what of theirs it refers to, what it offers, and the one thing it asks. | ~51 s |
| `measure_linkability` | A scorecard of how referenceable this corpus is — unique facts, addressable sections, citable format, freshness and permanence of URLs. | ~45 s |
| `verify_mention_gain` | Whether new references actually appeared after the work — searched again, compared against the earlier set, with referral traffic beside it. | ~42 s |
| `handoff_pr_targets` | The outreach packaged for a person: target, their page, the drafted message, the ask, and what a reply means. | ~33 s |

### Market expansion

| Tool | What only it tells you | Typical wait |
| ---- | ---------------------- | ------------ |
| `observe_audience_origins` | Where readers already come from — countries, languages, referrers — and how differently each group behaves once here. | ~32 s |
| `explain_market_stall` | Why a market that arrives does not convert — the language, the example, the pricing assumption or the missing proof that stops it. | ~42 s |
| `discover_adjacent_markets` | Audiences this product could serve that it does not reach at all — each with the evidence the need exists and the gate that would have to be passed. | ~48 s |
| `decide_next_market` | One market to enter next, with the rest rejected, and the ongoing cost of the choice stated before anybody commits. | ~36 s |
| `plan_market_entry` | The entry plan: which pages come first, what must be localised beyond language, and the checkpoint that decides whether to continue. | ~33 s |
| `draft_market_landing` | The market's landing page, written in its language with its examples, its currency and the proof that market asks for. | ~46 s |
| `measure_market_readiness` | A scorecard of whether the documentation is ready for a market — coverage, localisation beyond language, proof, discoverability and upkeep. | ~36 s |
| `verify_market_traction` | Whether entering the market changed anything — arrivals, outcomes and returns from that market, against a control and a stated window. | ~36 s |
| `learn_expansion_lessons` | The rule behind the markets that worked here — what was done for them that was not done for the others — with its boundary. | ~32 s |

Most take an optional `request` in your own words, which narrows the run without replacing the method, plus the typed inputs its question needs (`path`, `path_prefix`, `pages`, `competitors`, `window_days`). A payload that fails its own contract is reported as a failure with the violations listed — never as a successful answer with an empty result, because "no findings" reads as "the site is fine".

### Collectors — the evidence, without the reading of it

Five tools sit under the family in a cheaper billing class of their own, **Probe**: `collect_page_text`, `collect_corpus_map`, `collect_assistant_questions`, `collect_traffic` and `collect_onsite_search`. They hand back the normalised rows an action would have read, plus a `reproduce` block naming the exact calls behind every row — no model in the path, so there is nothing in them to disbelieve. Buy one when you want the numbers before deciding whether to buy the reading of them. `audit_geo` also survives from the previous generation: its evidence layer is code rather than a model, and it answers whether answer engines can fetch your pages at all.

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

## Standing agents

The tools above run once, on request. These two arm a standing route that runs on its own — on a schedule, on an event this workspace emits, or on new commits to a connected repository — the same catalog the admin panel's Agents tab shows and arms.

| Tool | Billing | Description |
|---|---|---|
| `find_agent` | Read | Search the catalog of routes this workspace can arm by the outcome you want ("keep the docs in step with the repo", "translate", "watch traffic"). Each result carries `state` — whether this workspace already has it armed, and on what — so you can tell "nothing is watching the repo" from "armed, and failing since Tuesday." Call it before proposing to set something up by hand: the route usually exists already. |
| `enable_agent` | Write | Arm (or disarm) one agent from `find_agent`'s catalog by its `agent_key`. What wakes it is exactly one of `schedule` (a cron expression, hourly at the fastest), `on_event` (something this workspace emits), or `watch_source_id` (a connected GitHub repository from `list_sources`/`connect_source` — the agent runs on the commits pushed to it). Arming on a repository records its current commit, so the first run is on the next push, not a replay of its whole history. `enabled: false` disarms it without forgetting how it was configured. Requires a **read-write** token. |

## Related

- [MCP server overview](../agent-ready/mcp.md) — connecting a client, the OAuth flow, and what the tools are for
- [Webhooks reference](./webhooks.md) — the 18 typed events and their payload schemas
- [API reference](./api.md) — the REST endpoint for asking your documentation a question
- [Chat hooks](../ai-chat/chat-hooks.md) — what `set_chat_hooks` configures
- [Analytics & insights](../analytics/README.md) — the reports the analytics tools read
