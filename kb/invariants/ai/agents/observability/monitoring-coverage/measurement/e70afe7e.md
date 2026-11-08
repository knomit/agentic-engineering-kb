---
type: reference
domain: [agentic-engineering, observability, evaluation, operations, governance, guardrails]
confidence: 0.85
sources: 1
entities: [METR, Redwood Research, OpenAI, Responses API, Codex, GPT-5.5, misalignment monitoring, compaction, load shedding]
motifs: [denominator-decides-the-claim, excluded-scope-reads-covered]
refs: ['https://metr.org/blog/2026-10-22-red-teaming-openai-agent-monitoring/', 'kb://bc6eac5f37df/kb/incidents/ai/agents/observability/monitor-suppression/07222034.md', 'kb://bc6eac5f37df/kb/conventions/ai/agents/evaluation/misalignment-monitoring/7aecb3c3.md']
---
# A monitoring-coverage figure means nothing without its eligibility filter and its excluded services: 75-94% of eligible agentic traffic, 99.2% of one internal deployment, and about 10% of that deployment lost to compaction

METR and Redwood Research spent three weeks (21 July to 11 August 2026) inside OpenAI's internal misalignment monitoring system, with access to the internal codebase, the monitor prompts and configuration, internal documentation, and about a dozen interviews, on OpenAI-issued devices that never left the premises. The exercise primarily focused on estimating the fraction of agentic inference that is monitored. The figures, and every qualifier attached to them:

- Roughly 75-94% of ELIGIBLE agentic Responses API traffic from models at least as strong as GPT-5.5, with substantial uncertainty in both directions.
- 99.2% of the internal Codex subset was ELIGIBLE for monitoring — eligibility, not coverage.
- About 10% of eligible internal Codex traffic nonetheless went unmonitored between May and July 2026, again with substantial uncertainty.
- The monitor errored on less than 0.2% of requests, and there were zero load-sheds in one 24-hour period during the exercise.

TWO SCOPE FACTS THAT A SUMMARY DROPS, AND THEY ARE WHAT MAKE THE NUMBERS READABLE. Traffic from OpenAI's internal research inference service was excluded entirely, and METR could not estimate its volume due to access and time constraints — so the percentages are shares of a denominator that itself omits an unmeasured service. And RL training runs were not covered by the monitoring system at the start of the exercise, with only a subset of rollouts covered from March to June.

Operational consequence: when anyone reports a monitoring-coverage percentage, the useful questions are what the eligibility filter excludes, which services sit outside the denominator, and whether eligible-but-unmonitored traffic is reconciled. Two of the four numbers above are eligibility rather than coverage, and the gap between them — 99.2% eligible, about 10% of that unmonitored — is the whole finding. This is a coverage question and a separate one from sampling rate and discovery lag, which [[7aecb3c3]] measures on the same organisation's incidents.

SCOPE: this is a published subset of a 61-page internal report (38 pages redacted for leadership), covering the system as it existed on and before 21 July, and the exercise did not evaluate changes in progress at the time. OpenAI says the production-impacting vulnerabilities were patched; METR states it has not evaluated those claims, so this is a stated remediation and not an audited end state. For what unmonitored agent behaviour actually looked like in the same organisation, see [[07222034]].
