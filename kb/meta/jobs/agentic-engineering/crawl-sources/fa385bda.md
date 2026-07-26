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
https://builder.aws.com/learn/topics/builders-library
https://code.claude.com/docs/en/best-practices
https://genai.owasp.org/
https://modelcontextprotocol.io/specification/versioning

*** READ THIS FIRST: THE BROWSER CHANGES WHAT IS REACHABLE ***
Added 2026-07-26 (fifth run). When the claude-in-chrome MCP tools are available in the
session, JS-rendered sources that WebFetch cannot read are trivially readable. The method
that worked first try, with no clicking or waiting:
    mcp__claude-in-chrome__navigate {url}      -> returns a tabId
    mcp__claude-in-chrome__get_page_text {tabId} -> returns full article text
This cleared builder.aws.com, which three runs had recorded as permanently blocked. Before
recording ANY source as dead, check whether the browser tools are loadable in the session.
Still-unattempted browser targets, all previously written off as JS-rendered:
  www.vectara.com hallucination leaderboard (needed to firm up kb/gotchas/ai/agents/
    reliability/cb98732e, whose 2026 numbers currently rest on secondary reporting)
  gorilla.cs.berkeley.edu/leaderboard.html (BFCL), www.swebench.com, www.promptfoo.dev/docs

note: the MCP versioning page was added 2026-07-26 because that run found the pack a full
protocol revision behind (facts cited 2025-06-18 while 2025-11-25 was current). It is cheap
to check and names the current revision directly; when it changes, re-read that revision's
changelog and re-check the kb/*/ai/agents/tools/mcp/** facts. Checked 2026-07-26 (fourth
run): still 2025-11-25, no action needed. Not re-checked on the fifth run.

redirects folded into the list above on 2026-07-26 so future runs stop paying a round-trip
for them:
  cookbook.openai.com -> developers.openai.com/cookbook
  blog.langchain.dev  -> www.langchain.com/blog
  aws.amazon.com/builders-library -> builder.aws.com/learn/topics/builders-library

CORRECTED 2026-07-26 (fourth run): this list had drifted to the bare domain
www.latent.space, which serves only the Substack subscribe header and no post list. It is
https://www.latent.space/archive and it works fine. Restored above. Lesson for future runs:
when a feed returns a subscribe wall or a bare header, suspect the URL before concluding the
source is dead.

CORRECTED 2026-07-26 (fifth run): two cognition slugs queued below by the fourth run were
guessed from titles and 404'd. Always pull https://cognition.com/blog for exact slugs.
  'Verifying Agentic Development at Scale' = /blog/testing-development (READ, 1 fact)
  'Coding Agents 101'  = /blog/coding-agents-101-the-art-of-actually-getting-things-done

YIELD RANKING as of the fifth run — spend the budget in this order:
  1. builder.aws.com Builders' Library — NEWLY UNBLOCKED and by far the biggest untouched
     seam. One article (timeouts-retries-and-backoff-with-jitter) produced four facts
     including the 243x retry-amplification figure. ~20 more are on the index, all pre-LLM
     distributed systems, all of which map onto agent reliability. Read next, in this order:
     'Using dependency isolation to contain concurrency overload' (bulkheads — an agent
     exhausting a shared tool pool is exactly this), 'Fairness in multi-tenant systems'
     (throttling and quotas for multi-tenant agent platforms), 'Minimizing correlated
     failures in distributed systems', 'Workload isolation using shuffle-sharding',
     'Implementing health checks', 'Challenges with distributed systems', 'Amazon's approach
     to failing successfully', 'Leader Election in Distributed Systems'. Article URLs are
     opaque content IDs — get them off the index page rather than guessing. The index has a
     'Load more' button, so the 20 listed are not the whole set.
  2. anthropic.com/engineering — still strong. Read this run: advanced-tool-use,
     managed-agents, demystifying-evals-for-ai-agents, effective-harnesses-for-long-running-
     agents, claude-think-tool, claude-code-sandboxing. STILL UNREAD and worth it:
     how-we-contain-claude, april-23-postmortem, eval-awareness-browsecomp,
     building-c-compiler (parallel Claudes), AI-resistant-technical-evaluations,
     equipping-agents-for-the-real-world-with-agent-skills, a-postmortem-of-three-recent-
     issues, contextual-retrieval, swe-bench-sonnet, desktop-extensions.
  3. cognition.com/blog — dense and specific; they publish reversals of their own positions.
     Unread and relevant: coding-agents-101-the-art-of-actually-getting-things-done,
     devin-sonnet-4-5-lessons-and-challenges, swe-grep (RL for fast context retrieval),
     blockdiff (VM disk snapshot format for agent VMs), devin-annual-performance-review-2025,
     evaluating-coding-agents, making-fable-cheaper-than-opus, devin-fusion.
     Skip the partnership/office-opening/funding posts — roughly half the feed is those.
  4. eugeneyan.com/writing — upgraded. Both articles read this run cleared the bar easily
     (cybersecurity-evals gave the Incalmo 3/40-vs-37/40 harness-beats-model number;
     working-with-ai gave the execution-vs-direction-drift split). Unread: secure-source-code
     (May 2026), plus whatever is newer than that.
  5. sourcegraph.com/blog — publishes real measurements (n=1,281 agent runs) rather than
     opinions. Unread: code-finder-fast-code-search-for-agents,
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone.
  6. latent.space/archive — interview format, but /p/bad-envs yielded the '>5% environment
     failure rate means a harness problem' threshold plus a full taxonomy of broken-env error
     classes. Unread: /p/modal2026, /p/gray-swan (red-teaming), /p/aiewf26trends.
  7. simonwillison.net/tags/llms/ — high volume, mostly link-blogging; scan for incidents and
     security, skip model-release commentary. Unread: the-first-known-runaway-ai-agent,
     thomas-ptacek (sandbox escapes), bad-codex-bug (file deletions).
  8. langchain.com/blog — steady agent/eval output but vendor-heavy; the eval-engineering and
     benchmark posts clear the bar, the customer stories do not.
  9. embracethered.com/blog — low volume, high value, security only.
 10. trychroma.com/research — rare (5 reports ever) but each is substantial. Read this run:
     generative-benchmarking. Unread: evaluating-chunking.

dead or unreadable, do not keep re-fetching blind:
  block.github.io/goose -> goose-docs.ai (the new host works; the old one only serves a
    'goose has moved' stub). goose-docs.ai/docs/guides/context-engineering/subagents was read
    this run and was worth it — concrete limits, not marketing.
  NOTE: builder.aws.com was listed here for three runs and was NEVER dead. See the browser
    note at the top.

checked and low-yield for this pack (do not deprioritise permanently, but do not lead with
them): research.google/blog — scanned 2026-07-26, recent output is health/quantum/diffusion
with nothing on agents, tool use, or evals. microsoft.com/en-us/security/blog — yielded one
good agent-identity post but is mostly threat-intel unrelated to building agents.
