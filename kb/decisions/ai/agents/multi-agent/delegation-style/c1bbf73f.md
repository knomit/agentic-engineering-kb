---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, multi-agent, architecture]
confidence: 0.85
sources: 3
entities: [OpenAI, Microsoft, handoff, manager pattern, agents as tools, approval surface, handoffDescription]
motifs: [wrong-deciding-variable]
refs: ['https://developers.openai.com/api/docs/guides/agents', 'https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns', 'https://developers.openai.com/api/docs/guides/agents/orchestration', 'kb://bc6eac5f37df/kb/decisions/ai/agents/multi-agent/f7dee43a.md']
---
# Manager (agents-as-tools) vs decentralized handoff: does control return to the caller?

Two distinct multi-agent delegation styles that get conflated, and the deciding question is whether control comes back.

Manager pattern / agents-as-tools — a coordinator invokes specialist agents the way it invokes any other tool. The specialist runs, returns a result, and control RETURNS to the manager, which retains the thread and decides what happens next. Use when a single entity should own the overall outcome and you want one place holding the full picture. This is what makes result validation possible: someone is still there to check the return value.

Decentralized handoff — control TRANSFERS to a peer agent, which now owns the conversation. The originator is out of the loop. Microsoft's framing: "Full control transfers from one agent to another agent," agents do not typically work in parallel, and the handoff chain yields a single result. Use when expertise requirements emerge mid-task and the new owner should genuinely take over, as with support triage routing to a billing specialist — the pattern exists for "scenarios in which the optimal agent for a task isn't known upfront or the task requirements become clear only during processing."

The trap in handoffs is that no agent holds the whole trajectory, so you need an explicit bound on handoff bouncing — A to B to A is a live failure mode with no natural termination. Microsoft lists it as a reason to avoid the pattern outright: "Avoiding an infinite handoff loop or avoiding excessive bouncing between agents is challenging," and their summary table names "Infinite handoff loops. Unpredictable routing paths" as the pattern's standing weakness.

Microsoft's guidance adds the complementary disqualifier: if the right specialist is identifiable from the initial input, do not use handoffs at all — "use deterministic routing or a simpler dispatcher that doesn't take an active role in processing. This dispatcher first classifies the input and then sends it to the appropriate agent." Handoff is for when the answer only becomes clear during processing; paying for a model to make a decision that a rule already determines buys latency and a failure mode for nothing. Two further avoid-conditions they name: when a suboptimal routing decision would itself produce a poor user experience, and when the task needs operations to run CONCURRENTLY — handoff is strictly one-active-agent-at-a-time, so it is the wrong pattern for anything parallel regardless of how the specialist is chosen.

Source dating: the Microsoft page is dated 2026-02-12, refreshed 2026-05-12, and is on a 180-day update cycle.

**OpenAI's orchestration guide states the same axis in the sharper form, and it is the form to ask the question in: who owns the final user-facing answer at each branch?** With a handoff, "Control moves to the specialist agent" and the specialist owns the next response for that branch. With agents as tools, "The manager keeps ownership of the reply" and the specialist is a bounded capability the manager calls. Decide the ownership first; the mechanism follows from it. Reach for agents-as-tools when the manager should synthesize the final answer, when the specialist does a bounded task such as summarization or classification, or when you want one stable outer workflow.

Its default is one agent — "Start with one agent whenever you can." — and it names four conditions that justify adding a specialist: a material improvement in capability isolation, policy isolation, prompt clarity, or trace legibility. The split is warranted only when the next branch needs different instructions, tools, or policy.

THE COST OF SPLITTING TOO EARLY, STATED AS THREE ITEMS, AND THE THIRD IS THE ONE THAT GOES UNCOUNTED: "Splitting too early creates more prompts, more traces, and more approval surfaces" without necessarily improving the workflow. Prompts and traces show up in a diff and a dashboard. An approval surface is a place a human now has to be, and it accrues silently, one per branch — so a decomposition that looks free in token terms can quietly add human latency to every request.

The SDK surface, for orientation: a `handoffs` list on the agent, optionally wrapping an entry in `handoff(...)`; a `handoffDescription` that should be "short and concrete"; `agent.asTool()` / `agent.as_tool()` with `toolName`/`tool_name` and `toolDescription`/`tool_description` for the agents-as-tools direction; and `lastAgent` plus resumable state for recovering which agent held the thread.

What this guide does NOT establish: it gives no numeric limits — no handoff counts, no depth, no timeouts, no token costs — and no determinism guarantees, so this choice is argued on design grounds alone. It is also a different axis from [[f7dee43a]], which decides multi-agent versus single-threaded on whether subtask outputs must be mutually consistent; this one decides, once you are already splitting, which of the two shapes to use.
