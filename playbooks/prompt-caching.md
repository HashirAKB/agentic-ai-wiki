# Prompt caching (cheaper cache reads on Sonnet 5.5)

Source: [Claude release notes](https://platform.claude.com/docs/en/release-notes/overview) · Type: API practice

## What it is for
Cache reads on Sonnet 5.5 dropped from $0.20 to $0.10 per million tokens on 2026-10-07. Agent loops that resend a stable prefix (system prompt, tool definitions, long context) get much cheaper when that prefix is cached.

## When to reach for it
Any agent loop or repeated call with a long, stable prefix.

## Commands that matter
- Put stable content first: tools, then system prompt, then the conversation.
- Set `cache_control` breakpoints at the end of the stable part.
- Read `usage.cache_creation_input_tokens` and `usage.cache_read_input_tokens`.

## First exercise (about 15 minutes)
1. Send the same long prompt twice with a cache breakpoint.
2. Compare the usage fields on both calls.

## How you know it worked
The second call shows `cache_read_input_tokens` above zero.

## Common mistake
Putting changing content (timestamps, user IDs) before the breakpoint, which breaks the cache every call.
