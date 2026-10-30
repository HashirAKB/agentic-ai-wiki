# Hamel Husain (with Shreya Shankar)

**Who:** ML engineer and consultant on LLM products; co-teaches the AI Evals course and co-wrote an O'Reilly book on evals with Shreya Shankar (UC Berkeley researcher).
**Why credible:** Practitioner advice drawn from many client deployments; widely cited.
**Ingested:** 2026-10-30 (FAQ overview)
**Related:** [Core concepts](../concepts/core-concepts.md)

## Key practices (LLM Evals FAQ)
- **Start with error analysis, not infrastructure.** Minimum viable setup: spend ~30 minutes manually reviewing 20 to 50 outputs whenever you make a significant change.
- **Error analysis is the most important eval activity.** It tells you which evals to write. Process: gather representative traces (synthetic if you have none), write raw observations on each, group them into failure modes, count them, fix the most frequent first.
- Many failures found this way are plain bugs; fix them directly without building eval infrastructure.
- Use one domain expert as the quality decision-maker (a "benevolent dictator") rather than a committee.
- Prefer binary pass/fail judgments with written critiques over vague 1 to 5 scores. Validate any LLM-as-judge against human labels.
- Generic off-the-shelf metrics are often counterproductive; build application-specific ones from observed failures.
- Repeat error analysis regularly; failure modes shift as the app and users change.
- A simple custom viewer for traces is one of the highest-return investments.

## Links
- https://hamel.dev/blog/posts/evals-faq/

## Still to ingest
- "Your AI product needs evals", "Creating an LLM-as-a-judge", "A field guide to rapidly improving AI products"
