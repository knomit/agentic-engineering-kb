---
type: pattern
domain: [agentic-engineering, reliability, distributed-systems, architecture, tools, operations]
confidence: 0.85
sources: 1
entities: [Amazon, AWS Builders' Library, load shedding, brownout, pagination, goodput, admission control]
motifs: [in-flight-work-starved]
refs: ['https://builder.aws.com/content/3Eun1EEyX6p2e3VYNyRLSJzLuMV/using-load-shedding-to-avoid-overload']
---
# When shedding, prioritise requests that FINISH work over requests that START it — the ordering is counter-intuitive and it is what protects goodput

Under overload the instinct is to prioritise by client importance. Amazon's more useful axis is position in a multi-step interaction, and the ordering inverts what arrival order would give you:

- Given a service with start() and end() APIs where a client must call both to complete anything, prioritise end() over start(). Prioritising start() admits work that then cannot be completed, which is the definition of a brownout.
- Given a paginated API, prioritise page N over page 1. A client that fails at page N-1 and discards the results has wasted N-2 calls plus every retry along the way, so the LATER pages are the ones worth protecting.

The unifying rule: shedding a request that would have completed a chain destroys all the work already spent on that chain, whereas shedding a request that would have started one destroys nothing.

For agents this is the admission policy for a tool server or orchestrator: a subagent's final write-back, a session's commit or finalise call, and the later pages of a search or listing tool should all outrank fresh task submissions. It also argues against agents paginating open-endedly through a service inside a synchronous operation — that pattern maximises the amount of in-flight work a single shed request can destroy.

Caveat Amazon flags: in a large architecture where many services each apply their own prioritisation heuristics, conflicting heuristics can hurt system-wide availability. Push prioritisation as early as possible — ideally at the service that receives the original request — rather than making independent local decisions at every layer.
