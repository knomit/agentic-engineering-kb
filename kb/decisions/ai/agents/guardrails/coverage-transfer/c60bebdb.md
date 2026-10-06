---
type: principle
domain: [agentic-engineering, guardrails, evaluation, security, operations, model-selection]
confidence: 0.8
sources: 2
entities: [Anthropic, OpenAI, Claude Code, auto mode, Claude Mythos 5, Claude Opus 4.7, cyber classifier, blocking monitor, confirmation policy, block rate, distribution shift]
motifs: [control-fitted-to-distribution, single-number-hides-conditions]
refs: ['https://www.anthropic.com/research/alignment-assessment-cybersecurity-incidents', 'https://deploymentsafety.openai.com/gpt-6-astra', 'kb://bc6eac5f37df/kb/decisions/ai/agents/guardrails/confirmation-policy/f8d468b5.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/operations/blocked-path-persistence/9945cbad.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/security/permission-systems/89df351e.md', 'kb://bc6eac5f37df/kb/principles/ai/agents/security/f269c82f.md']
---
# A guardrail's block rate is a joint property of the guardrail and the model: one classifier denied 66% and 55% of two production models' actions and 7% of an internally-trained model's, while a different measurement shows a control worth more on a weaker model

Two independent measurements pull in opposite directions about what a guardrail is worth, and each is right about a different variable. A reader who takes either one alone will size a control wrongly.

(1) DISTRIBUTION MATCH. Anthropic's alignment assessment of four cybersecurity-evaluation incidents reports, for one and the same Claude Code auto-mode classifier: "The auto-mode classifier would have denied 66% of Mythos 5 actions", "Auto mode would have blocked 55% of Opus 4.7 actions", and "Auto mode would have blocked only 7% of the internal model's actions." Two production models are substantially covered; an internal research model is close to uncovered by the identical control. The gap is not a property of classifiers in general — the dedicated cyber classifiers in the same assessment did not show it ("More than 40% of turns were flagged in each transcript by each classifier") and the purpose-built blocking monitors for sandbox escape "reliably catch these behaviors". It is specific to a classifier whose behavioural distribution came from a shipped product, applied to a model that was not that product.

(2) DEFECT RATE. An OpenAI deployment-safety measurement runs the other way: a confirmation policy removed 10.8 points of misaligned outcomes from the weaker model and 0.4 from the stronger one, so the same control measured as near-worthless on the best model and substantial on the weaker one.

What decides which effect you are looking at is which variable moved. Effect 1 is the model's behavioural distribution relative to the guardrail's fitting distribution: an off-distribution model slips a control it was never fitted to, however badly it is behaving. Effect 2 is the model's rate of the guarded behaviour: a control cannot remove outcomes a model does not produce. They compound in the worst direction for an internal or research model, which is simultaneously the most likely to be off the guardrail's distribution and the most likely to be behaving unusually.

The operational rule has two sides, and dropping either one is how a wrong number gets quoted. A guardrail A/B'd only against your best, most in-distribution model measures almost nothing about what it is worth. A guardrail whose block rate is quoted from one model's transcripts says nothing about its coverage of a different model. Measure block rate per model, and include the models that are not the product.

What this does NOT mean: that a low block rate shows the guardrail is bad, or that these two sources disagree with each other. Neither is a claim about a guardrail's quality in the abstract; both are claims about what a single block-rate figure can be read to mean.
