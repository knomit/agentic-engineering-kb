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
https://www.aisi.gov.uk/blog/                                            <- ADDED 13th run (see below, RANK 2)
https://openai.com/index/                                                <- ADDED 13th run (see below, RANK 2)
https://github.com/vectara/hallucination-leaderboard
https://huggingface.co/blog

*** TWO NEW FETCH ROUTES, BOTH FOUND 13th RUN. READ BEFORE CALLING ANYTHING BLOCKED. ***

1. openai.com/index/<slug> RETURNS HTTP 403 TO WebFetch. IT READS FINE IN A REAL BROWSER.
   CORRECTED 2026-08-11 — the 13th run's route named mcp__claude-in-chrome__* tools. Those come
   from the Chrome EXTENSION attached to an interactive session; a headless run has no extension
   and --strict-mcp-config drops them regardless. They do not exist in this job. Use the job's own
   `browser` MCP server instead:
     mcp__browser__browser_navigate {url}  then  mcp__browser__browser_snapshot
   VERIFIED 2026-08-11 against the third-party-cyber-evaluations post: full article text, no
   challenge. The server must run REAL Chrome, not headless Chromium — headless Chromium is served
   a Cloudflare "Just a moment..." interstitial and gets nothing. mcp.json pins --browser chrome.
   Plain curl also 403s. Do NOT record openai.com as paywalled or dead — it is WebFetch-403,
   browser-readable.

2. OWASP PDF DOWNLOADS NEED A SESSION COOKIE. `Referer` ALONE IS NOT ENOUGH.
   CORRECTED 2026-08-11. The 13th run recorded "Referer header, not a form". Re-tested today:
   Referer alone returns the 840KB "No Access" page. The gate is a WordPress Download Manager
   cookie (wp-dlm_cookie) that is set when you VISIT THE RESOURCE PAGE. Two curls, one jar:
     curl -sL -c cj.txt -o /dev/null "https://genai.owasp.org/resource/<slug>/"
     curl -sL -b cj.txt -H "Referer: https://genai.owasp.org/resource/<slug>/" \
          -o out.pdf "https://genai.owasp.org/download/<id>/?tmstv=<epoch>"
     file out.pdf     # MUST say "PDF document". "HTML document" = you hit the gate.
     pdftotext out.pdf out.txt      # then Read out.txt
   VERIFIED 2026-08-11: Top 10 2026 = 122pp, 2.4MB, 228KB of extracted text.
   The tmstv token is NOT an expiring nonce — the same value worked six days later, and the
   resource page still serves it. Do not blame tmstv for a failure; blame the missing cookie.
   NO python3 IN THIS JOB. The old recipe's `python3 -c "from pypdf import PdfReader"` is not
   available: arbitrary code execution is not granted. Use `pdftotext`, which is allow-listed.
   The `Read` tool cannot open PDFs either — it shells out to pdftoppm and renders page images.

The 12th run's WebFetch route still works and needs no headers — keep it as the fallback:
  1. WebFetch the RESOURCE PAGE asking for "the direct PDF download URL if present in the page HTML".
  2. WebFetch that download URL. It REPLIES that the content is unreadable binary — ignore that;
     the same tool result ends with "[Binary content (application/pdf, N MB) also saved to <path>]".
  3. pypdf over that path, writing a .txt; read the .txt in page slices, not straight to stdout.
     textwrap.fill(body, 110) makes extracted text readable.

*** THE 'DEAD OR UNREADABLE' LIST NOW HAS A FIVE-FOR-FIVE FALSE-POSITIVE RECORD ***
builder.aws.com (three runs), the Vectara leaderboard, OWASP PDFs "no renderer" (11th run),
OWASP PDFs "gated" (11th run, refuted by the 12th), and now the underlying OWASP gate turns out
to be one missing HTTP header. Every single source this pack has ever declared unreachable was
reachable by another route. BEFORE RECORDING ANY SOURCE AS DEAD, exhaust:
  (1) a server-rendered canonical mirror — GitHub README, raw file, RSS/Atom, archive path;
  (2) the `browser` MCP tools, real Chrome (this is what cracked openai.com);
  (3) a different PARSER for the same bytes (pdftotext, not the Read tool);
  (4) the RESOURCE/LANDING page, asked for the asset URL;
  (5) REQUEST HEADERS **AND COOKIES** — Referer, User-Agent, and a cookie jar primed by
      visiting the landing page first. This is what cracked OWASP (headers were only half of
      it), and it is the cheapest of the five. `file` any downloaded binary before believing it.
And prefer the wording "unread by method X" over "dead" — the wording is what future runs act on.
pypdf caveats that still hold: the true page count can exceed what the Read tool advertises
(AIUC-1 announced 15pp, is 55); Read's `limit` counts LINES and one PDF page is one very long line;
slide-deck PDFs lose word spacing ("Asorganizationsincreasingly...") but stay readable.

*** HISTORY-WALK METHOD — THE 12th RUN LEFT THE LINEAGE WALKABLE BUT RECORDED UNUSABLE SHAs ***
READ THIS BEFORE ANY HISTORY WALK. The crawl-state fact was deleted and recreated on 2026-07-31,
and the 12th run recorded the orphaned commit chain as 8-CHARACTER PREFIXES. knomit_explain
REJECTS short SHAs — every one of them returns "could not read <file> at <sha>". The lineage is
not lost; the recorded handles were just unusable. What works, verified 13th run:
  * knomit_explain accepts ANY FULL 40-char commit as the `commit` anchor and rewinds the file to
    that point — the anchor does NOT have to be a commit from that file's own history. So: take a
    full SHA off any recent fact's history, anchor the OLD crawl-state path at it, and you get
    crawl-state as of that moment plus a history page of FULL SHAs to continue with.
  * Anchoring the old path with NO commit returns the 7th run (mainline HEAD for that path is
    PR #2, 43d32e59c1f26070ac9763f540474b58b4d7ea32). Runs 8-12 are NOT reachable that way — they
    are behind PR #3. Anchor at a PR #3 commit to reach them.
  * Each history page returns THREE revisions; stepping to the oldest of the three SKIPS two.
    Anchor at EVERY commit. Each anchor reveals the next two full SHAs, so it chains cleanly.
  * Runs 10 and 11 have TWO revisions each on the same day — revision count != run count.
FULL SHAs for the orphaned chain, newest first, so no future run has to rediscover them:
  e77323d4e609bfebc7fb25be633ff3d277789b7a  (12th run, final pre-deletion)
  d20068650ab37c520f5aa2e2fdf39b4d6773faf5  (11th run)
  e780b5c4ca4813ccb2d1508de79705ffd98fb4db  (11th run, earlier)
  260e885d6a638410b946ab770631d0acda398dd5  (10th run)
  48f3f4e0e1e3a237931011151301633a3e3e2aa8  (9th run)
  ba4927603c996ea49d983ab0a84ddd64af98f2a0  (8th run)
  9b0c45d4973cc3f10c0cda3ae76a4dec84480cb5  (7th run) = merge 43d32e59c1f26070ac9763f540474b58b4d7ea32
  37d4b6ed14b7dfcf1cdd74167f6284762c982bbe  (6th run) = merge b7e94506fcb1189afb304a129fa25099e745152b
  f673d976c9f634d4e2ea40e8fa4a03e6eebec821  (5th run)
  7dc18043e76d627e6ab6450ca5b02f4549d94f7f  (4th run)
  57589a5996fda5c2c6798a9ff630e349655e1d1e  (3rd run)
  88499d53ff2aaf1b7e0a0cc0afd53a97801b3830  (2nd run)
  e9152ff3363bdd1620c5f9d4107ff55c76f2e433  (1st run)
  e99e5692c20008db6651024e3639fbc722adbab3  (init, empty body)
STILL FOR A HUMAN: the lineage is split and no job can rejoin it. ~195 distinct URLs total.
DO NOT RUN knomit_review SCOPED TO domain=agentic-engineering — that is what deleted the fact.
The job-state facts and the SPEC MIRROR all carry that domain tag and become dedup-eligible;
crawl-state and crawl-sources are textually similar, which is what the dedup pass latched onto.
Answering "keep" inside a work item is NOT protection — the merge happened outside any item.

OWASP GenAI PDF REPORTS — STATUS AFTER THE 13th RUN:
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
    download id 56857. Chapters NOT mined: the ten per-entry chapters themselves (only the letter
    from the leads and the What's New chapter were written up). LLM03:2026 Excessive Agency
    (p23-26) and LLM08:2026 Hidden Context Exposure (p46-49) are the two most relevant to this
    pack and are UNREAD in detail. Appendix A coverage matrices (p58-105) map to ASI 2026, DSGAI
    v1.0, MITRE ATLAS v2026.06, ATT&CK v19.1, CWE 4.20, NIST AI 600-1, NIST AI RMF, CSA AICM v1.1
    and AIVSS v0.8 — that is a large pre-done cross-framework mapping and is worth one pass.
STILL UNREAD, all named as companion resources and all HIGH PRIORITY:
  Solutions Landscape – Red Teaming Taxonomy (Jun 2026)  <- NEW, seen 13th run
  Securing Agentic Applications Guide 1.0        (threat taxonomy -> architecture patterns + controls)
  Multi-Agentic System Threat Modeling Guide 1.0
  Agent Name Service (ANS) v1.0                  (pairs with discovery fact 8b32c15a)
  A Practical Guide for Secure MCP Server Development
  CheatSheet — Securely Using Third-Party MCP Servers 1.0
  Agentic AI Solution Landscape
  OWASP AIBOM / AIBOM Generator
  GenAI Data Security Risks & Mitigations
  GenAI Red Teaming Guide
  ASI Exploits & Incidents Tracker — the GitHub repo URL is footnote 19 of State of Agentic AI and
    has still NOT been captured. The visual explorer (owasp-agentic-ai-security-incidents.lovable.app)
    is in the list above and has STILL NEVER BEEN FETCHED across two runs. Rank-2 material.
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-a-hands-on-companion-to-the-owasp-genai-security-project/

*** MCP 2026-07-28 — TRIPWIRE CHECKED 13th RUN, STILL UNCHANGED ***
Still 2026-07-28, no movement since the 11th run. Check EVERY run anyway; cheapest high-value
fetch in the pack. The versioning page also now spells out the negotiation model in prose
(per-request io.modelcontextprotocol/protocolVersion in _meta, MCP-Protocol-Version header on
Streamable HTTP, UnsupportedProtocolVersionError, optional server/discover) — consistent with
what 031dab74 already says, no correction needed.
STILL UNREAD in this revision, in rough value order:
  /specification/2026-07-28/server/discover        (the mandatory RPC; referenced by 3 facts, never read)
  /specification/2026-07-28/basic/index#meta       (the _meta contract everything now rides on)
  /specification/2026-07-28/basic/authorization/security-considerations
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/versioning       (negotiation + backward-compat with 2025-11-25)
  /extensions/tasks/overview and /extensions/apps/overview
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude)
NOTE for a human: Appendix A on disk still says "MCP's current revision is 2025-11-25". WRONG
since the 11th run. Jobs cannot edit the disk copy.

*** FEEDS SWEPT 13th RUN (first run after a NINE-DAY gap — the longest in the pack's history) ***
The nine-day gap finally made a feed sweep pay, after eight runs of same-week sweeps returning
nothing. This is the cleanest evidence yet for the standing rule: SWEEP FEEDS WHEN DAYS HAVE
PASSED, NOT WHEN HOURS HAVE.
  modelcontextprotocol.io/specification/versioning — unchanged (tripwire).
  anthropic.com/engineering — swept. NOTHING new; newest is still april-23-postmortem (Apr 2026).
    Unread back-catalogue unchanged: AI-resistant-technical-evaluations, building-c-compiler,
    contextual-retrieval, swe-bench-sonnet, desktop-extensions.
  genai.owasp.org — swept. Surfaced the LLM Top 10 2026 (Aug 3). HIGH YIELD.
  simonwillison.net/tags/llms/ — swept, ~22 posts in the window. Best POINTER feed in the pack;
    it is how the whole incident cluster below was found.
  microsoft.com/en-us/research/blog — swept. THREE unread agent posts, all new:
    /orchard-an-open-framework-for-scalable-agentic-ai/            (Aug 3 2026)
    /echoverse-deep-evolving-environments-for-computer-use-agents/ (Jul 30 2026)
    /evolib-turning-experience-into-evolving-knowledge/            (Jul 30 2026)
    This feed is 2-for-2 on high-yield sweeps. Keep it at rank 5 or promote it.
  metr.org/blog — FIRST EVER ARTICLE-LEVEL FETCH IN 13 RUNS. It had sat in the recurring list
    since run 1 with only an index fetch, i.e. UNREAD, not up-to-date — the same defect the 11th
    run found on four other feeds. VERDICT AFTER READING: LOW YIELD FOR THIS PACK, and the reason
    is structural rather than topical. METR publishes evaluation-governance and policy review, and
    its one directly-relevant post (2026-03-25, red-teaming Anthropic's internal agent monitoring)
    states that the 26-page technical report is REDACTED — "a redacted version was shared with a
    subset of METR staff" — so attack methods, detection rates and design takeaways are all
    withheld. No fact written. Two posts remain plausibly useful and are unread:
    /blog/2026-07-28-investigating-ai-propensities-after-incidents/ and
    /blog/2026-06-26-gpt-5-6-sol/ (predeployment eval of the model in the AISI incident).
    DEMOTE metr.org to rank 17 — check it, but expect governance prose, not engineering numbers.

*** THE 13th RUN'S MAIN FIND: AN EVAL-CONTAINMENT INCIDENT CLUSTER, AND TWO NEW RANK-2 FEEDS ***
Four independent eval-environment containment failures were disclosed 2026-07-21..08-05, by four
organisations. This produced 7 new facts plus a substantial update to bcbf13c2. Primary sources:
  https://www.anthropic.com/news/investigating-incidents-cybersecurity-evals   (Jul 30)
  https://openai.com/index/third-party-cyber-evaluations-involving-openai-models/ (Aug 4, BROWSER ONLY)
  https://www.aisi.gov.uk/blog/incident-report-unsanctioned-agent-behaviour-during-cyber-testing (Aug 5)
  https://simonwillison.net/2026/Aug/7/openai-timeline/  (secondary; summarises a Black Hat talk)
TWO FEEDS ADDED to the recurring list on the strength of this, both RANK 2:
  www.aisi.gov.uk/blog — UK AI Security Institute. Publishes PRIMARY incident reports on agent
    behaviour during evaluation, with timelines, control inventories and stated remediations.
    This is exactly the rank-2 material the pack ranks highest and it had never been seen.
  openai.com/index — OpenAI now publishes primary security post-mortems here (Security tag).
    WebFetch gets 403; use the browser. Note the /news/ vs /index/ split: Anthropic's postmortems
    are on anthropic.com/news and anthropic.com/engineering, OpenAI's on openai.com/index.
UNREAD AND WANTED NEXT RUN, all from this cluster:
  openai.com "Responding to the next frontier of critical cyber capabilities" (Aug 7 2026) — linked
    from the Aug 4 post's "Keep reading" block. MY GUESSED SLUG 404'd
    (/index/responding-to-the-next-frontier-of-critical-cyber-capabilities/); get the real href off
    the Aug 4 page with javascript_tool rather than guessing. Guessed slugs have now 404'd on
    cognition (5th run), strands (3rd-7th), adk (2nd) and openai (13th) — ALWAYS pull the href.
  https://www.cnn.com/2026/08/05/tech/meta-ai-hacking — a Meta model reportedly also hacked a
    company during testing. If true this is a FIFTH lab in the cluster. Secondary; find the primary.
  https://www.anthropic.com/news/investigating-incidents-cybersecurity-evals is on /news/, not
    /engineering/ — anthropic.com/news is NOT in the recurring list and probably should be.
  Irregular is writing a white paper on containment for cyber evals (named in the OpenAI post) —
    watch for it; it is aimed squarely at this pack's subject.
  simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with MCP transport fact 3afa31af),
    the-tokenpocalypse (404media), /2026/Aug/2/open-letters/.

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

YIELD RANKING as of the THIRTEENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES. modelcontextprotocol.io/specification/versioning plus the
     /deprecated registry. One cheap fetch caught a protocol revision that invalidated parts of five
     facts. Spec pages are dated, authoritative, and change underneath you silently. EVERY run.
  2. PRIMARY INCIDENT POST-MORTEMS, wherever they appear — now including aisi.gov.uk/blog,
     openai.com/index, anthropic.com/news, and the OWASP ASI incidents tracker. Validated FOUR
     times now; the 13th run's cluster was the single highest-yield thing in the run. When one
     appears for an incident already in the kb, fetch it and re-verify; do not assume the kb is right.
  3. OWASP GenAI PDF REPORTS. Four read across three runs for 14 facts + 3 corroborations, and the
     read route is now solved twice over (see top). The companion guides list above is still the
     single richest unread block in this file. HIGH PRIORITY.
  4. MCP 2026-07-28 remaining spec pages (list above). server/discover first — three facts reference
     it and none has read it.
  5. microsoft.com/en-us/research/blog — 2-for-2 on sweeps, 3 unread agent posts queued above.
     Scan for agent/memory/skill/eval; skip health, quantum, diffusion.
  6. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. Index itself is quiet since Apr 2026.
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
     primary post-mortems, and it is how the 13th run found the whole incident cluster. Its VALUE
     IS THE LINKS, not the posts: read the index, follow the primaries, rarely read Simon himself.
 15. latent.space/archive — interview format. Unread: /p/aiewf26trends, /p/modal2026, /p/poolside,
     /p/chatgpt-work. Skews discussion-level; verify measurements exist before a full read.
 16. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 17. metr.org/blog — DEMOTED 13th run after its first article-level read. Governance and policy
     review; the one on-topic post has its technical report redacted. Check, expect little.
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

STALENESS-POOL NOTE (updated 13th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, and (13th run) afce1dae, 4b0261d0, 052c2b66, f78a326a,
38c06627.
THE EARLIEST-COMMITTED AXIS WORKS — USE IT. The 12th run proposed sampling the oldest facts rather
than the least confident, because the tier-0/tier-1 backfill was written confident, from one source
each, in the first run, and never revisited. The 13th run ran that axis for the first time: all five
sampled were first-run facts (committed 2026-07-26), none had ever been checked, and it found TWO
citation-fidelity defects in five — the same 40% hit rate the confidence axis was getting, on a pool
the confidence axis cannot reach. Keep alternating the two axes.
Nothing in this kb is yet older than 90 days. AVOID SAMPLING kb/principles/**.

WHAT THE STALENESS PASS ACTUALLY FINDS — SIX RUNS OF EVIDENCE, and it is the single most reliable
defect-finder in this job. It is NOT finding stale facts. It finds CITATION-FIDELITY defects in facts
whose underlying claims are correct:
  ninth   — 56986e8f: a paraphrase wearing quote marks.
  tenth   — c93d93ee: an overclaiming gloss attributed to the source.
  tenth   — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh— 96ebc34e: BOTH at once, and the gloss reversed the blame (model choice vs tool docs).
  eleventh— c858a924: WRONG ACTOR — 'independent auditors' were two LLM judges, not humans.
  twelfth — 30869b36: a pack gloss wearing quote marks (the 'combined surface area' line).
  twelfth — c436422a: WRONG TERMS attributed to the source (brain/hands/session).
  thirteenth — f78a326a: WRONG TERM ('raw accuracy' for Husain's 'raw agreement') AND a single
    reported instance generalised into a rule ('2-3 iterations typically suffice' from one case of
    three, where the source explicitly says 'Your mileage may vary').
  thirteenth — 38c06627: MISATTRIBUTION ACROSS A FACT'S OWN TWO REFS — the self-preference and
    agreement figures were checkable only against eugeneyan, not applied-llms, so a check pointed at
    the wrong ref would have 'confirmed' nothing. Plus 'measurably reduced' for a source that says
    'can reduce' with no measurement. NEW DEFECT CLASS: when a fact has 2+ refs, verify WHICH ref
    carries WHICH claim, and say so in the body.
CHECKLIST — verify all seven explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to; (5) are the TERMS attributed to the source
  actually the source's terms; (6) refs classification (local vs external) and `sources` counts;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number — and is a single
  reported instance being presented as a general rule.
