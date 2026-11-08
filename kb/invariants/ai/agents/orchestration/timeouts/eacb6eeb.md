---
type: reference
domain: [agentic-engineering, orchestration, reliability, operations, architecture]
confidence: 0.85
sources: 1
entities: [OpenAI, Symphony, Codex, agent.max_concurrent_agents, agent.max_turns, codex.turn_timeout_ms, codex.stall_timeout_ms, Linear]
motifs: [defaults-encode-failure-budget]
refs: ['https://openai.com/index/open-source-codex-orchestration-symphony/']
---
# Symphony's published defaults are the numbers an unattended agent orchestrator actually needs: 10 concurrent agents, 20 turns, a 1-hour turn timeout and a 5-minute stall timeout that zero disables

The spec publishes its defaults, which is unusual and makes them a reference point for anyone sizing their own agent scheduler. Verbatim where quoted:

- `agent.max_concurrent_agents`: integer, default `10`
- `agent.max_turns`: integer, default `20`
- `codex.turn_timeout_ms`: integer, default `3600000` — one hour per turn
- `codex.stall_timeout_ms`: integer, default `300000` — five minutes; "If `<= 0`, stall detection is disabled."
- Poll interval 30000 ms; read timeout 5000 ms; hook timeout 60000 ms; network timeout 30000 ms
- Max retry backoff 300000 ms, with failure retry on exponential backoff starting at 10000 ms and capped there; continuation retry after a clean exit about 1000 ms
- Linear page size 50; max stdout line size 10 MB, recommended

Two things to read off this rather than copy blindly. The concurrency default (10) sits above the three-to-five sessions a human can drive, which is the point of the architecture — it is sized for review-at-the-end, not for supervision. And the gap between the turn timeout (1 hour) and the stall timeout (5 minutes) is the real design decision: a long ceiling on legitimate work, with a much shorter detector for work that has stopped producing output. Setting the stall timeout to zero does not mean "no limit soon", it disables stall detection entirely and leaves the hour as your only backstop.

The run phases a watchdog has to distinguish, as named: PreparingWorkspace, BuildingPrompt, LaunchingAgentProcess, InitializingSession, StreamingTurn, Finishing, terminating in Succeeded, Failed, TimedOut, Stalled or CanceledByReconciliation. Default tracker states are also given — active: `Todo`, `In Progress`; terminal: `Closed`, `Cancelled`, `Canceled`, `Duplicate`, `Done` — and note that the terminal list carries both spellings of cancelled, which is the kind of detail a hand-rolled state mapping gets wrong.
