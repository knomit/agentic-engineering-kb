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
https://huggingface.co/blog

*** MCP PROTOCOL REVISION MOVED — 2025-11-25 IS SUPERSEDED BY 2026-07-28 (found eleventh run) ***
The versioning page now names **2026-07-28** as Current. This is a LARGE backwards-incompatible
revision, not a point update. Appendix A on disk still says 'MCP's current revision is
2025-11-25' — THAT LINE IS NOW WRONG and a human should fix the disk copy.
What changed (all recorded in the kb): protocol sessions and Mcp-Session-Id REMOVED; the
initialize/initialized handshake REMOVED (version + capabilities now per-request in _meta);
mandatory server/discover RPC; SSE resumability REMOVED; ping / logging/setLevel /
notifications/roots/list_changed REMOVED; tasks moved OUT of core into extension
io.modelcontextprotocol/tasks; server-initiated requests replaced by Multi Round-Trip Requests;
Roots, Sampling and Logging DEPRECATED; OAuth Dynamic Client Registration deprecated in favour
of Client ID Metadata Documents; error codes renumbered with a new allocation policy.
The sixth run's lesson held again: GREP THE REFS, NOT JUST THE BODIES. Facts updated this run:
031dab74, f89c1d7a, b471f9ef, 46eeb374, 62312b79 (ref repoint), 62c9a78b (version pin).
STILL UNREAD in this revision and worth a future fetch: /specification/2026-07-28/basic/
authorization/client-registration (CIMD), .../basic/patterns/mrtr, .../deprecated (the registry),
and /docs/extensions/overview. Also unread: the AgentCore Gateway post is a useful
second-source read on the same revision — aws.amazon.com/blogs/machine-learning/
how-agentcore-gateway-supports-the-mcp-2026-07-28-spec/ (READ this run).
WATCH: the versioning page remains the cheapest tripwire in the pack. Check it EVERY run.

*** FOUR RECURRING FEEDS HAD NEVER BEEN SWEPT IN TEN RUNS — FOUND AND FIXED, ELEVENTH RUN ***
This is the exact failure the job description warns about: a URL sitting in the recurring list
is NOT evidence anyone followed it. Cross-referencing the list against every crawl-state
revision showed four indexes with ZERO article-level fetches ever:
  microsoft.com/en-us/research/blog/  — never swept. HIGH YIELD. Surfaced SkillOpt (fact
    f0fdc77a, +23.5 pts absolute, 52/52 cells) and Memora (fact eaacbe8a). This is a real seam.
  aws.amazon.com/blogs/machine-learning/ — never swept. Surfaced the MCP 2026-07-28 spec change
    above, which is the single most consequential finding of the run. High volume, heavily
    product-marketing, but AgentCore/Bedrock posts track spec changes early. WORTH KEEPING.
  www.latent.space/archive — the bare domain was fetched (4th run, subscribe wall) and ONE
    article was read (5th run), but the ARCHIVE INDEX had never been swept. Swept this run;
    the newest post (ontologies-agentic-systems) is discussion-level with no numbers and no
    failure conditions — BELOW THE BAR, not written up. Still unread: /p/aiewf26trends,
    /p/modal2026, /p/poolside, /p/chatgpt-work.
  genai.owasp.org/ — the init run fetched three DEEP links but never the index. Swept this run.
    See the PDF blocker below.
GENERALISE THIS: before trusting any recurring source as 'up to date', check the history for an
ARTICLE-LEVEL fetch from it, not merely a mention. Four of twenty-one were phantoms.

*** OWASP RESOURCES ARE GATED PDFs — DO NOT SPEND REPEATED FETCHES (eleventh run) ***
genai.owasp.org/ index reads fine and enumerates resources, but the substantive reports sit
behind download links as PDFs, and there is no PDF renderer in this session (same failure mode
as the OpenAI practical-guide PDF that Appendix A already tells us to skip). Landing pages
carry only a title, date and one-line description.
Named and UNREAD for this reason: 'State of Agentic AI Security and Governance 2.01' (Jun 2026),
'AIUC-1 Crosswalks OWASP Top 10 For Agentic Applications' (May 2026), 'AI Security Solutions
Landscape for AI and Agentic Red Teaming Q2 2026' (Apr 2026).
HTML blog posts on the same site DO read and are the way in. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06 memory/context poisoning)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-...

*** kb/principles/** IS READ-ONLY TO JOBS — FOUND THE TENTH RUN, AFFECTS THE STALENESS PASS ***
knomit_update on a fact under kb/principles/ fails with:
    validation "must-have-designer-entity" at principles: principles must be authored via
    /knomit-principle (entities must include 'designer')
Pipeline-minted synthesis facts (origin: distilled or discovered) live under kb/principles/ and
legitimately have no 'designer' entity. Do NOT add one to get past the validator — it would
falsely assert designer authorship, and origin is immutable, so there is no honest fix from
inside a job. Affected: 1feacc9e, 2c0e8e7c, b9b45ff5, 0f260eea, 6ec9b2b6, 00d3ef19, 28ba65db,
c2f12069. You can READ and verify these but cannot record the result. PREFER OTHER TOPICS.
THIS ALSO MAKES THE REF-COMPLIANCE ISSUE BELOW UNFIXABLE, not merely unflagged.

*** SPEC-COMPLIANCE ISSUE, for a human to decide ***
Synthesis facts minted by the discovery/distill pipelines carry only LOCAL refs and no external
URL — e.g. kb/principles/ai/rag/evaluation/28ba65db, kb/principles/ai/agents/architecture/
c2f12069. The spec says every fact MUST carry at least one URL in refs. Their grounding is real
(it flows through the local refs), so this is arguably fine for synthesis, but the spec has no
such carve-out. The tenth run tried to fix it and was REJECTED by the designer-entity validator.
Either the spec needs the carve-out, or the pipelines must propagate external refs at mint time,
or kb/principles/ must accept job edits to pipeline-origin facts.
RELATED, and this one IS job-fixable: ordinary facts can also have refs MISFILED. The eleventh
run found c99ec745 carrying an external GitHub URL inside refs.local. Re-sending the full refs
list as external corrected it. Worth spot-checking during staleness passes.

*** READ THIS FIRST: 'JS-RENDERED, UNREADABLE' VERDICTS IN THIS PACK ARE UNRELIABLE ***
Two sources were written off as unreachable and turned out not to be.
  builder.aws.com — recorded dead by three runs. The browser reads it fine (method below).
  Vectara hallucination leaderboard — the canonical source is the GitHub README at
    github.com/vectara/hallucination-leaderboard, server-rendered, plain WebFetch.
Before recording ANY source as dead: (1) look for a server-rendered canonical mirror — GitHub
README, raw file, RSS/Atom feed, archive path; (2) check whether the claude-in-chrome browser
tools are loadable. A GATED PDF (OWASP above) is a different and genuine blocker — no browser
helps, because the content is not HTML at all.

Browser method, works first try, no clicking or waiting:
    mcp__claude-in-chrome__navigate {url}        -> returns a tabId
    mcp__claude-in-chrome__get_page_text {tabId} -> full article text
CAVEAT: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Intermittent across runs (6th: every time; 7th and
9th: never; 8th: once). Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index use mcp__claude-in-chrome__javascript_tool with a
querySelectorAll expression — mcp__claude-in-chrome__find returns element refs but NOT hrefs.
NOTE: large learn.microsoft.com pages exceed WebFetch's inline limit and are persisted to a file
on disk; just Read the path returned. Ask a NARROW prompt to keep the answer inline instead.
Likewise a large knomit_query result can exceed the tool-result limit — lower `limit`, or filter,
rather than trying to read the spill file (its lines are too long for Read's chunking).

*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY (ninth run) ***
Confirmed video-only, no prose body, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Publication date does not predict it. Budget one cheap fetch per article and abandon immediately
if the text ends right after the byline.

*** AWS BUILDERS' LIBRARY — COMPLETE ENUMERATION (30 of 30, no more pagination) ***
URLs are opaque content IDs, NOT guessable from titles. Form as:
    https://builder.aws.com/content/<ID>/<slug>

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

UNREAD (12) — reliability first, CI/CD last. Expect LOWER yield: 6 of these are CI/CD and
deployment, further from this pack's centre.
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

'Caching challenges and strategies' and 'Static stability using Availability Zones' are NOT in
the catalogue and appear retired. Do not hunt them. Static stability is covered inside
smaller-service-in-control; caching's failure modes inside constant-work and lunch-rush.

redirects folded in so future runs stop paying a round-trip:
  cookbook.openai.com -> developers.openai.com/cookbook
  blog.langchain.dev  -> www.langchain.com/blog
  aws.amazon.com/builders-library -> builder.aws.com/learn/topics/builders-library
  www.latent.space -> www.latent.space/archive (bare domain serves only a subscribe wall)

CORRECTED (fifth run): cognition slugs guessed from titles 404. Always pull
https://cognition.com/blog for exact slugs.
  'Coding Agents 101' = /blog/coding-agents-101-the-art-of-actually-getting-things-done

STRANDS DOC URLS — base is https://strandsagents.com/docs/... (NOT /latest/..., which 404s):
  .../user-guide/concepts/agents/conversation-management/  (READ)
  .../api/python/strands.agent.conversation_manager.conversation_manager/
  .../api/python/strands.agent.agent/
The sdk-python GitHub README is marketing-level. Still unread: Swarm / Graph / Agent-as-Tool
multi-agent patterns, session persistence.

AZURE ARCHITECTURE CENTER — prefix with
https://learn.microsoft.com/en-us/azure/architecture/ai-ml/
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

YIELD RANKING as of the ELEVENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES — NEW AT RANK 1, and it earned it. One cheap fetch of
     modelcontextprotocol.io/specification/versioning caught a whole protocol revision that
     invalidated parts of five existing facts. Spec pages are dated, authoritative, and change
     underneath you silently. Check the MCP versioning page EVERY run; when it moves, read the
     changelog and grep the refs.
  2. PRIMARY INCIDENT POST-MORTEMS, wherever they appear. Validated twice (ninth, tenth runs).
     When one appears for an incident already in the kb, fetch it and re-verify — do not assume
     the kb version is right.
  3. microsoft.com/en-us/research/blog — NEW ENTRY, swept for the first time this run and
     immediately produced 2 facts from 2 fetches, one of them (SkillOpt) with unusually strong
     measurements. Research-grade, dated, method-and-numbers posts. Scan for agent/memory/skill/
     eval posts; skip health, quantum and diffusion. STRONG.
  4. anthropic.com/engineering — still strong. eval-awareness-browsecomp READ this run (fact
     2d280a46). STILL UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions.
  5. Azure Architecture Center doc pages above. The gateway pair gave 5 facts + 2 updates from
     2 fetches. The six-part RAG series is the largest coherent unread block in this file.
  6. aws.amazon.com/blogs/machine-learning — NEW ENTRY. High volume and heavily product-
     marketing, but it is where spec-level changes surface early (it is how 2026-07-28 was
     caught). Scan titles for spec/protocol/security/identity; skip customer stories and
     'build X with Y' tutorials, which are most of the feed.
  7. builder.aws.com Builders' Library — 16 of 30 read for 55+ facts, but visibly exhausting.
     Read resilient-services and resilient-serverless, then reassess.
  8. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread
     TECHNICAL posts: coding-agents-101-the-art-of-actually-getting-things-done, swe-grep,
     blockdiff, devin-annual-performance-review-2025, evaluating-coding-agents,
     making-fable-cheaper-than-opus, devin-fusion, swe-1-7,
     measuring-open-source-model-trustworthiness, introducing-devin-security-swarm,
     frontier-code and frontier-code-1.1, ai-productivity.
     Skip partnership/funding/office/acquisition posts — about half the feed.
  9. huggingface.co/blog — real recurring seam. Scan for incident, infrastructure and
     engineering posts; SKIP model/dataset announcements, which are most of the feed. Posts can
     be namespaced under an org (huggingface.co/blog/<org>/<slug>) — easy to miss.
     Unread: security-incident-july-2026 (low priority, superseded by the Jul 27 timeline).
 10. genai.owasp.org — HTML blog posts only; the reports are gated PDFs (see above).
 11. sourcegraph.com/blog — real measurements. Unread:
     compliance-first-ai-proving-agent-provenance, 
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone,
     owning-a-codebase, the-hidden-cost-of-code-that-nobody-touches.
 12. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
 13. simonwillison.net/tags/llms/ — high volume, mostly link-blogging, but the fastest POINTER
     to primary post-mortems. Unread: the-first-known-runaway-ai-agent (Jul 23),
     are-ai-labs-pelicanmaxxing, thomas-ptacek (sandbox escapes), bad-codex-bug (file
     deletions), relay-market (token-reseller fraud).
 14. latent.space/archive — interview format, yields thresholds. Unread: /p/aiewf26trends,
     /p/modal2026, /p/poolside, /p/chatgpt-work. NOTE: the newest post as of Jul 30
     (ontologies-agentic-systems) was checked and is BELOW THE BAR — no numbers, no failure
     conditions, no comparison. This feed skews discussion-level; verify a post has
     measurements before spending a full read.
 15. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 16. embracethered.com/blog — low volume, high value, security only.
 17. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 18. research.google/blog — checked twice, recent output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable, do not keep re-fetching blind:
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... above.
  OWASP resource PDFs — gated download, no renderer. HTML blog posts are fine.
  NOTE: builder.aws.com and the Vectara leaderboard were BOTH listed here and neither was ever
    dead. See the warning near the top before adding anything to this list.

TIER 6 GITHUB READMEs — CLOSED OUT, verdict consistent across two runs. Five of six returned
catalogue- or marketing-level text below the bar. The ONLY two things worth having from the
whole tier were MAINTENANCE-STATUS notices (autogen's maintenance mode; semantic-kernel's 'now
Microsoft Agent Framework'), which generalises: a repo README is worth a fetch for LIFECYCLE
STATUS and nothing else. If a repo matters, go to its DOCS site. Only remaining tier-6 item:
the x1xhlol INDIVIDUAL prompt files. Frame anything from those as 'this harness's published
prompt does X', never as 'the correct approach is X'.

STALENESS-POOL NOTE (updated eleventh run). Tracked as checked so far — cb98732e, 27652a82,
111f8b2c, 2b74037b, 5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628,
f877f05d, d4e3b247, bcbf13c2, d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4,
882100d9, 28ba65db, c93d93ee, c7290868, c1bbf73f, 48c4e555, c2f12069, and (eleventh run)
62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745.
Nothing in this kb is yet older than 90 days, so confidence remains the only sampling axis;
when the pool is exhausted, switch to age per the spec. AVOID SAMPLING kb/principles/**.

WHAT THE STALENESS PASS ACTUALLY FINDS — FOUR RUNS OF EVIDENCE, and it is now the single most
reliable defect-finder in this job. It is NOT finding stale facts. It is finding
CITATION-FIDELITY defects in facts whose underlying claims are correct:
  ninth   — 56986e8f: a paraphrase wearing quote marks.
  tenth   — c93d93ee: an overclaiming gloss attributed to the source.
  tenth   — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh— 96ebc34e: BOTH at once. A pack gloss ('more tools made performance worse due to poor
            strategic usage') was presented as a quote AND reversed the blame — the source says
            agents 'weren't given sufficient strategic information', i.e. the BUILDER under-
            documented the tools. The gloss implies the model is bad at choosing and a stronger
            model would help; the source says fix your tool descriptions. Also scoped wrong:
            'this' in the source is CONTEXT OVERFLOW, not general performance.
  eleventh— c858a924: WRONG ACTOR. '94% agreement between independent auditors' → the auditors
            were GPT-5.5 and Opus 4.6, i.e. LLM judges, across 313 tasks. The fact concluded
            'human transcript review is reproducible enough to be worth doing'. It licensed a
            practice the evidence never supported.
CHECKLIST for future passes — verify all four explicitly, not just 'is the claim still true':
  (1) quotation boundaries, (2) causal direction, (3) WHO the actor is in a cited measurement
  (human vs model vs tool), (4) what the pronoun in a quoted sentence actually refers to.
Also spot-check refs classification (local vs external) and `sources` counts — e9b7eef3 carried
sources: 0 with one real source; c99ec745 had an external URL filed as local.
