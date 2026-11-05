# Chip Huyen

**Who:** ML/AI engineer, author of *AI Engineering* (O'Reilly) and *Designing Machine Learning Systems*.
**Why credible:** Long record building ML platforms and teaching production ML; writes from primary experience.
**Ingested:** 2026-11-05 (agents post)
**Related:** [Core concepts](../concepts/core-concepts.md), [swyx](swyx.md), [Anthropic Engineering](anthropic-engineering.md)

## Key practices (Agents post)
Source: https://huyenchip.com/2025/01/07/agents.html
- An agent is defined by its environment and the actions it can take; the model is the planner that decides steps and when to stop.
- Three tool types: knowledge augmentation (retrieval, search, APIs), capability extension (calculator, code interpreter, other models), and write actions (email, transfers) which need the strongest safeguards.
- Separate plan generation from execution, so plans can be validated by heuristics, an AI judge or a human before running. Plans can be sequential, parallel, conditional or looping.
- Reflect at several points: after the request, the plan, each step and completion. ReAct and Reflexion help but cost latency and tokens.
- Failure modes: invalid tools or parameters, plans that miss constraints, falsely declaring success, wrong tool outputs, too many steps or cost.
- Evaluating agents: build tasks with tool inventories, sample several plans per task, measure the validity rate and attempts needed, test tools independently, log every call, run ablations, and compare efficiency with a human baseline.

## Open questions
- Whether LLMs truly plan (backtracking, outcome prediction) is debated; she treats them as useful components inside a larger planner.

## Still to ingest
- *AI Engineering* book themes, her evaluation and RAG posts.
