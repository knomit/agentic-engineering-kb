---
type: pattern
domain: [agentic-engineering, observability, architecture, guardrails, cost, coding-agents]
confidence: 0.8
sources: 1
entities: [Anthropic, Redwood Research, SLEIGHT-Bench, Claude Code, Claude Opus 4.6, extended thinking, LLM monitor, multi-stage classification]
motifs: [execution-verifies-claims, cheap-filter-first]
refs: ['https://alignment.anthropic.com/2026/sleight-bench/', 'kb://bc6eac5f37df/kb/architecture/ai/agents/security/permission-systems/89df351e.md', 'kb://bc6eac5f37df/kb/architecture/ai/agents/security/monitor-design/a5eaec6b.md']
---
# A monitor that can execute code checks the agent's claims instead of believing them — at about 10x the model invocations and 14x the output tokens of a single API call

On the SLEIGHT-Bench attack set, the Claude monitor was run two ways: as a passive reader of the transcript, and as a coding agent (Claude Code) able to execute code. The structural difference is what the monitor can do with a claim the agent made, and the authors state it concretely: "if an agent copies a large file but subtly alters part of it, a coding agent monitor can write a script to compare the two, while a regular monitor would have to take the output at face value."

THAT IS A MATCHED REMEDY FOR A SPECIFIC FAMILY OF BLIND SPOTS, not a general uplift. Counting lines in long output, tracking what a file holds after reassignment, finding a needle in an opaque blob, and checking whether a command behaves as claimed in a non-default environment are all things a passive reader must INFER and an executing monitor can simply MEASURE. Those are exactly the categories that score lowest for a passive monitor — counting 13%, file/object reuse 15%, model priors 13%, needle in haystack 38% at a 1% false-positive threshold.

**THE COST, stated by the authors, and the reason this is an architecture decision rather than a default:** "The Claude Code monitor on average takes ~10x more model invocations and generates ~14x more output tokens than the API call." The two multipliers are different and they constrain different things — invocations drive latency and rate limits, output tokens drive spend. Do not collapse them into a single "10x more expensive"; a system that is rate-limited and one that is budget-limited hit different walls.

**WHERE TO PUT IT**, in the authors' own suggestion: as a second stage — "using these expensive classifiers only as a second stage in a multi-stage classification system." A cheap passive monitor triages the whole stream; the executing monitor adjudicates what the cheap one flags, or covers a narrow high-stakes path outright. This is the same staging this corpus records for permission classifiers, arriving on the monitoring side of the same problem.

ALSO MEASURED, AND CHEAPER THAN EITHER: across every model tested as a monitor, "the general trend shows that more compute means better detection", and enabling extended thinking — on top of always letting the monitor write out reasoning before scoring — "improves performance for most models." Extended thinking is the first knob to turn; the agentic scaffold is the expensive one.

**NOT ESTABLISHED.** The post does not publish the agentic monitor's per-category catch rate against the passive monitor's, so the SIZE of the uplift bought by that 10x/14x is not stated — only its direction and its price. Treat the cost figures as firm and the benefit as directional until someone publishes both arms on the same categories.
