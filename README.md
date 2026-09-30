# Graph-of-Skills for Claude Code

Connects Claude Code to [Graph-of-Skills](https://www.akilima.tech/graph-of-skills) and adds one short skill. The skill tells your agent to check for a written method before a task in an unfamiliar file format, tool or convention. Graph-of-Skills searches a public skill catalog and your own skills, and returns the best matches with their full text.

You need an API key. Get a free one at https://www.akilima.tech/get-api-key, then add it to your shell profile:

```bash
export GOS_API_KEY=your_key_here
```

## Install as a plugin (connection and skill together)

Inside Claude Code:

```
/plugin marketplace add benman1/graph-of-skills-claude-plugin
/plugin install graph-of-skills@akilima
```

The plugin declares the MCP server, which reads your key from `GOS_API_KEY`. The key is never written into a config file.

## Install only the skill

```bash
npx skills add https://www.akilima.tech -g -a claude-code -y
```

Or from this repo:

```bash
npx skills add benman1/graph-of-skills-claude-plugin --skill graph-of-skills-lookup -g -a claude-code -y
```

The skill calls the `retrieve_skill_bundle` tool when the MCP server is connected. Without it, the skill falls back to a `curl` call to the REST endpoint.

## What is in this repo

- `.claude-plugin/marketplace.json`: the marketplace file (`akilima`).
- `plugins/graph-of-skills/`: the plugin (manifest, `.mcp.json`, the lookup skill).
- `skills/graph-of-skills-lookup/SKILL.md`: the same skill, at a path the skills CLI finds.

These files are generated from the Graph-of-Skills product code. Open issues about the service at https://www.akilima.tech/contact.
