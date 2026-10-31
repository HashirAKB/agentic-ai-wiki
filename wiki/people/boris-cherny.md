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

## Claude Code best-practices docs (team guidance, 2026-10-31)
Source: [Best practices for Claude Code](https://code.claude.com/docs/en/best-practices). Written by the Claude Code team, not Boris personally; it matches his practices above and adds detail.
- **Deterministic vs non-deterministic instructions:** prompts, CLAUDE.md and skills are advice the model may skip; hooks, deny rules and managed settings are enforced by the harness. If a CLAUDE.md line keeps being missed even with emphasis, make it a hook. If a hook only encodes a preference, delete it.
- **Only write what Claude can't see:** for each CLAUDE.md line ask: could it find this by reading the code, and would it actually look? If yes to both, drop it. Keep exact test/typecheck/lint commands, misleading code areas, decisions not in the repo, and anything corrected twice. Stay under about 200 lines; scope rules to paths with `.claude/rules/`.
- **Give Claude a pass/fail check** and ask for evidence (command and output), not a bare "all tests pass". Options from soft to hard: a prompt to loop until green, a `/goal` condition judged by a separate model, a Stop hook that blocks finishing until typecheck passes, review by a fresh subagent that never saw the conversation.
- **Interview first:** for vague features, ask Claude to interview you and write a SPEC.md, then build in a fresh session. Review against the spec and say to skip style, because a reviewer asked to find problems always finds something.
- **Be specific:** name the file, the symptom and what "fixed" looks like. Saying "be ambitious" helps when you want edge cases and follow-ons, since Claude reads requests conservatively.
- **Skills over CLAUDE.md for procedures:** only name and description load each session; mark side-effect workflows (e.g. release) as manual-only.
- **Trim MCP servers:** connected servers add tool descriptions to context even when unused; prefer a CLI (e.g. `gh`) when one exists.

## Links
- https://code.claude.com/docs/en/best-practices
- https://x.com/bcherny/status/2017742741636321619
- https://threadreaderapp.com/thread/2007179832300581177.html

## Still to ingest
- Original X threads in full (X blocks fetching; use thread mirrors); his talk on mastering Claude Code
- Docs pages on hooks, subagents, skills, `/goal`
