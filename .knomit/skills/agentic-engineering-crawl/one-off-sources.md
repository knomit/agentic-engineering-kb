# One-off sources (backfill)

Crawl each of these ONCE. After a source appears in `one-off-done.md` or in a
`seen/<host>.md` list, do not re-crawl it here — re-verification happens only in the staleness pass.

## Tier 0 — security (agents fail hardest here)

- https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/
- https://genai.owasp.org/llm-top-10/
- https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/
  (NOT settled. A documented counter-position exists and runs 12 and 13 both
  flagged its absence here. Treat this the way Tier 1 treats the Apple paper:
  find and record the counter-position, and if it survives, write a `decisions`
  fact naming the conditions each side holds under rather than picking one.)
- https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook
- https://www.nist.gov/itl/ai-risk-management-framework

## Tier 1 — contested questions (highest value)

Sources that reach opposite conclusions. Process as PAIRS: fetch both sides
before writing any fact from either side.

- https://cognition.com/blog/dont-build-multi-agents
  vs https://www.anthropic.com/engineering/multi-agent-research-system
  (NOTE: Cognition narrowed this position themselves in
  https://cognition.com/blog/multi-agents-working — crawled 2026-07-26. The pair
  is resolved in the kb; do not re-open it as an open question.)
- https://www.trychroma.com/research/context-rot
  vs https://arxiv.org/abs/2307.03172 (Lost in the Middle — the older claim
  this report re-tests on current models)
- https://www.databricks.com/blog/long-context-rag-performance-llms
  vs https://arxiv.org/abs/2404.16130 (GraphRAG)
  vs https://arxiv.org/abs/2005.11401 (original RAG)
- https://arxiv.org/abs/2506.06941 (Apple, "The Illusion of Thinking" — drew
  substantial published rebuttals disputing its experimental design; search for
  and record the counter-position, do not treat the paper as settled)
- https://a2a-protocol.org/latest/
  vs https://modelcontextprotocol.io/specification/2026-07-28
  (competing agent-interop models. A2A reached v1.0; MCP's current revision is
  **2026-07-28** — do not cite 2025-11-25 or 2025-06-18. Corrected 2026-08-11
  after runs 12 and 13 both flagged this line as stale; the live revision is
  pinned by the versioning tripwire in `sources.md`.)
- https://hamel.dev/blog/posts/llm-judge/
- https://applied-llms.org/

## Tier 2 — practitioner guidance

- https://www.anthropic.com/engineering/building-effective-agents
- https://www.anthropic.com/engineering/writing-tools-for-agents
- https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- https://code.claude.com/docs/en/best-practices
- https://www.anthropic.com/engineering/code-execution-with-mcp
- https://developers.openai.com/api/docs/guides/agents
- ~~`cdn.openai.com/.../a-practical-guide-to-building-agents.pdf`~~ — SKIP. Fetches
  as undecoded binary and there is no PDF renderer in this session; failed twice.
  Do not spend a fetch on it. Its multi-agent material is covered by the OpenAI
  agents guide above; the guardrails and model-selection sections remain unread.
- https://github.com/humanlayer/12-factor-agents
- https://www.philschmid.de/context-engineering
- https://huyenchip.com/2025/01/07/agents.html
- https://eugeneyan.com/writing/llm-patterns/
- https://hamel.dev/blog/posts/evals/

## Tier 3 — architecture and patterns (prescriptive; good invariant material)

- https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html
- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns
- https://learn.microsoft.com/en-us/azure/architecture/ai-ml/
- ~~`aws.amazon.com/builders-library`~~ → https://builder.aws.com/learn/topics/builders-library
  — BLOCKED, do not spend a blind fetch. Both the index and individual article
  URLs are JS-rendered and return an empty shell; three runs have now failed on
  it. The material (pre-LLM distributed systems: retries, timeouts, backpressure)
  is still the single most valuable unmined item in this file, because agent
  reliability is a distributed-systems problem. It needs a browser tool or a
  different fetch path — attempt it ONLY with one of those.
- https://docs.temporal.io/evaluate/use-cases-design-patterns
  (durable execution for long-running agents that crash mid-task)

## Tier 4 — specs and reference (ground invariants here, not in blog posts)

- https://modelcontextprotocol.io/docs/concepts/tools
- https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview
- https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices
- https://reference.langchain.com/python/langgraph/
  (the older `langchain-ai.github.io/langgraph/concepts/multi_agent` answers 200
  but serves a JS stub with no readable content, and the `docs.langchain.com`
  successor path 404s — use this instead)
- https://adk.dev/
- https://pydantic.dev/docs/ai/overview/
- https://ai-sdk.dev/docs/introduction

## Tier 5 — empirical measurement (numbers, not opinions)

Three of these serve no numbers to a plain fetch. They are JS-rendered and the
served HTML contains no scores or assertion types — crawled 2026-07-26, nothing
extractable. Do not expect measurements from them without a browser:
`gorilla.cs.berkeley.edu/leaderboard.html`, `www.swebench.com`,
`www.promptfoo.dev/docs/intro`.

- https://gorilla.cs.berkeley.edu/leaderboard.html (BFCL — tool calling; JS-rendered)
- https://github.com/sierra-research/tau-bench
- https://www.swebench.com/ (JS-rendered)
- https://arxiv.org/abs/2308.03688 (AgentBench — DONE, abstract only. Its named
  failure modes are below this pack's altitude bar and the paper is 2023. Treat
  as a tier-7 anchor; do not re-fetch expecting more.)
- https://www.promptfoo.dev/docs/intro/ (JS-rendered)
- https://docs.langchain.com/langsmith/evaluation-concepts

## Tier 6 — evidence of practice (what shippers actually do)

This tier is the LEAST covered as of 2026-07-26 — most entries are still unread.

- https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools
  (the repo root returns the directory listing of 25+ harnesses but no README
  text — nothing quotable. The value is in the individual prompt files; pick
  specific ones. Provenance is unverified: frame anything from here as "this
  harness's published prompt does X", never as "the correct approach is X".)
- https://github.com/anthropics/claude-cookbooks
- https://developers.openai.com/cookbook
- https://github.com/NirDiamant/GenAI_Agents
- https://github.com/NirDiamant/RAG_Techniques
- https://github.com/microsoft/autogen
- https://github.com/microsoft/semantic-kernel
- https://github.com/strands-agents/sdk-python
- https://strandsagents.com/
  (homepage only so far; two guessed doc paths 404'd. SummarizingConversationManager,
  SlidingWindowConversationManager, and the Swarm / Agent-as-Tool patterns are
  named on the homepage but undocumented there — find the real doc URLs.)
- https://goose-docs.ai/
  (block.github.io/goose now serves only a "goose has moved" stub. Known-good
  unfetched URL: https://goose-docs.ai/docs/guides/context-engineering/subagents)

## Tier 7 — papers (cite as anchors; do not restate their content)

- https://arxiv.org/abs/2210.03629 (ReAct)
- https://arxiv.org/abs/2303.11366 (Reflexion)
- https://arxiv.org/abs/2411.04468 (Magentic-One)