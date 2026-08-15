---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Recurring crawl sources

*** THIS SLOT IS THE SOURCE LIST AND NOTHING ELSE. ***
What belongs here: URLs to crawl, and URL catalogues that were expensive to discover.
What does NOT belong here, and where it went (split 2026-08-11):
  how to fetch a gated/blocked host  -> .knomit/jobs/agentic-engineering/fetch-routes.md
  standing rules for the job         -> spec.md on disk (Appendix S). Not writable from here, by design.
  per-run status, queues, rankings   -> crawl-state.md, whose revision history is the record.
Before this split, 93% of this file was not sources: 28 URL lines out of 436.
READ/UNREAD markers below are provenance hints only. The AUTHORITATIVE record of what has been
crawled is the ALREADY_CRAWLED union assembled by walking crawl-state's revisions.

=== RECURRING FEEDS — swept every run when days have passed ===

https://www.anthropic.com/engineering
https://www.anthropic.com/news/                                          <- ADDED 14th run (postmortems live here, NOT /engineering)
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
https://modelcontextprotocol.io/specification/2026-07-28/deprecated      <- ADDED 12th run (cheap tripwire)
https://owasp-agentic-ai-security-incidents.lovable.app/                 <- ADDED 12th run (ASI incidents tracker)
https://www.aisi.gov.uk/blog/                                            <- ADDED 13th run (RANK 2)
https://openai.com/index/                                                <- ADDED 13th run (RANK 2)
https://developers.openai.com/api/docs/guides/                           <- ADDED 15th run. The API guides tree is
    a DIFFERENT source from openai.com/index and from the cookbook, it is plain-WebFetch-readable (no browser,
    no 403), and agent-builder-safety was found there unread. Scan it for new guides, not just the two known ones.
https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification
    <- ADDED 16th run. THE MCP TRIPWIRE, ZERO-FETCH FORM, AND IT WORKS WHEN THE WEBSITE DOES NOT.
    Returns one directory per released revision; a new revision is a new directory. On 2026-08-12
    modelcontextprotocol.io refused connections all run and this route answered first try. Prefer it
    over the rendered /specification/versioning page. Route details in fetch-routes route 3.
https://blog.redwoodresearch.org/                                        <- ADDED 17th run, LOW VOLUME, WATCH ONLY.
    Redwood Research published a podcast episode on the OpenAI/Hugging Face incident, and Redwood +
    METR are contracted to publish the JOINT independent assessment of that incident (not landed as
    of 2026-08-15). This feed is where half of that lands. Caveat: podcast/talk write-ups are the
    weakest source form this pack uses — see the simonwillison talk-summary caveat. Prefer the joint
    blog when it appears; do not mine podcast summaries for quotable claims.
https://github.com/vectara/hallucination-leaderboard
https://huggingface.co/blog

=== SOURCE INVENTORIES — catalogues that cost real fetches to enumerate ===

*** OWASP GenAI — RESOURCE SLUG + DOWNLOAD ID MAP ***
The PDF lives at https://genai.owasp.org/download/<id>/?tmstv=<epoch>, and the id is NOT guessable.
Get it by WebFetching the /resource/<slug>/ page and asking for the download URL, then curl it with -A
(see fetch-routes). The tmstv token does not expire — 1754459367 was recorded 2026-08-05 and still
worked 2026-08-15, ten days later.
Ids captured so far:
  50592  State of Agentic AI Security and Governance 2.01   (139pp, read 12th run) tmstv=1754459367
         ^ RE-DOWNLOADED 18th run for the staleness pass. pdfinfo: 139 pages, CreationDate 2026-06-01.
  56857  OWASP GenAI LLM Top 10 2026                        (122pp, read 13th run) tmstv=1785822482
  49059  Securing Agentic Applications Guide 1.0            (July 2025, read 15th run) tmstv=1753666640
  46950  Multi-Agentic System Threat Modeling Guide v1.0    (April 2025, read 15th run) tmstv=1745459605
  47278  Agent Name Service (ANS) v1.0                      (14 May 2025, read 16th run) tmstv=1747275418
         Resource slug CONTAINS A TYPO and is unguessable — note "al" for "AI":
         /resource/agent-name-service-ans-for-secure-al-agent-discovery-v1-0/
  52117  OWASP Top 10 for Agentic Applications 2026         READ 17th + 18th run. 3137 lines, 1.2MB.
         https://genai.owasp.org/download/52117/?tmstv=1765059207   (labelled "Version 2026", Dec 2025)
         Resource slug: /resource/owasp-top-10-for-agentic-applications-for-2026/
         MINED SO FAR: the ten entries + T-taxonomy mappings, the per-entry disambiguation prose,
         "Least-Agency", Appendix D's incident tracker counted by frequency, and (18th run) the
         named mitigation PATTERNS — intent capsule (ASI01 mit. 5), Intent Gate PEP/PDP (ASI02
         mit. 4), adaptive tool budgeting (ASI02 mit. 5), semantic firewalls (ASI02 mit. 7),
         dry-run diff preview (ASI02 mit. 2). Entry line ranges in the extract: ASI01 476-578,
         ASI02 579 onward; Appendix D 2138-2750; Acknowledgements ~2851 (EXCLUDE from any count —
         it carries an ASI01-ASI10 roster that adds a phantom tag to every entry).
         *** STILL UNMINED IN THIS PDF: ***
           - per-entry "Prevention and Mitigation Guidelines" for ASI03..ASI07 and ASI09. ASI01,
             ASI02, ASI08 and ASI10 are now done.
           - Appendix B (relationship to OWASP CycloneDX and AIBOM) — unread.
           - Appendix C (mapping to the Non-Human Identities Top 10 2025) — unread; extract line
             1882 onward, table at 1886. The NHI Top 10 is not otherwise represented in this pack,
             and 069468bb already covers the NHI-vs-agent-identity distinction, so this pairs well.
           - Appendix D's per-incident detail. Counted, not read. ~21 incidents Mar-Oct 2025.
  54627  AIUC-1 Crosswalks (OWASP Top 10 for Agentic Applications)  *** ID CAPTURED 18th run. ***
         https://genai.owasp.org/download/54627/?tmstv=1779726713
         /resource/aiuc-1-crosswalks-owasp-top-10-for-agentic-applications/
         pdfinfo: 55 pages, CreationDate 2026-05-25. Read 11th run (3 facts + 1 upd); ALL THREE
         RE-VERIFIED 18th run against this PDF — 07eec7ff, 2d060289, 1719fe66. Document unchanged.
         The 11th run never recorded the id, so the 18th had to re-resolve it. It is here now.
         UNMINED: Part A / Part B per-requirement tables in full (they extract row-faithfully — see
         fetch-routes), and Appendix A/B.
  54018  AI Security Solutions Landscape for AI and Agentic Red Teaming Q2 2026  *** ID CAPTURED 18th. ***
         https://genai.owasp.org/download/54018/?tmstv=1775767894
         /resource/ai-security-solutions-landscape-for-ai-and-agentic-red-teaming-q2-2026/
         pdfinfo: 15 pages, CreationDate 2026-04-09. Read 11th run (1 fact, 43155c66); RE-VERIFIED
         18th run, unchanged. Vendor-sponsored market map — low remaining yield, do not re-mine.

*** OPENAI /index/ POST CATALOGUE — enumerated by WebSearch, 17th run ***
openai.com/index 403s to WebFetch; all of these need the browser (fetch-routes route 1). Slugs are
EXACT, taken from search results and from "Keep reading" footers — do not re-derive them.
  READ: /index/hugging-face-model-evaluation-security-incident/   (17th run re-read; the PRIMARY
        account of the HF incident, incl. the Jul 28 and Jul 29 updates. Already cited by bcbf13c2.)
  READ: /index/the-next-evolution-of-the-agents-sdk/              (17th run; Apr 15 2026. Framework
        post — one design decision harvested into c436422a, rest is product copy. Do not re-mine.)
  READ: /index/introducing-aardvark/                              *** 18th run. Oct 30 2025. ***
        The agentic security researcher. 1 fact (30543305): whole-repo threat model as a durable
        artifact + commit-delta evaluation, explicit rejection of fuzzing/SCA, sandbox reproduction
        stage, Codex-generated/Aardvark-scanned patches, 92% recall (recall only, no precision).
        *** CARRIES A 2026-03-06 BANNER: Aardvark is now CODEX SECURITY, research preview. ***
        Follow-up target: the Codex Security post that banner links to — NOT yet fetched.
  UNREAD, ranked:
    /index/unlocking-self-improvement-gpt-red/   <- NOW TOP. "GPT-Red: Unlocking Self-Improvement for
                                             Robustness". A METHOD post — prefer over framework posts.
    the CODEX SECURITY post (slug unknown)  <- linked from the Aardvark banner; resolve with
                                             WebSearch allowed_domains=[openai.com] before fetching.
    /index/responding-next-frontier-critical-cyber-capabilities/  <- CORRECT SLUG, resolved 17th run.
                                             ALREADY CITED by bcbf13c2 and ee458c93 — so it HAS been
                                             read; treat as done unless re-verifying.
    /index/putting-frontier-cyber-models-in-more-trusted-hands/   (Aug 10 2026)
    /index/expanding-daybreak-cyber-defense-window-narrows/       <- SLUG INFERRED and PROBABLY WRONG:
                                             facts 2d7219c8, 8193c07b and ee458c93 all cite
                                             /index/expanding-daybreak-as-the-cyber-defense-window-narrows/
                                             (note "as-the"), which means that post is already READ.
    /index/patch-the-planet/              (Daybreak initiative for OSS maintainers; program/policy)
    /index/safety-alignment-long-horizon-models/
    /index/introducing-openai-presence/   (product)
    /index/trusted-access-for-cyber/, /index/scaling-trusted-access-for-cyber-defense/,
    /index/updating-our-preparedness-framework/   (governance; lower altitude)
  ALSO SPOTTED, product announcements, almost certainly below the bar — listed only so nobody spends
  a fetch discovering that: "Previewing Ultrafast mode: GPT-5.6 Sol at up to 14X the speed" (Aug 13),
  "Testing ads in ChatGPT" (Aug 11), "Daybreak models are now available on AWS" (Aug 11).
  CONFIRMED 18th run: those same three are what the "Keep reading" footer returns from a 2025 post,
  so the footer is a RECENCY feed, not a related-posts feed. Do not expect siblings from it.

*** COUNTER-POSITION TARGET — READ 16th RUN, keep for provenance ***
https://arxiv.org/abs/2508.09815 (PDF: https://arxiv.org/pdf/2508.09815) — Krawiecka & Schroeder de Witt,
  "Extending the OWASP Multi-Agentic System Threat Modeling Guide". 8pp, downloads with plain curl -A.
  READ 16th run: 3 facts + 1 update to c02ac546. Sixteen proposed threat classes tabulated against
  OWASP coverage. NOTE ITS MODALITY — anticipatory, no measurements, no incidents; every fact written
  from it says so. Its reference list is a small unmined catalogue of multi-agent eval work:
  NetSafe (arXiv 2410.15686, topological safety of agent networks), TrustAgent (EMNLP Findings 2024),
  chaos engineering for LLM MAS (arXiv 2505.03096), The Traitors (arXiv 2505.12923, deception/trust
  in MAS simulations), Open Challenges in Multi-Agent Security (arXiv 2505.02077). NetSafe and the
  chaos-engineering paper look closest to this pack's bar; the rest are game-simulation benchmarks.

*** AWS BUILDERS' LIBRARY — COMPLETE ENUMERATION (30 of 30, no more pagination) ***
URLs are opaque content IDs, NOT guessable from titles: https://builder.aws.com/content/<ID>/<slug>

READ (16 of 30):
  timeouts-retries-and-backoff-with-jitter | 3EumjoZascWd1oZiEgL8ORlv3qE            (4 facts)
  using-dependency-isolation-to-contain-concurrency-overload | 3EuxuD6bWtQ6gEp9FaKQfd3Z2AM (7)
  fairness-in-multi-tenant-systems | 3Eupj3d2bo4fEvlzYbICMZNhQ3B                   (5 facts)
  workload-isolation-using-shuffle-sharding | 3F06NpJ8YeoIGP8VHTw4n81pFn8          (1 fact)
  minimizing-correlated-failures-in-distributed-systems | 3Ev2H7t3l2eZa9xBXiZcAjz12JK (3+1upd)
  challenges-with-distributed-systems | 3F08f7GPFiZMCgXD8gny6OjxR0Z               (2+1upd)
  implementing-health-checks | 3Ev53O39izHCtWLzp4XU6t8PC1O                         (5 facts)
  making-retries-safe-with-idempotent-apis | 3Ev0BENTyBr0XxzRk5FDZzgNYos           (3 facts)
  avoiding-fallback-in-distributed-systems | 3EuS9Sakq7L3VLQIF3qzfMfke1Y           (3 facts)
  using-load-shedding-to-avoid-overload | 3Eun1EEyX6p2e3VYNyRLSJzLuMV              (5+1upd)
  avoiding-insurmountable-queue-backlogs | 3EuRcgkTP1MI0c7zM8W6HL3WIqA             (6 facts)
  avoiding-overload-...-smaller-service-in-control | 3EukISjbJAGNdrxjKaN6RG0wlHG   (2 facts)
  reliability-constant-work-and-a-good-cup-of-coffee | 3F05oqNtNUWxHJ5r6L6I2HrH4rI (3 facts)
  instrumenting-distributed-systems-for-operational-visibility | 3EuxPBdIiiUhB5IK47p3O3fxhy7 (6+2upd)
  leader-election-in-distributed-systems | 3Ev0vH0hfkcUizISUWYTvHibtcp             (2 facts)
  resilience-lessons-from-the-lunch-rush | 3Ev17ZWA9QX88MmoaULAKevIR8H             (1 fact)

UNREAD (12) — reliability first, CI/CD last. Expect LOWER yield; 6 are CI/CD and deployment.
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

'Caching challenges and strategies' and 'Static stability using Availability Zones' are NOT in the
catalogue and appear retired. Static stability is covered inside smaller-service-in-control;
caching's failure modes inside constant-work and lunch-rush.
redirects folded in:
  cookbook.openai.com -> developers.openai.com/cookbook
  blog.langchain.dev  -> www.langchain.com/blog
  aws.amazon.com/builders-library -> builder.aws.com/learn/topics/builders-library
  www.latent.space -> www.latent.space/archive (bare domain serves only a subscribe wall)
  modelcontextprotocol.io/docs/concepts/tools -> /specification/2026-07-28/server/tools
    (VERIFIED 200 + redirect, 17th run. The 16th run recorded this URL as GONE; it is not.)

CORRECTED (fifth run): cognition slugs guessed from titles 404. Always pull
https://cognition.com/blog for exact slugs.
  'Coding Agents 101' = /blog/coding-agents-101-the-art-of-actually-getting-things-done
STRANDS DOC URLS — base is https://strandsagents.com/docs/... (NOT /latest/..., which 404s):
  .../user-guide/concepts/agents/conversation-management/  (READ; re-verified 15th run)
  .../api/python/strands.agent.conversation_manager.conversation_manager/   <- NEEDED. The 15th run found
     fact 714a540c attributing pin_first / proactive_compression parameters to the user-guide page, which
     does not document them. If those params are real they are here. Fetch before restoring them.
  .../api/python/strands.agent.agent/
Still unread: Swarm / Graph / Agent-as-Tool multi-agent patterns, session persistence.
NOTE (15th run): the Strands docs carry snake_case AND camelCase spellings side by side and document
some defaults for the TypeScript binding only. Do not record a default without recording its binding.

*** MCP SPECIFICATION — THE REPO IS THE SOURCE, AND SITE URLs DO NOT MAP TO REPO PATHS ***
github.com/modelcontextprotocol/modelcontextprotocol renders directly to modelcontextprotocol.io.
Enumerate with the recursive git-tree API and grep; NEVER build a repo path from an old site URL.
  site /specification/<rev>/...  -> repo docs/specification/<rev>/...
  site /docs/<rev>/...           -> repo docs/docs/<rev>/...
PAGE MOVES — CORRECTED 17th run, the 16th run's version was wrong. Full detail in fetch-routes route 3.
  security_best_practices: now at docs/docs/<rev>/tutorials/security/security_best_practices.mdx,
    and it exists for every revision, which is what makes revision-diffing possible.
  /docs/concepts/tools: NOT gone — it REDIRECTS to /specification/2026-07-28/server/tools. Its content
    lives at docs/specification/<rev>/server/tools.mdx, NOT at learn/server-concepts.mdx as the 16th
    run recorded (that page contains none of the tool-contract material; grepped and confirmed empty).
    Facts ee3bc7d3, ca3382bd and 46eeb374 all cite the old URL and were never actually broken; all
    three were re-verified against 2026-07-28 on the 17th run and now carry the canonical URL too.
*** AUTHORIZATION WAS ONE FILE AND IS NOW FOUR PAGES — ADDED 18th run. ***
  through 2025-11-25:  docs/specification/<rev>/basic/authorization.mdx        (single file, 708 lines)
  2026-07-28 + draft:  docs/specification/<rev>/basic/authorization/index.mdx
                       .../authorization/security-considerations.mdx
                       .../authorization/client-registration.mdx
                       .../authorization/authorization-server-discovery.mdx
  So a predecessor path built by substituting the revision date 404s. Resolve from tree.json.
  See fetch-routes 3b and 3c — the 404 body diffs as "entirely new" and will fabricate a version claim.
RELEASED REVISION DIRECTORIES as of 2026-08-15: 2024-11-05, 2025-03-26, 2025-06-18, 2025-11-25,
  2026-07-28, plus draft. Unchanged since the 11th run — EIGHT consecutive runs.

CLAUDE PLATFORM DOCS — the prompting page routes to PER-MODEL sub-pages (found 12th run):
  .../prompt-engineering/prompting-claude-opus-5    <- has a 'Controlling subagent spawning' section
  .../prompt-engineering/prompting-claude-opus-4-8
  .../prompt-engineering/prompting-claude-sonnet-5
  .../prompt-engineering/prompting-claude-fable-5
All four UNREAD. The general claude-4-best-practices page now covers Fable 5, Mythos 5, Opus 5,
4.8, 4.7, 4.6, Sonnet 5, Sonnet 4.6, Haiku 4.5 and is ~58KB — grep the persisted file, don't re-read.
AZURE ARCHITECTURE CENTER — prefix https://learn.microsoft.com/en-us/azure/architecture/ai-ml/
  .../guide/ai-agent-design-patterns                       (READ — c926c07b)
  .../guide/manage-foundation-models-lifecycle             (READ — updated 27652a82)
  .../guide/azure-openai-gateway-guide                     (READ — 2 facts + upd 5ad0fb45)
  .../guide/azure-openai-gateway-multi-backend             (READ — 4 facts + upd 27652a82)
  .../guide/azure-openai-gateway-monitoring                <- LAST of the gateway trio, UNREAD
  .../guide/rag/rag-solution-design-and-evaluation-guide   <- LARGEST unread block, plus:
      rag-preparation-phase, rag-chunking-phase, rag-enrichment-phase,
      rag-generate-embeddings, rag-information-retrieval, rag-llm-evaluation-phase
  .../guide/secure-multitenant-rag
  .../guide/genaiops-for-mlops
