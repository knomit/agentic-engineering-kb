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
https://www.latent.space/
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
changelog and re-check the kb/*/ai/agents/tools/mcp/** facts. Checked 2026-07-26 (third run):
still 2025-11-25, no action needed.

redirects folded into the list above on 2026-07-26 so future runs stop paying a round-trip
for them:
  cookbook.openai.com -> developers.openai.com/cookbook
  blog.langchain.dev  -> www.langchain.com/blog

langchain's blog is the highest-yield recurring feed found so far — five agent/eval posts in
the week to 2026-07-25, and no run before the third one had followed it to articles. Do not
skip it.

dead or unreadable via WebFetch, do not keep re-fetching blind:
  aws.amazon.com/builders-library -> builder.aws.com (JS-rendered; both the index and
    individual article URLs return an empty shell). Needs a different fetch path or a
    browser; the Builders' Library material on retries/timeouts/backpressure is still
    unmined and is worth real effort.
  block.github.io/goose -> goose-docs.ai (the new host works; the old one only serves a
    "goose has moved" stub)
