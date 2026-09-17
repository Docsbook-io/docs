---
title: "Publishing what you wrote: preview, transport, configuration"
description: "How a finished documentation set gets previewed, published in one atomic commit, configured as a real site, and reported — including the route that needs no GitHub account at all."
tldr: "Preview the tree and real excerpts before asking to publish. Two transports exist: a connected platform that hosts the repository itself and needs no GitHub account, or plain git. Publish every page in one atomic commit, then configure the site."
---

# Publishing what you wrote

Publishing is the stage where a folder of good Markdown becomes a site somebody can be sent a link to. It changes no content. Everything below either shows the reader what exists, moves it, or configures how it is served.

## What counts as a preview?

Print the folder tree, **including the folders**, and excerpts from up to three representative pages plus the FAQ. A one-line summary is not a preview: nobody can decide from it, and the decision is the entire point of the step.

Then ask, plainly: "Does this look right? Type **yes** to publish, or describe what to change."

A run nobody is watching may skip the asking. It may never skip the preview, and it may never create a repository silently.

## Which transport are you publishing through?

Two of them, and **which one you have decides what the reader needs to own.** Check in this order.

### Route A — a connected platform hosts it, and no GitHub account is needed

This is the route whenever the [Docsbook MCP server](../../mcp/README.md) is connected, and it is the answer to "we have no repository", "I do not want to connect GitHub" and "just make me a documentation site".

1. Call [`create_workspace`](../../mcp/create/create-workspace.md) **without** `repo_full_name`, passing `custom_name` — the project name derived from the brand, never invented. The platform creates and hosts the documentation repository under its own GitHub organisation with its own credentials. The reader needs no GitHub account, no connected GitHub app and no repository of their own. Pass `repo_full_name: "owner/repo"` **only** when they pointed at a repository they own.
2. Call [`write_docs`](../../mcp/content/write-docs.md) with **every page in one call**. It commits them as one atomic commit and creates the hosted repository on first write. Keep the paths repository-relative: `index.md`, `guides/setup.md`.
3. Read the returned `site_url` and report that link verbatim. Never construct a URL by hand and never guess one.
4. Configure the live site through the same connection, below. A branding manifest, if you keep one, goes in with the pages.

A missing `repo_full_name` is **not an error to route around**: it is the from-scratch path working as designed. If the call is rejected for some other reason, report that reason verbatim rather than translating it into "connect GitHub".

### Route B — plain git, when nothing is connected and the reader wants their own repository

1. **Verify the transport is authenticated first.** If it is not, and no platform is connected either, stop with a crawl-only result: the local path, and the exact follow-up command to run afterwards. This is a clean ending, not a failure — the crawl output has already been delivered.
2. **Derive the repository name from the folder name**, which earlier stages set from the site brand or the source repository. A placeholder-looking name — `docs-output`, `untitled`, a timestamp — means ask for a real one rather than publishing under it. Ask on a genuine collision too.
3. **Initialise the repository only if it is not one already**; otherwise reuse the current branch.
4. **Create the repository, add the remote, push.** Never overwrite an existing repository: a taken name is a stop, not a force-push.
5. **One atomic commit for all pages**, not one commit per file.
6. **Keep any branding manifest in the repository** — the configuration step reads it.

If the tooling is not installed at all, return the equivalent manual commands rather than failing silently.

## Configuring the live site

The point is not to flip switches; it is to make the site feel like the product's own documentation. A published-but-unconfigured site undersells the work that went into it.

| What | Why it matters | Where |
|---|---|---|
| Branding | The documentation reads as a continuation of the product rather than as a third-party page | [`update_branding`](../../mcp/settings/update-branding.md) |
| Reading affordances | Copy-page, feedback, breadcrumbs, on-page contents — what separates a documentation site from a rendered README | [`update_ui_settings`](../../mcp/settings/update-ui-settings.md) |
| Navigation | The sub-header built from your top-level folders, social links in the header, a link back to the source site | [`update_navigation`](../../mcp/settings/update-navigation.md) |
| Discovery | Real titles and descriptions plus indexing enabled, and the answer-engine layer — the reason the FAQ and use-case content exists | [SEO](../../seo/indexing.md), [AEO](../../aeo/README.md) |
| Assistant | A live "ask" over the documentation removes the go-and-find-it-yourself barrier for an unsold reader | [`update_ai_settings`](../../mcp/settings/update-ai-settings.md), [AI chat](../../ai-chat/README.md) |

Apply the accent, scheme, logo and icon collected during the [product audit](./know-the-reader.md#brand-signals). **Never push a default accent when extraction failed** — run the branding path so it asks for a reference instead. Derive the assistant's suggested questions from the pages you just created, never generic ones.

Confirm before applying. Language settings in particular can enable several languages at once and surprise people; see [translation](../../translation/README.md). If the platform transport is unreachable, print the connection instructions and exit cleanly — the local folder and the repository URL have already been delivered, so the run does not fail.

## Declare the goals and the funnel while the room is still full

The [product audit](./know-the-reader.md#what-to-ask-when-the-source-cannot-answer) wrote down the goals and a three-to-five step path per segment. On almost every run they stay prose in a report: the site ships, and three months later nobody can say whether it worked, because nothing was ever declared as success.

Turning them into real measurement is one step — [`create_goal`](../../mcp/goals/create-goal.md) for each observable thing a reader does, then [`create_funnel`](../../mcp/goals/create-funnel.md) for the order they happen in — and it is cheap here in a way it never is later, because the person who decided what the site was for is still in the room. The method is in [goals and funnels](../auditing/goals-and-funnels.md).

## Interactive checkpoints

Six pauses, one question per turn, each waiting for an explicit answer and each applied before the next stage runs:

1. **Source** — show the detected type and wait. A different source means re-running detection, never assuming.
2. **Structure** — display the proposed tree; apply the requested changes before generating any file.
3. **Enrichment** — which optional sections, which competitors, how many pages per section (four by default, three to five allowed). No evidence for a section means saying so and letting the reader type names or skip.
4. **Branding** — show the detected palette and let the reader override it before anything is written.
5. **Where it lives** — on route A, confirm the site name and say plainly that the platform hosts the repository, so nothing on GitHub is needed. On route B, confirm the owner and repository name. Propose the derived name; ask outright when none can be derived. **Never turn this checkpoint into a request to connect GitHub.**
6. **Features** — which optional site features to enable. Apply only what was selected; never enable an extra silently.

The final report summarises every choice made at every checkpoint, including the per-section enrichment counts.

## The final report

```
Local path:   docs-output/<name>/
Repository:   <url>            (hosted by the platform, or the user's own — or: not published, crawl_only)
Live site:    <url>            (or: not configured — <reason>)
Pages:        N across M folders
  index.md — hero
  getting-started.md — tutorial (N steps)
  concepts.md — explanation
  features/<feature>.md ×K — benefit-first
  guides/<topic>.md ×K — how-to
  use-cases.md — job stories
  faq.md — N Q&A
  reference.md — reference [if API/CLI]
Branding:     accent <hex> (from <source>) · icon <url> · logo <url or skipped>
Skipped:      <section> — <reason>
```

Every skipped section carries its reason. A gap with a reason next to it is a decision somebody can revisit; a gap without one looks like a bug.

## What comes next

A freshly published site is the start of a loop, not the end of one. Wire the drift guards and monitors once the documentation is live ([automation](../automation/setting-it-up.md)), and audit the site with the [auditing](../auditing/README.md) section after it has readers — not on the day it ships, and not with the same run that wrote it.

## Related

<!-- widget:cards plain cols=2 -->

- [Routing the input](./route-the-input.md) — the four stages this one closes. {compass}
- [Deciding the page set](./page-set.md) — the folders that become this site's navigation. {list}
- [Know the reader before you write the page](./know-the-reader.md) — where the branding, the call-to-action destination and the goals came from. {search}
- [Goals and funnels](../auditing/goals-and-funnels.md) — declaring success while it is still cheap. {target}
- [MCP server](../../mcp/README.md) — the full tool surface behind route A. {plug}

<!-- /widget -->
