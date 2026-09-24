Call Docsbook from your own backend with one API key and plain HTTPS. Everything your MCP connection can do has its own endpoint here: projects, your pages, site settings, languages and translations, goals, webhook alerts, the agent's memory, `docsbook_agent` — and the AI chat that answers from your docs.

## Get your key

Open **Settings ▸ Domain & API** in the panel to view, copy or reset the project's API key. Send it as `Authorization: Bearer dbk_…`.

There is one live key per project. Resetting it revokes the old key everywhere at once, so update your callers first — and keep the key on your server, never in a browser or mobile app: it can change your site.

## How the endpoints are shaped

- **Reads** — `GET /api/v1/{tool}`, arguments in the query string: `GET /api/v1/search_project_docs?query=custom%20domain`.
- **Changes** — `POST /api/v1/{tool}`, arguments as the JSON body: `POST /api/v1/update_branding` with `{"accent_color": "#0f766e"}`.
- **Ask your docs** — `POST /api/v1/chat`, a grounded answer with sources: the same engine as the [AI chat](../ai-chat/README.md).
- **By name** — `POST /api/v1/tools/{tool}` with `{"args": {…}}`, for a caller that holds the tool name in a variable.

The project is taken from the key, so there is no workspace to name. Every endpoint answers `{ "ok": true, "result": … }`; a tool that ran and refused (a bad argument, an empty balance) answers `200` with `ok: false` and its reason.

## What a call costs

Each call is charged to your balance at **twice what serving it costs us** — the price is on every endpoint's page, and it is the same price as the MCP tool it runs. For most endpoints that is a few cents per thousand calls; discovery calls are free. Model tokens are billed at twice the provider's price, and an endpoint that calls a paid data vendor adds twice the vendor's price. `POST /api/v1/chat` is billed by its tokens only. See [pricing](../pricing/plans.md).
