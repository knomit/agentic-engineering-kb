---
type: process
domain: [agentic-engineering, rag, evaluation, context-engineering, benchmarks]
confidence: 0.7
sources: 1
entities: [Chroma, Brandon Smith, Anton Troynikov, MTEB, BEIR, RecursiveCharacterTextSplitter, ClusterSemanticChunker, LLMSemanticChunker, Precision-Omega, IoU, chunking]
motifs: [benchmark-blind-to-variable, recall-without-efficiency-misleads]
refs: ['https://www.trychroma.com/research/evaluating-chunking', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/context-engineering/052c2b66.md', 'kb://bc6eac5f37df/kb/gotchas/ai/rag/contextual-retrieval/d032790e.md']
---
# Document-level IR benchmarks cannot measure a chunking strategy at all — scoring retrieval at the token level, with an efficiency metric alongside recall, is what makes chunk size and overlap comparable

Chroma's chunking study (2024-07-03, Brandon Smith and Anton Troynikov) starts from a measurement gap: the standard retrieval benchmarks are "aimed at whole-document retrieval tasks." so they score whether the right document came back and are structurally blind to how that document was split. If you are tuning chunk size, overlap, or a semantic splitter against MTEB- or BEIR-style numbers, you are not measuring the thing you changed.

The instrument they use instead scores retrieval at the TOKEN level against LLM-generated queries paired with the exact excerpts that answer them, across five corpora (government speech, Wikipedia, chatbot logs, financial reports, biomedical papers), with no LLM judge in the loop. Four metrics, and the last two are the ones a recall-only setup is missing: recall (share of relevant tokens retrieved); precision (share of retrieved tokens that are relevant); Precision-Omega, computed as if every chunk containing relevant tokens were retrieved, which "gives an upper bound on token efficiency given perfect recall."; and token-level IoU, "as this metric penalizes redundant information."

Why the efficiency side matters operationally: a strategy can win on recall purely by returning more text, and in an agent that text is context you pay for and that crowds the window. The study's own comparison shows this — a large-chunk, heavy-overlap configuration scored below average on recall AND poorly on the efficiency metrics, while recursive character splitting at small chunk sizes with no overlap performed consistently well. Overlap bought recall for the weaker embedding model but cost IoU, because overlap is by construction redundant tokens. Two new splitters were introduced: a cluster-based one that groups small pieces by embedding similarity under a length cap, which led on precision and IoU at smaller chunk sizes, and an LLM-chosen-split-point one, which led on recall.

The claim to carry away is the method, not a winning splitter. The authors call the work preliminary and state these limits: the dataset is small and narrow with a uniform LLM-generated query style; excerpt filtering may bias the sample and relevant text the generator never produced is never counted; runtime and cost were NOT evaluated, though the LLM splitter is flagged as potentially slow and the cluster method must recompute chunks as data changes; the LLM splitter was tested with only two models. Logit-based, attention-based and ContextCite-inspired splitting were tried and yielded no usable signal. Chroma sells retrieval infrastructure and two of the compared strategies are its own, so the ranking is a vendor's; the measurement framework is the transferable part, and the code was released.

The strategy results are also tied to 2024-era embedding models and splitter defaults — re-measure on your own embedding model rather than inheriting a ranking.
