---
title: "Quick start: publish a documentation site with Docsbook"
description: "Generate a Docsbook draft from a repository, a website or an idea, review it before signing in, and publish it to a public URL you can share."
---

# Quick start: publish a documentation site with Docsbook

**What you will learn:** how to turn one source — a GitHub repository, a website, or a description of your product — into a published Docsbook documentation site with a public URL, a search index and analytics.

## Before you start

You need all of the following:

- A current version of Chrome, Firefox, Safari or Edge.
- **One** source, and only one: a GitHub repository containing at least one `.md` file, a public website URL, or two sentences describing what you sell.
- A way to sign in at step 3: a GitHub account, a Google account, an Apple ID, or an email address where you can receive a one-time code.

You do not need a credit card, a build pipeline, or an account before step 3.

<!-- widget:stepper -->

## Step 1 — Generate a draft
<!-- anchor: step-1-create-website -->

1. Open [docsbook.io/start](https://docsbook.io/start).
2. Paste your source into the single field: a website URL, a GitHub repository link, or a sentence about your product. Docsbook works out which it is — there is no type to pick.
3. Wait while Docsbook reads the source. Each step names what it read and what it found.

**Expected result:** a draft site opens on its own admin panel, with the page count, the source it came from, and every section for branding, layout and SEO. No account has been created yet.

## Step 2 — Open the draft and check it

1. Press **Open** on the admin panel, or click the preview itself.
2. Browse the generated pages as a real documentation site — header, sidebar tree, outline, breadcrumbs and prev/next all work.
3. Use **Assistant** in the panel to change wording or ask about the site. In the message box, **interactive mode** opens the site with the chat beside it and every block clickable.

**Expected result:** you have read the draft and know whether it describes your product correctly. A draft from a website or an idea lives in your browser only until you publish it.

## Step 3 — Sign in to publish

1. Press **Publish this site** on the panel's front page, or the blue button in the toolbar on the documentation itself. It reads **Publish** if you have changed nothing yet, **Save changes** if you have, and **Claim ownership** if you arrived through a claim link — all three do the same thing.
2. Choose a sign-in method: GitHub, Google, Apple, or email with a one-time code.
3. Complete the sign-in flow.

**Expected result:** the draft becomes a live Docsbook project with a public address, a search index and analytics. Nothing you wrote is re-done.

If your site came from a GitHub repository and you signed in with Google, Apple or email, Docsbook asks you to authorise GitHub access as well — it reads the repository files through that authorisation.

## Step 4 — Open the published site

1. Open the address Docsbook shows you. It follows the pattern below.

```text
docsbook.io/{owner}/{repo}
```

2. Use the search box in the header, or press Cmd+K (Ctrl+K on Windows and Linux), and search for a phrase from one of your pages.

**Expected result:** the page loads at a public URL, search returns your phrase, and the site is readable without signing in.

<!-- /widget -->

## What you have now

You have a published documentation site: a public URL, full-text search, a `sitemap.xml`, `llms.txt` for AI agents, and analytics recording page views from the first visitor. A site built from a GitHub repository re-checks the repository when it is visited, so pushing to GitHub updates the pages with no build step.

## Next steps

- [Manage your documentation](./guides/getting-started/managing-docs.md) — settings, reindexing, and who is allowed to read the site
- [Point your own domain at it](./guides/advanced/custom-domain.md) — one CNAME, SSL provisioned automatically
- [Turn on translation](./translation/settings.md) — publish the same pages in 15 languages
- [Connect an AI agent over MCP](./agent-ready/mcp.md) — read and edit the docs from Claude Code or Cursor
- [Pricing](./pricing.md) — what is metered, and what a project balance pays for

<!-- widget:cta -->

## Publish your first site

Paste a repository, a website URL, or a sentence about your product, and read the draft before you sign in.

[Create your first project](https://docsbook.io/start)

<!-- /widget -->
