---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, reliability, distributed-systems, operations]
confidence: 0.85
sources: 1
entities: [Amazon, AWS Builders' Library, SO_RCVTIMEO, TLS handshake, p99.9]
motifs: [threshold-encodes-unmeasured-distribution]
refs: ['https://builder.aws.com/content/3EumjoZascWd1oZiEgL8ORlv3qE/timeouts-retries-and-backoff-with-jitter']
---
# Pick a timeout by choosing an acceptable false-timeout rate and reading that latency percentile off the downstream service

Amazon's method for choosing a timeout value, from the Builders' Library: decide what rate of false timeouts you will tolerate (their worked example is 0.1%), then set the timeout to the corresponding latency percentile of the downstream service (p99.9 for 0.1%). This replaces the usual practice of picking a round number.

Two stated conditions where the method fails:
1. Clients with substantial network latency — anything over the internet rather than intra-Region. Downstream-measured percentiles omit client-side network time, so you must add reasonable worst-case network latency, remembering clients can be global.
2. Services with tight latency bounds where p99.9 is close to p50. Here the percentile leaves no headroom, and a small latency increase converts into a large number of timeouts. Pad deliberately.

Setting the timeout too low is not the safe direction: it raises backend traffic and latency because too many requests are retried, and a small latency increase on the backend can then cascade into a full outage as everything starts retrying at once.

The gotcha that costs a day: verify what the timer actually covers. Amazon hit a case where a 20ms timeout was silently including new TLS connection establishment, so a burst of timeouts appeared only immediately after each deployment, when fresh servers had no warm connections — and vanished the rest of the time, making it look intermittent. Their durable fix was to establish connections at process startup before the host receives traffic, not to raise the timeout. Related traps: Linux SO_RCVTIMEO is unsuitable as an end-to-end socket timeout (Java exposes it directly; Go provides better mechanisms), and many implementations leave DNS resolution and TLS handshakes outside the timeout entirely. Prefer the timeouts built into well-tested clients over rolling your own.
