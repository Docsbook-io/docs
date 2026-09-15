Point an agent at your documentation and it can read it, write it, measure it and watch
it — over MCP, the protocol Claude, Cursor, Windsurf and VS Code already speak.

## Connect

```bash
claude mcp add --transport http docsbook https://docsbook.io/api/mcp/server
```

Authentication is OAuth 2.0 + PKCE: your client opens a browser once, you approve, and
the token is stored by the client. Nothing to paste.

Every tool below is also callable as a plain HTTP request, at the same price — each page
shows both forms, and the REST one comes with a form you can send from the page.

## Start with the expert

`docsbook_expert` is the first call to make for any documentation request, however
narrow, in any language. It is an **expert, not a runner**: one round trip returns how to
think about the request, the steps in order with the tool on each, what to carry between
them, what makes the answer wrong — and it runs none of it. `workspace_id` is optional,
because most of what it knows is true of documentation work rather than of one project.

## What a call costs

A flat price per call, decided by what serving it costs — reading a row, scanning the
event warehouse, leaving the network, running a model — and charged to your project's
balance. Each tool's page names its own price; the classes behind them are on the
[pricing page](https://docsbook.io/pricing). A call refused for an empty balance says so.

## READ and WRITE

The pill beside each tool in the sidebar says whether it only reads your project or can
change it. A handful of tools are marked **no token needed** — those are the ones your
own readers reach through the public endpoint on your published site.
