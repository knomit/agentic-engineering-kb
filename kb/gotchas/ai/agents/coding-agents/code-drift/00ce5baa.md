---
type: observation
domain: [agentic-engineering, coding-agents, operations, conventions, maintenance]
confidence: 0.75
sources: 1
entities: [OpenAI, Codex, AI slop, golden principles, quality grades, linters, structural tests, refactoring PRs]
motifs: [imitation-propagates-defects, cleanup-outpaced-by-throughput]
refs: ['https://openai.com/index/harness-engineering/']
---
# An agent copies the patterns already in the repository, bad ones included, so a fully agent-written codebase needs a mechanical garbage collector rather than a weekly cleanup shift

Because the agent imitates the code already present, a defect introduced once becomes the local convention and spreads with every subsequent change. The OpenAI team reports the manual remedy and its failure directly: "Our team used to spend every Friday (20% of the week) cleaning up 'AI slop.'" That did not scale, because the cleanup rate was human and the drift rate was not.

What replaced it has two parts. The principles the team cared about were encoded as mechanical rules — custom linters and structural tests — rather than left as prose guidance; and background agent tasks scan the repository for deviations, update per-area quality grades, and open small refactoring PRs, of which "Most of these can be reviewed in under a minute and automerged."

The operational consequence when planning an agent-heavy codebase: the cleanup path has to be continuous and automated from the start, and its throughput has to scale with the same thing that scales the drift. A scheduled human cleanup slot is a fixed-rate remedy for a growing problem, and the share of the week it consumes is the symptom to watch.

One mechanism worth copying separately: the team writes remediation instructions into their lint error messages, so a violation the agent hits carries its own fix into the agent's context instead of only reporting a rule name.
