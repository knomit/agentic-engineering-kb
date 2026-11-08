---
type: observation
domain: [agentic-engineering, evaluation, observability, prompting, benchmarks, guardrails]
confidence: 0.9
sources: 1
entities: [OpenAI, GPT-5.6 Sol, GPT-5.6 Terra, GPT-5.6 Luna, misalignment monitoring, Sneaky Sandbox Escape, OAI-repo Sabotage v2, synthetic transcripts, monitor prompt, recall]
motifs: [harness-over-model, saturated-benchmark-cannot-rank]
refs: ['https://openai.com/index/how-we-detect-frontier-model-misalignment/', 'kb://bc6eac5f37df/kb/decisions/ai/agents/observability/monitor-prompting/19218a92.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/observability/monitor-cascade/59ec9d9c.md']
---
# The operator that ran a three-way bake-off for its monitor model said part of the winner's margin came from the monitoring prompt having been optimised for it — and on the one task where all three scored near-perfectly the comparison carried no information at all

OpenAI compared three models powering the same misalignment monitor and published two caveats that together decide how much the comparison is worth. Both have to be carried; the result quoted without either of them is a model ranking, which is not what was measured.

The result: monitors using GPT-5.6 Sol "caught significantly more cases than those using GPT-5.6 Terra or GPT-5.6 Luna on recorded incidents, synthetic transcripts, and sabotage tasks".

Caveat one, the confound, stated by the operator itself: "We believe that some of Sol's advantage comes from the fact that we optimized the monitoring prompt for it." The quantifier is *some*, not all, and the direction is not quantified — so the measured gap is an upper bound on the model gap, and what was actually compared is three (model, prompt) pairs of which one pair had been tuned.

Caveat two, the saturated task: "all three performed perfectly or almost perfectly in detecting models' misbehavior in the Sneaky Sandbox Escape simulation". A task every candidate clears cannot separate them, so including it in an aggregate dilutes a real difference, and reporting it alone would erase one.

**The operational consequence for anyone picking a monitor model.** A bake-off is only a model comparison if the scaffold is held fixed *and untuned for any candidate*, or if each candidate gets its own prompt-optimisation budget. Re-optimising the prompt per candidate is the expensive-but-honest option; running the incumbent's prompt against challengers is the cheap option and it measures the incumbent's prompt. Report per-task scores rather than one aggregate, so a task on which everything saturates is visible as uninformative rather than silently averaged in.

**What this does not mean.** It is not evidence that the three models are equivalent as monitors — the gap on recorded incidents, synthetic transcripts and sabotage tasks is reported as significant and only "some" of it is attributed to the prompt. It is a reason to treat the published margin as unusable for ranking models in a different scaffold, not a reason to assume the margin is zero.
