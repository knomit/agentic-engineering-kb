---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.8
sources: 2
entities: [OpenAI, Microsoft, handoff, manager pattern]
motifs: [wrong-deciding-variable]
refs: ['https://developers.openai.com/api/docs/guides/agents', 'https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns']
---
# Manager (agents-as-tools) vs decentralized handoff: does control return to the caller?

Two distinct multi-agent delegation styles that get conflated, and the deciding question is whether control comes back.

Manager pattern / agents-as-tools — a coordinator invokes specialist agents the way it invokes any other tool. The specialist runs, returns a result, and control RETURNS to the manager, which retains the thread and decides what happens next. Use when a single entity should own the overall outcome and you want one place holding the full picture. This is what makes result validation possible: someone is still there to check the return value.

Decentralized handoff — control TRANSFERS to a peer agent, which now owns the conversation. The originator is out of the loop. Microsoft's framing: "Full control transfers from one agent to another agent," agents do not typically work in parallel, and the handoff chain yields a single result. Use when expertise requirements emerge mid-task and the new owner should genuinely take over, as with support triage routing to a billing specialist — the pattern exists for "scenarios in which the optimal agent for a task isn't known upfront or the task requirements become clear only during processing."

The trap in handoffs is that no agent holds the whole trajectory, so you need an explicit bound on handoff bouncing — A to B to A is a live failure mode with no natural termination. Microsoft lists it as a reason to avoid the pattern outright: "Avoiding an infinite handoff loop or avoiding excessive bouncing between agents is challenging," and their summary table names "Infinite handoff loops. Unpredictable routing paths" as the pattern's standing weakness.

Microsoft's guidance adds the complementary disqualifier: if the right specialist is identifiable from the initial input, do not use handoffs at all — "use deterministic routing or a simpler dispatcher that doesn't take an active role in processing. This dispatcher first classifies the input and then sends it to the appropriate agent." Handoff is for when the answer only becomes clear during processing; paying for a model to make a decision that a rule already determines buys latency and a failure mode for nothing. Two further avoid-conditions they name and this fact previously omitted: when a suboptimal routing decision would itself produce a poor user experience, and when the task needs operations to run CONCURRENTLY — handoff is strictly one-active-agent-at-a-time, so it is the wrong pattern for anything parallel regardless of how the specialist is chosen.

VERIFIED (staleness pass, 2026-07-29): both refs live. The Microsoft page is dated 2026-02-12, refreshed 2026-05-12, on a 180-day update cycle. Every claim re-checked and confirmed, several now quoted verbatim rather than paraphrased, and two missing avoid-conditions added. Confidence 0.7 → 0.8.
