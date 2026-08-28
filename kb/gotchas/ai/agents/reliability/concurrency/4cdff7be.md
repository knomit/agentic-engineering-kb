---
type: observation
domain: [agentic-engineering, reliability, distributed-systems, architecture]
confidence: 0.8
sources: 1
entities: [Amazon, AWS Builders' Library, modal behaviour, exponential backoff, constant work]
motifs: [measured-scope-excludes-cost]
refs: ['https://builder.aws.com/content/3EuxuD6bWtQ6gEp9FaKQfd3Z2AM/using-dependency-isolation-to-contain-concurrency-overload']
---
# Concurrency blows up even when every dependency is fast — guard the code that calls the dependency, not the remote call

Amazon's observation is that a service can hit concurrency limits with all of its dependencies responding normally. Two mechanisms, both of which look like a healthy dependency on the dependency's own dashboards:

1. RETRIES AND BACKOFF. A dependency returning errors or throttles causes the client library or SDK to retry, and backoff means the client deliberately sleeps between attempts. The dependency's per-call latency is fine; the caller's end-to-end latency for that codepath multiplies, and concurrency multiplies with it. Backoff makes this dramatically worse, not better, from the caller's resource-consumption point of view.

2. MODAL BUSINESS LOGIC. Amazon's example: a ListTransactions API paginating a database 10 rows at a time. Typical queries return 4 rows, so one database call per request. A client changes to longer time ranges returning 100 rows, and it becomes 10 back-to-back calls. Remote-call latency is unchanged; the request now occupies concurrency 10x longer.

Both are 'modal behaviour' — the same code is cheap in one mode and expensive in another. The prescription is to instrument and bulkhead the concurrency of the whole codepath that uses a dependency, not just the time spent inside the remote call, because only the former captures retry sleeps and loop counts. Amazon's structural counter-measure is to design for constant work per request so the modes collapse.

For agents this is the common case rather than the exception: agent loops are inherently modal (a turn may take 1 tool call or 40), and retry-with-backoff around model and tool calls is standard. An agent-concurrency limit measured on model-call time alone will read as healthy while the harness runs out of workers.
