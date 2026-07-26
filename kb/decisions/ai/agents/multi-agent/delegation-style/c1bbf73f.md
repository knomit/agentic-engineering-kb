---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.7
sources: 2
entities: [OpenAI, Microsoft, handoff, manager pattern]
refs: ['https://developers.openai.com/api/docs/guides/agents', 'https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns']
---
# Manager (agents-as-tools) vs decentralized handoff: does control return to the caller?

Two distinct multi-agent delegation styles that get conflated, and the deciding question is whether control comes back.

Manager pattern / agents-as-tools — a coordinator invokes specialist agents the way it invokes any other tool. The specialist runs, returns a result, and control RETURNS to the manager, which retains the thread and decides what happens next. Use when a single entity should own the overall outcome and you want one place holding the full picture. This is what makes result validation possible: someone is still there to check the return value.

Decentralized handoff — control TRANSFERS to a peer agent, which now owns the conversation. The originator is out of the loop. Use when expertise requirements emerge mid-task and the new owner should genuinely take over, as with support triage routing to a billing specialist.

The trap in handoffs is that no agent holds the whole trajectory, so you need an explicit bound on handoff bouncing — A to B to A is a live failure mode with no natural termination. Microsoft's guidance adds the complementary disqualifier: if the right specialist is identifiable from the initial input, do not use handoffs at all, use deterministic routing or a plain classifying dispatcher. Handoff is for when the answer only becomes clear during processing; paying for a model to make a decision that a rule already determines buys latency and a failure mode for nothing.
