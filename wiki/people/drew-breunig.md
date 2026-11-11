# Drew Breunig

**Who:** Independent writer and practitioner on applied AI and data (blog dbreunig.com). His context-failure taxonomy is cited by the LangChain team and others.
**Why credible:** Grounds each failure mode in a named study or a vendor technical report rather than opinion. Caveat: he mostly synthesizes other people's results; he does not run his own benchmarks in these posts.
**Ingested:** 2026-11-11 (How Contexts Fail, 2025-06-22; How to Fix Your Context, 2025-06-26)
**Related:** [Harrison Chase / LangChain](harrison-chase.md), [Anthropic Engineering](anthropic-engineering.md), [Walden Yan / Cognition](walden-yan.md), [Core concepts](../concepts/core-concepts.md)

## Failure modes
Source: https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html
- **Poisoning:** a hallucination lands in context and gets reused. In the Gemini 2.5 report, a Pokémon agent's goals and summary were corrupted and it chased impossible goals for a long time.
- **Distraction:** very long history makes the model repeat past actions instead of planning. Same agent, past roughly 100k tokens. A Databricks study saw Llama 3.1 405b correctness fall from about 32k tokens.
- **Confusion:** extra content, especially extra tools, degrades output. A quantized Llama 3.1 8b failed with 46 tools but passed with 19.
- **Clash:** conflicting information accumulates. A Microsoft/Salesforce study that split prompts across turns saw an average 39% drop; models commit to early assumptions and do not recover.

## Fixes
Source: https://www.dbreunig.com/2025/06/26/how-to-fix-your-context.html
- **RAG:** add only relevant information, even when the window is huge.
- **Tool loadout:** retrieve a small set of tools per task. Cited work: tool confusion beyond about 30 tools; narrowing below 30 gave up to 3x better selection accuracy.
- **Quarantine:** separate contexts per job. Suits breadth-first parallel work (Anthropic's research system), not tightly coupled work.
- **Pruning:** remove irrelevant text with a model or tool; keep instructions and goals in a structured part of context.
- **Summarization:** also a remedy for distraction, not just window limits. Treat it as its own LLM stage so it can be evaluated.
- **Offloading:** scratchpad or "think" tool outside the main flow; Anthropic reported up to 54% gain on a policy-heavy benchmark when paired with a domain prompt.
- Principle: every token shapes behavior, so each must earn its place.

## Open questions
- Numbers come from older, smaller models (Llama 3.1, 2024-25 era); how far they hold for current frontier models is unverified.
