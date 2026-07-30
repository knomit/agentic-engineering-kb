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

*** PDFs ARE READABLE. THIS PACK HAS NOW MIS-DECLARED THREE SOURCE TYPES DEAD. ***
EARLIER THE SAME DAY this run recorded OWASP's reports as an unfixable blocker — 'gated PDF,
no renderer, do not spend repeated fetches'. WRONG, and corrected within the hour once a human
downloaded two of them. The method, which needs no browser and no download step for files
already on disk:
    python3 -c "from pypdf import PdfReader; ..."   # pypdf IS installed in this environment
The Read tool's PDF path requires pdftoppm/poppler, which is NOT installed — that failure is
what produced the false 'no renderer' verdict. Do not conclude from a Read failure that a PDF
is unreadable. Extract text with pypdf and read the .txt.
CAVEATS: (a) pypdf reports the true page count, which can differ from what the Read tool
advertises — the AIUC-1 crosswalk was announced as 15 pages and is 55. (b) Extracted text can
exceed the Read tool's token cap even with a small `limit`, because `limit` counts LINES and one
PDF page is one very long line; use offset with limit ≈ 100-120 lines. (c) Slide-deck PDFs lose
word spacing ("Asorganizationsincreasingly...") but remain readable.
A browser can also DOWNLOAD gated PDFs, per the user — worth doing when a report is behind a
form rather than already on disk.
THE PATTERN, THIRD OCCURRENCE, NOW THE PACK'S MOST REPEATED PROCESS ERROR: builder.aws.com
(three runs), the Vectara leaderboard, and now OWASP PDFs were each declared unreachable on the
strength of ONE tool failing. In all three cases the content was reachable by another route.
BEFORE RECORDING ANY SOURCE AS DEAD, exhaust: (1) a server-rendered canonical mirror — GitHub
README, raw file, RSS/Atom, archive path; (2) the claude-in-chrome browser tools; (3) a
different PARSER for the same bytes (pypdf for PDF, not the Read tool). And prefer 'unread by
method X' over 'dead' in this file — the wording is what future runs act on.

OWASP PDF REPORTS — STATUS AFTER THE CORRECTION:
  AIUC-1 Crosswalks OWASP Top 10 for Agentic Applications (May 2026, 55pp)  READ, 3 facts + 1 upd
  AI Security Solutions Landscape for AI/Agentic Red Teaming Q2 2026 (15pp) READ, 1 fact
  State of Agentic AI Security and Governance 2.01 (Jun 2026)              STILL UNREAD - GET IT
The crosswalk was the single densest security document read into this pack: an eight-item gap
analysis naming agentic controls that a serious standard omits entirely. HIGH PRIORITY: the
remaining State of Agentic AI report, plus these OWASP docs it cites that the pack has never
seen — Securing Agentic Applications Guide 1.0, Multi-Agentic System Threat Modeling Guide 1.0,
Agent Name Service (ANS) v1.0, CheatSheet - Securely Using Third-Party MCP Servers 1.0, Secure
MCP Server Development Guide. The last two pair directly with this run's MCP 2026-07-28 work.
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06 memory poisoning)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/

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
STILL UNREAD in this revision: /specification/2026-07-28/basic/authorization/client-registration
(CIMD), .../basic/patterns/mrtr, .../deprecated (the registry), /docs/extensions/overview.
Second-source read on the same revision (READ this run): aws.amazon.com/blogs/machine-learning/
how-agentcore-gateway-supports-the-mcp-2026-07-28-spec/
WATCH: the versioning page remains the cheapest tripwire in the pack. Check it EVERY run.

*** FOUR RECURRING FEEDS HAD NEVER BEEN SWEPT IN TEN RUNS — FOUND AND FIXED, ELEVENTH RUN ***
A URL sitting in the recurring list is NOT evidence anyone followed it. Cross-referencing the
list against every crawl-state revision showed four indexes with ZERO article-level fetches:
  microsoft.com/en-us/research/blog/  — HIGH YIELD. SkillOpt (f0fdc77a) and Memora (eaacbe8a).
  aws.amazon.com/blogs/machine-learning/ — surfaced the MCP 2026-07-28 change. Heavily
    product-marketing, but spec changes surface here early.
  www.latent.space/archive — bare domain fetched once (4th run, subscribe wall), one article
    read (5th), but the ARCHIVE INDEX never swept. Newest post (ontologies-agentic-systems) is
    discussion-level, no numbers, BELOW THE BAR. Unread: /p/aiewf26trends, /p/modal2026,
    /p/poolside, /p/chatgpt-work.
  genai.owasp.org/ — three deep links fetched at init, index never swept. See PDF section above.
GENERALISE: before trusting a recurring source as 'up to date', check the history for an
ARTICLE-LEVEL fetch from it, not merely a mention. Four of twenty-one were phantoms.

*** kb/principles/** IS READ-ONLY TO JOBS — AFFECTS THE STALENESS PASS ***
knomit_update on a fact under kb/principles/ fails with:
    validation "must-have-designer-entity" at principles: principles must be authored via
    /knomit-principle (entities must include 'designer')
Pipeline-minted synthesis facts (origin: distilled or discovered) live there and legitimately
have no 'designer' entity. Do NOT add one — it would falsely assert designer authorship, and
origin is immutable. Affected: 1feacc9e, 2c0e8e7c, b9b45ff5, 0f260eea, 6ec9b2b6, 00d3ef19,
28ba65db, c2f12069. You can READ and verify these but cannot record the result. PREFER OTHER
TOPICS. This also makes the ref-compliance issue below unfixable, not merely unflagged.

*** SPEC-COMPLIANCE ISSUE, for a human to decide ***
Synthesis facts minted by the discovery/distill pipelines carry only LOCAL refs and no external
URL, while the spec requires every fact to carry at least one URL. Grounding is real (it flows
through the local refs), but the spec has no carve-out. The tenth run tried to fix it and was
REJECTED by the designer-entity validator. Either the spec needs the carve-out, the pipelines
must propagate external refs at mint time, or kb/principles/ must accept job edits.
RELATED, and job-fixable: ordinary facts can have refs MISFILED. The eleventh run found
c99ec745 carrying an external GitHub URL inside refs.local; re-sending the full list as external
corrected it. Spot-check ref classification and `sources` counts during staleness passes.

BROWSER METHOD (works first try, no clicking or waiting):
    mcp__claude-in-chrome__navigate {url}        -> returns a tabId
    mcp__claude-in-chrome__get_page_text {tabId} -> full article text
CAVEAT: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Intermittent (6th run: every time; 7th and 9th:
never; 8th: once). Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index use mcp__claude-in-chrome__javascript_tool with a
querySelectorAll expression — mcp__claude-in-chrome__find returns element refs but NOT hrefs.
The browser can also DOWNLOAD gated files for local parsing (see PDF section).
NOTE: large learn.microsoft.com pages exceed WebFetch's inline limit and are persisted to a file
on disk; just Read the path returned. Ask a NARROW prompt to keep the answer inline instead.
Likewise a broad knomit_query can exceed the tool-result limit — lower `limit` or filter, rather
than reading the spill file (its lines are too long for Read's chunking).

*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY ***
Confirmed video-only, no prose body, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Publication date does not predict it. Budget one cheap fetch per article and abandon if the text
ends right after the byline.

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

'Caching challenges and strategies' and 'Static stability using Availability Zones' are NOT in
the catalogue and appear retired. Static stability is covered inside smaller-service-in-control;
caching's failure modes inside constant-work and lunch-rush.

redirects folded in:
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
Still unread: Swarm / Graph / Agent-as-Tool multi-agent patterns, session persistence.

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

YIELD RANKING as of the ELEVENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES. One cheap fetch of modelcontextprotocol.io/specification/
     versioning caught a protocol revision that invalidated parts of five facts. Spec pages are
     dated, authoritative, and change underneath you silently. Check EVERY run.
  2. PRIMARY INCIDENT POST-MORTEMS, wherever they appear. Validated twice. When one appears for
     an incident already in the kb, fetch it and re-verify — do not assume the kb is right.
  3. OWASP GenAI PDF REPORTS — NEW AT RANK 3, and they were locked behind a false blocker for
     eleven runs. The AIUC-1 crosswalk gave 3 facts + 1 corroboration from ONE document,
     including an eight-item gap analysis that is the best security material in the pack. The
     cited companion guides (Securing Agentic Applications, Multi-Agentic System Threat
     Modeling, ANS, the two MCP cheat sheets) are all unread. HIGH PRIORITY.
  4. microsoft.com/en-us/research/blog — first sweep gave 2 facts from 2 fetches, one with
     unusually strong measurements. Research-grade, dated, method-and-numbers. Scan for
     agent/memory/skill/eval; skip health, quantum, diffusion.
  5. anthropic.com/engineering — eval-awareness-browsecomp READ (2d280a46). STILL UNREAD:
     AI-resistant-technical-evaluations, building-c-compiler, contextual-retrieval,
     swe-bench-sonnet, desktop-extensions.
  6. Azure Architecture Center doc pages above. The six-part RAG series is the largest coherent
     unread block in this file.
  7. aws.amazon.com/blogs/machine-learning — high volume, heavily product-marketing, but where
     spec-level changes surface early. Scan titles for spec/protocol/security/identity; skip
     customer stories and 'build X with Y' tutorials, which are most of the feed.
  8. builder.aws.com Builders' Library — 16 of 30 read for 55+ facts, visibly exhausting. Read
     resilient-services and resilient-serverless, then reassess.
  9. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread
     TECHNICAL posts: coding-agents-101-the-art-of-actually-getting-things-done, swe-grep,
     blockdiff, devin-annual-performance-review-2025, evaluating-coding-agents,
     making-fable-cheaper-than-opus, devin-fusion, swe-1-7,
     measuring-open-source-model-trustworthiness, introducing-devin-security-swarm,
     frontier-code and frontier-code-1.1, ai-productivity.
     Skip partnership/funding/office/acquisition posts — about half the feed.
 10. huggingface.co/blog — scan for incident/infrastructure/engineering; SKIP model and dataset
     announcements. Posts can be namespaced under an org (huggingface.co/blog/<org>/<slug>).
 11. sourcegraph.com/blog — real measurements. Unread:
     compliance-first-ai-proving-agent-provenance,
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone,
     owning-a-codebase, the-hidden-cost-of-code-that-nobody-touches.
 12. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
 13. simonwillison.net/tags/llms/ — high volume, mostly link-blogging, but the fastest POINTER
     to primary post-mortems. Unread: the-first-known-runaway-ai-agent, are-ai-labs-
     pelicanmaxxing, thomas-ptacek (sandbox escapes), bad-codex-bug, relay-market.
 14. latent.space/archive — interview format. Unread: /p/aiewf26trends, /p/modal2026,
     /p/poolside, /p/chatgpt-work. Skews discussion-level; verify a post has measurements
     before spending a full read.
 15. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 16. embracethered.com/blog — low volume, high value, security only.
 17. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 18. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — SHORT LIST, and read the three-strikes warning at the top before adding:
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... above.
  NOTE: builder.aws.com, the Vectara leaderboard, and OWASP PDFs were ALL listed here and NONE
    of them was ever actually unreachable. This list has a 100% false-positive rate so far.

TIER 6 GITHUB READMEs — CLOSED OUT. Five of six returned catalogue- or marketing-level text
below the bar. The only two useful things were MAINTENANCE-STATUS notices (autogen's maintenance
mode; semantic-kernel's 'now Microsoft Agent Framework'), which generalises: a repo README is
worth a fetch for LIFECYCLE STATUS and nothing else. If a repo matters, go to its DOCS site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

STALENESS-POOL NOTE (updated eleventh run). Checked so far — cb98732e, 27652a82, 111f8b2c,
2b74037b, 5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d,
d4e3b247, bcbf13c2, d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9,
28ba65db, c93d93ee, c7290868, c1bbf73f, 48c4e555, c2f12069, and (eleventh run) 62c9a78b,
e9b7eef3, 96ebc34e, c858a924, c99ec745.
Nothing here is yet older than 90 days, so confidence remains the only sampling axis; when the
pool is exhausted, switch to age per the spec. AVOID SAMPLING kb/principles/**.

WHAT THE STALENESS PASS ACTUALLY FINDS — FOUR RUNS OF EVIDENCE, and it is now the single most
reliable defect-finder in this job. It is NOT finding stale facts. It finds CITATION-FIDELITY
defects in facts whose underlying claims are correct:
  ninth   — 56986e8f: a paraphrase wearing quote marks.
  tenth   — c93d93ee: an overclaiming gloss attributed to the source.
  tenth   — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh— 96ebc34e: BOTH at once. A pack gloss ('more tools made performance worse due to poor
            strategic usage') was presented as a quote AND reversed the blame — the source says
            agents 'weren't given sufficient strategic information', i.e. the BUILDER under-
            documented the tools. The gloss implies a stronger model would help; the source says
            fix your tool descriptions. Also scoped wrong: 'this' meant CONTEXT OVERFLOW.
  eleventh— c858a924: WRONG ACTOR. '94% agreement between independent auditors' → the auditors
            were GPT-5.5 and Opus 4.6, i.e. LLM judges. The fact concluded 'human transcript
            review is reproducible enough to be worth doing', licensing a practice the evidence
            never supported.
CHECKLIST — verify all four explicitly, not just 'is the claim still true':
  (1) quotation boundaries, (2) causal direction, (3) WHO the actor is in a cited measurement
  (human vs model vs tool), (4) what the pronoun in a quoted sentence refers to.
Also spot-check refs classification (local vs external) and `sources` counts.
