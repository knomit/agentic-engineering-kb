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
https://modelcontextprotocol.io/specification/2026-07-28/deprecated      <- ADDED 12th run (cheap tripwire)
https://owasp-agentic-ai-security-incidents.lovable.app/                 <- ADDED 12th run (ASI incidents tracker)
https://github.com/vectara/hallucination-leaderboard
https://huggingface.co/blog

*** HOW TO READ AN OWASP PDF — SOLVED 12th RUN, AND IT NEEDS NO BROWSER AND NO GATE ***
The 11th run recorded these as "gated PDF" and the 12th run read one end to end in four calls.
The working route, exactly:
  1. WebFetch the RESOURCE PAGE (e.g. genai.owasp.org/resource/state-of-agentic-ai-security-and-governance/)
     with a prompt asking for "the direct PDF download URL if present in the page HTML". It returns
     one, of the form https://genai.owasp.org/download/<id>/?tmstv=<epoch>. There is NO form gate.
  2. WebFetch that download URL. It will REPLY that the content is unreadable binary — ignore that,
     because the same tool result ends with "[Binary content (application/pdf, N MB) also saved to
     <path>]". That path is the whole point of the call.
  3. python3 -c "from pypdf import PdfReader; ..." over that path, writing a .txt.
  4. Read the .txt in page slices. Do NOT pipe a big slice straight to stdout — it will exceed the
     tool-result cap and spill to a file; write to a scratch file and Read that instead.
     textwrap.fill(body, 110) makes the extracted text readable.
The State of Agentic AI report is 139 pages / ~275k chars this way.

*** THE 'DEAD OR UNREADABLE' LIST NOW HAS A FOUR-FOR-FOUR FALSE-POSITIVE RECORD ***
builder.aws.com (three runs), the Vectara leaderboard, OWASP PDFs "no renderer" (11th run), and now
OWASP PDFs "gated" (11th run, refuted by the 12th). Every single source this pack has ever declared
unreachable was reachable by another route. BEFORE RECORDING ANY SOURCE AS DEAD, exhaust:
  (1) a server-rendered canonical mirror — GitHub README, raw file, RSS/Atom, archive path;
  (2) the claude-in-chrome browser tools;
  (3) a different PARSER for the same bytes (pypdf, not the Read tool);
  (4) the RESOURCE/LANDING page, asked for the asset URL — this is what cracked OWASP.
And prefer the wording "unread by method X" over "dead" — the wording is what future runs act on.
pypdf caveats that still hold: the true page count can exceed what the Read tool advertises
(AIUC-1 announced 15pp, is 55); Read's `limit` counts LINES and one PDF page is one very long line;
slide-deck PDFs lose word spacing ("Asorganizationsincreasingly...") but stay readable.

OWASP GenAI PDF REPORTS — STATUS AFTER THE 12th RUN:
  AIUC-1 Crosswalks OWASP Top 10 for Agentic Applications (May 2026, 55pp)  READ (11th), 3 facts+1 upd
  AI Security Solutions Landscape for AI/Agentic Red Teaming Q2 2026 (15pp) READ (11th), 1 fact
  State of Agentic AI Security and Governance 2.01 (Jun 2026, 139pp)        READ (12th), 8 facts+1 upd
    ^ the densest document in the pack. Chapters worth re-mining that the 12th run did NOT write up:
      Enterprise Adoption Maturity Model (p53-62), Alignment with Top 10 Agentic (p61),
      Future Trends / What Remains Unsolved (p63-68) incl. governance-deployment collision,
      cyber-insurance coverage collapse, OT/ICS, adversarial agent weaponisation;
      AI SBOM and Supply Chain Provenance (p46-48); Explainable AI (p49);
      Appendix 1 agent-type taxonomy (p70-76); Appendix 3 ASI risk classes by adoption tier (p116);
      Appendix 6 Top 10 Impacting Personal Agents (p128). Appendix 2 (regulatory, p77-116) is
      reference material, low altitude for this pack — the four headline clocks are already captured.
STILL UNREAD, all named by the report as companion resources and all HIGH PRIORITY:
  Securing Agentic Applications Guide 1.0        (threat taxonomy -> architecture patterns + controls)
  Multi-Agentic System Threat Modeling Guide 1.0
  Agent Name Service (ANS) v1.0                  (pairs with the new discovery fact 8b32c15a)
  A Practical Guide for Secure MCP Server Development
  CheatSheet — Securely Using Third-Party MCP Servers 1.0
  Agentic AI Solution Landscape                  (maps Top 10 Agentic risks to tooling)
  OWASP AIBOM / AIBOM Generator
  GenAI Data Security Risks & Mitigations
  GenAI Red Teaming Guide
  ASI Exploits & Incidents Tracker — the GitHub repo URL is footnote 19 and was NOT captured; the
    visual explorer is https://owasp-agentic-ai-security-incidents.lovable.app/ (now in the list
    above). This is a LIVING tracker of real-world agentic incidents mapped to ASI categories, which
    makes it rank-2 material by this file's own yield ranking. Find the repo URL next run.
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/

*** MCP 2026-07-28 — THE BACKLOG NAMED BY THE 11th RUN IS NOW CLEARED ***
Tripwire checked 12th run: still 2026-07-28, NO movement since the 11th. Check it EVERY run anyway;
it remains the cheapest high-value fetch in the pack.
READ this run (all four the 11th run queued):
  /specification/2026-07-28/basic/patterns/mrtr                      -> edf39c27 + upd e26efa36
  /specification/2026-07-28/basic/authorization/client-registration  -> 00fd386c
  /specification/2026-07-28/deprecated                               -> upd 012daf73
  /docs/extensions/overview                                          -> fafca497
STILL UNREAD in this revision, in rough value order:
  /specification/2026-07-28/server/discover        (the mandatory RPC; referenced by 3 facts, never read)
  /specification/2026-07-28/basic/index#meta       (the _meta contract everything now rides on)
  /specification/2026-07-28/basic/authorization/security-considerations
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/versioning       (negotiation + backward-compat with 2025-11-25)
  /extensions/tasks/overview and /extensions/apps/overview
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude)
NOTE for a human: Appendix A on disk still says "MCP's current revision is 2025-11-25". WRONG since
the 11th run. Jobs cannot edit the disk copy. Also worth a disk edit: Appendix A's Tier-0 lethal-
trifecta entry now has a documented counter-position (see below).

*** A TIER-0 FACT HAD A COUNTER-POSITION NOBODY HAD LOOKED FOR (12th run) ***
48c9de1b said "any two [of the lethal trifecta] are survivable". OWASP names the counter-evidence:
Meta's Agents Rule of Two (Oct 2025) turns the trifecta into "no more than two without approval",
BUT "Invitation Is All You Need" (2025) documents calendar-invite attacks viable with only TWO of
the three present. Fact corrected to a screening heuristic rather than a safety threshold.
GENERALISE: the pack's oldest facts are its least re-examined. Tier-0 and Tier-1 material was all
written in the first run from a single source each, and nothing has revisited whether the field
moved. The staleness pass samples on confidence, which systematically MISSES these because they
were written confident. Consider sampling the earliest-written facts as a separate axis.

*** FOUR RECURRING FEEDS HAD NEVER BEEN SWEPT IN TEN RUNS — FOUND AND FIXED, 11th RUN ***
A URL sitting in the recurring list is NOT evidence anyone followed it. Cross-referencing the list
against every crawl-state revision showed four indexes with ZERO article-level fetches:
microsoft.com/research (HIGH YIELD), aws.amazon.com/blogs/machine-learning (surfaced the MCP
revision), latent.space/archive, genai.owasp.org. GENERALISE: before trusting a recurring source as
"up to date", check the history for an ARTICLE-LEVEL fetch from it, not merely a mention.

*** kb/principles/** IS READ-ONLY TO JOBS — AFFECTS THE STALENESS PASS ***
knomit_update on a fact under kb/principles/ fails with:
    validation "must-have-designer-entity" at principles: principles must be authored via
    /knomit-principle (entities must include 'designer')
Pipeline-minted synthesis facts (origin: distilled or discovered) live there and legitimately have
no 'designer' entity. Do NOT add one — it would falsely assert designer authorship, and origin is
immutable. Affected: 1feacc9e, 2c0e8e7c, b9b45ff5, 0f260eea, 6ec9b2b6, 00d3ef19, 28ba65db, c2f12069.
You can READ and verify these but cannot record the result. PREFER OTHER TOPICS.

*** SPEC-COMPLIANCE ISSUE, for a human to decide ***
Synthesis facts minted by the discovery/distill pipelines carry only LOCAL refs and no external URL,
while the spec requires every fact to carry at least one URL. Grounding is real (it flows through the
local refs), but the spec has no carve-out. The 10th run tried to fix it and was REJECTED by the
designer-entity validator. Either the spec needs the carve-out, the pipelines must propagate external
refs at mint time, or kb/principles/ must accept job edits.
RELATED, and job-fixable: ordinary facts can have refs MISFILED. The 11th run found c99ec745 carrying
an external GitHub URL inside refs.local. Spot-check ref classification and `sources` counts.

BROWSER METHOD (works first try, no clicking or waiting):
    mcp__claude-in-chrome__navigate {url}        -> returns a tabId
    mcp__claude-in-chrome__get_page_text {tabId} -> full article text
CAVEAT: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub ending
in 'Loading article'; call it again. Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index use mcp__claude-in-chrome__javascript_tool with a querySelectorAll
expression — mcp__claude-in-chrome__find returns element refs but NOT hrefs.
NOTE: large learn.microsoft.com and platform.claude.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned, or grep it. Ask a NARROW prompt to keep the
answer inline instead. Likewise a broad knomit_query can exceed the tool-result limit — lower `limit`.

*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY ***
Confirmed video-only, no prose body, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Publication date does not predict it. Budget one cheap fetch per article and abandon if the text ends
right after the byline.

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

CORRECTED (fifth run): cognition slugs guessed from titles 404. Always pull
https://cognition.com/blog for exact slugs.
  'Coding Agents 101' = /blog/coding-agents-101-the-art-of-actually-getting-things-done

STRANDS DOC URLS — base is https://strandsagents.com/docs/... (NOT /latest/..., which 404s):
  .../user-guide/concepts/agents/conversation-management/  (READ)
  .../api/python/strands.agent.conversation_manager.conversation_manager/
  .../api/python/strands.agent.agent/
Still unread: Swarm / Graph / Agent-as-Tool multi-agent patterns, session persistence.

CLAUDE PLATFORM DOCS — the prompting page now routes to PER-MODEL sub-pages (found 12th run):
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

YIELD RANKING as of the TWELFTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES. modelcontextprotocol.io/specification/versioning plus the
     /deprecated registry. One cheap fetch caught a protocol revision that invalidated parts of five
     facts. Spec pages are dated, authoritative, and change underneath you silently. EVERY run.
  2. PRIMARY INCIDENT POST-MORTEMS, wherever they appear — now including the OWASP ASI incidents
     tracker, which is a curated feed of exactly this. Validated three times. When one appears for an
     incident already in the kb, fetch it and re-verify; do not assume the kb is right.
  3. OWASP GenAI PDF REPORTS. Three read across two runs for 12 facts + 2 corroborations, and the
     read route is now solved (see top). The companion guides list above is the single richest
     unread block in this file. HIGH PRIORITY.
  4. MCP 2026-07-28 remaining spec pages (list above). server/discover first — three facts reference
     it and none has read it.
  5. microsoft.com/en-us/research/blog — first sweep gave 2 facts from 2 fetches with unusually
     strong measurements. Scan for agent/memory/skill/eval; skip health, quantum, diffusion.
  6. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions.
  7. Azure Architecture Center. The six-part RAG series is the largest coherent unread block.
  8. aws.amazon.com/blogs/machine-learning — high volume, heavily product-marketing, but where
     spec-level changes surface early. Scan titles for spec/protocol/security/identity.
  9. builder.aws.com Builders' Library — 16 of 30 read for 55+ facts, visibly exhausting.
 10. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread:
     coding-agents-101-the-art-of-actually-getting-things-done, swe-grep, blockdiff,
     devin-annual-performance-review-2025, evaluating-coding-agents, making-fable-cheaper-than-opus,
     devin-fusion, swe-1-7, measuring-open-source-model-trustworthiness,
     introducing-devin-security-swarm, frontier-code and frontier-code-1.1, ai-productivity.
     Skip partnership/funding/office/acquisition posts — about half the feed.
 11. huggingface.co/blog — scan for incident/infrastructure/engineering; SKIP model and dataset
     announcements. Posts can be namespaced under an org (huggingface.co/blog/<org>/<slug>).
 12. sourcegraph.com/blog — real measurements. Unread:
     compliance-first-ai-proving-agent-provenance,
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone,
     owning-a-codebase, the-hidden-cost-of-code-that-nobody-touches.
 13. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
 14. simonwillison.net/tags/llms/ — high volume, mostly link-blogging, but the fastest POINTER to
     primary post-mortems. Unread: the-first-known-runaway-ai-agent, are-ai-labs-pelicanmaxxing,
     thomas-ptacek (sandbox escapes), bad-codex-bug, relay-market.
 15. latent.space/archive — interview format. Unread: /p/aiewf26trends, /p/modal2026, /p/poolside,
     /p/chatgpt-work. Skews discussion-level; verify measurements exist before a full read.
 16. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 17. embracethered.com/blog — low volume, high value, security only.
 18. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 19. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — EMPTY except for host moves. Read the four-for-four warning above before adding.
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... above.
  NOTE: builder.aws.com, the Vectara leaderboard, and OWASP PDFs (twice, on two different stated
    reasons) were ALL listed here and NONE was ever actually unreachable.

TIER 6 GITHUB READMEs — CLOSED OUT. Five of six returned catalogue- or marketing-level text below
the bar. The only useful things were MAINTENANCE-STATUS notices (autogen's maintenance mode;
semantic-kernel's 'now Microsoft Agent Framework'), which generalises: a repo README is worth a fetch
for LIFECYCLE STATUS and nothing else. If a repo matters, go to its DOCS site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

STALENESS-POOL NOTE (updated 12th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, and (12th run)
30869b36, c436422a, c1e18090, 9920b5d6, 773a89ee.
Also re-examined outside the pass, on a different axis: 48c9de1b (see the tier-0 note above).
Nothing here is yet older than 90 days, so confidence remains the sampling axis — BUT the 12th run
found that confidence sampling structurally misses the first-run tier-0/tier-1 facts, which were
written confident from a single source each and never revisited. ADD A SECOND AXIS: sample the
EARLIEST-COMMITTED facts, not just the least confident. AVOID SAMPLING kb/principles/**.

WHAT THE STALENESS PASS ACTUALLY FINDS — FIVE RUNS OF EVIDENCE, and it is the single most reliable
defect-finder in this job. It is NOT finding stale facts. It finds CITATION-FIDELITY defects in facts
whose underlying claims are correct:
  ninth   — 56986e8f: a paraphrase wearing quote marks.
  tenth   — c93d93ee: an overclaiming gloss attributed to the source.
  tenth   — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh— 96ebc34e: BOTH at once, and the gloss reversed the blame (model choice vs tool docs).
  eleventh— c858a924: WRONG ACTOR — 'independent auditors' were two LLM judges, not humans.
  twelfth — 30869b36: a pack gloss ('the combined surface area became untenable') wearing quote
            marks; the source actually says a company 'moved on after the project scope overwhelmed
            their infrastructure team'. Same defect class as 56986e8f, four runs later.
  twelfth — c436422a: WRONG TERMS attributed to the source. The fact presented brain/hands/session
            as Anthropic's decomposition; the article's own words are 'a session, a harness, and a
            sandbox'. Harmless-looking, but it makes the fact unsearchable against the source and
            invents vendor vocabulary.
CHECKLIST — verify all six explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to; (5) are the TERMS attributed to the source
  actually the source's terms; (6) refs classification (local vs external) and `sources` counts.
