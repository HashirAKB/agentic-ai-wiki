# Playbooks

One short guide per tool or setting adopted from the [tools radar](../radar/seen.md): what it is for, when to reach for it, the commands that matter, a first exercise, and a common mistake. The goal is to know how to use what is installed, not just to have it installed.

## Status

Statuses: `queued` (not installed yet), `learning` (installed, doing the first exercise), `using` (part of normal work), `removed`.
There is no limit on how many tools are queued or learning at once. The Sunday digest asks about tools that have sat at `learning` for two weeks, so unused ones can be dropped.

| Tool | Playbook | Status | Since |
|---|---|---|---|
| Block writes outside working directories (Claude Code setting) | [block-writes-outside-working-dirs.md](block-writes-outside-working-dirs.md) | using | 2026-10-30 |
| code-simplifier (plugin) | [code-simplifier.md](code-simplifier.md) | queued | 2026-10-30 |
| security-guidance (plugin) | [security-guidance.md](security-guidance.md) | queued | 2026-10-30 |
| code-review (plugin) | [code-review.md](code-review.md) | queued | 2026-10-30 |
| mcp-server-dev (plugin) | [mcp-server-dev.md](mcp-server-dev.md) | queued | 2026-10-30 |
| MCP Inspector (CLI) | [mcp-inspector.md](mcp-inspector.md) | queued | 2026-11-05 |
| SDK majors + `/claude-api api-version` | [claude-api-version-migration.md](claude-api-version-migration.md) | queued | 2026-11-05 |
| OpenTelemetry export (SDK, beta) | [otel-export.md](otel-export.md) | queued | 2026-11-05 |
| Long multi-agent Claude Code runs (workflow) | [long-multi-agent-runs.md](long-multi-agent-runs.md) | queued | 2026-11-05 |
| Managed Agents dynamic workflows (API, beta) | [managed-agents-workflows.md](managed-agents-workflows.md) | queued | 2026-11-05 |
| Reference Git MCP server | [git-mcp-server.md](git-mcp-server.md) | queued | 2026-11-05 |
| Prompt caching / Sonnet 5.5 cache reads | [prompt-caching.md](prompt-caching.md) | queued | 2026-11-05 |
| knowledge-work-plugins `data` (plugin) | [knowledge-work-data.md](knowledge-work-data.md) | queued | 2026-11-05 |
| claude-plugins-community (marketplace) | [claude-plugins-community.md](claude-plugins-community.md) | queued | 2026-11-05 |
| Opus 5.5 fast mode + SDK computer-use classes | [opus-fast-mode.md](opus-fast-mode.md) | queued | 2026-11-05 |

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
