---
type: reference
domain: [agentic-engineering, error-handling, reliability, api, observability]
confidence: 0.85
sources: 1
entities: [OpenAI, Agents API, error.code, error.param, server_overloaded, server_is_overloaded, sandbox_error, executor_version_incompatible, idle_timeout, requires_action, context_length_exceeded]
motifs: [identifier-collision, layered-failure-conflated]
refs: ['https://developers.openai.com/api/docs/guides/agents-api/errors']
---
# OpenAI's Agents API reports failure at three independent layers and reuses code strings across them — server_overloaded is a turn code while server_is_overloaded is the HTTP one, and a failed turn does not imply a failed session

A failure in OpenAI's Agents API surfaces at one of three layers, and which layer it is decides what recovery is even available.

THE THREE LAYERS. An HTTP request failure carries a status plus an `error` object. A turn failure arrives as `agent.session.turn.failed`, and the turn then has `status: "failed"` with its own `error.code` and `error.message`. A session failure arrives as `agent.session.failed`; an environment failure as `agent.session.environment.failed`, read from `environment.error`. The documented rule that ties them together is that a failed turn does not necessarily fail the session — after one you retrieve the session to decide whether it can continue or must be replaced, and if its `status` is `requires_action` you handle the required actions before anything else.

THE NAMESPACE COLLIDES IN BOTH DIRECTIONS. Turn codes are not HTTP statuses, and the strings are not aligned with them: overload is `server_overloaded` as a turn code and `server_is_overloaded` as the HTTP one. In the other direction the same string spans layers with different remedies: `executor_version_incompatible` appears as an HTTP 409, as a turn code and as a session code; `sandbox_error` appears as both a turn code and an environment code; `internal_error` appears at all three. So a handler keyed on the string alone, without knowing which layer delivered it, can take the wrong recovery for the right condition.

MATCH ON THE CODE, NOT THE PROSE. The guide states it for the Files API limit — "Check `error.code` to identify this condition instead of matching the message text" — and the structure generalises: branch on `error.code`, use `error.message` only for explanation and `error.param` to name the invalid field, and handle both unknown codes and an absent `param`.

RECOVERY IS OUTCOME-FIRST, NOT RETRY-FIRST. Before retrying anything the guide has you establish what actually happened, because "An `error` event or a disconnected stream doesn't confirm the turn's final state." Retrieve the session, the turn and the saved items; if the turn is still active keep following it, and if it completed use its result. Then check completed actions, because a failed turn may already have written files or called external tools. Only then wait and retry, honouring `Retry-After` and setting an attempt limit or deadline, and "Stop automatic retries if the error changes or the retry limit is reached." A follow-up to a session waits until it is `idle` and asks only for the unfinished work.

A LIMIT THAT IS NOT PER REQUEST. Session creation and file attachment can return a 429 for a per-user Files API limit, and each attached file may need its own check, so one request can consume several; "Immediate retries can continue to exhaust the allowance." This one is synchronous, unlike the asynchronous session and turn failures, and backing off rather than retrying promptly is the documented response.

WHAT THE PAGE DOES NOT GIVE. No idempotency rules — confirming completed effects by hand is the stated substitute. No numeric timeouts, retry counts or backoff values; `idle_timeout` is described only as inactivity-based. Do not read a retry policy off this page: it defers those numbers to separate rate-limit guidance.

SCOPE. One vendor's documented contract for its own agent API, read as a reference rather than measured; the condition names are what the service emits, not a portable taxonomy.
