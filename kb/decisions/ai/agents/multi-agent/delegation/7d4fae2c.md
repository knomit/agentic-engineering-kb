---
kind: pragmatic
type: heuristic
domain: [agentic-engineering, multi-agent, cost, coding-agents, architecture]
confidence: 0.9
sources: 1
entities: [Anthropic, Claude Code, subagent, Haiku, /usage, model selection]
motifs: [cost-without-capability-gain]
refs: ['https://code.claude.com/docs/en/best-practices', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/multi-agent/delegation/773a89ee.md', 'kb://bc6eac5f37df/kb/decisions/ai/agents/multi-agent/context-isolation/e06d35eb.md']
---
# A subagent buys parallelism or an independent reader, never a better answer on the same task — by default it runs the same model, bills against the same usage, and can be slower because it must re-gather context the parent already had

Claude Code's best-practices page prices subagents from the operator's side. "What they cost you is mostly tokens, since every subagent sends its own requests" "and they count against the same usage as your main conversation." "Sometimes it's time as well: a fresh subagent first has to gather context your conversation already had" "so it can end up *slower* than doing the task where you are." "And by default it's the same model (or a smaller one) on the same task." The conclusion it draws from those three: "You get parallelism or a fresh pair of eyes out of it, but not a smarter answer."

So the decision rule keys on the SHAPE of the work, not on its difficulty. Delegate when the work genuinely runs in parallel, or when the value is precisely that the reader has not seen your conversation. Do not delegate a hard single-threaded task in the hope of a better result: it is the same model, with less context than you have, and you pay for the re-gathering in both tokens and wall clock. The harder the task, the worse that trade, because the context the subagent lacks is the context the task needed.

TWO LEVERS THE SAME SECTION NAMES. "Set `model: haiku` in a subagent's definition if its work is simple", because "That kind of job doesn't need the bigger model, and Haiku costs a lot less per request" — the page gives no multiple and no token figure, only that qualitative comparison, so do not quote a ratio from it. And "Check `/usage` to see what share of your usage each subagent type takes, so you can tell which ones are earning their cost", which turns per-subagent-type spend into an observable rather than a guess.

What this does NOT mean: not that a second agent never improves correctness. The fresh-reader case is real and rests on different grounds — a model is a poor verifier of its own output inside the same context, which is an independence argument rather than a capability argument. The claim being retired is specifically that handing the SAME task to a subagent produces a better ANSWER.

And the pressure runs the other way by default: current Claude models delegate to subagents more readily than earlier ones and do so without being asked, so over-delegation is the behaviour you get for free rather than something an operator has to choose.
