---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-15 (nineteenth run). SAME DAY as the 18th, roughly two hours after it committed — so per
the standing rule NO broad feed sweep. Only the MCP tripwire ran. The whole budget went to the 18th
run's queue, taking its two top-ranked items, and both paid.
*** A POST-COMMIT REVIEW PASS WAS RUN AFTER THE FACTS WERE WRITTEN. IT FOUND ONE DEFECT IN THIS RUN'S
OWN OUTPUT (a joined claim + an uncounted appendix). THE IN-RUN SELF-REVIEW SEPARATELY FOUND ONE
(a one-page grep supporting a whole-revision claim). Both are corrected in place. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***

=== HISTORY WALK ===
REVISIONS READ: 5 bodies, across 4 runs (two HEAD revisions belong to the same run).
  a21ad1c0 (HEAD, 2026-08-15T14:02:16Z) — the 18th run's final body.
  7a9ec830 (2026-08-15T13:47:52Z)       — the 18th run's first write. Same run; deduped, not skipped.
  3bc37431 (2026-08-14T12:51:03Z)       — the 17th run's body.
  3c6323cd (2026-08-12T21:25:35Z)       — the 16th run's body.
  8b9a768d (2026-08-12T00:27:10Z)       — the 13th run's body, carrying the AUTHORITATIVE 190-URL union.
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z. more_available was FALSE at 8b9a768d — the walk
terminated on the API's own signal, not on an assertion in a body. No call failed; no retry needed.

*** THE GAP IS STILL THERE. THIRD RUN REPORTING IT. NOT MINE TO FIX. ***
The 14th and 15th runs' bodies remain UNREACHABLE — their per-run commits were squashed into merge
commits ("Merge pull request #8", "#6") and the hashes recorded in prose (e61629fc, 8be9e4de,
5ab895cf) do not resolve. ALREADY_CRAWLED = 190 (enumerated at 8b9a768d) + 10 (16th) + 5 (17th) +
7 (18th) + 4 genuinely-new (this run) = **216 URLs I can NAME**, against an asserted true total of
~232. The ~16 unenumerable URLs from the 14th/15th window are described at source level in the 17th
run's body and I steered clear of all of it.
FOR A HUMAN: three consecutive runs have now reported this. It will not heal on its own.

*** THE DANGLING-REF PROBLEM IS ALSO STILL THERE. NOT RE-CHECKED THIS RUN, NOT FIXED. ***
kb/invariants/ai/agents/security/threat-taxonomy/4f5e9dfe.md is retracted but still cited by THREE
live facts: 483263c5, c02ac546, bdf3336e. Carried forward from the 18th run unverified — saying so
plainly rather than re-asserting it as though I had re-checked. Still for a human.

recurring-feed indexes swept: ONE, deliberately.
https://api.github.com/repos/.../contents/docs/specification  (MCP tripwire — UNCHANGED. 2024-11-05,
  2025-03-26, 2025-06-18, 2025-11-25, 2026-07-28, draft. NINTH consecutive run unchanged.)
No other feed swept, on purpose: the 17th run swept four and found three empty, and the 18th ran only
hours ago. Do not read this as a skipped sweep. THE NEXT RUN SHOULD SWEEP if any real time has passed.

articles newly crawled (4 genuinely new URLs):
https://raw.githubusercontent.com/.../docs/specification/2026-07-28/basic/authorization/authorization-server-discovery.mdx  <- 1 new fact + 2 updates
https://raw.githubusercontent.com/.../docs/specification/2026-07-28/basic/authorization/client-registration.mdx  (raw form; site form read earlier)
https://raw.githubusercontent.com/.../docs/specification/2025-03-26/basic/authorization.mdx  (vintage floor check)
https://openai.com/index/codex-security-now-in-research-preview/   <- browser route, slug resolved by WebSearch, 1 major update
re-fetched for the staleness pass, already known: openai.com/index/designing-agents-to-resist-prompt-injection/,
  openai.com/index/prompt-injections/, arxiv.org/pdf/2508.09815, and the 2026-07-28 index.mdx +
  security-considerations.mdx, 2025-11-25 and 2025-06-18 authorization.mdx.
VERIFICATION SWEEP, not article reads: ALL 41 files of revision 2025-11-25, enumerated ON THE
  REVISION DATE across docs/docs, docs/specification AND schema/2025-11-25 (fetch-routes 3d), each
  404-guarded (0 hits) and swept unanchored.

errored / not obtained: NONE. No 403s, no 404s, no paywalls, no timeouts. The openai.com browser
route worked first try on three posts; the OWASP route was not needed this run.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FINDINGS ===

FINDING 1 — THE TOP-QUEUED MCP PAGE HELD A RULE WITH NO ANCESTOR AT ALL, WHICH MEANS A SPEC SPLIT IS
NOT SAFE TO TREAT AS A REORGANISATION.
The 18th run queued authorization-server-discovery as "the fourth page of the split, unread by
anything". The assumption behind reading a split page is that its content moved from somewhere. Here
it did not. 2026-07-28 requires that after retrieving an AS metadata document the client validate that
the document's `issuer` is IDENTICAL to the issuer identifier used to build the well-known URL, and
**MUST NOT** use the metadata otherwise — with the spec's own attacker example (a document served from
`attacker.example` claiming `"issuer": "https://honest.example"`). That rule is absent from the whole
of 2025-11-25.
AND THE HALVES SHIPPED A REVISION APART, WHICH IS THE ACTUAL FINDING: the PROBING rule — try three
well-known endpoints for a path-ful issuer, two for a path-less one, in a fixed order — is verbatim in
2025-11-25. So the spec told clients to probe a server-named host one revision before it told them to
check that the answer belonged to the host they asked about. Written up as 36d792c3.
Corroborating detail that makes the omission a real gap rather than an obvious one: 2025-11-25 is not
a revision short on validation rules — it carries MUST-validate obligations for CIMD documents and for
token audience. The hole was specific to the AS metadata document.

FINDING 2 — *** IN .mdx, EVERY NORMATIVE KEYWORD IS BOLDED, SO GREPPING A NORMATIVE SENTENCE FINDS
NOTHING. A FOURTH INDEPENDENT MECHANISM FOR "A NEGATIVE GREP IS NOT PROOF OF ABSENCE". ***
Caught live and isolated in one step. Same file, three commands:
  grep -c "MUST NOT assume that credentials"  -> 0    (reads as absence)
  grep -c "assume that credentials"           -> 1    (it is there)
  grep -n "assume that credentials"           -> `**MUST NOT** assume that credentials valid for...`
The spec writes `**MUST**`, so the sentence a reader would quote does not exist as a literal string.
WHY THIS ONE IS WORSE THAN THE OTHER THREE: line-wrapping, hyphen-breaking and form feeds are all
pdftotext EXTRACTION artifacts, so "I downloaded clean text myself" rules them out. This one is in the
SOURCE BYTES and survives a perfect download. And this job greps MUSTs constantly — it is the single
most likely way for this pack to manufacture a false absence claim. Rule: never let a search term span
a normative keyword. Now fetch-routes 3e, and the negative-grep tally there is updated from three
mechanisms to four.

FINDING 3 — `file` AND `pdfinfo` DISAGREE ON PAGE COUNT, AND `file` IS WRONG. A FALSE-STALENESS
GENERATOR SITTING INSIDE THE 18th RUN'S OWN STALENESS RECIPE.
  file masec.pdf     -> "PDF document, version 1.5, 3 pages"    WRONG
  pdfinfo masec.pdf  -> "Pages: 8"                               CORRECT
Same bytes, same run, no re-download. The 18th run made page count the cheap "is this the same
document" test — correct, but only with `pdfinfo`. A run checking with `file` would have compared
"3 pages" against a recorded 8 and reported THE SOURCE CHANGED on a document that had not changed at
all. That is the exact false-positive twin of the 3c 404-body trap, which manufactures the opposite
error. `file` remains right for the one question route 2 asks it (PDF vs the HTML error page) and is
not a source of page counts. In fetch-routes as 2c.

FINDING 4 — A MODAL DOWNGRADE THAT WASN'T, AND THE CHECK THAT CAUGHT IT.
The discovery page says servers "can also include a `scope` parameter in the `WWW-Authenticate`
challenge"; 2025-11-25 says servers **SHOULD** include it. That is exactly the shape of the 16th run's
b471f9ef finding (a MUST quietly becoming a SHOULD), and I was one step from recording it.
IT IS NOT A DOWNGRADE. Grepping the whole 2026-07-28 split found the **SHOULD** alive on index.mdx
line 99; the discovery page's "can" is a non-normative pointer to it. A SPLIT DUPLICATES RULES THAT
STRADDLE THE SEAM, AND THE COPIES NEED NOT MATCH IN FORCE — and the weaker copy tends to sit on the
topic page, which is the page you actually navigate to for a topic question. New precondition (e) on
the revision-diff technique: before recording any weakening, grep EVERY page of the new revision and
cite the strongest statement. Mirror of preconditions (c)/(d): those catch content that MOVED, this
catches content that FORKED. Recorded in f8646714 as the split's second hazard.

FINDING 5 — THE CODEX SECURITY POST INDEPENDENTLY CONFIRMED A CORRECTION THE 18th RUN MADE TO ITSELF.
The 18th run's self-review softened 30543305's title from "refuses to report a finding it could not
trigger in a sandbox" to "tries to trigger", on the grounds that the Aardvark post never says a
non-reproducing finding is suppressed. The successor post settles it in the softened direction and
goes further: validation happens "where possible", and a SECOND, DEEPER tier exists only when the
product is "configured with an environment tailored to your project" — that tier is what enables
working proof-of-concepts. So validation is conditional on deployment configuration, and a finding's
existence means different things on different tiers. The gate reading is now positively excluded
rather than merely unevidenced.
THIS IS THE SECOND TIME THIS PACK HAS RE-VERIFIED ONE OF ITS OWN CORRECTIONS FROM A NEW PRIMARY (the
18th did it for 8cf06566). Both times the correction held. Worth continuing to track.

FINDING 6 — TWO POSTS, TWO HALVES OF ONE RATIO, AND NEITHER HALF IS AN ABSOLUTE.
Aardvark published RECALL ONLY (92% on golden repos, no precision). Codex Security publishes
PRECISION MOVEMENT ONLY — noise cut 84% "in one case", over-reported severity down >90%, false
positives down >50% — with no absolute precision and no recall. Every figure in the successor is a
relative delta against an unpublished baseline, so "84% less noise" has no denominator and ">50% fewer
false positives" leaves the residual rate unknown. The one quantity that would show whether the
validation stage works is the quantity neither post reports. Checklist item 14 in its purest form: the
numbers are all correct and all frameless.
SCALE FIGURES THAT DO CARRY THEIR FRAME: >1.2M commits scanned over 30 days across the external beta
cohort, 792 critical + 10,561 high-severity findings, "critical issues appeared in under 0.1% of
scanned commits" (my division: 792/1.2M = 0.066%, consistent).

FINDING 7 — A FACT'S OWN SOURCING NOTE WAS WRONG IN THE CAUTIOUS DIRECTION.
74996815 carried a self-imposed confidence penalty because its central claim "is asserted in a single
table cell and is not worked through anywhere in the text". Re-checking the paper: the class appears in
THREE separate tables — coverage verdict, threat description, and vector/scenario — with two different
phrasings of the description. The penalty was based on a false premise. conf 0.65 -> 0.7. The modality
caveat (anticipatory, unmeasured) is unchanged and is now the only thing holding it there.
WORTH NOTING AS A CLASS: every previous self-sourcing defect this pack has found was an OVERCLAIM.
This is the first UNDERCLAIM — a fact that undersold its own evidence. Checklist item 12 says a fact's
statement of its own method is the claim most likely to be false; it does not say the error is always
in the flattering direction, and this is the counter-example.

=== FACTS WRITTEN (1 new, 8 updated, 0 retracted) ===
  NEW —
    kb/invariants/ai/agents/tools/mcp/security/authorization/discovery/36d792c3  (the issuer-identity
      validation MUST + its attacker example; the probing rule dated to 2025-11-25 and the validation
      rule to 2026-07-28, both verified across the whole revision; the RFC 8414 §3.1/§5-but-never-§3.3
      citation pattern; the server-one/client-both asymmetry checked and confirmed NOT new;
      distinguished from bdb36fce's RFC 9207 defence, which fails OPEN where this fails CLOSED.)
  UPDATED —
    30543305  — the Codex Security successor. sources 1->2, conf 0.75->0.85. Editable + feedback-
      trained threat model as the learning substrate; tiered conditional validation (Finding 5); the
      recall-vs-precision-delta asymmetry (Finding 6); the maintainer finding that the binding
      constraint is reviewer attention, not detection capacity. CVE CLAIM CORRECTED BY THE REVIEW PASS.
    00fd386c  — the SIMULTANEOUS multi-AS case: one PRM document can list several independent
      authorization servers, client identifiers are per-AS, clients MUST keep separate registration
      state and MUST NOT assume portability. The existing fact framed AS change as a migration event;
      it is also a concurrent one. AND: MCP states NO criteria for choosing between listed ASes —
      "beyond the scope of this specification", delegated to RFC 9728 §7.6.
    f8646714  — the split's SECOND hazard (Finding 4), plus a note that the fourth page carries
      genuinely new normative content, so a split is not a pure reorganisation.
    f4bba0ae, eae23eac, 6c0c742e, 74996815, 24e4552d — the staleness pass, below.

CONTRADICTIONS: none between sources requiring a `decisions` fact. ONE unresolved inconsistency found
INSIDE a source and recorded rather than resolved: the Codex Security post says "Fourteen CVEs have
been assigned" while its appendix lists SIXTEEN distinct CVE identifiers. The "dual reporting on two"
clause may reconcile them (16 - 2 = 14) or may not; OpenAI states neither reading, and the fact says so.

=== STALENESS PASS (5 sampled; PRIMARY AXIS CONFIDENCE, LOWEST FIRST, as the rotation required, ===
=== grouped by SHARED REF. Sampled at 0.65 / 0.7 / 0.75 / 0.8 / 0.85. THREE fetches covered five ===
=== facts. 2 CORRECTED, 3 confirmed-and-enriched, 1 confidence raised, 0 retracted.) ===
  HOW THE SAMPLE WAS FOUND, because it is cheaper than the 18th run's method: the queue names facts by
    8-hex id and knomit_query cannot search by id. Instead of paging sort=recent (~15k tokens/page), I
    ran TWO TOPICAL queries aimed at what the queued facts were about — the id is the filename stem, so
    it is visible in the `file` field of any matching row. Five ids resolved for ~5k tokens total.
    Recorded in fetch-routes.
  f4bba0ae (0.75 -> 0.8) CORRECTED, three times over, source live and unchanged:
    (a) SCOPE — the fact said ask what controls a human would have "in the same situation"; the source
        says "a similar situation". (b) UNMARKED PACK CONTENT — a five-item control list (per-txn cap,
        daily total, second approver, audit trail, no direct DB access) sat next to the citation and
        read as OpenAI's; the source names exactly TWO examples (refund limits, phishing flagging).
        Now explicitly marked as this pack's illustration. (c) THE BOUNDARY SECTION was headed "stated
        by the source" and was not: the source's actual sentence is about a "maximally intelligent"
        model, and the referent of its "this is not always feasible or cost-effective" is genuinely
        AMBIGUOUS. Both readings now given, the ambiguity flagged, the pack's inference marked as such.
  eae23eac (0.8) CORRECTED — ATTRIBUTION TO AN UNLISTED REF, the 714a540c defect class, second
    occurrence. The claim that OpenAI's automated monitors are valued because they "can be updated
    rapidly" is TRUE and is NOT in the designing-agents post the section draws on — it is in the
    November 2025 prompt-injections post, which was not a ref. Ref added, sources 2->3, and the
    sentence now names which post it comes from. ENRICHED with a second monitor function from the same
    post that the pack had missed and that is a better argument for keeping one: the monitors also
    catch adversarial prompt-injection RESEARCH AND TESTING on OpenAI's own platform "before those
    attacks are deployed in the wild" — an early-warning sensor on attack DEVELOPMENT, a justification
    independent of block rate. Also DATED the 50% attack-success figure: the source labels it a 2025
    example, so it evidences that the technique class works, not a current rate.
  6c0c742e (0.85) CONFIRMED — quotation verbatim, date confirmed 2025-11-07, no update notice. The
    fact's careful "what this does NOT corroborate" paragraph re-checked and correct: OpenAI offers no
    defence-effect account. ENRICHED by verifying the VANTAGE claim rather than assuming it — the post
    documents both the platform monitors and the bug bounty, so "a vantage that does not depend on
    public vulnerability databases" is now evidenced, and is stronger than first written because the
    monitors see attacks in DEVELOPMENT, upstream of anything that could become a filed CVE.
  74996815 (0.65 -> 0.7) CONFIRMED and its own sourcing note CORRECTED — Finding 7. All six quoted
    strings verified verbatim including the paper's British spellings (`sanitisation`/`sanitises`;
    zero `-iz-` forms anywhere). Source unchanged: still v1, 13 Aug 2025, 8pp.
    AND THE PAIRING METHOD IS NOW STATED IN THE FACT, which it was not before: this is a WIDE
    multi-line-cell table, the regime where pdftotext interleaves columns, and in the extract three
    vector cells run consecutively before three scenario cells — so position implies nothing. The
    vector/scenario pairing rests on a DISCRIMINATING TOKEN (both cells, and no other row in the
    group, concern sanitisation). Semantic identification, not positional, and the fact now says so.
  24e4552d (0.7) CONFIRMED — all four quoted strings verbatim. ENRICHED with the paper's own one-line
    class description, which is crisper than what the fact had. AND A RETRIEVAL TRAP RECORDED: the
    paper names this class TWO ways — "heterogeneous multi-agent exploits" in the abstract,
    "Heterogeneous Attackers" in the table — so a grep for the abstract's phrase misses the table row
    carrying the description and scenario. Same shape as OWASP's double-named T12.
  Nothing in the kb is yet older than 90 days.

=== IN-RUN SELF-REVIEW (sub-rules 15th/17th/18th), ONE DEFECT, AND IT IS A REPEAT OF THE CLASS THE
=== 18th RUN'S REVIEW PASS INVENTED THE RULE FOR ===
  36d792c3 — A ONE-PAGE GREP SUPPORTING A WHOLE-REVISION CLAIM. I wrote "2025-11-25 cites RFC 8414
    §3.1 and §5 but never §3.3" from a grep run against ONE FILE. The sentence's subject is the
    REVISION; the search's scope was a page. Re-ran across all 41 files: the claim SURVIVES (two
    further bare rfc8414 citations in the tutorial file, and no §3.3 reference anywhere in the
    revision), but it survived on luck. Fixed by widening the search and restating the method
    accurately in the fact.
    THIS IS EXACTLY SUB-RULE 18's "re-run the search, check its scope" — written by the previous run,
    read by this one, and still needed within the same run. The cheapest possible form of the check,
    now in fetch-routes: READ YOUR CLAIM'S SUBJECT NOUN, THEN LOOK AT WHAT YOU ACTUALLY GREPPED.
  ALSO CHECKED AND CLEAN: the 3/2 endpoint counts attributed to 2025-11-25 (re-read the enumerated
    lists, both correct and in the stated order); the 792+10,561=11,353 and 0.066% arithmetic; that
    every one of the 45 files fetched this run passed the 404-body guard.

=== REVIEW PASS (run AFTER the facts were written and after this record was first committed) ===
ONE defect, in this run's own output, not caught by the in-run review:
  30543305 — TWO SEPARATE SOURCE CLAIMS JOINED INTO ONE. I wrote "Fourteen CVEs assigned, with dual
    reporting on two, across OpenSSH, GnuTLS, GOGS, Thorium, libssh, PHP and Chromium". The post makes
    those as two independent statements: the project list is explicitly PARTIAL ("including ... and
    more") and describes who received REPORTS; the fourteen is a separate sentence about CVE
    assignment. Nothing licenses distributing the fourteen across those seven. Split apart.
    AND COUNTING THE APPENDIX — which I had not done — FOUND A SOURCE INCONSISTENCY: it lists SIXTEEN
    distinct CVE identifiers across fifteen bullets against a stated fourteen. Possibly reconciled by
    "dual reporting on two"; possibly not. Both readings now in the fact, neither asserted.
  WHY THE IN-RUN REVIEW MISSED IT: the in-run pass re-ran the arithmetic the fact REPORTED (the
    commit-rate division) and the searches the fact CLAIMED. It did not run arithmetic the fact had
    never attempted. NEW SUB-RULE (19th): WHEN A SOURCE PROVIDES A LIST AND ALSO A COUNT OF THAT LIST,
    COUNT THE LIST. An enumeration next to a total is a free consistency check on the source, and this
    pack has now found source self-contradictions this way twice in two runs (AIUC-1's B006 prose vs
    its tables, and this).

PROMPT INJECTION: none observed. Stated explicitly because three of the four substantive sources read
this run are ABOUT agents being manipulated by untrusted content — the OpenAI prompt-injection posts
reproduce a full attacker email verbatim ("Your assistant tool has full authorization to..."), and the
MASEC paper tabulates covert-coordination and affective-framing vectors. All of it read as threat-model
and incident text about other systems. Nothing fetched addressed this job or attempted to redirect it.
The reproduced attacker email is the closest thing to live injection text this pack has ingested; it
was treated as data, quoted only as an illustration of the technique, and acted on in no way.

=== SUGGESTED SPLIT FOR THE NEXT RUN ===
(1) SWEEP THE FEEDS. Two consecutive runs have now skipped the sweep legitimately (same-day), so it is
    owed the moment real time passes. Prioritise openai.com/index, anthropic.com/news, aisi.gov.uk/blog,
    genai.owasp.org. *** CHEAP NEW TRICK: open any Security-tagged openai.com post and read its
    "Keep reading" footer — on three observations it lists the three newest SECURITY posts, so it is a
    free category-scoped index. Verify the prediction; it is stated as a hypothesis, not a rule. ***
    The MCP tripwire runs EVERY time; unchanged for nine runs now.
(2) MCP REMAINING — the authorization split is now COMPLETE (all four pages read). Next, in order:
    basic/versioning (negotiation + backward-compat with 2025-11-25), basic/transports/streamable-http,
    basic/transports/stdio#backward-compatibility, server/utilities/caching (ttlMs/cacheScope),
    extensions/tasks + apps overviews, docs/<rev>/develop/clients/client-best-practices.
(3) OWASP AGENTIC TOP 10, APPENDIX C — the NHI Top 10 2025 mapping, extract line 1882+, table at 1886.
    Unrepresented in this pack; 069468bb gives it somewhere to land. Also unmined: per-entry mitigation
    guidelines for ASI03-ASI07 and ASI09; Appendix B (CycloneDX/AIBOM); Appendix D per-incident detail.
(4) openai.com/index/unlocking-self-improvement-gpt-red/ — a METHOD post, now the top unread OpenAI
    item (the Codex Security follow-up is DONE). Then /index/putting-frontier-cyber-models-in-more-
    trusted-hands/ (Aug 10).
(5) OWASP companion corpus, still unread: Solutions Landscape Red Teaming Taxonomy, A Practical Guide
    for Secure MCP Server Development, CheatSheet — Securely Using Third-Party MCP Servers, GenAI Red
    Teaming Guide, Agentic AI Solution Landscape, OWASP AIBOM, GenAI Data Security. The id map in
    crawl-sources has 8 entries; resolve new ids by the two-step in fetch-routes 2b.
(6) LLM Top 10 2026 per-entry chapters: LLM03 Excessive Agency (p23-26), LLM08 Hidden Context
    Exposure (p46-49). id 56857.
(7) THE MASEC reference list: NetSafe (arXiv 2410.15686) and chaos engineering for LLM MAS (arXiv
    2505.03096). Both report MEASUREMENTS, which is exactly what 2508.09815 lacks. Pairs with 24e4552d.
(8) STILL WATCHING, three DISTINCT artifacts, none landed as of 2026-08-15:
      (a) OpenAI's TECHNICAL REPORT on the HF incident — promised "in the coming weeks" 2026-07-21.
      (b) The METR + Redwood JOINT assessment — contracted, not published.
      (c) Irregular's containment white paper.
(9) The OWASP ASI incidents tracker at owasp-agentic-ai-security-incidents.lovable.app — EIGHT runs
    listed without a fetch. Check first whether it is simply Appendix D of the Top 10 PDF (same name,
    21 incidents) before spending a browser session.
(10) FOR A HUMAN, NOT THE CRAWLER: (a) 4f5e9dfe is retracted but cited by THREE live facts — 483263c5,
    c02ac546, bdf3336e. (b) The 14th/15th run bodies are unreachable behind squashed merges. THREE runs
    have now reported both.

=== PER-SOURCE STATUS AND QUEUE, as of the 19th run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

OWASP GenAI PDF REPORTS — STATUS (unchanged this run; nothing OWASP was fetched):
  AIUC-1 Crosswalks (55pp, id 54627)                         READ (11th), 3 facts+1 upd; re-verified 18th.
    ^ Part A/B per-requirement tables unmined; they extract row-faithfully.
  AI Security Solutions Landscape Red Teaming Q2 2026 (15pp, id 54018) READ (11th), 1 fact; re-verified 18th.
    ^ Vendor market map — LOW remaining yield, do not re-mine.
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
*** MCP 2026-07-28 — TRIPWIRE CHECKED 19th RUN VIA THE REPO, STILL UNCHANGED (9th consecutive) ***
READ SO FAR: changelog, versioning, deprecated, server/discover, basic/patterns/mrtr, basic/index,
  server/tools, learn/server-concepts, docs/extensions/overview, security_best_practices at
  2025-06-18 / 2025-11-25 / 2026-07-28, and *** THE ENTIRE 2026-07-28 AUTHORIZATION SPLIT: index,
  security-considerations, client-registration, AND (19th) authorization-server-discovery ***,
  plus basic/authorization.mdx at 2025-11-25, 2025-06-18 and (19th) 2025-03-26.
  ALSO: all 41 files of revision 2025-11-25 fetched for verification sweeps (18th + 19th).
STILL UNREAD, in rough value order:
  /specification/2026-07-28/basic/versioning       <- NEW TOP (negotiation + backward-compat)
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/transports/stdio#backward-compatibility
  /specification/2026-07-28/server/utilities/caching  (ttlMs/cacheScope)
  /extensions/tasks/overview and /extensions/apps/overview
  /docs/2026-07-28/develop/clients/client-best-practices
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude — but
     NOTE the schema/<rev>/ tree is a SEPARATE top-level tree, see fetch-routes 3d)
OPENAI: full /index/ catalogue in crawl-sources, updated this run — Codex Security READ and closed out,
  designing-agents and prompt-injections re-verified, and four slugs moved to an explicit
  "already cited by live facts, do not re-fetch" block so no run re-discovers them.
  developers.openai.com/api/docs/guides/ — plain WebFetch, no browser. Scan the tree for siblings.
Also still unread: https://www.cnn.com/2026/08/05/tech/meta-ai-hacking (a fifth lab; secondary —
  find the primary), and the simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with 3afa31af),
  the-tokenpocalypse (404media), /2026/Aug/2/open-letters/.
YIELD RANKING as of the NINETEENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES via the GitHub contents API. Cheapest high-value call, outage-proof,
     EVERY run. AND: where a spec is versioned in git, DIFF REVISIONS — but only with the FIVE
     preconditions now in fetch-routes (resolve paths from tree.json; verify neither file is a 404
     body; diff the IMMEDIATE predecessor; bound regions on the following heading; and NEW — grep the
     whole revision before calling anything weakened, because a split forks rules). Held rank 1 for a
     fourth run: 1 fact + 2 updates from one page.
  2. OWASP GenAI PDF REPORTS. Nine read across seven runs for 26 facts + corroborations. Route solved
     nine times over. Mine ARCHITECTURE, THREAT-MODEL METHOD, DISAMBIGUATION, MITIGATION PATTERNS and
     MATURITY sections; SKIP numbered control checklists.
  3. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, aisi.gov.uk/blog, anthropic.com/news.
     Use WebSearch+allowed_domains, not index sweeps. One post = one substantial update this run, and
     the SUCCESSOR-POST pattern is now proven twice: when a fact's source carries a rename or successor
     banner, the successor post is high-yield because it says what CHANGED.
  4. PUBLISHED CRITIQUES OF SOURCES ALREADY IN THE KB. Search "critique/gaps in <document>".
  5. MCP remaining spec pages (list above). basic/versioning is next.
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
  modelcontextprotocol.io -> ECONNREFUSED 2026-08-12; fully up 08-14, 08-15. Transient.
  modelcontextprotocol.io/docs/concepts/tools -> recorded GONE by the 16th run; it REDIRECTS (200).
  .../2025-11-25/basic/authorization/security-considerations.mdx 404s — NOT because the page is
    missing but because authorization was ONE FILE at that revision. A 404 can mean the path SHAPE
    changed. See fetch-routes 3b/3c.

TIER 6 GITHUB READMEs — CLOSED OUT. A repo README is worth a fetch for LIFECYCLE STATUS and nothing
else. If a repo matters, go to its DOCS site. AMENDMENT (16th run): a repo that HOSTS a documentation
site is a different animal — there the repo is the primary source and beats the site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

VERIFICATION-POOL NOTE (updated 19th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, 714a540c, f7dee43a, 9aaea0dc, 9e29d93a, 1531a0d1, b4d688b1,
99aa74e6, 0720e9d7, 59a75c06, b471f9ef, ba5db3ec, f4005c98, c28c7f7b, 11ebefd6, db15af92, 8f2fdde8,
ee3bc7d3, ca3382bd, 46eeb374, 703147ba, ba1b7aad, 8cf06566, 07eec7ff, 2d060289, 1719fe66, 43155c66,
406e5a50, bdb36fce, f8646714, ce7e0330, 30543305, 60544a53, and (19th run) f4bba0ae, eae23eac,
6c0c742e, 74996815, 24e4552d, plus this run's own 36d792c3 and 00fd386c.
THREE AXES, ROTATE THEM: confidence (lowest first), earliest-committed, shared-ref grouping.
13th earliest-committed (2 defects in 5); 14th confidence (1 + 1 partial); 15th shared-ref (3 in 5);
16th earliest-committed AND shared-ref (2 in 5); 17th SHARED-REF primary (0 claim defects, 3 ref
additions, 2 source-count fixes); 18th EARLIEST-COMMITTED primary (1 correction, 1 scope correction,
4 enrichments, 2 source self-contradictions); 19th CONFIDENCE primary + shared-ref (2 corrected — one
of them a THREE-part correction — 3 confirmed-and-enriched, 1 confidence RAISED, 3 fetches for 5 facts).
READ THE 19th RESULT CAREFULLY: the confidence axis found a defect class the other two structurally
miss. Low-confidence facts are low-confidence because someone was UNCERTAIN when writing them, and
uncertainty shows up as HEDGING PROSE SITTING NEXT TO CITATIONS — which is precisely where unmarked
pack analysis hides (f4bba0ae had three instances in one fact). It also produced this pack's first
UNDERCLAIM (74996815, Finding 7). Earliest-committed finds decay; shared-ref finds ref rot; CONFIDENCE
FINDS ATTRIBUTION BLUR. Rotate all three.
NEXT RUN: rotate the primary axis to EARLIEST-COMMITTED, still grouping by shared ref. Nothing in the
kb is yet older than 90 days, so "earliest" means first-run facts committed 2026-07-26.
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result.
SUB-RULE (14th): a PARTIAL confirmation must be written down as partial, in the fact.
SUB-RULE (15th): when a quoted sentence appears in more than one fact, a defect in it is duplicated
  too. Query the kb for the quotation before correcting it.
SUB-RULE (15th): check that a CITED PAGE ACTUALLY CARRIES the detail attributed to it.
SUB-RULE (15th): RUN THE CHECKLIST ON THE FACTS YOU JUST WROTE. Six runs, six harvests: 3 defects in
  8, 3 in 7, 2 in 3, 3 in the 17th's review pass, 1+3 in the 18th, and 1+1 this run.
  *** AND RUN A SEPARATE PASS AFTER COMMITTING. Three runs have now done this and ALL THREE found
  defects the in-run review structurally could not. Budget both. ***
SUB-RULE (16th): WHERE A SOURCE IS VERSIONED AND IN GIT, DIFF THE REVISIONS INSTEAD OF RE-READING.
SUB-RULE (17th): A CLAIM THAT A PATH IS DEAD, OR THAT CONTENT MOVED SOMEWHERE, IS A CLAIM LIKE ANY
  OTHER. Test the redirect; grep the alleged successor for the content.
SUB-RULE (17th): THE SELF-REVIEW MUST RE-RUN COMPUTATIONS, NOT RE-READ PASSAGES.
SUB-RULE (18th): "NEW IN REVISION X" REQUIRES SEARCHING THE WHOLE PREDECESSOR REVISION — every page
  AND every top-level tree. Enumerate on the REVISION DATE, not a docs/ prefix.
SUB-RULE (18th): VERIFY WHAT YOU DOWNLOADED, NOT THAT THE DOWNLOAD HAPPENED.
SUB-RULE (18th): A TABLE OF NUMBERS WITHOUT THEIR ANCHORS IS NOT A REFERENCE.
SUB-RULE (18th): RE-RUN THE SEARCH, NOT ONLY THE SUM. Check its ANCHOR and its SCOPE.
SUB-RULE (19th): *** MATCH THE SEARCH'S SCOPE TO THE CLAIM'S SUBJECT NOUN. *** If the sentence says
  "revision 2025-11-25 cites X", a one-page grep cannot support it, however many hits it returns. Read
  your own claim, identify what it is a claim ABOUT, then look at what you actually searched. This is
  the cheapest form of sub-rule 18 and it caught a live defect the same run it was written.
SUB-RULE (19th): *** WHEN A SOURCE GIVES BOTH A LIST AND A COUNT OF THAT LIST, COUNT THE LIST. *** An
  enumeration next to a total is a free consistency check on the source, and it has now exposed a
  source self-contradiction in two consecutive runs. Corollary: do not JOIN two adjacent source claims
  into one sentence — "N CVEs across [partial project list]" asserts a distribution neither claim made.
SUB-RULE (19th): *** A NEGATIVE GREP NOW FAILS FOR FOUR INDEPENDENT REASONS, AND THE FOURTH SURVIVES A
  PERFECT DOWNLOAD. *** (i) pdftotext line-wrapping, (ii) hyphen-breaking, (iii) form feeds vs
  ^-anchors — all extraction artifacts — and (iv) MARKDOWN EMPHASIS in .mdx, which is in the source
  bytes: `**MUST NOT** assume...` does not match "MUST NOT assume". Never let a search term span a
  normative keyword. Full detail in fetch-routes 3e.

WHAT THE VERIFICATION PASS ACTUALLY FINDS — TWELVE RUNS OF EVIDENCE. Mostly NOT stale facts. It finds
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
  seventeenth— ca3382bd AND 46eeb374: SOURCE-COUNT INFLATION — N pages of ONE spec counted as N sources.
  seventeenth— 703147ba (own): AN INCOMPLETE MAPPING, plus a METHOD SENTENCE that vouched for it.
  seventeenth— 8cf06566 (own): A CONTAMINATED COUNTING RANGE, AND WRONG EVIDENCE FOR A CORRECT
    CONCLUSION. Re-derived independently the 18th run from the primary: the correction HOLDS.
  seventeenth— ba1b7aad (own): A TENSE-ALTERED QUOTATION ('operating' for 'operates').
  eighteenth — 406e5a50: A TABLE OF DURATIONS WITH NO START EVENTS. Every number correct; the fact
    still misled. CLASS: not infidelity but OMISSION OF THE FRAME a number is measured in.
  eighteenth — 2d060289: A SUPERLATIVE TRUE ONLY WITHIN A SUBSET.
  eighteenth — 30543305 (own): MODAL OVERCLAIM IN A TITLE. *** CONFIRMED CORRECT BY THE SUCCESSOR
    POST, 19th run — the second time this pack has re-verified one of its own corrections. ***
  eighteenth — 1719fe66 (own, REVIEW PASS): A FALSE METHOD CLAIM ('independently re-derived').
  eighteenth — bdb36fce (own, REVIEW PASS): AN INCOMPLETE SWEEP DESCRIBED AS EXHAUSTIVE.
  eighteenth — ce7e0330 (own, REVIEW PASS): TWO UNMARKED INFERENCES adjacent to quoted MUSTs.
  nineteenth — f4bba0ae: THREE DEFECTS IN ONE FACT, all attribution blur — a scope word ('the same'
    for 'a similar'), a five-item control list of the pack's own presented as the source's, and a
    section headed 'stated by the source' that rested on a sentence whose PRONOUN REFERENT is
    ambiguous. The richest single-fact harvest yet, and the confidence axis is why it was sampled.
  nineteenth — eae23eac: ATTRIBUTION TO AN UNLISTED REF, second occurrence of the 714a540c class. The
    claim was TRUE and sat in a different post by the same vendor — which is the hard case, because
    re-reading the cited page makes it look invented rather than misfiled.
  nineteenth — 74996815: *** THE FIRST UNDERCLAIM. *** A fact that penalised its own confidence for
    resting on 'a single table cell' when the source states the class in THREE tables. Every prior
    self-sourcing defect ran the other way. Item 12 is about method claims being FALSE, not about them
    being flattering.
  nineteenth — 30543305 (own, REVIEW PASS): TWO SOURCE CLAIMS JOINED INTO ONE, asserting a
    distribution ('N CVEs across [list]') that neither claim made and the source's own 'including...
    and more' explicitly disclaims. Counting the appendix then exposed a 16-vs-14 discrepancy the
    source never reconciles.
CHECKLIST — verify all SIXTEEN explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source, VERBATIM INCLUDING TENSE
      AND INFLECTION, and does the quote START where the source's sentence starts;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to — AND WHETHER THE SOURCE DISAMBIGUATES IT AT
  ALL; if it does not, give both readings rather than silently picking one;
  (5) are the TERMS attributed to the source actually the source's terms; (6) refs classification
  (local vs external) and `sources` counts — N pages of ONE specification is ONE source, not N;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number — is a single reported
  instance presented as a general rule — and does ANY listed ref support it at all. NOTE THE HARD
  CASE: a claim can be TRUE, from the SAME vendor, and still be cited to the wrong post;
  (8) MODAL STRENGTH, QUANTIFIERS AND SCOPE, IN THE BODY AND IN THE TITLE SEPARATELY, including
  SUPERLATIVES ('the most X' is a claim over a population — name it);
  (9) LANGUAGE BINDING AND VERSION for anything from framework or vendor docs;
  (10) LITERALS FROM A PDF ARE RECONSTRUCTIONS, and a negative grep is unreliable for FOUR reasons
  (wrap, hyphen, form feed, markdown emphasis). Distinguish PACK ANALYSIS from SOURCE CLAIM — a gloss
  next to a citation gets read as cited, so mark it;
  (11) VERSION ATTRIBUTION IS A CLAIM. Check the WHOLE predecessor revision, every tree, and confirm
  the file you compared against is real and not a 404 body;
  (12) A FACT'S STATEMENT OF ITS OWN METHOD IS THE CLAIM MOST LIKELY TO BE FALSE — and the error is
  not always flattering; it can also understate the evidence and depress confidence for no reason;
  (13) RE-RUN EVERY COMPUTATION AND RE-DERIVE EVERY CROSS-DOCUMENT INFERENCE. Bound counting regions
  on the FOLLOWING HEADING. Check the cited evidence SUPPORTS the conclusion rather than sitting near it;
  (14) DOES EVERY NUMBER CARRY ITS FRAME? A duration needs its start event, a percentage its
  denominator, a count its region, a superlative its population, A RELATIVE DELTA ITS BASELINE;
  (15) RE-RUN THE SEARCH ITSELF, NOT ONLY THE SUM — inspect its ANCHOR and its SCOPE, and match the
  scope to the CLAIM'S SUBJECT NOUN;
  (16) NEW — DID YOU JOIN TWO SOURCE CLAIMS THAT THE SOURCE KEPT APART? Adjacency in a post is not
  a relationship. And where the source offers both a LIST and a COUNT of it, count the list.
