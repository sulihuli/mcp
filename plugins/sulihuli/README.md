# SuliHuli plugin

The SuliHuli electric-vehicle catalog inside Claude Code and Cursor: specs, range by test cycle, charging, prices,
rankings and comparisons - every figure with its source link and date, verified figures marked.

- **MCP server** `sulihuli` - `https://sulihuli.com/api/mcp` (read-only, no sign-in).
- **Skill** `sulihuli` - which door to use (MCP or HTTP API) and how to quote the data: source, status, test cycle.

Install in Claude Code:

    /plugin install sulihuli --marketplace sulihuli/mcp
