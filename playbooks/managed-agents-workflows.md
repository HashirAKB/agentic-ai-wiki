# Managed Agents dynamic workflows (beta)

Source: [Claude release notes](https://platform.claude.com/docs/en/release-notes/overview) · Type: API feature

## What it is for
Server-side multi-agent orchestration for Managed Agents sessions, without writing your own loop. Turned on with `"multiagent": {"type": "multiagent_20261001", "workflows": {"type": "enabled"}}`; runs report `workflow_run.*` events.

## When to reach for it
A task that splits into parallel or staged sub-tasks (research, then synthesis) where you would otherwise hand-write an orchestrator.

## Commands that matter
- Add the config above to a Managed Agents session (check the docs for the current shape; it's beta).
- Watch the `workflow_run.*` events in the stream.

## First exercise (about 30 minutes)
1. Read the docs page for dynamic workflows.
2. Run a two-step research task with workflows on.
3. Read the event stream end to end.

## How you know it worked
You can trace each workflow step from the events and say which agent did what.

## Common mistake
Leaving it on for small tasks. Multi-agent runs burn tokens quickly; set a budget and use it only when the task needs it.
