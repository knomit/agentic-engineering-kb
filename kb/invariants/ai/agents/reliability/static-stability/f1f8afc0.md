---
type: principle
domain: [agentic-engineering, reliability, architecture, distributed-systems, operations]
confidence: 0.85
sources: 1
entities: [Amazon, AWS Builders' Library, static stability, control plane, data plane, Amazon S3, AWS Hyperplane]
refs: ['https://builder.aws.com/content/3EukISjbJAGNdrxjKaN6RG0wlHG/avoiding-overload-in-distributed-systems-by-putting-the-smaller-service-in-control']
---
# An agent must keep running on its last known good configuration when the control plane is down — including agents that start DURING the outage

Static stability is the named property: the data plane continues operating on the configuration it already has when the control plane is unavailable. Amazon calls it out as a desirable attribute of distributed systems and as a direct benefit of the pattern where a control service publishes configuration to a hyperscale store (S3) that workers poll and cache locally, rather than serving it from a request-scoped API.

The clause that carries the weight, and the one implementations usually miss: 'the data plane can continue running with the last known configuration, EVEN AS SERVERS COME IN AND OUT OF SERVICE.' Surviving a control-plane outage on warm in-memory cache is easy and is not static stability. Static stability means a worker that boots cold during the outage, or one that autoscaling adds during it, also comes up working. That requires the last-known-good configuration to be durable and reachable independently of the control plane — on disk, in an image, or in the object store — not merely cached in a running process.

For agent platforms the configuration in question is the system prompt, the tool and skill catalogue, model routing and fallback policy, per-tenant limits, and credentials scope. If any of these is fetched from a control service at agent-process startup with no durable local fallback, then a control-plane blip does not degrade the fleet — it prevents every new agent process from starting, which is precisely when a fleet is restarting and needs to start the most. The failure is invisible in steady state and total during recovery.

The tradeoff to state honestly rather than pretend away: static stability means running on stale configuration, so any control action that must take effect promptly — revoking a tool, disabling a tenant, killing a runaway model version — cannot rely on the same path. Those need their own fast channel with its own failure mode, which is the argument for the inverted push architectures rather than for polling.
