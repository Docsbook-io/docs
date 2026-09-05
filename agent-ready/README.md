---
title: "Agent-ready docs: documentation an AI agent can act on"
description: "Four machine surfaces over one documentation set — a SKILL.md catalog, an MCP server, a document graph and llms.txt — and what each one buys an agent."
tldr: "Docsbook publishes your documentation four ways a machine can consume it: SKILL.md files that teach an agent the method, an MCP server that gives it 310 typed tools, a document graph it can navigate by heading and link, and llms.txt for agents with no connection at all."
---

# Agent-ready content

A documentation site built only for people is a wall of HTML to everything else. An agent arriving at it has to guess which page matters, scrape prose for facts, and has no way to act on what it read. Docsbook publishes the same documentation through four surfaces a machine consumes directly — so an agent can find the method, read the corpus, navigate its structure, and change it.

The four are not alternatives. They answer four different questions an agent asks in sequence: *how is this job done*, *what can I call*, *where does this live*, and *what exists at all*.

<!-- widget:cards -->

- [Docs Skills](./skills.md) — the SKILL.md catalog: four orchestrator skills that teach any agent how documentation work is actually done, plus how they are discovered, versioned and run
- [MCP Server](./mcp.md) — 310 typed tools over the Model Context Protocol: read pages, commit them, read analytics, change settings, start agent runs
- [Source of Truth](./source-of-truth.md) — the document graph: pages, headings, links and anchors as nodes and edges an agent can traverse instead of grepping
- [MCP security](./mcp-security.md) — the authentication model, token scopes, what the server stores, and the compliance gaps stated plainly
- [llms.txt](../geo/llms-txt.md) — the machine-readable index of the published site, for an agent with no token and no checkout

<!-- /widget -->

## What each surface buys

| Surface | The agent's question | What it gets | What it costs |
|---|---|---|---|
| SKILL.md catalog | "How is this job done properly?" | A workflow with guardrails, ordered steps and acceptance criteria, fetched from GitHub | Nothing — the catalog is public and `find_skill` is never metered |
| MCP server | "What can I call, on which project?" | 310 tools, an `instructions` block at connect time, structured errors that name the next move | Metered per call against the project's balance; discovery calls are free |
| Document graph | "Where does this concept live, and what links to it?" | Pages and headings as separate node namespaces, four kinds of edge, broken links and anchor collisions | Free on every plan — it is built from your own markdown |
| llms.txt | "What exists on this site at all?" | A flat, fetchable index of every published page, with no auth | Free, and readable without a Docsbook account |

## How the surfaces hand off to each other

The handoffs are the design, not a coincidence.

- **A skill names a need, the MCP server answers it.** Docsbook's skills state what evidence a step requires ("read the numbers before reading a page") and let the model pick the tool. That is deliberate: a skill that hard-codes tool names breaks the moment a tool is renamed, and the failure is silent — the agent picks something adjacent and improvises a different method behind an identical-looking report.
- **The MCP server can run the skill for you.** `run_docs_analyze`, `run_docs_create`, `run_docs_manage` and `run_docs_automate` execute one of the four orchestrator skills on Docsbook's machines against your workspace, and return a run id rather than a result.
- **The graph is what the content tools read.** `search_docs`, `read_doc` and `get_doc_outline` do not grep files; they query a `RichDocGraph` built from your repository's markdown and cached server-side.
- **llms.txt is the fallback for an agent with neither.** No token, no checkout, no MCP client — just an HTTP GET over the published site.

## Why this is the right way (evidence)

| Rule | Why it works on the machine that consumes it | Source |
|---|---|---|
| Publish the method as a file the agent loads on demand, not as prose in a system prompt | Anthropic's Agent Skills design loads a skill in stages — "until a Skill is triggered, only its name and description occupy context" | [Agent Skills overview](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) |
| Keep the tool surface typed and named, not a single "do documentation" endpoint | MCP tools are "designed to be **model-controlled**", discovered and invoked by the model from `tools/list` | [MCP spec 2026-07-28, Tools](https://modelcontextprotocol.io/specification/2026-07-28/server/tools) |
| Do not load everything into the context window at once | "Context, therefore, must be treated as a finite resource with diminishing marginal returns" | [Effective context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) |
| Give a large catalog structure a model can search rather than a flat list | Anthropic measures that "Claude's ability to pick the right tool degrades once you exceed 30–50 available tools" | [Tool search tool](https://platform.claude.com/docs/en/agents-and-tools/tool-use/tool-search-tool) |
| Give retrieval a graph, not a bag of pages | Long-context retrieval degrades in the middle: performance "significantly degrades when models must access relevant information in the middle of long contexts" (Liu et al., TACL 2024) | [Lost in the Middle](https://aclanthology.org/2024.tacl-1.9/) |

Two of these deserve their measured form rather than a slogan. Retrieval over a large tool registry has been benchmarked independently: RAG-MCP (arXiv preprint 2505.03275, Gan and Sun, May 2025) reports tool-selection accuracy of "43.13% vs 13.62% baseline" when tools are retrieved instead of all listed, cutting prompt tokens "by over 50%". A 2026 preprint benchmarking registries "ranging from 20 to 3,251 tools" reports 93.1% against 87.1% selection accuracy for adaptive shortlisting over a fixed five-tool shortlist (arXiv 2605.24660). Both are unrefereed preprints; treat the direction as well supported and the exact figures as one team's measurement.

## Limits and open questions

- **The four surfaces do not all cost the same.** The skills catalog, the graph and llms.txt are free on every plan. MCP tool calls are metered per call against the project's balance, and the two capabilities that spend Docsbook's model budget — agent runs (`run_docs_*`, `agent_*`) and the reader-facing AI chat — start at Pro. Current amounts are on the [pricing page](https://docsbook.io/pricing); this documentation deliberately quotes none, because a price copied into a page goes stale silently.
- **"Agent-ready" is a shape claim, not a ranking claim.** Docsbook can show you that a page is fetchable, that its sections stand alone and that its anchors resolve. Whether any particular assistant then cites it is not something this product measures for you, and no public source establishes a general rate. See [GEO](../geo/README.md) for what is measurable.
- **The tool count moves.** 310 is the number of tool names this build registers. The authoritative count is whatever `tools/list` returns for your token, which the MCP section of your admin panel reads live rather than from a written-down copy.
- **The MCP specification moved under us.** Revision `2026-07-28` made MCP stateless and removed the `initialize` handshake entirely — "There is no negotiation handshake" ([Versioning and Compatibility](https://modelcontextprotocol.io/specification/2026-07-28/basic/lifecycle)). Docsbook's server is served over a stateless HTTP transport but still speaks the initialization-based revisions its SDK supports — latest `2025-11-25` — and carries its orientation text in `initialize`, which is a pre-`2026-07-28` placement. A client that speaks only `2026-07-28` will not connect. See [MCP server security](./mcp-security.md) for the rest of the gap list.
- **No surface here is a substitute for the docs being right.** An agent that can navigate a corpus perfectly still reports what the corpus says.

## Related

- [GEO](../geo/README.md) — being quoted by an assistant that never connects to anything
- [llms.txt](../geo/llms-txt.md) — the fourth surface, documented with the SEO and GEO family
- [MCP tools reference](../reference/mcp-tools.md) — every tool with its parameters and billing class
- [Webhooks](../reference/webhooks.md) — the push half: being told when something happened, rather than asking
- [AI Chat](../ai-chat/README.md) — the assistant your readers talk to, which reads the same graph
