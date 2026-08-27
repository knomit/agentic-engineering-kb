---
type: pattern
domain: [agentic-engineering, operations, reliability, cost]
confidence: 0.8
sources: 0
entities: [Amazon, AWS Builders' Library, token bucket, burst capacity, rate limiting]
motifs: [burst-and-sustained-conflated]
refs: ['https://builder.aws.com/content/3Eupj3d2bo4fEvlzYbICMZNhQ3B/fairness-in-multi-tenant-systems']
---
# Compose two token buckets to allow bursts without an unbounded burst rate

A token bucket's burst capacity is the maximum number of tokens it can hold, and those tokens can all be spent instantly. Amazon's framing is that this is a double-edged sword: burst capacity is what lets you tolerate the natural non-uniformity of real traffic, but if you size it generously enough to do that, a client can consume the whole bucket in one instant and you have effectively removed the rate limit you thought you had configured.

The composition that resolves it: chain two buckets and require a token from both.
- Bucket one: low refill rate, high burst capacity. This is the long-run budget and permits a large total burst.
- Bucket two: high refill rate, low burst capacity. This caps how fast that burst may be drawn down.

The result is a large burst allowance that can only be spent at a bounded rate, which is what people usually mean when they ask for 'bursty but limited'.

Amazon adds a fleet-shape caveat that matters if you enforce locally: how uniform requests are across servers determines how relaxed the per-server burst values can be. Non-uniform request distribution calls for either more conservative bursting or distributed admission control.

This is directly reusable for agent rate limits, where the burst is real and desirable — a user kicking off a long task legitimately issues a rapid sequence of tool calls — but an unbounded burst means a runaway loop can drain a tenant's entire hourly budget before any monitoring fires.
