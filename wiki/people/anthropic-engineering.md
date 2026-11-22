# Anthropic Engineering blog (Applied AI team)

**Who:** The team behind Claude, Claude Code and the Agent SDK, publishing how they build agents internally.
**Why credible:** Primary source from a frontier lab, based on production systems.
**Ingested:** 2026-10-30 (context engineering via summaries); 2026-10-30 (Building effective agents, Writing tools for agents read from primary pages); 2026-11-01 (Effective harnesses for long-running agents); 2026-11-02 (multi-agent research system); 2026-11-03 (Demystifying evals for AI agents); 2026-11-04 (Code execution with MCP); 2026-11-18 (Agent Skills, Claude Code sandboxing); 2026-11-19 (Advanced tool use); 2026-11-20 (Building a C compiler with parallel Claudes); 2026-11-21 (auto mode); 2026-11-22 (two quality postmortems)
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

## Demystifying evals for AI agents
- Vocabulary: a *task* is one test, a *trial* one attempt (run several, outputs vary), a *grader* scores something, the *transcript* is the full record, the *outcome* is the final environment state (a reservation row exists, not "I booked it"). Evaluating an agent means evaluating harness plus model together.
- Graders: code-based (fast, objective, brittle), model-based (flexible, nondeterministic, must be calibrated to humans; allow an "Unknown" answer, one judge per dimension), human (gold standard, slow). Combine them; grade the outcome rather than a rigid tool-call sequence, and give partial credit on multi-part tasks.
- Capability evals start at a low pass rate and give a target; regression evals sit near 100% and catch backsliding. Saturated capability evals graduate to regression suites, and you then need harder tasks.
- pass@k (at least one success in k) fits cases where one good answer is enough; pass^k (all k succeed) fits customer-facing consistency. At 75% per trial, three in a row is about 42%.
- Per agent type: coding uses deterministic tests (SWE-bench Verified, Terminal-Bench); conversational combines end-state, turn limits and rubric-graded tone with a simulated user (tau-bench); research mixes groundedness, coverage and source-quality checks; computer use checks real page, backend and file state.
- Roadmap: start early with 20-50 tasks from real failures and what you already test manually; write tasks two experts would grade identically, each with a known-good reference solution (0% over many trials usually means a broken task); balance positive and negative cases; start every trial from a clean environment; make graders hard to game; read the transcripts; maintain the suite. Eval-driven development means defining capabilities before agents can meet them.
- Pitfalls: over-rigid step checks, grader bugs (one example moved from 42% to 95% after fixing grader and scaffold), shared state between trials, infrastructure limits causing correlated failures, one-sided sets, loopholes, trusting scores without reading transcripts.
- Evals are one layer among production monitoring, A/B tests, user feedback, manual transcript review and human studies; none catches everything.

## Code execution with MCP
- Problem: loading every MCP tool definition up front, and routing big intermediate results through the model, burns context. Thousands of tools can mean hundreds of thousands of tokens before the request is read; a 2-hour meeting transcript passed between tools costs roughly 50k extra tokens.
- Pattern: present MCP servers as code on a filesystem (one file per tool). The agent lists the directory and reads only the tools it needs, or calls a `search_tools` tool with a chosen detail level (name, description, full schema). This is progressive disclosure.
- Do filtering, loops, conditionals and polling in code in the sandbox so the model sees a summary (5 rows of a 10,000-row sheet), not the raw data. Their Drive-to-Salesforce example went from about 150k to 2k tokens.
- Privacy: intermediate results stay in the execution environment by default; the client can tokenize PII so the model sees placeholders while real values flow between tools.
- State and skills: agents can save files to resume work and save working code as reusable functions; add a SKILL.md and it becomes a skill.
- Caveat: needs a secure sandbox, resource limits and monitoring. Weigh that overhead against the token, cost and latency savings.

## Equipping agents with Agent Skills (Oct 2025)
- A skill is a directory with a `SKILL.md` (YAML frontmatter with `name` and `description`, then instructions) plus optional bundled files and scripts.
- Progressive disclosure in three levels: name and description of every installed skill sit in the system prompt; the full `SKILL.md` loads only when the skill looks relevant; linked files (e.g. a `forms.md`) load only for the specific scenario. So bundled context is effectively unbounded.
- Scripts can run without the script or its data entering context, which makes steps deterministic and cheaper than generating the same logic as tokens.
- Authoring: start from evals (run agents on representative tasks, see where they struggle, add skills to close gaps); split a large `SKILL.md` and keep rarely combined contexts on separate paths; say whether a script is to be run or read; watch real trajectories and refine the description, since it drives triggering; ask the agent to record its successful approaches and mistakes into the skill.
- Security: a malicious skill can leak data or take unintended actions, so install from trusted sources and audit bundled code, dependencies and any instruction to contact external hosts.
- Stated direction: sharing tools for organizations, pairing skills with MCP servers (skills teach the multi-step workflow), and agents eventually writing and evaluating their own skills.

## Beyond permission prompts: Claude Code sandboxing (Oct 2025)
- Problem: per-action approval causes fatigue, so people stop reading prompts, and a prompt-injected agent with broad access is risky.
- Design: OS-level sandbox (bubblewrap on Linux, seatbelt on macOS, no container overhead) with two layers that must both exist. Filesystem isolation limits read/write to the working directory; network isolation routes traffic through a proxy outside the sandbox that allows only approved domains. Without the network layer, a compromised agent can exfiltrate files such as SSH keys; without the filesystem layer, it can escape to the network.
- Web version: sessions run in cloud sandboxes with git credentials kept outside. A proxy checks a scoped credential and the request (e.g. push only to the configured branch) and then attaches the real token.
- Reported result: 84% fewer permission prompts in internal use (self-reported, not independently verified). The runtime is open source and can sandbox arbitrary agents and MCP servers; in Claude Code it is `/sandbox`.

## Advanced tool use (Nov 2025)
- Problem: tool definitions eat context (their five-server example: 58 tools, about 55K tokens; they saw 134K internally), similar tool names cause wrong picks, every intermediate result lands in context, and JSON Schema says what is valid, not how a tool is normally used. Three beta features (header `advanced-tool-use-2025-11-20`), each aimed at one bottleneck.
- Tool Search: mark tools `defer_loading: true`; Claude sees only a search tool plus non-deferred tools and pulls full definitions on demand (regex, BM25 or custom embedding search). Keeps the prompt cacheable. Reported: about 77K to 8.7K tokens of upfront context; MCP eval accuracy Opus 4 49% to 74%, Opus 4.5 79.5% to 88.1%. Use when definitions exceed about 10K tokens, you have 10+ tools or several MCP servers; skip for small or always-used toolsets. Costs a search step of latency. Keep the 3-5 most-used tools loaded, write precise names and descriptions, and tell the model in the system prompt what capability areas exist. (The post's "85% reduction" headline does not quite match its own 77K to 8.7K figures, which is closer to 89%.)
- Programmatic tool calling: Claude writes Python in a sandbox that calls your tools (`allowed_callers`), aggregates, and returns only the result. Example: 2,000+ expense lines (about 200KB) reduced to the 2-3 over-budget people (about 1KB). Reported: average tokens 43.6K to 27.3K on research tasks, fewer round trips, small accuracy gains (46.5% to 51.2% on GIA). Best for big datasets, 3+ dependent calls, parallel fan-out; skip for single calls or when the model must reason over every intermediate result. Document return formats (the model writes parsing code) and prefer idempotent, parallel-safe tools. This is the API-level version of the code-execution-with-MCP pattern above.
- Tool use examples: `input_examples` on a tool show conventions the schema cannot (date formats, ID patterns, when optional nested fields apply). Reported: complex-parameter accuracy 72% to 90% in internal tests. Use realistic values, 1-5 examples, spread from minimal to full calls; skip for obvious tools. Costs tokens on every request.
- Advice: start with your biggest bottleneck (context bloat -> search; large intermediate results -> programmatic calls; parameter errors -> examples). All numbers are Anthropic's own, not independently verified.

## Building a C compiler with a team of parallel Claudes (Feb 2026, Nicholas Carlini)
- Setup: a bash loop restarts Claude Code on a fixed prompt file whenever a session ends, inside a container. Several agents each run in their own container, clone a shared bare git repo and push back. No orchestrator and no channel beyond git.
- Coordination: an agent claims a task by writing a lock file in `current_tasks/`; git sync makes a second claimant pick something else. Merge conflicts were frequent and the agents resolved them. Agents keep notes on failed approaches and the project leans on READMEs and progress files because each session starts cold.
- The verifier is the bottleneck: with no human watching, the tests must be near-flawless or the agent optimizes for the wrong target. Tests came from existing compiler suites plus build and verify scripts for open-source packages; failure patterns became new tests; CI was added late to stop regressions.
- Designing for model limits: keep terminal output to a few lines and send detail to log files with greppable error tags (context pollution); give a `--fast` mode that runs a deterministic random 1% or 10% sample, with samples differing per agent so the whole suite is still covered (time blindness).
- Parallelism breaks on monolithic tasks: with many independent failing tests it was easy, but compiling the Linux kernel was one task and agents collided on the same bug. Fix: use GCC as a known-good oracle, compile most files with GCC and only a subset with the new compiler, so agents fix different bugs in different files; delta debugging found failures that only occur in combination.
- Specialist agents handled deduplication, compiler performance, output efficiency, design critique and docs.
- Reported outcome: about 2,000 sessions over roughly two weeks, around 2B input and 140M output tokens, just under $20,000; a ~100,000-line Rust compiler that builds Linux 6.9 on x86, ARM and RISC-V and passes about 99% of most test suites. Limits: needs GCC for 16-bit real-mode boot code, no own assembler or linker, less efficient output than unoptimized GCC, new features often broke old ones. Capability rose by model: Opus 4 barely worked, 4.5 passed suites but not real projects, 4.6 near the model's limit.
- Author's caution: passing tests is not the same as done, and he is uneasy about shipping software nobody has personally verified. (Figures are Anthropic's own.)

## Claude Code auto mode (2026, Anthropic Engineering)
- Problem: users approve 93% of permission prompts, so approval fatigue makes manual review weak. Auto mode sits between manual approval and skipping permissions: a classifier decides instead.
- Two layers: an input probe scans tool outputs (file reads, fetches, shell output) for injection and adds a warning; an output classifier (Sonnet 4.6) checks each action first with a fast single-token yes/no filter tuned to block, then chain-of-thought only on flagged actions.
- Reasoning-blind by design: the classifier sees user messages and the agent's tool calls only, not the agent's prose or tool results, so the agent cannot talk its way past it and injected text has little route in.
- Tiers: read-only tools and user allow rules pass (broad rules granting arbitrary code execution are dropped on entry); in-project file edits skip the classifier (reviewable in git); shell, web, external tools, subagent spawns and out-of-project writes go to the classifier. Default trust boundary is the current git repo.
- Threat model, in tuned priority: overeager behavior and honest blast-radius mistakes first, then injection and a misaligned model. Blocked examples: escalating scope in a vague cleanup, hunting for other credentials after an auth error, guessing a target by similar name, posting data to a public gist, retrying a deploy with a verification-skip flag. Customizable slots: environment, block rules (20+ defaults), allow exceptions.
- Measured (Anthropic's own): full pipeline 0.4% false positives on 10,000 real calls, but a 17% miss rate on 52 real overeager actions and 5.7% on synthetic exfiltration. Stage 1 alone: 8.5% false positives, 6.6% misses. Most misses come from treating a nearby approval as consent for the full blast radius.
- Behavior on block: the denial and its reason go back to the agent to find a safer path; 3 consecutive or 20 total denials stop the session (headless: terminate). Subagents are checked at delegation (can deny) and at return (warn only).
- Authors' caution: not a replacement for careful human review on high-stakes infrastructure; better than skipping permissions, possibly worse than careful manual review. Compare with the sandbox approach above, which enforces boundaries rather than judging actions.

## Quality postmortems: Aug-Sep 2025 infrastructure bugs and the Mar-Apr 2026 Claude Code changes
- **2025 post** ([three recent issues](https://www.anthropic.com/engineering/a-postmortem-of-three-recent-issues)): three overlapping infrastructure bugs. (1) Context-window routing sent some Sonnet 4 requests to servers meant for the 1M-context window; at the worst hour 16% of requests were affected and "sticky" routing kept unlucky users on the bad servers (about 30% of Claude Code users had at least one misrouted message). (2) A TPU misconfiguration occasionally boosted unlikely tokens, producing stray Thai or Chinese characters or syntax errors. (3) An approximate top-k bug in the XLA:TPU compiler, previously masked by a workaround, surfaced after a sampling rewrite and only on some batch sizes. Anthropic states it does not lower quality because of demand or load.
- **2026 post** ([April 23 update](https://www.anthropic.com/engineering/april-23-postmortem)): three product-layer changes, not model changes, and the API was unaffected. (1) Default reasoning effort lowered from high to medium on March 4 to cut perceived latency, reverted April 7 as the wrong tradeoff. (2) A cache-clearing change meant to drop old thinking once after an hour idle ran on every turn (March 26 to April 10), so the agent seemed forgetful and repetitive and caused cache misses. (3) A verbosity-limiting prompt (25 words between tool calls, 100 in the final answer) ran April 16-20; ablations showed about a 3% eval drop.
- Why it was missed: internal evals showed the effort cut as a small intelligence loss for a big latency win; the caching bug hid behind an internal-only experiment and a display change, passed unit, end-to-end and dogfood checks, and took over a week to root-cause; the prompt change passed weeks of testing on a narrow eval set and only showed up on a broader one. In 2025, benchmarks, safety evals and canaries missed it, and Claude's habit of recovering from isolated mistakes masked the damage.
- How it was found: user reports via feedback commands and reproducible public examples, then line-by-line prompt ablations. Back-testing their code-review tool with a newer model on the offending PRs found the caching bug when given full repository context.
- Lessons stated: run continuous quality evals on production, not only pre-release; evaluate every system-prompt change per model on a broad set and ablate line by line; gate model-specific changes to that model; use soak periods and gradual rollouts for anything that trades intelligence for speed; have staff use the exact public build.
- Takeaway for agent builders: quality regressions often come from harness changes (effort defaults, context trimming, prompt edits), not weights, and aggregate evals can miss them. (Both posts are Anthropic's own account.)

## Links
- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- https://www.anthropic.com/engineering/building-effective-agents
- https://www.anthropic.com/engineering/writing-tools-for-agents
- https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- https://www.anthropic.com/engineering/multi-agent-research-system
- https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- https://www.anthropic.com/engineering/code-execution-with-mcp
- https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
- https://www.anthropic.com/engineering/claude-code-sandboxing
- https://www.anthropic.com/engineering/advanced-tool-use
- https://www.anthropic.com/engineering/building-c-compiler
- https://www.anthropic.com/engineering/claude-code-auto-mode
- https://www.anthropic.com/engineering/a-postmortem-of-three-recent-issues
- https://www.anthropic.com/engineering/april-23-postmortem
- https://www.anthropic.com/engineering
