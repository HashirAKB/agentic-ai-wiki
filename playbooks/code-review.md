# code-review

Source: [anthropics/claude-plugins-official/plugins/code-review](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-review) · Type: plugin (command)

## What it is for
`/code-review` reviews a pull request with four agents in parallel: two check compliance with the project's `CLAUDE.md`, one looks for obvious bugs in the change, one reads git history for context. Each issue gets a 0-100 confidence score and only issues at 80+ are reported, which keeps noise down.

## When to reach for it
On every pull request before you merge, including your own solo projects. It matches how the Claude Code team works: automated review first, human attention on design questions.

## Commands that matter
- Install: `/plugin install code-review@claude-plugins-official`
- Requires the GitHub CLI: install `gh` (https://cli.github.com) and run `gh auth login` once.
- On the PR branch: `/code-review` prints the review in the terminal; `/code-review --comment` posts it on the PR.

## First exercise (about 20 minutes)
1. Make one small, real change on a new branch and push it; open a pull request.
2. Before running the tool, write down what you would flag yourself.
3. Run `/code-review` and compare: what did it catch that you missed, and what did it miss?
4. Fix what is real, push, and merge.

## How you know it worked
A review appears in the terminal (or on the PR) and you can sort its findings into real versus not.

## Common mistake
Running it without a `CLAUDE.md` in the repo. Half of its reviewers check against that file, so write down the project's conventions first. It also skips closed, draft and trivial PRs by design.
