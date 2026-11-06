# Eugene Yan

**Who:** Applied ML/LLM engineer and writer on recommender systems and LLM products.
**Why credible:** Writes from production experience; his posts are widely used as practical references for shipping LLM features.
**Ingested:** 2026-11-06 (Patterns for Building LLM-based Systems & Products)
**Related:** [Core concepts](../concepts/core-concepts.md), [Hamel Husain](hamel-husain.md), [Chip Huyen](chip-huyen.md)

## Key practices (Patterns for LLM-based systems)
Source: https://eugeneyan.com/writing/llm-patterns/
- **Evals:** build task-specific test sets rather than trusting generic benchmarks. Use a strong LLM as judge for open-ended output, but watch for its biases (favoring the first answer, longer answers, its own outputs), and pair with human review.
- **RAG:** retrieve at query time to ground answers and keep knowledge fresh. Combine keyword and embedding search, since embeddings handle names, acronyms and IDs poorly; use metadata filters.
- **Fine-tuning:** needs a real volume of demonstration data and can regress other tasks. Start with small open models and parameter-efficient methods (LoRA/QLoRA).
- **Caching:** semantic-similarity keys risk returning wrong near-matches. Prefer safe keys (item IDs, constrained inputs); it pays off when few requests dominate traffic.
- **Guardrails:** enforce structure directly and use deterministic checks for simple rules; reserve LLM checks for nuanced cases such as harmfulness or faithfulness to sources.
- **Defensive UX:** plan for mistakes. Set expectations, make AI output easy to dismiss, show sources, and prefer constrained interfaces over open chat.
- **User feedback:** collect explicit (thumbs, regenerate) and implicit (accepted or edited suggestions, usage trends) signals as the data flywheel for evals and tuning.

## Open questions
- The post dates from 2023, before agents were mainstream; check which patterns carry over to tool-using agents.

## Still to ingest
- Applied LLMs lessons ("What We've Learned"), eval and LLM-as-judge posts, product evals.
