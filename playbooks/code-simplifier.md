# code-simplifier

Source: [anthropics/claude-plugins-official/plugins/code-simplifier](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-simplifier) · Type: plugin (subagent)

## What it is for
A subagent that rewrites recently changed code to be clearer and smaller without changing what it does: less nesting, fewer redundant abstractions, consistent naming. It counters the agent habit of producing bloated code.

## When to reach for it
After Claude finishes a feature or a fix and the tests pass, before you commit.

## Commands that matter
- Install: `/plugin install code-simplifier@claude-plugins-official`
- Use: ask "use the code-simplifier agent on the files you just changed".

## First exercise (about 15 minutes)
1. In a real project, let Claude implement one small feature and get the tests green.
2. Commit it, then ask for the code-simplifier agent on those files.
3. Read the diff (`git diff`). For each change, ask yourself: is it simpler, and is the behaviour identical? Run the tests again.
4. Keep the changes you agree with; revert the rest (`git checkout -- <file>`).

## How you know it worked
A smaller or flatter diff, tests still green, and you can say why each change is better.

## Common mistake
The agent's built-in style rules are written for TypeScript/React projects (ES modules, `function` keyword, React props). On Kotlin or other languages, put the project's own conventions in the project's `CLAUDE.md`, since the agent follows CLAUDE.md, and reject changes that fight the language's idioms.
