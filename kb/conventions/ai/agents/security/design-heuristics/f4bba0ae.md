---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, security, prompt-injection, architecture, guardrails]
confidence: 0.8
sources: 1
entities: [OpenAI, social engineering, three-actor system, customer support agent, deterministic limits, prompt injection]
refs: ['https://openai.com/index/designing-agents-to-resist-prompt-injection/', 'kb://bc6eac5f37df/kb/invariants/ai/agents/security/prompt-injection/48c9de1b.md']
---
# Derive an agent's controls by asking what limits a human in the same seat would have — the frame assumes deception succeeds and bounds the blast radius instead

OpenAI's security team offers a concrete method for deriving agent controls, and it is more useful than the usual advice to "apply least privilege" because it tells you where to get the specific limits from. (Post dated 2026-03-11, authors Thomas Shadwell and Adrian Spânu; verified live and unchanged 2026-08-15.)

**THE FRAME.** An agent exposed to third-party content sits in the same three-actor structure as a human customer-support representative: it acts for an employer, and it is continuously exposed to external parties who may mislead it or apply pressure. OpenAI's move was to stop treating socially-engineered prompt injection as a novel class of problem and manage it the way the industry already manages social engineering against humans.

**THE PREMISE THAT DOES THE WORK.** In the human case nobody assumes the representative is never fooled. They are given rules, and it is *expected* that in an adversarial environment they will sometimes be misled — so the surrounding system is built to survive that. The controls that result are ones that bound the consequences of a deception that already succeeded, rather than ones that try to prevent it. The source's own examples are exactly two: deterministic limits on the amount of refund value that can go to a single customer, and flagging of potential phishing emails.

**THE DERIVATION RULE, which is the actionable part.** When integrating an AI model with an application system, OpenAI recommends asking what controls a human agent should have in **a similar situation** and implementing those.

*The following control list is this pack's illustration of the method, not OpenAI's — the post names only the two examples above.* Worked through for a refund desk, a human agent typically has a per-transaction cap, a daily total, a second approver above a threshold, an audit trail, and no direct database access; the method says those become the agent's controls, at those thresholds, rather than a generic "add a guardrail". The value of the heuristic is that it produces *specific numbers and specific approvers* from an existing operational design, which is the part "apply least privilege" never supplies.

Notice which properties this pushes you toward: the effective limits in the human case are **deterministic and enforced outside the actor** — the representative cannot raise their own refund cap. That is the same split as the rest of this pack's evidence, and it is why the heuristic tends to produce boundaries rather than suggestions.

**WHAT THE SOURCE SAYS ABOUT THE HEURISTIC'S LIMIT, AND WHAT IT LEAVES AMBIGUOUS.** The post's closing qualification is: "We expect that a maximally intelligent AI model will be able to resist social engineering better than a human agent, but this is not always feasible or cost-effective depending on the application."

Read that carefully, because **the referent of "this" is not disambiguated in the source.** It can be read as *deploying a maximally intelligent model* is not always feasible or cost-effective — i.e. you will often be running a weaker model and will therefore need the human-derived controls — or as *relying on model resistance instead of controls* is not always feasible. Both readings converge on the same practical advice, which is why the ambiguity is tolerable: implement the controls. What the source does **not** state is a condition under which the heuristic stops applying.

*Pack analysis, not the source's:* the qualification does imply the heuristic is calibrated to a capability regime rather than being a permanent architectural claim, and it suggests an escape clause — controls whose only justification is "a human in this seat would have needed one" are worth re-examining in a deployment where the model is *measurably* more resistant to social engineering than the human baseline. No such measurement is offered here, and absent one, assume you need the controls.
