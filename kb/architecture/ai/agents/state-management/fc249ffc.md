---
type: pattern
domain: [agentic-engineering, architecture, state-management]
confidence: 0.7
sources: 1
entities: [12-factor-agents, HumanLayer, stateless reducer]
refs: ['https://github.com/humanlayer/12-factor-agents']
---
# Make the agent a stateless reducer and unify execution state with business state

The 12-factor-agents position on agent state, which is the framework-independent part worth taking:

- Factor 12, stateless reducer: model the agent as a pure function from (state, event) to new state, with no hidden internal state. What you gain is testability — you can replay any point of a run from its state alone — plus the ability to parallelise and to debug a failure without reproducing the whole session.
- Factor 5, unify execution state and business state: do not maintain the agent's step/status tracking separately from your application's domain state. Two trackers drift, and when they do you cannot tell whether the agent is stuck or the order actually shipped.
- Factor 6, launch/pause/resume via simple APIs: this falls out of the previous two almost for free, and is what makes long-running agents survivable. A monolithic in-memory loop cannot be paused, inspected mid-flight, or resumed after a crash.
- Factor 7, contact humans with tool calls: model human escalation as just another tool the agent can call, not as special-case control flow outside the loop. Escalation then gets the same logging, the same retry semantics, and the same resumability as everything else — and pausing for a human becomes indistinguishable from any other pending tool result.

These four are one design, not four tips: externalised state is what makes pause, resume, and human-in-the-loop cheap rather than each being a separate mechanism.
