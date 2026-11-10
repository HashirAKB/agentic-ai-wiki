# Proposed updates for Hashir

Practices found during research that could change how Claude works with Hashir. Nothing here is active until Hashir approves it; approved items are then saved as preferences or skills and marked APPROVED.

Format: `### [date] Title` then the practice, the source, and the suggested wording.

## Already adopted (2026-10-30)
- Karpathy working rules saved as preferences (assumptions up front, push back, simplicity, surgical edits, goal-driven execution, spec first, visual explanations, file answers worth keeping).
- Skills: agentic-engineering, llm-wiki.
- 2026-10-30: Claude Code `permissions.blockWritesOutsideWorkingDirectories` turned on in user settings (from radar 2026-10-30).

## Approved 2026-11-05 (saved as Claude preferences)
### APPROVED 2026-11-05: [2026-10-31] Enforce zero-exception rules with hooks, keep CLAUDE.md lean
Practice: rules with no exceptions (never read .env, always format) belong in hooks or deny rules, not CLAUDE.md; CLAUDE.md should hold only what Claude can't learn from the repo. Source: [Claude Code best practices](https://code.claude.com/docs/en/best-practices).
Suggested wording: "When a rule keeps being missed, propose a hook or deny rule instead of adding emphasis; audit CLAUDE.md files for lines Claude could infer from the code."

### APPROVED 2026-11-05: [2026-10-31] Interview-to-spec for vague tasks
Practice: for under-specified features, interview me with multiple-choice questions, write SPEC.md, then build in a fresh session and review against the spec (skip style). Source: same page.

### APPROVED 2026-11-05: [2026-11-01] Long tasks: feature list, progress file, end-to-end check
Practice: for multi-session builds, write a JSON feature list (all failing, only the pass flag editable), a progress log and an init script; work one feature per session, start by running the app, end with a commit. Source: [Anthropic](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents).
Suggested wording: "For work spanning sessions, keep a feature list and progress file in the repo; never mark a feature done without running it end to end."

### APPROVED 2026-11-05: [2026-11-03] Self-review agent-written PRs before asking for review
Practice: never hand over a PR or description you have not read and tested; keep it small, state the goal, attach evidence of manual testing. Source: [Willison anti-patterns](https://simonwillison.net/guides/agentic-engineering-patterns/anti-patterns/).
Suggested wording: "Before opening or requesting review of a PR, run the tests, exercise the change, read the description for accuracy, and list what was verified."

## Approved 2026-11-10 (saved as Claude preferences)
### APPROVED 2026-11-10: [2026-11-07] Diagnose long-session drift with the four context failure modes
Practice: when an agent degrades mid-task, check for poisoning, distraction, confusion or clash, then fix with write/select/compress/isolate (save the plan to a file, use a subagent for noisy searches) rather than adding more instructions. Source: [LangChain context engineering](https://www.langchain.com/blog/context-engineering-for-agents).
Suggested wording: "If a session has gotten long or noisy, say so, write the plan and state to a file, and offer to delegate noisy research to a subagent or start fresh."

## Pending

### [2026-11-08] Monthly audit of CLAUDE.md, memory and skills
Practice: every few weeks run `/doctor` and `/memory`, remove rules the model can infer or that newer models no longer need, then test a real task without them; keep what fails the way it was meant to prevent. Source: [Addy Osmani](https://addyosmani.com/blog/audit-your-agent-files/).
Suggested wording: "Monthly, offer to audit CLAUDE.md, saved preferences and installed skills for stale or inferable entries, and propose removals with a test task."
