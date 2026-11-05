# Reference Git MCP server

Source: [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers/tree/main/src/git) · Type: MCP server

## What it is for
Read, search and change Git repositories over MCP. It's one of the active reference servers (with Fetch, Filesystem, Memory, Sequential Thinking and Time). Claude Code already has native git, so its main value is as a well-built example and for other MCP clients.

## When to reach for it
Learning how a good MCP server is shaped, or giving git access to a client without a shell.

## Commands that matter
- Add: `claude mcp add git -- uvx mcp-server-git --repository <path>` (check the README first).
- Inspect it with [MCP Inspector](mcp-inspector.md).

## First exercise (about 15 minutes)
1. Add it scoped to one repo.
2. Ask Claude to summarise the last five commits using the MCP tool.
3. Read the server's tool list and compare it to your own server design.

## How you know it worked
The answer comes through the MCP tool, not shell git.

## Common mistake
Leaving it unscoped. It can change repos; point it at one repo.
