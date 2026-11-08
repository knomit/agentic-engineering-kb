---
type: observation
domain: [agentic-engineering, coding-agents, context-engineering, state-management, operations, reliability]
confidence: 0.7
sources: 1
entities: [OpenAI, Codex, GPT-5.3-Codex, long-horizon agents, milestone, git worktree, documentation.md, plan.md, METR]
motifs: [external-file-carries-state, milestone-bounds-repair-cost]
refs: ['https://developers.openai.com/blog/run-long-horizon-tasks-with-codex', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/coding-agents/state-files/15e7bf02.md', 'kb://bc6eac5f37df/kb/conventions/ai/agents/coding-agents/verification/519ec939.md']
---
# A single uninterrupted agent run of about 25 hours, 13M tokens and 30k lines of code was structured by four things outside the context window: spec, plan, constraints and status in files, milestones sized to one loop, and a stop-and-fix validation gate

A published practitioner account reports the scale plainly: "Codex ran for about 25 hours uninterrupted, used about 13M tokens, and generated about 30k lines of code." The configuration was "GPT-5.3-Codex at “Extra High” reasoning".

WHAT CARRIED THE RUN WAS NOT IN THE CONVERSATION. "I wrote the spec, plan, constraints, and status in markdown files that Codex could revisit repeatedly." The status file records current milestone status — what is done, what is next — plus decisions and known issues, and the author's stated payoff is a human one: it is how he could step away for hours and still understand what happened. Two rules in the plan file did the rest of the work: "Milestones small enough to complete in one loop", and "Stop-and-fix rule: if validation fails, repair before moving on", with tests, lint, typecheck and build as the checks run after each milestone. Git worktrees isolated runs and kept diffs reviewable.

THE OPERATIONAL CONSEQUENCE. The milestone size and the validation gate are a pair, and neither works alone: a milestone small enough for one loop is what makes a failed validation cheap to repair, and a gate that forbids advancing on a failure is what stops a long run compounding a defect for hours. Sizing milestones without the gate buys a tidy plan and a broken tree.

WHAT IS NOT ESTABLISHED. The author's own caveat: "This was an experiment, not a production rollout", and the result was not production-ready. No checkpoint or resume feature is described — the file-based status IS the resumption mechanism here — and no compaction or context-window handling is described at all. There are no runtime, token or cost caps stated, so the 25-hour figure is an observed run, not a supported limit.

Pack analysis, and a tension worth knowing: this account has the AGENT maintaining a markdown status file, while [[15e7bf02]] records that agents overwrite markdown state files and recommends JSON for machine-maintained progress state. The two are compatible only if the human-authored spec, plan and constraints are kept separate from the machine-maintained progress — which this source does not say it did.
