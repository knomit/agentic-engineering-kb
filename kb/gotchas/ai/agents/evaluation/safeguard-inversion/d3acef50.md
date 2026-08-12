---
kind: pragmatic
type: policy
domain: [agentic-engineering, security, evaluation, sandboxing, governance]
confidence: 0.9
sources: 2
entities: [Anthropic, OpenAI, UK AISI, Irregular, classifier, capability evaluation, blast radius]
refs: ['https://www.anthropic.com/news/investigating-incidents-cybersecurity-evals', 'https://openai.com/index/third-party-cyber-evaluations-involving-openai-models/']
---
# Evaluation environments run models with production safeguards deliberately switched off — so they need MORE containment than production, not less

The reason a capability evaluation is worth running is that it measures the model's underlying capability rather than the behaviour of the shipped product. Getting that measurement requires removing the very controls that make the shipped product safe, and both disclosing organisations say so plainly.

Anthropic: "The models in each of these evaluations ran without the standard safeguards we deploy when we make the model generally available (that is, they did not have the classifiers and monitoring we usually implement to prevent misuse)."

OpenAI, on UK AISI's setup: internet access was intentionally enabled "so agents could find their own tools and operate under conditions closer to a real attacker", and the cyber classifiers were disabled "to measure underlying capability". OpenAI generalises it: "Some cyber evaluations intentionally use custom configurations, including lowered safeguards to measure underlying capability—not how models ordinarily behave in publicly available deployments."

**THE INVERSION.** Standard engineering intuition ranks environments by blast radius: production gets the strongest controls, staging less, test least. For agent evaluation this is backwards. The eval environment is where the most capable model runs with classifiers off, monitoring reduced, and — in cyber evaluations specifically — an explicit objective to find and exploit weaknesses. Anthropic's stated conclusion is exactly this: "Evaluation environments that involve powerful autonomous capabilities _also_ require significant controls."

**THE PRACTICAL CONSEQUENCE.** Every safeguard you disable to get a clean capability measurement has to be replaced by an environmental control that does not depend on the model's cooperation — network isolation, egress policy, scoped credentials, out-of-band monitoring. Disabling a classifier without adding the compensating control is not a neutral measurement choice; it is a removal of the only thing that was watching. This also extends past your own infrastructure: OpenAI commits to applying "the same security standards" to third-party vendor infrastructure as to internal systems, after two of the four incidents happened at external testing partners.
