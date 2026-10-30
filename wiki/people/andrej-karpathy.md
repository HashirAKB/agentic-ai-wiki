# Andrej Karpathy

**Who:** Founding member of OpenAI, former Director of AI at Tesla (Autopilot vision), designed Stanford CS231n, now runs Eureka Labs and makes AI education videos. Coined "vibe coding" (Feb 2025) and pushed "agentic engineering" (2026).
**Why credible:** Has trained frontier models and shipped production AI; writes from daily hands-on use.
**Ingested:** 2026-10-30
**Related:** [Core concepts](../concepts/core-concepts.md)

## Key practices

### Coding with agents (X post, 27 Jan 2026)
- Went from ~80% manual coding to ~80% agent coding in a few weeks (Nov to Dec 2025). Calls it his biggest workflow change in two decades.
- Agents' mistakes are now conceptual, not syntax: wrong assumptions made silently, no clarifying questions, no surfacing of inconsistencies or tradeoffs, no pushback, sycophancy.
- They overcomplicate: bloated abstractions, dead code left behind, edits to unrelated code. Asking "couldn't you just do X?" often cuts 1000 lines to 100.
- Watch code you care about closely in an IDE beside the agent. His setup: a few Claude Code sessions on the left, IDE on the right.
- Leverage comes from declarative goals: give success criteria, have it write tests first then pass them, put it in a loop with a browser, write the naive correct version then optimize.
- Warns about skill atrophy: writing code and reading code are different abilities.

### Agentic engineering vs vibe coding (Sequoia Ascent, Apr 2026)
- Vibe coding raises the floor (anyone can build). Agentic engineering raises the ceiling: coordinating fallible agents while keeping correctness, security, taste and maintainability.
- The human owns spec, design and oversight. Example: his agent matched Stripe payments to Google accounts by email; the correct design needed persistent user IDs.
- You can forget API details (dim vs axis) but must understand fundamentals (storage, views, invariants, identity, security boundaries).
- Hiring should test this directly: build a substantial project with agents, deploy it, secure it, then let adversarial agents try to break it.
- Build agent-native surfaces: markdown docs, CLIs, APIs, MCP servers, copy-pasteable agent instructions instead of "click here" docs.

### Verifiability and jagged intelligence (blog, Nov 2025)
- Software 1.0 automates what you can specify; LLMs/RL automate what you can verify (resettable, efficient, rewardable).
- Models spike where tasks are verifiable and labs invest training effort (code, math) and stay rough elsewhere. Check whether your task is "on the model's rails"; if not, add context, tools, evals or fine-tuning.

### Context engineering (X, Jun 2025)
- Preferred "context engineering" over "prompt engineering": filling the context window with just the right information for the next step. Real LLM apps also handle orchestration of LLM calls, generation-verification UX, guardrails, evals and cost tradeoffs. "ChatGPT wrapper" is the wrong mental model.

### Partial autonomy (YC AI Startup School, Jun 2025)
- Build "Iron Man suits", not robots: AI generates, human verifies, with an autonomy slider. Keep AI on a leash: small concrete chunks, fast verify loops.

### Daily-use tips
- **Ramble sessions (X, Jul 2026):** switch to voice and ramble for ~10 minutes to give the model the bits it needs; LLMs reconstruct messy rambles well and the shared understanding improves.
- **Better output formats (X, Oct 2026):** for understanding, ask for controlled-language writing (ASD-STE100 style), diagrams, interactive HTML pages, or bespoke explainer videos.
- **Capability gap (X, Apr 2026):** free and old models mislead people; frontier gains are peaky in technical, verifiable domains. Use the best agentic tools for technical work.
- **LLM Wiki (gist, Apr 2026):** compile sources into a persistent wiki (raw, wiki, schema; ingest, query, lint). This repo is built on it.
- **Append-and-review note (blog, Mar 2025):** one single note; append ideas at the top; periodically scroll down and rescue what matters.

### Education
- You can outsource thinking but not understanding; the human still directs.
- Learning path: Zero to Hero (micrograd to GPT), Deep Dive into LLMs, How I use LLMs, microGPT.

## Links
- https://x.com/karpathy/status/2015883857489522876
- https://karpathy.bearblog.dev/sequoia-ascent-2026/
- https://karpathy.bearblog.dev/verifiability/
- https://karpathy.bearblog.dev/year-in-review-2025/
- https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
- https://x.com/karpathy/status/2079610838143623371
- https://x.com/karpathy/status/2105819303471976479
- https://x.com/karpathy/status/2042334451611693415
- https://karpathy.ai

## Still to ingest
- Dwarkesh podcast 2025 (current limits of agents)
- How I use LLMs video (full)
- Animals vs Ghosts, The space of minds, Power to the people, Vibe coding MenuGen
- nanochat / microGPT repos
