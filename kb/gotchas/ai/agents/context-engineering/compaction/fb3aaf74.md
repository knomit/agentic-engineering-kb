---
type: observation
domain: [agentic-engineering, context-engineering, coding-agents, cost, operations]
confidence: 0.9
sources: 1
entities: [Anthropic, Claude Code, prompt caching, compaction, cache lifetime, context window, subagent]
motifs: [idle-state-rewritten-silently]
refs: ['https://code.claude.com/docs/en/best-practices', 'kb://bc6eac5f37df/kb/decisions/ai/agents/context-engineering/compaction/468c75d4.md', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/cost/prompt-caching/dd1a3738.md']
---
# An idle session past about 200K tokens is compacted on its own shortly before the one-hour prompt cache expires, so you can return to a summary you never asked for — and the behaviour is stated only for the one-hour cache tier

Claude Code's best-practices page states it in one sentence: "On the one-hour cache, a session past about 200K tokens that sits idle is compacted shortly before the cache expires, so after lunch you continue from a summary."

THREE CONDITIONS, ALL OF THEM LOAD-BEARING. The one-hour cache tier; a context past about 200K tokens; and the session sitting IDLE. Drop any one of the three and the sentence stops describing your session. The one-hour tier in particular is not universal: the same page gives the lifetime as "about an hour on a subscription and five minutes on an API key, cloud provider, or usage credits", so a session billed through an API key, a cloud provider or usage credits has no one-hour window for this to fire inside, and "Subagents get five minutes unless you change it."

The consequence is about what you find when you come back, not about the bill. A long session you walked away from may resume from a summary rather than from the turns you left in it, and the compaction is initiated by the harness while nobody is interacting, so there is no turn boundary at which it could have been declined. Anything you were relying on being present verbatim — an exact error string, a directory listing, a half-written plan, the output of a command you did not save — should be written to a file before the break rather than left in the conversation.

What this does NOT mean: it is not a statement that compaction is undesirable or should be avoided. The same vendor's cost guidance treats compaction as an investment that pays back over subsequent turns, which is why compacting deliberately before a break is the recommended move; this fact is about the case where the harness does it for you while you are not there to know.
