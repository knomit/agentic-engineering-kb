---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-15 (eighteenth run). ONE DAY after the 17th, so per the standing rule NO broad feed
sweep — the 17th swept four feeds and found three of them empty. The budget went to the queued
backlog instead, and the queue was well-aimed: three of the four items I took paid off.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***

=== HISTORY WALK ===
REVISIONS READ: 3.
  3bc37431 (HEAD, 2026-08-14T12:51:03Z) — the 17th run's body.
  3c6323cd (2026-08-12T21:25:35Z)       — the 16th run's body.
  8b9a768d (2026-08-12T00:27:10Z)       — the 13th run's body, carrying the AUTHORITATIVE 190-URL union.
more_available was FALSE at 8b9a768d. The walk terminated on the API's own signal.
I did NOT read 0ac250fd (2026-08-14T12:23:46Z) — it is the 17th run's FIRST write, superseded by
3bc37431 the same day and by the same run. Deduped as one run, not skipped as a gap.

*** THE GAP THE 17th RUN FOUND IS STILL THERE, UNCHANGED, AND STILL NOT MINE TO FIX. ***
The 14th and 15th runs' bodies remain UNREACHABLE — their per-run commits were squashed into merge
commits ("Merge pull request #8", "#6") and the hashes recorded in prose (e61629fc, 8be9e4de,
5ab895cf) do not resolve. ALREADY_CRAWLED = 190 (enumerated at 8b9a768d) + 10 (16th) + 5 (17th) +
7 (this run) = 212 URLs I can NAME, against an asserted true total of ~228. The ~16 unenumerable
URLs from the 14th/15th window are described at source level in the 17th run's body (OWASP guides
49059 and 46950, MCP basic/index work, three openai.com posts) and I steered clear of all of it.
NOTE FOR A HUMAN: this is now the SECOND run to report the same gap. It will not heal on its own.

*** THE DANGLING-REF PROBLEM IS ALSO STILL THERE, AND IS NOW WORSE THAN REPORTED. ***
kb/invariants/ai/agents/security/threat-taxonomy/4f5e9dfe.md is retracted but still cited. The 17th
run named 483263c5 and c02ac546. I confirmed BOTH still carry the dangling kb:// ref, and found a
THIRD: kb/invariants/ai/agents/security/chained-attacks/bdf3336e.md. Three live facts, one dead
target. Still for a human: restore it or strip the refs.

recurring-feed indexes swept: ONE, deliberately.
https://api.github.com/repos/.../contents/docs/specification  (MCP tripwire — UNCHANGED. 2024-11-05,
  2025-03-26, 2025-06-18, 2025-11-25, 2026-07-28, draft. EIGHTH consecutive run unchanged.)
No other feed swept, on purpose. Do not read this as a skipped sweep — read the 17th run's evidence.

articles newly crawled (7):
https://raw.githubusercontent.com/.../docs/specification/2026-07-28/basic/authorization/security-considerations.mdx  <- 3 facts
https://raw.githubusercontent.com/.../docs/specification/2026-07-28/basic/authorization/index.mdx
https://raw.githubusercontent.com/.../docs/specification/2025-11-25/basic/authorization.mdx   (predecessor)
https://raw.githubusercontent.com/.../docs/specification/2025-06-18/basic/authorization.mdx   (vintage check)
https://openai.com/index/introducing-aardvark/                    <- browser route, 1 fact
https://genai.owasp.org/download/54627/?tmstv=1779726713           <- AIUC-1 crosswalk, staleness (3 facts)
https://genai.owasp.org/download/54018/?tmstv=1775767894           <- Red Teaming Q2 2026, staleness (1 fact)
re-downloaded for the staleness pass, already known: genai.owasp.org/download/50592 and /52117.
Also fetched: all 38 .mdx files of revision 2025-11-25 (bulk grep, one loop — see Finding 2). Those
are a verification sweep, not article reads; I am not listing them as crawled URLs.

errored / not obtained: NONE that survived. One 404 (the naive 2025-11-25 path for
authorization/security-considerations) was expected-shaped and turned into Finding 3 rather than a
failure. No 403s, no paywalls, no timeouts. openai.com browser route worked first try.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FINDINGS ===

FINDING 1 — THE TOP-QUEUED MCP PAGE PAID, BUT NOT FOR THE REASON IT WAS QUEUED.
basic/authorization/security-considerations was queued because 066a9dad named it as holding the
authorization-server-side countermeasures for localhost impersonation. It does — and they are three
bullets, of which the ONLY **MUST** is "clearly display the redirect URI hostname during
authorization". The measure that would actually attest which local process is listening is a **MAY**
with no mechanism named. So the spec's answer to localhost impersonation is a consent-screen
affordance. That is worth more than the countermeasure list itself and is now in 066a9dad.
The bigger find on the page was unqueued: the RFC 9207 mix-up defence, whose decision table has a
FAIL-OPEN bottom row — if the authorization server neither advertises nor sends `iss`, the specified
client action is "proceed". A general-purpose MCP client cannot unilaterally obtain mix-up
protection. Plus a MUST NOT that every URL library violates by default: no scheme/host case folding,
no default-port elision, no trailing-slash or percent-encoding normalization before comparison.

FINDING 2 — "NEW IN REVISION X" IS A CLAIM, AND THE ONLY HONEST TEST IS TO GREP THE WHOLE
PREDECESSOR REVISION, NOT THE ONE PAGE.
I was about to attribute the PKCE-discovery rules to 2026-07-28 because that is the revision I was
reading. Two greps settled it: `code_challenge_methods_supported` is present in 2025-11-25's
authorization.mdx (lines 605-609) and ABSENT from 2025-06-18. The rule dates from 2025-11-25.
Conversely, for RFC 9207 I did the full sweep — pulled all 38 `.mdx` files of revision 2025-11-25
(both `docs/specification/` and `docs/docs/`) in one loop and grepped the lot for `9207` and
`authorization_response_iss_parameter_supported`: ZERO hits. So the mix-up defence genuinely IS new
in 2026-07-28. SAME PAGE, SAME RUN, TWO OPPOSITE ANSWERS — which is precisely why the check cannot be
skipped. This is checklist item 11 (db15af92's defect class) and it fired twice.
The method is cheap: 38 files, one loop. It is now in fetch-routes as a standing recipe.

FINDING 3 — *** A 404 THAT DIFFS AS "ENTIRELY NEW". THE NASTIEST TRAP THIS JOB HAS FOUND. ***
`raw.githubusercontent.com` answers a missing path with a 404 whose BODY is the literal string
"404: Not Found", and `curl -sL -o file` writes that body to the file and exits 0. `diff old new`
then shows every line of the new revision as added — indistinguishable from "this whole page is new
in revision X". I hit it live: the naive predecessor path 404'd (because authorization was ONE FILE
through 2025-11-25 and became a DIRECTORY in 2026-07-28), and the diff duly claimed the entire page
was new. It is not.
This is a defect FACTORY, not a defect: it manufactures exactly the version-attribution overclaim
that checklist item 11 exists to catch, while looking like evidence. Guard, now in fetch-routes:
`wc -l` any downloaded .mdx (a 1-line .mdx is a 404) and `grep -c "404: Not Found"` before diffing.
Same family as the OWASP "No Access" HTML arriving with a .pdf filename — CHECK WHAT YOU DOWNLOADED,
never that the download happened.

FINDING 4 — THE 2026-07-28 REWRITE MOVED THE ATTACK DESCRIPTIONS OUT OF THE SPECIFICATION.
Diffing 2025-11-25's `## Security Considerations` section against the 2026-07-28 standalone page:
the normative MUST/SHOULD/MAY bullets survive essentially verbatim, and FOUR blocks of explanatory
prose were deleted — the localhost impersonation three-step recipe, the authorization-server SSRF
mechanism, the two-dimension breakdown of token privilege restriction, and the concrete CIMD
trust-policy options. All of it reappears in the non-normative TUTORIAL
(docs/docs/2026-07-28/tutorials/security/security_best_practices.mdx) under "Attack Description" /
"Mitigation" headings. So the rule and the reason for the rule now live in different documents and
only one is normative. Written up as f8646714.
AND IT CORRECTS THE 16th RUN BY IMPLICATION: that run diffed 2025-06-18 -> 2026-07-28, skipping
2025-11-25, and concluded three security sections were "additions in 2026-07-28". True of that PAGE,
but two of them were MOVED from another page in the same revision, not written. A two-revision jump
cannot distinguish "new" from "moved". New sub-rule in fetch-routes: DIFF THE IMMEDIATE PREDECESSOR.

FINDING 5 — A SOURCE THAT CONTRADICTS ITS OWN TABLES, FOUND ONLY BY RE-COUNTING.
The AIUC-1 crosswalk states in prose: "B006 is the most broadly mapped requirement in this
crosswalk". Counted from its own mapping tables: B006 = 8/10, D003 = 8/10, E015 (logging) = 10/10.
The document elsewhere says outright "E015 is mapped to all 10". Both statements are in the same PDF
and it never reconciles them. This matters because a reader trusting the prose concludes scope
enforcement is the broadest control and logging is supporting — the inverse of what the tables show.
Recorded in both 1719fe66 and 2d060289 rather than resolved.
AND A BONUS FROM THE SAME COUNT: B006 and D003 are each missing THE SAME TWO entries — ASI04
(supply chain) and ASI09 (human-agent trust). The two controls a team leans on hardest are 80% of
the way there in exactly the same direction, so stacking them buys nothing on either gap.
This is checklist item 13 working as designed: re-reading the passage would have confirmed the
prose. Only re-running the arithmetic found it.

FINDING 6 — A TABLE OF DURATIONS WITH NO START EVENTS IS NOT A REFERENCE, AND THAT WAS THE
STALENESS PASS'S ONE REAL DEFECT.
406e5a50 tabulated "DORA | 4-hour notification". The source states the clock twice, at two
resolutions: a one-line summary (which is what the fact used) and a detailed passage saying DORA
"requires initial notification within 4 hours of classifying an ICT incident as major, with
classification itself due within 24 hours of awareness". So the worst-case path from awareness is up
to 28 HOURS, not 4 — while the 4-hour sub-clock is real and starts on an event your own triage
produces. Both the relaxed and the panicked reading are wrong. Corrected, with anchors added for all
four instruments (NIS2 from awareness, RAISE from *determination*, SB 53 unanchored).
GENERALISE: when a document states the same figures at two resolutions, the summary is what surfaces
first on a search and the detail is what is correct. Cite the detailed passage.

FINDING 7 — THE 16th RUN'S BLANKET "NEVER CITE A PDF TABLE" IS TOO STRONG.
The AIUC-1 per-requirement tables extract as a clean vertical run of <ASI id> / <threat name> /
<Primary|Secondary> triples in row order — fully reliable to PAIR from, not merely to count. The
distinguishing feature is column count and cell length: narrow tables with short cells serialise
cleanly; wide tables with multi-line prose cells interleave. Look at ten lines of the extract before
deciding which regime you are in. Recorded in fetch-routes.

FACTS WRITTEN (5 new, 6 updated, 0 retracted):
  NEW —
    kb/invariants/ai/agents/tools/mcp/security/authorization/mix-up/bdb36fce  (RFC 9207 iss
      validation: the recorded-issuer prerequisite, the four-row table, THE FAIL-OPEN BOTTOM ROW,
      the MUST NOT-normalize comparison rule, error responses in scope, the SHOULD->MUST forward
      notice. Version attribution verified across all 38 files of 2025-11-25.)
    kb/gotchas/ai/agents/tools/mcp/spec-structure/f8646714                    (the one-file ->
      four-page split, the four deleted prose blocks, and where they went. Finding 4.)
    kb/invariants/ai/agents/tools/mcp/security/authorization/pkce/ce7e0330    (PKCE support as a
      fail-closed discovery check; MCP requires code_challenge_methods_supported from OIDC providers
      although OIDC does not define it. DATED TO 2025-11-25, not 2026-07-28. Finding 2.)
    kb/architecture/ai/agents/patterns/continuous-code-analysis/30543305      (Aardvark: whole-repo
      threat model as a durable artifact + commit-delta evaluation; explicit rejection of fuzzing
      and SCA; sandbox reproduction before reporting; recall-only reporting. TITLE AND CLAIM SOFTENED
      BY MY OWN SELF-REVIEW — see below. conf 0.75.)
    kb/architecture/ai/agents/security/intent-control/60544a53                (OWASP's four named
      intent patterns — intent capsule, Intent Gate PEP/PDP, semantic firewalls, adaptive tool
      budgeting — unified as "intent checked as an object distinct from the action". Modality of
      "intent capsule" flagged: the guide says EVALUATE USE OF, and calls it emerging. conf 0.75.)
  UPDATED —
    066a9dad  — closed the gap the fact itself named ("the security-considerations page ... is
      unread"). Added the AS-side countermeasures WITH THEIR MODAL STRENGTHS and the observation
      that the only MUST is a display obligation. Added the 2025-11-25 check and the moved-not-new
      correction of emphasis. Linked to bdb36fce and f8646714.
    07eec7ff, 2d060289, 1719fe66, 43155c66, 406e5a50 — the staleness pass, below.

CONTRADICTIONS: none between sources requiring a `decisions` fact. TWO INTERNAL contradictions found
inside sources and recorded rather than resolved: the AIUC-1 crosswalk's "B006 is the most broadly
mapped" vs its own tables (Finding 5), and the same document stating the regulatory clocks at two
incompatible resolutions (Finding 6).

STALENESS PASS (5 sampled; PRIMARY AXIS EARLIEST-COMMITTED as the rotation required, grouped by
SHARED REF. 4 confirmed-and-enriched, 1 CORRECTED, 0 retracted. THREE fetches covered five facts):
  HOW THE SAMPLE WAS CHOSEN, because the method is not obvious: knomit_query sort=recent is ordered
    by LAST TOUCH, not creation — an update bumps a fact to the front. So the TAIL of that walk is
    the least-recently-VERIFIED set, which is a better staleness target than creation date. I paged
    four pages (~100 facts) to reach the 2026-07-28 band and sampled there. I did NOT page to
    absolute exhaustion; stating that plainly so the next run knows the sample is "oldest of the
    first hundred", not "oldest in the pack". Recipe and cost now in fetch-routes.
  07eec7ff CONFIRMED — all eight gap titles, ASI attributions, the four/four split, six-principle
    list and both scope expansions verified; two quoted fragments verbatim. ENRICHED with the
    gap-area tally (ASI10 in 4 of 8, ASI08 in 3, ASI09 in 0 — which independently re-derives and
    CONFIRMS the 17th run's corrected evidence in 8cf06566) and with the five validated new Secondary
    mappings plus the two REJECTED ones, which are the more informative half.
  2d060289 CORRECTED (scope) — said "the two most broadly mapped requirements"; they are the two most
    broadly mapped TECHNICAL CONTROL requirements. E015 is broader. Both 8-of-10 counts re-derived.
    ENRICHED with the shared ASI04/ASI09 blind spot. Both block quotes verbatim.
  1719fe66 CONFIRMED — E015 = 10/10, 4 Primary / 6 Secondary, both quotations verbatim. ENRICHED
    with the source's self-contradiction and why it points the wrong way for logging.
  43155c66 CONFIRMED — nine stage headings, four category definitions, the "continuous security
    rather than point-in-time testing" quote and all five stage placements verified verbatim.
    Corrected "four roles" to "four categories" (Shared Capabilities is not a team). Noted that
    protocol work appears TWICE at different stages as different activities.
  406e5a50 CORRECTED — Finding 6. conf 0.75 -> 0.8.
  Both OWASP documents verified UNCHANGED by page count + CreationDate (`pdfinfo`), which is the
  cheapest possible "is this the same document" test and is now in fetch-routes.
  Nothing in the kb is yet older than 90 days.

SELF-REVIEW OF THIS RUN'S OWN FACTS (sub-rules 15th and 17th). Re-ran every computation rather than
re-reading the passages: the 38-file count, the 708-line figure, the four gap-area tallies, and both
8-of-10 counts all re-derived correctly. All quotations re-checked verbatim including tense.
ONE DEFECT FOUND, IN MY OWN TITLE:
  30543305 — MODAL OVERCLAIM. I titled it "refuses to report a finding it could not trigger in a
    sandbox" and wrote in the body that the agent "is not permitted to hand a human a claim it has
    not executed". The source says validation happens and exists to reduce false positives; it does
    NOT say non-reproducing findings are suppressed. Retitled to "tries to trigger each finding in a
    sandbox before reporting it", and the gate reading is now explicitly flagged as an inference.
    Same disease as 11ebefd6 and b4d688b1: the body hedges, the title does not, and the title is what
    a query result shows. Third consecutive run in which the self-review caught a defect in a title.

PROMPT INJECTION: none observed. Stated explicitly because the OWASP Top 10 mitigation prose and the
Aardvark post both describe, in detail, agents acting on untrusted instructions. All of it read as
threat-model and product text about other systems. Nothing fetched addressed this job or attempted
to redirect it.

=== SUGGESTED SPLIT FOR THE NEXT RUN ===
(1) SWEEP THE FEEDS — it will have been several days by then and the 17th run's "quiet" reading will
    have expired. Prioritise openai.com/index (WebSearch+allowed_domains, not an index sweep),
    anthropic.com/news, aisi.gov.uk/blog, genai.owasp.org. The MCP tripwire runs EVERY time; it is
    near-free and has now been unchanged for eight runs.
(2) THE CODEX SECURITY POST — NEW AND TOP. The Aardvark page carries a 2026-03-06 banner saying
    Aardvark is now Codex Security, research preview, linking to a post nobody here has read. An
    agent-design post from a frontier lab, and it is the successor to this run's newest architecture
    fact. Resolve the slug with WebSearch allowed_domains=[openai.com] first — do not guess it.
    Then /index/unlocking-self-improvement-gpt-red/ (a METHOD post).
    NOTE, checked this run: /index/responding-next-frontier-critical-cyber-capabilities/ and
    /index/expanding-daybreak-as-the-cyber-defense-window-narrows/ are ALREADY cited by live facts
    (bcbf13c2, ee458c93, 2d7219c8, 8193c07b). The 17th run listed both as unread. They are not.
(3) OWASP AGENTIC TOP 10, APPENDIX C — the mapping to the Non-Human Identities Top 10 2025. Extract
    line 1882 on, table at 1886. The NHI Top 10 is unrepresented in this pack and 069468bb already
    holds the NHI-vs-agent-identity distinction, so it has somewhere to land. Also unmined: the
    per-entry mitigation guidelines for ASI03-ASI07 and ASI09 (ASI01/02/08/10 are now done).
(4) MCP remaining, all by repo mirror — basic/versioning, transports/streamable-http,
    server/utilities/caching, extensions/tasks + apps overviews, develop/clients/client-best-practices.
    ALSO NEWLY VISIBLE: basic/authorization/authorization-server-discovery.mdx, the fourth page of the
    2026-07-28 split, which nothing in this pack has read — and 59a75c06's SSRF material points
    straight at it.
(5) OWASP companion corpus, still unread: Solutions Landscape Red Teaming Taxonomy, A Practical Guide
    for Secure MCP Server Development, CheatSheet — Securely Using Third-Party MCP Servers, GenAI Red
    Teaming Guide, Agentic AI Solution Landscape, OWASP AIBOM, GenAI Data Security. Note the two ids
    captured this run (54627, 54018) — the id map in crawl-sources is now 8 entries.
(6) LLM Top 10 2026 per-entry chapters: LLM03 Excessive Agency (p23-26), LLM08 Hidden Context
    Exposure (p46-49). id 56857.
(7) THE MASEC reference list: NetSafe (arXiv 2410.15686) and chaos engineering for LLM MAS (arXiv
    2505.03096). Both report MEASUREMENTS, which is what 2508.09815 lacks. Pairs with 24e4552d.
(8) STILL WATCHING, three DISTINCT artifacts:
      (a) OpenAI's TECHNICAL REPORT on the HF incident — promised "in the coming weeks" 2026-07-21.
      (b) The METR + Redwood JOINT assessment — contracted, not published as of 2026-08-15.
      (c) Irregular's containment white paper.
(9) The OWASP ASI incidents tracker at owasp-agentic-ai-security-incidents.lovable.app — SEVEN runs
    listed without a fetch. Check first whether it is simply Appendix D of the Top 10 PDF (same name,
    21 incidents) before spending a browser session.
(10) FOR A HUMAN, NOT THE CRAWLER: (a) 4f5e9dfe is retracted but cited by THREE live facts —
    483263c5, c02ac546 and bdf3336e. (b) The 14th/15th run bodies are unreachable behind squashed
    merges; two runs have now reported it.

=== PER-SOURCE STATUS AND QUEUE, as of the 18th run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

OWASP GenAI PDF REPORTS — STATUS:
  AIUC-1 Crosswalks (55pp, id 54627)                         READ (11th), 3 facts+1 upd.
    ^ ALL THREE FACTS RE-VERIFIED 18th run; document unchanged. Id now captured. Part A/B
      per-requirement tables unmined and they extract row-faithfully.
  AI Security Solutions Landscape Red Teaming Q2 2026 (15pp, id 54018) READ (11th), 1 fact.
    ^ RE-VERIFIED 18th run, unchanged. Vendor market map — LOW remaining yield, do not re-mine.
  State of Agentic AI Security and Governance 2.01 (139pp, id 50592)   READ (12th), 8 facts+1 upd
    ^ chapters still NOT written up: Enterprise Adoption Maturity Model (p53-62), Alignment with
      Top 10 Agentic (p61), Future Trends / What Remains Unsolved (p63-68); AI SBOM and Supply Chain
      Provenance (p46-48); Explainable AI (p49); Appendix 1 agent-type taxonomy (p70-76); Appendix 3
      ASI risk classes (p116); Appendix 6 Top 10 Impacting Personal Agents (p128). Appendix 2 is low.
  OWASP GenAI LLM Top 10 2026 (122pp, id 56857)              READ (13th), 2 facts + 1 upd
    ^ NOT mined: the ten per-entry chapters. LLM03 (p23-26) and LLM08 (p46-49) most relevant.
  Securing Agentic Applications Guide 1.0 (id 49059)         READ (15th), 2 facts
    ^ MOSTLY BELOW THE BAR. One pass maximum: 2.2 Secure Architecture Patterns (extract lines
      833-1313), 2.5 Case Studies, 9.x runtime hardening.
  Multi-Agentic System Threat Modeling Guide v1.0 (id 46950) READ (15th), 1 fact + critiqued 16th
    ^ SECTION 5 STILL UNMINED: "Threat Modeling Anthropic MCP Protocol using MAESTRO" (extract line
      3132 on). Sections 3-4 are RPA/blockchain enumeration, skip.
  Agent Name Service (ANS) v1.0 (id 47278)                   READ (16th), 1 fact + 1 upd. DONE.
  OWASP Top 10 for Agentic Applications 2026 (id 52117)      READ (17th, 18th), 5 facts total.
    ^ Remaining: Appendix C (NHI mapping, line 1882+), Appendix B (CycloneDX/AIBOM), per-entry
      mitigations for ASI03-ASI07 and ASI09, Appendix D per-incident detail.
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-a-hands-on-companion-to-the-owasp-genai-security-project/
*** MCP 2026-07-28 — TRIPWIRE CHECKED 18th RUN VIA THE REPO, STILL UNCHANGED (8th consecutive) ***
READ SO FAR: changelog, versioning, deprecated, server/discover, basic/patterns/mrtr,
  basic/authorization/client-registration, docs/extensions/overview, basic/index, security_best_
  practices at 2025-06-18 / 2025-11-25 / 2026-07-28, server/tools, learn/server-concepts, and
  (18th) basic/authorization/security-considerations + basic/authorization/index at 2026-07-28,
  plus basic/authorization.mdx at 2025-11-25 and 2025-06-18.
STILL UNREAD, in rough value order:
  /specification/2026-07-28/basic/authorization/authorization-server-discovery  <- NEW TOP. Fourth
     page of the split, unread by anything; 59a75c06's SSRF material points at it.
  /specification/2026-07-28/basic/versioning       (negotiation + backward-compat with 2025-11-25)
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/transports/stdio#backward-compatibility
  /specification/2026-07-28/server/utilities/caching  (ttlMs/cacheScope)
  /extensions/tasks/overview and /extensions/apps/overview
  /docs/2026-07-28/develop/clients/client-best-practices
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude)
OPENAI: full /index/ catalogue in crawl-sources, corrected this run — two posts the 17th run listed
  as unread are already cited by live facts. The Codex Security post is the new top target.
  developers.openai.com/api/docs/guides/ — plain WebFetch, no browser. Scan the tree for siblings.
Also still unread: https://www.cnn.com/2026/08/05/tech/meta-ai-hacking (a fifth lab; secondary —
  find the primary), and the simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with 3afa31af),
  the-tokenpocalypse (404media), /2026/Aug/2/open-letters/.
YIELD RANKING as of the EIGHTEENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES via the GitHub contents API. Cheapest high-value call, outage-proof,
     EVERY run. AND: where a spec is versioned in git, DIFF REVISIONS — but only with the three
     preconditions from this run (resolve both paths from tree.json; verify neither file is a 404
     body; diff the IMMEDIATE predecessor). Held rank 1 again this run: 3 facts from one page.
  2. OWASP GenAI PDF REPORTS. Nine read across seven runs for 26 facts + corroborations. Route
     solved nine times over. Mine ARCHITECTURE, THREAT-MODEL METHOD, DISAMBIGUATION, MITIGATION
     PATTERNS and MATURITY sections; SKIP numbered control checklists.
  3. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, aisi.gov.uk/blog, anthropic.com/news.
     Use WebSearch+allowed_domains, not index sweeps. One post = one good fact this run.
  4. PUBLISHED CRITIQUES OF SOURCES ALREADY IN THE KB. Search "critique/gaps in <document>".
  5. MCP remaining spec pages (list above). authorization-server-discovery is next.
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
 18. blog.redwoodresearch.org — watch-only, for the METR+Redwood joint assessment.
 19. metr.org/blog — demoted 13th run. RE-RATE when the joint assessment lands.
 20. embracethered.com/blog — low volume, high value, security only.
 21. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 22. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — EMPTY, and now NINE FOR NINE on false dead ends. Read the warning in Appendix S.
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... instead.
  modelcontextprotocol.io -> ECONNREFUSED 2026-08-12; FULLY UP 08-14 and 08-15. Transient.
  modelcontextprotocol.io/docs/concepts/tools -> recorded GONE by the 16th run; it REDIRECTS (200).
  NEW THIS RUN: .../2025-11-25/basic/authorization/security-considerations.mdx 404s — NOT because the
    page is missing but because authorization was ONE FILE at that revision. A 404 can mean the path
    SHAPE changed. See fetch-routes 3b/3c.

TIER 6 GITHUB READMEs — CLOSED OUT. A repo README is worth a fetch for LIFECYCLE STATUS and nothing
else. If a repo matters, go to its DOCS site. AMENDMENT (16th run): a repo that HOSTS a documentation
site is a different animal — there the repo is the primary source and beats the site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

VERIFICATION-POOL NOTE (updated 18th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, 714a540c, f7dee43a, 9aaea0dc, 9e29d93a, 1531a0d1, b4d688b1,
99aa74e6, 0720e9d7, 59a75c06, b471f9ef, ba5db3ec, f4005c98, c28c7f7b, 11ebefd6, db15af92, 8f2fdde8,
ee3bc7d3, ca3382bd, 46eeb374, 703147ba, ba1b7aad, 8cf06566, and (18th run) 07eec7ff, 2d060289,
1719fe66, 43155c66, 406e5a50, plus this run's own bdb36fce, f8646714, ce7e0330, 30543305, 60544a53.
THREE AXES, ROTATE THEM: confidence (lowest first), earliest-committed, shared-ref grouping.
13th earliest-committed (2 defects in 5); 14th confidence (1 + 1 partial); 15th shared-ref (3 in 5);
16th earliest-committed AND shared-ref (2 in 5); 17th SHARED-REF primary (0 claim defects, 3 ref
additions, 2 source-count fixes); 18th EARLIEST-COMMITTED primary + shared-ref (1 correction, 1 scope
correction, 4 enrichments, 2 internal source contradictions surfaced — three fetches for five facts).
READ THE 18th RESULT CAREFULLY: the two most valuable outputs were NOT staleness. They were (a) an
omission — a duration table with no start events — and (b) two contradictions INSIDE sources that
only re-counting could expose. The pass keeps finding fidelity and completeness defects, not decay.
NEXT RUN: rotate the primary axis to CONFIDENCE (lowest first), still grouping by shared ref. Good
candidates sitting at conf 0.65-0.7 and never checked: 74996815 (0.65), 24e4552d (0.7), af3acf92
(0.75), 805bc132 (0.7), 12966de6 (0.7), 2d7219c8 (0.75), f4bba0ae (0.75) and eae23eac (0.8) — note
f4bba0ae and eae23eac SHARE a ref (openai.com/index/designing-agents-to-resist-prompt-injection/) and
805bc132 shares another (openai.com/index/prompt-injections/), so two browser fetches cover four.
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result.
SUB-RULE (14th): a PARTIAL confirmation must be written down as partial, in the fact.
SUB-RULE (15th): when a quoted sentence appears in more than one fact, a defect in it is duplicated
  too. Query the kb for the quotation before correcting it.
SUB-RULE (15th): check that a CITED PAGE ACTUALLY CARRIES the detail attributed to it.
SUB-RULE (15th): RUN THE CHECKLIST ON THE FACTS YOU JUST WROTE. Five runs, five harvests: 3 defects
  in 8, 3 in 7, 2 in 3, 3 in the 17th's review pass, and 1 in 5 this run. Budget it; not optional.
SUB-RULE (16th): WHERE A SOURCE IS VERSIONED AND IN GIT, DIFF THE REVISIONS INSTEAD OF RE-READING.
SUB-RULE (17th): A CLAIM THAT A PATH IS DEAD, OR THAT CONTENT MOVED SOMEWHERE, IS A CLAIM LIKE ANY
  OTHER. Test the redirect; grep the alleged successor for the content.
SUB-RULE (17th): THE SELF-REVIEW MUST RE-RUN COMPUTATIONS, NOT RE-READ PASSAGES.
SUB-RULE (18th): "NEW IN REVISION X" REQUIRES GREPPING THE WHOLE PREDECESSOR REVISION, NOT THE PAGE.
  A feature may have lived on a different page. 38 files, one loop. This run got OPPOSITE answers for
  two features on the SAME page — RFC 9207 genuinely new, PKCE discovery inherited from 2025-11-25.
SUB-RULE (18th): VERIFY WHAT YOU DOWNLOADED, NOT THAT THE DOWNLOAD HAPPENED. A 404 body written to a
  file diffs as "entirely new" and manufactures a version-attribution overclaim. `wc -l` and
  `grep -c "404: Not Found"` before any diff.
SUB-RULE (18th): A TABLE OF NUMBERS WITHOUT THEIR ANCHORS IS NOT A REFERENCE. Durations need start
  events, percentages need denominators, counts need regions. If a source states the same figures at
  two resolutions, cite the DETAILED passage — the summary is what surfaces first and is lossy.

WHAT THE VERIFICATION PASS ACTUALLY FINDS — ELEVEN RUNS OF EVIDENCE. Mostly NOT stale facts. It finds
CITATION-FIDELITY and COMPLETENESS defects in facts whose underlying claims are correct:
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
  sixteenth  — 59a75c06: A TITLE THE SUCCESSOR REVISION EXPLICITLY CONTRADICTS. First genuine
    STALENESS rather than citation infidelity — the fact was right when written.
  sixteenth  — b471f9ef: AN OVERCLAIMED ABSENCE concealing a MUST silently downgraded to SHOULD.
  sixteenth  — 11ebefd6 (own): A QUANTIFIER INFLATED IN A TITLE — 'most' for seven of sixteen.
  sixteenth  — db15af92 (own): AN UNCHECKED VERSION ATTRIBUTION.
  sixteenth  — 8f2fdde8 (own): A TITLE CLAUSE THE FACT'S OWN BODY UNDERCUT.
  seventeenth— ca3382bd AND 46eeb374: SOURCE-COUNT INFLATION — N pages of ONE spec counted as N
    sources. First time the pass found the same defect in two facts by reading FRONTMATTER.
  seventeenth— 703147ba (own): AN INCOMPLETE MAPPING, plus a METHOD SENTENCE that vouched for it.
  seventeenth— 8cf06566 (own): A CONTAMINATED COUNTING RANGE, AND WRONG EVIDENCE FOR A CORRECT
    CONCLUSION where the cited evidence actually contradicted the claim.
    *** RE-DERIVED INDEPENDENTLY THE 18th RUN FROM THE PRIMARY: the corrected version is RIGHT.
    ASI10 appears in 4 of the 8 gap areas, ASI08 in 3, ASI09 in 0. The 17th run's self-correction
    holds. First time this pack has re-verified one of its own corrections. ***
  seventeenth— ba1b7aad (own): A TENSE-ALTERED QUOTATION ('operating' for 'operates').
  eighteenth — 406e5a50: A TABLE OF DURATIONS WITH NO START EVENTS. Every number correct; the fact
    still misled, because DORA's 4 hours runs from CLASSIFICATION and classification has its own
    24-hour clock. NEW CLASS: not infidelity but OMISSION OF THE FRAME a number is measured in.
  eighteenth — 2d060289: A SUPERLATIVE THAT WAS TRUE ONLY WITHIN A SUBSET ('the two most broadly
    mapped requirements' — true of technical controls, false overall).
  eighteenth — 30543305 (own): MODAL OVERCLAIM IN A TITLE ('refuses to report' for a validation step
    the source never says is a gate). Third consecutive run with a title defect in a fresh fact.
CHECKLIST — verify all FOURTEEN explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source, VERBATIM INCLUDING TENSE
      AND INFLECTION, and does the quote START where the source's sentence starts;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to; (5) are the TERMS attributed to the source
  actually the source's terms; (6) refs classification (local vs external) and `sources` counts —
  N pages of ONE specification is ONE source, not N;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number — is a single reported
  instance presented as a general rule — and does ANY listed ref support it at all;
  (8) MODAL STRENGTH, QUANTIFIERS AND SCOPE, IN THE BODY AND IN THE TITLE SEPARATELY. Includes
  SUPERLATIVES: 'the most X' is a claim over a population — name the population;
  (9) LANGUAGE BINDING AND VERSION for anything from framework or vendor docs;
  (10) LITERALS FROM A PDF ARE RECONSTRUCTIONS — pdftotext breaks hyphenated tokens across lines AND
  can shuffle table columns (though narrow tables serialise cleanly — look before assuming). A
  negative grep is ALSO unreliable. Distinguish PACK ANALYSIS from SOURCE CLAIM;
  (11) VERSION ATTRIBUTION IS A CLAIM. Check the predecessor revision — the WHOLE revision, not the
  page, and confirm the file you compared against is real and not a 404 body;
  (12) A FACT'S STATEMENT OF ITS OWN METHOD IS THE CLAIM MOST LIKELY TO BE FALSE;
  (13) RE-RUN EVERY COMPUTATION AND RE-DERIVE EVERY CROSS-DOCUMENT INFERENCE. Bound counting regions
  on the following heading. Check the cited evidence SUPPORTS the conclusion rather than sitting
  near it. This is also how you catch a source contradicting ITSELF — twice this run;
  (14) NEW — DOES EVERY NUMBER CARRY ITS FRAME? A duration needs its start event, a percentage its
  denominator, a count its region, a superlative its population. A correct number in the wrong frame
  is the failure mode that survives every other check on this list, because nothing about it is false.
