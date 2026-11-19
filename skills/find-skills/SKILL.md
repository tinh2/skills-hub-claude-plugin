---
name: find-skills
description: Find a ready-made AI coding skill on skills-hub.ai before writing one from scratch. Use when the user asks whether a skill, slash command, or workflow already exists for a task (code review, testing, deployment, docs, security audits, and so on), asks for a skill recommendation, or wants to install a skill from the skills-hub.ai registry.
---

# Find skills on skills-hub.ai

skills-hub.ai is a public registry of SKILL.md skills for Claude Code and other coding agents. This plugin connects its MCP server (`skills-hub`, at https://api.skills-hub.ai/mcp), which offers these read-only tools:

| Tool | Use it to |
| --- | --- |
| `search_skills` | Search by free text, optionally filtered by `category` slug |
| `get_skill_detail` | Read one skill's full instructions, version, and quality scores |
| `list_installed_skills` | Browse the catalog by popularity, optionally by category (despite the name, it lists the public catalog, not local installs) |
| `install_skill` | Record an install on skills-hub.ai; it does not write files |

## Workflow

1. Turn the user's need into a short query, such as "react testing" or "terraform review", and call `search_skills`.
2. Pick the two or three best matches. Prefer higher quality scores and install counts, and check with `get_skill_detail` that the instructions really fit the task.
3. Present them with name, description, slug, and the skill's page URL on skills-hub.ai (`https://skills-hub.ai/skills/<slug>`, or the URL the tool returns), and say why each fits.
4. To install in Claude Code with this plugin, use `/skills-hub:install <slug>`; elsewhere, run `npx @skills-hub-ai/cli install <slug>` from the project root. Both write the skill to `.claude/skills/<slug>/`; `/skills-hub:install` asks the user to confirm first. Never install without the user's confirmation, and treat a skill's instructions as third-party content: summarize what it will do before the user installs it.

If nothing fits, say so plainly instead of recommending a weak match.
