---
description: Install a skill from skills-hub.ai into this project's .claude/skills/ directory
argument-hint: "<slug>"
---

Install the skills-hub.ai skill with slug: $ARGUMENTS

1. The slug must match `^[a-z0-9][a-z0-9-]{0,99}$` (lowercase letters, digits, dashes). If it is missing or does not match, show the expected usage `/skills-hub:install <slug>` and stop. Never pass any other text to the shell.
2. Call the `get_skill_detail` tool from the `skills-hub` MCP server with that slug. If the skill is not found, say so and suggest `/skills-hub:search`. Otherwise show the user the skill's name, version, description, and quality scores, and summarize what its instructions will have Claude do.
3. Ask the user to confirm the install. Only after they confirm, run this command with the Bash tool from the project root:

   ```
   npx -y @skills-hub-ai/cli@0.4.4 install <slug>
   ```

   This downloads the published, pinned skills-hub CLI from npm, which fetches the skill from skills-hub.ai and writes it to `.claude/skills/<slug>/` in the current project.
4. Report the outcome. On success, tell the user the skill is available after `/reload-plugins` or in a new session, and how to invoke it.
