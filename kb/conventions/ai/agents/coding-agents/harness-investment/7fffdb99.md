---
type: principle
domain: [agentic-engineering, coding-agents, conventions, operations, harness-design]
confidence: 0.75
sources: 1
entities: [OpenAI, Codex, AGENTS.md, harness engineering, agent-generated code, Ryan Lopopolo]
motifs: [misattributed-environment-defect]
refs: ['https://openai.com/index/harness-engineering/', 'kb://bc6eac5f37df/kb/principles/ai/agents/tools/82383efe.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/coding-agents/code-retrieval/46f3ea69.md']
---
# When a coding agent stalls on a task, the question that moved the needle was which capability the environment was missing — not how to prompt harder

An OpenAI team's account of building and shipping an internal beta "with 0 lines of manually-written code" reports the diagnosis that changed their throughput: "Early progress was slower than we expected, not because Codex was incapable, but because the environment was underspecified." Their rule from it is that "the fix was almost never 'try harder.'" In practice: when a task failed, they stopped retrying it and asked which capability was absent, then had the agent build that capability.

The setting, as reported: "roughly 1,500 pull requests have been opened and merged with a small team of just three engineers driving Codex"; "the repository contains on the order of a million lines of code"; "This translates to an average throughput of 3.5 PRs per engineer per day"; and "We estimate that we built this in about 1/10th the time it would have taken to write the code by hand."

Scope, and it is narrow: one team, one repository, self-reported, with no external measurement and no comparison arm. The post states its own limit — the end-to-end autonomy it describes "should not be assumed to generalize without similar investment—at least, not yet." So the transferable claim is the diagnostic habit, not the figures: treat a repeated agent failure as a missing-capability report about the environment before treating it as a prompting problem.
