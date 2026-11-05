# knowledge-work-plugins: data

Source: [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) · Type: plugin

## What it is for
Anthropic's role plugins (productivity, data, enterprise-search, sales, legal, finance and others) with commands, skills and connectors. `data` covers SQL and analysis; `productivity` covers tasks and daily workflow.

## When to reach for it
Writing or checking SQL, exploring a dataset, or quick analysis.

## Commands that matter
- `claude plugin marketplace add anthropics/knowledge-work-plugins`
- `claude plugin install data@knowledge-work-plugins`

## First exercise (about 15 minutes)
1. Install `data` with no connectors turned on.
2. Paste a schema you know and ask for a query that answers a real question.
3. Run the query and check the result by hand.

## How you know it worked
The query is right and the explanation matches what it does.

## Common mistake
Turning on every connector. Private data plus untrusted messages plus write access is a lethal trifecta; enable only what you need.
