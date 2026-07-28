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
navigate SOMETIMES returns the literal string 'Loading article'; call it again and the
content is there. UPDATE 2026-07-27 (seventh run): did not reproduce once across five
article fetches — every first call returned full text. So treat it as an occasional race,
not a required two-step. Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index, use
    mcp__claude-in-chrome__javascript_tool with a querySelectorAll expression —
    mcp__claude-in-chrome__find returns element refs but NOT hrefs.

*** AWS BUILDERS' LIBRARY — COMPLETE ARTICLE ENUMERATION (30 of 30, 'Load more' fully
    expanded on the seventh run; this is the WHOLE catalogue, no more pagination) ***
Article URLs are opaque content IDs and CANNOT be guessed from titles. Form the URL as:
    https://builder.aws.com/content/<ID>/<slug>

READ (8 of 30):
  timeouts-retries-and-backoff-with-jitter | 3EumjoZascWd1oZiEgL8ORlv3qE            (4 facts)
  using-dependency-isolation-to-contain-concurrency-overload | 3EuxuD6bWtQ6gEp9FaKQfd3Z2AM (7)
  fairness-in-multi-tenant-systems | 3Eupj3d2bo4fEvlzYbICMZNhQ3B                   (5 facts)
  workload-isolation-using-shuffle-sharding | 3F06NpJ8YeoIGP8VHTw4n81pFn8          (1 fact)
  minimizing-correlated-failures-in-distributed-systems | 3Ev2H7t3l2eZa9xBXiZcAjz12JK (3+1upd)
  challenges-with-distributed-systems | 3F08f7GPFiZMCgXD8gny6OjxR0Z               (2+1upd)
  implementing-health-checks | 3Ev53O39izHCtWLzp4XU6t8PC1O                         (5 facts)
  making-retries-safe-with-idempotent-apis | 3Ev0BENTyBr0XxzRk5FDZzgNYos           (3 facts)
  avoiding-fallback-in-distributed-systems | 3EuS9Sakq7L3VLQIF3qzfMfke1Y           (3 facts)

UNREAD (21) — read roughly in this order, reliability material first, CI/CD last:
  using-load-shedding-to-avoid-overload | 3Eun1EEyX6p2e3VYNyRLSJzLuMV
  avoiding-insurmountable-queue-backlogs | 3EuRcgkTP1MI0c7zM8W6HL3WIqA
  avoiding-overload-in-distributed-systems-by-putting-the-smaller-service-in-control | 3EukISjbJAGNdrxjKaN6RG0wlHG
  reliability-constant-work-and-a-good-cup-of-coffee | 3F05oqNtNUWxHJ5r6L6I2HrH4rI
  instrumenting-distributed-systems-for-operational-visibility | 3EuxPBdIiiUhB5IK47p3O3fxhy7
  amazons-approach-to-failing-successfully | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
  resilience-lessons-from-the-lunch-rush | 3Ev17ZWA9QX88MmoaULAKevIR8H
  leader-election-in-distributed-systems | 3Ev0vH0hfkcUizISUWYTvHibtcp
  amazons-approach-to-building-resilient-services | 3Ev4sNuZLsnpwl9CZAOOO8hkZyf
  architecting-and-operating-resilient-serverless-systems-at-scale | 3Ev4bbEHBC5KvyYC6IcNazUXJmk
  automating-safe-hands-off-deployments | 3ErTKQOTKc5NIw031UePBPxTQ6I
  amazons-approach-to-high-availability-deployment | 3F087SyGBr7uIRtrGQDJC6trKA8
  ensuring-rollback-safety-during-deployments | 3F04j2yRAAMBuPSPs50xwXZqg01
  amazons-approach-to-automated-software-and-systems-testing | 3F07fTC9nQCkhqCTP5vIzgyOcIH
  amazons-approach-to-security-during-development | 3F07JXrYkwtKDhPgoUbI0UAA0Zf
  building-dashboards-for-operational-visibility | 3Ev2iw3R3ahQOM8BT4OUR0WP51z
  operational-excellence-at-amazon | 3Ev4irLmkHOBR3BhODX2vuE0Syf
  hands-off-automating-continuous-delivery-pipelines-at-amazon | 3Ev3Nho3q1Cs04EZUVB1ckhNJWL
  my-cicd-pipeline-is-my-release-captain | 3Ev3XnnYuuBhlgnywbbVFzwibm1
  going-faster-with-continuous-delivery | 3F08Mhh186qOa4VhG19egs06NJa

NOTE: two articles cross-referenced from inside the ones already read are NOT in the
30-item catalogue and appear to be retired or hosted elsewhere — 'Caching challenges and
strategies' and 'Static stability using Availability Zones'. Do not keep hunting the index
for them; they are not there. Everything else previously listed as 'named but missing' has
now been located and is in the UNREAD list above.

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

STRANDS DOC URLS — FOUND (seventh run). Three earlier runs 404'd on guessed paths. The
working base is https://strandsagents.com/docs/... (NOT /latest/..., which 404s):
  https://strandsagents.com/docs/user-guide/concepts/agents/conversation-management/  (READ)
  https://strandsagents.com/docs/api/python/strands.agent.conversation_manager.conversation_manager/
  https://strandsagents.com/docs/api/python/strands.agent.agent/
The sdk-python GitHub README is marketing-level and yielded nothing — go straight to /docs.
Still unread there: Swarm / Graph / Agent-as-Tool multi-agent patterns, session persistence.

YIELD RANKING as of the seventh run — spend the budget in this order:
  1. builder.aws.com Builders' Library — still the best seam in the pack by a wide margin.
     Two runs, 8 articles, 33 facts. 21 of 30 remain unread and the catalogue is now fully
     enumerated above, so there is zero discovery cost. Pre-LLM distributed systems material
     that maps directly onto agent reliability. The five reliability titles at the top of the
     UNREAD list are the highest-value remaining items in the entire pack.
  2. anthropic.com/engineering — still strong. Read so far: advanced-tool-use,
     managed-agents, demystifying-evals-for-ai-agents, effective-harnesses-for-long-running-
     agents, claude-think-tool, claude-code-sandboxing, harness-design-long-running-apps,
     infrastructure-noise, claude-code-auto-mode, equipping-agents-for-the-real-world-with-
     agent-skills. STILL UNREAD: how-we-contain-claude, april-23-postmortem,
     eval-awareness-browsecomp, building-c-compiler, AI-resistant-technical-evaluations,
     a-postmortem-of-three-recent-issues, contextual-retrieval, swe-bench-sonnet,
     desktop-extensions.
  3. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread
     TECHNICAL posts: coding-agents-101-the-art-of-actually-getting-things-done, swe-grep,
     blockdiff, devin-annual-performance-review-2025, evaluating-coding-agents,
     making-fable-cheaper-than-opus, devin-fusion, swe-1-7,
     measuring-open-source-model-trustworthiness, introducing-devin-security-swarm.
     Skip partnership/funding/office/acquisition posts — about half the feed, and ALL THREE
     of the newest posts as of 2026-07-27 (interaction, cognition-doe-genesis-mission,
     welcoming-tierzero) are in that category.
  4. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
  5. sourcegraph.com/blog — real measurements (n=1,281 agent runs), not opinions. Unread:
     code-finder-fast-code-search-for-agents (Jul 23 2026),
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone.
  6. latent.space/archive — interview format but yields thresholds. Unread: /p/modal2026,
     /p/gray-swan, /p/aiewf26trends.
  7. simonwillison.net/tags/llms/ — high volume, mostly link-blogging; scan for incidents and
     security, skip model-release commentary. Unread: the-first-known-runaway-ai-agent
     (Jul 23), thomas-ptacek (sandbox escapes), bad-codex-bug (file deletions), relay-market
     (Jul 26, token-reseller fraud).
  8. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
  9. embracethered.com/blog — low volume, high value, security only.
 10. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.

dead or unreadable, do not keep re-fetching blind:
  block.github.io/goose -> goose-docs.ai (old host serves only a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... (see STRANDS DOC URLS above).
  NOTE: builder.aws.com and the Vectara leaderboard were BOTH listed here and neither was
    ever dead. See the warning at the top of this file before adding anything to this list.

checked and low-yield for this pack (do not deprioritise permanently, but do not lead with
them): research.google/blog — recent output is health/quantum/diffusion, nothing on agents,
tools, or evals. microsoft.com/en-us/security/blog — one good agent-identity post, otherwise
threat intel unrelated to building agents. TIER 6 GITHUB READMEs (checked seventh run) —
microsoft/autogen, NirDiamant/GenAI_Agents, strands-agents/sdk-python all return
catalogue-level or marketing-level README text that is below this pack's altitude bar. The
ONE thing worth having from that sweep was autogen's maintenance-mode notice. Do not spend
more budget on tier-6 repo READMEs; if a repo matters, go to its DOCS site instead. Still
unattempted from tier 6: anthropics/claude-cookbooks, NirDiamant/RAG_Techniques,
microsoft/semantic-kernel, and the x1xhlol individual prompt files.
