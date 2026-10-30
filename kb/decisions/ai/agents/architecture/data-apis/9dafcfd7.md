---
type: observation
domain: [agentic-engineering, architecture, distributed-systems, reliability, operations]
confidence: 0.85
sources: 1
entities: [OpenAI, Habitat, TAO, Azure Cosmos DB, Rockset, change data capture, Postgres, NoSQL, partitioning]
motifs: [unbounded-fanout-at-interface, capability-removed-not-optimised]
refs: ['https://openai.com/index/scaling-storage-one-billion-users-part-one/']
---
# Habitat's deliberate refusal of a powerful query API is what let it scale — no unbounded queries, object-and-edge NoSQL only, with complex querying pushed to a CDC-fed replica the client team scales itself

OpenAI states the tradeoff in its own words: "The lack of a powerful API is an explicit tradeoff in Habitat's design." Habitat exposes a simple NoSQL API over client-defined object and edge types, inspired by TAO. Clients predefine the types and how they relate, and the API does not support graph traversal beyond querying a particular object's direct edges. There are no unbounded queries a client can express.

The reason is a cost imbalance at the interface, named directly: "it is cheap and easy to write SQL queries that are expensive and hard to run." Before Habitat, most of OpenAI's online data was on Postgres, where reviewing every query and schema change for good behaviour worked until the team and product count grew, after which it "became unmanageable and was a frequent cause of outages where a single expensive new query on a hot path took out the database." The design target is "simple, predictable, constant-work requests"; the thing refused is "Requests with unpredictable fanout", which "complicate isolation, load balancing, and introduce latency cliffs that are hard to scale for both the service and its clients."

The price is paid openly. Graph traversal is inefficient by construction: each object and its edges are colocated in one storage partition, but nothing colocates an object with the remote objects its edges point at, so a single hop "may require fetching from two entirely different Azure Cosmos DB accounts stored in different regions." Clients that genuinely need complex queries get an escape hatch rather than an API change — change data capture streams Habitat's changes into per-team Rockset instances in near-real-time, which each client team scales itself. That friction is deliberate, and it also isolates online storage from analytical and search load.

The operational consequence for anyone designing an agent's data or tool layer: the lever is making the expensive request impossible to EXPRESS, not making it fast. An interface where a costly request is cheap to issue moves the blast radius from the caller to the platform, and review does not scale past the point where every team can add a query.

What this does NOT mean: not "avoid SQL", and not "deny the complex query". The claim is about where unbounded fanout may be expressed at all, and the same design keeps an explicit, documented path for the queries the main API refuses, with the operational burden placed on the client that wants them.
