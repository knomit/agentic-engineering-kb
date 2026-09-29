---
type: observation
domain: [agentic-engineering, rag, context-engineering, evaluation]
confidence: 0.75
sources: 1
entities: [Databricks, Claude 3.5 Sonnet, GPT-4o, Mixtral, DBRX]
motifs: [scalar-hides-failure-mode]
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

Consequence for evaluation: an accuracy-only score conflates "refused", "summarised instead", and "answered wrongly", which have completely different fixes. Classify failures by type before tuning chunk counts. Also note retrieval recall itself saturates at very different points by corpus — the NQ dataset "saturates early at 8k context length", while "DocsQA, HotpotQA and FinanceBench datasets saturate at 96k and 128k context length". That is more than an order of magnitude between corpora on the same models, so there is no portable "right" number of chunks and the figure has to be measured on your own corpus.

SCOPE, which decides what may be quoted from this. The study was published 2024-08-12 and covers 13 models current as of mid-2024, and it carries no update notice and no newer-models addendum. Every named threshold is therefore a point-in-time measurement several model generations old and must not be quoted as current — in particular, conclude nothing about a 2026 model's behaviour from the GPT-4o row.

What survives the model turnover is the shape rather than the numbers: the failure taxonomy, the steepness of the two quantified curves, and the finding that the corpus and not only the model sets where retrieval recall saturates. The confidence on this fact sits below 0.8 because the figures are model-bound by construction, not because the measurement is in doubt.
