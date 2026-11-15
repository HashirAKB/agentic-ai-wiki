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

## Your AI product needs evals (ingested 2026-11-04)
Source: https://hamel.dev/blog/posts/evals/
- Products fail mostly because they lack an eval system, not because of the model. The same system powers debugging and fine-tuning data.
- Three levels, costliest last: (1) unit tests, cheap assertions run on every change; (2) human and LLM-judge review of logged traces on a cadence; (3) A/B tests for mature products.
- Unit tests: scope by feature and scenario (one match, many, none), add generic ones (e.g. regex that internal IDs never leak), have an LLM generate test inputs, keep them hard and updated. A 100% pass rate is not required; the target is a product decision.
- Human review: build a simple domain-specific viewer (Gradio, Streamlit) showing everything on one screen, make outputs editable, start with binary good/bad, and read data until you stop learning new things.
- LLM judge: align mainly through prompt iteration against human labels, measure precision and recall rather than raw agreement (class imbalance), and re-check periodically.
- Synthetic data: use an LLM to brainstorm realistic inputs, filter with your assertions and judge, then curate by hand. Fine-tuning suits style, syntax and rules; RAG suits fresh facts.
- Pitfalls: prompt whack-a-mole, vibe checks only, skipping unit tests, generic frameworks, buying tools too early, too little data reading, treating evals as done.

## Using LLM-as-a-Judge: critique shadowing (ingested 2026-11-12)
Source: https://hamel.dev/blog/posts/llm-judge/
1. Name one principal domain expert (founder or CEO in small firms; a solo dev must be honest about their expertise). Not a proxy such as a manager.
2. Build a dataset along features, scenarios and personas, mixing logs with synthetic user inputs (the LLM generates inputs only, never AI responses). Generate until no new failure modes appear.
3. The expert answers "did the AI achieve the desired outcome?" as pass/fail plus a detailed written critique usable as a few-shot example, with all context on one screen. About 30 examples to start; about 100 per failure mode to validate a judge.
4. Fix obvious errors first, then re-review.
5. Build the judge only after seeing data (criteria drift: writing criteria and reading outputs shape each other). Iterate the prompt against the expert's labels; report true positive and true negative rates, since an always-Pass judge shows 95% agreement when failures are rare.
6. Validate like a classifier: train split (10-20%) supplies few-shot examples, dev split (40-45%) for prompt revision, test split (40-45%) used once with a frozen prompt.
7. Run on unseen data, classify failures into root causes, fix, repeat. Build specialized judges only for persistent failure modes; code assertions suffice for some. Write a test for every fixed error.
- Judge model: the most capable you can afford; humans can shrink to sampling but not leave. Rerun the process after model updates. The judge's main value is pushing people to read their data.

## A field guide to rapidly improving AI products (ingested 2026-11-15)
Source: https://hamel.dev/blog/posts/field-guide/ (Mar 2025; also republished by [O'Reilly](https://www.oreilly.com/radar/a-field-guide-to-rapidly-improving-ai-products/))
- Teams chase tools and generic metrics; instead read real conversations, note failures, group them into a taxonomy, count, and fix the top categories (in one case three issues caused over 60% of problems).
- A custom data viewer (full context on one screen, one-click pass/fail, notes, filters, keyboard shortcuts) is the highest-value investment; AI-assisted coding builds one in hours, and a spreadsheet is a fine start.
- Let domain experts edit prompts directly, ideally in an admin mode inside the real product. Talk to them in concrete capabilities, not buzzwords like "agent" or "RAG".
- Bootstrap evals with synthetic inputs (never expected outputs) across features, scenarios and personas, grounded in real data; check each case triggers its intended scenario.
- Evals drift as reviewers see more outputs, so treat criteria as living. Binary judgments plus written critiques; use critiques as few-shot examples for judges; recheck judges against human labels (one team passed 90% agreement after three rounds).
- Roadmaps: plan around experiments, not features. Use a capability funnel (valid output up to fully solving the problem), time-box exploration with decision points, share failures, and count experiments run as the progress metric.

## Links
- https://hamel.dev/blog/posts/llm-judge/
- https://hamel.dev/blog/posts/field-guide/

## Still to ingest
- Later parts of the series on error analysis and sustained improvement loops
