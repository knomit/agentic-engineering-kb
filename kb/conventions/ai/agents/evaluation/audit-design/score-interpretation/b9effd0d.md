---
type: process
domain: [agentic-engineering, evaluation, benchmarks, llm-judge, reliability]
confidence: 0.8
sources: 1
entities: [Anthropic, Alignment Science, Petri, Petri 2.0, seed library, behavioural audit, LLM-as-judge, auditor model, Claude Sonnet 4.5, GPT-5.1, Claude Opus 4.5, Gemini 3 Pro]
motifs: [instrument-defines-the-denominator, single-judge-bias-channel]
refs: ['https://alignment.anthropic.com/2026/petri-v2/', 'kb://bc6eac5f37df/kb/conventions/ai/agents/evaluation/audit-realism/realism-measurement/b84c73e8.md', 'kb://bc6eac5f37df/kb/conventions/ai/agents/evaluation/dataset-construction/65694027.md']
---
# A seeded behavioural audit's absolute score is not a quantity — Petri 2.0 states values are meaningful only in relative terms, and runs every target through two auditors and three independent judges

A behavioural-audit suite scores a target model by running it against seed instructions and having a judge score the resulting transcripts. Petri 2.0 runs a fixed library — "Each target model was run on all 181 seed instructions once per auditor model" — and states outright that "Score values are primarily meaningful in relative (rather than absolute) terms". The reason is that the absolute level is set by how often the suite's seeds could plausibly elicit the behaviour at all, which is a property of the seed library rather than of the model.

Two consequences for anyone reading or running one.

(1) DO NOT QUOTE AN AUDIT SCORE AS A RATE, and do not compare scores across suites or across versions of the same suite. Petri 2.0 "added 70 fully new seed instructions to Petri's seed library" to reach 181, which changes the denominator: a suite revision is a change of instrument, not a measurement of drift. Comparisons belong between models on one fixed suite, in one configuration.

(2) DO NOT RUN ONE AUDITOR AND ONE JUDGE. Each target was run "using two different auditors (Claude Sonnet 4.5 and GPT-5.1)" and each transcript "independently judged by Claude Opus 4.5, Gemini 3 Pro, and GPT-5.1", so no single model's idiosyncrasy — as attacker or as scorer — carries a result on its own. A result that exists only under one auditor-judge pair is a property of that pair until a second pair reproduces it.

WHAT THIS DOES NOT MEAN: not that the scores are useless, and not that the suite should be frozen. It means the comparison has to be held inside one instrument. A suite whose seeds rarely elicit the behaviour yields a low score for a reason that has nothing to do with the model's propensity, so a low number is evidence about the pair (model, suite) and never about the model alone.
