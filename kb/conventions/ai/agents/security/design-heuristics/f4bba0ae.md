---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, security, prompt-injection, architecture, guardrails]
confidence: 0.75
sources: 1
entities: [OpenAI, social engineering, three-actor system, customer support agent, deterministic limits, prompt injection]
refs: ['https://openai.com/index/designing-agents-to-resist-prompt-injection/', 'kb://bc6eac5f37df/kb/invariants/ai/agents/security/prompt-injection/48c9de1b.md']
---
# Derive an agent's controls by asking what limits a human in the same seat would have — the frame assumes deception succeeds and bounds the blast radius instead

OpenAI's security team offers a concrete method for deriving agent controls, and it is more useful than the usual advice to "apply least privilege" because it tells you where to get the specific limits from.

**THE FRAME.** An agent exposed to third-party content sits in the same three-actor structure as a human customer-support representative: it acts for an employer, and it is continuously exposed to external parties who may mislead it or apply pressure. OpenAI's move was to stop treating socially-engineered prompt injection as a novel class of problem and manage it the way the industry already manages social engineering against humans.

**THE PREMISE THAT DOES THE WORK.** In the human case nobody assumes the representative is never fooled. They are given rules, and it is *expected* that in an adversarial environment they will sometimes be misled — so the surrounding system is built to survive that. The controls that result are ones that bound the consequences of a deception that already succeeded, rather than ones that try to prevent it. The source's own examples: deterministic caps on how much refund value can go to a single customer, and flagging of likely phishing.

**THE DERIVATION RULE, which is the actionable part.** When integrating a model into an application, OpenAI recommends asking what controls a human agent should have in the same situation, and implementing those. This is a cheap, repeatable way to generate a specific control list for a specific product: a human refund agent has a per-transaction cap, a daily total, a second approver above a threshold, an audit trail, and no direct database access — so those are the controls the agent needs, at those thresholds, rather than a generic "add a guardrail".

Notice which properties this pushes you toward: the effective limits in the human case are **deterministic and enforced outside the actor** — the representative cannot raise their own refund cap. That is the same split as the rest of this pack's evidence, and it is why the heuristic tends to produce boundaries rather than suggestions.

**THE BOUNDARY ON THE HEURISTIC, stated by the source.** OpenAI expects that a sufficiently capable model will eventually resist social engineering better than a human representative does, but says this is not always feasible or cost-effective depending on the application. So this is a stance for the current capability regime, not a permanent architectural claim — and it argues against paying for controls whose only justification is that a human would have needed them, in a deployment where the model is measurably more resistant than the human baseline. Absent that measurement, assume you need the controls.
