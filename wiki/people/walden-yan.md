# Walden Yan (Cognition)

**Who:** Co-founder at Cognition, maker of the Devin coding agent.
**Why credible:** Builds and operates a production coding agent. Caveat: vendor post, opinion-based, no benchmarks, and dated June 2025.
**Ingested:** 2026-11-11 (Don't Build Multi-Agents, 2025-06-12)
**Related:** [Anthropic Engineering](anthropic-engineering.md), [Harrison Chase / LangChain](harrison-chase.md), [Drew Breunig](drew-breunig.md), [Simon Willison](simon-willison.md), [Core concepts](../concepts/core-concepts.md)

## Key practices
Source: https://cognition.com/blog/dont-build-multi-agents
- **Share context:** give a subagent the full trace, not just a task message, since the message omits earlier decisions.
- **Actions carry implicit decisions:** parallel agents act on different hidden assumptions and their outputs clash (his illustrative example: one agent builds a background, another a mismatched bird).
- **Default architecture:** a single-threaded linear agent. For long tasks, add a compression model that condenses history into key events and decisions; he says this is hard and Cognition fine-tuned a smaller model for it.
- **Subagents, where they fit:** Claude Code's then-current subagents answered narrow questions without writing code, keeping investigation out of the main history.
- Calls context engineering effectively the number one job of agent builders.

## Open questions
- Conflicts with Anthropic's multi-agent research results; see [core concepts](../concepts/core-concepts.md). The post carries no data, so the disagreement is unresolved.
