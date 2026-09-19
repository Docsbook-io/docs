Point an agent at your documentation and it can read it, write it, measure it and watch
it — over MCP, the protocol Claude, Cursor, Windsurf and VS Code already speak.

## Connect

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

Authentication is OAuth 2.0 + PKCE: your client opens a browser once, you approve, and
the token is stored by the client. Nothing to paste.

## Two surfaces, one endpoint

Since 2026-09-18 your own connected agent and this catalog are not the same thing.

**Your token** — the one your editor holds after the OAuth step above — meets a small,
fixed surface: orientation (`get_info`, `list_workspaces`, `get_workspace`), reading your
own documentation and Docsbook's own docs, creating a project, and the five tools that
give a job to **`docsbook_agent`** and watch it. That is the whole of "manage the
documentation" from your own agent now. A handful of the tools below are also reachable
without a token at all — those are the ones your own readers reach through the public
endpoint on your published site.

**Everything else on this page** — writing documentation, translations, webhooks,
analytics beyond your own project's summary, the product's own accumulated memory — is
performed by `docsbook_agent`, the background worker Docsbook runs on your behalf. You do
not call `write_docs` yourself any more; you describe the job to `docsbook_agent`
("restructure the getting-started section around three personas"), it plans, does the
work, and reports back what it did. This page still documents every one of those tools in
full, because knowing what `docsbook_agent` *can* do is exactly how you know what to ask
it for — read them as its capability list, not as a menu your own token can dial directly.

A narrow additional slice of pure configuration (branding, navigation, the chatbot,
translation mode, mention tracking) is reachable directly by your **workspace API key**
over REST, even though it is not on your MCP token's surface — see the API Reference
section for that list and why it stops where it does.

## Start with the agent

`docsbook_agent` is the first call to make for any documentation request, however narrow,
in any language: describe the outcome, not the steps. `docsbook_agent_status` and
`docsbook_agent_tasks` watch it, `docsbook_agent_reply` answers a question it asks
mid-run, `docsbook_agent_stop` cancels it. `workspace_id` is required on all five.

## What a call costs

A flat price per call, decided by what serving it costs — reading a row, scanning the
event warehouse, leaving the network, running a model — and charged to your project's
balance. Each tool's page names its own price; the classes behind them are on the
[pricing page](https://docsbook.io/pricing). A call refused for an empty balance says so.

## READ and WRITE

The pill beside each tool in the sidebar says whether it only reads a project or can
change it. A handful of tools are marked **no token needed** — those are the ones your
own readers reach through the public endpoint on your published site.
