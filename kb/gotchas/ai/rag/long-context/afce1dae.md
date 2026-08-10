---
type: observation
domain: [agentic-engineering, rag, context-engineering, evaluation]
confidence: 0.75
sources: 1
entities: [Databricks, Claude 3.5 Sonnet, GPT-4o, Mixtral, DBRX]
refs: ['https://www.databricks.com/blog/long-context-rag-performance-llms']
---
# Long-context RAG failures are model-specific and qualitatively different, not just lower accuracy

Databricks measured RAG accuracy against retrieved-context length and found each model breaks in its own characteristic way, at its own threshold. Saturation points: GPT-4o and Claude 3.5 Sonnet held to ~125k with little deterioration; GPT-4-0125-preview declined past 64k; Llama-3.1-405b past 32k; GPT-4-Turbo and Claude 3 Sonnet past 16k; DBRX-Instruct past 8k; Mixtral-8x7b-Instruct past 4k.

The important part is the failure taxonomy, because these do not look like degraded accuracy in your metrics:
- Copyright refusal — Claude 3 Sonnet increasingly declined to answer at all: 3.7% of cases at 16k, 21% at 32k, 49.5% at 64k.
- Instruction non-compliance — DBRX summarised the context rather than answering the question: 5.2% at 8k, 17.6% at 16k, 50.4% at 32k.
- Repeated content — Mixtral emitted degenerate repetition.
- Random or irrelevant content, and plain wrong answers (GPT-4, Llama-3.1-405b).

Note the shape of both quantified curves: each roughly TRIPLES per doubling of context and passes 50% within two doublings of onset. A failure mode sitting at 4-5% in your longest tested configuration is not a tolerable background rate — on this evidence it is the visible start of a steep curve, so test one doubling beyond your intended maximum before setting a context budget.

Consequence for evaluation: an accuracy-only score conflates "refused", "summarised instead", and "answered wrongly", which have completely different fixes. Classify failures by type before tuning chunk counts. Also note retrieval recall itself saturates at very different points by corpus — 8k on Natural Questions but 128k on HotPotQA and FinanceBench — so there is no portable "right" number of chunks.

STALENESS: published 2024-08-12, covering 13 models current as of mid-2024. Re-verified 2026-08-09: still live, still NO update notice and no newer-models addendum, and every saturation point and failure percentage matches verbatim. Every named threshold is therefore a point-in-time measurement several model generations old and should not be quoted as current — do not conclude anything about a 2026 model's behaviour from the GPT-4o row. The durable contributions are the failure taxonomy, the steepness of the curves, and the finding that the corpus, not just the model, sets where retrieval recall saturates. Confidence 0.7 -> 0.75 on a clean second verification; it stays below 0.8 because the numbers are model-bound by construction.
