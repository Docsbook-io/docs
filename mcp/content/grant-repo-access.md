---
title: "Grant repo access"
description: "grant_repo_access has been removed. Whether Docsbook can commit to a GitHub repository now surfaces from write_docs itself."
status: generated
version: "0.2"
---

# Grant repo access

`grant_repo_access` is no longer a callable tool on this MCP server. A call to it now returns "no tool named `grant_repo_access`" (checked live 2026-09-20); the Content family carries 14 tools today, not the 15 this page's own index used to list.

There is no separate advance check any more. Call [`write_docs`](./write-docs.md) directly: if the repository it publishes to is not reachable, the write itself is refused with `NO_GITHUB_ACCESS` rather than committed to, instead of a prior call telling you so first.
