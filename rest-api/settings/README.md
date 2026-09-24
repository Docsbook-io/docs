---
title: "Settings"
description: "Change one thing about the site to a value the user stated."
---

# Settings

Change one thing about the site to a value the user stated.

<!-- widget:endpoints -->

- [Approve translation](./approve-translation.md) `POST /api/v1/approve_translation` — Approve a draft translation, moving it to status 'published'.
- [Configure mentions](./configure-mentions.md) `POST /api/v1/configure_mentions` — Choose what the mention checks watch on one engine: turn the daily check on or off, and set the queries (up to 5) —…
- [Delete translation](./delete-translation.md) `POST /api/v1/delete_translation` — Delete a translation row.
- [Get chat system prompt](./get-chat-system-prompt.md) `GET /api/v1/get_chat_system_prompt` — Get the current custom AI chat system prompt for a workspace.
- [Get translation](./get-translation.md) `GET /api/v1/get_translation` — Get the translation for a specific source path and language.
- [Get translation status](./get-translation-status.md) `GET /api/v1/get_translation_status` — How each enabled language stands against the source RIGHT NOW: pages current / behind / missing / manual, the…
- [List pending translations](./list-pending-translations.md) `GET /api/v1/list_pending_translations` — List draft translations awaiting approval for a workspace.
- [Run translation pass](./run-translation-pass.md) `POST /api/v1/run_translation_pass` — Start a REAL translation catch-up run for one or more languages: the same batch the panel's 'Translate now' starts,…
- [Set chat hooks](./set-chat-hooks.md) `POST /api/v1/set_chat_hooks` — Set pre-, post-, and streaming webhook URLs for the AI chatbot.
- [Set chat system prompt](./set-chat-system-prompt.md) `POST /api/v1/set_chat_system_prompt` — Set a custom system prompt for the AI chatbot.
- [Set translation mode](./set-translation-mode.md) `POST /api/v1/set_translation_mode` — Set the translation workflow mode for a workspace: 'auto' (Docsbook AI), 'manual' (drafts via API), or 'external'…
- [Test chat hook](./test-chat-hook.md) `GET /api/v1/test_chat_hook` — Send a test ping to one of the configured AI chat hooks and return status.
- [Update access](./update-access.md) `POST /api/v1/update_access` — Make a workspace private and configure its unlock method (password and/or bring-your-own SSO/OIDC identity provider —…
- [Update ai settings](./update-ai-settings.md) `POST /api/v1/update_ai_settings` — Configure the AI chatbot.
- [Update branding](./update-branding.md) `POST /api/v1/update_branding` — Update visual branding: colors, fonts, logo, theme, the site's call-to-action URL, and the Site source URL the AI…
- [Update domain](./update-domain.md) `POST /api/v1/update_domain` — Set or remove a custom domain (e.g.
- [Update languages](./update-languages.md) `POST /api/v1/update_languages` — Set the languages the site is served in — the call for 'we need docs in Spanish and German', «нужна документация на…
- [Update navigation](./update-navigation.md) `POST /api/v1/update_navigation` — Update every curated link on the docs site: header links, social links, FOOTER link columns, folder navigation tabs,…
- [Update site address](./update-site-address.md) `POST /api/v1/update_site_address` — Change the ADDRESS of the site: the <name> in <name>.docsbook.io — its path name / subdomain.
- [Update ui settings](./update-ui-settings.md) `POST /api/v1/update_ui_settings` — Show or hide one interface element of the docs site — the header search button, sidebar search, collapsible top-level…
- [Upload translation](./upload-translation.md) `POST /api/v1/upload_translation` — Upload or replace a translation for a workspace document.

<!-- /widget -->
