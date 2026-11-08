---
type: reference
domain: [agentic-engineering, context-engineering, api, reliability, cost, state-management]
confidence: 0.85
sources: 2
entities: [OpenAI, Responses API, context_management, compact_threshold, /responses/compact, previous_response_id, compaction item, store=false, ZDR, Codex, auto_compact_limit, encrypted_content]
motifs: [mode-dependent-safety, remedy-needs-headroom]
refs: ['https://developers.openai.com/api/docs/guides/compaction', 'https://openai.com/index/unrolling-the-codex-agent-loop/', 'kb://bc6eac5f37df/kb/invariants/ai/agents/context-engineering/compaction/714a540c.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/runtime/state/statelessness/92df8660.md']
---
# OpenAI compaction returns an opaque encrypted item, and whether you may prune around it INVERTS with the chaining mode — prune before it on stateless input-array chaining, never prune with previous_response_id, never prune the standalone endpoint's output

Two compaction surfaces on the OpenAI Responses API, with one shared artefact and three different pruning rules.

**Server-side, automatic.** Send `context_management` carrying a `compact_threshold` on a Responses create request — the documented example is `{"type": "compaction", "compact_threshold": 200000}`. The server runs compaction when the RENDERED token count crosses that threshold and prunes the context before inference continues; there is no separate call to make. The response stream then contains an encrypted compaction item, which the documentation describes as carrying forward key prior state and reasoning into the next run using fewer tokens, and which is opaque to you.

**Standalone, explicit.** `POST /responses/compact` is the stateless version: you send the full context window — messages, tools and other items — and it returns a compacted window to pass to your next `/responses` call. Its output generally contains the compaction item plus some retained items from the previous window.

THE PRUNING RULE IS NOT ONE RULE, AND THE CORRECT ACTION IN ONE MODE IS THE WRONG ONE IN ANOTHER. With stateless input-array chaining you MAY drop the items that came before the most recent compaction item, and the documentation offers that as a latency improvement. When you chain with `previous_response_id`, you must NOT prune manually. And the standalone endpoint's returned window must not be pruned at all — pass it on as-is. So "compaction means you can drop the old items" is true in exactly one of the three cases.

THE LIMIT THAT DECIDES WHEN YOU CALL IT: the window you send to `/responses/compact` must itself still fit within the model's context window. Compaction is therefore not a recovery path for a context that has already overflowed — it is an operation you have to perform while you still fit, which is why the automatic surface is threshold-driven rather than error-driven. An agent loop that waits for a context-length error before compacting has waited too long.

Both surfaces are described as ZDR-friendly — the server-side one when `store=false`, the standalone one as fully stateless.

WHAT IS NOT ESTABLISHED. The page does not state whether individual tool calls or reasoning items survive compaction as items; it says only that the compaction item carries key prior state and reasoning forward, and that the standalone output can include retained items. So do not build anything that depends on a specific earlier tool call still being addressable afterwards. This is the mechanics of one vendor's compaction, not a general model: Anthropic's compaction behaviour is recorded separately ([[714a540c]]), and the two differ in what the caller is responsible for.

A SHIPPING CLIENT OF THE STATELESS-CHAINING MODE, which fixes which column of the table above applies in practice. OpenAI's Codex deliberately does not pass `previous_response_id`, in order to "keep requests fully stateless and to support Zero Data Retention (ZDR) configurations", and carries reasoning forward as `encrypted_content` instead. So a harness that wants ZDR is in the stateless input-array column by construction, not by preference, and inherits that column's pruning rule rather than being able to choose between them.

Its trigger is client-side and must not be conflated with the API parameter. Codex "automatically uses this endpoint to compact the conversation when the auto_compact_limit is exceeded" — `auto_compact_limit` is the client's own configured threshold for deciding when to call, a different thing from the request-level `compact_threshold` the API exposes. Codex's published account gives no numeric value for it, so no default should be assumed. Its earlier approach was a manual `/compact` that summarised the conversation client-side and replaced the input with the summary; the move to the endpoint is what introduced the opaque compaction item into its loop.
