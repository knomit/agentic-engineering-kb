---
type: pattern
domain: [agentic-engineering, context-engineering, architecture, multi-agent, operations]
confidence: 0.8
sources: 1
entities: [LangChain, Content Studio, Managed Deep Agents, AGENTS.md, learn_from_job, skills, progressive disclosure, agent memory]
motifs: [unbounded-self-accumulation, candidate-needs-promotion-gate]
refs: ['https://www.langchain.com/blog/design-agent', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/coding-agents/instruction-files/eca14d07.md']
---
# A self-writing agent memory needs both a promotion gate and a hard size cap — Content Studio caps each AGENTS.md index at 200 lines after an early version grew to 500K tokens

LangChain's internal design agent writes its own memory, in two file layers (a team layer and a per-user layer), and the account names both controls that keep it usable.

Admission runs as two loops. The fast loop saves a rule in the same turn the user states it. The slow loop runs after a job: "After each job, our `learn_from_job` tool launches a lightweight subagent that captures up to five" evidence-backed lessons, each linked to a specific skill; later jobs rate those lessons, and a weekly background agent promotes the ones that proved useful. So a lesson is a candidate on write and only becomes memory by earning it in subsequent use.

Size is capped separately: "We now limit these files to a 200-line index after an early version grew to 500K tokens." The capped file is an INDEX — the content sits behind links, and the same system links its wiki from skills rather than duplicating it, so a rule such as a font rule is changed in one place.

The pattern is that these two controls do not substitute for each other. A promotion gate with no cap still grows the always-loaded layer forever, because every promoted lesson is permanent. A cap with no gate discards lessons by recency or truncation rather than by value. Both are needed because the admitted layer is injected into the system prompt on every call, so its size is a tax on every request while its contents are what the agent is for.

Two things not to compress away. The 200-line limit is on the always-loaded index, not on total memory, which lives behind it unbounded. And "up to five" lessons is a per-job admission limit on CANDIDATES — the rating-and-promotion step is what decides whether any of them survive.
