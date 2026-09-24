Call Docsbook from your own backend with one API key and plain HTTPS — ask your docs a question, read them, change settings or hand work to the Docsbook agent.

## Get your key

Open **Settings ▸ Domain & API** in the panel to view, copy or reset the project's API key. Send it as `Authorization: Bearer dbk_…`.

There is one live key per project. Resetting it revokes the old key everywhere at once, so update your callers first — and keep the key on your server, never in a browser or mobile app.

## What the key reaches

- **`POST /api/v1/chat`** — a grounded answer from your docs, with sources: the same engine as the [AI chat](../ai-chat/README.md).
- **Reads** — `GET /api/v1/{tool}` for your projects, your pages, your agent jobs and Docsbook's own manual.
- **Settings** — `POST /api/v1/{tool}` for branding, navigation, site toggles, languages, translation mode, mention tracking, page status and the AI chat.
- **Everything else your MCP connection can call** — `POST /api/v1/tools/{tool}` with the tool's arguments as `args`, including `docsbook_agent` and `write_docs`. Each tool is described in the [MCP tools reference](../mcp-tools/README.md).

## What a call costs

`POST /api/v1/chat` spends from the project's balance, the same wallet the Ask AI widget on your site uses. Every other call costs the same flat price as the MCP tool it runs, shown on that tool's page.
