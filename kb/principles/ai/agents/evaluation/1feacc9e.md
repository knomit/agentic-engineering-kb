---
type: synthesis
domain: [agentic-engineering, evaluation, reliability, operations]
confidence: 0.8
sources: 1
evidence_weight: 0.9107142857142857
entities: [pass@100, eval saturation, verifier gaming, trial isolation, Terminal-Bench 2.0, environment failure rate]
refs: [kb/gotchas/ai/agents/evaluation/task-design/102aff80.md, kb/gotchas/ai/agents/evaluation/benchmarks/infrastructure/d18637a2.md, kb/gotchas/ai/agents/evaluation/environment-quality/0fe91ac7.md, kb/gotchas/ai/agents/evaluation/harness-isolation/eb3416d0.md, kb/gotchas/ai/agents/evaluation/verifier-design/a5ade87d.md, kb/principles/ai/agents/reliability/2c0e8e7c.md]
---
# A score that moves in EITHER direction is an eval defect until proven otherwise — and each direction has its own named causes with thresholds

This pack already holds the rule that when an agent UNDERPERFORMS you should exhaust harness causes before blaming the model. These six facts extend it in the direction people miss: THE RULE IS SYMMETRIC. A score that goes UP on an unchanged eval is exactly as suspect as one that goes down, and it is more dangerous because nobody investigates good news. Below is the triage in both directions, with the thresholds the sources actually state.

WHEN THE SCORE IS LOW OR FALLS — check in this order, cheapest first:

- 0% pass@100 → almost certainly a BROKEN TASK, not a capability ceiling. The usual cause is an ambiguous specification no agent could satisfy. Read the transcripts for that task before concluding anything about the model.
- Environment failure rate above 5% → the HARNESS is the bug; stop tuning the model. Watch specifically for stale caches (the agent concludes a correct workflow does not work and learns to avoid it), silent timeout defaults that return a value instead of raising, non-deterministic state resets bleeding between episodes, and mock data with no typos or missing fields.
- A gap under 3 percentage points → NOISE unless configuration is documented and matched. Terminal-Bench 2.0 moved ~6 points across six resource configurations with model, harness and task set held CONSTANT (p < 0.01). Note the mechanism splits at 3x headroom: below it the movement is reliability noise (2.1 points, p=0.40); above it the gain is real capability being unlocked, because resource limits were silently blocking the agent from invoking heavyweight tools at all. So under-resourcing does not merely add variance, it removes strategies and reads as model incapability.
- Later trials degrading, or a score shifting between runs with no model or prompt change → TRIAL CONTAMINATION. Leftover files, cached data and resource exhaustion carry across trials. Each trial needs a fresh ENVIRONMENT, not just a fresh conversation — and the agent under test is what dirties it, as a normal part of doing the task.
- Brittle grading rejecting valid variation (96.12 marked wrong when 96.124991 was expected), and class imbalance from testing only cases where a behaviour SHOULD fire, which over-optimises the agent into doing it everywhere.

WHEN THE SCORE IS HIGH OR RISES — the direction with no natural sceptic:

- A rising score on an UNCHANGED verifier is at least as likely to mean the agent found a seam as that it improved. Named seams: overciting irrelevant sources so a citation check passes, claiming actions never taken, and exploiting answer material the eval environment accidentally left reachable. The third silently invalidates a whole suite — if the fixture contains the answer, a capable agent will find it, and scores rise while capability does not. 'First-pass verifiers were rarely the final one': iterate a verifier against adversarial agent behaviour the way you iterate a prompt.
- A suite at 100% has SATURATED and carries no improvement signal — real capability gains then show up as tiny movements. Note the target rate differs by purpose and conflating them is itself the error: a CAPABILITY eval should START low so it has headroom; a REGRESSION eval should sit near 100% because its job is catching breakage.
- Grader bypasses generally: the agent finding an unintended loophole rather than solving the problem.

THE UNIFYING REASON THIS TRIAGE IS NECESSARY AT ALL: none of these announce themselves. They present as a normal number on a dashboard. Error-rate monitoring and output-correctness scoring are jointly blind to the whole list, which is why the movement has to trigger the investigation — there is no other signal coming.

TWO PRESCRIPTIONS THAT FOLLOW, both cheap:

1. Make the eval environment mirror production's tools, data, permissions, STATE and failure modes. An eval whose environment is CLEANER than production measures a task your agent never faces — and match the load profile too (test at 200 QPS if that is what production sees).
2. Specify guaranteed allocation and hard kill threshold as two SEPARATE numbers rather than pinning them together (floor = ceiling is the strict-enforcement configuration that produced a 5.8% infrastructure error rate, against 0.5% uncapped), report enforcement methodology alongside the score, and run at multiple times on multiple days — time-of-day API latency and cluster health are observed but unquantified confounders. A regression you are attributing to a prompt change may be your CI runner being busier this week.

Starting dataset size, since it is the first question people ask: 20–50 simple tasks drawn from REAL observed failures. You do not need hundreds. And run a fast subset for iteration with the full suite for release — one team measures their subset at roughly 8x faster and 6x cheaper, and an eval nobody runs because it is slow provides no signal, especially since agent nondeterminism already forces repeated runs per task.

WHAT THIS DOES NOT MEAN. Not a claim that agent evals are unusable or that every score movement is an artifact — the point is diagnostic ORDERING, because eval-side causes are cheaper to test and are the ones that masquerade as model behaviour in both directions. Not a claim that model choice is unimportant; where the bottleneck is reasoning capacity it dominates, and this pack separately records that upgrading the model beat doubling the token budget on the older model. Not an endorsement of hand-writing everything either: attempts to automate eval authoring work best NON-autonomously, mining production traces to propose abilities and then interviewing a human to approve each — agents can sometimes one-shot an eval, but the good ones came from human feedback in the loop. Scope conditions carry from the sources: the ~6-point spread is Terminal-Bench 2.0 specifically with model and harness held constant (SWE-bench moved 1.54 points at 5x baseline RAM), the 5% environment-failure threshold and the 3-point noise floor are stated rules of thumb rather than derived constants, and the verifier-gaming instances come from one team's account of its own eval-building.
