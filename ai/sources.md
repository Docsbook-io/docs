---
title: "Sources — What Your Documentation Reads From"
description: "Connect a repository or a website as a source of truth, and the Docsbook assistant and your own MCP agents read it themselves instead of guessing at prices, versions and behaviour."
---

# Sources

**Sources** are the repositories and websites your documentation is allowed to read from. Connect one, and asking the assistant to *update the documentation* or *resolve the drift* starts with it going and reading — instead of answering from what it happens to remember about your product.

Open the **Sources** section of your project's admin panel, directly under MCP and Prompts.

## Connecting one

There is one field. Paste a link, and Docsbook works out what it is:

| What you paste | What it becomes | What gets read |
|---|---|---|
| `github.com/acme/api` | Repository | Its files, on demand — README and docs first |
| `github.com/acme/api/tree/main/docs` | Repository folder | Only that subtree |
| `acme.com` or `acme.com/docs` | Website | Several of its pages, found from its own `sitemap.xml` |
| `acme.com/pricing.html` | Page | That one page |

A link pasted from an issue or a pull request connects the **repository**, not the issue. Tracking parameters (`?utm_source=…`) are dropped, so the same page pasted from a tweet and from your address bar is one source rather than two.

Two entries appear without you adding them, and neither can be removed here:

- **This site's repo** — the repository your documentation is built from.
- **From Branding** — the Site source URL, if your workspace set one. It still lives on the Branding card.

Each connected source can carry a short note about *why* it is connected. That note is not decoration: the assistant reads it as instruction.

## Live, paused, and what the green dot means

Every connected source shows a green dot and the word **LiveSync**.

> **That badge means the source is connected and your agents may read it. It is not a health check.** Nothing pings the host, and nothing checks the repository still exists — a status light that no code writes is worse than no light at all. The honest signal is **Last read**, shown on the row and written only when a tool actually fetched the source successfully.

**Pause** keeps a source in the list and stops anything reading it. **Remove** disconnects it. The two are different on purpose: "stop reading this for now" should not make you retype the address later.

## What reads them

**The assistant in your admin panel.** Its two tools, `list_sources` and `read_source`, are available on every turn rather than behind a lookup, and its instructions name your connected sources literally — a rule that says "check your sources" without naming them is one a model cannot follow.

**Your own MCP agents.** The same two tools are served over your project's MCP endpoint, so a source you register means the same thing in Claude Code or Cursor as it does here. See the [MCP server](./mcp.md) reference.

**Background runs.** Scheduled prompts and agent runs read them too, which is where it matters most: there is nobody sitting there to paste a link.

A repository read without a path lists its readable files; with one, it returns that file. A website read without a path returns several of its pages as Markdown, discovered from the site's own sitemap and scoped to the section you connected — connect `acme.com/docs` and the blog stays out of it. Sites with no sitemap return the entry page alone, and the result says so, so a thin read is never mistaken for a thin site.

## Which runs can actually read them

Not every tool reaches a source, so the panel says which do rather than implying they all can. Wherever a run is listed — the **Sources** column in the Prompts table, and the strip under an MCP tool's description — the chips are drawn in two states:

- **Lit** — this run fetches the source: your site's pages, your repository's files.
- **Unlit** — this run knows the source is connected and will not fetch it. Ask the assistant instead; it has no such limit.
- **Nothing at all** — this run reaches no source. A settings write has no business reading your repository, and a chip there would say otherwise.

## What it is for

Prices, plan names, limits, endpoints, version numbers and behaviour all change faster than documentation does. Without a source, an assistant asked about any of them either says it does not know or invents something plausible — and a plausible invention is the version that ships to your readers.

With one connected, that question has an address. The assistant reads your pricing page and corrects the three pages that quote the old tier; it reads the repository and finds the four things your quickstart claims that the code stopped doing.

## Related

- [MCP Server](./mcp.md) — the same two tools, for your own agents
- [AI Chat](./chat.md) — the assistant on your docs site
- [MCP tools reference](../reference/mcp-tools.md) — `list_sources` and `read_source` in full
