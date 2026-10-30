# Core concepts

Cross-cutting ideas, each linked to its sources. Split into separate pages as they grow.

## Agentic engineering vs vibe coding
Vibe coding: build by describing, without caring about the code (fine for prototypes; raises the floor). Agentic engineering: professionals coordinating fallible agents while owning correctness, security and maintainability (raises the ceiling). Sources: [Karpathy](../people/andrej-karpathy.md), [Simon Willison](../people/simon-willison.md).

## Context engineering
Curating everything in the context window (instructions, tools, memory, retrieved data, history) with the minimum high-signal tokens for the next step. Techniques: right-altitude prompts, compaction, external notes, sub-agents for isolated context. Sources: [Karpathy](../people/andrej-karpathy.md), [Anthropic](../people/anthropic-engineering.md).

## Verification loops and declarative goals
Agents are strongest when they can check their own work. Give success criteria rather than steps; tests first (red/green TDD); run existing tests first; browser or app-level verification; naive correct version, then optimize. Sources: [Karpathy](../people/andrej-karpathy.md), [Simon Willison](../people/simon-willison.md), [Boris Cherny](../people/boris-cherny.md).

## Verifiability and jagged intelligence
LLMs advance fastest where outcomes are automatically checkable and labs invest training effort. Expect brilliance and basic failures side by side; test empirically whether your task is on the model's rails. Source: [Karpathy](../people/andrej-karpathy.md).

## Partial autonomy
AI generates, human verifies; an autonomy slider; small chunks; human checkpoints. Increase autonomy only where reliability has been earned. Source: [Karpathy](../people/andrej-karpathy.md).

## Compounding engineering
Every mistake becomes a rule (CLAUDE.md), every repeated workflow becomes a command or skill, every good answer gets filed into the knowledge base. Sources: [Boris Cherny](../people/boris-cherny.md), [Simon Willison](../people/simon-willison.md), [Karpathy](../people/andrej-karpathy.md).

## Evals and error analysis
Look at real outputs first, categorize failures, fix the most common, then build targeted pass/fail evals and validated LLM judges. Source: [Hamel Husain](../people/hamel-husain.md).

## Agent-native surfaces
Build for the agent as user: markdown docs, CLIs, APIs, MCP servers, copy-pasteable agent instructions. Source: [Karpathy](../people/andrej-karpathy.md).

## Agent security: lethal trifecta
Private data + untrusted content + ability to send data out = prompt-injection exfiltration risk. Remove at least one leg. Source: [Simon Willison](../people/simon-willison.md) (to verify against his primary post).
