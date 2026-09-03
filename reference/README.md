---
title: "Reference for the Docsbook MCP tools, API and webhooks"
description: "Where to find the exact tool names, endpoints, payload fields and event types for driving a Docsbook workspace from an agent, a script or your own backend."
---

# API & Tools Reference

Technical reference for developers integrating with Docsbook — programmatic control over workspaces, content, analytics, and automation. Three surfaces exist, and they are not interchangeable: MCP for agents, webhooks for being told when something happened, and the REST API for calling your docs chat from your own code.

## Pages

- [MCP tools reference](./mcp-tools.md) — every tool exposed by the Docsbook MCP server, grouped by category, with the billing class of each
- [Webhooks](../webhooks.md) — event catalog, payload schemas, HMAC signature format
- [API reference](../api.md) — the REST endpoint that answers a question against your own documentation
- [MCP server overview](../ai/mcp.md) — OAuth flow, connection setup, conceptual model

## Related

- [AI features](../ai/README.md)
- [Analytics & insights](../analytics/README.md) — the reports the analytics tools read
