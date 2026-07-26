---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Recurring crawl sources

https://www.anthropic.com/engineering
https://developers.openai.com/cookbook
https://simonwillison.net/tags/llms/
https://www.langchain.com/blog/
https://www.latent.space/archive
https://eugeneyan.com/writing/
https://www.microsoft.com/en-us/research/blog/
https://www.microsoft.com/en-us/security/blog/
https://aws.amazon.com/blogs/machine-learning/
https://research.google/blog/
https://embracethered.com/blog/
https://metr.org/blog/
https://sourcegraph.com/blog
https://cognition.com/blog
https://www.trychroma.com/research
https://code.claude.com/docs/en/best-practices
https://genai.owasp.org/
https://modelcontextprotocol.io/specification/versioning

note: the MCP versioning page was added 2026-07-26 because that run found the pack a full
protocol revision behind (facts cited 2025-06-18 while 2025-11-25 was current). It is cheap
to check and names the current revision directly; when it changes, re-read that revision's
changelog and re-check the kb/*/ai/agents/tools/mcp/** facts. Checked 2026-07-26 (fourth
run): still 2025-11-25, no action needed.

redirects folded into the list above on 2026-07-26 so future runs stop paying a round-trip
for them:
  cookbook.openai.com -> developers.openai.com/cookbook
  blog.langchain.dev  -> www.langchain.com/blog

CORRECTED 2026-07-26 (fourth run): this list had drifted to the bare domain
www.latent.space, which serves only the Substack subscribe header and no post list — which
is why three runs recorded it as yielding nothing. The seed file on disk had the correct
path all along. It is https://www.latent.space/archive and it works fine. Restored above.
Lesson for future runs: when a feed returns a subscribe wall or a bare header, suspect the
URL before concluding the source is dead.

YIELD RANKING as of the fourth run — spend the budget in this order:
  1. anthropic.com/engineering — BIGGEST FIND of the fourth run. Only the four Appendix A
     tier-2 articles had ever been read; the index carries a deep back-catalogue that no run
     had followed. Still unmined there: how-we-contain-claude, managed-agents (Apr 2026),
     eval-awareness-browsecomp, building-c-compiler (parallel Claudes), april-23-postmortem,
     AI-resistant-technical-evaluations, demystifying-evals-for-ai-agents. Start here.
  2. cognition.com/blog — dense and specific. Note they publish reversals of their own
     earlier positions, so re-reading them resolves contested facts. Unread and relevant:
     verifying-agentic-development-at-scale, coding-agents-101, devin-sonnet-4-5-lessons.
  3. sourcegraph.com/blog — publishes real measurements (n=1,281 agent runs) rather than
     opinions. Unread: code-finder-fast-code-search-for-agents,
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone.
  4. latent.space/archive — NEWLY REACHABLE, never mined. Interview-format but the guests
     are practitioners. Unread and on-topic: /p/bad-envs (shipping low-quality RL
     environments), /p/modal2026 (infrastructure for agent experience), /p/gray-swan
     (red-teaming), /p/aiewf26trends.
  5. simonwillison.net/tags/llms/ — high volume, mostly link-blogging; scan for incidents and
     security, skip model-release commentary. Unread: the-first-known-runaway-ai-agent,
     thomas-ptacek (sandbox escapes), bad-codex-bug (file deletions).
  6. langchain.com/blog — steady agent/eval output but vendor-heavy; the eval-engineering and
     benchmark posts clear the bar, the customer stories do not.
  7. embracethered.com/blog — low volume, high value, security only.
  8. trychroma.com/research — rare (5 reports ever) but each is substantial. Unread:
     generative-benchmarking, evaluating-chunking.
  9. eugeneyan.com/writing — unread and promising: cybersecurity-evals (Jun 2026),
     working-with-ai (May 2026), secure-source-code (May 2026).

dead or unreadable via WebFetch, do not keep re-fetching blind:
  aws.amazon.com/builders-library -> builder.aws.com (JS-rendered; both the index and
    individual article URLs return an empty shell). Needs a different fetch path or a
    browser; the Builders' Library material on retries/timeouts/backpressure is still
    unmined and is worth real effort.
  block.github.io/goose -> goose-docs.ai (the new host works; the old one only serves a
    "goose has moved" stub)

checked and low-yield for this pack (do not deprioritise permanently, but do not lead with
them): research.google/blog — scanned 2026-07-26, recent output is health/quantum/diffusion
with nothing on agents, tool use, or evals. microsoft.com/en-us/security/blog — yielded one
good agent-identity post but is mostly threat-intel unrelated to building agents.
