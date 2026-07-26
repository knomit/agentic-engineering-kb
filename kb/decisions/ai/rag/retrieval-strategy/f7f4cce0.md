---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, rag, architecture]
confidence: 0.75
sources: 3
entities: [GraphRAG, Microsoft Research, Databricks, RAG]
refs: ['https://arxiv.org/abs/2404.16130', 'https://arxiv.org/abs/2005.11401', 'https://www.databricks.com/blog/long-context-rag-performance-llms']
---
# Baseline RAG vs GraphRAG vs long-context stuffing: choose by question shape, not corpus size

Three approaches to grounding, and the deciding variable is what kind of question the user asks — not how big the corpus is.

Baseline vector RAG (Lewis et al., 2020) retrieves the top-k chunks most similar to the query. It works when the answer LIVES in a small number of locatable passages. Its structural failure, stated plainly by the GraphRAG authors, is global questions — "what are the main themes in this dataset?" There is no chunk to retrieve, because the answer is a property of the whole corpus, so top-k similarity returns arbitrary passages and the model confabulates a summary from them.

GraphRAG targets exactly that gap: query-focused summarization / global sensemaking over ~1M-token corpora. It builds an LLM-derived entity knowledge graph, precomputes summaries for detected communities of related entities, then at query time map-reduces partial answers from each community summary into a final answer. Reported gains are in answer comprehensiveness and diversity over a conventional RAG baseline. The cost is a heavy LLM-driven indexing pass over the whole corpus before any query — pay it only if global questions are a real part of your traffic, and re-pay it as the corpus changes.

Long-context stuffing — skip retrieval, pass everything — is the tempting third option and it saturates: measured per-model degradation begins between 4k and 125k tokens depending on the model, cost scales linearly with context, and coherent long contexts measurably underperform.

Decision: local/extractive questions → baseline RAG with hybrid keyword+vector. Global/thematic questions → graph or hierarchical summarization; baseline RAG will not get there with more chunks. Never → stuffing as a substitute for retrieval, whatever the advertised window.
