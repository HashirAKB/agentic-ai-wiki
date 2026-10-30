# Anthropic Engineering blog (Applied AI team)

**Who:** The team behind Claude, Claude Code and the Agent SDK, publishing how they build agents internally.
**Why credible:** Primary source from a frontier lab, based on production systems.
**Ingested:** 2026-10-30 (summaries; full posts still to read)
**Related:** [Core concepts](../concepts/core-concepts.md)

## Effective context engineering for AI agents (Sep 2025)
- Context engineering is the natural progression of prompt engineering: curating everything that enters the model's context, not just the instruction wording.
- Working definition of an agent: an LLM autonomously using tools in a loop.
- Treat context as a finite attention budget. Aim for the smallest set of high-signal tokens that produces the outcome.
- Write system prompts at the "right altitude": neither brittle hard-coded logic nor vague.
- Long-horizon techniques: compaction (summarize and restart), structured note-taking outside the context window, and sub-agents that keep detailed search context isolated while the lead agent synthesizes.

## Related posts (to ingest)
- Building effective agents (Dec 2024): workflows vs agents, start simple, composable patterns
- How we built our multi-agent research system
- Effective harnesses for long-running agents
- Code execution with MCP
- Demystifying evals for AI agents
- Writing tools for agents

## Links
- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- https://www.anthropic.com/engineering
