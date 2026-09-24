---
title: "Goals"
description: "Declare what a reader was supposed to do, and count who did."
---

# Goals

Declare what a reader was supposed to do, and count who did.

<!-- widget:endpoints -->

- [Create funnel](./create-funnel.md) `POST /api/v1/create_funnel` — Define an ORDERED route through the docs, as a list of goal names.
- [Create goal](./create-goal.md) `POST /api/v1/create_goal` — Define a goal — one thing you want a reader to do.
- [Delete goal](./delete-goal.md) `POST /api/v1/delete_goal` — Archive a goal by name.
- [Edit goal](./edit-goal.md) `POST /api/v1/edit_goal` — CORRECT a goal that already exists — its label, what one completion is worth, or what it matches — without breaking it.
- [List goals](./list-goals.md) `GET /api/v1/list_goals` — The goals and funnels defined for this workspace, with what each one MATCHES.
- [Mark path as funnel step](./mark-path-as-funnel-step.md) `POST /api/v1/mark_path_as_funnel_step` — Add a documentation PAGE to a funnel as its next step, creating the page goal if it does not exist yet.

<!-- /widget -->
