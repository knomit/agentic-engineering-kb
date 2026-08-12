# agentic-engineering

A knowledge pack for people building agentic products — and for coding agents
handed this repo as context. Every fact is distilled from a named external source
that took a position and could be wrong. Nothing is invented, and nothing is
written without a URL.

## What this pack is for

The reader is at a decision point and needs guidance concrete enough to act on.
**A good fact changes what gets built.**

The bar is one question:

> **Would a competent model already produce this, at this level of specificity,
> from its own priors?** If yes, it does not belong here.

That is a test of altitude, not of subject. Patterns and good practices are very
much in scope — stated generically they are noise, because the model already knows
them; stated with their boundary conditions they are the most useful thing here.
Naming ReAct is not a fact. When ReAct beats a single call, what it costs, and how
it fails, is.

| Too generic — discarded | Specific enough — kept |
|---|---|
| "Use the orchestrator-worker pattern for complex tasks." | "Orchestrator-worker buys context isolation, not parallelism: each worker sees only its subtask. It stops paying once subtasks need each other's intermediate results." |
| "Write good tool descriptions." | "Tool descriptions compete with their siblings, not with a blank page. Lead with the distinguishing condition — 'use when X, not Y'." |
| "Agents should handle errors." | "Return tool failures as readable tool results, not exceptions that abort the loop. The error string is a prompt: say what to do differently." |
| "Evaluate your agent." | "Output-only evals pass an agent that reached the right answer through a destructive tool call. Tool-calling agents need trajectory assertions." |

So: patterns and architectures with the conditions where they stop being right;
thresholds, limits and ordering constraints; contested tradeoffs and what decides
them; failure modes with symptom and cause; spec-level rules that are easy to get
wrong.

## How facts are written

Before a fact is created, the pack is queried for the same claim.

1. If an existing fact makes the claim, it is **updated** — new ref, adjusted
   confidence, refined wording. A second fact is not created.
2. If an existing fact **contradicts** it, no winner is silently picked. Both are
   kept and a `decisions` fact names the conditions under which each holds, citing
   both sources. A live disagreement between credible sources is never flattened
   into one confident claim — the conditions that separate them are what a reader
   actually needs.
3. Otherwise a new fact is written.

**Every fact carries at least one URL in `refs`. No exceptions.**

Confidence follows source strength: **0.85–0.9** for a spec, official docs, or a
reproducible published measurement; **0.7–0.8** for a vendor or practitioner post
reporting production experience; **0.6–0.65** for a single blog assertion or advice
tied to one model version. Claims whose numbers depend on a model generation carry
a staleness note in the body — read it before quoting the figure.

Facts live at `kb/<topic>/<category>/<uuid>.md`. The topic says what kind of claim
it is — `invariants` (violate it and it breaks), `gotchas` (surprising, costs you a
day), `decisions` (a tradeoff with rationale and conditions), `conventions` (idioms
that work), `architecture` (how components fit), `incidents` (a documented failure
and its fix). Categories are freeform paths under `ai/agents/<area>` and
`ai/rag/<area>`; see `domains/ontology.yaml`.

## Where the knowledge comes from

Roughly eighty sources, all external and all cited. The families that matter:

- **Vendor engineering writing** — Anthropic engineering (the densest single
  source), Claude platform and Claude Code docs, Cognition/Devin, OpenAI, LangChain,
  Sourcegraph, AWS Builders' Library, Microsoft/Azure, Goose, Vercel AI SDK.
- **Specs and standards** — Model Context Protocol (tracked at revision
  2025-11-25), OWASP GenAI, A2A, NIST AI RMF.
- **Independent practitioners and research** — Chroma research, Simon Willison,
  Eugene Yan, applied-llms.org, Hamel Husain, Chip Huyen, embracethered, Latent
  Space, Databricks, and arXiv anchors (ReAct, Reflexion, Magentic-One, Lost in the
  Middle, GraphRAG).

Some facts exist *because* two credible sources disagree, and are kept as
`decisions` facts naming the deciding condition rather than collapsed: Cognition's
*Don't Build Multi-Agents* against Anthropic's multi-agent research system; Chroma's
*Context Rot* against *Lost in the Middle*; long-context RAG against GraphRAG;
Apple's *Illusion of Thinking* against its rebuttals; A2A against MCP; and Vectara's
HHEM against FaithJudge, where the same models score ~1% and ~8–12% because the
grader sets the headline number.

## Maintenance

A periodic crawl job refreshes the pack. Its state lives under
`.knomit/jobs/agentic-engineering/`: `crawl-sources/` holds the live source list, yield
ranking and known-dead URLs, and `crawl-state/` holds **only the most recent run** —
the full crawl record is that fact's revision history, not its body. Each run also
re-checks a sample of low-confidence and ageing facts against their sources and
corrects or retracts them; this is a field where advice expires.
