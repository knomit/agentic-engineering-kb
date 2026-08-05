---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, reliability, architecture, multi-agent, distributed-systems]
confidence: 0.85
sources: 1
entities: [Amazon, AWS Builders' Library, leader election, idempotency, sharding, DynamoDB, Step Functions, TLA+]
refs: ['https://builder.aws.com/content/3Ev0vH0hfkcUizISUWYTvHibtcp/leader-election-in-distributed-systems']
---
# You cannot guarantee exactly one orchestrator — decide whether the work is idempotent enough to tolerate two

Any agent system with a single coordinator — an orchestrator assigning subtasks, a scheduler driving long-running runs, a single writer to shared state — has made a leader-election decision whether or not it was named. Amazon's position, from the Builders' Library, sets the terms.

THE INVARIANT YOU DO NOT GET: in a distributed system it is not possible to guarantee exactly one leader. What you get is MOSTLY one leader, with windows of zero or two during failures. Designing as though 'one orchestrator' is enforced is the error.

THE DECISION THAT FOLLOWS, and it is the whole choice: what happens when there are two?
- If the work is IDEMPOTENT, two leaders cost some duplicated effort and nothing else. You can then choose a WEAKER, more available election mechanism and accept overlap. This is the cheaper branch and most agent orchestration can be pushed onto it.
- If the system genuinely needs at-most-one, it is much harder: the election must always be correct and consistent, and it must depose the outgoing leader BEFORE electing a new one — which is difficult because you often cannot distinguish a failed leader from one still working in another network partition.

So the design move is to make the work idempotent so you can buy the cheap branch, rather than to strengthen the election. Amazon says the same thing at the top: before implementing leader election at all, prefer idempotent APIs, optimistic locking, or a workflow service (they name Step Functions), which get many of the same benefits without the failure modes.

COSTS OF A SINGLE LEADER, beyond the obvious single point of failure: it is a single point of SCALING in both data size and request rate, and outgrowing it forces a re-architecture rather than a scale-out. It is a single point of TRUST with a high blast radius — a bad leader doing wrong work unchecked affects everything. And, least obvious and most relevant to shipping agent infrastructure: LEADER ELECTION BREAKS PARTIAL-DEPLOYMENT SAFETY. One-box, A/B, blue-green, and incremental deployment with automatic rollback all assume you can run two versions side by side; a single-leader system cannot, so you lose your safest rollout mechanisms.

Mitigation when you do need leaders: shard, so leadership is per-item and the system holds many leaders. This is how DynamoDB, EBS and EFS are built. The cost is design complexity and having to reason about the shard key.

Ordering rule for leader failure: always make work durable BEFORE announcing it complete (or explicitly tolerate the loss). Idempotency is what lets the incoming leader safely redrive work the outgoing one may have half-finished or finished without telling anyone.
