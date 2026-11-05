# Anthropic SDK majors and `/claude-api api-version`

Source: [Claude release notes](https://platform.claude.com/docs/en/release-notes/overview) · Type: Claude Code command + SDK upgrade

## What it is for
Late October 2026 shipped breaking SDK majors (Python 2.0.0, TypeScript 1.0.0, Go 2.0.0, Java 3.0.0) and API version 2026-10-21. The SDKs and the `ant` CLI are now Apache 2.0. Claude Code 2.1.307 added `/claude-api api-version` to migrate code to a newer API version.

## When to reach for it
Any project that calls the Claude API and needs to move to the new SDK major or API version.

## Commands that matter
- Update Claude Code, then in the project: `/claude-api api-version`.
- Read the migration guide linked from the release notes first.

## First exercise (about 20 minutes)
1. On a throwaway branch of a small SDK project, run the tests once so you know they pass.
2. Run `/claude-api api-version`.
3. Read the whole diff, run the tests, and fix what fails.

## How you know it worked
The tests pass on the new SDK major and you can explain every change in the diff.

## Common mistake
Merging the bump without reading the diff. Breaking changes can hide in places the tests don't cover.
