---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-14 (seventeenth run; started 08-13, spanned the date boundary). Two days after the
16th. The feed sweep owed for three runs was finally attempted — and came back near-empty, which is
itself the result: see "sweep" below.
*** A POST-RUN REVIEW PASS WAS RUN AFTER THE FACTS WERE WRITTEN AND FOUND THREE DEFECTS IN THIS RUN'S
OWN OUTPUT, ONE OF THEM IN THE CENTRAL EVIDENCE OF A NEW FACT. See REVIEW PASS at the foot. Findings
below have been corrected in place; do not read this file against an older memory of it. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***

=== HISTORY WALK: READ THIS FIRST, THERE IS A REAL GAP AND IT IS NOT MINE TO FIX ===
REVISIONS READ: 2.
  3c6323cd (HEAD, 2026-08-12T21:25:35Z) — the 16th run's body.
  8b9a768d (2026-08-12T00:27:10Z)       — the 13th run's body, carrying the AUTHORITATIVE 190-URL union.
more_available was FALSE at 8b9a768d. The walk terminated on the API's own signal, not on an assertion.

*** THE GAP. *** HEAD's body names a backfill floor at e61629fc (197 URLs) and revisions 8be9e4de and
5ab895cf for the 15th run. NONE OF THOSE COMMITS RESOLVE. I probed e61629fc and 5ab895cf explicitly
by passing them as `commit`; both returned "could not read ... at <hash>". The mainline now carries
SQUASHED MERGE COMMITS ("Merge pull request #8 from knomit/agent/...", "#6 from knomit/knomit") and
the per-run agent commits the 15th and 16th runs recorded are no longer addressable on this path.
CONSEQUENCE: the 14th and 15th runs' bodies are UNREACHABLE. Their URLs survive only as the
source-level descriptions carried forward in HEAD's status section, not as an enumerable list.
WHAT I AM CONFIDENT OF: 190 URLs enumerated in 8b9a768d + 10 enumerated in HEAD = 200 URLs I can
name. HEAD asserts the true total is 216, i.e. ~16 URLs from the 14th and 15th runs that I cannot
enumerate. I did not re-fetch anything in that window, because HEAD's status section describes what
those runs read at source level (OWASP guides 49059 and 46950, the MCP basic/index work, three
openai.com posts) and I steered clear of all of it.
WHAT A FUTURE RUN SHOULD KNOW: abbreviated hashes recorded in a BODY are not durable addresses under
this repo's merge strategy. If per-run commits keep getting squashed, the walk will keep bottoming
out at merge boundaries. Record full 40-char hashes from `history.revisions` if you record any at all
— and do not trust a body's self-reported floor over what the API actually returns.

*** SEPARATE FINDING FOR A HUMAN: A LIVE FACT WAS RETRACTED AND THREE FACTS STILL CITE IT. ***
kb/invariants/ai/agents/security/threat-taxonomy/4f5e9dfe.md — the pack's central ASI taxonomy fact —
returns `deleted: true` from knomit_explain and is ABSENT from the query index, while 483263c5,
c02ac546 and others still carry kb:// refs to it. This matches the knomit_review dedup hazard the
13th run warned about ("DO NOT RUN knomit_review SCOPED TO domain=agentic-engineering"). I did NOT
resurrect it — this run rebuilt that ground from the PRIMARY document instead (703147ba), which is
better sourced than the retracted secondary-sourced version. But the dangling refs remain.

recurring-feed indexes swept (FOUR, the first real sweep since the 13th run):
https://api.github.com/repos/.../contents/docs/specification  (MCP tripwire — UNCHANGED. 2024-11-05,
  2025-03-26, 2025-06-18, 2025-11-25, 2026-07-28, draft. SEVENTH consecutive run unchanged.)
https://www.anthropic.com/news/     (NOTHING since 2026-08-07 "Improving Fable 5's biology
  safeguards", a model-safety product post, below the bar. Newest on-topic item is still 07-30.)
https://www.aisi.gov.uk/blog/       (NOTHING since the 08-04 incident report, already read.)
https://openai.com/index/ via WebSearch  (SIX previously-unknown post URLs — see crawl-sources.)
SWEEP VERDICT: three of four feeds were genuinely quiet across the 5-day window since the 13th run's
sweep. The sweep was owed and is now paid; the backlog anxiety in the last three runs' notes was
largely unfounded. Do NOT re-sweep anthropic/news or aisi.gov.uk for at least several days.

articles newly crawled (5):
https://genai.owasp.org/download/52117/?tmstv=1765059207        <- THE MAIN EVENT, 3 facts
https://openai.com/index/the-next-evolution-of-the-agents-sdk/   <- 1 update (c436422a)
https://raw.githubusercontent.com/.../docs/docs/2026-07-28/learn/server-concepts.mdx
https://raw.githubusercontent.com/.../docs/docs/2025-06-18/learn/server-concepts.mdx  (diff pair)
https://raw.githubusercontent.com/.../docs/specification/2026-07-28/server/tools.mdx  <- staleness, 3 facts
re-read, not newly crawled: openai.com/index/hugging-face-model-evaluation-security-incident/
  (already cited by bcbf13c2; opened to check for a duplicate before writing one. It was right to check.)
re-fetched for the staleness pass only: langchain.com/blog/towards-automating-eval-engineering

errored / not obtained: NONE. No 403s, no 404s, no paywalls, no timeouts. modelcontextprotocol.io was
fully responsive — the 16th run's ECONNREFUSED was transient, recorded as such in fetch-routes.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FINDINGS ===

FINDING 1 — THE LONGEST-QUEUED ITEM IN THE PACK WAS ONE CURL, AND THE VALUE WAS NOT WHERE ANYONE
EXPECTED. The OWASP Top 10 for Agentic Applications 2026 sat unfetched for five runs. The list of ten
is the least interesting thing in it — this pack already had the names from secondary sources. The
value is the DISAMBIGUATION PROSE each entry carries, which encodes a STAGE AXIS: ASI01/04/07 are the
compromise, ASI06 its persistence, ASI08 its propagation, ASI10 the behavioural drift after it. The
document says so in its own words — "not the initial intrusion itself", "not the initial vulnerability
itself", "describes degradation after poisoning occurs" — and gives an explicit tie-breaker for ASI08:
file it there ONLY when the defect "spreads ... causing measurable fan-out". So four of the ten are one
incident at four stages, each with a different control set.
GENERALISE THIS: when a source is a LIST, the value is usually in what SEPARATES the items, not in the
items. Skim the enumeration, read the disambiguation.

FINDING 2 — AN INVERSION BETWEEN TWO OWASP DOCUMENTS THAT NEITHER STATES.
*** CORRECTED BY THE REVIEW PASS. The finding stands; the evidence I first gave for it did not. ***
Counting ASI tags across Appendix D's incident tracker (57 tags over 21 incidents, all 2025,
Mar-Oct): ASI10 appears 2 times and ASI08 3 times, the two rarest. Cross-referenced against the
AIUC-1 crosswalk already in the kb (07eec7ff), ASI10 is named in 4 of its 8 control-gap areas and
ASI08 in 3 — MORE THAN ANY OTHER ENTRY. So the thinnest incident evidence sits where the controls are
most consistently missing.
WHAT I GOT WRONG FIRST, recorded so nobody re-derives it: I originally argued this from the
crosswalk's four "no dedicated requirement at all" gap areas, claiming ASI08 and ASI10 were "two of
the three" entries in that bucket. Those four areas actually touch SIX entries — ASI02, ASI03, ASI05,
ASI07, ASI08, ASI10 — and two of them (ASI02, ASI05) are the MOST common entries in the tracker.
Counted that way the correlation vanishes entirely. Only the frequency-across-all-eight-gap-areas
measure shows it. The "three entries" figure was imported unexamined from the retracted 4f5e9dfe's
remark that gaps "cluster" at ASI07/ASI08/ASI10 — a DIFFERENT claim, and ASI07 turns out to appear in
only ONE gap area, so that cluster framing is itself loose.
AND A COUNTER-EXAMPLE THAT KEEPS IT HONEST: ASI09 is also sparse (3 tags) but appears in ZERO gap
areas. Low incident count does NOT imply missing controls as a general rule; the claim is specific to
ASI08 and ASI10, and ASI09 is why it must stay specific. All of this is now in 8cf06566.
This CUTS AGAINST the existing 6c0c742e reading — that a low incident count can mean a category is
well DEFENDED. Both facts left standing, with the deciding variable (does instrumentation exist?)
named in each.

FINDING 3 — *** THE 16th RUN'S "DEAD PATH" WAS NEVER DEAD, AND ITS SUCCESSOR WAS THE WRONG PAGE. ***
The 16th run recorded modelcontextprotocol.io/docs/concepts/tools as GONE and its content as having
moved to docs/docs/<rev>/learn/server-concepts.mdx, and queued three facts as ref-rotted. Both wrong:
  * The old URL answers HTTP 200 and REDIRECTS to /specification/2026-07-28/server/tools. Tested with
    `curl -o /dev/null -w "%{http_code} %{url_effective}"`.
  * learn/server-concepts.mdx does NOT contain the material. Grepped for `annotations`,
    `outputSchema`, `structuredContent`, `isError`: ZERO hits for all four. The tool contract lives at
    docs/specification/<rev>/server/tools.mdx.
The 16th run could not test the redirect (host was down) and inferred the successor from a plausible
title. THE RULE, now in fetch-routes: a redirect target is evidence, a guessed successor is not —
confirm a page move by GREPPING THE NEW PAGE FOR THE CONTENT. Eighth consecutive time a source
recorded as dead/blocked/moved turned out fine by another route.

FINDING 4 — A TABLE YOU MUST NOT QUOTE IS STILL A TABLE YOU MAY COUNT — BUT BOUND THE REGION.
Column interleaving destroys row/cell PAIRINGS, not the cells, so token frequency over a table region
is trustworthy where pairings are not. That is the basis of Finding 2. THE REVIEW PASS ADDED THE
SHARP EDGE: my first count ran to an eyeballed line number that overshot Appendix D into the
ACKNOWLEDGEMENTS, whose entry-lead roster lists ASI01-ASI10 once each — adding exactly one phantom tag
to every entry. Total 67 vs the true 57. The contamination was UNIFORM, so the ranking survived and
the finding held, but every absolute number was wrong. BOUND A COUNTING REGION ON THE HEADING THAT
FOLLOWS IT, not on a line number you guessed. Recorded in fetch-routes.

FINDING 5 — A NEGATIVE GREP IS NOT PROOF OF ABSENCE WHEN THE SOURCE IS A PDF. Grepping for "Agent
Behaviour Hijack" returned nothing and I nearly recorded that the variant did not exist. It does —
wrapped as "Agent Behaviour\nHijack". Mirror image of the 15th run's 0720e9d7 defect, where a wrap was
silently reconstructed INTO a literal. Same root cause, opposite direction.

FINDING 6 — CHECKING FOR A DUPLICATE SAVED A WASTED FACT. HEAD's queue said the OpenAI/Hugging Face
primary account was still being watched for. It is NOT — bcbf13c2 already cites it, and the correct
slug for the post the 13th run 404'd on is also already in that fact's refs. Still outstanding: the
separate TECHNICAL REPORT, and the METR + Redwood joint assessment (contracted, confirmed NOT
published as of 2026-08-14). The queue had compressed three artifacts into one line.

FACTS WRITTEN (3 new, 5 updated, 0 retracted):
  NEW —
    kb/invariants/ai/agents/security/threat-taxonomy/agentic-top-10-2026/703147ba  (the ten entries
      from the PRIMARY, the many-to-many T-mapping, the T12 DOUBLE-NAMING trap, Least-Agency.
      ASI09 MAPPING CORRECTED by the self-review.)
    kb/decisions/ai/agents/security/threat-taxonomy/entry-boundaries/ba1b7aad      (the stage axis,
      the ASI08 measurable-fan-out tie-breaker, ASI08's five detection hooks, the tool-side
      ASI02/03/05 split, the ASI09-vs-ASI10 line. EXTENDED and a QUOTE FIXED by review.)
    kb/gotchas/ai/agents/security/threat-taxonomy/coverage-blind-spots/8cf06566    (the tracker
      frequency counts and the incident-evidence / control-coverage inversion. COUNTS AND CENTRAL
      EVIDENCE BOTH CORRECTED by the review pass — see Finding 2 and REVIEW PASS. conf 0.7.)
  UPDATED —
    c436422a  — INDEPENDENT SECOND VENDOR for harness/compute separation: OpenAI's Agents SDK reaches
      the same decomposition with the same three reasons, plus the Manifest workspace abstraction.
      Explicitly notes the TTFT numbers remain Anthropic's alone and are NOT corroborated.
      sources 1->2, conf 0.85->0.9.
    ee3bc7d3  — CONFIRMED against 2026-07-28, still a MUST, quoted verbatim. Added a SCOPE NOTE: the
      spec's MUST carries an "unless they come from trusted servers" carve-out that the title does
      not, so the title is a policy for the untrusted-server case. VERIFICATION SCOPE names what was
      not re-checked (the annotation field list).
    ca3382bd  — CONFIRMED verbatim. sources 2->1: both refs are pages of ONE specification.
    46eeb374  — CONFIRMED: protocol error (-32602) vs `isError: true`. sources 3->1, same reason.

CONTRADICTIONS: none between sources requiring a `decisions` fact. One cross-document tension handled
as a scoped refinement rather than a flattening (Finding 2 — 8cf06566 vs 6c0c742e, both standing,
deciding variable named). One INTERNAL contradiction found inside a source and recorded rather than
resolved: OWASP's own T12 carries two different names in one document (703147ba).

STALENESS PASS (5 sampled; primary axis SHARED-REF as split item 3 required. 5 confirmed, 3 ref
additions, 2 source-count fixes, 0 retracted. TWO fetches covered four facts):
  ee3bc7d3, ca3382bd, 46eeb374 — the three facts on the supposedly-dead MCP path. ALL THREE CONFIRMED
    against 2026-07-28 in ONE fetch. The premise of the sample (ref rot) turned out false — Finding 3.
    Refs were ADDED, never swapped. NOTE: the 16th run said TWO facts cite that path; there are THREE.
    46eeb374 was missed by that count.
  a5ade87d (conf 0.7) — CONFIRMED. Source live, no update notice. Both halves of the title verified:
    verifier gaming ("overciting irrelevant sources to receive full credit on the eval, claim an
    action it never took, exploit exposed answer material") and "the first verifier was rarely the
    final one". No change needed.
  c436422a — re-verified as part of the corroboration; the 14th run's brain/hands/session terminology
    correction still holds and was preserved verbatim.
  Nothing in the kb is yet older than 90 days.

=== REVIEW PASS (run AFTER the facts were written and after this record was first committed) ===
Three defects, all in THIS RUN'S OWN OUTPUT, none of which the in-run self-review caught:
  8cf06566 — CONTAMINATED COUNTING RANGE. 67 tags reported, true figure 57; every per-entry count
    inflated by exactly one. Cause in Finding 4. Ranking unaffected, absolutes all wrong.
  8cf06566 — WRONG EVIDENCE FOR A CORRECT CONCLUSION, and the worst defect of the run because the
    stated evidence actively CONTRADICTED the claim once counted properly (the "no requirement"
    bucket contains the two MOST common entries). Cause in Finding 2. A reader checking my citation
    would have concluded the fact was wrong, when the fact was right and the citation was wrong.
  ba1b7aad — A TENSE-ALTERED QUOTATION: I wrote "operating within its authorized privileges" inside
    quote marks; the source says "operates". Small, but it is the 56986e8f defect class again
    (paraphrase wearing quote marks) and it appeared in a fact written the same day the checklist
    warning about it was re-read.
WHY THE IN-RUN SELF-REVIEW MISSED ALL THREE: it checked facts against THE SOURCE DOCUMENT, and two of
these are defects in ARITHMETIC OVER the source and in a CROSS-DOCUMENT inference — neither is visible
by re-reading the page the fact cites. NEW SUB-RULE (17th): the self-review must RE-RUN ANY COMPUTATION
A FACT REPORTS (counts, ratios, "N of M") rather than re-reading the passage it came from, and must
RE-DERIVE ANY CROSS-DOCUMENT CLAIM from both documents, not from the memory of one.

=== SUGGESTED SPLIT FOR THE NEXT RUN ===
(1) DO NOT SWEEP THE FEEDS unless several days have passed. Three of four were empty. The MCP
    tripwire is near-free and should still run EVERY time.
(2) openai.com/index/introducing-aardvark/ — TOP PICK. An agentic security researcher, i.e. an agent
    DESIGN post from a frontier lab, and this pack has nothing on it. Then
    /index/unlocking-self-improvement-gpt-red/ (a METHOD post). Full catalogue in crawl-sources.
(3) FINISH THE OWASP AGENTIC TOP 10 — PDF already extracted, unmined sections listed in crawl-sources
    under id 52117. Best remaining: the "intent capsule" / "Intent Gate" mitigation patterns
    (ASI03-ASI07, ASI09), and Appendix C's mapping to the Non-Human Identities Top 10, a taxonomy
    this pack does not cover at all.
(4) MCP, remaining, ALL reachable by repo mirror: basic/authorization/security-considerations (named
    by 066a9dad, still TOP), basic/versioning, transports/streamable-http, server/utilities/caching,
    extensions/tasks + apps overviews, docs/<rev>/develop/clients/client-best-practices.
(5) OWASP companion corpus, still unread: Solutions Landscape Red Teaming Taxonomy, A Practical Guide
    for Secure MCP Server Development, CheatSheet — Securely Using Third-Party MCP Servers, GenAI Red
    Teaming Guide, Agentic AI Solution Landscape, OWASP AIBOM, GenAI Data Security.
(6) LLM Top 10 2026 per-entry chapters: LLM03 Excessive Agency (p23-26), LLM08 Hidden Context
    Exposure (p46-49). id 56857, file already extracted.
(7) THE MASEC reference list: NetSafe (arXiv 2410.15686) and chaos engineering for LLM MAS (arXiv
    2505.03096). Both report MEASUREMENTS, which is what 2508.09815 lacks. Pairs with 24e4552d.
(8) STILL WATCHING, three DISTINCT artifacts — do not conflate them again (Finding 6):
      (a) OpenAI's own TECHNICAL REPORT on the HF incident — promised "in the coming weeks" as of
          2026-07-21. Not published as of 08-14.
      (b) The METR + Redwood JOINT assessment — contracted and confirmed, not published as of 08-14.
          Watch blog.redwoodresearch.org (now in crawl-sources) and metr.org/blog.
      (c) Irregular's containment white paper.
    The primary OpenAI incident POST is already read and cited by bcbf13c2 — that item is CLOSED.
(9) The OWASP ASI incidents tracker at owasp-agentic-ai-security-incidents.lovable.app — SIX runs
    listed without a fetch. NOTE: Appendix D of the Top 10 PDF is a tracker with the same name and 21
    incidents; check whether the site is simply the same data before spending a browser session.
(10) FOR A HUMAN, NOT THE CRAWLER: 4f5e9dfe is retracted but still referenced by live facts. Either
    restore it or strip the dangling kb:// refs from 483263c5 and c02ac546.

=== PER-SOURCE STATUS AND QUEUE, as of the 17th run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

OWASP GenAI PDF REPORTS — STATUS:
  AIUC-1 Crosswalks (55pp)                                   READ (11th), 3 facts+1 upd
  AI Security Solutions Landscape Red Teaming Q2 2026 (15pp) READ (11th), 1 fact
  State of Agentic AI Security and Governance 2.01 (139pp)   READ (12th), 8 facts+1 upd
    ^ chapters still NOT written up: Enterprise Adoption Maturity Model (p53-62), Alignment with
      Top 10 Agentic (p61), Future Trends / What Remains Unsolved (p63-68); AI SBOM and Supply Chain
      Provenance (p46-48); Explainable AI (p49); Appendix 1 agent-type taxonomy (p70-76); Appendix 3
      ASI risk classes (p116); Appendix 6 Top 10 Impacting Personal Agents (p128). Appendix 2 is low.
  OWASP GenAI LLM Top 10 2026 (122pp, id 56857)              READ (13th), 2 facts + 1 upd
    ^ NOT mined: the ten per-entry chapters. LLM03 (p23-26) and LLM08 (p46-49) most relevant.
  Securing Agentic Applications Guide 1.0 (id 49059)         READ (15th), 2 facts
    ^ MOST OF THIS GUIDE IS BELOW THE BAR. Possibly worth one pass: 2.2 Secure Architecture Patterns
      (extract lines 833-1313), 2.5 Case Studies, 9.x runtime hardening. One pass maximum.
  Multi-Agentic System Threat Modeling Guide v1.0 (id 46950) READ (15th), 1 fact + critiqued 16th
    ^ SECTION 5 STILL UNMINED: "Threat Modeling Anthropic MCP Protocol using MAESTRO" (extract line
      3132 on). Sections 3-4 are RPA/blockchain enumeration, skip.
  Agent Name Service (ANS) v1.0 (id 47278)                   READ (16th), 1 fact + 1 upd. DONE.
  *** OWASP Top 10 for Agentic Applications 2026 (id 52117)  READ (17th), 3 facts. ***
    ^ PARTIALLY MINED — see split item 3 and the detailed unmined list in crawl-sources.
      Appendix D spans extract lines 2138-2750. Acknowledgements start ~2851 and contain an
      ASI01-ASI10 roster — exclude it from any count (Finding 4).
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-a-hands-on-companion-to-the-owasp-genai-security-project/
*** MCP 2026-07-28 — TRIPWIRE CHECKED 17th RUN VIA THE REPO, STILL UNCHANGED (7th consecutive) ***
READ SO FAR: changelog, versioning, deprecated, server/discover, basic/patterns/mrtr,
  basic/authorization/client-registration, docs/extensions/overview, basic/index, security_best_
  practices at BOTH 2025-06-18 and 2026-07-28, and (17th) server/tools + learn/server-concepts.
STILL UNREAD, in rough value order:
  /specification/2026-07-28/basic/authorization/security-considerations  <- TOP; named by 066a9dad
  /specification/2026-07-28/basic/versioning       (negotiation + backward-compat with 2025-11-25)
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/transports/stdio#backward-compatibility
  /specification/2026-07-28/server/utilities/caching  (ttlMs/cacheScope)
  /extensions/tasks/overview and /extensions/apps/overview
  /docs/2026-07-28/develop/clients/client-best-practices
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude)
OPENAI: see the full /index/ catalogue now in crawl-sources — six unread posts ranked, plus three
  product announcements explicitly marked below the bar so nobody spends a fetch on them.
  developers.openai.com/api/docs/guides/ — plain WebFetch, no browser. Scan the tree for siblings.
Also still unread: https://www.cnn.com/2026/08/05/tech/meta-ai-hacking (a fifth lab; secondary —
  find the primary), and the simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with 3afa31af),
  the-tokenpocalypse (404media), /2026/Aug/2/open-letters/.
YIELD RANKING as of the SEVENTEENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES via the GitHub contents API. Cheapest high-value call, outage-proof,
     EVERY run. AND: where a spec is versioned in git, DIFF REVISIONS rather than re-reading. NOTE
     the 17th run's calibration — a near-empty diff is a real result, not a failed technique.
  2. OWASP GenAI PDF REPORTS. Eight read across six runs for 21 facts + 5 corroborations. Route
     solved six times over. Mine ARCHITECTURE, THREAT-MODEL METHOD, DISAMBIGUATION and MATURITY
     sections; SKIP numbered control checklists. Count tables, never quote their pairings.
  3. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, aisi.gov.uk/blog, anthropic.com/news.
     Demoted from 2 to 3 THIS RUN on evidence: three of four feeds were empty over five days. Still
     rank 3 because when they do fire, they fire hard. Use WebSearch+allowed_domains, not index sweeps.
  4. PUBLISHED CRITIQUES OF SOURCES ALREADY IN THE KB. One 8-page paper produced 3 facts + 1
     sharpening at a fraction of a 139-page guide's cost. Search "critique/gaps in <document>".
  5. MCP remaining spec pages (list above). security-considerations is next.
  6. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. Index quiet since Apr 2026.
  7. microsoft.com/en-us/research/blog — 1 fact of 3 last time. Prefer METHOD over FRAMEWORK posts.
  8. Azure Architecture Center. The six-part RAG series is the largest coherent unread block.
  9. aws.amazon.com/blogs/machine-learning — product-heavy, but spec-level changes surface early.
 10. builder.aws.com Builders' Library — 16 of 30 read for 55+ facts; the 12 unread skew CI/CD.
 11. cognition.com/blog — dense, specific, publishes reversals of its own positions. Unread:
     coding-agents-101-the-art-of-actually-getting-things-done, swe-grep, blockdiff,
     devin-annual-performance-review-2025, evaluating-coding-agents, making-fable-cheaper-than-opus,
     devin-fusion, swe-1-7, measuring-open-source-model-trustworthiness,
     introducing-devin-security-swarm, frontier-code and frontier-code-1.1, ai-productivity.
     Skip partnership/funding/office/acquisition posts — about half the feed.
 12. huggingface.co/blog — scan for incident/infrastructure/engineering; SKIP model/dataset launches.
 13. sourcegraph.com/blog — real measurements. Unread: compliance-first-ai-proving-agent-provenance,
     owning-a-codebase, sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone,
     the-hidden-cost-of-code-that-nobody-touches.
 14. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
 15. simonwillison.net/tags/llms/ — VALUE IS THE LINKS: read the index, follow the primaries. CAVEAT:
     his summaries of TALKS are the weakest link here and produced two uncorroborated claims.
 16. latent.space/archive — unread: /p/aiewf26trends, /p/modal2026, /p/poolside, /p/chatgpt-work.
 17. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 18. blog.redwoodresearch.org — NEW, watch-only, for the METR+Redwood joint assessment.
 19. metr.org/blog — demoted 13th run. RE-RATE when the joint assessment lands.
 20. embracethered.com/blog — low volume, high value, security only.
 21. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 22. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — EMPTY, and now EIGHT FOR EIGHT on false dead ends. Read the warning in Appendix S.
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... instead.
  modelcontextprotocol.io -> was ECONNREFUSED 2026-08-12; FULLY UP 2026-08-14. Transient.
  modelcontextprotocol.io/docs/concepts/tools -> recorded GONE by the 16th run; it REDIRECTS (200).
  NOTE: builder.aws.com, the Vectara leaderboard, OWASP PDFs (three times, three stated reasons),
    openai.com, modelcontextprotocol.io and now /docs/concepts/tools were ALL listed or headed here
    and NONE was unreachable.

TIER 6 GITHUB READMEs — CLOSED OUT. A repo README is worth a fetch for LIFECYCLE STATUS and nothing
else. If a repo matters, go to its DOCS site. AMENDMENT (16th run): a repo that HOSTS a documentation
site is a different animal — there the repo is the primary source and beats the site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

VERIFICATION-POOL NOTE (updated 17th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, 714a540c, f7dee43a, 9aaea0dc, 9e29d93a, 1531a0d1, b4d688b1,
99aa74e6, 0720e9d7, 59a75c06, b471f9ef, ba5db3ec, f4005c98, c28c7f7b, 11ebefd6, db15af92, 8f2fdde8,
and (17th run) ee3bc7d3, ca3382bd, 46eeb374, plus this run's own 703147ba, ba1b7aad and 8cf06566.
THREE AXES, ROTATE THEM: confidence (lowest first), earliest-committed, shared-ref grouping.
13th earliest-committed (2 defects in 5); 14th confidence (1 + 1 partial); 15th shared-ref (3 in 5);
16th earliest-committed AND shared-ref together (2 in 5, two fetches); 17th SHARED-REF as primary
(0 claim defects in 5, but 3 ref additions + 2 source-count fixes, two fetches for four facts).
READ THE 17th RESULT CAREFULLY: zero CLAIM defects is not zero yield — the pass invalidated the
PREMISE it was given (the refs were never rotted) and fixed two source-count errors nobody had
queried. NEXT RUN: rotate the primary axis to EARLIEST-COMMITTED, still grouping by shared ref.
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result.
SUB-RULE (14th): a PARTIAL confirmation must be written down as partial, in the fact.
SUB-RULE (15th): when a quoted sentence appears in more than one fact, a defect in it is duplicated
  too. Query the kb for the quotation before correcting it.
SUB-RULE (15th): check that a CITED PAGE ACTUALLY CARRIES the detail attributed to it.
SUB-RULE (15th): RUN THE CHECKLIST ON THE FACTS YOU JUST WROTE. Four runs, four harvests: 3 defects
  in 8, 3 in 7, 2 in 3, and 3 more in this run's REVIEW pass. Budget it; it is not optional.
SUB-RULE (16th): WHERE A SOURCE IS VERSIONED AND IN GIT, DIFF THE REVISIONS INSTEAD OF RE-READING.
SUB-RULE (17th): A CLAIM THAT A PATH IS DEAD, OR THAT CONTENT MOVED SOMEWHERE, IS A CLAIM LIKE ANY
  OTHER. Test the redirect; grep the alleged successor for the content.
SUB-RULE (17th): THE SELF-REVIEW MUST RE-RUN COMPUTATIONS, NOT RE-READ PASSAGES. Re-reading the
  source cannot catch a bad count or a bad cross-document inference. Re-run every "N of M" a fact
  reports, and re-derive every cross-document claim from BOTH documents.

WHAT THE VERIFICATION PASS ACTUALLY FINDS — TEN RUNS OF EVIDENCE. Mostly NOT stale facts. It finds
CITATION-FIDELITY defects in facts whose underlying claims are correct:
  ninth      — 56986e8f: a paraphrase wearing quote marks.
  tenth      — c93d93ee: an overclaiming gloss attributed to the source.
  tenth      — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh   — 96ebc34e: BOTH at once, and the gloss reversed the blame.
  eleventh   — c858a924: WRONG ACTOR — 'independent auditors' were two LLM judges, not humans.
  twelfth    — 30869b36: a pack gloss wearing quote marks ('combined surface area').
  twelfth    — c436422a: WRONG TERMS attributed to the source (brain/hands/session).
  thirteenth — f78a326a: WRONG TERM + one instance generalised into a rule.
  thirteenth — 38c06627: MISATTRIBUTION ACROSS A FACT'S OWN TWO REFS.
  fourteenth — d18637a2: MODAL STRENGTHENING + a scope error.
  fifteenth  — f7dee43a AND 9aaea0dc: MODAL STRENGTHENING, the same quotation, in two facts.
  fifteenth  — 714a540c: ATTRIBUTION TO AN UNLISTED REF + a language-binding error.
  fifteenth  — b4d688b1: MODAL STRENGTHENING IN A TITLE, in a fact written that same run.
  fifteenth  — 0720e9d7: A PDF LINE-WRAP SILENTLY RECONSTRUCTED and printed as a literal.
  sixteenth  — 59a75c06: A TITLE THE SUCCESSOR REVISION EXPLICITLY CONTRADICTS. First instance of
    genuine STALENESS rather than citation infidelity — the fact was right when written.
  sixteenth  — b471f9ef: AN OVERCLAIMED ABSENCE concealing a MUST silently downgraded to SHOULD.
  sixteenth  — 11ebefd6 (own): A QUANTIFIER INFLATED IN A TITLE — 'most' for seven of sixteen.
  sixteenth  — db15af92 (own): AN UNCHECKED VERSION ATTRIBUTION.
  sixteenth  — 8f2fdde8 (own): A TITLE CLAUSE THE FACT'S OWN BODY UNDERCUT.
  seventeenth— ca3382bd AND 46eeb374: SOURCE-COUNT INFLATION — N pages of ONE spec counted as N
    sources. Neither claim was wrong; the corroboration signal was. First time the pass found the
    same defect in two facts by reading FRONTMATTER rather than prose.
  seventeenth— 703147ba (own): AN INCOMPLETE MAPPING, plus a METHOD SENTENCE that vouched for it.
  seventeenth— 8cf06566 (own): A CONTAMINATED COUNTING RANGE (uniform +1 to every bucket — ranking
    survived, absolutes did not), AND, separately, WRONG EVIDENCE FOR A CORRECT CONCLUSION where the
    cited evidence actually contradicted the claim. NEW AND THE MOST DANGEROUS CLASS YET: a reader
    checking the citation would have rejected a fact that was right.
  seventeenth— ba1b7aad (own): A TENSE-ALTERED QUOTATION ('operating' for 'operates').
CHECKLIST — verify all THIRTEEN explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source, VERBATIM INCLUDING TENSE
      AND INFLECTION, and does the quote START where the source's sentence starts;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to; (5) are the TERMS attributed to the source
  actually the source's terms; (6) refs classification (local vs external) and `sources` counts —
  N pages of ONE specification is ONE source, not N;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number — is a single reported
  instance presented as a general rule — and does ANY listed ref support it at all;
  (8) MODAL STRENGTH, QUANTIFIERS AND SCOPE, IN THE BODY AND IN THE TITLE SEPARATELY;
  (9) LANGUAGE BINDING AND VERSION for anything from framework or vendor docs;
  (10) LITERALS FROM A PDF ARE RECONSTRUCTIONS — pdftotext breaks hyphenated tokens across lines AND
  SHUFFLES TABLE COLUMNS. A negative grep is ALSO unreliable for the same reason. Distinguish PACK
  ANALYSIS from SOURCE CLAIM — a gloss next to a citation gets read as cited;
  (11) VERSION ATTRIBUTION IS A CLAIM. Check the predecessor revision;
  (12) A FACT'S STATEMENT OF ITS OWN METHOD ('all from prose', 'every figure re-verified') IS THE
  CLAIM MOST LIKELY TO BE FALSE, because it is written once, at the end, about piecemeal work;
  (13) NEW — RE-RUN EVERY COMPUTATION AND RE-DERIVE EVERY CROSS-DOCUMENT INFERENCE. Bound counting
  regions on the following heading, not a guessed line number. And check that the cited evidence
  actually SUPPORTS the conclusion rather than merely sitting near it — the worst defect found so far
  was a correct claim whose stated evidence, counted properly, argued against it.
