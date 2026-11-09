---
type: reference
domain: [agentic-engineering, tools, api, reliability, architecture, state-management]
confidence: 0.9
sources: 1
entities: [OpenAI, Responses API, async tool calling, call_id, task_handle, wait_for_tasks, previous_response_id, GPT-6 Astra, Background mode]
motifs: [identifier-not-position, handle-lifetime-exceeds-request]
refs: ['https://developers.openai.com/api/docs/guides/async-tool-calling']
---
# Async tool results are matched by call_id, not by position: handles must stay unique for the whole conversation including finished tasks, and a wait tool's status must be returned AFTER the results it waited on

Async tool calling lets the model "continue working after it calls a tool, without waiting for that tool's result", enabled per tool with `async: true`. What moves is the model's turn, not the work: "Your application still executes the tool", and "Async tools don't move execution to OpenAI or manage your background jobs." Ordinary synchronous calls keep their old contract — they "must finish before the model resumes".

THE THREE RULES THAT ARE EASY TO GET WRONG, all of them stated as requirements and all compound.

First, correlation is by identifier: "Use the original API call_id to match the result to its call", pairing `function_call` with `function_call_output` and `custom_tool_call` with `custom_tool_call_output`. Calls "can arrive together or across responses", so position carries no information. On a continuation, "Set previous_response_id to the latest response ID, and include the tools and instructions in the continuation request" — the response id advances while the call_id does not.

Second, handle uniqueness is conversation-scoped, not request-scoped: "Keep handles unique throughout the conversation, including completed tasks and repeated lookup requests", and "Keep the registry for the entire conversation to prevent reuse of a completed task's handle." A registry cleared when a job finishes reintroduces exactly the collision the rule forbids.

Third, when a wait tool is used, ordering inside one input array matters: "Return each newly completed result on its original call_id, then return status on the wait call's own call_id", because "This order gives the model the results when it resumes." The wait tool itself is an ordinary synchronous function — "omit async or set it to false" — and is not a built-in.

THE HUMAN-INPUT CASE has its own trap: "Don't complete the tool call with an acknowledgment that you displayed the question; its result is the user's answer." Async execution "doesn't keep a response open until the user replies", so a dismissed or timed-out question needs "an explicit no-answer result so the model can decide how to proceed" rather than silence.

SCOPE LIMITS, stated. "Async execution applies to function and custom tools that your application runs" and "doesn't apply to hosted built-in tools". "Use direct tool calls; don't configure async tools for programmatic tool calling." "In Multi-agent mode, don't combine async tools with parallel tool calls." Supported by "GPT-6 Astra and later models". This is a different mechanism from Background mode, "which runs response generation asynchronously".

NOT STATED, and each of these is a failure the caller must design for anyway: no timeout or maximum duration for a pending job or question, no cap on concurrent calls or handles, no defined behaviour if a result is never returned, no error named for a wrong call_id or a duplicate handle, and no completion-order guarantee beyond "together or across responses".
