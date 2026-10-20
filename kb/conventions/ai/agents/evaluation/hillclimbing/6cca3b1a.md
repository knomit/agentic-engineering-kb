---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, evaluation, prompting, cost]
confidence: 0.8
sources: 1
entities: [Anthropic, Claude Code, claude-api skill, hillclimb, train set, held-out test set, overfitting, prompt optimisation]
motifs: [optimiser-overfits-its-signal]
refs: ['https://claude.dev/blog/automating-eval-design-and-hillclimbing/']
---
# An automated prompt-hillclimb keeps a patch only when the train AND the unseen test set both improve; a train-only gain is reverted as overfitting

Claude Code's `/claude-api hillclimb` loop proposes one patch per round against a root cause and accepts it on a three-part rule, every component of which matters: the patch is kept only if the train set AND the test set both improve; if the train set improves but the test set is flat, the loop treats that as overfitting and reverts; and a regression on either split reverts. The optimiser may read failures from one split only — "Use a train set that the hillclimber may read and a test set that is never seen." On the published case study the split was 44 cases, 30 for the search and 14 held out.

Operational consequence: a prompt-optimisation loop needs a holdout it never reads before it is allowed to accept anything, and a flat holdout is grounds to discard the patch rather than ship it on the strength of the train gain.

This does NOT mean a flat test score proves the patch worthless — it is the loop declining to bank a gain it cannot verify. Nor does the rule make accepted patches transfer: in the same study the accepted configuration reached 98.9% on the search set and 90.5% on the holdout, so a train-test gap survives the rule.

When the score stalls the loop stops patching and categorises the remaining failures by cause, which is where ambiguous tasks, grader bugs and harness errors surface instead of more prompt work.
