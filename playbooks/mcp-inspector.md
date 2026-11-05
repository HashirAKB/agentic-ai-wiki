# MCP Inspector

Source: [modelcontextprotocol/inspector](https://github.com/modelcontextprotocol/inspector) · Type: CLI/tool

## What it is for
A local web UI that connects to any MCP server (stdio command or URL) and lets you list and call its tools, resources and prompts by hand, outside the model loop.

## When to reach for it
Building or debugging an MCP server: check tool schemas, descriptions and error messages before Claude ever sees them. Pairs with [mcp-server-dev](mcp-server-dev.md).

## Commands that matter
- Run: `npx @modelcontextprotocol/inspector` (opens the UI), or `npx @modelcontextprotocol/inspector <command> <args>` to start a stdio server directly.
- Check the README for current flags; they change.

## First exercise (about 15 minutes)
1. Run `npx @modelcontextprotocol/inspector uvx mcp-server-time`.
2. List the tools and read each input schema.
3. Call one with a timezone (e.g. `Asia/Kolkata`), then call it with a bad timezone.

## How you know it worked
You see the JSON result, and the bad call returns an error you could act on.

## Common mistake
Pointing it at a server command you have not read. It runs that command on your machine.
