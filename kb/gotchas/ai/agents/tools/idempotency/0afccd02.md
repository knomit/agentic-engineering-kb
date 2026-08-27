---
type: observation
domain: [agentic-engineering, tools, reliability, error-handling, distributed-systems]
confidence: 0.8
sources: 1
entities: [Amazon, AWS Builders' Library, idempotency, semantic equivalence, principle of least astonishment, Amazon EC2]
motifs: [implementation-shaped-interface]
refs: ['https://builder.aws.com/content/3Ev0BENTyBr0XxzRk5FDZzgNYos/making-retries-safe-with-idempotent-apis']
---
# Returning AlreadyExists to a retried tool call is a side effect from the caller's point of view — return a semantically equivalent response instead

A subtle distinction from Amazon's Builders' Library that decides whether idempotency actually buys you anything.

When a retried request arrives bearing a token the service has already seen, the minimal correct behaviour is to not create a second resource — for example, return `ResourceAlreadyExists`. That technically satisfies idempotency: no side effect occurred server-side. Amazon argues it is still the wrong answer. From the CALLER's perspective the response changed, and a changed response changes the caller's flow of execution. The caller now has to handle 'already exists' in a situation where, as far as it knows, the resource did not exist when it made the call. So there IS a side effect — it just landed on the client. This is precisely what stops retry-by-default from being safe to bake into an SDK.

The alternative Amazon implements: return a SEMANTICALLY EQUIVALENT response to every request bearing the same token, for some retention interval. Not byte-identical — their RunInstances example shows the state field legitimately progressing from `pending` to `running` between the original call and the retry — but the same KIND of response, so the caller can process it identically and never needs to know a retry occurred.

For agents this is the difference between an invisible retry and a derailed trajectory. A model that issues a tool call, gets a timeout, retries, and receives `AlreadyExists` will not treat that as a successful retry. It typically concludes either that it made an error, or that some other actor created the resource, and it will go and investigate, apologise to the user, or attempt a cleanup — spending turns and sometimes doing real damage. Handing back the same successful result it would have received the first time keeps the trajectory on rails. This is a specific instance of the general rule that a tool result is a prompt: `AlreadyExists` reads to the model as 'something is wrong', because in a non-retry context it usually is.

They also apply the principle of least astonishment to the awkward late-arrival case — a retry that arrives after some other actor deleted the resource still gets the semantically equivalent response (their example returns the instance in `terminated` state rather than erroring), because a consistent contract beats a technically-accurate surprise.
