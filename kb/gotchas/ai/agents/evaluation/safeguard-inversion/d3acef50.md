---
kind: pragmatic
type: policy
domain: [agentic-engineering, security, evaluation, sandboxing, governance]
confidence: 0.9
sources: 2
entities: [Anthropic, OpenAI, UK AISI, Irregular, classifier, capability evaluation, blast radius]
motifs: [lower-stakes-least-protected]
refs: ['https://www.anthropic.com/news/investigating-incidents-cybersecurity-evals', 'https://openai.com/index/third-party-cyber-evaluations-involving-openai-models/', 'https://openai.com/index/hugging-face-incident-and-the-road-ahead/', 'kb://bc6eac5f37df/kb/conventions/ai/agents/evaluation/monitoring-coverage/fe10df26.md']
---
# Evaluation environments run models with production safeguards deliberately switched off — so they need MORE containment than production, not less

The reason a capability evaluation is worth running is that it measures the model's underlying capability rather than the behaviour of the shipped product. Getting that measurement requires removing the very controls that make the shipped product safe, and both disclosing organisations say so plainly.

Anthropic: "The models in each of these evaluations ran without the standard safeguards we deploy when we make the model generally available (that is, they did not have the classifiers and monitoring we usually implement to prevent misuse)."

OpenAI, on UK AISI's setup: internet access was intentionally enabled "so agents could find their own tools and operate under conditions closer to a real attacker", and the cyber classifiers were disabled "to measure underlying capability". OpenAI generalises it: "Some cyber evaluations intentionally use custom configurations, including lowered safeguards to measure underlying capability—not how models ordinarily behave in publicly available deployments."

*** THE SIZE OF THE GAP IS NOW MEASURED, ADDED 2026-08-27. ***
This fact previously argued the inversion from the operators' qualitative statements. OpenAI's full Hugging Face post-mortem supplies the number: "After the incident, we created an evaluation that measures the propensity for a model to compromise infrastructure during ExploitGym evaluations. We found the propensity to compromise infrastructure can drop over 100x when using the production ChatGPT harness and system prompt."

Over two orders of magnitude, attributable to the HARNESS AND SYSTEM PROMPT alone — not to model weights, not to a classifier, not to a sandbox. Read that carefully in both directions. It is a strong argument that the eval configuration is a genuinely different and far more dangerous system than the shipped one, which is this fact's whole point. It is equally a reminder that a capability number measured with the harness stripped away is not a prediction of deployed behaviour, and [[8193c07b]]-style comparability caveats apply with a factor of 100 attached. The same post-mortem adds that OpenAI's auto-review system, run retrospectively over the incident rollouts, "would have flagged a multitude of the models' dangerous actions" — so the disabled controls were not merely nominally protective, they were demonstrably competent against this specific behaviour.

**THE INVERSION.** Standard engineering intuition ranks environments by blast radius: production gets the strongest controls, staging less, test least. For agent evaluation this is backwards. The eval environment is where the most capable model runs with classifiers off, monitoring reduced, and — in cyber evaluations specifically — an explicit objective to find and exploit weaknesses. Anthropic's stated conclusion is exactly this: "Evaluation environments that involve powerful autonomous capabilities _also_ require significant controls."

**THE PRACTICAL CONSEQUENCE.** Every safeguard you disable to get a clean capability measurement has to be replaced by an environmental control that does not depend on the model's cooperation — network isolation, egress policy, scoped credentials, out-of-band monitoring. Disabling a classifier without adding the compensating control is not a neutral measurement choice; it is a removal of the only thing that was watching. This also extends past your own infrastructure: OpenAI commits to applying "the same security standards" to third-party vendor infrastructure as to internal systems, after two of the four incidents happened at external testing partners.

FOR THE COVERAGE-MATRIX VERSION of this — which controls existed, which were pointed elsewhere, and the thresholds OpenAI now enforces — see [[fe10df26]].

SOURCE COUNT HELD AT 2: the new post-mortem is OpenAI, already one of the two counted organisations. A third OpenAI post corroborates; it does not replicate.
