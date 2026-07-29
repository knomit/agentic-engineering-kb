---
type: synthesis
domain: [agentic-engineering, prompting, context-engineering, evaluation, operations, cost]
confidence: 0.75
sources: 1
evidence_weight: 0.7014925373134329
entities: [Anthropic, Claude Code, reasoning effort, clear_thinking_20251015, ablation, long-horizon agents, intermediate reasoning]
refs: [kb/gotchas/ai/agents/prompting/verbosity/f1c005e1.md, kb/incidents/ai/agents/coding-agents/quality-regression/2c11f9dc.md, kb/gotchas/ai/agents/long-horizon/persistence/1a3b1ccf.md]
---
# Four documented ways an agent's intermediate reasoning gets truncated — and every one of them arrives disguised as something other than a capability cut

Four separately-documented failures share a mechanism that none of them names on its own: an agent's effective capability tracks how much of its intermediate reasoning survives into the next step, and every documented way that reasoning gets cut short PRESENTED AS SOMETHING ELSE. Three were shipped deliberately by people optimising for latency or cost, and the fourth is the model doing it to itself.

THE THREE OPERATOR-INFLICTED CUTS, all from Anthropic's April 2026 Claude Code postmortem:

1. A STYLE PREFERENCE. A system-prompt instruction to "keep text between tool calls to ≤25 words" and "keep final responses to ≤100 words" measured a 3% ablation drop on both Opus 4.6 and Opus 4.7. The between-tool-call text is where the model states what it just learned and what it intends next, so it conditions the following call; capping it removes reasoning the model would otherwise have conditioned on.

2. A LATENCY OPTIMISATION. The reasoning-effort default was lowered from `high` to `medium` to cut latency. Note the sharp part: the internal eval measured this CORRECTLY — "slightly lower intelligence with significantly less latency" — and the team shipped it anyway. The eval was not wrong; it simply did not encode the user's exchange rate between latency and intelligence. An accurate measurement is not by itself a correct decision.

3. A CACHE OPTIMISATION. A header intended to clear cached reasoning once after an hour of idle instead cleared thinking on every turn for the rest of the session, so memory loss compounded turn over turn.

THE FOURTH IS DIFFERENT IN KIND and should not be collapsed into the others: the model truncates its OWN reasoning. On cryptanalysis work where the honest prior is that the problem is intractable, "the models tend to think it is impossible to solve so they don't try; they need a good amount of prompting." Premature abandonment presents as a confident, well-reasoned decision to stop rather than as an error. No operator chose this one, which is why no configuration review would have caught it.

WHAT TO DO WITH IT. First, a diagnostic checklist for "the agent feels dumber" that does not require reproducing the failure: audit what has recently changed in the reasoning path — verbosity or tone instructions, effort/thinking-budget defaults, cache and context-clearing behaviour, compaction — before suspecting the model. Second, a gate: treat ANY prompt or config change motivated by tone, cost or latency as an intelligence-affecting change until an ablation says otherwise, which was Anthropic's own remedy (per-model evals for all system-prompt changes, soak periods and gradual rollouts). Third, for open-ended long-horizon work, the harness needs an explicit mechanism to push the agent past its own negative assessment, plus a stated bar for what counts as a result.

TWO SECONDARY SIGNALS worth wiring up, because the primary signal is absent by construction. The cache bug's second symptom was usage limits draining faster than expected — dropping reasoning blocks mid-session invalidates the prefix cache, so an unexplained COST or quota anomaly is a usable detector for a context-management bug, and may be the sharper of the two signals. And overlap defeats attribution: three small regressions running concurrently is what made the April signal unreadable, and the root-cause took over a week partly because two unrelated concurrent experiments masked the bug in testing.

WHAT THIS DOES NOT MEAN, carried from the sources because each blocks a specific misreading. The 3% figure is an ablation on ONE harness and TWO model versions — an order-of-magnitude signal, not a constant, and not a number to quote as a general cost of brevity. It says nothing against constraining the FINAL response alone, which was only half the instruction; the between-tool-call cap is the part sitting in the reasoning path, and the two halves should not be treated as one rule. The self-abandonment limb is the least supported of the four: it comes from a single reported research effort relayed second-hand, with no token accounting published and no controlled comparison against a differently-prompted run, so treat it as a failure mode to design against rather than a measured effect. And none of this argues for maximising verbosity or effort unconditionally — the reasoning-effort case is explicitly a TRADE that was measured and then mis-decided, not a setting with a strictly correct value; the failure was leaving the user's exchange rate out of the decision, not choosing `medium`.
