---
description: List the 10 most recently published skills on skills-hub.ai
---

Show the 10 newest skills on skills-hub.ai.

Fetch `https://skills-hub.ai/api/v1/skills?limit=10&sort=newest` (a public, read-only, unauthenticated endpoint) with the WebFetch tool. The response is JSON with a `data` array; each item has `slug`, `name`, `description`, `category.name`, `latestVersion`, `installCount`, and `qualityScore`.

List each skill with its name, version, category, and a one-line description. Then suggest two or three the user might want to try, with `/skills-hub:install <slug>` for each.
