# Lilian Weng

**Who:** AI researcher (formerly OpenAI), writes the Lil'Log blog.
**Why credible:** Long-running, carefully sourced technical surveys; her 2023 agents post became a common reference frame for agent design.
**Ingested:** 2026-11-09 (agents post)
**Related:** [Chip Huyen](chip-huyen.md), [Anthropic Engineering](anthropic-engineering.md), [Core concepts](../concepts/core-concepts.md)

## Key ideas (LLM-Powered Autonomous Agents, June 2023)
Source: https://lilianweng.github.io/posts/2023-06-23-agent/
- Frame: LLM as the brain, supported by planning, memory and tool use.
- Planning: decompose tasks into subgoals (chain of thought, tree of thoughts that branches and searches), or offload to a classical planner (LLM+P). Self-reflection (ReAct's thought/action/observation loop, Reflexion's stored verbal lessons) lets the agent learn from failures.
- Memory: the context window is short-term; an external vector store is long-term, queried by fast approximate nearest-neighbor search.
- Tool use: calculators, search, code, APIs; MRKL-style routing to expert modules. Whether the model picks the right tool and arguments is the crux.
- Stated limits: finite context, weak long-horizon planning and recovery from surprises, and unreliable natural-language interfaces (much agent code is output parsing).

## Notes
- This is a 2023 snapshot; later practice (see [Anthropic](anthropic-engineering.md), [Chip Huyen](chip-huyen.md)) moves toward tool design, context management and evals. Her limits list is still a useful checklist of what harnesses compensate for.

## Still to ingest
- Her later posts (reward hacking, hallucination, reasoning).
