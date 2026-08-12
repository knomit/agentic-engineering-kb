---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-12 (sixteenth run, 19:48Z — about five hours after the fifteenth, which committed
14:30-14:40Z the same day). A SAME-DAY run, so per the standing rule NO broad feed sweep was
attempted; the budget went to the 15th run's queued backlog. THAT IS NOW THREE CONSECUTIVE RUNS
WITHOUT A SWEEP (14th, 15th, 16th), all legitimately same-day or next-day. The sweep is genuinely
owed the moment real time elapses — see the split below, item 1.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***
The BACKFILL FLOOR is e61629fc (2026-08-12T02:26Z), carrying the complete 197-URL ALREADY_CRAWLED
union computed once with git over all 34 pre-floor revisions. A walk that reaches it has reached the
bottom. Do NOT reproduce that union here.
ALREADY_CRAWLED = 197 (floor) + 9 (15th run) + 10 (this run, below) = 216.

HISTORY WALK PERFORMED THIS RUN: 3 revision bodies read — HEAD 5ab895cf (15th run, 14:40Z), then
8be9e4de (15th run's first write, 14:34Z), then e61629fc (the floor, 02:26Z). Oldest commit date
reached: 2026-08-12T02:26:10Z. 8be9e4de was read rather than skipped precisely because HEAD's diff
showed -39 lines and a dropped URL would have been invisible otherwise; it carried the identical
9-URL list, so nothing was lost in that edit.
HONEST NOTE ON WHERE THE WALK STOPPED: more_available was still TRUE at the floor. I stopped at the
floor by its own declaration, not because the API said there was nothing left. Behind it sit
9452da53 and bb31f926, which the 15th run read and reported as carrying the identical 197-URL union.
So the stop is deliberate and documented, not a partial walk — but it is a stop on an assertion in a
body, not on an API signal, and a future run should know that is what "reached the floor" means here.

recurring-feed indexes swept: ONE, and by a NEW ROUTE.
https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification
  (MCP tripwire — UNCHANGED. Released revision directories: 2024-11-05, 2025-03-26, 2025-06-18,
   2025-11-25, 2026-07-28, draft. No new revision. Sixth consecutive run unchanged.)
The rendered tripwire page could not be used — see "errored" below. This is now the PREFERRED form.

articles crawled (10 new):
https://arxiv.org/abs/2508.09815  +  https://arxiv.org/pdf/2508.09815   <- TIER-1 PAIR, THE BIG ONE
https://modelcontextprotocol.io/specification/2026-07-28/basic/index     <- via repo mirror; 2 facts
https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/specification/2026-07-28/basic/index.mdx
https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/specification/2025-11-25/basic/index.mdx  (vintage check only)
https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/docs/2026-07-28/tutorials/security/security_best_practices.mdx
https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/docs/docs/2025-06-18/tutorials/security/security_best_practices.mdx
https://genai.owasp.org/resource/agent-name-service-ans-for-secure-al-agent-discovery-v1-0/
https://genai.owasp.org/download/47278/?tmstv=1747275418                 (ANS v1.0, 2587 lines)
https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/  (resource page ONLY —
  the PDF at /download/52117/?tmstv=1765059207 is resolved but NOT fetched; it is one curl for next run)

errored / not obtained — ONE HOST, AND IT WAS ROUTED AROUND, NOT DROPPED:
modelcontextprotocol.io was DOWN for the whole run. `connect ECONNREFUSED 76.76.21.21:443` from
WebFetch on three separate paths, and curl timed out (exit 28, HTTP 000). Not a 403, not a gate —
the origin refused. Every other host that run was fine, so the variable was isolated before blaming
the tool. Recovered in full via the spec's own GitHub repository (fetch-routes route 3, NEW). Six
documents read that way. Do NOT record this host as unreliable; record the mirror.
Nothing else errored. No paywalls, no 404s, no guessed slugs.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

FINDING 1 — A SOURCE BEING DOWN PRODUCED A BETTER ROUTE THAN THE ONE IT REPLACED, AND THE BEST
STALENESS TECHNIQUE THIS JOB HAS FOUND.
modelcontextprotocol.io renders .mdx straight out of its GitHub repo, so the repo is not a mirror,
it IS the source. Three compounding wins, all now in fetch-routes route 3:
  * THE TRIPWIRE GOT CHEAPER AND MORE ROBUST. One contents-API call lists a directory per released
    revision. A new revision is a new directory. No page render, no parsing, works when the site is
    down. This replaces the /specification/versioning fetch as rank-1 every run.
  * REVISION DIFFING. Every revision of every page sits side by side in the tree, so
    `diff <old-rev>.mdx <new-rev>.mdx` turns the staleness pass from "re-read and hope you notice"
    into a mechanical enumeration of what changed. ONE diff command on the MCP security page yielded
    FOUR results at once: a heading rename that confirmed a fact's prediction, a MUST downgraded to
    SHOULD that corrected the same fact, a new subsection that directly contradicted a different
    fact's TITLE, and three brand-new attack sections worth their own fact. Nothing else in this job
    has that yield-per-call. Use it wherever a source is versioned and in git.
  * IT EXPOSED REF ROT NOBODY HAD SEEN. Site URLs do not map to repo paths, and pages MOVE between
    the two trees. `security_best_practices` left /specification/<rev>/basic/ for
    /docs/<rev>/tutorials/security/ — four facts cite the old path. And /docs/concepts/tools is gone
    entirely, its material now at /docs/<rev>/learn/server-concepts; TWO facts (ee3bc7d3, ca3382bd)
    still cite the dead path and are UNCHECKED. Caveat honestly recorded in every fact: I could not
    test whether the old URLs still redirect, because the site was down. Old refs were kept and new
    ones ADDED, never swapped.

FINDING 2 — THE TIER-1 COUNTER-POSITION PAPER PAID OFF, AND ITS VALUE WAS IN READING THE TABLE
SIDEWAYS RATHER THAN IN ITS OWN THESIS.
arXiv 2508.09815 (Krawiecka & Schroeder de Witt, Oxford) tabulates sixteen threat classes against
whether OWASP's MAS guide covers them. Taken as a list it is a list. Sorted by WHAT EACH ONE ATTACKS,
seven of the sixteen turn out to be the same story: a **verifier agent defeated with nobody
compromised** — planner overrides it, executor's confident tone biases it, it shares the pipeline's
success metric so it rubber-stamps, it inherits executor permissions through subgraph design, it
accepts hallucinations against vague criteria. Since "add a reviewer agent" is the standard safety
answer, that list is an enumeration of why the standard answer under-delivers. The deciding variable
in four of the seven is SHARED INCENTIVE: a verifier scored on the pipeline's success is a
participant in it, not a check on it.
TWO DISCIPLINE POINTS I had to hold onto while writing it:
  * MODALITY. MASEC is explicitly anticipatory — "guided by what is mathematically or physically
    possible rather than limited to observed incidents". No measurements, no incidents, constructed
    scenarios. Every fact from it says so, and confidence sits at 0.65-0.7. This paper would be very
    easy to over-write into hard claims.
  * THE GROUPING IS MINE, NOT THEIRS. The paper never claims a verifier through-line. Marked as pack
    analysis in the fact and in the c02ac546 update.
AND IT SHARPENED AN EXISTING FACT RATHER THAN CONTRADICTING IT. c02ac546 says a MAESTRO layer-walk
generates threats the taxonomy lacks. The critique's gap is a DIFFERENT KIND: general classes that
neither the taxonomy holds nor the layer walk produces — because MAESTRO's layers are
INFRASTRUCTURE-shaped while the missing classes are properties of ROLE RELATIONSHIPS AND INCENTIVES,
which have no layer to sit in and are not "emergent" enough to fall out of a cross-layer pass. Not a
contradiction, so not a `decisions` fact — a documented limit, written into c02ac546 with the
distinction spelled out so a future run does not mistake one gap for the other.

FINDING 3 — THE STALENESS PASS CAUGHT A FACT WHOSE TITLE THE CURRENT SPEC CONTRADICTS IN SO MANY
WORDS, WHICH IS THE CLEANEST VINDICATION OF THE "CHECK THE TITLE SEPARATELY" SUB-RULE SO FAR.
59a75c06 was titled "In MCP, the SSRF victim is the client". Correct for 2025-06-18. The 2026-07-28
revision adds a subsection opening "**SSRF risks are not limited to MCP clients.**" — CIMD makes the
authorization server fetch a URL supplied by an unknown client. The body's mechanics were all still
right; only the generalisation in the title had gone stale. Retitled, and the durable rule restated:
in OAuth-for-agents, whichever party dereferences a URL supplied by the other is the SSRF target.

FINDING 4 — A FACT THAT PREDICTED SOMETHING CORRECTLY ALSO OVERCLAIMED, AND ONLY THE PRIMARY SOURCE
COULD SHOW BOTH.
b471f9ef predicted that removing MCP sessions RELOCATED the hijacking class into tool arguments
rather than fixing it. The 2026-07-28 security page confirms it outright — the section is renamed
"State Handle Hijacking". But the same fact asserted the handles were "no longer covered by any
transport-layer rule about entropy, rotation, or user binding". Wrong: the rules were REWRITTEN for
handles. And the rewrite hides the real finding — **the entropy requirement dropped from MUST to
SHOULD** ("MUST use secure, non-deterministic session IDs" -> "SHOULD use secure, non-deterministic
handles"), while the binding rule GAINED an explicit "reject a handle presented by any other
principal" clause. A guessable handle is now conformant. That is a one-word normative change nobody
finds by re-reading; the diff found it in seconds.

*** FINDING 5 — THE POST-WRITE SELF-REVIEW FOUND THREE DEFECTS IN SEVEN NEW FACTS, ALL THREE IN
TITLES, ONE OF THEM A CLAIM I HAD NEVER CHECKED. SECOND RUN RUNNING; THIS STEP IS EARNING ITS COST. ***
  11ebefd6 — QUANTIFIER OVERCLAIM. Title said "MOST of the threats missing… converge on one
    component". It is SEVEN OF SIXTEEN. The body said "seven" correctly; the title rounded it up to a
    majority it does not have. Retitled to state the count. Same disease as the 15th run's b4d688b1:
    the body hedges, the title does not, and the title is what a query result shows.
  db15af92 — AN UNVERIFIED VINTAGE CLAIM, AND THE SELF-REVIEW IS THE ONLY REASON IT WAS CHECKED.
    Title said "MCP 2026-07-28 ADDS two places where a client dereferences a server-chosen URI". I
    had verified the $ref ban was new; I had simply assumed `icons` was too. Two three-second greps
    across three revisions of basic/index.mdx settled it: **`icons` dates from 2025-11-25**, only
    `$ref` is new in 2026-07-28. Retitled, and the vintage now stated explicitly in the body because
    it decides what an implementer must support. THE LESSON, and it is a new checklist item (11): a
    fact written from ONE revision of a versioned source will happily attribute everything on the
    page to that revision. Version-attribution is a claim like any other and needs its own check.
  8f2fdde8 — A TITLE CLAUSE MY OWN BODY UNDERCUT. Title said the ANSName "pins a capability and
    version RATHER THAN an agent". The name contains AgentID too, so it pins all three; and the body
    separately notes the in-name version is not even the registry match key. Reworded to "carries a
    capability and version alongside the agent".
  NOT CHANGED, but flagged for the next reader: 24e4552d's title states "per-agent safety evaluation
    does not compose" as flat fact, from an anticipatory source. It survives because the composition
    claim is independently supported by bdf3336e from OBSERVED bypasses, and the body marks the
    cross-model-chaining vector as unevidenced. If bdf3336e is ever retracted, this title must soften.

FACTS WRITTEN (7 new, 3 updated from crawling, 5 touched by the staleness pass, 3 revised by the
self-review, 0 retracted):
  NEW —
    kb/architecture/ai/agents/multi-agent/verifier-role/11ebefd6      (seven of sixteen missing
      threats are one story: the verifier defeated with nobody compromised; shared incentive is the
      deciding variable; Planner/Executor/Verifier/Refiner vocabulary. TITLE FIXED post-review.)
    kb/invariants/ai/agents/security/multi-agent/composition/24e4552d (heterogeneous multi-agent
      exploits — split a task across models with different refusal tuning; attribution degrades
      before detection does)
    kb/gotchas/ai/agents/security/guardrails/context-distortion/74996815 (the rewriting guardrail is
      itself a threat class; sanitising a query can BROADEN what the database returns. conf 0.65 —
      the concrete claim rests on one table cell and the fact says so)
    kb/invariants/ai/agents/tools/mcp/metadata/fa61c895               (_meta reserved by the SECOND
      label — com.mcp.tools/ reserved, com.example.mcp/ not; required per-request fields; -32602 vs
      MissingRequiredClientCapabilityError -32021; the OpenTelemetry prefix exception)
    kb/invariants/ai/agents/tools/mcp/security/dereference/db15af92   ($ref MUST NOT auto-dereference
      + reject-rather-than-silently-permissive + composition-keyword DoS; icons as untrusted URI and
      untrusted bytes. VINTAGE CORRECTED post-review.)
    kb/architecture/ai/agents/interop/naming/8f2fdde8                 (ANS: ANSName grammar, the
      registry-signed EndpointRecord, and section 5.5's explicit disclaimer that ANS does NOT
      translate between protocols. TITLE FIXED post-review.)
    kb/gotchas/ai/agents/tools/mcp/security/client-identity/066a9dad  (CIMD proves a domain, not which
      local process holds the localhost redirect; PKCE does not stop a mix-up attack and the spec
      says why; CIMD admission is server policy)
  UPDATED FROM CRAWLING —
    c02ac546  — the MAESTRO method's own documented limit, with the two kinds of gap distinguished.
      sources 1->2.
    3afa31af  — normative statelessness text + the stdio trap ("a STDIO process is not a conversation
      or session"), which is where an implementer leaks across conversations. sources 1->2 (the AWS
      post was always an independent source and was undercounted).
    8b32c15a  — ANS's own two-tier validation split: the RA validates once, the CALLER must validate
      before EVERY interaction, and capability alignment has no cryptographic form — the spec's
      suggested check is testing the peer on sample tasks. conf 0.8->0.85, sources 1->2.

CONTRADICTIONS: none between sources requiring a `decisions` fact. One near-miss handled as a
documented limit rather than a disagreement (c02ac546 vs arXiv 2508.09815, see Finding 2) — they
describe different gaps and neither denies the other. One INTERNAL contradiction found and fixed:
the corpus's own 59a75c06 title vs the current MCP spec (Finding 3).

STALENESS PASS (5 sampled on the EARLIEST-COMMITTED axis as the rotation required, and grouped by
SHARED REF as a bonus — all five predate 2026-07-27 and four cite one page, so TWO fetches covered
five facts. 2 corrected, 3 confirmed):
  59a75c06 CORRECTED — title contradicted by the successor revision (Finding 3). Scope-correction
    section added; VERIFICATION SCOPE names what was NOT re-checked (the CIDR list and the
    encoding-evasion wording in the newer revision). Smokescreen and DNS-rebinding confirmed as the
    spec's own, not imported. conf 0.9 held.
  b471f9ef CORRECTED — overclaim removed, MUST->SHOULD downgrade found, comparison table added
    (Finding 4). sources 2->1: both refs are pages of the MCP spec, which is ONE source. conf 0.9 held.
  ba5db3ec CONFIRMED and ENRICHED — the 2026-07-28 revision splits the vulnerability into TWO
    dimensions, audience-validation failure (complete on its own, at acceptance) and passthrough
    (forwarding). Retitled, because "we don't do passthrough" answers only the second. conf 0.9 held.
  f4005c98 CONFIRMED verbatim — MUST allow only http/https, MUST reject javascript:/data:/file:/
    vbscript:, MUST NOT use shell commands, SHOULD use non-shell URL opening. Unchanged in the newer
    revision. Refs updated for the moved path; body untouched.
  c28c7f7b CONFIRMED verbatim — all FOUR vulnerable conditions present as a list, and the fact's
    framing is sharper than the source's own prose intro, which names only three. Refs updated.

PROMPT INJECTION: none observed. Stated explicitly because arXiv 2508.09815 describes, in a table
cells' worth of detail, how agents could evolve covert symbolic protocols and how one agent could use
"affective prompt framing" to bias another. That is threat-taxonomy prose about hypothetical systems,
not text addressed to this job, and it was treated as data. Nothing fetched attempted to redirect
this run.

SUGGESTED SPLIT FOR THE NEXT RUN:
(1) SWEEP THE FEEDS THE MOMENT DAYS HAVE PASSED — owed for THREE runs. Prioritise openai.com/index,
    anthropic.com/news, genai.owasp.org, aisi.gov.uk/blog. Top priority if any real time has elapsed.
(2) OWASP TOP 10 FOR AGENTIC APPLICATIONS 2026 — the full download URL is now resolved and recorded
    in crawl-sources; it is literally one curl. Longest-standing unfetched high-value item.
(3) THE TWO FACTS CITING A DEAD MCP DOC PATH: ee3bc7d3 and ca3382bd both cite
    modelcontextprotocol.io/docs/concepts/tools, which no longer exists. Their content is now at
    docs/docs/<rev>/learn/server-concepts.mdx. Make them the next staleness sample — the shared ref
    means one fetch does both, and the page has moved AND been rewritten across revisions, so diff it.
(4) MCP, remaining: basic/authorization/security-considerations (named by 066a9dad, holds the
    authorization-server-side countermeasures for localhost impersonation and CIMD trust policies —
    the direct completion of this run's newest fact), then basic/versioning,
    transports/streamable-http, server/utilities/caching, extensions/tasks + apps overviews.
    ALL now reachable by repo mirror even if the site is still down.
(5) OWASP companion corpus: Solutions Landscape Red Teaming Taxonomy, A Practical Guide for Secure
    MCP Server Development, CheatSheet — Securely Using Third-Party MCP Servers, GenAI Red Teaming
    Guide, Agentic AI Solution Landscape, OWASP AIBOM, GenAI Data Security. ANS is now DONE.
(6) The MASEC paper's reference list is a small unmined catalogue — NetSafe (arXiv 2410.15686) and
    chaos engineering for LLM MAS (arXiv 2505.03096) are the two closest to this pack's bar, and both
    report MEASUREMENTS, which is exactly what 2508.09815 lacks. Good pairing with 24e4552d.
(7) The OWASP ASI incidents tracker — now FIVE runs listed without a single fetch.
(8) LLM Top 10 2026 per-entry chapters: LLM03 Excessive Agency (p23-26), LLM08 Hidden Context
    Exposure (p46-49). id 56857.
(9) FINISH THE OPENAI CLUSTER — two left, both likely low-yield policy:
    /index/putting-frontier-cyber-models-in-more-trusted-hands/, /index/safety-alignment-long-horizon-models/.
    STILL WATCHING for: OpenAI's full HF technical report, the JOINT METR + Redwood assessment,
    Irregular's containment white paper. None had landed as of 2026-08-12.


=== PER-SOURCE STATUS AND QUEUE, as of the 16th run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

OWASP GenAI PDF REPORTS — STATUS:
  AIUC-1 Crosswalks (55pp)                                  READ (11th), 3 facts+1 upd
  AI Security Solutions Landscape Red Teaming Q2 2026 (15pp) READ (11th), 1 fact
  State of Agentic AI Security and Governance 2.01 (139pp)  READ (12th), 8 facts+1 upd
    ^ chapters still NOT written up: Enterprise Adoption Maturity Model (p53-62), Alignment with
      Top 10 Agentic (p61), Future Trends / What Remains Unsolved (p63-68); AI SBOM and Supply Chain
      Provenance (p46-48); Explainable AI (p49); Appendix 1 agent-type taxonomy (p70-76); Appendix 3
      ASI risk classes (p116); Appendix 6 Top 10 Impacting Personal Agents (p128). Appendix 2 is low.
  OWASP GenAI LLM Top 10 2026 (122pp, id 56857)             READ (13th), 2 facts + 1 upd
    ^ NOT mined: the ten per-entry chapters. LLM03 (p23-26) and LLM08 (p46-49) most relevant.
      Appendix A coverage matrices (p58-105) map to ASI 2026, DSGAI v1.0, MITRE ATLAS v2026.06,
      ATT&CK v19.1, CWE 4.20, NIST AI 600-1, NIST AI RMF, CSA AICM v1.1, AIVSS v0.8.
  Securing Agentic Applications Guide 1.0 (id 49059)        READ (15th), 2 facts
    ^ MOST OF THIS GUIDE IS BELOW THE BAR — sections 5.x and 4.4 are generic control checklists.
      Possibly still worth one pass: 2.2 Secure Architecture Patterns (extract lines 833-1313),
      2.5 Case Studies, 9.x runtime hardening. Do not budget more than one pass.
  Multi-Agentic System Threat Modeling Guide v1.0 (id 46950) READ (15th), 1 fact + critiqued 16th
    ^ SECTION 5 STILL UNMINED: "Threat Modeling Anthropic MCP Protocol using MAESTRO" (extract line
      3132 on). Sections 3-4 are RPA/blockchain enumeration, skip. READ arXiv 2508.09815 FIRST — done
      as of the 16th run, so this guide may now be mined without re-opening the pairing question.
  Agent Name Service (ANS) v1.0 (id 47278)                  READ (16th), 1 fact + 1 upd
    ^ DONE. Sections 3.5 (naming/resolution), 3.6 (governance), 3.7 (identity), 5.5 (interop limit)
      and 6.x (MAESTRO threat analysis) all read. The remainder — 3.1-3.4 registration/PKI mechanics,
      section 4 request/response schema, section 7 implementation, section 8 future — is conventional
      PKI plumbing and unlikely to clear the bar. DO NOT re-mine. NOTE: its "Summary of ANS Functional
      Layers" TABLE extracts with shuffled columns; the ZKP-capability-verification claim circulating
      about ANS traces to that cell and is NOT in the prose.
STILL UNREAD, all named as companion resources: see split items 2 and 5.
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-a-hands-on-companion-to-the-owasp-genai-security-project/
*** MCP 2026-07-28 — TRIPWIRE CHECKED 16th RUN VIA THE REPO, STILL UNCHANGED ***
No movement since the 11th run. Check EVERY run; now near-free via the contents API (crawl-sources).
READ SO FAR: changelog, versioning, deprecated, server/discover, basic/patterns/mrtr,
  basic/authorization/client-registration, docs/extensions/overview, docs/concepts/tools (dead path),
  and (16th) basic/index — the _meta contract, statelessness, JSON Schema and icons rules — plus the
  security_best_practices page at BOTH 2025-06-18 and 2026-07-28.
STILL UNREAD, in rough value order:
  /specification/2026-07-28/basic/authorization/security-considerations  <- NOW TOP; named by 066a9dad
  /specification/2026-07-28/basic/versioning       (negotiation + backward-compat with 2025-11-25)
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/transports/stdio#backward-compatibility
  /specification/2026-07-28/server/utilities/caching  (ttlMs/cacheScope)
  /extensions/tasks/overview and /extensions/apps/overview
  /docs/2026-07-28/learn/server-concepts   <- the successor to the dead /docs/concepts/tools
  /docs/2026-07-28/develop/clients/client-best-practices   <- NEW, spotted in the repo tree, unread
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude)
*** THE OPENAI SECURITY CLUSTER — SEVEN POSTS READ; NEARLY EXHAUSTED. See split item 9. ***
UNREAD, both likely policy/program, one cheap fetch each:
  /index/putting-frontier-cyber-models-in-more-trusted-hands/   (Aug 10)
  /index/safety-alignment-long-horizon-models/
  /index/trusted-access-for-cyber/, /index/scaling-trusted-access-for-cyber-defense/,
  /index/updating-our-preparedness-framework/   (governance; lower altitude)
developers.openai.com/api/docs/guides/ — plain WebFetch, no browser. Scan the tree for siblings.
Also still unread: https://www.cnn.com/2026/08/05/tech/meta-ai-hacking (a fifth lab; secondary —
  find the primary), and the simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with 3afa31af,
  which this run substantially enriched — good time to read it), the-tokenpocalypse (404media),
  /2026/Aug/2/open-letters/.
YIELD RANKING as of the SIXTEENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES, now via the GitHub contents API, not the rendered page. Cheapest
     high-value call in the pack and outage-proof. EVERY run. AND: where a spec is versioned in git,
     DIFF REVISIONS rather than re-reading — highest yield-per-call found so far (Finding 1).
  2. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, aisi.gov.uk/blog, anthropic.com/news, the
     OWASP ASI tracker. Validated six times. When the kb holds an incident fact, CHECK WHETHER THE
     OPERATOR PUBLISHED ITS OWN ACCOUNT, by SEARCHING; the same search is also the cheapest discovery
     sweep available (route 1b, now validated three runs running).
  3. OWASP GenAI PDF REPORTS. Seven read across five runs for 18 facts + 5 corroborations. Route
     solved twice over. Mine ARCHITECTURE, THREAT-MODEL METHOD and MATURITY sections; SKIP the
     numbered control checklists, which are below the bar. And skip TABLES — they extract shuffled.
  4. PUBLISHED CRITIQUES OF SOURCES ALREADY IN THE KB. NEW ENTRY, promoted straight to rank 4 on this
     run's evidence: one 8-page arXiv paper produced 3 facts and sharpened an existing one, at a
     fraction of the cost of a 139-page guide. When the kb holds a fact from a framework or standard,
     search for "extending/critique/gaps in <that document>". Cheap, and it is the only reliable way
     to find a limit that the document itself will never state.
  5. MCP remaining spec pages (list above). security-considerations is next.
  6. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. Index quiet since Apr 2026.
     anthropic.com/news is where postmortems actually land.
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
     his summaries of TALKS are the weakest link here and produced two uncorroborated claims
     (4e923405, bcbf13c2).
 16. latent.space/archive — unread: /p/aiewf26trends, /p/modal2026, /p/poolside, /p/chatgpt-work.
 17. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 18. metr.org/blog — demoted 13th run. RE-RATE IF the joint METR + Redwood assessment lands.
 19. embracethered.com/blog — low volume, high value, security only.
 20. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 21. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — EMPTY. Read the six-for-six warning in Appendix S first. It is now SEVEN for
seven: modelcontextprotocol.io was hard-down for an entire run and was fully recovered via its repo.
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... instead.
  modelcontextprotocol.io -> ECONNREFUSED 2026-08-12. NOT dead: use fetch-routes route 3.
  NOTE: builder.aws.com, the Vectara leaderboard, OWASP PDFs (three times, three stated reasons),
    openai.com and now modelcontextprotocol.io were ALL listed or headed here and NONE was unreachable.

TIER 6 GITHUB READMEs — CLOSED OUT. A repo README is worth a fetch for LIFECYCLE STATUS and nothing
else. If a repo matters, go to its DOCS site. BUT NOTE THE 16th RUN'S AMENDMENT: a repo that HOSTS a
documentation site is a different animal entirely — there the repo is the primary source and beats
the site (fetch-routes route 3). The README rule was about marketing READMEs, not about source trees.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

VERIFICATION-POOL NOTE (updated 16th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, 714a540c, f7dee43a, 9aaea0dc, 9e29d93a, 1531a0d1, b4d688b1,
99aa74e6, 0720e9d7, and (16th run) 59a75c06, b471f9ef, ba5db3ec, f4005c98, c28c7f7b, plus this run's
own 11ebefd6, db15af92, 8f2fdde8 via the self-review.
THREE AXES, ROTATE THEM: confidence (lowest first), earliest-committed, shared-ref grouping.
13th ran earliest-committed (2 defects in 5); 14th confidence (1 + 1 partial); 15th shared-ref
(3 in 5); 16th ran EARLIEST-COMMITTED **AND** SHARED-REF TOGETHER and got 2 defects in 5 at TWO
fetches. THAT COMBINATION IS THE NEW DEFAULT WHERE IT IS AVAILABLE — the axes are not mutually
exclusive, and the oldest facts in this kb turn out to cluster on a handful of source pages, so
sorting by age and then grouping by ref costs nothing and halves the fetches. Next run: rotate the
PRIMARY axis to confidence, still grouping by ref. Nothing here is yet older than 90 days.
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result.
SUB-RULE (14th): a PARTIAL confirmation must be written down as partial, in the fact.
SUB-RULE (15th): when a quoted sentence appears in more than one fact, a defect in it is duplicated
  too. Query the kb for the quotation before correcting it.
SUB-RULE (15th): check that a CITED PAGE ACTUALLY CARRIES the detail attributed to it.
SUB-RULE (15th): RUN THE CHECKLIST ON THE FACTS YOU JUST WROTE. Two runs, two harvests: 3 defects in
  8 last run, 3 in 7 this run, and this run's rate is understated because one of the three was a
  claim I would never have thought to check. Budget it; it is not optional.
SUB-RULE (16th): WHERE A SOURCE IS VERSIONED AND IN GIT, DIFF THE REVISIONS INSTEAD OF RE-READING.
  One `diff` produced four distinct findings on one page. Re-reading finds what you notice; diffing
  finds what changed, including one-word normative changes (MUST -> SHOULD) that no reader catches.

WHAT THE VERIFICATION PASS ACTUALLY FINDS — NINE RUNS OF EVIDENCE. It is NOT finding stale facts. It
finds CITATION-FIDELITY defects in facts whose underlying claims are correct:
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
  sixteenth  — 59a75c06: A TITLE THE SUCCESSOR REVISION EXPLICITLY CONTRADICTS. The body aged fine;
    the generalisation in the title did not. First instance of genuine STALENESS rather than
    citation infidelity — the fact was right when written.
  sixteenth  — b471f9ef: AN OVERCLAIMED ABSENCE ('no longer covered by any rule') where the rules had
    been rewritten, not removed — concealing the real finding, a MUST silently downgraded to SHOULD.
  sixteenth  — 11ebefd6 (own): A QUANTIFIER INFLATED IN A TITLE — 'most' for seven of sixteen.
  sixteenth  — db15af92 (own): AN UNCHECKED VERSION ATTRIBUTION — features of an older revision
    credited to the revision I happened to be reading.
  sixteenth  — 8f2fdde8 (own): A TITLE CLAUSE THE FACT'S OWN BODY UNDERCUT.
CHECKLIST — verify all ELEVEN explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source, and does the quote START
      where the source's sentence starts, or has a qualifier been cut off the front;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to; (5) are the TERMS attributed to the source
  actually the source's terms; (6) refs classification (local vs external) and `sources` counts —
  N pages of ONE specification is ONE source, not N;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number — is a single reported
  instance presented as a general rule — and does ANY listed ref support it at all;
  (8) MODAL STRENGTH, QUANTIFIERS AND SCOPE, IN THE BODY AND IN THE TITLE SEPARATELY: 'is noise' vs
  'deserves skepticism', 'works when' vs 'works best today when', 'became 80%' vs 'can eventually
  reach 80%', and — NEW — 'most' vs an actual count. Does a number measured on ONE
  benchmark/model/config get presented as holding generally;
  (9) LANGUAGE BINDING AND VERSION for anything from framework or vendor docs;
  (10) LITERALS TAKEN FROM A PDF ARE RECONSTRUCTIONS — pdftotext breaks hyphenated tokens across
  lines AND SHUFFLES TABLE COLUMNS. Mark it or confirm it against prose. And distinguish PACK
  ANALYSIS from SOURCE CLAIM in the prose — a gloss written next to a citation gets read as cited;
  (11) NEW — VERSION ATTRIBUTION IS A CLAIM. Reading one revision of a versioned document and
  crediting everything on the page to that revision is an assumption, not an observation. If a fact
  says a feature was ADDED in revision X, check the predecessor. Two greps settled db15af92.
