---
type: observation
domain: [agentic-engineering, operations, reliability, distributed-systems, incident-response, architecture]
confidence: 0.85
sources: 1
entities: [OpenAI, Microsoft Azure, Habitat, Azure Cosmos DB, regional failover, failback, connection stampede, gateway mode, co-managed service, thundering herd]
motifs: [recovery-action-becomes-outage, untested-at-production-scale]
refs: ['https://openai.com/index/scaling-storage-one-billion-users-part-two/']
---
# Failing back after a regional outage caused a second outage: the client reconnected every connection to the recovered region although only some partitions had moved back, and neither team had ever tested failover at that scale

A documented two-outage sequence at an operator running one of the largest deployments of a managed database, published as the reason it changed how it works with its cloud provider.

FIRST OUTAGE, late 2024: "a power outage struck the primary Azure region for one of our largest Azure Cosmos DB accounts. In the resulting failover exercise, we realized that our largest accounts would take several hours to fail over to a secondary region, something neither our team nor the Azure Cosmos DB team had tested at our scale." The failover mechanism existed and was supported; what was untested was its behaviour at this data volume, and the discovery happened during a real incident.

SECOND OUTAGE, about a month later, DURING THE FAILBACK: "while failing those accounts back to the original region, we triggered another serious outage. A connection stampede to the original region overwhelmed the original region's Azure Cosmos DB gateway. A quirk in how the gateway-mode Azure Cosmos DB client handled failovers caused all clients to immediately establish connections and send requests to the original region, even though only a subset of physical partitions had moved back to that region."

The mechanism is worth stating precisely because it generalises: the client treated a region-level signal as authoritative for all of its traffic, while the actual migration was partition-by-partition and incomplete. Every client therefore converged on a region that could serve only part of what it was being asked for, and the recovery action became the outage. Two separable defects — an all-at-once reconnect with no stagger, and a region-granular routing decision over partition-granular state.

THE FIX WAS ORGANISATIONAL AS WELL AS TECHNICAL, and the operator is explicit that the per-incident root causes were not the real lesson: "In each outage, both OpenAI and Azure ran through their incident management processes, with a number of root causes identified and fixes deployed. But these outages were symptoms of a larger systemic issue between the way our team and Azure Cosmos DB team operated and tested." The stated general claim: "When companies grow to OpenAI's scale, managed services become less 'managed.' Many workloads become outliers in the cloud provider's infrastructure."

What the co-managed model consists of, concretely: joint monitoring from the service layers "down into Azure Cosmos DB's physical storage layers"; "a production-sized but non-production Azure Cosmos DB account" to test changes against; joint SDK testing; and "direct engineering access to each other through Teams" with "ways to directly page each other without going through support tiers". The named joint work includes control-plane and gateway scalability, "load protection and caching of various Azure Cosmos DB metadata in their gateway to protect the Azure Cosmos DB metadata partition", connection pooling and reuse to reduce pressure from the client fleet, workload colocation, and isolating critical from offline workloads in different VPCs.

WHAT TO TAKE FROM IT: a failover path you have not exercised at your production data volume is not a tested failover path, and failback deserves its own test because it has a failure mode failover does not — a healthy region that everything rushes back to at once. Scale context for calibration: the largest account "stores 10s of petabytes of data and serves more than 20M QPS", with the platform at over 500 petabytes overall.

WHAT THIS DOES NOT MEAN: this is not an argument against managed services, which the operator credits for letting them "move fast and focus on business goals" early on. The claim is bounded to the point where your workload becomes an outlier in the provider's fleet, at which point the provider's untested edges become yours.
