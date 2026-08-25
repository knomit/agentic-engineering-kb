---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, reliability, architecture, distributed-systems]
confidence: 0.8
sources: 0
entities: [Amazon, AWS Builders' Library, circuit breaker, token bucket, bulkhead, Resilience4j, AWS Lambda]
motifs: [disagreement-dissolves-on-distinction]
refs: ['https://builder.aws.com/content/3EuxuD6bWtQ6gEp9FaKQfd3Z2AM/using-dependency-isolation-to-contain-concurrency-overload', 'https://builder.aws.com/content/3EumjoZascWd1oZiEgL8ORlv3qE/timeouts-retries-and-backoff-with-jitter']
---
# Amazon both warns against circuit breakers and builds them everywhere — the split is retry control vs concurrency isolation

Two AWS Builders' Library articles take opposite-sounding positions and both are right about different things. Do not flatten them.

AGAINST: the timeouts/retries article argues Amazon generally prefers a retry token bucket to a circuit breaker, because a breaker introduces modal behaviour — the system behaves one way open and another way closed — and that mode is rarely exercised, hard to test, and can keep a recovered dependency shut out.

FOR: the dependency-isolation article describes bulkheads (explicitly 'a form of circuit breaker', the name Resilience4j gives them) as a core Amazon pattern, baked into AWS Lambda as per-function concurrency and into the EC2 control plane's regional frontend.

The reconciling condition is what the breaker is deciding:
- Breaking on ERROR RATE to suppress retries is the case Amazon is sceptical of. A token bucket does the same job with no mode: it just runs out of tokens and refills continuously, so recovery is automatic and gradual rather than a step change.
- Breaking on CONCURRENCY to protect a finite local resource is the case Amazon endorses. Here the 'mode' is not a heuristic guess about the dependency's health — it is a hard local fact about thread, memory, or socket exhaustion, and there is no non-modal alternative because the resource itself is finite.

Both articles agree on the mitigation for the residual risk: the modal path must be regularly exercised (fault injection) and deployed instrumentation-first, or it should be assumed broken.

Practical reading for an agent harness: use a retry budget/token bucket to govern retrying a flaky tool or model endpoint; use a concurrency bulkhead to govern how many in-flight calls that tool may hold. They are different mechanisms answering different questions, and choosing one does not substitute for the other.
