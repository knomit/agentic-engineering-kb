---
type: principle
domain: [agentic-engineering, reliability, tools, error-handling, distributed-systems]
confidence: 0.85
sources: 1
entities: [Amazon, AWS Builders' Library, idempotency, UNKNOWN, request/reply, Jacob Gabrielson]
refs: ['https://builder.aws.com/content/3F08f7GPFiZMCgXD8gny6OjxR0Z/challenges-with-distributed-systems']
---
# A tool call has five outcomes, not two — and UNKNOWN (timeout) is the one that corrupts state

Amazon's Builders' Library enumerates the outcomes of any request/reply over a network as POST_FAILED, RETRYABLE, FATAL, UNKNOWN, and SUCCESS. Agent harnesses almost universally collapse this to success/failure, and the collapsed case is the dangerous one.

The distinction that matters: POST_FAILED means the caller knows deterministically that the request never reached the server — it is always safe to retry. UNKNOWN means the request timed out, and the caller knows nothing: it may have succeeded, may have failed, or may have been received and processed but the reply lost. These are not the same and must not share a code path.

Why this bites agents specifically: a tool that times out has, from the model's point of view, simply 'failed'. If the tool had a side effect — a payment, a file write, a ticket creation, an email — the side effect may already have happened. An agent loop that retries on timeout will double-execute it, and unlike a human operator the agent has no instinct that says 'check whether it went through first'. The compounding-error property of agent loops makes this worse: the agent will keep going and build subsequent reasoning on a state it has misread.

What to do: give every side-effecting tool an idempotency key supplied by the caller, so a retry after UNKNOWN is safe by construction. Where that is impossible, return the timeout to the model as an explicitly UNKNOWN result — say in the tool result that the operation may have completed and that the next step is to query for its effect, not to repeat it. Surfacing 'timed out, state unknown, verify before retrying' is a different prompt to the model than 'error'.

This is not a rare edge case. The article's point is that the eight steps of a round trip can each fail independently, and the client and server do not share fate — so UNKNOWN is a permanent, irreducible feature of any tool that crosses a network, which today is nearly all of them.
