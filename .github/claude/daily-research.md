# Daily research run

You are maintaining this wiki, a public knowledge base built on Karpathy's LLM Wiki pattern. It collects best practices from credible AI practitioners on building and working with AI agents and LLMs.

1. Read `CLAUDE.md` (rules and layout), `index.md` and `queue.md`. Follow `CLAUDE.md` exactly. Run `date` to get today's date.
2. Take the top one or two TODO items from `queue.md`. Research them from primary sources (the person's own blog, posts, docs, talks) with WebSearch and WebFetch. If X/Twitter pages are blocked, use search snippets or thread mirrors. Skip hype and low-credibility summaries.
3. Ingest: update or create `wiki/people/<name>.md`, update `wiki/concepts/` with new cross-cutting ideas, update `index.md`, append to `log.md` (`## [YYYY-MM-DD] ingest | Title`), and update `queue.md` (mark DONE with date; add newly found credible sources at the right priority). Your own words; quotes under 15 words, at most one per source; always link sources. Extend before creating; record disagreements under "Open questions".
4. On Sundays, also lint: contradictions, stale claims, orphan pages, missing concept pages, gaps. Fix what you can and log it as `lint`.
5. Practices that should change how Claude works with the wiki owner, or workflows worth a skill, go into `proposals.md` under "Pending" with source and suggested wording.
6. This repo is public. Never write anything personal about the owner.
7. Check that every relative markdown link points at a file that exists.
8. Commit all changes in one commit (`ingest: <short title>`, or `lint: ...` on Sundays) and `git push`. If the push is rejected, `git pull --rebase` and push again.
9. End with a 3-5 line summary of what you researched and the most useful new insight.

Only edit files in this repository. Do not edit anything under `.github/`.
