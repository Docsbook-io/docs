---
title: "Private Docs: Password & SSO Setup"
description: "Restrict who can read your documentation — set a shared password, or gate the site behind your own Google Workspace, Microsoft Entra ID, or Okta SSO."
---

# Private Docs: Password & SSO

By default, a Docsbook site is public — anyone with the link can read it. On Pro and Business, you
can switch a workspace to **private** and require readers to unlock it first, either with a shared
password or by signing in through your own SSO identity provider.

**Required:** Pro (monthly, 7-day free trial) or Business (monthly, 14-day free trial)

## How It Works

- **Public** (default) — anyone with the link reads the site, same as today.
- **Private** — an anonymous reader sees an unlock screen instead of your content. Nothing about
  the docs (structure, pages, search index) is exposed until they unlock it.
- The **owner** always has full access, regardless of visibility — the gate only applies to
  everyone else.
- You can configure a password, SSO, or both at once. If both are set, a reader picks whichever
  they have.

## Option 1: Password Protection

The simpler option — set one shared password for the whole workspace.

1. Open your documentation while logged in
2. Click the Float Widget in the bottom right → **Settings** → **Privacy & Access**
3. Switch visibility to **Private**
4. Enter a password (at least 8 characters) and click **Set**

Readers who enter the correct password stay unlocked for a while, so they don't have to re-enter
it on every visit. To change the password, set a new one the same way. To remove password
protection, click **Remove** next to the password field.

## Option 2: SSO (Bring Your Own Identity Provider)

For team or company docs, SSO lets readers sign in with their existing work account instead of
sharing a password. You register your own app with your identity provider — Docsbook never sees or
stores your provider's admin credentials, only the OAuth app details you enter.

You'll need, from your identity provider's app registration:

| Field | What it is |
|-------|------------|
| Issuer URL | Your provider's OIDC issuer identifier |
| Client ID | The app registration's public identifier |
| Client secret | The app registration's secret (stored encrypted, never shown again after saving) |
| Authorization endpoint | Where readers are sent to sign in |
| Token endpoint | Where Docsbook exchanges the sign-in code for an identity token |
| JWKS URI | Where Docsbook verifies the identity token's signature |
| Allowed domain *(optional)* | Restrict sign-in to one email domain, e.g. `acme.com` — anyone outside it is rejected even with valid IdP credentials |

### Google Workspace

1. In the [Google Cloud Console](https://console.cloud.google.com), create an **OAuth 2.0 Client ID** (type: Web application)
2. Add redirect URI: `https://docsbook.io/api/workspaces/<workspace_id>/access/sso/callback` (your workspace ID is shown in the Privacy & Access panel)
3. Use these standard Google endpoints:
   - Issuer: `https://accounts.google.com`
   - Authorization endpoint: `https://accounts.google.com/o/oauth2/v2/auth`
   - Token endpoint: `https://oauth2.googleapis.com/token`
   - JWKS URI: `https://www.googleapis.com/oauth2/v3/certs`
4. Set **Allowed domain** to your Google Workspace domain (e.g. `acme.com`) to restrict sign-in to your organization

### Microsoft Entra ID

1. In the [Entra admin center](https://entra.microsoft.com), register a new application
2. Add redirect URI: `https://docsbook.io/api/workspaces/<workspace_id>/access/sso/callback`
3. Create a client secret under **Certificates & secrets**
4. Use your tenant's OIDC endpoints (found under **Endpoints** in the app overview), typically:
   - Issuer: `https://login.microsoftonline.com/<tenant-id>/v2.0`
   - Authorization endpoint: `https://login.microsoftonline.com/<tenant-id>/oauth2/v2.0/authorize`
   - Token endpoint: `https://login.microsoftonline.com/<tenant-id>/oauth2/v2.0/token`
   - JWKS URI: `https://login.microsoftonline.com/<tenant-id>/discovery/v2.0/keys`

### Okta

1. In your Okta admin console, create a new **OIDC – Web Application** integration
2. Add sign-in redirect URI: `https://docsbook.io/api/workspaces/<workspace_id>/access/sso/callback`
3. Use your Okta domain's endpoints, typically:
   - Issuer: `https://<your-org>.okta.com`
   - Authorization endpoint: `https://<your-org>.okta.com/oauth2/v1/authorize`
   - Token endpoint: `https://<your-org>.okta.com/oauth2/v1/token`
   - JWKS URI: `https://<your-org>.okta.com/oauth2/v1/keys`

### Saving SSO Settings

1. Open the Float Widget → **Settings** → **Privacy & Access**
2. Switch visibility to **Private** if you haven't already
3. Click **Configure Google Workspace / Entra ID / Okta…** under SSO
4. Fill in the fields above and click **Save SSO**

To remove SSO, click **Remove** next to the SSO status. Removing SSO does not affect a
separately-configured password, and vice versa.

## Via MCP (AI agents)

An AI agent connected to your workspace's MCP server can configure this with the `update_access`
tool — same fields as above, passed as `visibility`, `password`, and `sso` (with `client_id`,
`client_secret`, `authorization_endpoint`, `token_endpoint`, `jwks_uri`, `allowed_domain`).

## Troubleshooting

### Reader gets "Incorrect password"

Passwords are case-sensitive. Set a new one if you're unsure what was configured — the current
password can't be revealed, only replaced.

### SSO sign-in fails with "domain_not_allowed"

The signed-in account's email domain doesn't match **Allowed domain**. Either sign in with an
account on the right domain, or clear the Allowed domain restriction if you want to admit any
account your identity provider authenticates.

### SSO sign-in fails with "token_exchange_failed" or "id_token_verification_failed"

Double-check the client secret and the three endpoint URLs — a typo in any of them breaks the
handshake. Endpoints must be the exact ones your identity provider issues for your tenant/org, not
generic placeholders.

## What's Next?

- [Managing Your Documentation](../getting-started/managing-docs.md)
- [Pro and Business plans](./premium.md)
