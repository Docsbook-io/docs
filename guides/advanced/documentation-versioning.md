---
title: "Documentation versioning: patterns, and how Docsbook handles it"
description: "The common ways teams version their docs — URL-path versions, a version switcher, branch-per-version — and which one to use with Docsbook, which publishes one version per branch."
status: review
---

# Documentation versioning

"Versioning" your documentation means keeping more than one release's docs available at once, so a reader on an older release of your product is not reading instructions for a newer one. This page covers the common ways teams do that, and how to get the same result with Docsbook, which is not the same as picking a plan feature — it is a decision about how you organize content and repositories.

## Common versioning patterns

**URL-path versioning.** Each version gets its own path segment — `/docs/v1/`, `/docs/v2/` — and a switcher in the header lets a reader jump between them. This is what most large API-heavy products use, because a reader can bookmark or link to a specific version and it will not change under them.

**A version switcher over one canonical set of docs.** Smaller changes (a config option renamed, a default changed) are called out inline with a note like "as of v2.3" rather than duplicating the whole page. This avoids maintaining N complete copies of every page, at the cost of the page reading slightly more like a changelog.

**Branch-per-version, one deployed site.** The documentation source lives on version branches (`docs/v1`, `docs/v2`) in the same repository, and a build step publishes all of them behind a switcher. This keeps history and diffing simple in git, but needs a build pipeline that knows how to publish more than one branch at once.

**Separate repositories or sites per major version.** The simplest to reason about, and the easiest to get wrong silently — a fix made on the v2 docs is easy to forget to backport to v1, and nothing enforces it.

Which pattern fits depends mostly on how many versions you realistically need live at once. Most products with a stable, slow-moving API need at most "current" and "previous major"; more than that is usually a sign the underlying product's compatibility policy, not the docs tooling, needs attention.

## How Docsbook handles this today

Docsbook publishes **one version of your documentation: the current state of the branch you connected.** There is no built-in version switcher and no way to publish multiple versions of the same workspace side by side.

If you need more than one version live, the supported workaround is **one workspace per version**, each pointed at its own branch or repository:

1. Keep each version's docs on its own branch (`docs/v1`, `docs/v2`) or in its own repository.
2. Create a separate Docsbook workspace for each one you want published (`create_workspace`, or **Add project** in the app).
3. Give each its own subdomain or path via a [custom domain](../advanced/custom-domain.md) — for example `v1-docs.yourproduct.com` and `docs.yourproduct.com` for the current version — so readers can tell which one they are on.
4. Link between them from a visible spot on each site (for example, a line at the top of the older version's README) so a reader who lands on stale docs can find the current ones.

This reproduces the "separate sites per version" pattern above. It does not give you a single switcher UI across versions, and each workspace is billed and configured independently. For most teams keeping only a current and a previous-major version, this is a small amount of one-time setup rather than an ongoing cost.

If your real need is smaller — a handful of "changed in vX" callouts rather than a fully separate historical copy of the docs — the inline-note pattern above usually costs less to maintain than standing up a second workspace, and works today with no extra setup: just write the note directly on the current page.

## Next steps

- [Manage your documentation site](../getting-started/managing-docs.md) — everyday publishing, once your site is live.
- [Set up a custom domain](../advanced/custom-domain.md) — needed if you are running one workspace per version.
- [Create your first documentation site](../getting-started/creating-docs.md) — for setting up the second workspace.
