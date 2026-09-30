# Graph-of-Skills for Claude Code

Docs: https://benman1.github.io/graph-of-skills-claude-plugin/

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

## Troubleshooting

**401, or "Missing environment variables: GOS_API_KEY".** Claude Code reads the key from its own environment when it starts. It was started from somewhere that never loaded your shell profile (an IDE, a desktop app, a launcher), or before you exported the key. In a terminal, `echo ${#GOS_API_KEY}` must print a number above 0; start Claude Code from that terminal (`claude --continue` keeps your conversation). `/mcp` reconnect cannot pick up a new variable.

**Starting from an app instead?** Use a header helper that reads the key at every connect. The steps are in the [docs](https://www.akilima.tech/graph-of-skills/docs#troubleshooting).

**"Monthly retrieval free-tier cap reached" (429).** The free plan's monthly retrievals are used up; every call counts, including test scripts. The allowance resets at the start of the calendar month.

## What is in this repo

- `.claude-plugin/marketplace.json`: the marketplace file (`akilima`).
- `plugins/graph-of-skills/`: the plugin (manifest, `.mcp.json`, the lookup skill).
- `skills/graph-of-skills-lookup/SKILL.md`: the same skill, at a path the skills CLI finds.

These files are generated from the Graph-of-Skills product code. Open issues about the service at https://www.akilima.tech/contact.
