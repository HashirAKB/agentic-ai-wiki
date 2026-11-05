# Long multi-agent Claude Code runs

Source: [Simon Willison, 2026-10-16](https://simonwillison.net/2026/Oct/16/sqlite-sparql-rust/) · Type: workflow

## What it is for
Willison reports a Rust SQLite extension built in about 12 hours by Claude Code for web in a multi-agent mode. It's a worked example of how much a well-specified task with a strong test suite can run on its own.

## When to reach for it
A task with a clear spec and a test suite that can judge success without you (a parser, a format converter, a port).

## Commands that matter
None. Read the post for his prompt and setup, and see [Anthropic engineering](../wiki/people/anthropic-engineering.md) on long-running harnesses.

## First exercise (about 15 minutes)
1. Read the post and note his spec, his tests and how he checked the result.
2. Take one of your own task specs and list what it lacks next to his.

## How you know it worked
You have a list of concrete gaps in your spec (missing tests, unclear done-criteria, unstated constraints).

## Common mistake
Starting a long run without tests strong enough to catch wrong output. Long runs also cost a lot; set a budget.
