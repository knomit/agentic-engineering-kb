---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, architecture, evaluation, security]
confidence: 0.75
sources: 1
entities: [Incalmo, MHBench, Claude Sonnet 4, Eugene Yan, attack graph]
motifs: [wrong-deciding-variable]
refs: ['https://eugeneyan.com/writing/cybersecurity-evals/']
---
# Harness architecture dominates model choice: the same model went from 3/40 to 37/40 networks with a better scaffold

The clearest published measurement of harness-versus-model leverage comes from MHBench, a multi-host network attack benchmark of 40 simulated networks. Claude Sonnet 4 driving the Incalmo framework captured assets in 37 of 40 networks. The SAME model without that framework managed 3 of 40. A greater-than-tenfold swing from scaffolding alone, on a fixed model.

What Incalmo supplies is worth naming because it generalises: decoupled planning and execution, auxiliary services the agent can call rather than reimplement, and an explicit attack graph — a structured representation of problem state that the agent reads and updates instead of holding it in context. The reviewer's conclusion was that these architectural choices outperformed model improvements alone.

The consequence for where to spend: when an agent is failing at a long-horizon task, upgrading the model is usually the more expensive and less effective lever than giving it a structured external state representation, splitting planning from execution, and providing services for the sub-steps it currently improvises. Two corroborating observations from the same survey: context bloat specifically impaired long-horizon planning in the multi-host scenarios, and decomposing objectives into subtasks improved the interpretability of partial progress — both harness-level changes.

The honest boundary, and the condition that decides it: this measurement comes from offensive-security benchmarks, where the task decomposes cleanly into discrete stages with verifiable outcomes and the state genuinely fits in a graph. Do not assume the tenfold figure transfers to open-ended tasks whose state cannot be externalised that way — there, model capability reasserts itself. What transfers is the direction of the effect and the order in which to try things.
