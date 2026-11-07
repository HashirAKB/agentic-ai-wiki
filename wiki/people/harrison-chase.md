# Harrison Chase / LangChain team

**Who:** Co-founder and CEO of LangChain (LangChain, LangGraph, LangSmith). The source ingested here is published under "LangChain Team", not under his name, so claims are attributed to the team.
**Why credible:** Builds widely used agent frameworks and observability tooling, and the post synthesizes work from Anthropic, Cognition, Windsurf and Karpathy with concrete implementations. Caveat: the post is also a vendor's guide (it recommends LangSmith/LangGraph).
**Ingested:** 2026-11-07 (Context Engineering for Agents, 2025-07-02)
**Related:** [Core concepts](../concepts/core-concepts.md), [Anthropic Engineering](anthropic-engineering.md), [Andrej Karpathy](andrej-karpathy.md), [Simon Willison](simon-willison.md), [Hamel Husain](hamel-husain.md)

## Key practices (Context Engineering for Agents)
Source: https://www.langchain.com/blog/context-engineering-for-agents
- **Framing:** borrows Karpathy's analogy of LLM as CPU and context window as RAM. Context covers instructions, knowledge and tool feedback. Long agent runs grow tokens quickly, raising cost, latency and error rates.
- **Failure modes** (citing Drew Breunig): poisoning (a hallucination enters context), distraction, confusion (superfluous context), clash (conflicting context).
- **Write:** persist information outside the window. Scratchpads (file or state field) within a task, memories across sessions. Example: Anthropic's researcher saves its plan so truncation cannot lose it.
- **Select:** pull in only what is relevant: scratchpad reads, memories (few-shot, instructions, facts), tool selection by retrieval over tool descriptions, knowledge retrieval. Simple setups load fixed files (CLAUDE.md, rules files); bigger ones need embeddings or graphs. Risk: wrongly surfaced memories (Willison's location-in-image example). Windsurf notes embedding search degrades on large codebases, so combine AST chunking, grep, graphs and re-ranking.
- **Compress:** summarization (Claude Code auto-compact near 95% capacity, summaries of heavy tool output or at agent handoffs) and trimming (drop old messages by heuristic).
- **Isolate:** sub-agents with their own windows (Anthropic reports better results than a single agent but up to 15x the tokens of chat), sandboxed code execution that returns only selected results, and state schemas exposing only some fields to the model.
- **Process:** trace and track token usage first, then build a simple test of whether a context change helps, then iterate.

## Open questions
- Isolate (multi-agent) vs one agent with good compaction: the post leans on Anthropic's multi-agent gains, while [Willison](simon-willison.md) cautions against many specialists. Cognition (cited) stresses context sharing across agents. Unresolved; token cost is the tradeoff.
- Terminology: Anthropic frames the same ideas as an attention budget; the write/select/compress/isolate split is the team's own taxonomy.

## Still to ingest
- Harrison Chase's own posts and talks on agent architectures; LangGraph docs; Drew Breunig's long-context failure modes post; Cognition's multi-agent critique.
