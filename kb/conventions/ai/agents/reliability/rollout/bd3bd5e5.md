---
kind: pragmatic
type: policy
domain: [agentic-engineering, reliability, operations, distributed-systems]
confidence: 0.85
sources: 0
entities: [Amazon, AWS Builders' Library, AWS Fault Injection Simulator, circuit breaker, instrumentation]
refs: ['https://builder.aws.com/content/3EuxuD6bWtQ6gEp9FaKQfd3Z2AM/using-dependency-isolation-to-contain-concurrency-overload', 'https://builder.aws.com/content/3Eupj3d2bo4fEvlzYbICMZNhQ3B/fairness-in-multi-tenant-systems']
---
# Ship concurrency limiters and quota rules in instrumentation-only mode first — and assume an untested limiter does not work

Amazon deploys a new concurrency bulkhead in 'instrumentation only' mode: the limiter measures and reports concurrency per breaker at the start of each request, but rejects nothing. Only once the observed median and maximum concurrency confirm the configured limit will not cause a background failure rate does it get flipped to enforcement mode. The same two-step is used for quota rule changes, which are deployed in an evaluation mode that verifies the rule would match the intended traffic before it goes live.

This buys two things: it prevents a limiter shipped with a wrong constant from becoming a self-inflicted outage, and it produces the concurrency time-series you need in order to pick the constant at all.

The instrumentation itself has to distinguish three outcomes that otherwise look identical in a metric: request rejected by the limiter, request timed out talking to the dependency, request failed talking to the dependency. Collapsing them makes it impossible to tell a tripped breaker from a broken dependency during an incident.

Amazon's closing position on the whole family of techniques is the strongest form of the rule: if you do not regularly exercise your dependency-isolation breakers — they use fault injection for this — you should assume they do not work. These mechanisms are easy to get wrong, only run in rare conditions, and therefore rot silently.

Agent-side application: the same discipline applies to guardrails, budget caps, and step-limit enforcement in a harness. A step cap or token budget that has never been deliberately tripped in a test is an untested code path on the exact line that is supposed to save you.
