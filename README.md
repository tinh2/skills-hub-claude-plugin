# Skills Hub plugin for Claude Code

Search, inspect, and install AI coding skills from [skills-hub.ai](https://skills-hub.ai) without leaving Claude Code. skills-hub.ai is an open registry of `SKILL.md` skills (code review, testing, deployment, documentation, security, and more) that work in Claude Code and other coding agents. Every published skill carries a version, a quality score, and an install count, so you can pick a proven skill instead of writing your own.

## Install

```
/plugin install skills-hub@claude-community
```

Or add the community marketplace from your shell first:

```bash
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install skills-hub@claude-community
```

### Any agent with the skills CLI or GitHub CLI

To install only the `find-skills` skill (no slash commands or MCP config) into Claude Code, Cursor, Codex, OpenCode, and other agents, use Vercel's [skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add tinh2/skills-hub-claude-plugin
```

Or the [GitHub CLI](https://cli.github.com) (v2.90.0 or later, `gh skill` is in public preview):

```bash
gh skill install tinh2/skills-hub-claude-plugin find-skills
# target one agent, for example Claude Code:
gh skill install tinh2/skills-hub-claude-plugin find-skills --agent claude-code
```

The skill calls the skills-hub.ai MCP tools when they are connected. Without them, add the MCP server at `https://api.skills-hub.ai/mcp`, or install a result with `npx @skills-hub-ai/cli install <slug>`.

### Cursor and other Agent Plugins clients

This repo is also an [Agent Plugins](https://agent-plugins.org) 1.0.0 plugin (`plugin.json` and `mcp.json` at the root), so clients that support the standard, such as Cursor, get the `find-skills` skill and the remote MCP server. The slash commands below are Claude Code only.

## What you get

| Command                         | What it does                                                                              |
| ------------------------------- | ----------------------------------------------------------------------------------------- |
| `/skills-hub:search <query>`    | Search the registry and show the 10 best matches                                          |
| `/skills-hub:install <slug>`    | Show a skill's details, ask you to confirm, then install it into `.claude/skills/<slug>/` |
| `/skills-hub:browse [category]` | Link to the catalog on skills-hub.ai and list its most popular skills                     |
| `/skills-hub:recent`            | List the 10 most recently published skills                                                |

The plugin also includes a `find-skills` skill, so Claude can suggest an existing skill when you ask whether one exists for a task.

## Example prompts

Once the plugin is installed you can just ask Claude in plain language:

- "Is there a skill for reviewing database migrations?"
- "Find me a skill that writes Playwright tests, and show me the top three."
- "What does the `code-review` skill actually do before I install it?"
- "Install the best Terraform skill for this repo."

Or use the slash commands directly, for example `/skills-hub:search security audit` then `/skills-hub:install <slug>`.

## Troubleshooting

- **Claude doesn't use the skills-hub tools:** run `/mcp` and check that `skills-hub` is connected. If it isn't, add it with `claude mcp add --transport http skills-hub https://api.skills-hub.ai/mcp`.
- **Install fails with an npm error:** the install command needs Node.js 18 or later on your PATH (`node -v`).
- **A skill didn't show up after install:** skills land in `.claude/skills/<slug>/` of the folder you ran Claude from. Restart Claude Code, or start a new session, so it picks up the new skill.

## What it runs, sends, and fetches

- **MCP server:** the plugin connects Claude to the skills-hub.ai remote MCP server at `https://api.skills-hub.ai/mcp` (HTTPS, no account or API key). Its tools are `search_skills`, `get_skill_detail`, `list_installed_skills` (browses the public catalog), and `install_skill` (records an install count on skills-hub.ai, writes no files). Your search queries and the slugs you look up are sent to skills-hub.ai.
- **Recent skills:** `/skills-hub:recent` fetches the public, read-only endpoint `https://skills-hub.ai/api/v1/skills?limit=10&sort=newest`.
- **Installing a skill:** only after you confirm, `/skills-hub:install` runs `npx -y @skills-hub-ai/cli@0.4.4 install <slug>` from your project root. That downloads the open-source skills-hub CLI (version pinned) from npm; the CLI fetches the skill from skills-hub.ai and writes it to `.claude/skills/<slug>/`. The slug is checked against `^[a-z0-9][a-z0-9-]{0,99}$` before anything runs.
- The plugin has no hooks, collects no telemetry of its own, and never reads your credentials or environment.

Installed skills are third-party content written by registry authors. Read what a skill will do before you install it; the install command shows you its details first.

See the [privacy policy](https://skills-hub.ai/privacy) and [terms](https://skills-hub.ai/terms).

## Related

- [skills-hub.ai](https://skills-hub.ai): browse and publish skills
- [@skills-hub-ai/mcp](https://www.npmjs.com/package/@skills-hub-ai/mcp) ([source](https://github.com/tinh2/skills-hub-mcp)): a local MCP server that serves your installed skills as prompts in any MCP client
- [@skills-hub-ai/cli](https://www.npmjs.com/package/@skills-hub-ai/cli): the command-line client used for installs

## License

MIT. See [LICENSE](LICENSE).
