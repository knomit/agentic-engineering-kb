---
type: reference
domain: [agentic-engineering, context-engineering, api, reliability, cost, state-management]
confidence: 0.85
sources: 1
entities: [OpenAI, Responses API, context_management, compact_threshold, /responses/compact, previous_response_id, compaction item, store=false, ZDR]
motifs: [mode-dependent-safety, remedy-needs-headroom]
refs: ['https://developers.openai.com/api/docs/guides/compaction', 'kb://bc6eac5f37df/kb/invariants/ai/agents/context-engineering/compaction/714a540c.md']
---
# OpenAI compaction returns an opaque encrypted item, and whether you may prune around it INVERTS with the chaining mode — prune before it on stateless input-array chaining, never prune with previous_response_id, never prune the standalone endpoint's output

Two compaction surfaces on the OpenAI Responses API, with one shared artefact and three different pruning rules.

**Server-side, automatic.** Send `context_management` carrying a `compact_threshold` on a Responses create request — the documented example is `{"type": "compaction", "compact_threshold": 200000}`. The server runs compaction when the RENDERED token count crosses that threshold and prunes the context before inference continues; there is no separate call to make. The response stream then contains an encrypted compaction item, which the documentation describes as carrying forward key prior state and reasoning into the next run using fewer tokens, and which is opaque to you.

**Standalone, explicit.** `POST /responses/compact` is the stateless version: you send the full context window — messages, tools and other items — and it returns a compacted window to pass to your next `/responses` call. Its output generally contains the compaction item plus some retained items from the previous window.

THE PRUNING RULE IS NOT ONE RULE, AND THE CORRECT ACTION IN ONE MODE IS THE WRONG ONE IN ANOTHER. With stateless input-array chaining you MAY drop the items that came before the most recent compaction item, and the documentation offers that as a latency improvement. When you chain with `previous_response_id`, you must NOT prune manually. And the standalone endpoint's returned window must not be pruned at all — pass it on as-is. So "compaction means you can drop the old items" is true in exactly one of the three cases.

THE LIMIT THAT DECIDES WHEN YOU CALL IT: the window you send to `/responses/compact` must itself still fit within the model's context window. Compaction is therefore not a recovery path for a context that has already overflowed — it is an operation you have to perform while you still fit, which is why the automatic surface is threshold-driven rather than error-driven. An agent loop that waits for a context-length error before compacting has waited too long.

Both surfaces are described as ZDR-friendly — the server-side one when `store=false`, the standalone one as fully stateless.

WHAT IS NOT ESTABLISHED. The page does not state whether individual tool calls or reasoning items survive compaction as items; it says only that the compaction item carries key prior state and reasoning forward, and that the standalone output can include retained items. So do not build anything that depends on a specific earlier tool call still being addressable afterwards. This is the mechanics of one vendor's compaction, not a general model: Anthropic's compaction behaviour is recorded separately ([[714a540c]]), and the two differ in what the caller is responsible for.
