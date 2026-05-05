# Translation Settings

Publish your documentation in multiple languages — automatically, with no manual work.

## Settings

| Setting | What it does |
|---|---|
| Enabled languages | Which languages to publish your docs in |
| Language switcher in sidebar | Show the language selector in the left sidebar |
| Language selector in header | Show the language selector in the top header bar |

## How to Enable

1. Requires a **Pro plan**.
2. Open your docs site.
3. Float Widget → **Translation** tab.
4. Check the languages you want to enable.
5. Save — translation starts automatically in the background.

Translation typically takes **1–5 minutes** for small repositories, up to 30 minutes for large ones.

## Supported Languages

15 core languages are available:

| Language | Code |
|---|---|
| Spanish | `es` |
| French | `fr` |
| German | `de` |
| Portuguese | `pt` |
| Italian | `it` |
| Russian | `ru` |
| Chinese | `zh` |
| Japanese | `ja` |
| Korean | `ko` |
| Arabic | `ar` |
| Hindi | `hi` |
| Turkish | `tr` |
| Polish | `pl` |
| Dutch | `nl` |
| English | `en` (default) |

## Language Switcher Placement

The language switcher can appear in the **sidebar**, the **header**, or both.

**Recommendation:** Pick one location. Showing it in both places is redundant.

| Placement | Best for |
|---|---|
| Header | More visible, better for international audiences |
| Sidebar | Saves header space when header is already full |

Configure placement in:
- [Header Options →](../design/header)
- [Sidebar Control →](../design/sidebar)

## URL Structure

Each language gets its own URL path:

```
docsbook.io/{username}/{repo}           → English (default)
docsbook.io/{username}/es/{repo}        → Spanish
docsbook.io/{username}/fr/{repo}        → French
```

Each language version is indexed separately by search engines, which means passive SEO traffic in every language you publish.

## Disabling a Language

Uncheck the language in the Translation tab → Save.

Visitors on that language's URL are automatically redirected to the English version. Cached translations are kept — re-enabling is instant.

---

> **Reach a global audience without hiring translators.**
> [Upgrade to Pro →](https://docsbook.io/connect)

See also: [How AI Translations work →](./ai-translations)
