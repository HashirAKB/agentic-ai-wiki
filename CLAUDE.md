# Schema: how this wiki works

Owner: Hashir. Maintainer: Claude. Pattern: Andrej Karpathy's LLM Wiki (April 2026).

## Purpose
A persistent, compounding knowledge base on (1) how to get the most out of AI agents and LLMs, and (2) how Hashir can position himself as a strong agentic AI developer. Claude reads it before helping with agentic work and adds to it on a daily scheduled run.

## Layout
- `CLAUDE.md` (this file): conventions and workflows.
- `index.md`: every page with a one-line summary. Read it first on every query.
- `log.md`: append-only timeline. Each entry starts with `## [YYYY-MM-DD] ingest|query|lint|setup | Title`.
- `queue.md`: sources still to research, in priority order, with status.
- `proposals.md`: suggested changes to how Claude works with Hashir (preferences, skills), waiting for his approval.
- `wiki/people/<name>.md`: one per practitioner. Who they are, why credible, key practices, links, still-to-ingest.
- `wiki/concepts/<concept>.md`: cross-cutting ideas.
- Personal pages (how the knowledge applies to Hashir: career positioning, portfolio, his projects) do NOT live in this repo. They are Google Docs prefixed `H - ` in the private Drive folder "Agentic AI Wiki".

Link pages with relative markdown links, e.g. `[Karpathy](../people/andrej-karpathy.md)`.

## Rules for Claude
0. **This repo is public.** Never write anything personal about Hashir here: job search status, employers' internal details, compensation, notice periods, health, or his private plans. That belongs in the private Drive folder.
1. Credibility bar: practitioners who build and ship (lab engineers, tool creators, respected independent builders). Prefer primary sources (their own blog, posts, talks, docs) over summaries. Skip hype accounts.
2. Paraphrase in your own words. Quotes under 15 words, at most one per source. Always link the source.
3. Extend an existing page before creating a new one. Never silently overwrite a claim; if sources disagree, record both under "Open questions".
4. Every ingest: update the person page, update or create affected concept pages, update `index.md`, append to `log.md`, update `queue.md`.
5. Keep what a source said separate from Claude's application to Hashir (applications go in the private Drive `H - ` docs).
6. Weekly lint (Sundays): contradictions, stale claims, orphan pages, missing concept pages, gaps worth a search.
7. Durable practices that should change how Claude behaves go into `proposals.md` for Hashir to approve. Never change Claude's settings directly.
8. Commit with a short message per run, e.g. `ingest: Simon Willison red/green TDD`. Push to `main`.
