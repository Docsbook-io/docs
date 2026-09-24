---
title: "Private docs: password or SSO login for readers"
description: "Make Docsbook docs private: readers unlock them with a shared password or sign in through your own OIDC provider, such as Google Workspace, Entra ID or Okta."
---

# Private docs

Close your docs to the public and let readers in with a shared password, your company's single sign-on, or both, on every plan.

<!-- widget:stepper -->

### Switch the site to private

Open **Settings ▸ Access ▸ Privacy & Access** and turn off **Public — anyone with the link**.

### Choose how readers get in

Turn on **Password** and set one of at least 8 characters, or turn on **SSO (bring your own IdP)**, or both.

### Check what readers see

Open the site in a private browser window.

<!-- /widget -->

<!-- widget:callout type=warning -->

A private site with no password and no SSO can only be read by you and your collaborators. The card says so until you turn one on.

<!-- /widget -->

## What readers see

Readers land on a sign-in page instead of your docs: **This workspace is private**, with **Sign in with SSO**, a password field and **Unlock**, or both.

- **After unlocking**, they stay in for 30 days in that browser.
- **You and your collaborators** (**Settings ▸ Access ▸ Collaborators**) skip the page while signed in to Docsbook.
- **Search engines and AI crawlers** get the same sign-in page when they open a page.
- **Your [public MCP server](../brain/mcp-server.md)** refuses to read a private site for anonymous agents.

## Set up SSO

Docsbook signs readers in with OpenID Connect (authorization code with PKCE, scopes `openid email profile`), so Google Workspace, Microsoft Entra ID, Okta or any other OIDC provider works.

1. **Register a web app** in your provider with this redirect URI: `https://<host>/api/workspaces/<project id>/access/sso/callback`, where `<host>` is the domain readers open, your [custom domain](./custom-domain.md) if you have one. Your agent can read the project id with `get_workspace`.
2. **Fill in the SSO form**: **Issuer URL**, **Client ID**, **Client secret**, **Authorization endpoint**, **Token endpoint**, **JWKS URI** and, optionally, **Allowed email domain**. Every provider lists these values at `<issuer>/.well-known/openid-configuration`.
3. **Press Save SSO.** The client secret is stored encrypted and never shown again.

For Google Workspace, the values are:

| Field | Value |
|---|---|
| Issuer URL | `https://accounts.google.com` |
| Authorization endpoint | `https://accounts.google.com/o/oauth2/v2/auth` |
| Token endpoint | `https://oauth2.googleapis.com/token` |
| JWKS URI | `https://www.googleapis.com/oauth2/v3/certs` |

<!-- widget:callout type=warning -->

Leave **Allowed email domain** empty and anyone your provider lets sign in gets in. Set it to your company domain, such as `acme.com`: Docsbook checks Google's `hd` claim, or the domain of the reader's email for other providers.

<!-- /widget -->

A failed sign-in shows its reason on the sign-in page: `domain_not_allowed` means the email is outside the allowed domain; `token_exchange_failed` usually means the client secret, token endpoint or redirect URI doesn't match; `id_token_verification_failed` points at the Issuer URL, the JWKS URI or the client ID.

## The repository behind the site

- **A Docsbook-hosted repository** turns private on GitHub when the site does. Making the site public again leaves it private until you switch **Public on GitHub** in **Settings ▸ Access ▸ Source repository**.
- **Your own repository** is never touched. If it's public, anyone can still read the Markdown on GitHub, and the **Source repository** card warns you.

To keep a public site out of search results or AI answers without locking readers out, use the **Search engines** and **AI engines** cards on the same tab.

## Tell your agent

The Docsbook agent never changes who can read your site: ask it in the panel chat and it opens the **Privacy & Access** card for you to switch. Your own agent in Claude Code, Cursor or Codex can do it with `update_access`, which sets visibility, the password and SSO. It isn't in the default tool list, so the agent finds it with `find_tool` and runs it through `call_tool` ([Connect your agent](../get-discovered.md)).

## Next steps

<!-- widget:cards plain cols=2 arrow=hover -->

- [Custom domain](./custom-domain.md) — Serve the private site on your own domain {globe}
- [Edit and publish](./editing.md) — Hosted repositories, GitHub sync and review {pencil}
- [Public MCP server](../brain/mcp-server.md) — What readers' agents can reach, and what they can't {plug}
- [Plans and pricing](../pricing/plans.md) — What each plan includes {credit-card}

<!-- /widget -->
