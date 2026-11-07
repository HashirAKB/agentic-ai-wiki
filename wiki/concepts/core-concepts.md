# Core concepts

Cross-cutting ideas, each linked to its sources. Split into separate pages as they grow.

## Agentic engineering vs vibe coding
Vibe coding: build by describing, without caring about the code (fine for prototypes; raises the floor). Agentic engineering: professionals coordinating fallible agents while owning correctness, security and maintainability (raises the ceiling). Sources: [Karpathy](../people/andrej-karpathy.md), [Simon Willison](../people/simon-willison.md).

## Context engineering
Curating everything in the context window (instructions, tools, memory, retrieved data, history) with the minimum high-signal tokens for the next step. Techniques: right-altitude prompts, compaction, external notes, sub-agents for isolated context. Sources: [Karpathy](../people/andrej-karpathy.md), [Anthropic](../people/anthropic-engineering.md).
A useful checklist from the [LangChain team](../people/harrison-chase.md): **write** (scratchpads, memories outside the window), **select** (retrieve only relevant notes, tools, facts), **compress** (summarize, trim), **isolate** (sub-agents, sandboxes, state fields). Named failure modes: context poisoning, distraction, confusion, clash. Instrument token use and test each context change before keeping it.

## Verification loops and declarative goals
Agents are strongest when they can check their own work. Give success criteria rather than steps; tests first (red/green TDD); run existing tests first; browser or app-level verification; naive correct version, then optimize. The short prompts "Use red/green TDD" and "First run the tests" each carry a whole workflow. Sources: [Karpathy](../people/andrej-karpathy.md), [Simon Willison](../people/simon-willison.md), [Boris Cherny](../people/boris-cherny.md).

## Long-running agents: durable state between sessions
When work spans many context windows, put state in files and git, not memory: a feature list with pass/fail flags the agent may only flip, a progress log, an init script, one feature per session, a startup check that the app still works, and a commit at the end. Verify end to end like a user (real browser), not just unit tests or curl. Sources: [Anthropic](../people/anthropic-engineering.md), [Simon Willison](../people/simon-willison.md) (manual testing: run the code, record real output, turn bugs into tests).

## Subagents and multi-agent systems
Subagents isolate context: explore, parallel and specialist roles keep the parent's window clean. Multi-agent setups pay off for broad, parallelizable, high-value work (about 15x chat tokens) and poorly for tightly coupled work like most coding. Teach delegation (objective, format, boundaries), put effort-scaling rules in the prompt, and avoid piles of specialists. Sources: [Simon Willison](../people/simon-willison.md), [Anthropic](../people/anthropic-engineering.md).

## Verifiability and jagged intelligence
LLMs advance fastest where outcomes are automatically checkable and labs invest training effort. Expect brilliance and basic failures side by side; test empirically whether your task is on the model's rails. Source: [Karpathy](../people/andrej-karpathy.md).

## Partial autonomy
AI generates, human verifies; an autonomy slider; small chunks; human checkpoints. Increase autonomy only where reliability has been earned. Source: [Karpathy](../people/andrej-karpathy.md).

## Compounding engineering
Every mistake becomes a rule (CLAUDE.md), every repeated workflow becomes a command or skill, every good answer gets filed into the knowledge base. Sources: [Boris Cherny](../people/boris-cherny.md), [Simon Willison](../people/simon-willison.md), [Karpathy](../people/andrej-karpathy.md).

## Evals and error analysis
Look at real outputs first, categorize failures, fix the most common, then build targeted pass/fail evals and validated LLM judges. Hamel frames three levels: cheap unit tests on every change, trace review plus judges on a cadence, A/B tests last; measure judge agreement with precision and recall. Source: [Hamel Husain](../people/hamel-husain.md). Anthropic adds: grade the final environment outcome rather than the tool-call path, run several trials per task, use pass@k when one success suffices and pass^k when consistency matters, keep capability evals (low pass rate) separate from regression evals (near 100%), give every task a reference solution, and read transcripts. See [Anthropic Engineering](../people/anthropic-engineering.md).

## Code execution over direct tool calls
When many tools or large intermediate results are involved, let the agent write code against tools exposed as files: load tool definitions on demand, filter and loop in the sandbox, keep sensitive data out of the model's context. Costs a sandbox and its security work. Source: [Anthropic](../people/anthropic-engineering.md).

## Reviewing agent output before handing it on
Sending unreviewed agent-generated code or text to collaborators shifts the verification work onto them. Verify it yourself, keep changes small, explain the goal, and show evidence of testing. Source: [Simon Willison](../people/simon-willison.md).

## Agent-native surfaces
Build for the agent as user: markdown docs, CLIs, APIs, MCP servers, copy-pasteable agent instructions. Source: [Karpathy](../people/andrej-karpathy.md).

## Agent security: lethal trifecta
Private data + untrusted content + ability to send data out = prompt-injection exfiltration risk. Remove at least one leg. Cause: models cannot reliably tell operator instructions from instructions inside content. Prompt wording and guardrail products are not dependable; constrain actions after untrusted input. Source: [Simon Willison](../people/simon-willison.md).

## Workflows vs agents, and tool design
Start with the simplest pattern (single call, chain, routing, parallelization, orchestrator-workers, evaluator-optimizer) and move to autonomous agents only when it measurably helps. Tools are an interface for the model: few, well-scoped, namespaced, token-efficient, with actionable errors, and refined through evals on transcripts. Source: [Anthropic](../people/anthropic-engineering.md).

## Deterministic vs non-deterministic instructions
Prompts, CLAUDE.md and skills are advice the model can decide not to follow; hooks, deny rules, sandboxing, tests and CI are enforced. Use advice for guidelines with exceptions, enforcement for rules with none, and keep CLAUDE.md to what the model cannot learn from the repo. Source: [Boris Cherny / Claude Code docs](../people/boris-cherny.md).

## AI engineer role and agent planning
The AI engineer builds products on existing models; the job centres on owning data and evals and shipping fast, with ordinary code kept central. Source: [swyx](../people/swyx.md). For agents, validate plans before executing them, reflect at checkpoints, and evaluate plan validity, tool-call errors and step efficiency separately. Source: [Chip Huyen](../people/chip-huyen.md).

## Production patterns for LLM features
Beyond the model call: hybrid keyword plus embedding retrieval, caching on safe keys rather than semantic similarity, deterministic guardrails before LLM-based ones, UX that makes errors cheap to dismiss, and feedback signals feeding evals. LLM judges show position, length and self-preference biases, so pair them with human review. Source: [Eugene Yan](../people/eugene-yan.md).

## Open questions
- Subagents: Willison says a root agent can often review its own work and warns against many specialists, while Boris Cherny's workflow uses verification subagents ([Boris Cherny](../people/boris-cherny.md)). Likely depends on remaining context; not settled.
- Agents on novel code: [Karpathy's Oct 2025 interview](../people/andrej-karpathy.md) found coding agents net unhelpful on nanochat, while his 2026 posts treat agentic engineering as the main mode. Probably model progress plus the verifiability point, but not confirmed in his own words.
