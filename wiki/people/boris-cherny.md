# Boris Cherny

**Who:** Created Claude Code at Anthropic (started as a side project in Sep 2024).
**Why credible:** Builds the tool and ships heavily with it daily.
**Ingested:** 2026-10-30 (via write-ups of his Jan 2026 X threads; primary threads still to read)
**Related:** [Core concepts](../concepts/core-concepts.md)

## Key practices
- **Parallel sessions:** runs about five Claude Code sessions in numbered terminal tabs with system notifications, plus more in the browser. The Claude Code team calls parallel work with git worktrees its biggest productivity unlock.
- **Strongest model with thinking:** prefers the top model with extended thinking over faster small models, because fewer correction loops save time overall.
- **Plan first:** starts complex tasks in plan mode and iterates on the plan until it's right, then lets it implement, often in one shot.
- **Shared CLAUDE.md in git:** whenever Claude does something wrong, add a rule so it doesn't repeat. During PR review, tag Claude to add learnings to CLAUDE.md ("compounding engineering").
- **Slash commands** for every repeated inner-loop workflow (e.g. commit, push, open PR), checked into the repo.
- **Subagents** for recurring jobs, e.g. a code simplifier after work is done and a verify-app agent that tests end to end.
- **Hooks:** a post-tool-use hook to auto-format code.
- **Permissions:** pre-allow known-safe commands rather than skipping permission checks.
- **Give Claude a way to verify its work** (tests, browser, running the app). This closes the loop and raises quality.
- **Learning mode:** use explanatory output styles, or ask for an HTML presentation to understand unfamiliar code.

## Links
- https://x.com/bcherny/status/2017742741636321619
- https://threadreaderapp.com/thread/2007179832300581177.html

## Still to ingest
- Original threads in full; his talk on mastering Claude Code
