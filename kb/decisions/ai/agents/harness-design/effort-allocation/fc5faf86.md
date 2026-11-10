---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, architecture, evaluation, security]
confidence: 0.9
sources: 3
entities: [Incalmo, ExpertPromptShell, MHBench, Multi-Host Bench, Claude Sonnet 4, Eugene Yan, attack graph, Equifax replica, OpenAI, Codex, ARC-AGI-3, GPT-5.6 Sol, context compaction, retained reasoning, OWASP, GenAI Security Project, harness variance]
motifs: [wrong-deciding-variable]
refs: ['https://eugeneyan.com/writing/cybersecurity-evals/', 'https://developers.openai.com/blog/codex-as-a-platform', 'https://genai.owasp.org/resource/llm-exploit-generation-guide-2-0/', 'https://genai.owasp.org/download/58316/?tmstv=1793097168', 'kb://bc6eac5f37df/kb/decisions/ai/agents/harness-design/build-vs-adopt/fac118c1.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/evaluation/benchmarks/static-vs-live/0b8318eb.md']
---
# Harness architecture dominates model choice: the same model went from 3/40 to 37/40 networks with a better scaffold

The clearest published measurement of harness-versus-model leverage comes from MHBench, a multi-host network attack benchmark of 40 simulated networks. Claude Sonnet 4 driving the Incalmo framework captured assets in 37 of 40 networks. The SAME model without that framework managed 3 of 40. A greater-than-tenfold swing from scaffolding alone, on a fixed model.

What Incalmo supplies is worth naming because it generalises: decoupled planning and execution, auxiliary services the agent can call rather than reimplement, and an explicit attack graph — a structured representation of problem state that the agent reads and updates instead of holding it in context. The reviewer's conclusion was that these architectural choices outperformed model improvements alone.

The consequence for where to spend: when an agent is failing at a long-horizon task, upgrading the model is usually the more expensive and less effective lever than giving it a structured external state representation, splitting planning from execution, and providing services for the sub-steps it currently improvises. Two corroborating observations from the same survey: context bloat specifically impaired long-horizon planning in the multi-host scenarios, and decomposing objectives into subtasks improved the interpretability of partial progress — both harness-level changes.

The honest boundary, and the condition that decides it: this measurement comes from offensive-security benchmarks, where the task decomposes cleanly into discrete stages with verifiable outcomes and the state genuinely fits in a graph. Do not assume the tenfold figure transfers to open-ended tasks whose state cannot be externalised that way — there, model capability reasserts itself. What transfers is the direction of the effect and the order in which to try things.

THE TWO SCAFFOLDS BY NAME, AND ONE PRECISION THE HEADLINE GLOSSES. The benchmark is Multi-Host Bench (MHBench). The baseline is a different scaffold, not a weaker prompt: "On the previous best system (ExpertPromptShell), Claude Sonnet 4 captured critical assets in just 3 out of 40 networks." The improved figure is "With Incalmo, that number jumped to 37 out of 40 networks, including the 50-host Equifax replica."

Worth knowing before citing this as a same-model comparison: the source names Claude Sonnet 4 only for the 3/40 figure. For 37/40 it says "that number", which refers back to the Sonnet 4 result, so the same-model reading is an implication the page supports rather than a sentence it states. The page's own conclusion is explicit and does not depend on that reading: "The experiments showed that the system framework matters far more than the underlying model."

A SECOND INDEPENDENT MEASUREMENT, FROM A DIFFERENT TASK FAMILY AND A DIFFERENT VENDOR, AND IT NAMES THE TWO FEATURES. OpenAI reports: "Harness design can materially change results: on ARC-AGI-3, retained reasoning and context compaction raised" — "GPT-5.6 Sol's score from 13.3% to 38.3% while reducing output tokens sixfold."

This matters for the spend argument beyond adding a second datapoint, because it breaks the assumption that scaffolding buys accuracy by spending more tokens. Here the score nearly tripled WHILE output tokens fell by a factor of six, so on this benchmark the harness change was Pareto-improving rather than a quality-for-cost trade. The two features named are both state-retention choices — what the harness carries forward between steps, and how it compresses what it carries — which is the same lever as this fact's external-state-representation finding, arrived at independently.

The boundary is the same as above and worth restating against this source too: ARC-AGI-3 is a puzzle benchmark with discrete steps and a verifiable outcome, which is exactly the shape where externalising state pays. Neither measurement establishes the effect on open-ended work.

A THIRD MEASUREMENT, AND THIS ONE PUTS A RATIO ON THE EFFECT RATHER THAN A PAIR OF SCORES. An OWASP GenAI Security Project assessment of cyber-capability benchmarks reports "harness variance roughly 7.8 times model variance", and separately that "the harness alone produced a 23.8-point gap on a fixed model pool". Holding the model set constant and changing only the scaffold moved the result by nearly a quarter of the scale.

What the ratio adds to the two score pairs above is a decision rule with a magnitude in it: if the harness contributes close to eight times the spread that the model does, then a model upgrade is the smaller of the two levers by roughly an order of magnitude, and a leaderboard gap smaller than the harness's own spread carries no information about the models at all. The same assessment's accompanying rule follows from this directly — a cyber score should not be accepted without the harness alongside k, trial count and the compute or cost budget.

The same boundary applies as to the other two measurements, and here it is narrower than the ratio's generality suggests: the 7.8x figure is drawn from offensive-security benchmarks, which is the third source from that one task family. The ARC-AGI-3 result is the only one of the three from a different domain, so the cross-domain evidence for the ratio's size remains one datapoint even though the direction of the effect now has three.
