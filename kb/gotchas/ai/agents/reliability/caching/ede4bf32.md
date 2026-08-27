---
type: observation
domain: [agentic-engineering, reliability, architecture, distributed-systems, performance]
confidence: 0.85
sources: 1
entities: [Amazon, AWS Builders' Library, Colm MacCarthaigh, cache, anti-fragility, modal behaviour, cascading failure]
motifs: [mitigation-becomes-steady-state, common-cause-synchronises-demand]
refs: ['https://builder.aws.com/content/3F05oqNtNUWxHJ5r6L6I2HrH4rI/reliability-constant-work-and-a-good-cup-of-coffee']
---
# A cache looks anti-fragile and is actually a mode — it gets better under load right up until it collapses and takes its backing service with it

The trap named directly in Amazon's constant-work article. Caches are the example everyone reaches for when told that a good pattern should perform BETTER under stress: they improve response times, and they improve them more as load rises and hit rates climb. But most caches HAVE MODES, and modes are the thing constant-work design exists to eliminate.

The two mode transitions that hurt:
- **Empty/cold cache**: response times get much worse, and that alone can destabilise the system. Any event that empties the cache — a deploy, a restart, an eviction wave, a key-schema change — moves the whole system into its slow mode at once.
- **Cache rendered ineffective by too much load**: the traffic it was absorbing now lands directly on the backing source, which was never scaled for it, and the source falls over. This is a cascading failure, and it is triggered by the success condition (high load), not by any component being broken.

The conclusion to carry: caches appear anti-fragile at first but most AMPLIFY fragility when over-stressed. That does not mean do not cache — it means size and test the backing service for the cache being absent, treat cold-start as a load case you have measured rather than a transient, and never let a cache be the reason a capacity number looks affordable.

This is the same shape as the documented 2001 amazon.com outage, where a cache-miss fallback to the database took down the website and every fulfillment center — there the cache's failure mode was an explicit fallback path; here it is the implicit one. Amazon states that building a genuinely anti-fragile cache is possible but is its own body of work, not a default property you get by adding one.

For agent systems the caches in question are prompt/prefix caches, embedding and retrieval caches, tool-result caches, and model-response caches. Each has the same two transitions, and the second one — a cache-miss storm arriving at a rate-limited model or vector store — is the one that converts a latency problem into an outage.
