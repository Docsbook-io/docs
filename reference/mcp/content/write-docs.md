---
title: "Write docs"
description: "Write, delete, move and rename markdown documentation files — this is how a site gets its pages and how its structure is changed, including a site just created from scratch by…"
---

# Write docs

<!-- widget:mcp access=write -->

## write_docs

Write, delete, move and rename markdown documentation files — this is how a site gets its pages and how its structure is changed, including a site just created from scratch by create_workspace. EVERYTHING in one call lands in ONE atomic git commit: batch a restructure (the moves, the deletions, and the pages whose links they change) into a single call rather than calling this repeatedly — a rename split across two commits leaves the published site with a broken link in between. `files` writes whole files. `operations` says what a content array cannot: {op:'delete', path, redirect_to?} removes a page, {op:'move', from, to, content?} renames or relocates one (its body carries over untouched unless you pass `content`; naming a directory moves every page under it). Operations are applied before `files`, so writing a page at a path you just moved away from leaves a stub behind rather than cancelling the move. Every move — and every delete that names `redirect_to` — is recorded in the site's redirect map in the same commit, so the old URL keeps working instead of 404-ing every external link to it. Publishes to the Docsbook-hosted repository using Docsbook's own GitHub credentials, so the user needs no GitHub access; the repository is created on the first write if it does not exist yet. A site served from a repository in the user's OWN GitHub account is refused (NO_GITHUB_ACCESS) rather than committed to hosting the site does not read — the refusal names the routes that can write it. The result carries `site_url` — report that link, do not construct one. It also carries `widget_review`: a read of the markdown you just wrote, naming any widget marker that will NOT render (unclosed, misspelled, nested, switched off) and any region that has the shape of a content widget and was left as plain markdown — a stacked set of snippets in three languages, a bare list of links closing the page, numbered step headings, a bolded `Note:`. Act on the ones that fit the page with a follow-up call; `list_content_widgets` has each widget's full contract. REQUIRES a read-write MCP token — a read-only token gets a READ_ONLY_TOKEN error. BEFORE WRITING, call `docsbook_expert` with what you are trying to achieve: it answers what this page has to do, what to read before touching it, and what would make the result wrong — and it will tell you when the evidence is too thin to write from yet. One call, cheapest on the server, changes nothing.

| Field | Type | Required | Description |
|---|---|---|---|
| `workspace_id` | string | no | Workspace ID (optional when MCP endpoint is auto-scoped). Numeric workspace id — OR the project as the user names it: 'owner/repo', the repo name alone, the site's display name, its docs URL or custom domain. Text is resolved server-side; an ambiguous name returns the candidates instead of guessing, so pass what the user said rather than calling list_workspaces first. |
| `files` | object[] | no | Files to write in full. Committed together with `operations` as a single commit. Optional only when `operations` is given. |
| `operations` | string[] | no | Structural changes — deletes, moves and renames — applied in the same commit as `files`, in the order given. |
| `message` | string | no | Commit message (default: 'docs: update via Docsbook MCP'). |
| `intent` | string | no | What the person asked for, in their own words — the goal behind this edit, not a summary of the diff. Shown on the change in the Changes panel so the owner can later see what the edit was for and judge whether it worked. Pass the user's original request verbatim when you have it. |
| `closes_issues` | integer[] | no | The issue numbers this change finishes. Written into the pull request body as `Closes #N`, so merging it closes the work — on GitHub as well as here — and the board folds the change into that issue's card instead of drawing it as unattached work. Pass them even when the review mode merges immediately: the record is what makes the change readable in six weeks. |
| `hypothesis` | string | no | The key of the hypothesis this change TESTS, from list_hypotheses. 🔴 Without it a merged change has nothing to be judged against and shows on get_work_board as `unmeasured` — which is the honest word, and the debt somebody pays later by reconstructing what you already knew. Write the claim first with add_hypothesis; this call attaches it. |

<!-- /widget -->

## Call it

<!-- widget:code-group -->

### MCP

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "write_docs",
    "arguments": {}
  }
}
```

### curl

```bash
curl -X POST 'https://docsbook.io/api/mcp/server' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"write_docs","arguments":{}}}'
```

<!-- /widget -->

## Try it over REST

The same tool is callable as a plain HTTP request, no MCP client required. It runs on the same server, at the same price.

Your workspace is resolved from the API key, so `workspace_id` is decided server-side here and anything you send for it is ignored.

<!-- widget:api -->

### POST /api/v1/tools/write_docs

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | Your API key, sent as `Authorization: Bearer dbk_YOUR_API_KEY`. |
| `args` | object | no | The arguments above, as one JSON object. |

#### Request

```bash
curl -X POST 'https://docsbook.io/api/v1/tools/write_docs' \
  -H 'Authorization: Bearer dbk_YOUR_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"args":{}}'
```

<!-- /widget -->
