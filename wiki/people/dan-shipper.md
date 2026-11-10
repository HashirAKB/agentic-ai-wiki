# Dan Shipper / Every (compound engineering)

**Who:** Dan Shipper is CEO of Every, a media and software company. The compound engineering method was written up with Kieran Klaassen, who runs the Cora product at Every and built the open-source plugin.
**Why credible:** Every ships real products with agents writing nearly all the code and publishes the workflow plus an MIT-licensed plugin. Caveat: productivity claims are their own experience, not independently measured.
**Ingested:** 2026-11-10
**Related:** [Core concepts](../concepts/core-concepts.md), [Boris Cherny](boris-cherny.md), [Simon Willison](simon-willison.md)

## Compound engineering: the loop
Source: [Compound Engineering: How Every Codes With Agents](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents).

1. **Plan:** agents research the codebase, its history and outside best practice, then write a plan with goals, architecture, approach and success criteria.
2. **Work:** agents turn the plan into tasks and build, testing their own output in a browser or simulator.
3. **Assess:** linters, tests, manual checks and review agents (one setup runs about a dozen parallel reviewer subagents for security, performance, overbuilding). The developer decides what to fix.
4. **Compound:** bugs, solutions and architectural guidance are written back as rules or prompts so every future agent and new teammate inherits them.

- **Effort split:** roughly 80% on planning and review, 20% on work and compounding. The bottleneck moves to deciding what to build and defining "good".
- **Plans as files or issues** build shared understanding before any code is written.
- **Plugin:** the open-source compound-engineering plugin packages the loop as commands and skills; learnings are stored in the repo (reported as `docs/solutions/`, per secondary sources).

## Open questions
- Evidence: no public benchmark compares this loop against plain disciplined agent use; the "one developer does the work of five" claim is testimony.
- Planning overhead matters less for small projects as models improve (the article itself says so).
- Secondary sources say the plugin is tied to Every's Rails/Cora stack and that the guide and repo have diverged; I could not fetch the plugin docs (404), so verify before adopting.

## Still to ingest
- Plugin README and current command list; Kieran Klaassen's own posts; Shipper's podcast episodes (AI & I)
