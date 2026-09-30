---
name: graph-of-skills-lookup
description: Before a task that involves a file format, tool, API or team convention you may not know well, look up a written skill for it. Use at the start of the task.
---

Before starting such a task, check whether a skill already covers it.

1. If the `retrieve_skill_bundle` tool is available (the Graph-of-Skills MCP server), call it with one sentence describing the task.
2. If it is not, run this instead:

```bash
curl -s -X POST https://www.akilima.tech/api/graph-of-skills/retrieve \
  -H "Authorization: Bearer $GOS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query": "describe the task here"}'
```

The result lists matching skills with their full text. If one fits, follow it.
If nothing fits, or you already know how to do the task, carry on without it.
Skip the lookup for small edits and for work you have done many times in this project.
