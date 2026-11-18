---
description: Search skills-hub.ai for AI coding skills and show the best matches
argument-hint: "<query>"
---

Search the skills-hub.ai registry for skills matching: $ARGUMENTS

1. If no query was given, ask the user what kind of skill they are looking for and stop.
2. Call the `search_skills` tool from the `skills-hub` MCP server with `query` set to the user's query and `limit` 10.
3. Show the results as a short list: name, one-line description, quality score and install count when present, and the slug.
4. Point out the two or three strongest matches and why. For each, show the install command: `/skills-hub:install <slug>`.
