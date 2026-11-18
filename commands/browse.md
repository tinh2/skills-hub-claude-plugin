---
description: Get a link to browse skills-hub.ai, optionally filtered by category
argument-hint: "[category]"
---

Give the user a link to browse the skills-hub.ai catalog. Category argument: $ARGUMENTS

- With no category, the link is https://skills-hub.ai/browse
- With a category made only of letters, digits, and dashes (for example `review`, `build`, `test`), the link is `https://skills-hub.ai/browse?category=<category>` with the category lowercased. Reject any other category text.

Print the link. Then call the `list_installed_skills` tool from the `skills-hub` MCP server (it browses the catalog by popularity, despite its name) with the category if one was given and `limit` 10, and list the top results with their slugs so the user can install one with `/skills-hub:install <slug>`.
