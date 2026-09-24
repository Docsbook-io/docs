---
title: "MCP server for your docs: let readers' AI agents query them"
description: "Every public Docsbook site is an anonymous, read-only MCP server. Readers connect Claude Code, Cursor, VS Code or Codex and search your current docs by meaning."
---

# MCP server for your docs

Every public Docsbook site is also an MCP server: your readers connect it to Claude Code, Cursor, VS Code or Codex, and their agent searches and quotes your current pages instead of guessing — no account, no token, read-only.

## Where is it?

Each project serves its own endpoint:

```text
https://docsbook.io/<owner>/<repo>/api/mcp/server
```

With a [custom domain](../site/custom-domain.md) connected, the same server also answers at `https://<your-domain>/api/mcp/server`. The **Public MCP server** card in **Settings ▸ Domain & API** shows your exact address and a Claude Code command to copy.

## What can a reader's agent do with it?

The server and its main tools carry your project's name, so an agent knows whose docs it is reading before its first call. The name is your repository's, in lowercase, with each run of other characters turned into one `_`: `acme/api-docs` serves a server called `api_docs-docs`.

| Tool | What it does |
|---|---|
| `search_<slug>_docs` | Finds the pages that answer a question, by meaning — or by exact words while [search by meaning](./README.md#how-fresh-is-the-brain) is off |
| `read_<slug>_doc` | Reads one page in full, so the agent quotes it instead of inferring it from a title |
| `get_<slug>_doc_outline` | Lists every page, for "what do these docs cover" |
| `docsbook_agent_activity` | Shows what the Docsbook agent recently did on these docs: pages read and written, translations run |
| `find_skill` | Returns the [skills](./skills.md) you placed on this door, then Docsbook's public skills catalog |
| `get_info` | Says which product the server is for and how to connect it |
| `find_widget`, `list_content_widgets` | Describe the widgets a Docsbook page or chat can show |
| `search_docsbook_docs`, `read_docsbook_doc`, `list_docsbook_docs` | Read Docsbook's own manual |

Agents that learned the older names `search`, `read_doc` and `get_doc_outline` still reach the same tools.

## Connect it

Replace the address with your own; the server name is the label the client shows.

<!-- widget:code-group -->

### Claude Code

```bash
claude mcp add --transport http api_docs-docs https://docsbook.io/acme/api-docs/api/mcp/server
```

### Cursor

```json
{
  "mcpServers": {
    "api_docs-docs": {
      "url": "https://docsbook.io/acme/api-docs/api/mcp/server"
    }
  }
}
```

### VS Code

```json
{
  "servers": {
    "api_docs-docs": {
      "type": "http",
      "url": "https://docsbook.io/acme/api-docs/api/mcp/server"
    }
  }
}
```

### Codex

```toml
[mcp_servers.api_docs-docs]
url = "https://docsbook.io/acme/api-docs/api/mcp/server"
```

<!-- /widget -->

Cursor reads `~/.cursor/mcp.json` or `.cursor/mcp.json`, VS Code reads `.vscode/mcp.json`, and Codex reads `~/.codex/config.toml`. The agent then has your docs as tools, with nothing to sign in to.

## What readers see on your pages

The **Copy page** menu on every page carries two ways in, both on by default:

- **Connect MCP** — copies a prompt that installs your server in whatever agent the reader uses, and tells the agent to search first and read the page before relying on it.
- **Connect to VSCode** — installs the server in VS Code with one click.

Hide either one with the toggles on the **Copy page menu** card in **Customize ▸ Content**.

<!-- widget:callout type=note -->

This is your readers' server. **Your own** connection is `https://docsbook.io/api/mcp/server`: signed in, it reaches your projects' settings and hands work to the Docsbook agent — see [Tell your agent, get discovered](../get-discovered.md).

<!-- /widget -->

## What stays private

The server reads your published pages, plus any skills you choose to place on it:

- **Nothing writes.** No tool changes a page, a setting or a source.
- **Nothing behind the site is read** — not your analytics, settings, sources or the agent's [memory](./memory.md).
- **A private site stays private.** The endpoint still answers, but every tool that reads your pages refuses with `PRIVATE_DOCS`.

## FAQ

**Does a reader's agent cost me anything?** Calls are not billed one by one. With search by meaning on, each question is embedded on your balance; if that balance is empty, `search_<slug>_docs` answers `INSUFFICIENT_BALANCE` while reading pages keeps working.

**Can I switch the server off?** There is no switch for the endpoint itself — it serves the same pages your public site does. You can hide **Connect MCP** and **Connect to VSCode**, or make the site [private](../site/private-docs.md).

**How is this different from llms.txt?** `llms.txt` is an index an AI reads to find your pages; the MCP server lets an agent search and read them while it works. See [llms.txt and Markdown for AI](../geo/llms-txt.md).

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Skills](./skills.md) — Put your house rules in front of readers' agents {sparkles}
- [Custom domain](../site/custom-domain.md) — Serve the docs, and this server, from your own domain {globe}
- [Tell your agent, get discovered](../get-discovered.md) — Connect your own agent to Docsbook {terminal}
- [A second brain for your product](./README.md) — Everything this server answers from {network}

<!-- /widget -->
