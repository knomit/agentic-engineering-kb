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
https://github.com/vectara/hallucination-leaderboard

*** READ THIS FIRST: 'JS-RENDERED, UNREADABLE' VERDICTS IN THIS PACK ARE UNRELIABLE ***
Two separate sources have now been written off as unreachable and turned out not to be.
  builder.aws.com — recorded dead by three runs. The browser reads it fine (method below).
  Vectara hallucination leaderboard — recorded as needing a browser. It does not: the
    canonical source is the GitHub README at github.com/vectara/hallucination-leaderboard,
    which is server-rendered and reads with a plain WebFetch.
Before recording ANY source as dead, do both of these: (1) look for a server-rendered
canonical mirror — a GitHub README, a raw file, an RSS/Atom feed, an archive path; (2) check
whether the claude-in-chrome browser tools are loadable in the session.

Browser method, works first try, no clicking or waiting:
    mcp__claude-in-chrome__navigate {url}        -> returns a tabId
    mcp__claude-in-chrome__get_page_text {tabId} -> full article text
CAVEAT added 2026-07-26 (sixth run): on builder.aws.com the FIRST get_page_text after a
navigate returns the literal string 'Loading article'. Call it a SECOND time and the content
is there. A single call plus a hasty conclusion is very likely what produced the original
false 'blocked' verdicts. To pull links/hrefs off an index, use
    mcp__claude-in-chrome__javascript_tool with a querySelectorAll expression —
    mcp__claude-in-chrome__find returns element refs but NOT hrefs.

Still-unattempted browser targets: gorilla.cs.berkeley.edu/leaderboard.html (BFCL),
www.swebench.com, www.promptfoo.dev/docs. Check each for a GitHub mirror first.

*** AWS BUILDERS' LIBRARY — ENUMERATED ARTICLE IDS (pulled 2026-07-26, sixth run) ***
Article URLs are opaque content IDs and CANNOT be guessed from titles. They are listed here
so no future run has to re-derive them. Form the URL as:
    https://builder.aws.com/content/<ID>/<slug>
READ so far (3 of 20):
  timeouts-retries-and-backoff-with-jitter | 3EumjoZascWd1oZiEgL8ORlv3qE   (4 facts)
  using-dependency-isolation-to-contain-concurrency-overload | 3EuxuD6bWtQ6gEp9FaKQfd3Z2AM (7)
  fairness-in-multi-tenant-systems | 3Eupj3d2bo4fEvlzYbICMZNhQ3B          (5 facts)
  workload-isolation-using-shuffle-sharding | 3F06NpJ8YeoIGP8VHTw4n81pFn8 (1 fact)
UNREAD — read roughly in this order (reliability material first, CI/CD material last):
  minimizing-correlated-failures-in-distributed-systems | 3Ev2H7t3l2eZa9xBXiZcAjz12JK
  challenges-with-distributed-systems | 3F08f7GPFiZMCgXD8gny6OjxR0Z
  implementing-health-checks | 3Ev53O39izHCtWLzp4XU6t8PC1O
  amazons-approach-to-failing-successfully | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
  resilience-lessons-from-the-lunch-rush | 3Ev17ZWA9QX88MmoaULAKevIR8H
  leader-election-in-distributed-systems | 3Ev0vH0hfkcUizISUWYTvHibtcp
  amazons-approach-to-building-resilient-services | 3Ev4sNuZLsnpwl9CZAOOO8hkZyf
  architecting-and-operating-resilient-serverless-systems-at-scale | 3Ev4bbEHBC5KvyYC6IcNazUXJmk
  ensuring-rollback-safety-during-deployments | 3F04j2yRAAMBuPSPs50xwXZqg01
  amazons-approach-to-automated-software-and-systems-testing | 3F07fTC9nQCkhqCTP5vIzgyOcIH
  amazons-approach-to-security-during-development | 3F07JXrYkwtKDhPgoUbI0UAA0Zf
  building-dashboards-for-operational-visibility | 3Ev2iw3R3ahQOM8BT4OUR0WP51z
  operational-excellence-at-amazon | 3Ev4irLmkHOBR3BhODX2vuE0Syf
  hands-off-automating-continuous-delivery-pipelines-at-amazon | 3Ev3Nho3q1Cs04EZUVB1ckhNJWL
  my-cicd-pipeline-is-my-release-captain | 3Ev3XnnYuuBhlgnywbbVFzwibm1
  going-faster-with-continuous-delivery | 3F08Mhh186qOa4VhG19egs06NJa
The index has a 'Load more' button, so these 20 are NOT the whole catalogue. Articles
cross-referenced from inside the ones already read, but absent from the un-expanded index —
all directly relevant, IDs still needed:
  'Using load shedding to avoid overload', 'Caching challenges and strategies',
  'Avoiding insurmountable queue backlogs', 'Reliability, constant work, and a good cup of
  coffee', 'Static stability using Availability Zones', 'Instrumenting distributed systems
  for operational visibility'.

note: the MCP versioning page names the current protocol revision directly and is cheap to
check; when it changes, re-read that revision's changelog and re-check the
kb/*/ai/agents/tools/mcp/** facts. Checked 2026-07-26 (fourth run): still 2025-11-25. The
sixth run found kb/architecture/ai/agents/interop/protocols/62312b79 still REFERENCING the
superseded 2025-06-18 revision and repointed it — when the revision moves, grep the refs, not
just the bodies.

redirects folded into the list above so future runs stop paying a round-trip for them:
  cookbook.openai.com -> developers.openai.com/cookbook
  blog.langchain.dev  -> www.langchain.com/blog
  aws.amazon.com/builders-library -> builder.aws.com/learn/topics/builders-library
  www.latent.space -> www.latent.space/archive (the bare domain serves only a subscribe wall)

CORRECTED (fifth run): two cognition slugs guessed from titles 404'd. Always pull
https://cognition.com/blog for exact slugs.
  'Coding Agents 101' = /blog/coding-agents-101-the-art-of-actually-getting-things-done

YIELD RANKING as of the sixth run — spend the budget in this order:
  1. builder.aws.com Builders' Library — confirmed the best seam in the pack. Three articles
     produced 13 facts on the sixth run, the highest facts-per-fetch of any source. 17 of 20
     enumerated articles are unread and the catalogue is larger than 20. Pre-LLM distributed
     systems material that maps directly onto agent reliability: bulkheads, admission
     control, blast radius, correlated failure, health checks.
  2. anthropic.com/engineering — still strong. Read so far: advanced-tool-use,
     managed-agents, demystifying-evals-for-ai-agents, effective-harnesses-for-long-running-
     agents, claude-think-tool, claude-code-sandboxing, harness-design-long-running-apps,
     infrastructure-noise, claude-code-auto-mode, equipping-agents-for-the-real-world-with-
     agent-skills. STILL UNREAD: how-we-contain-claude, april-23-postmortem,
     eval-awareness-browsecomp, building-c-compiler, AI-resistant-technical-evaluations,
     a-postmortem-of-three-recent-issues, contextual-retrieval, swe-bench-sonnet,
     desktop-extensions.
  3. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread:
     coding-agents-101-the-art-of-actually-getting-things-done, devin-sonnet-4-5-lessons-and-
     challenges, swe-grep, blockdiff, devin-annual-performance-review-2025,
     evaluating-coding-agents, making-fable-cheaper-than-opus, devin-fusion. Skip the
     partnership/funding/office posts — about half the feed.
  4. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
  5. sourcegraph.com/blog — real measurements (n=1,281 agent runs), not opinions. Unread:
     code-finder-fast-code-search-for-agents,
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone.
  6. latent.space/archive — interview format but yields thresholds. Unread: /p/modal2026,
     /p/gray-swan, /p/aiewf26trends.
  7. simonwillison.net/tags/llms/ — high volume, mostly link-blogging; scan for incidents and
     security, skip model-release commentary. Unread: the-first-known-runaway-ai-agent,
     thomas-ptacek (sandbox escapes), bad-codex-bug (file deletions).
  8. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
  9. embracethered.com/blog — low volume, high value, security only.
 10. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.

dead or unreadable, do not keep re-fetching blind:
  block.github.io/goose -> goose-docs.ai (old host serves only a 'goose has moved' stub).
  NOTE: builder.aws.com and the Vectara leaderboard were BOTH listed here and neither was
    ever dead. See the warning at the top of this file before adding anything to this list.

checked and low-yield for this pack (do not deprioritise permanently, but do not lead with
them): research.google/blog — recent output is health/quantum/diffusion, nothing on agents,
tools, or evals. microsoft.com/en-us/security/blog — one good agent-identity post, otherwise
threat intel unrelated to building agents.
