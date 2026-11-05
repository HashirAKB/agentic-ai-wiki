# OpenTelemetry export for the Messages API and Managed Agents (beta)

Source: [Claude release notes](https://platform.claude.com/docs/en/release-notes/overview) · Type: SDK feature

## What it is for
The SDKs (seven languages) can emit OpenTelemetry spans for API requests and agent sessions, so you can see each model call and tool call as a trace.

## When to reach for it
Debugging an agent, or building evals from real traces (see [Hamel Husain](../wiki/people/hamel-husain.md) on reading your data).

## Commands that matter
- Follow the SDK observability docs to turn on export.
- Run a local collector and viewer, e.g. Jaeger: `docker run -p 16686:16686 -p 4317:4317 jaegertracing/all-in-one`.

## First exercise (about 20 minutes)
1. Start the local collector.
2. Turn on export in a small script that makes one tool-using call.
3. Open the trace and walk through the span tree.

## How you know it worked
Each tool call shows up as its own span, with timing.

## Common mistake
Sending spans to a hosted backend without thinking. Traces contain prompts and user data; keep the collector local unless you have scrubbed them.
