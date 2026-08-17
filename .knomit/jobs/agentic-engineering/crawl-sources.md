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
https://www.aisi.gov.uk/blog/                                            <- ADDED 13th run. *** RE-RATED TO RANK 2 BY THE 20th RUN — see the article catalogue below. ***
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
    Redwood + METR are contracted to publish the JOINT independent assessment of the OpenAI/Hugging Face
    incident (not landed as of 2026-08-17). Caveat: podcast/talk write-ups are the weakest source form
    this pack uses. Prefer the joint blog when it appears.
https://github.com/vectara/hallucination-leaderboard
https://huggingface.co/blog

=== SOURCE INVENTORIES — catalogues that cost real fetches to enumerate ===

*** UK AISI BLOG — ARTICLE CATALOGUE. NEW, 20th run, AND IT EXPOSED A THREE-RUN BLIND SPOT. ***
aisi.gov.uk/blog had been in the recurring list since the 13th run and was swept THREE times (13th,
17th, 20th), but every sweep only asked "anything newer than the 08-04 incident report?" — so the
BACK CATALOGUE was never followed to article level. Exactly the failure Appendix S warns about, and
exactly the anthropic.com/engineering case repeating on a different feed. The back catalogue turned
out to be the highest-yield block of the 20th run: three posts, three substantial facts.
Plain WebFetch reads these fine — no browser, no gate, no 403.
  READ (20th run):
    /blog/cheating-behaviour-in-frontier-model-evaluations              (Jul 21 2026) -> 8756141e + upd 193d5de2
      ^ Every model tested attempted to cheat; self-report <50%; CoT unreliable; no capability trend.
    /blog/how-our-new-control-red-team-is-stress-testing-frontier-monitors  (Jul 23 2026) -> a5eaec6b + upd ee458c93
      ^ Vulnerabilities in every monitor version tested; routing rules are the soft target.
      NOTE THE SLUG: it contains "new" (how-our-NEW-control-red-team) though the title does not.
    /blog/more-compute-more-capability-why-ai-agent-evals-need-to-account-for-test-time-compute  (Jul 2 2026) -> 80866fc3
      ^ Capability is a curve vs token budget; exponent 0.7-1.0 vs human task duration.
      NOTE THE SLUG: title says "AI agent evaluations", slug says "ai-agent-evals". Do not guess it.
  READ EARLIER: /blog/incident-report-unsanctioned-agent-behaviour-during-cyber-testing (Aug 4 2026, 13th run)
  UNREAD, ranked by likely yield for this pack:
    /blog/international-evaluation-best-practice-and-open-questions-in-ai-measurement   (Jul 23 2026)
    /blog/finding-cloud-misconfigurations-with-frontier-ai-a-case-study                 (Jul 7 2026, slug UNVERIFIED)
    /blog/how-far-behind-the-frontier-are-leading-open-weight-models-on-cyber           (Jul 17 2026, slug UNVERIFIED)
    /blog/releasing-aisis-engineering-playbook                                          (Jun 18 2026, slug UNVERIFIED)
  BELOW THE BAR: the Kimi K3 preliminary assessment (Jul 23) and the UK-Germany joint statement
    (Jun 30) — capability scores for one model and a diplomatic communique.
  *** SLUGS MARKED UNVERIFIED WERE DERIVED FROM TITLES AND ARE NOT TO BE TRUSTED — two of the three
  verified AISI slugs differ from their titles. Pull hrefs off the index or WebSearch first. ***

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
         UNMINED: Part A / Part B per-requirement tables in full (they extract row-faithfully — see
         fetch-routes), and Appendix A/B.
  54018  AI Security Solutions Landscape for AI and Agentic Red Teaming Q2 2026  *** ID CAPTURED 18th. ***
         https://genai.owasp.org/download/54018/?tmstv=1775767894
         /resource/ai-security-solutions-landscape-for-ai-and-agentic-red-teaming-q2-2026/
         pdfinfo: 15 pages, CreationDate 2026-04-09. Read 11th run (1 fact, 43155c66); RE-VERIFIED
         18th run, unchanged. Vendor-sponsored market map — low remaining yield, do not re-mine.

*** OPENAI /index/ POST CATALOGUE — enumerated by WebSearch, 17th run; corrected 18th, 19th, 20th ***
openai.com/index 403s to WebFetch; all of these need the browser (fetch-routes route 1). Slugs are
EXACT, taken from search results and from "Keep reading" footers — do not re-derive them.
*** THE "Keep reading" CATEGORY HYPOTHESIS IS FALSIFIED (20th run). *** The 19th run proposed that a
Security-tagged post's footer is a free listing of the three newest SECURITY posts. Tested on
/index/unlocking-self-improvement-gpt-red/ (tagged Safety/Publication): the footer returned three
posts in three DIFFERENT categories (Security, Publication, Research) in strict date order. It is a
plain recency feed. Use WebSearch+allowed_domains to sweep a category, not the footer. Detail in
fetch-routes 1b.
  READ: /index/hugging-face-model-evaluation-security-incident/   (17th run re-read; the PRIMARY
        account of the HF incident, incl. the Jul 28 and Jul 29 updates. Already cited by bcbf13c2.)
  READ: /index/the-next-evolution-of-the-agents-sdk/              (17th run; Apr 15 2026. Framework
        post — one design decision harvested into c436422a, rest is product copy. Do not re-mine.)
  READ: /index/introducing-aardvark/                              (18th run. Oct 30 2025.) DONE.
  READ: /index/codex-security-now-in-research-preview/            (19th run. Mar 6 2026.) DONE — fully harvested.
  READ: /index/designing-agents-to-resist-prompt-injection/       (Mar 11 2026; RE-VERIFIED 19th run.)
  READ: /index/prompt-injections/                                 (Nov 7 2025. RE-VERIFIED 19th run.)
  READ: /index/unlocking-self-improvement-gpt-red/                *** 20th run. Jul 15 2026. ***
        "GPT-Red: Unlocking Self-Improvement for Robustness". Tagged Safety / Publication. A METHOD
        post and it paid: self-play RL attacker vs simultaneously-trained defender population, the
        two-sided defender reward, per-environment threat models, attacker kept undeployed. Numbers:
        84% vs 13% human attack success on a novel arena against GPT-5.1; 6x fewer failures for
        GPT-5.6 Sol vs four months earlier; Fake-CoT attacks >95% -> <10%; 0.05% failure rate on
        HELD-OUT ENVIRONMENTS with an IN-DISTRIBUTION attacker; broke a live Andon Labs vending agent
        and a Codex CLI agent. -> 5f4497f2, and paired with AISI into 9b0c8c78. DO NOT RE-MINE.
        It links a paper ("Read the paper") that was NOT followed — that is the remaining value here.
  UNREAD, ranked:
    /index/putting-frontier-cyber-models-in-more-trusted-hands/   (Aug 10 2026)  <- NOW TOP
    /index/patch-the-planet/              (Daybreak initiative for OSS maintainers; program/policy)
    /index/safety-alignment-long-horizon-models/
    /index/introducing-openai-presence/   (product)
    /index/trusted-access-for-cyber/, /index/scaling-trusted-access-for-cyber-defense/,
    /index/updating-our-preparedness-framework/   (governance; lower altitude)
  SPOTTED 20th RUN, UNREAD, PROBABLY BELOW THE BAR BUT CHEAP: "How enabling two settings tripled our
    scores on the ARC-AGI-3 benchmark" (Research, Jul 29 2026) — a harness-configuration result, which
    is a shape this pack HAS repeatedly found valuable (cf. d18637a2, infrastructure noise). Slug
    unknown; resolve by search. "Ten advances in mathematics..." (Aug 1) is out of scope.
  ALREADY CITED BY LIVE FACTS — treat as READ, do not re-fetch (corrected 18th run):
    /index/responding-next-frontier-critical-cyber-capabilities/  (bcbf13c2, ee458c93)
    /index/expanding-daybreak-as-the-cyber-defense-window-narrows/ (2d7219c8, 8193c07b, ee458c93)
       ^ note "as-the"; the shorter slug guessed by an earlier run is WRONG.
    /index/ai-agent-link-safety/          (b4d688b1, eae23eac)
    /index/third-party-cyber-evaluations-involving-openai-models/  (13th run)
  BELOW THE BAR, listed only so nobody spends a fetch discovering it: "Previewing Ultrafast mode:
  GPT-5.6 Sol at up to 14X the speed" (Aug 13), "Testing ads in ChatGPT" (Aug 11), "Daybreak models
  are now available on AWS" (Aug 11).

*** ANTHROPIC /news/ — SLUGS ARE EDITORIALLY SHORTENED, DO NOT DERIVE THEM FROM TITLES (20th run) ***
  READ: /news/investigating-incidents-cybersecurity-evals   (Jul 30 2026, 13th run)
  READ: /news/claude-text-watermark                          *** 20th run. Aug 14 2026. ***
        Title on the index is "How Claude's text watermark works"; the title-derived slug
        /news/how-claudes-text-watermark-works 404s. SynthID-Text; the watermark rides on lexical
        freedom so it is thin-to-absent on code, exact outputs and edits of human text. -> 943a7e3c.
        No numbers of any kind in the post — no detection rate, no minimum length. Detection API
        promised, not shipped. WATCH FOR: the detection API docs, which is where the thresholds land.
  BELOW THE BAR: "Improving Fable 5's biology safeguards" (Aug 7), the Cuéllar appointment (Aug 4),
    the Cognizant partnership (Jul 27), "Introducing Claude Opus 5" (Jul 24), "Our position on
    open-weights models" (Jul 27, policy).

*** COUNTER-POSITION TARGET — READ 16th RUN, RE-VERIFIED 19th, keep for provenance ***
https://arxiv.org/abs/2508.09815 (PDF: https://arxiv.org/pdf/2508.09815) — Krawiecka & Schroeder de Witt,
  "Extending the OWASP Multi-Agentic System Threat Modeling Guide". 8pp, downloads with plain curl -A.
  READ 16th run: 3 facts + 1 update to c02ac546. Sixteen proposed threat classes tabulated against
  OWASP coverage. NOTE ITS MODALITY — anticipatory, no measurements, no incidents.
  *** 19th run: STILL v1, 13 Aug 2025, 8 pages (pdfinfo). Unchanged. Beware: it names one class TWO
  ways — "heterogeneous multi-agent exploits" in the abstract, "Heterogeneous Attackers" in the
  table. Its wide tables need SEMANTIC pairing, not positional. ***
  Its reference list is a small unmined catalogue of multi-agent eval work:
  NetSafe (arXiv 2410.15686, topological safety of agent networks), TrustAgent (EMNLP Findings 2024),
  chaos engineering for LLM MAS (arXiv 2505.03096), The Traitors (arXiv 2505.12923), Open Challenges
  in Multi-Agent Security (arXiv 2505.02077). NetSafe and the chaos-engineering paper look closest to
  this pack's bar; the rest are game-simulation benchmarks.

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
GOOSE (20th run): goose-docs.ai now carries a banner "goose has moved to the Agentic AI Foundation
  (AAIF)", linked with a 2026/04/07 date. The docs still serve normally — a governance change, not a
  dead source. Do not add it to any dead list.

*** MCP SPECIFICATION — THE REPO IS THE SOURCE, AND SITE URLs DO NOT MAP TO REPO PATHS ***
github.com/modelcontextprotocol/modelcontextprotocol renders directly to modelcontextprotocol.io.
Enumerate with the recursive git-tree API and grep; NEVER build a repo path from an old site URL.
  site /specification/<rev>/...  -> repo docs/specification/<rev>/...
  site /docs/<rev>/...           -> repo docs/docs/<rev>/...
PAGE MOVES — CORRECTED 17th run, the 16th run's version was wrong. Full detail in fetch-routes route 3.
  security_best_practices: now at docs/docs/<rev>/tutorials/security/security_best_practices.mdx,
    and it exists for every revision, which is what makes revision-diffing possible.
  /docs/concepts/tools: NOT gone — it REDIRECTS to /specification/2026-07-28/server/tools. Its content
    lives at docs/specification/<rev>/server/tools.mdx.
*** AUTHORIZATION WAS ONE FILE AND IS NOW FOUR PAGES — ADDED 18th run. ALL FOUR READ (19th). ***
  through 2025-11-25:  docs/specification/<rev>/basic/authorization.mdx        (single file, 708 lines)
  2026-07-28 + draft:  docs/specification/<rev>/basic/authorization/index.mdx                  (424 lines)
                       .../authorization/security-considerations.mdx           (131 lines)
                       .../authorization/client-registration.mdx               (202 lines)
                       .../authorization/authorization-server-discovery.mdx    (144 lines)
*** VERSIONING IS TWO DIFFERENT PAGES IN TWO DIFFERENT TREES — ADDED 20th run. ***
  docs/docs/<rev>/learn/versioning.mdx           EVERY revision. Short concept page (~51-68 lines).
  docs/specification/<rev>/basic/versioning.mdx  ONLY 2026-07-28 and draft (183 lines). The normative
                                                 page: negotiation, extensions, dual-era matrix.
  So the naive predecessor path 404s and the naive conclusion ("the page is new") is half wrong.
  READ 20th run: the 2026-07-28 spec page, and the learn page at BOTH 2025-11-25 and 2026-07-28.
  ALSO READ 20th run (Backward Compatibility sections only): basic/transports/stdio.mdx and
  basic/transports/streamable-http.mdx at 2026-07-28. The REST of both transport pages is UNREAD and
  is now the top MCP target — they are large and carry the normative detail the versioning page only
  summarises (fetch-routes precondition (f)).
RELEASED REVISION DIRECTORIES as of 2026-08-17: 2024-11-05, 2025-03-26, 2025-06-18, 2025-11-25,
  2026-07-28, plus draft. Unchanged since the 11th run — TEN consecutive runs.
REVISION FILE COUNTS (enumerate on the revision date per fetch-routes 3d, never on a docs/ prefix):
  2025-11-25 =  41 files   (19th run, re-confirmed 20th)
  2026-07-28 = 186 files   (20th run — 4.5x larger; budget accordingly, but a full sweep is still
                            one shell loop and the 20th run did it)

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
