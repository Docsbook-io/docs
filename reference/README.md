---
title: "Reference for the Docsbook MCP tools, API and webhooks"
description: "Where to find the exact tool names, endpoints, payload fields and event types for driving a Docsbook workspace from an agent, a script or your own backend."
---

# API & Tools Reference

Technical reference for developers integrating with Docsbook — programmatic control over workspaces, content, analytics, and automation. Three surfaces exist, and they are not interchangeable: MCP for agents, webhooks for being told when something happened, and the REST API for calling Docsbook from your own backend.

The API and MCP sections are generated from the running server — the OpenAPI document at [docsbook.io/openapi.json](https://docsbook.io/openapi.json) and the live tool catalog — so every call listed is a call that exists, with the arguments it actually takes.

## Pages

- [MCP tools](../mcp/README.md) — every tool on the Docsbook MCP server, one page each: its arguments, the JSON-RPC envelope a client sends, the REST equivalent you can try from the page, and what the call costs
- [API reference](../rest-api/README.md) — the REST surface: ask your documentation a question, or dispatch any tool by name
- [Webhooks](./webhooks.md) — event catalog, payload schemas, HMAC signature format
- [MCP server overview](../agent-ready/mcp.md) — OAuth flow, connection setup, conceptual model

## Related

- [Get cited by AI and found by search](../seo/README.md)
- [Answer readers with AI chat](../ai-chat/README.md)
- [Analytics & insights](../analytics/README.md) — the reports the analytics tools read
