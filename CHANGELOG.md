---
title: "Docsbook Changelog"
description: "Release notes for Docsbook — new features, improvements and bug fixes to the AI-powered documentation platform, newest first."
layout: changelog
status: generated
version: "0.11"
---

# Product updates

New features, improvements and bug fixes in Docsbook — newest first. Each update has its own page; filter by type or by the part of the product it touches.

## 2026-09-25 — Claim links open the docs, not sign-in

When you mint a claim link the recipient now sees the gifted documentation first instead of being bounced to sign-in. You can also manage who has access — withdraw pending invites and revoke accepted members — from the same Collaborators card that listed them before.

### New releases

- **`/claim/<token>` no longer redirects straight to sign-in.** For a live link to a public site it now opens the docs themselves with `?claim=<token>`; a banner on the page tells the reader the documentation is a gift and a **Claim** button runs sign-up / sign-in and the explicit confirm step. Private sites and dead links still go to the claim page — there is nothing to show for them anyway.
- **Revoke access from the Collaborators card.** Settings ▸ Access ▸ Collaborators now carries a **Withdraw** button for pending invites and a **Revoke** button (with inline confirmation) for accepted members. The API (`DELETE /api/workspaces/:id/collaborators`) takes `member: true` to remove an accepted member from the roster; self-removal and the project owner are refused.

### Improvements

- **Token validation now accepts base64url**, the encoding used by every link minted from the panel and MCP. Previously only hex tokens were recognized, which meant valid links rarely displayed their gift banner. This is a bug fix — most claim links were always going straight to sign-in rather than opening the docs. `Auth`

### Bug fixes

- Same as the token-validation improvement above — fixed claim links showing the gift banner correctly for the first time. `Auth`

---

## 2026-09-20 — Watch an agent task while it works
