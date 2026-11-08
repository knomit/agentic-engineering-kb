---
type: principle
domain: [agentic-engineering, reliability, distributed-systems, operations, architecture]
confidence: 0.8
sources: 1
entities: [Amazon, AWS Builders' Library, rolling update, backwards compatible, protocol change, heartbeat, rollback]
motifs: [trivial-diff-breaks-contract, coexistence-breaks-the-contract]
refs: ['https://builder.aws.com/content/3F04j2yRAAMBuPSPs50xwXZqg01/ensuring-rollback-safety-during-deployments']
---
# The commonest reason a deployment cannot be rolled back is a protocol change, and the subtlest ones change no data format at all — a heartbeat period moved from five seconds to ten breaks rollback in both directions

Amazon reports that the most common reason a change cannot be rolled back is a change of protocol between the two versions, and the instructive case is the one that alters no serialization format whatsoever. Two servers agree to heartbeat every five seconds and to close the connection if none arrives in that window. A commit raises the period to ten seconds. Now neither direction is safe: during the rolling update the new version heartbeats every ten seconds while the old version, which has not changed its timeout, sees no heartbeat within five and terminates the connection. Across a large fleet that is an availability drop, produced by a one-number diff that reads as trivial in review.

The mechanism is specific to the coexistence window a rolling update creates: in a standalone process deployment is atomic and two versions never run together, so only the state format has to be readable both ways. In a distributed deployment the writer and the reader can be on different versions, communicating by RPC or through shared persistent state, and then any change to what either side EXPECTS of the other — timing, field presence, compression, encoding — is a protocol change.

Operational consequence: the review question is not "does the new version work?" but "does the new version work while talking to the old one, in both directions?". The source's own conclusion is that this cannot be settled by reading code or design docs, which is why it is tested explicitly rather than analysed.

Pack analysis, not stated by the source: the same window exists wherever an agent system versions a contract that two running components share — a tool schema an older worker still calls, a memory or checkpoint format a resumed run has to read, a sub-agent prompt contract. A timing or expectation change in any of those is this bug with different words.
