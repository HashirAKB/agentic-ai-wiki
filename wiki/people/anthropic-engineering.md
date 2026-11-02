# Anthropic Engineering blog (Applied AI team)

**Who:** The team behind Claude, Claude Code and the Agent SDK, publishing how they build agents internally.
**Why credible:** Primary source from a frontier lab, based on production systems.
**Ingested:** 2026-10-30 (context engineering via summaries); 2026-10-30 (Building effective agents, Writing tools for agents read from primary pages); 2026-11-01 (Effective harnesses for long-running agents); 2026-11-02 (multi-agent research system)
**Related:** [Core concepts](../concepts/core-concepts.md)

## Effective context engineering for AI agents (Sep 2025)
- Context engineering is the natural progression of prompt engineering: curating everything that enters the model's context, not just the instruction wording.
- Working definition of an agent: an LLM autonomously using tools in a loop.
- Treat context as a finite attention budget. Aim for the smallest set of high-signal tokens that produces the outcome.
- Write system prompts at the "right altitude": neither brittle hard-coded logic nor vague.
- Long-horizon techniques: compaction (summarize and restart), structured note-taking outside the context window, and sub-agents that keep detailed search context isolated while the lead agent synthesizes.

## Building effective agents (Dec 2024)
- **Workflows** follow predefined code paths (predictable); **agents** direct their own process and tools (flexible, costlier, errors can compound).
- Building block: the augmented LLM (retrieval, tools, memory). Patterns, in rising complexity: prompt chaining, routing, parallelization (sectioning or voting), orchestrator-workers, evaluator-optimizer, then autonomous agents.
- Use the simplest thing that works; add complexity only when it demonstrably improves outcomes. Frameworks can hide prompts and responses, so consider direct API calls first.
- Treat the agent-computer interface like a UI: clear tool descriptions, examples, boundaries between similar tools, and "poka-yoke" design (e.g. requiring absolute file paths removed a class of errors).

## Writing tools for agents
- Build few, well-scoped tools for high-impact workflows, not thin wrappers over every endpoint; consolidate multi-step operations (a `search_logs` tool rather than `read_logs`).
- Namespace related tools; return meaningful natural-language fields over opaque IDs; offer concise vs detailed responses; paginate/filter/truncate with sensible defaults; write actionable error messages.
- Write descriptions like onboarding a new teammate; unambiguous parameter names (`user_id`, not `user`).
- Process: prototype, build realistic eval tasks with verifiable outcomes, run them programmatically while tracking accuracy, tool calls and tokens, read transcripts for confusion, then let an agent refactor the tools and check on held-out tasks.

## Effective harnesses for long-running agents
- Problem: agents work in separate sessions with no memory, so long projects drift, leave half-built features, or declare victory early.
- Two roles, same tools and system prompt, different first prompts. The **initializer** session expands the request into a long end-to-end feature list (200+ items in their claude.ai-clone example), writes an `init.sh` that starts the app, creates a progress file, and makes the first git commit. **Coding** sessions then do one feature at a time.
- The feature list is JSON with description, user-level test steps and a `passes` flag, all initially failing. Agents may only flip `passes`; removing or editing tests is forbidden. JSON was chosen because models alter it less casually than Markdown.
- Session startup routine: confirm working directory, read git log and progress notes, pick the top unfinished feature, run `init.sh` and a basic end-to-end check to catch state left broken by the last session. End each session with a descriptive commit and progress update, leaving a mergeable state.
- Testing: agents marked features done after unit tests or curl alone. Browser automation (Puppeteer MCP) and "test like a human user" prompting caught real bugs. Limits: imperfect vision, native browser alert modals invisible.
- Open question from the authors: one general agent vs specialized testing, QA or cleanup agents.

## How we built our multi-agent research system
- Architecture: orchestrator-worker. A lead agent plans (saving the plan to external memory so truncation cannot lose it), spawns parallel subagents that each run their own search loop and return condensed findings, then a separate citation agent attributes claims. Search is iterative, unlike one-shot RAG.
- Delegation must be taught: each subagent needs an objective, output format, tool/source guidance and boundaries, or they duplicate work or leave gaps.
- Embed effort-scaling rules in the prompt: simple fact-finding is 1 agent with a few tool calls; comparisons 2-4 subagents; complex research 10+. Early versions spawned up to 50 subagents for trivial queries.
- Practices: simulate the agent step by step to see failure modes; search broad then narrow; extended thinking for the lead, interleaved thinking for subagents; a tool-testing agent that rewrote a flawed tool description cut later task time about 40%; prefer heuristics over rigid rules; subagents write to files and pass references back rather than relaying everything through the lead.
- Evals: start with about 20 realistic queries; judge outcomes not paths; a single-prompt LLM judge (accuracy, citations, completeness, source quality, tool efficiency) matched humans best; human testing still caught agents preferring SEO content farms.
- Results and costs: Opus lead plus Sonnet subagents beat single-agent Opus by 90.2% on their internal eval; token usage explained about 80% of BrowseComp variance. Cost is about 4x chat tokens for an agent and 15x for multi-agent, so use it for high-value, parallelizable work, not tightly coupled tasks like most coding.
- Production: resume from checkpoints, full tracing, rainbow deployments for in-flight agents; a lead that waits synchronously for subagents is a known bottleneck.

## Related posts (to ingest)
- Code execution with MCP
- Demystifying evals for AI agents

## Links
- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- https://www.anthropic.com/engineering/building-effective-agents
- https://www.anthropic.com/engineering/writing-tools-for-agents
- https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- https://www.anthropic.com/engineering/multi-agent-research-system
- https://www.anthropic.com/engineering
