# mcp-server-dev

Source: [anthropics/claude-plugins-official/plugins/mcp-server-dev](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/mcp-server-dev) · Type: plugin (skills)

## What it is for
Three skills for designing and building MCP servers that work well with Claude. `build-mcp-server` is the entry point: it asks what you are connecting to, who will use it and how many actions it needs, then recommends a path (remote HTTP server, MCP app with in-chat UI, a packaged local server, or a local stdio prototype) and scaffolds it, with references on auth, tool descriptions and security hardening.

## When to reach for it
When a project needs to let Claude (or any MCP client) act on something you own: a device, an app's data, an internal API.

## Commands that matter
- Install: `/plugin install mcp-server-dev@claude-plugins-official`
- Start: `/mcp-server-dev:build-mcp-server`, or just ask "help me build an MCP server".

## First exercise (about 30 minutes)
1. Pick a small real target, e.g. a smart device on your home network that you can already control from a script.
2. Run `/mcp-server-dev:build-mcp-server` and answer its questions honestly; note which deployment path it recommends and why.
3. Ask it to scaffold the smallest version with two tools (for example: read state, set state). Use red/green TDD.
4. Connect it to Claude Code and try both tools.

## How you know it worked
Claude can call your two tools from a session, and you can explain why the recommended deployment model fits.

## Common mistake
Exposing too many thin tools. Anthropic's guidance: few, well-scoped tools with clear descriptions and actionable errors. Also check the lethal trifecta before adding tools that send data out.
