# security-guidance

Source: [anthropics/claude-plugins-official/plugins/security-guidance](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/security-guidance) · Type: plugin (hooks)

## What it is for
Security review of code Claude writes, in three layers: instant warnings on ~25 known-dangerous patterns while editing (hardcoded secrets, unsafe deserialization, raw `innerHTML` and similar); an LLM review of the diff when Claude finishes a turn, with high-severity findings fed back so Claude fixes them; and a deeper agentic review on `git commit` that traces data flow across files (injection, XSS, SSRF, IDOR, auth bypass, path traversal).

## When to reach for it
Always on once installed. It is most valuable on anything that handles input, credentials, network calls, or an LLM agent with tools.

## Commands that matter
- Install: `/plugin install security-guidance@claude-plugins-official`
- Needs Python 3.8+ on PATH and Claude Code 2.1.144 or later.
- Model and behaviour are set with environment variables (see the plugin README), e.g. `SECURITY_REVIEW_MODEL` to pin or cheapen the reviewer.

## First exercise (about 15 minutes)
1. In a throwaway branch, ask Claude to add a quick config loader that reads an API key and writes it into a log line.
2. Watch for the warning or review finding. When it appears, ask Claude: "explain this risk and the safe pattern".
3. Let Claude fix it, then commit and see whether the commit review has anything to add.
4. Delete the branch.

## How you know it worked
You see at least one warning or finding, and you can explain the risk in one sentence.

## Common mistake
Treating silence as proof of safety. It catches common web vulnerability classes; it does not review your architecture. For agents, still check the lethal trifecta yourself (private data + untrusted content + a way to send data out). Each review also uses model calls, so it adds some usage.
