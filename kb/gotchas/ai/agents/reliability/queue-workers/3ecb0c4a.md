---
type: observation
domain: [agentic-engineering, reliability, architecture, operations, distributed-systems]
confidence: 0.85
sources: 1
entities: [Amazon, AWS Builders' Library, Amazon SQS, Amazon Kinesis, visibility timeout, black hole, queue poller]
refs: ['https://builder.aws.com/content/3Ev53O39izHCtWLzp4XU6t8PC1O/implementing-health-checks']
---
# A queue-polling agent worker has nothing removing it from service, so a broken one becomes a message black hole

Amazon's Builders' Library names this as a distinct failure pattern, and it is the one agent architectures are most exposed to because so many agent deployments are queue-driven rather than load-balancer-fronted.

The asymmetry: a server behind a load balancer has something external asking whether it is healthy and removing it if not. A server that gets its work by polling a queue — SQS, Kinesis, or any job broker — has NOTHING performing that role. It decides for itself whether to keep polling. So a worker with a full disk, exhausted file descriptors, expired credentials, or a dead tool subprocess keeps pulling messages off the queue as fast as it can receive them and fails every one of them. Because failing is fast, it out-competes the healthy workers for messages. The article makes the black-hole point explicit: this is the same dynamic as a least-requests load balancer favouring a fast-failing server, and it is HARDER to work around here, since there is no routing layer to fix.

The compensating factors it names, which are worth verifying you actually have rather than assuming:
- Visibility timeout / redelivery. If the worker fails to process a message, SQS redelivers it to another worker after the visibility timeout. Messages are not lost, but end-to-end latency rises — so the symptom is a latency and redelivery-count problem, not an error-rate problem, and error-rate alarms will not catch it.
- An alarm on message processing errors, and on processing delay, reported by the QUEUE service rather than by the worker — necessary because a worker broken enough to black-hole is often too broken to report its own failures.

The design consequence for agent workers: a queue-driven agent must gate its own polling on a health check, not just its request handling. 'Should I take another job' is the decision point that a load balancer would otherwise be making for it, and if the answer is unconditionally yes, one sick worker silently absorbs and drops a large share of the fleet's work. This compounds badly with agent workloads specifically, because a failed agent run is expensive to redo and the redelivered message lands on the SAME hungry black-hole worker with high probability.
