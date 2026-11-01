---
type: observation
domain: [agentic-engineering, data-agents, reliability, evaluation, operations]
confidence: 0.8
sources: 1
entities: [OpenAI, data agent, many-to-many joins, filter pushdown, nulls, zero-row result, text-to-SQL]
motifs: [silent-invalid-result]
refs: ['https://openai.com/index/inside-our-in-house-data-agent/']
---
# A data agent's dangerous failures return a plausible number with no error — many-to-many joins, filter pushdown errors and unhandled nulls are the named classes

OpenAI names the failure classes for its internal analytics agent explicitly: "Common failure modes—many-to-many joins, filter pushdown errors, and unhandled nulls—can silently invalidate results." The operative word is silently. None of the three raises an error; each returns a well-formed table of numbers that is wrong, which is the shape of failure that survives review.

Two further classes the post reports in the same register: similar-looking tables are hard to tell apart, so the agent can answer a correct question against the wrong source; and missing context produces badly wrong user counts or misreads internal terminology.

The mitigations reported are about making wrongness visible rather than preventing it. The agent detects problems such as zero-row results from bad joins or filters, then investigates and retries. It asks clarifying questions and falls back to a stated default when none is given, such as the last 7 or 30 days. And it surfaces its assumptions and links to the underlying results so the person reading an answer can check what produced it.

The consequence for anyone building one: the checks have to be on the shape of the result — row counts, join cardinality, null handling, the source table's identity — because the query parses, the agent reports success, and nothing in the loop objects. A zero-row result is the easy case precisely because it is the one wrong answer that announces itself.
