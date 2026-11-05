# claude-plugins-community marketplace

Source: [anthropics/claude-plugins-community](https://github.com/anthropics/claude-plugins-community) · Type: plugin marketplace

## What it is for
A read-only mirror of community plugins submitted through Anthropic's pipeline, each said to have passed automated security scanning. Listed on 2026-10-31: `eli5`, `html-plan`, `next-steps`, `quickdesign`, `testdino`.

## When to reach for it
Looking for a plugin beyond the official directory.

## Commands that matter
- `claude plugin marketplace add anthropics/claude-plugins-community`
- `claude plugin install <name>@claude-community`

## First exercise (about 20 minutes)
1. Read `marketplace.json` and pick one plugin.
2. Read every file in its folder: commands, hooks, MCP config.
3. Install it and run its main command.

## How you know it worked
You can say what the plugin touches (files, network, hooks) before and after running it.

## Common mistake
Treating the scan as a guarantee. Plugins can ship hooks and MCP servers; read them first.
