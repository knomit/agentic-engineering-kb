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

*** kb/principles/** IS READ-ONLY TO JOBS — FOUND THE TENTH RUN, AFFECTS THE STALENESS PASS ***
knomit_update on a fact under kb/principles/ fails with:
    validation "must-have-designer-entity" at principles: principles must be authored via
    /knomit-principle (entities must include 'designer')
Pipeline-minted synthesis facts (origin: distilled or discovered) live under kb/principles/ and
legitimately have no 'designer' entity. Do NOT add one to get past the validator — it would
falsely assert designer authorship, and origin is immutable, so there is no honest fix from
inside a job. Affected facts, all unfixable from here: 1feacc9e, 2c0e8e7c, b9b45ff5, 0f260eea,
6ec9b2b6, 00d3ef19, 28ba65db, c2f12069.
PRACTICAL EFFECT ON THE STALENESS PASS: you can read and verify these, but you cannot record
the result — no confidence bump, no correction, no note. Sampling them spends budget for no
durable change. PREFER OTHER TOPICS unless a human resolves this. The tenth run verified
c2f12069 (durability substrate) as CONFIRMED and could not write it; the check will have to be
redone by whoever fixes this.
THIS ALSO MAKES THE REF-COMPLIANCE ISSUE BELOW UNFIXABLE, not merely unflagged — see below.

*** SPEC-COMPLIANCE ISSUE, escalated by the tenth run, for a human to decide ***
Synthesis facts minted by the discovery/distill pipelines carry only LOCAL refs and no external
URL — e.g. kb/principles/ai/rag/evaluation/28ba65db, kb/principles/ai/agents/architecture/
c2f12069. The spec says every fact MUST carry at least one URL in refs. Their grounding is real
(it flows through the local refs, which do carry URLs), so this is arguably fine for synthesis
specifically, but the spec has no such carve-out. The ninth run flagged it. The TENTH run tried
to FIX it on c2f12069 — listing the external URLs already reached through its local refs
alongside them, which changes grounding not at all — and the edit was REJECTED by the
designer-entity validator above. So a job cannot close this. Either the spec needs the carve-out
written in, or the pipelines need to propagate external refs at mint time, or kb/principles/
needs to accept job edits to pipeline-origin facts. Not retracted; the facts are sound.

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
CAVEAT, settled across four runs: on builder.aws.com the FIRST get_page_text after a navigate
SOMETIMES returns a stub ending in the literal string 'Loading article'; call it again and the
full text is there. Sixth run: reproduced every time. Seventh: zero times in five fetches.
Eighth: once. NINTH: zero times in four fetches. Genuine but intermittent race, plausibly
cold-cache-related. Always check whether the text ends at 'Loading article' and re-call if so.
Never conclude 'blocked' from one empty call.
To pull links/hrefs off an index, use
    mcp__claude-in-chrome__javascript_tool with a querySelectorAll expression —
    mcp__claude-in-chrome__find returns element refs but NOT hrefs.
NOTE (tenth run): large learn.microsoft.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned. This is normal, not a failure — the
multi-backend gateway guide (6,881 words) and the agent-design-patterns page (7,133 words) both
did this. Ask a NARROW prompt if you want the answer inline instead.

*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY (ninth run) ***
Two of the four titles the eighth run ranked as highest-value turned out to have NO PROSE BODY.
The page renders a title, a one-line abstract, an author and a date, and nothing else — they are
landing pages for recorded conference talks. Confirmed video-only, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl  ('Formerly presented
     by Becky Weiss' — that byline phrasing is the tell)
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Both are 'Published Jun 12, 2026', as are leader-election and lunch-rush which DO have full
prose — so publication date does not predict it. Budget one cheap fetch per article and abandon
immediately if the text ends right after the byline.

*** AWS BUILDERS' LIBRARY — COMPLETE ARTICLE ENUMERATION (30 of 30, fully expanded on the
    seventh run; this is the WHOLE catalogue, no more pagination) ***
Article URLs are opaque content IDs and CANNOT be guessed from titles. Form the URL as:
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
  leader-election-in-distributed-systems | 3Ev0vH0hfkcUizISUWYTvHibtcp             (2 facts, ninth run)
  resilience-lessons-from-the-lunch-rush | 3Ev17ZWA9QX88MmoaULAKevIR8H             (1 fact, ninth run)

VIDEO-ONLY, NO PROSE — do not re-fetch (2 of 30):
  amazons-approach-to-failing-successfully | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm

UNREAD (12) — reliability first, CI/CD last. Expect LOWER yield than the read set: lunch-rush
was largely a survey of articles already mined (1 new fact, 3 corroborations), and 6 of these
are CI/CD and deployment, further from this pack's centre.
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
30-item catalogue and appear to be retired — 'Caching challenges and strategies' and 'Static
stability using Availability Zones'. Do not keep hunting for them. Static stability IS covered
in substance inside smaller-service-in-control, and caching's failure modes inside
constant-work and lunch-rush, so neither gap is as bad as it looked.

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

AZURE ARCHITECTURE CENTER — doc URLs harvested from the ai-ml index (eighth run). The index
itself is a pure catalogue with no guidance of its own; do not re-fetch it. Prefix every one
with https://learn.microsoft.com/en-us/azure/architecture/ai-ml/
  .../guide/ai-agent-design-patterns                       (READ — fact c926c07b; re-verified
      tenth run for c1bbf73f, dated 2026-02-12 refreshed 2026-05-12)
  .../guide/manage-foundation-models-lifecycle             (READ, ninth run — updated 27652a82)
  .../guide/azure-openai-gateway-guide                     (READ, tenth run — 2 facts + upd 5ad0fb45)
  .../guide/azure-openai-gateway-multi-backend             (READ, tenth run — 4 facts + upd 27652a82;
      the single densest page in this seam so far, 6,881 words, heavily prescriptive)
  .../guide/azure-openai-gateway-monitoring                <- LAST of the gateway trio, still unread
  .../guide/rag/rag-solution-design-and-evaluation-guide   <- NEXT RUN, plus per-phase pages:
      rag-preparation-phase, rag-chunking-phase, rag-enrichment-phase,
      rag-generate-embeddings, rag-information-retrieval, rag-llm-evaluation-phase
  .../guide/secure-multitenant-rag
  .../guide/genaiops-for-mlops

YIELD RANKING as of the TENTH run — spend the budget in this order:
  1. PRIMARY INCIDENT POST-MORTEMS, wherever they appear (huggingface.co/blog, vendor
     engineering blogs, simonwillison as a pointer to them). VALIDATED TWICE NOW. The ninth run
     promoted this on the strength of the HF timeline; the tenth run's two Anthropic postmortems
     produced 6 facts from 2 fetches and established a whole new axis for the pack (the SERVING
     STACK degrades a pinned model while evals stay green). Across those two postmortems, SIX
     regressions and not one was a weights change. When a primary post-mortem appears for an
     incident already in the kb, fetch it and re-verify — do not assume the kb version is right.
  2. Azure Architecture Center doc pages listed above — PROMOTED from 3. Best-validated unread
     seam in the pack: the gateway pair gave 5 new facts + 2 updates from 2 fetches. Microsoft
     doc pages are prescriptive, structured, dated, and on 180-day update cycles, which clears
     this pack's bar far better than vendor blog posts. The six-part RAG series is the largest
     coherent unread block anywhere in this file — take it next.
  3. anthropic.com/engineering — still strong, and BOTH postmortems are now read. STILL UNREAD:
     eval-awareness-browsecomp, AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. The first two look strongest.
     Index re-checked 2026-07-29: nothing newer than how-we-contain-claude.
  4. builder.aws.com Builders' Library — still good but visibly exhausting: 16 of 30 read for
     55+ facts, but the ninth run got only 3 facts from 4 fetches (2 video-only, 1 survey
     article). The remaining 12 skew CI/CD. Read resilient-services and resilient-serverless,
     then reassess whether the seam deserves further budget.
  5. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread
     TECHNICAL posts: coding-agents-101-the-art-of-actually-getting-things-done, swe-grep,
     blockdiff, devin-annual-performance-review-2025, evaluating-coding-agents,
     making-fable-cheaper-than-opus, devin-fusion, swe-1-7,
     measuring-open-source-model-trustworthiness, introducing-devin-security-swarm,
     frontier-code and frontier-code-1.1, ai-productivity.
     Skip partnership/funding/office/acquisition posts — about half the feed.
  6. huggingface.co/blog — INDEX SWEPT FOR THE FIRST TIME on the tenth run, and it paid: it
     surfaced ibm-research/model-routing-is-simple-until-it-isnt (READ, 1 fact with real
     AppWorld cost measurements) plus security-incident-july-2026 (Jul 16, HF's own FIRST
     disclosure of the intrusion — UNREAD, but the Jul 27 technical timeline already read by
     the ninth run supersedes most of it; low priority). Confirmed as a real recurring seam,
     not a one-article fluke. Scan for incident, infrastructure and engineering posts; SKIP
     model/dataset announcements, which are most of the feed. Note posts can be namespaced
     under an org (huggingface.co/blog/<org>/<slug>) — those are easy to miss.
  7. sourcegraph.com/blog — real measurements, not opinions. Unread:
     compliance-first-ai-proving-agent-provenance (Jul 27),
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone (Jun 16),
     owning-a-codebase, the-hidden-cost-of-code-that-nobody-touches.
  8. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
  9. simonwillison.net/tags/llms/ — high volume, mostly link-blogging, but the fastest POINTER
     to primary post-mortems. Scan for incidents and security; skip model-release commentary.
     Index re-checked 2026-07-29. discovering-cryptographic-weaknesses-with-claude is now READ
     (fact 1a3b1ccf: 60h, ~$100k). Unread: the-first-known-runaway-ai-agent (Jul 23),
     are-ai-labs-pelicanmaxxing (Jul 22), thomas-ptacek (sandbox escapes), bad-codex-bug
     (file deletions), relay-market (Jul 26, token-reseller fraud). Nothing new since Jul 28
     except a TIL on adding MCP servers to Claude/ChatGPT, which is below the bar.
 10. latent.space/archive — interview format but yields thresholds. Unread: /p/modal2026,
     /p/gray-swan, /p/aiewf26trends.
 11. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
     3-years-of-graph-engineering-with-langgraph re-verified live 2026-07-29 (dated 2026-07-22).
 12. embracethered.com/blog — low volume, high value, security only.
 13. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.

dead or unreadable, do not keep re-fetching blind:
  block.github.io/goose -> goose-docs.ai (old host serves only a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... (see STRANDS DOC URLS above).
  NOTE: builder.aws.com and the Vectara leaderboard were BOTH listed here and neither was
    ever dead. See the warning at the top of this file before adding anything to this list.

checked and low-yield for this pack (do not deprioritise permanently, but do not lead with
them): research.google/blog — recent output is health/quantum/diffusion, nothing on agents,
tools, or evals. microsoft.com/en-us/security/blog — one good agent-identity post (re-verified
live on the tenth run, 2026-07-16, every claim confirmed), otherwise threat intel unrelated to
building agents.

TIER 6 GITHUB READMEs — CLOSED OUT, verdict consistent across two runs. Checked seventh run:
microsoft/autogen, NirDiamant/GenAI_Agents, strands-agents/sdk-python. Checked eighth run:
anthropics/claude-cookbooks, NirDiamant/RAG_Techniques, microsoft/semantic-kernel. Five of
those six returned catalogue- or marketing-level text below this pack's altitude bar. The ONLY
two things worth having from the whole tier were MAINTENANCE-STATUS notices — autogen's
maintenance mode and semantic-kernel's 'now Microsoft Agent Framework' succession — which
generalises: a repo README is worth a fetch for LIFECYCLE STATUS and nothing else. Do not spend
more budget here; if a repo matters, go to its DOCS site. Only remaining tier-6 item: the
x1xhlol INDIVIDUAL prompt files. Frame anything from those as 'this harness's published prompt
does X', never as 'the correct approach is X'.

STALENESS-PASS POOL NOTE (updated tenth run): the low-confidence pool is shallow and runs had
begun re-sampling the same facts. Tracked as checked so far — cb98732e, 27652a82, 111f8b2c,
2b74037b, 5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d,
d4e3b247, bcbf13c2, d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9,
28ba65db, and (tenth run) c93d93ee, c7290868, c1bbf73f, 48c4e555, c2f12069.
The three facts the ninth run listed as UNCHECKED are now all done. Nothing in this kb is yet
older than 90 days, so confidence remains the only sampling axis; when the pool is exhausted,
switch to age per the spec. AVOID SAMPLING kb/principles/** — see the write-block at the top.

WHAT THE STALENESS PASS ACTUALLY FINDS — three runs of evidence, worth acting on. It is NOT
finding stale facts (nothing here is 90 days old yet). It is finding CITATION-FIDELITY defects
in facts whose underlying claims are entirely correct:
  ninth run  — 56986e8f: a paraphrase wearing quote marks.
  tenth run  — c93d93ee: an overclaiming gloss ('a loop is a DCG with ONE node') attributed to
               the source, which said only 'a loop is just a directed, cyclic graph'.
  tenth run  — c7290868: INVERTED CAUSATION. Source: managers are prescriptive because they were
               TRAINED on small-scoped delegation, and shallow codebase context makes that
               BACKFIRE. The fact had said shallow context CAUSES the prescriptiveness, and then
               drew a diagnostic inference that pointed at the wrong remedy.
So: when re-checking a fact, verify QUOTATION BOUNDARIES and CAUSAL DIRECTION explicitly, not
just whether the claim is still true. An accurate claim with the causality reversed is worse
than a stale one, because it silently redirects the reader's fix.
