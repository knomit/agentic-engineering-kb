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
https://github.com/vectara/hallucination-leaderboard
https://huggingface.co/blog

*** FETCH ROUTES. READ BEFORE CALLING ANYTHING BLOCKED. ***

1. openai.com/index/<slug> RETURNS HTTP 403 TO WebFetch. IT READS FINE IN A REAL BROWSER.
   CORRECTED AGAIN 2026-08-11 (14th run) — AND THE CORRECTION IS ABOUT WHICH BROWSER SERVER EXISTS.
   The 13th run's route named mcp__claude-in-chrome__*. The 13th run's own correction then said those
   "do not exist in this job" and mandated mcp__browser__*. BOTH CLAIMS ARE TOO ABSOLUTE. The 14th run
   ran with mcp__claude-in-chrome__* PRESENT and working first try on openai.com/index/*.
   THE RULE: the browser server available depends on how the job was invoked, not on the job identity.
   DO NOT hardcode either name. Check what is actually present, then use it:
     mcp__claude-in-chrome__navigate {url}        -> returns a tabId
     mcp__claude-in-chrome__get_page_text {tabId} -> full article text
     mcp__browser__browser_navigate {url}  then  mcp__browser__browser_snapshot
   Both are read-only navigation + text extraction and both cracked openai.com. The server must run
   REAL Chrome, not headless Chromium — headless Chromium gets a Cloudflare "Just a moment..."
   interstitial. Plain curl also 403s. Do NOT record openai.com as paywalled or dead — it is
   WebFetch-403, browser-readable. VERIFIED 2026-08-11 on four separate openai.com/index/ posts.

1b. *** CHEAPEST WAY TO RESOLVE AN UNKNOWN SLUG: WebSearch WITH allowed_domains. NEW, 14th run. ***
   Guessed slugs have now 404'd on cognition, strands, adk and openai. The standing advice was
   "always pull the href off the index", which needs a browser. There is a cheaper first move:
     WebSearch {query: "<exact article title>", allowed_domains: ["openai.com"]}
   This resolved the Aug 7 post in ONE call, no browser, and surfaced THREE sibling posts nobody
   knew existed. Use it before spending a browser navigation. Then still pull hrefs off the page
   with javascript_tool for anything you intend to fetch — a querySelectorAll over a[href*="/index/"]
   returns slug + title + date together and is how the two Aug 10 posts were found.

2. OWASP PDF DOWNLOADS ARE GATED ON THE USER-AGENT. NOTHING ELSE. `-A` IS THE WHOLE FIX.
     curl -sL -A "Mozilla/5.0" -o out.pdf "https://genai.owasp.org/download/<id>/?tmstv=<epoch>"
     file out.pdf     # MUST say "PDF document". "HTML document" = the default curl UA went out.
     pdftotext out.pdf out.txt      # then Read out.txt
   ISOLATED A/B, 2026-08-11, same URL, four requests back to back:
     bare curl                  -> HTML  (821KB, <title> "No Access - OWASP Gen AI Security Project")
     -A only                    -> PDF   122pp, 2.4MB, 228KB extracted text
     Referer only               -> HTML
     -A + Referer, NO cookies   -> PDF
   THIS SOURCE HAS NOW BEEN MISDIAGNOSED THREE TIMES, EACH BY A RUN THAT SUCCEEDED WITHOUT
   ISOLATING THE VARIABLE:
     11th run   "gated PDF, needs a form"          -> wrong; no form exists
     13th run   "gated on a Referer header"        -> wrong; Referer alone returns HTML
     14th pass  "needs a wp-dlm session cookie"    -> wrong; an EMPTY cookie jar downloads fine,
                and the jar it prescribed was verified empty in the run that "proved" it
   Every one was written down from a command that happened to work, crediting all flags equally.
   WHEN A FETCH FINALLY WORKS, DROP ONE FLAG AT A TIME BEFORE RECORDING THE RECIPE. A recipe
   carrying passenger flags is worse than verbose: it sends the next run hunting a cookie that
   does not exist, and it manufactures a false "this source is gated" when the real gate moves.
   The tmstv token is NOT an expiring nonce — the same value worked six days later.

The 12th run's WebFetch route still works and needs no headers — keep it as the fallback:
  1. WebFetch the RESOURCE PAGE asking for "the direct PDF download URL if present in the page HTML".
  2. WebFetch that download URL. It REPLIES that the content is unreadable binary — ignore that;
     the same tool result ends with "[Binary content (application/pdf, N MB) also saved to <path>]".
  3. Parse that path with pdftotext, writing a .txt; read the .txt in page slices.

*** THE 'DEAD OR UNREADABLE' LIST HAS A FIVE-FOR-FIVE FALSE-POSITIVE RECORD ***
builder.aws.com (three runs), the Vectara leaderboard, OWASP PDFs "no renderer" (11th run),
OWASP PDFs "gated" (11th run, refuted by the 12th), and the underlying OWASP gate turning out to be
one missing HTTP header. Every single source this pack has ever declared unreachable was reachable
by another route. BEFORE RECORDING ANY SOURCE AS DEAD, exhaust:
  (1) a server-rendered canonical mirror — GitHub README, raw file, RSS/Atom, archive path;
  (2) whichever browser MCP server is present, real Chrome (this is what cracked openai.com);
  (3) a different PARSER for the same bytes (pdftotext, not the Read tool);
  (4) the RESOURCE/LANDING page, asked for the asset URL;
  (5) REQUEST HEADERS **AND COOKIES** — Referer, User-Agent, and a cookie jar primed by visiting the
      landing page first. Cheapest of the five. `file` any downloaded binary before believing it.
And prefer the wording "unread by method X" over "dead" — the wording is what future runs act on.
ADD A SIXTH, 14th run: a 404 IS NOT A DEAD SOURCE, IT IS USUALLY A WRONG SLUG. See 1b.
pypdf caveats that still hold: the true page count can exceed what the Read tool advertises
(AIUC-1 announced 15pp, is 55); Read's `limit` counts LINES and one PDF page is one very long line;
slide-deck PDFs lose word spacing but stay readable.

*** THE HISTORY WALK IS BACK — THE MODEL CHANGED 2026-08-11. WALK IT. ***
Supersedes every earlier "the walk is over / do not reopen it" banner in this file. crawl-state no
longer carries a cumulative union; each run REPLACES its body with only what that run newly crawled,
and the full ALREADY_CRAWLED set is reconstructed by walking crawl-state's revisions with
knomit_explain. Protocol and the aging rule are in Appendix S. The last cumulative revision (14th
run, 197 URLs) is the BACKFILL FLOOR — a walk that reaches it has reached the bottom.
Why: a cumulative body grows without bound and is re-read in full every run, and a flat union has no
per-URL dates, so it cannot express "older than N days counts as never crawled".
OWASP GenAI PDF REPORTS — STATUS:
  AIUC-1 Crosswalks OWASP Top 10 for Agentic Applications (May 2026, 55pp)  READ (11th), 3 facts+1 upd
  AI Security Solutions Landscape for AI/Agentic Red Teaming Q2 2026 (15pp) READ (11th), 1 fact
  State of Agentic AI Security and Governance 2.01 (Jun 2026, 139pp)        READ (12th), 8 facts+1 upd
    ^ chapters still NOT written up: Enterprise Adoption Maturity Model (p53-62), Alignment with
      Top 10 Agentic (p61), Future Trends / What Remains Unsolved (p63-68) incl. governance-
      deployment collision, cyber-insurance coverage collapse, OT/ICS, adversarial agent
      weaponisation; AI SBOM and Supply Chain Provenance (p46-48); Explainable AI (p49);
      Appendix 1 agent-type taxonomy (p70-76); Appendix 3 ASI risk classes by adoption tier (p116);
      Appendix 6 Top 10 Impacting Personal Agents (p128). Appendix 2 (regulatory) is low altitude.
  OWASP GenAI LLM Top 10 2026 (2026-08-03, 122pp)   READ (13th), 2 facts + 1 update (4f5e9dfe).
    download id 56857. Chapters NOT mined: the ten per-entry chapters themselves. LLM03:2026
    Excessive Agency (p23-26) and LLM08:2026 Hidden Context Exposure (p46-49) are the two most
    relevant to this pack and are UNREAD in detail. Appendix A coverage matrices (p58-105) map to
    ASI 2026, DSGAI v1.0, MITRE ATLAS v2026.06, ATT&CK v19.1, CWE 4.20, NIST AI 600-1, NIST AI RMF,
    CSA AICM v1.1 and AIVSS v0.8 — a large pre-done cross-framework mapping, worth one pass.
STILL UNREAD, all named as companion resources and all HIGH PRIORITY:
  Securing Agentic Applications Guide 1.0        (threat taxonomy -> architecture patterns + controls)
  Multi-Agentic System Threat Modeling Guide 1.0
  Solutions Landscape – Red Teaming Taxonomy (Jun 2026)
  Agent Name Service (ANS) v1.0                  (pairs with discovery facts 8b32c15a and 995c167b)
  A Practical Guide for Secure MCP Server Development
  CheatSheet — Securely Using Third-Party MCP Servers 1.0
  Agentic AI Solution Landscape
  OWASP AIBOM / AIBOM Generator
  GenAI Data Security Risks & Mitigations
  GenAI Red Teaming Guide
  ASI Exploits & Incidents Tracker — the GitHub repo URL is footnote 19 of State of Agentic AI and
    has still NOT been captured. The visual explorer (owasp-agentic-ai-security-incidents.lovable.app)
    is in the list above and has STILL NEVER BEEN FETCHED across THREE runs. Rank-2 material.
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-a-hands-on-companion-to-the-owasp-genai-security-project/

*** MCP 2026-07-28 — TRIPWIRE CHECKED 14th RUN, STILL UNCHANGED ***
Still 2026-07-28, no movement since the 11th run. Check EVERY run anyway; cheapest high-value fetch
in the pack. server/discover WAS READ THIS RUN (14th) — three facts had referenced it and none had
read it; it produced 995c167b and corroborated 031dab74 (sources 2->3). Confirmed: servers MUST
implement it, clients need not call it, serverInfo is self-reported and explicitly not for security
decisions, `instructions` is server-controlled text on the injection path, and on stdio it is the
SHOULD-do backward-compatibility probe because there is no HTTP status code to key fallback on.
STILL UNREAD in this revision, in rough value order:
  /specification/2026-07-28/basic/index#meta       (the _meta contract everything now rides on)
  /specification/2026-07-28/basic/authorization/security-considerations
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/versioning       (negotiation + backward-compat with 2025-11-25)
  /specification/2026-07-28/basic/transports/stdio#backward-compatibility  <- NEW, named by discover
  /specification/2026-07-28/server/utilities/caching  <- NEW, named by discover (ttlMs/cacheScope)
  /extensions/tasks/overview and /extensions/apps/overview
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude)
NOTE for a human: Appendix A on disk was corrected 2026-08-11 and now says 2026-07-28. Good.

*** THE OPENAI CYBER CLUSTER — FOUR POSTS READ 14th RUN, AND THE FEED IS RANK 2 FOR A REASON ***
openai.com/index carries primary security post-mortems under its Security tag and is the single
highest-yield feed found in the last two runs. READ SO FAR:
  /index/third-party-cyber-evaluations-involving-openai-models/          (Aug 4, read 13th)
  /index/hugging-face-model-evaluation-security-incident/                (Jul 21 + updates Jul 28/29)
     ^ THE PRIMARY OPERATOR ACCOUNT of the HF incident. Read 14th run, folded into bcbf13c2.
       Nobody had fetched it for THIRTEEN RUNS while the fact rested on secondary reporting.
  /index/responding-next-frontier-critical-cyber-capabilities/           (Aug 7)
     ^ NOTE THE SLUG. The 13th run guessed "responding-TO-THE-next-frontier-..." and 404'd. The real
       slug drops "to-the". Resolved via WebSearch+allowed_domains — see route 1b.
  /index/expanding-daybreak-as-the-cyber-defense-window-narrows/         (Aug 10) HIGHEST YIELD of the
     ^ four: hard numbers on refusal rates, a turn-budget ranking reversal, a composite-eval
       regression, and real-world vulnerability counts. Three facts came off this one page.
UNREAD AND WANTED NEXT RUN:
  /index/putting-frontier-cyber-models-in-more-trusted-hands/            (Aug 10) — the only one of
     the four Aug 7-10 posts not yet read. Likely program/policy; budget one cheap fetch.
  /index/safety-alignment-long-horizon-models/     (linked from the HF post; long-horizon alignment)
  /index/designing-agents-to-resist-prompt-injection/   <- SURFACED BY SEARCH, never seen before,
     and squarely on this pack's subject. HIGH PRIORITY.
  /index/trusted-access-for-cyber/, /index/scaling-trusted-access-for-cyber-defense/,
  /index/updating-our-preparedness-framework/      (governance; lower altitude)
WATCH FOR THESE TWO — both promised, neither published as of 2026-08-11, both aimed at this pack:
  * OpenAI's full technical report on the Hugging Face incident.
  * A JOINT METR + Redwood Research blog giving a third-party assessment of the model behaviour,
    covering engagement terms, scope and findings. NOTE this partly re-rates metr.org/blog, which the
    13th run demoted to rank 17 — if that joint post lands it is rank-2 material, not rank-17.
  * Irregular's containment white paper for cyber evals (named in the Aug 4 post).
Also still unread: https://www.cnn.com/2026/08/05/tech/meta-ai-hacking (a fifth lab; secondary —
  find the primary), and the simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with 3afa31af),
  the-tokenpocalypse (404media), /2026/Aug/2/open-letters/.

*** MICROSOFT RESEARCH — ALL THREE QUEUED POSTS READ 14th RUN. FEED NOW 2-FOR-3. ***
  /orchard-an-open-framework-for-scalable-agentic-ai/  (Aug 3) READ. NO FACT. Framework announcement.
    Numbers are model-capability scores (69.7% SWE-bench Verified at ~3B active params, 73% with
    value-model reranking; 68.4% GUI; 59.6% Claw-Eval) that describe THEIR models, not a transferable
    engineering constraint. The one idea near the bar — train inside the real deployment harness
    rather than a simplified proxy — is asserted, not measured. Revisit only if they publish the
    train/deploy mismatch as a measurement.
  /echoverse-deep-evolving-environments-for-computer-use-agents/ (Jul 30) READ. 1 FACT (12966de6).
    Best of the three: database-grounded verification and environment-repair loops are method claims
    that transfer. 9B model 36.5%->67.1%; RL held-out 58%->69%.
  /evolib-turning-experience-into-evolving-knowledge/ (Jul 30) READ. NO FACT. Inference-time memory
    consolidation + utility weighting. The blog reports NO absolute numbers, NO named baselines and
    NO failure modes — only shape claims ("higher performance throughout most of the compute range").
    Below the bar as published. If a paper appears with numbers, revisit.
LESSON, worth generalising: a research-lab blog announcing a FRAMEWORK tends to publish capability
scores for its own models, which are not transferable facts. The same feed announcing a METHOD
(Echoverse) publishes design decisions, which are. Prefer method posts; skim framework posts for the
one design decision and move on.

*** kb/principles/** IS READ-ONLY TO JOBS — AFFECTS THE STALENESS PASS ***
knomit_update on a fact under kb/principles/ fails with:
    validation "must-have-designer-entity" at principles: principles must be authored via
    /knomit-principle (entities must include 'designer')
Pipeline-minted synthesis facts (origin: distilled or discovered) live there and legitimately have
no 'designer' entity. Do NOT add one — it would falsely assert designer authorship, and origin is
immutable. Affected: 1feacc9e, 2c0e8e7c, b9b45ff5, 0f260eea, 6ec9b2b6, 00d3ef19, 28ba65db, c2f12069,
f269c82f. You can READ and verify these but cannot record the result. PREFER OTHER TOPICS.

*** SPEC-COMPLIANCE ISSUE, for a human to decide ***
Synthesis facts minted by the discovery/distill pipelines carry only LOCAL refs and no external URL,
while the spec requires every fact to carry at least one URL. Grounding is real (it flows through the
local refs), but the spec has no carve-out. The 10th run tried to fix it and was REJECTED by the
designer-entity validator. Either the spec needs the carve-out, the pipelines must propagate external
refs at mint time, or kb/principles/ must accept job edits.
RELATED, and job-fixable: ordinary facts can have refs MISFILED. The 11th run found c99ec745 carrying
an external GitHub URL inside refs.local. Spot-check ref classification and `sources` counts.
NOTE 14th run: knomit_update REPLACES the entire refs list. Read the existing refs and resend the
full merged list, or you will silently drop sources. This bit nothing this run only because it was
checked first.

BROWSER CAVEATS: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index use javascript_tool with a querySelectorAll expression — `find`
returns element refs but NOT hrefs.
NOTE: large learn.microsoft.com and platform.claude.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned, or grep it. Ask a NARROW prompt to keep the
answer inline instead. Likewise a broad knomit_query can exceed the tool-result limit — CONFIRMED
AGAIN 14th run: sort=recent with limit=60 blew the limit at 69k chars. Use limit<=25.

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

YIELD RANKING as of the FOURTEENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES. modelcontextprotocol.io/specification/versioning plus the
     /deprecated registry. One cheap fetch caught a protocol revision that invalidated parts of five
     facts. Spec pages are dated, authoritative, and change underneath you silently. EVERY run.
  2. PRIMARY INCIDENT POST-MORTEMS, wherever they appear — openai.com/index, aisi.gov.uk/blog,
     anthropic.com/news, and the OWASP ASI incidents tracker. Validated FIVE times now. THE 14th RUN
     ADDS A SHARPER VERSION OF THIS RULE: when the kb holds a fact about an incident, CHECK WHETHER
     THE OPERATOR HAS PUBLISHED ITS OWN ACCOUNT. bcbf13c2 rested on secondary reporting for thirteen
     runs while OpenAI's primary post-mortem sat unfetched, and it contained a claim the secondary
     account contradicted. A fact assembled from secondary sources is an OPEN TASK, not a done one.
  3. OWASP GenAI PDF REPORTS. Four read across three runs for 14 facts + 3 corroborations, and the
     read route is solved twice over. The companion guides list above is still the single richest
     unread block in this file. HIGH PRIORITY.
  4. MCP 2026-07-28 remaining spec pages (list above). server/discover is now DONE; basic/index#meta
     is the next-most-referenced unread page.
  5. microsoft.com/en-us/research/blog — all three queued posts now read (see above); 1 fact of 3.
     Prefer METHOD posts over FRAMEWORK posts. Scan for agent/memory/skill/eval; skip health,
     quantum, diffusion.
  6. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. Index quiet since Apr 2026.
     anthropic.com/news is NEWLY ADDED to the recurring list — postmortems live there, not on
     /engineering, and that is where the July incident review was published.
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
     primary post-mortems. Its VALUE IS THE LINKS: read the index, follow the primaries, rarely read
     Simon himself. CAVEAT ADDED 14th run — his summaries of TALKS are the weakest link in this pack
     and have now produced two claims no primary source corroborates (see 4e923405, bcbf13c2).
     Use him to FIND primaries, not as a substitute for one.
 15. latent.space/archive — interview format. Unread: /p/aiewf26trends, /p/modal2026, /p/poolside,
     /p/chatgpt-work. Skews discussion-level; verify measurements exist before a full read.
 16. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 17. metr.org/blog — demoted 13th run; governance and policy review, one on-topic post redacted.
     RE-RATE IF the joint METR + Redwood assessment of the OpenAI incident lands (see above).
 18. embracethered.com/blog — low volume, high value, security only.
 19. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 20. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — EMPTY except for host moves. Read the five-for-five warning above before adding.
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... above.
  NOTE: builder.aws.com, the Vectara leaderboard, OWASP PDFs (three times, on three different
    stated reasons) and openai.com were ALL listed or headed here and NONE was ever unreachable.

TIER 6 GITHUB READMEs — CLOSED OUT. Five of six returned catalogue- or marketing-level text below
the bar. The only useful things were MAINTENANCE-STATUS notices (autogen's maintenance mode;
semantic-kernel's 'now Microsoft Agent Framework'), which generalises: a repo README is worth a fetch
for LIFECYCLE STATUS and nothing else. If a repo matters, go to its DOCS site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

STALENESS-POOL NOTE (updated 14th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627,
and (14th run) d18637a2, 1beb89e6, f1cbb540, 89df351e, 4e923405.
TWO AXES, ALTERNATE THEM. Confidence axis (lowest-confidence first) and earliest-committed axis.
The 13th run introduced the earliest-committed axis and got 2 defects in 5; the 14th ran the
confidence axis and got 1 clear defect + 1 partial-verification flag in 5. Both work. Nothing in this
kb is yet older than 90 days. AVOID SAMPLING kb/principles/**.
NEW SUB-RULE, 14th run: PREFER FACTS THAT SHARE A SOURCE. f1cbb540 and 89df351e both cite
claude-code-auto-mode, so ONE fetch verified TWO facts. Group the sample by ref where you can — it
roughly halves the fetch cost of the pass at no loss of coverage.
SECOND SUB-RULE: if a narrow verification prompt confirms only PART of a fact, say so IN THE FACT
rather than bumping confidence as if the whole thing were checked (see 1beb89e6's VERIFICATION SCOPE
section). A silent partial confirmation is how an unverified claim acquires false authority.

WHAT THE STALENESS PASS ACTUALLY FINDS — SEVEN RUNS OF EVIDENCE, and it is the single most reliable
defect-finder in this job. It is NOT finding stale facts. It finds CITATION-FIDELITY defects in facts
whose underlying claims are correct:
  ninth   — 56986e8f: a paraphrase wearing quote marks.
  tenth   — c93d93ee: an overclaiming gloss attributed to the source.
  tenth   — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh— 96ebc34e: BOTH at once, and the gloss reversed the blame.
  eleventh— c858a924: WRONG ACTOR — 'independent auditors' were two LLM judges, not humans.
  twelfth — 30869b36: a pack gloss wearing quote marks (the 'combined surface area' line).
  twelfth — c436422a: WRONG TERMS attributed to the source (brain/hands/session).
  thirteenth — f78a326a: WRONG TERM ('raw accuracy' for 'raw agreement') AND a single reported
    instance generalised into a rule.
  thirteenth — 38c06627: MISATTRIBUTION ACROSS A FACT'S OWN TWO REFS.
  fourteenth — d18637a2: A RECOMMENDATION STRENGTHENED INTO A RULE. The fact said "treat sub-3-point
    leaderboard gaps as noise"; the source says such gaps "deserve skepticism until the eval
    configuration is documented and matched". Those prescribe different actions — discard the number
    versus go and get the configuration. ALSO a scope error in the same fact: the 6-point figure is
    Terminal-Bench 2.0 only; the same experiment moved SWE-bench just 1.54 points, so the headline
    number had been silently generalised across benchmarks.
CHECKLIST — verify all EIGHT explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to; (5) are the TERMS attributed to the source
  actually the source's terms; (6) refs classification (local vs external) and `sources` counts;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number — and is a single
  reported instance being presented as a general rule;
  (8) NEW — MODAL STRENGTH AND SCOPE: does the fact state as a rule what the source stated as a
  caution ('is noise' vs 'deserves skepticism', 'reduces' vs 'can reduce'), and does a number
  measured on ONE benchmark/model/config get presented as holding generally?
