# Opus 5.5 fast mode and SDK computer-use classes

Source: [Claude release notes](https://platform.claude.com/docs/en/release-notes/overview) · Type: API feature

## What it is for
Fast mode on Opus 5.5 is now generally available (no beta header). The Python and TypeScript SDKs gained browser and computer-use classes. Fast mode for Opus 4.8 is removed on 2026-11-30.

## When to reach for it
Interactive loops where latency matters; quick computer-use prototypes.

## Commands that matter
- Set `speed: "fast"` on Opus 5.5 requests (check pricing first).
- See the SDK docs for the browser and computer-use classes.

## First exercise (about 15 minutes)
1. Send the same prompt in normal and fast mode.
2. Compare latency, output and cost.

## How you know it worked
You have numbers for both and know when fast mode is worth it.

## Common mistake
Running computer use on untrusted pages outside a sandbox. Use a container or VM.
