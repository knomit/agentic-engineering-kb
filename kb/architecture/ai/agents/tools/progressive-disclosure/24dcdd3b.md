---
type: pattern
domain: [agentic-engineering, tools, architecture, context-engineering, coding-agents]
confidence: 0.8
sources: 1
entities: [Anthropic, Claude Code, Claude Code Guide, subagent, progressive disclosure, tool selection, context rot, system prompt]
motifs: [digest-return-bounds-context]
refs: ['https://claude.dev/blog/seeing-like-an-agent/', 'kb://bc6eac5f37df/kb/principles/ai/agents/tools/00d3ef19.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/tools/mcp/62c9a78b.md']
---
# Reference knowledge the agent needs rarely belongs behind a subagent that returns only the ANSWER — Claude Code's team rejected both the system prompt and a docs link, and names why each failed

Claude Code ships about 20 tools, and its team states the rule that holds the number there: "The bar to add a new tool is high, because this gives the model one more option to think about." A tool's cost is paid on every turn in selection, not when it runs.

The worked case is reference knowledge the agent needs only occasionally — here, the documentation for Claude Code itself. Two obvious answers were tried and rejected, and the reasons are the transferable part:

- **Put the documentation in the system prompt.** Rejected because users rarely ask, so the tokens pay rent in every context: it causes context rot and interferes with the main job of writing code.
- **Give the agent a link to the docs.** Rejected because the agent pulled large chunks of documentation into context to answer questions that needed one sentence. A reference the agent can reach is not bounded by the size of the answer.

What shipped is a Claude Code Guide subagent, invoked for questions about Claude Code, which searches the docs in ITS OWN context, follows detailed search instructions, and returns only the answer. The load-bearing property is the answer-only return, not the delegation: a subagent that handed back the retrieved documents would reproduce the second failure exactly. The parent's context receives a sentence; the subagent's context absorbs the retrieval and is then discarded.

The team reports a residual failure the pattern does not fix: the agent can still get confused when asked how to set ITSELF up, where the question is about the running configuration rather than about the documentation.

What this does NOT mean: it is not a claim that a subagent is cheaper than a tool or than context. A subagent costs a model call and its own prefix. The comparison that favoured it here was against documentation resident in every context for a question asked rarely — invert the frequency and resident context wins.
