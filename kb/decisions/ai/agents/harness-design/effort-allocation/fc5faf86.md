---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, architecture, evaluation, security]
confidence: 0.8
sources: 1
entities: [Incalmo, ExpertPromptShell, MHBench, Multi-Host Bench, Claude Sonnet 4, Eugene Yan, attack graph, Equifax replica]
motifs: [wrong-deciding-variable]
refs: ['https://eugeneyan.com/writing/cybersecurity-evals/']
---
# Harness architecture dominates model choice: the same model went from 3/40 to 37/40 networks with a better scaffold

The clearest published measurement of harness-versus-model leverage comes from MHBench, a multi-host network attack benchmark of 40 simulated networks. Claude Sonnet 4 driving the Incalmo framework captured assets in 37 of 40 networks. The SAME model without that framework managed 3 of 40. A greater-than-tenfold swing from scaffolding alone, on a fixed model.

What Incalmo supplies is worth naming because it generalises: decoupled planning and execution, auxiliary services the agent can call rather than reimplement, and an explicit attack graph — a structured representation of problem state that the agent reads and updates instead of holding it in context. The reviewer's conclusion was that these architectural choices outperformed model improvements alone.

The consequence for where to spend: when an agent is failing at a long-horizon task, upgrading the model is usually the more expensive and less effective lever than giving it a structured external state representation, splitting planning from execution, and providing services for the sub-steps it currently improvises. Two corroborating observations from the same survey: context bloat specifically impaired long-horizon planning in the multi-host scenarios, and decomposing objectives into subtasks improved the interpretability of partial progress — both harness-level changes.

The honest boundary, and the condition that decides it: this measurement comes from offensive-security benchmarks, where the task decomposes cleanly into discrete stages with verifiable outcomes and the state genuinely fits in a graph. Do not assume the tenfold figure transfers to open-ended tasks whose state cannot be externalised that way — there, model capability reasserts itself. What transfers is the direction of the effect and the order in which to try things.

THE TWO SCAFFOLDS BY NAME, AND ONE PRECISION THE HEADLINE GLOSSES. The benchmark is Multi-Host Bench (MHBench). The baseline is a different scaffold, not a weaker prompt: "On the previous best system (ExpertPromptShell), Claude Sonnet 4 captured critical assets in just 3 out of 40 networks." The improved figure is "With Incalmo, that number jumped to 37 out of 40 networks, including the 50-host Equifax replica."

Worth knowing before citing this as a same-model comparison: the source names Claude Sonnet 4 only for the 3/40 figure. For 37/40 it says "that number", which refers back to the Sonnet 4 result, so the same-model reading is an implication the page supports rather than a sentence it states. The page's own conclusion is explicit and does not depend on that reading: "The experiments showed that the system framework matters far more than the underlying model."
