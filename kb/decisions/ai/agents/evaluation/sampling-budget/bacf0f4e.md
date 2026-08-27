---
type: reference
domain: [agentic-engineering, evaluation, benchmarks, cost]
confidence: 0.8
sources: 1
entities: [UK AISI, optstop, Inspect, hierarchical Bayesian model, credible interval, optimal stopping, sequential analysis]
motifs: [fixed-budget-ignores-uncertainty, cheap-filter-first]
refs: ['https://www.aisi.gov.uk/blog/optimal-stopping-spending-evaluation-compute-where-it-counts']
---
# Fixed trials-per-task is where evaluation compute is wasted: adaptive stopping on a credible interval saved 57–97% of planned trials without moving the scores

UK AISI's `optstop` attacks a specific waste in agent evaluation: a fixed sample size "allocates the same number of trials to every task regardless of how much uncertainty remains", so compute is spent re-confirming estimates that are already precise while genuinely uncertain tasks stay under-sampled. AISI's framing of the cost side is that some frontier evaluations now require "hundreds of millions of tokens".

THE MECHANISM. Sample sequentially and stop per-task on either of two conditions, quoted verbatim: "1. **Precision**. The credible interval is narrow enough. 2. **Stabilisation**. The interval has stopped changing, so the data has nothing more to tell us." Stabilisation is the non-obvious half — it stops you paying for trials that are not narrowing the interval, which a pure precision threshold never does. Above the individual task, "a hierarchical Bayesian model combines information across tasks", so a task borrows strength from its grouping rather than being estimated in isolation.

THE SAFEGUARD, and it is the part to copy if you copy nothing else: a conservatism mechanism "demand[s] more data when estimated success falls below 1%". Near-zero success rates are exactly where a narrow interval is most likely to be an artifact of not having sampled the rare success yet, so the naive stopping rule is least trustworthy precisely where a capability evaluation's conclusion matters most.

THE MEASUREMENT. Across three scoring types — "binary (e.g. pass/fail), ordinal (e.g. rubric ratings from 0-10), and continuous (e.g. 0-100%)" — and "three levels of expected model performance (low, medium, and high)", "`optstop`'s early stopping saved between 57% and 97% of planned trials, _without impacting score estimates_."

WHEN IT DOES NOT PAY. AISI states the practical precondition — "The main practical requirement is that tasks are presented in a randomised order" — because a stopping rule reading a sequentially-ordered stream will stop on an artifact of the ordering. It also notes that genuinely noisy estimates never reach the precision threshold and run to the full budget, so the saving is not uniform, and that the method is most effective when individual trials are long and expensive. That last condition is the real gate: adaptive stopping buys nothing on cheap trials, because the machinery costs more than the trials it skips.

NOT ESTABLISHED BY THIS SOURCE. Asked directly, the post does NOT state whether the 57–97% figures come from live frontier-model evaluation runs or from simulation over synthetic conditions, and it does not state that the method was left unvalidated on real evaluations either — it is silent on the question in both directions. The phrase "three levels of expected model performance (low, medium, and high)" reads like a designed sweep rather than a set of real models, but that is this pack's inference and not the source's claim. Anyone deciding whether to adopt this should resolve that before treating 57–97% as a figure they will see. Note also that this is the tool's author reporting on the tool.

RELATION TO [[80866fc3]]: that fact is about the budget WITHIN a trial (tokens, turns) and says capability is a curve against it. This is about the number OF trials. They are separate axes and both are usually set by convention rather than by measurement — but note they interact, because the more expensive you make each trial, the more adaptive stopping is worth.
