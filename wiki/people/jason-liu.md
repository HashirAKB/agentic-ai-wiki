# Jason Liu

**Who:** Independent consultant on RAG and LLM applications, creator of the Instructor library (structured outputs), teaches a course on systematically improving RAG. His current employer is reported inconsistently across sources, so it is not recorded here.
**Why credible:** Ships a widely used open-source library and consults for production AI teams; writes from that practice at [jxnl.co](https://jxnl.co/writing/).
**Ingested:** 2026-11-09 (two posts)
**Related:** [Core concepts](../concepts/core-concepts.md), [Hamel Husain](hamel-husain.md), [Eugene Yan](eugene-yan.md), [Chip Huyen](chip-huyen.md)

## Key practices
### Systematically improving RAG
Source: https://jxnl.co/writing/2024/05/22/systematically-improving-your-rag/
- Start with synthetic data: generate the questions each chunk should answer and check retrieval finds that chunk. This gives a baseline before any user traffic and shows which retrieval changes help.
- Measure each change on recall and latency together; how much latency is acceptable depends on the stakes.
- Segment real queries by topic and by capability (tables, comparisons, deadlines), with domain experts naming the clusters. Prioritize clusters by volume times dissatisfaction, and watch for traffic shifts (his example: one query type jumping from 2% to 80% after onboarding a client).
- Make feedback questions specific ("did we answer the question correctly?") instead of vague thumbs, then fold the answers into the eval set and re-cluster regularly.
- Extract metadata (dates, owners) and use hybrid full-text plus vector search; text similarity alone cannot answer "latest" style questions.

### Only six RAG evals
Source: https://jxnl.co/writing/2025/05/19/there-are-only-6-rag-evals/
- A RAG system is question, context, answer. Judging each ordered pair gives six checks: context relevance, faithfulness (answer vs context), answer relevance, context support coverage, question answerability, self-containment.
- Tier them: cheap non-LLM retrieval metrics (precision, recall, MRR) daily; the first three LLM-judged checks as the core; the rest for monthly or release reviews.
- Use the failing pair to diagnose: wrong answer points to faithfulness, off-topic to answer relevance, missing facts to context relevance or support.
- Weight by domain: medical leans on faithfulness, support on answer relevance, docs on answerability.

## Open questions
- His blog index lists posts arguing coding agents do better with grep and direct exploration than with embedding RAG, and that multi-agent setups are fragile. They cite other teams' experience (Augment, Cline, Cognition) and are not yet read; the multi-agent claim overlaps with the subagent disagreement in core concepts.

## Still to ingest
- RAG series index, "Grep beats embeddings", "No multi-agents", "AI from the trenches", Instructor docs, career advice.
