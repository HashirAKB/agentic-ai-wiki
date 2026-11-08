# Addy Osmani

**Who:** Engineer and author on developer tooling and AI-assisted engineering; his site lists him as working on Claude Code at Anthropic (earlier career at Google Chrome/Cloud). Author of the open-source Agent Skills repo and an upcoming O'Reilly book on agentic engineering.
**Why credible:** Ships tooling, speaks at AI Engineer events, and writes a steady run of long-form posts on running coding agents in real teams.
**Ingested:** 2026-11-08 (Own the Outer Loop, Audit your Agent files, Agentic Skill Decay; feed titles for the rest)
**Related:** [Core concepts](../concepts/core-concepts.md), [Simon Willison](simon-willison.md), [Boris Cherny](boris-cherny.md), [Karpathy](andrej-karpathy.md)

## Key practices
### Own the outer loop ([post](https://addyosmani.com/blog/own-the-outer-loop/))
- Agents run the inner loop (investigate, implement, verify). Humans own the outer loop: the boundary where output enters production.
- Three terms: **quality** (checks installed beforehand that produce evidence), **verdict** (the human ship/block/narrow decision), **answerability** (someone can explain what changed and why it was safe).
- Hidden costs of delegation: cognitive surrender (accepting output unexamined), cognitive debt (understanding erodes), orchestration tax (human attention does not parallelize).
- Apply back pressure: types, tests, hooks, sandbox limits, audit logs. Let an independent check, not the model's claim, decide "done". Give agents only enough autonomy for these signals to work.
- Brownfield: turn runbooks, edge cases and past incidents into explicit constraints and tests. Limit coupling with worktrees and scoped tasks.

### Audit your agent files ([post](https://addyosmani.com/blog/audit-your-agent-files/))
- Agent config decays as models and codebases change. Re-audit roughly monthly; make each rule justify itself again.
- Claude Code's `/doctor` flags unused skills, MCP servers, slow hooks and duplicated or inferable CLAUDE.md content; `/memory` reviews stale preferences. Treat output as triage.
- Keep context files near 200 lines, with only what the model cannot infer (how to run checks, expensive operations, generated files, odd conventions). Point at real code rather than prose summaries.
- Snapshot, remove, then test a real task without the skills; keep a skill if the run fails in exactly the way it was written to prevent. Unused skills cost confusion more than tokens.
- Hard constraints belong in tests, hooks or permissions.

### Agentic skill decay ([post](https://addyosmani.com/blog/agentic-skill-decay/))
- Agents let you skip the reps that built expertise. Practice decision making, specifying, steering and verifying deliberately.
- Habits: predict the solution before prompting, ask the agent why it chose an approach, read the diff and predict failures, ask for explanations, work some problems by hand, mine finished tasks for lessons, and codify lessons as lint rules, types or tests.
- He cites an Anthropic study where AI-assisted juniors scored lower on a quiz, except those who asked conceptual questions (he notes it was short and narrow).

### Other posts seen by title only (to read)
Software Factories, Light and Dark (light keeps humans in loop, dark removes them); Practical Loop Engineering; Agentic Code Quality; Earning taste and judgment; The Agent-Era Career; Brownfield Agentic Engineering. Index: [RSS feed](https://addyosmani.com/rss.xml).

## Open questions
- His skill-audit advice (remove rules, test without them) sits alongside his own large Agent Skills repo; his stance is that installing and keeping are separate decisions, not that skills are bad.
- Search results gave conflicting employer info (Google vs Anthropic); his own site is taken as current.

## Still to ingest
- Software Factories, Practical Loop Engineering, Agentic Code Quality, Agent-Era Career, Brownfield, Loop Engineering (June 2026), Agent Skills repo README.
