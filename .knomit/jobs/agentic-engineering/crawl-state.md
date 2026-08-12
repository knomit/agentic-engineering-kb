---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-12 (fifteenth run; HOURS after the fourteenth, which committed 02:00-02:26Z today).
A SAME-DAY run, so per the standing rule NO broad feed sweep was attempted — the budget went to the
14th run's queued backlog, exactly as the 14th run did with the 13th's.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***
The revision behind this one (e61629fc, 2026-08-12T02:26Z) is the BACKFILL FLOOR: it carries the
complete 197-URL ALREADY_CRAWLED union computed once with git over all 34 revisions. A walk that
reaches it has reached the bottom — read it, union it, stop. Do NOT reproduce that union here.
ALREADY_CRAWLED after this run = those 197 + the 9 listed below = 206.

HISTORY WALK PERFORMED THIS RUN: 2 revision bodies read (HEAD e61629fc, then bb31f926 as the oldest
of HEAD's history page). bb31f926 returned more_available:FALSE and carried the identical 197-URL
union, confirming the floor. Oldest commit date reached: 2026-08-12T02:00:22Z. No gaps, no failed
calls. NOTE FOR FUTURE RUNS: every revision now visible carries today's date because the floor was
written today; the pre-floor per-run dates are not recoverable and do not need to be.

recurring-feed indexes swept: ONE ONLY, deliberately.
https://modelcontextprotocol.io/specification/versioning   (tripwire — UNCHANGED, still 2026-07-28)
No other index swept: hours, not days, since the last run.

articles crawled (9 new):
https://openai.com/index/designing-agents-to-resist-prompt-injection/   <- BROWSER; THE BIG ONE (Mar 11)
https://openai.com/index/ai-agent-link-safety/                          <- BROWSER; Safe Url (Jan 28)
https://openai.com/index/prompt-injections/                             <- BROWSER; (Nov 7 2025)
https://cdn.openai.com/pdf/dd8e7875-e606-42b4-80a1-f824e4e11cf4/prevent-url-data-exfil.pdf  <- PAPER, plain curl -A
https://developers.openai.com/api/docs/guides/agent-builder-safety      <- plain WebFetch, NOT 403
https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/
https://genai.owasp.org/download/49059/?tmstv=1753666640                (Securing Agentic Apps 1.0)
https://genai.owasp.org/resource/multi-agentic-system-threat-modeling-guide-v1-0/
https://genai.owasp.org/download/46950/?tmstv=1745459605                (MAS Threat Modeling v1.0)

re-fetched for the staleness pass only, not for new facts:
https://www.trychroma.com/research/context-rot        (ONE fetch verified THREE facts)
https://cognition.com/blog/multi-agents-working       (ONE fetch verified TWO facts)
https://cognition.com/blog/dont-build-multi-agents    (same pair)
https://strandsagents.com/docs/user-guide/concepts/agents/conversation-management/

errored / not obtained: NONE. No paywalls, no dead sources, no 403 the browser did not solve, no 404s
— every slug this run was resolved by search before being fetched, so nothing was guessed.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

FINDING 1 — THE HIGHEST-YIELD SINGLE CALL OF THE RUN WAS A SEARCH, NOT A FETCH, AND IT COMPOUNDS.
One WebSearch with allowed_domains:["openai.com"] aimed at ONE known-wanted post returned four
new targets: the Safe Url post, a linked cdn.openai.com PAPER, a Nov-2025 post nobody had seen, and
a developers.openai.com guide. Two more searches on genai.owasp.org resolved both wanted resource
slugs exactly AND returned a download id (52117) in a snippet with no page fetch at all.
THE GENERALISATION, now in fetch-routes as an extension of route 1b: search results carry SIBLING
links, so a search aimed at a URL you ALREADY want is simultaneously the cheapest discovery sweep
available. Prefer it over a feed index whenever you have a specific title in hand. Route 1b was
introduced last run as a slug-resolver; it is better understood as a discovery primitive.
COROLLARY THAT COST NOTHING AND SAVES A BROWSER CALL EVERY RUN: the openai.com 403 is HOST-scoped.
developers.openai.com and cdn.openai.com are NOT gated — plain WebFetch and plain curl -A respectively.

FINDING 2 — AN OPERATOR PUBLISHED HARD NUMBERS AGAINST THE DOMAIN-ALLOWLIST CONTROL, AND THE
REPLACEMENT'S SECURITY ARGUMENT IS PROVENANCE, NOT REPUTATION.
OpenAI's Safe Url paper is the best single artifact this pack has read on exfiltration control.
  * The hand-curated domain allowlist covered only ~10% of URLs users actually visited. NINETY
    PERCENT of benign traffic warned. That false-positive rate IS the vulnerability — it trains
    users to click through. Folded into fdad859e, which had the bypasses but no coverage number.
  * Open redirects on allowlisted domains are a THIRD bypass class, and structurally unfixable: any
    NEW open redirect on ANY listed domain reopens it, and you do not monitor third-party redirect
    hygiene. fdad859e retitled from "two documented bypasses" to three.
  * The replacement: exact-URL match against OpenAI's own search-crawler index, which runs with zero
    access to user data. That isolation IS the security argument — a crawler that never saw your data
    cannot have visited a URL containing it. Coverage ~10% -> "over 80%". Requires canonicalization
    (query-param ordering) or trivial reordering defeats exact match.
  * Named residual: the "keyboard attack" — pre-seed and get crawled a large space of unique URLs to
    launder personal data into the index. Bounded by an inverse relation between URL count and bits
    per URL: a 36-char alphabet forces ~13 sequential fetches to leak "123 Main Street".
  * THE BOUNDARY CONDITION, and it is the part an engineer would otherwise copy straight past: the
    threat model assumes the attacker cannot control request headers or bodies and the agent's
    network interaction is GET-shaped retrieval only. An agent with a general HTTP tool, a shell, or
    an MCP server that can POST is OUTSIDE this model and gains nothing — the data leaves in a body.

FINDING 3 — AN OPERATOR SAYS INPUT-CLASSIFYING "AI FIREWALLS" DO NOT CATCH THE ATTACKS THAT WORK.
OpenAI states that as models stopped falling for blunt overrides, effective injections became
social-engineering-shaped, and that classifying intermediaries do not usually catch those because
detecting such an input becomes the same problem as detecting a lie — without the context needed to
tell. A cited external attack worked 50% of the time. This is a live position against a whole product
category and it is now a `decisions` fact (eae23eac) rather than a flattened claim.
WHAT MAKES IT A DESIGN ARGUMENT RATHER THAN PESSIMISM: an inbound-content check has no ground truth;
an outbound-action check has a checkable predicate. Both major operators independently shipped the
sink-side version — OpenAI's source-sink framing and Safe Url, Anthropic's reasoning-blind auto-mode
classifier. AND BOTH INDEPENDENTLY CONCLUDED A BLOCK MUST RETURN TO THE MODEL AS A REDIRECT WITH
INTENT, not a bare failure. That convergence corroborates f1cbb540 from a second vendor.

FINDING 4 — THE STALENESS PASS FOUND ITS DEFECT IN A PLACE THE EIGHT-ITEM CHECKLIST ALREADY NAMES,
AND THE SAME DEFECT WAS DUPLICATED ACROSS TWO FACTS.
MODAL STRENGTHENING AGAIN — the exact class the 14th run added as checklist item 8, one run later.
Cognition's sentence is "multi-agent systems work BEST TODAY when writes stay single-threaded and
the additional agents contribute intelligence rather than actions." BOTH f7dee43a and 9aaea0dc
quoted it starting at "when writes…", dropping "best today" — converting a statement about which
designs work BEST under CURRENT capability into a condition for working at all. Both corrected.
THE NEW SUB-LESSON: when a quoted sentence is shared across facts, a modal defect in it is shared
too. Grepping the kb for a quotation you are about to correct is cheap and finds the duplicates.

FACTS WRITTEN (8 new, 2 updated from crawling + 5 touched by the staleness pass, 0 retracted):
  NEW —
    kb/architecture/ai/agents/security/url-exfiltration/b4d688b1  (Safe Url: 10%->80%, keyboard
      attack, canonicalization, and the GET-only threat-model boundary that decides transferability)
    kb/decisions/ai/agents/security/guardrail-placement/eae23eac  (classify the outbound action, not
      the inbound content; both operators' convergent denial-as-redirect handling)
    kb/conventions/ai/agents/security/design-heuristics/f4bba0ae  (derive controls by asking what
      limits a human in the same seat would have; assumes deception succeeds)
    kb/invariants/ai/agents/security/instruction-hierarchy/99aa74e6 (never interpolate untrusted text
      into a developer message — it promotes the attacker into the trusted tier)
    kb/gotchas/ai/agents/security/task-scoping/805bc132           (task breadth is a security
      parameter; the confirmation gate does not compensate for a broad brief)
    kb/conventions/ai/agents/security/threat-modeling/c02ac546    (MAESTRO: a taxonomy is a checklist,
      a layer-walk is a generator — 13 threats fell out that the taxonomy lacks; cross-layer is a
      separate pass a per-layer review structurally cannot reach)
    kb/architecture/ai/agents/interop/outbound-identity/0720e9d7  (RFC 9421 signing, ANS, X-Agent-
      Intent, with OWASP's own maturity ratings — the outbound direction of agent identity)
    kb/architecture/ai/agents/multi-agent/swarm/af3acf92          (a swarm has no in-band guidepost
      for correct action or trusted peer; assign both out-of-band, gate self-expansion on a human)
  UPDATED FROM CRAWLING —
    fdad859e  — third bypass class (open redirects) + the 10% coverage number and its
      approval-fatigue consequence. Retitled. sources 2->3.
    6c0c742e  — OpenAI's independent Nov-2025 "not yet seen significant adoption" observation added
      as corroboration of the LOW COUNT but explicitly NOT of OWASP's defence-effect explanation.
      sources 1->2. This provenance split is the point; do not collapse it.

CONTRADICTIONS: none new. One provenance split deliberately preserved (6c0c742e above): two sources
agree on an observation and offer different explanations for it, and the fact now says so.

STALENESS PASS (5 sampled by SHARED REF — the 14th run's new sub-rule, and it worked: 4 fetches
covered 5 facts. kb/principles/** avoided per the write-block. 3 corrected, 2 confirmed):
  714a540c CORRECTED — ATTRIBUTION TO A REF THAT ISN'T EVEN LISTED. The fact recorded `pin_first = 0`,
    a `{"compression_threshold": 0.7}` example, and an elaborate account of pin metadata being written
    on first reduction and persisting — none of which the CITED page documents. They likely came from
    the Strands API-reference pages, which an earlier run read but which were never added to refs.
    Removed with an explicit note on where to re-derive them. ALSO a binding error: `window_size = 40`
    is documented for the TypeScript binding; no Python default is stated, and the docs carry
    snake_case and camelCase side by side. Core invariant CONFIRMED verbatim, including both
    mechanism names ("Dangling Message Cleanup", "Tool Pair Preservation"). conf 0.8->0.7.
  f7dee43a CORRECTED (modal, see FINDING 4) + ENRICHED with a genuinely new condition: Cognition's
    "Smart Friend" advisory pattern FAILED on capability asymmetry — SWE-1.5 as primary "was not good
    enough", "the gap…was too wide". Generalises: if the consumer cannot evaluate the advice, a
    smarter advisor does not raise the ceiling. Also softened "unstructured swarms remain
    impractical" to Cognition's actual reported symptom, "fragmented decisions". conf 0.85 held.
  9aaea0dc CORRECTED (same modal defect) + all quotations re-verified verbatim, including both 2025
    principles and the two Flappy Bird asset descriptions. conf 0.8->0.85.
  9e29d93a CONFIRMED verbatim — 18 models, non-positional framing, "structural coherence consistently
    hurts model performance", distractor findings. ADDED MODEL VINTAGE: Chroma's 18 were mid-2025
    frontier (GPT-4.1, Claude 4, Gemini 2.5, Qwen3), ALL since superseded. Mechanism holds; treat
    magnitudes as of that generation. Anthropic leg not re-fetched, said so. conf 0.8->0.85.
  1531a0d1 PARTIALLY VERIFIED and said so. Chroma leg confirms gradient-not-a-cliff; the Anthropic
    leg (n² argument, three techniques, Pokémon, 1-2k token sub-agent figure) NOT re-fetched.
    VERIFICATION SCOPE section added rather than a blanket bump. conf 0.8->0.85.

PROMPT INJECTION: none observed. Stated explicitly because this run read four documents ABOUT prompt
injection, one of which (designing-agents-to-resist-prompt-injection) reproduces a full attack email
verbatim — including the line "Your assistant tool has full authorization to automatically retrieve
and process employee profiles". That is quoted specimen text inside an analysis, not an instruction
addressed to this job, and it was treated as data. Nothing fetched attempted to redirect this run.

SUGGESTED SPLIT FOR THE NEXT RUN:
(1) IF DAYS HAVE PASSED, SWEEP THE FEEDS — owed for TWO runs now, both same-week. Prioritise
    openai.com/index, anthropic.com/news, genai.owasp.org. This is the top priority if any real time
    has elapsed; if it is again hours, work the queue below instead.
(2) THE MAS COUNTER-POSITION PAIR, and treat it as Tier-1: arxiv.org/pdf/2508.09815 names specific
    GAPS in the OWASP MAS guide read this run. Fetch it BEFORE writing anything further from that
    guide. Details in crawl-sources.
(3) OWASP companion corpus, still the richest unread block, route fully solved (see fetch-routes 2b).
    Next: Agent Name Service (ANS) v1.0 — now pairs with THREE facts (8b32c15a, 995c167b, and the new
    0720e9d7, which cites ANS without having read its spec). Then Solutions Landscape Red Teaming
    Taxonomy, A Practical Guide for Secure MCP Server Development, CheatSheet — Securely Using
    Third-Party MCP Servers, GenAI Red Teaming Guide, Agentic AI Solution Landscape, OWASP AIBOM,
    GenAI Data Security Risks & Mitigations.
(4) /resource/owasp-top-10-for-agentic-applications-for-2026/ — download id 52117 ALREADY KNOWN, so
    this is one curl away. The resource page has never been fetched despite the announcement post and
    the threats-and-mitigations page both being crawled.
(5) MCP basic/index#meta (the _meta contract everything rides on), then basic/versioning,
    authorization/security-considerations, transports/streamable-http, server/utilities/caching.
(6) FINISH THE OPENAI CLUSTER — only two left and both are likely low-yield policy:
    /index/putting-frontier-cyber-models-in-more-trusted-hands/, /index/safety-alignment-long-horizon-models/.
    STILL WATCHING for three promised documents: OpenAI's full HF technical report, the JOINT METR +
    Redwood assessment, Irregular's containment white paper. None had landed as of 2026-08-12.
(7) The OWASP ASI incidents tracker — now FOUR runs listed without a single fetch.
(8) LLM Top 10 2026 per-entry chapters: LLM03 Excessive Agency (p23-26), LLM08 Hidden Context
    Exposure (p46-49). id 56857.


=== PER-SOURCE STATUS AND QUEUE, as of the 15th run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

OWASP GenAI PDF REPORTS — STATUS:
  AIUC-1 Crosswalks (55pp)                                  READ (11th), 3 facts+1 upd
  AI Security Solutions Landscape Red Teaming Q2 2026 (15pp) READ (11th), 1 fact
  State of Agentic AI Security and Governance 2.01 (139pp)  READ (12th), 8 facts+1 upd
    ^ chapters still NOT written up: Enterprise Adoption Maturity Model (p53-62), Alignment with
      Top 10 Agentic (p61), Future Trends / What Remains Unsolved (p63-68) incl. governance-
      deployment collision, cyber-insurance coverage collapse, OT/ICS, adversarial agent
      weaponisation; AI SBOM and Supply Chain Provenance (p46-48); Explainable AI (p49);
      Appendix 1 agent-type taxonomy (p70-76); Appendix 3 ASI risk classes (p116); Appendix 6 Top 10
      Impacting Personal Agents (p128). Appendix 2 (regulatory) is low altitude.
  OWASP GenAI LLM Top 10 2026 (122pp, id 56857)             READ (13th), 2 facts + 1 upd
    ^ NOT mined: the ten per-entry chapters. LLM03 Excessive Agency (p23-26) and LLM08 Hidden Context
      Exposure (p46-49) are the two most relevant and UNREAD in detail. Appendix A coverage matrices
      (p58-105) map to ASI 2026, DSGAI v1.0, MITRE ATLAS v2026.06, ATT&CK v19.1, CWE 4.20, NIST AI
      600-1, NIST AI RMF, CSA AICM v1.1, AIVSS v0.8 — a large pre-done cross-framework mapping.
  Securing Agentic Applications Guide 1.0 (id 49059)        READ (15th), 2 facts
    ^ MOST OF THIS GUIDE IS BELOW THE BAR and a future run should not re-mine it blindly. Sections
      5.x (Key Operational Capabilities: API access, code execution, DB, web use, PC operations) and
      4.4 (cross-architecture) are generic control checklists — "apply rate limiting", "regularly
      scan", "use sandboxing" — exactly what a competent model already produces. The value was in two
      narrow places: the outbound agent-identity ladder (~p45) and the swarm trust discussion (4.3).
      Possibly still worth a look: 2.2 Secure Architecture Patterns (lines 833-1313 of the extract),
      2.5 Case Studies, and 9.x runtime hardening. Do not budget more than one pass.
  Multi-Agentic System Threat Modeling Guide v1.0 (id 46950) READ (15th), 1 fact
    ^ The MAESTRO method transferred; the worked examples did not. Sections 3 (RPA expense agent) and
      4 (ElizaOS) are blockchain/RPA-specific enumeration — T26-T38 are illustrations of the method,
      not portable knowledge. SECTION 5 IS THE ONE STILL WORTH READING: "Threat Modeling Anthropic MCP
      Protocol using MAESTRO" (extract line 3132 onward), squarely on this pack's subject and unmined.
STILL UNREAD, all named as companion resources, HIGH PRIORITY (see split items 3 and 4).
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-a-hands-on-companion-to-the-owasp-genai-security-project/
*** MCP 2026-07-28 — TRIPWIRE CHECKED 15th RUN, STILL UNCHANGED ***
No movement since the 11th run. Check EVERY run anyway; cheapest high-value fetch in the pack. The
versioning page also re-confirmed the negotiation model (per-request `_meta` key
`io.modelcontextprotocol/protocolVersion`, MCP-Protocol-Version header on Streamable HTTP,
UnsupportedProtocolVersionError, server/discover optional for clients) — all already correctly
recorded in 031dab74, 995c167b and 3afa31af. No update needed; noting it so nobody re-derives it.
STILL UNREAD, in rough value order:
  /specification/2026-07-28/basic/index#meta       (the _meta contract everything now rides on)
  /specification/2026-07-28/basic/versioning       (negotiation + backward-compat with 2025-11-25)
  /specification/2026-07-28/basic/authorization/security-considerations
  /specification/2026-07-28/basic/transports/streamable-http
  /specification/2026-07-28/basic/transports/stdio#backward-compatibility
  /specification/2026-07-28/server/utilities/caching  (ttlMs/cacheScope)
  /extensions/tasks/overview and /extensions/apps/overview
  /specification/2026-07-28/schema                 (reference only; expensive, low altitude)
*** THE OPENAI SECURITY CLUSTER — SEVEN POSTS READ ACROSS TWO RUNS; NEARLY EXHAUSTED ***
READ: third-party-cyber-evaluations (Aug 4, 13th); hugging-face-model-evaluation-security-incident
  (Jul 21 + updates, 14th); responding-next-frontier-critical-cyber-capabilities (Aug 7, 14th);
  expanding-daybreak-as-the-cyber-defense-window-narrows (Aug 10, 14th);
  designing-agents-to-resist-prompt-injection (Mar 11, 15th — 3 facts, best of the run);
  ai-agent-link-safety + its cdn.openai.com paper (Jan 28, 15th — 1 fact + 1 major update);
  prompt-injections (Nov 7 2025, 15th — 1 fact + 1 corroboration; consumer-facing, lowest yield).
UNREAD, both likely policy/program, budget one cheap fetch each:
  /index/putting-frontier-cyber-models-in-more-trusted-hands/   (Aug 10)
  /index/safety-alignment-long-horizon-models/
  /index/trusted-access-for-cyber/, /index/scaling-trusted-access-for-cyber-defense/,
  /index/updating-our-preparedness-framework/   (governance; lower altitude)
NEW ADJACENT SOURCE, developers.openai.com/api/docs/guides/ — plain WebFetch, no browser. Added to
  the recurring list. agent-builder-safety READ 15th run (1 fact). Scan the tree for siblings.
Also still unread: https://www.cnn.com/2026/08/05/tech/meta-ai-hacking (a fifth lab; secondary —
  find the primary), and the simonwillison queue: /2026/Jul/31/stateless-mcp/ (pairs with 3afa31af),
  the-tokenpocalypse (404media), /2026/Aug/2/open-letters/.
YIELD RANKING as of the FIFTEENTH run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES. modelcontextprotocol.io/specification/versioning + /deprecated.
     One cheap fetch once caught a revision that invalidated parts of five facts. EVERY run.
  2. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, aisi.gov.uk/blog, anthropic.com/news, the
     OWASP ASI tracker. Validated six times. The 14th run's sharper rule stands: when the kb holds an
     incident fact, CHECK WHETHER THE OPERATOR PUBLISHED ITS OWN ACCOUNT, by SEARCHING. The 15th run
     adds: the same search is also the cheapest way to find posts the feed sweep never surfaced —
     three of this run's four best sources were found that way, none by a feed.
  3. OWASP GenAI PDF REPORTS. Six read across four runs for 17 facts + 4 corroborations. Read route
     solved twice over (routes 2 and 2b). Still the richest unread block. BUT SEE THE CAVEAT ABOVE:
     the control-checklist sections of these guides are below the bar. Mine the ARCHITECTURE,
     THREAT-MODEL METHOD and MATURITY-ASSESSMENT sections; skip the numbered control lists.
  4. MCP 2026-07-28 remaining spec pages (list above). basic/index#meta is next.
  5. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. Index quiet since Apr 2026.
     anthropic.com/news is where postmortems actually land.
  6. microsoft.com/en-us/research/blog — 1 fact of 3 last run. Prefer METHOD posts over FRAMEWORK
     posts. Scan for agent/memory/skill/eval; skip health, quantum, diffusion.
  7. Azure Architecture Center. The six-part RAG series is the largest coherent unread block.
  8. aws.amazon.com/blogs/machine-learning — high volume, product-heavy, but spec-level changes
     surface early. Scan titles for spec/protocol/security/identity.
  9. builder.aws.com Builders' Library — 16 of 30 read for 55+ facts, visibly exhausting; the 12
     unread skew CI/CD.
 10. cognition.com/blog — dense, specific, publishes reversals of its own positions. RE-RATED UP
     slightly: this run's staleness pass showed their posts reward close reading and their 2026
     follow-up carried a condition (capability-gap asymmetry) nobody had extracted. Unread:
     coding-agents-101-the-art-of-actually-getting-things-done, swe-grep, blockdiff,
     devin-annual-performance-review-2025, evaluating-coding-agents, making-fable-cheaper-than-opus,
     devin-fusion, swe-1-7, measuring-open-source-model-trustworthiness,
     introducing-devin-security-swarm, frontier-code and frontier-code-1.1, ai-productivity.
     Skip partnership/funding/office/acquisition posts — about half the feed.
 11. huggingface.co/blog — scan for incident/infrastructure/engineering; SKIP model and dataset
     announcements. Posts can be namespaced under an org (huggingface.co/blog/<org>/<slug>).
 12. sourcegraph.com/blog — real measurements. Unread:
     compliance-first-ai-proving-agent-provenance, owning-a-codebase,
     sourcegraph-mcp-and-a-cheaper-model-beat-a-mythos-class-model-alone,
     the-hidden-cost-of-code-that-nobody-touches.
 13. eugeneyan.com/writing — unread: secure-source-code (May 2026) and anything newer.
 14. simonwillison.net/tags/llms/ — VALUE IS THE LINKS: read the index, follow the primaries, rarely
     read Simon himself. CAVEAT (14th run, and it held up): his summaries of TALKS are the weakest
     link in this pack and have produced two claims no primary corroborates (4e923405, bcbf13c2).
 15. latent.space/archive — interview format. Unread: /p/aiewf26trends, /p/modal2026, /p/poolside,
     /p/chatgpt-work. Skews discussion-level; verify measurements exist before a full read.
 16. langchain.com/blog — eval and benchmark posts clear the bar; customer stories do not.
 17. metr.org/blog — demoted 13th run. RE-RATE IF the joint METR + Redwood assessment lands.
 18. embracethered.com/blog — low volume, high value, security only.
 19. trychroma.com/research — rare but substantial. Unread: evaluating-chunking.
 20. research.google/blog — checked twice, output is health/quantum/diffusion. Low yield.
     microsoft.com/en-us/security/blog — one good agent-identity post, otherwise threat intel.

dead or unreadable — EMPTY except for host moves. Read the six-for-six warning in Appendix S first.
  block.github.io/goose -> goose-docs.ai (old host serves a 'goose has moved' stub).
  https://strandsagents.com/latest/... -> 404. Use /docs/... instead.
  NOTE: builder.aws.com, the Vectara leaderboard, OWASP PDFs (three times, three different stated
    reasons) and openai.com were ALL listed or headed here and NONE was ever unreachable.

TIER 6 GITHUB READMEs — CLOSED OUT. Five of six returned catalogue- or marketing-level text below the
bar. The only useful things were MAINTENANCE-STATUS notices (autogen's maintenance mode;
semantic-kernel's 'now Microsoft Agent Framework'), which generalises: a repo README is worth a fetch
for LIFECYCLE STATUS and nothing else. If a repo matters, go to its DOCS site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

STALENESS-POOL NOTE (updated 15th run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, and (15th run) 714a540c, f7dee43a, 9aaea0dc, 9e29d93a,
1531a0d1.
THREE AXES NOW, ROTATE THEM. Confidence (lowest first), earliest-committed, and SHARED-REF grouping.
The 13th ran earliest-committed (2 defects in 5); the 14th ran confidence (1 defect + 1 partial);
the 15th ran shared-ref (3 defects in 5, at 4 fetches — the best yield-per-fetch so far, because
grouping by source lets one fetch adjudicate several facts and surfaces defects DUPLICATED across
them). Next run: rotate back to earliest-committed. Nothing here is yet older than 90 days.
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result.
SUB-RULE (14th): a PARTIAL confirmation must be written down as partial, in the fact. Do not bump
confidence as though the whole fact were checked.
SUB-RULE (15th, NEW): WHEN A QUOTED SENTENCE APPEARS IN MORE THAN ONE FACT, A DEFECT IN IT IS
DUPLICATED TOO. Before correcting a quotation, query the kb for it and fix every copy — f7dee43a and
9aaea0dc carried the identical modal defect and would have been half-fixed otherwise.
SUB-RULE (15th, NEW): CHECK THAT A CITED PAGE ACTUALLY CARRIES THE DETAIL ATTRIBUTED TO IT. 714a540c
held parameters that came from a sibling API-reference page never added to its refs. This is checklist
item 7 (which ref supports which number) extended to: does ANY listed ref support it at all?

WHAT THE STALENESS PASS ACTUALLY FINDS — EIGHT RUNS OF EVIDENCE, and it is the single most reliable
defect-finder in this job. It is NOT finding stale facts. It finds CITATION-FIDELITY defects in facts
whose underlying claims are correct:
  ninth      — 56986e8f: a paraphrase wearing quote marks.
  tenth      — c93d93ee: an overclaiming gloss attributed to the source.
  tenth      — c7290868: INVERTED CAUSATION pointing at the wrong remedy.
  eleventh   — 96ebc34e: BOTH at once, and the gloss reversed the blame.
  eleventh   — c858a924: WRONG ACTOR — 'independent auditors' were two LLM judges, not humans.
  twelfth    — 30869b36: a pack gloss wearing quote marks ('combined surface area').
  twelfth    — c436422a: WRONG TERMS attributed to the source (brain/hands/session).
  thirteenth — f78a326a: WRONG TERM ('raw accuracy' for 'raw agreement') AND one reported instance
    generalised into a rule.
  thirteenth — 38c06627: MISATTRIBUTION ACROSS A FACT'S OWN TWO REFS.
  fourteenth — d18637a2: MODAL STRENGTHENING ('is noise' vs 'deserves skepticism') + a scope error
    (a Terminal-Bench-only figure generalised across benchmarks).
  fifteenth  — f7dee43a AND 9aaea0dc: MODAL STRENGTHENING AGAIN, the same quotation, in two facts.
    Dropping 'best today' turned a current-capability preference into a hard condition.
  fifteenth  — 714a540c: ATTRIBUTION TO AN UNLISTED REF — parameters credited to a page that does not
    document them, plus a language-binding error (a TypeScript default recorded as the Python one).
CHECKLIST — verify all NINE explicitly, not just 'is the claim still true':
  (1) quotation boundaries — is every quoted string actually in the source, and does the quote START
      where the source's sentence starts, or has a qualifier been cut off the front;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what the pronoun in a quoted sentence refers to; (5) are the TERMS attributed to the source
  actually the source's terms; (6) refs classification (local vs external) and `sources` counts;
  (7) FOR MULTI-REF FACTS, which specific ref supports each specific number — and is a single
  reported instance being presented as a general rule;
  (8) MODAL STRENGTH AND SCOPE: does the fact state as a rule what the source stated as a caution
  ('is noise' vs 'deserves skepticism', 'works when' vs 'works best today when'), and does a number
  measured on ONE benchmark/model/config get presented as holding generally;
  (9) NEW — DOES ANY LISTED REF SUPPORT THE DETAIL AT ALL? A fact can accumulate specifics from
  sources that were read but never cited. If no listed ref carries it, remove it or add the ref.
  And for framework docs: record the LANGUAGE BINDING a default belongs to.
