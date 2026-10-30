# Weekly tools radar

Find new or newly useful tools for an individual developer doing AI-assisted and agentic work with Claude: Anthropic features, Claude connectors, Claude Code plugins and skills, MCP servers, CLIs, and concrete workflow tips. The reader has no time to follow X, Substack, YouTube or forums, so this run does it for them.

## 1. Know what was already suggested
Run `date`. Read `radar/seen.md` (create it if missing, with a header row `| Name | URL | First suggested | Verdict |`). Do not suggest anything already listed there unless it has had a major update since; then mark it "Update".

## 2. Scan (last ~14 days first)
Primary sources first:
- Anthropic: https://www.anthropic.com/news and https://www.anthropic.com/engineering
- Claude release notes: https://docs.claude.com/en/release-notes/overview and the Claude Help Center release notes (search "Claude release notes")
- Claude Code changelog: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md
- Anthropic's official skills, plugins and connector repositories on GitHub (search github.com/anthropics for skills, plugins, MCP)
- MCP: the official registry (https://registry.modelcontextprotocol.io) and https://github.com/modelcontextprotocol/servers
- Practitioners already in this wiki (see `index.md`), especially https://simonwillison.net
Then use WebSearch for "new MCP server", "Claude Code plugin", "Claude skill", "Claude connector" and similar from the last two weeks to catch what people are actually using. Treat X/Twitter, Reddit and YouTube as leads only: confirm each item at its own repo, docs or announcement before including it.

## 3. Filter
Include an item only if it is real (has a repo, docs or an official page), maintained, and plausibly useful for coding with agents, building agents, research, job search, productivity, or Android/Kotlin development. Skip hype, paid-course funnels, abandoned repos and near-duplicates. Prefer Anthropic-official and well-known maintainers.

## 4. Write `radar/YYYY-MM-DD.md` (today's date), at most 10 items
For each item:
- **Name** (link) — category: Anthropic feature | Connector | Plugin | Skill | MCP server | CLI/tool | Workflow tip — from: who publishes it
- **What it does:** one or two lines.
- **Why it's useful:** the concrete job it does better.
- **How to try:** the one or two real steps (install command, where to enable it).
- **Risks:** permissions it needs, data it can reach, and whether it can create a lethal trifecta (private data + untrusted content + a way to send data out). Note if it is unofficial or young.
- **Verdict:** Try now | Watch | Skip-for-now.

Put the three best "Try now" items first under a "Top picks" heading. End with a "Sources checked" list.

## 5. Bookkeeping
Append one row per item to `radar/seen.md`. Make sure `index.md` has a "Tools radar" section linking `radar/seen.md` and the newest radar file (update the link). Append to `log.md`: `## [YYYY-MM-DD] radar | <n> items, top: <names>`.

## 6. Commit
This repo is public: write nothing personal about the owner. Check relative links resolve. Commit (`radar: YYYY-MM-DD`) and `git push`; if rejected, `git pull --rebase` and push again. Only edit `radar/`, `index.md` and `log.md`. Do not edit anything under `.github/`.
