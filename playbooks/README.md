# Playbooks

One short guide per tool or setting adopted from the [tools radar](../radar/seen.md): what it is for, when to reach for it, the commands that matter, a first exercise, and a common mistake. The goal is to know how to use what is installed, not just to have it installed.

## Status

Statuses: `queued` (not installed yet), `learning` (installed, doing the first exercise), `using` (part of normal work), `removed`.
A tool that stays at `learning` for two weeks is suggested for removal in the Sunday digest.

| Tool | Playbook | Status | Since |
|---|---|---|---|
| Block writes outside working directories (Claude Code setting) | [block-writes-outside-working-dirs.md](block-writes-outside-working-dirs.md) | using | 2026-10-30 |
| code-simplifier (plugin) | [code-simplifier.md](code-simplifier.md) | queued | 2026-10-30 |
| security-guidance (plugin) | [security-guidance.md](security-guidance.md) | queued | 2026-10-30 |
| code-review (plugin) | [code-review.md](code-review.md) | queued | 2026-10-30 |
| mcp-server-dev (plugin) | [mcp-server-dev.md](mcp-server-dev.md) | queued | 2026-10-30 |

## Template for new playbooks
```
# <Tool>
Source: <official link> · Type: plugin | setting | skill | MCP server | connector
## What it is for
## When to reach for it
## Commands that matter
## First exercise (about 15 minutes)
## How you know it worked
## Common mistake
```
