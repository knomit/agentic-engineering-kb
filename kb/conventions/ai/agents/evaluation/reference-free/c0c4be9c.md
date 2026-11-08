---
type: process
domain: [agentic-engineering, evaluation, benchmarks, llm-judge, reliability]
confidence: 0.8
sources: 1
entities: [Anthropic, Alignment Science, ACCoRD, Conceptual Reasoning Index, consistency constraints, reference-free evaluation, preference ordering]
motifs: [coherence-without-ground-truth, necessary-not-sufficient-check]
refs: ['https://alignment.anthropic.com/2026/conceptual-reasoning-index/', 'kb://bc6eac5f37df/kb/conventions/ai/agents/evaluation/harness-design/47f5445a.md', 'kb://bc6eac5f37df/kb/invariants/ai/agents/evaluation/measurement/8a7dc152.md']
---
# Logical consistency across separate queries is an eval signal that needs no ground truth — a model inconsistent in a domain should not have its single-sample judgement there treated as authoritative

ACCoRD scores whether a model's reported probabilities and preference orderings are mutually consistent across separate queries: each constraint asserts a relation that any coherent answerer must satisfy, and the check is run over answers elicited independently. No correct answer is needed anywhere in the method. A model whose answer to one query contradicts its own answer to another has been caught without anyone establishing which of the two was right.

Operational consequence: for subjective or unverifiable work where you cannot build a key — triage priorities, risk ratings, severity scores, preference judgements, numeric estimates — you can still measure coherence. Elicit the same underlying judgement through separate, independently sampled calls, state the relations a coherent answerer must satisfy, and check them. Violations are defects you can act on immediately and localise by domain. The result also carries a direct deployment consequence: in a domain where an agent contradicts itself across queries, a single sample of its judgement is not authoritative, so that domain is where you add a second sample, a tie-break, or a human.

What this does not mean: consistency is not correctness. A model can be perfectly coherent and uniformly wrong, so a consistency score is a necessary-condition check and never evidence that the answers are right — do not report it as accuracy or let it stand in for a key where a key is obtainable. In the CRI itself it is weighted below the argument-rating benchmark, and only the human-approved subset of its constraints counts.
