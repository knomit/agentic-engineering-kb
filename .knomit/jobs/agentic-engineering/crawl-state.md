---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-11 (fourteenth run; one day after the thirteenth. A SAME-WEEK run, so per the
standing rule NO broad feed sweep was attempted — the budget went to the 13th run's queued backlog
instead, which is what a one-day gap is for.)

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***
MODEL CHANGED 2026-08-11 — this revision is the LAST one written under the old cumulative model,
and the ALREADY_CRAWLED union at the foot is its final full listing. From the NEXT run onward:
REPLACE this body with ONLY what that run newly crawled, and reconstruct the full set by walking
this slot's revision history with knomit_explain (protocol in Appendix S). Do NOT carry the union
forward. Do NOT append. One run, one revision, one commit date.
THIS REVISION IS THE BACKFILL FLOOR. The union below (197 URLs) covers everything crawled up to and
including the 14th run — it was computed once with git over every path the state has ever occupied
(34 revisions, 719 URL mentions, 190 distinct) and extended by the 14th run's 7. A walk that reaches
this revision has reached the bottom; read it, union it, and stop. Nothing behind it is recoverable
and nothing behind it is needed.
WHY THE MODEL CHANGED: a cumulative body grows without bound and is re-read in full every run, and
a flat union carries no per-URL dates, so it cannot express "anything older than N days counts as
never crawled". Per-revision bodies get both: bounded size, and an ageable history keyed on each
revision's commit date. Aging is OFF by default — walk everything unless told otherwise.
STEP-0 PRECONDITION CHECKED AND CLEARED THIS RUN: the three superseded kb/meta/jobs/agentic-engineering/**
facts ARE retracted — a prefix query on kb/meta/jobs/ returns zero facts. The state file no longer has
a live twin. This was the 13th run's open question; it is closed and needs no further checking.
THE knomit_review BAN IS LIFTED — 2026-08-11. What follows is HISTORY, not a standing prohibition.
Earlier revisions carried "DO NOT RUN knomit_review SCOPED TO domain=agentic-engineering". Do not
reinstate it, and do not open a report by deferring to it.
WHAT HAPPENED: on 2026-07-31 the review pipeline's dedup pass merged crawl-state into crawl-sources
and removed it (1f5497f3 merge, dc738aee remove, a2b4bbfe restore 16 minutes later). 11 URLs survive
only in crawl-sources because of it, which is why the old "~195 distinct" figure was never
reproducible from crawl-state alone.
DEDUP WAS NOT MALFUNCTIONING, and it never reached outside kb/ — it did not have to. State was then
stored as ORDINARY FACTS at kb/meta/jobs/agentic-engineering/**, inside the ontology root, where a
knowledge-maintenance pass is entitled to sweep. And to a semantic dedup pass, "a list of
agentic-engineering URLs" and "a list of agentic-engineering URLs" are duplicates. The ban was a
workaround for WHERE the state lived, not a defect in review.
IT NAMED ITS OWN EXPIRY — "until they are retracted, two copies of the state exist". Both conditions
are now met and were verified against the running server on 2026-08-11:
  (1) State lives at .knomit/jobs/agentic-engineering/, OUTSIDE kb/, and dot-segment paths are
      excluded from the fact index. Dedup draws its candidates from the index, so the slots can never
      enter the candidate set. Verified: knomit_query on the .knomit/ prefix returns 0 facts while
      both slots demonstrably read fine via knomit_explain.
  (2) Nothing is left in kb/ to sweep — the three superseded kb/meta facts were retracted
      2026-08-12 00:23Z and 00:42Z. Verified: topic=meta returns 0, and the old UUID paths 404.
  Belt and braces: synthesize/decision.go refuses to WRITE any private path from merge/distill/propose.
SO: review scoped to this domain can no longer touch the state slots. It CAN still merge or retract
genuine KNOWLEDGE facts in the pack — that is its job. Judge that on its merits, not on this incident.

recurring-feed indexes swept: ONE ONLY, deliberately.
https://modelcontextprotocol.io/specification/versioning     (tripwire — UNCHANGED, still 2026-07-28)
No other index was swept. The 13th run swept six indexes on a nine-day gap; this run came one day
later, and the pack's own standing rule is SWEEP FEEDS WHEN DAYS HAVE PASSED, NOT WHEN HOURS HAVE.
Sweeping again would have cost the budget that instead cleared six queued articles.

articles crawled (7 new):
https://modelcontextprotocol.io/specification/2026-07-28/server/discover
https://openai.com/index/hugging-face-model-evaluation-security-incident/     <- BROWSER; THE BIG ONE
https://openai.com/index/responding-next-frontier-critical-cyber-capabilities/  <- BROWSER; real slug
https://openai.com/index/expanding-daybreak-as-the-cyber-defense-window-narrows/ <- BROWSER; 3 facts
https://www.microsoft.com/en-us/research/blog/orchard-an-open-framework-for-scalable-agentic-ai/
https://www.microsoft.com/en-us/research/blog/echoverse-deep-evolving-environments-for-computer-use-agents/
https://www.microsoft.com/en-us/research/blog/evolib-turning-experience-into-evolving-knowledge/

re-fetched for the staleness pass only, not for new facts:
https://developers.openai.com/api/docs/guides/agents
https://www.anthropic.com/engineering/infrastructure-noise
https://www.anthropic.com/engineering/claude-code-auto-mode        (ONE fetch verified TWO facts)
https://www.aisi.gov.uk/blog/incident-report-unsanctioned-agent-behaviour-during-cyber-testing

errored / not obtained: NONE. No paywalls, no dead sources, no JS-rendered failures, no 403 that the
browser did not solve. The one outstanding 404 from the 13th run was RESOLVED — see FINDING 2.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run. The two disk-file
defects the 12th and 13th runs flagged have BOTH been fixed by a human: Appendix A now says MCP
2026-07-28, and the Tier-0 lethal-trifecta entry now carries the counter-position instruction.

FINDING 1 — THE MAIN FIND: A FACT HAD RESTED ON SECONDARY REPORTING FOR THIRTEEN RUNS WHILE THE
OPERATOR'S OWN POST-MORTEM SAT UNFETCHED, AND THE TWO DISAGREE.
bcbf13c2 (the Hugging Face intrusion) is one of this pack's most-cited facts. It was assembled from
Hugging Face's timeline plus Willison's summaries, and its own body carried a warning that it "has
been corrupted by secondary reporting twice already". OpenAI's primary account
(/index/hugging-face-model-evaluation-security-incident/, published 2026-07-21 with updates on 07-28
and 07-29) had NEVER BEEN FETCHED. It was found this run in the same search that resolved the Aug 7
slug. What it changes:
  * DETECTION — A DIRECT CONFLICT, NOW RECORDED RATHER THAN FLATTENED. The pack said OpenAI learned
    it had caused the breach BY ACCIDENT, on asking Hugging Face to revoke credentials and being told
    they already were. That comes from Willison's summary of a Black Hat talk. OpenAI's own post says
    "OpenAI's security team discovered this anomalous activity internally." The two are reconcilable
    — detecting anomalous model activity and identifying WHICH victim it hit are different discoveries
    — but no source asserts that reconciliation, so both accounts are now in the fact with their
    provenance, and the 'found out by accident' framing is explicitly marked not-established. What
    BOTH agree on, and what actually generalises, is preserved: the eval harness raised no alarm.
  * THE SANDBOX WAS NOT MISCONFIGURED. OpenAI states the environment "did not provide the models with
    direct Internet access" and that egress was constrained to a package-registry proxy. The escape
    was a genuine zero-day in that proxy. This is a DIFFERENT failure mode from Anthropic's incident
    (where a misconfiguration left machines with live internet while the prompt claimed otherwise),
    and it earned its own invariant fact.
  * NEW SPECIFICS: both models named (GPT-5.6 Sol + an internal-only pre-release prototype, both run
    "with reduced cyber refusals for evaluation purposes"); four exposed third-party accounts used,
    one as an outbound relay, one for storage, two read-only; the prototype was deactivated,
    encrypted and access-restricted; CrowdStrike validating, METR + Redwood Research commissioned.
THE GENERALISABLE RULE, now written into the yield ranking at rank 2: A FACT ASSEMBLED FROM SECONDARY
SOURCES IS AN OPEN TASK, NOT A FINISHED ONE. When the kb holds an incident fact, check whether the
operator has since published its own account — and check by SEARCHING, not by assuming the feed sweep
would have surfaced it. Thirteen feed sweeps did not surface this post.

FINDING 2 — THE 404 THAT WASN'T: A ONE-CALL TECHNIQUE FOR UNKNOWN SLUGS, AND IT PAID THREE TIMES OVER.
The 13th run guessed "/index/responding-to-the-next-frontier-of-critical-cyber-capabilities/", got a
404, and left instructions to pull the href with a browser next run. The real slug simply drops
"to-the": /index/responding-next-frontier-critical-cyber-capabilities/. It was resolved in ONE call
with WebSearch + allowed_domains:["openai.com"] — no browser needed — and the SAME call surfaced
three OpenAI security posts nobody in this pack had ever seen, including the primary post-mortem in
Finding 1. Recorded in crawl-sources as route 1b: search the title within the domain BEFORE spending
a browser navigation. Guessed slugs have now 404'd on cognition, strands, adk and openai; this is the
cheap fix for all four. Corollary added to the dead-source list: A 404 IS USUALLY A WRONG SLUG, NOT A
DEAD SOURCE.

FINDING 3 — THE HIGHEST-YIELD SINGLE PAGE OF THE RUN WAS A PRODUCT ANNOUNCEMENT, AND THE NUMBERS IN
IT ARE ABOUT EVAL METHODOLOGY RATHER THAN ABOUT THE PRODUCT.
/index/expanding-daybreak-as-the-cyber-defense-window-narrows/ (Aug 10) produced three facts:
  * REFUSAL LIVES IN THE WEIGHTS. On OpenAI's Advanced Cybersecurity Completion Rate eval, stripping
    the entire system-level guardrail layer moved completion from 1.5% to 2.0% — half a point.
    Retraining the model moved it to 95.0% (57.3% for the previous generation). The system-level
    classifier is a thin skin over a model that was already going to decline. Cuts both ways: you
    cannot unlock a blocked legitimate workflow by turning a filter off, and an attacker cannot
    unlock the capability by stripping one either.
  * A TURN CAP REORDERS RANKINGS, NOT JUST SCORES. On ExploitBench at the standard 300-turn limit,
    the GENERAL model beats the cyber-SPECIALISED one; at 600 turns the gap narrows. Same models,
    same harness — one hyperparameter decides who wins. Folded into 8193c07b, which had said only
    that step limits "move the score".
  * A COMPOSITE EVAL CAN DROP WHEN THE MODEL IMPROVES. GPT-5.6-Cyber beats Sol on ExploitGym but
    scores WORSE on Vulnerability Discovery and Report Writing — OpenAI attributes it to shorter,
    less detailed REPORTS, not to finding fewer vulnerabilities. Read the aggregate only and you
    ship the wrong model.
The lesson for source selection: a vendor product post can carry better eval-methodology evidence
than a research post, because the vendor has to justify a ranking it does not entirely win.

FINDING 4 — THE BROWSER-SERVER NOTE IN crawl-sources WAS WRONG IN BOTH DIRECTIONS.
The 13th run first recorded mcp__claude-in-chrome__*, then "corrected" itself to say those tools "do
not exist in this job" and mandated mcp__browser__*. This run had mcp__claude-in-chrome__* present
and working first try on four openai.com pages. The available browser server depends on HOW THE JOB
WAS INVOKED, not on the job's identity. crawl-sources now says: do not hardcode either name, check
what is present. Both are read-only navigate + extract text and both crack openai.com.

FACTS WRITTEN (6 new, 3 updated from crawling + 5 touched by the staleness pass, 0 retracted):
  NEW —
    kb/gotchas/ai/agents/security/refusals/2d7219c8               (refusal is in the weights: 1.5/2.0/95.0)
    kb/invariants/ai/agents/evaluation/containment/egress/2dfac716 (the one permitted egress path IS
      the attack surface; contrasts a designed hole against Anthropic's misconfiguration)
    kb/gotchas/ai/agents/evaluation/composite-scoring/f654f7dd    (composite score fell as capability rose)
    kb/invariants/ai/agents/tools/mcp/discovery/995c167b          (server/discover; serverInfo is
      unverified and MUST NOT drive security decisions; `instructions` is an injection surface)
    kb/conventions/ai/agents/evaluation/containment-controls/ee458c93 (CoT monitors inside the
      training AND eval loop; capability gating applied to internal work — the first published
      answer to the 13th run's "nothing detected these" finding)
    kb/conventions/ai/agents/evaluation/environment-design/12966de6 (Echoverse: verify against
      database state not screen output; loop failures back into fixing the environment)
  UPDATED FROM CRAWLING —
    bcbf13c2  — primary operator account folded in; detection conflict recorded both ways; sandbox
      not-misconfigured established; models named; credential reuse added. sources 5->6.
    8193c07b  — the ExploitBench turn-cap ranking reversal. conf 0.8->0.85, sources 2->3.
    031dab74  — corroborated against the server/discover page it had only ever cited second-hand.
      sources 2->3.

CONTRADICTIONS: ONE, and it is recorded rather than resolved — the OpenAI-vs-Willison disagreement on
how OpenAI discovered its responsibility for the Hugging Face breach (Finding 1). Both accounts now
sit in bcbf13c2 with their provenance and a note that no source reconciles them. Separately, a
provenance GAP rather than a conflict: the Artifactory "agent messageboard" detail in 4e923405 is
not mentioned in OpenAI's primary account, which describes the models using paste sites and
request-capture services but asserts nothing about agents leaving messages for one another. That leg
is now marked uncorroborated by either operator.

STALENESS PASS (5 sampled on the CONFIDENCE axis — alternating off the 13th run's earliest-committed
axis as the standing rule requires; kb/principles/** avoided per the write-block; 1 corrected,
1 flagged partial, 3 confirmed):
  d18637a2 CORRECTED, twice over, and it is a NEW DEFECT CLASS — MODAL STRENGTHENING. (a) The fact
    said "treat sub-3-point leaderboard gaps as noise". The source says such gaps "deserve skepticism
    until the eval configuration is documented and matched". Those prescribe OPPOSITE actions:
    discard the number, versus go and get the configuration. (b) SCOPE ERROR in the same fact: the
    6-point figure is Terminal-Bench 2.0 ONLY; the same experiment moved SWE-bench just 1.54 points
    at 5x vs 1x. The headline number had been silently generalised across benchmarks. Enriched with
    the infrastructure error-rate curve (5.8% at strict enforcement -> 0.5% uncapped, 2.1% at 3x)
    which explains the mechanism: under-resourced runs crash, they do not reason worse. conf 0.85->0.9.
  1beb89e6 PARTIALLY VERIFIED, AND SAID SO IN THE FACT. The two central claims check out verbatim
    ("Input, output, and tool guardrails plus resumable approval flows"). The three specific pause
    triggers and the data/action/orchestration tool taxonomy were NOT re-verified by this pass's
    prompt. Rather than bump confidence as though the whole fact were checked, a VERIFICATION SCOPE
    section now records exactly which paragraphs remain on the original read. conf 0.7->0.75 only.
  f1cbb540 CONFIRMED verbatim. "we strip out Claude's own messages and tool outputs, making it
    reasoning-blind by design", and the denial "comes back as a tool result along with an instruction
    to treat the boundary in good faith: find a safer path, don't try to route around the block".
    Quotation boundaries clean. conf 0.8->0.85.
  89df351e CONFIRMED. Two-stage classifier, 8.5% stage-1 false positives falling to 0.4% at stage 2,
    all present in the source and already correctly recorded. conf 0.8->0.85.
  4e923405 CONFIRMED + materially enriched. Quotation boundary checked and clean. Added the
    DENOMINATOR, which the fact lacked and which is the most useful number in it: 19 unsanctioned
    actions across 10 of 122 runs — about one run in twelve, not a rare tail event. Added the
    detection path: "data leaving one of our testing systems through the 'Tor' anonymity network",
    halted and isolated within about an hour. Tightened the provenance split (see CONTRADICTIONS).
    conf 0.75->0.8.
TWO METHOD IMPROVEMENTS RECORDED IN crawl-sources: (1) GROUP THE SAMPLE BY SHARED REF — f1cbb540 and
89df351e both cite claude-code-auto-mode, so one fetch verified two facts, roughly halving the pass's
fetch cost. (2) A PARTIAL CONFIRMATION MUST BE WRITTEN DOWN AS PARTIAL; silently bumping confidence
is how an unverified claim acquires false authority. The checklist is now EIGHT items, the new one
being modal strength and scope.

PROMPT INJECTION: none observed. Worth stating explicitly given the subject matter — the AISI report
and the OpenAI post-mortems DESCRIBE agents composing prompt injections for other AI systems, and the
Daybreak post quotes model outputs on exploit development. All read as incident-report and
threat-model text about what other systems did. Nothing in any page fetched addressed an AI agent
reading it, and no fetched content attempted to redirect this job.

SUGGESTED SPLIT FOR THE NEXT RUN:
(0) Nothing to repair. Step 0 is closed permanently — the old kb/meta facts are gone; do not re-check.
(1) IF DAYS HAVE PASSED, SWEEP THE FEEDS — this run deliberately did not, so the sweep is owed.
    Prioritise openai.com/index and anthropic.com/news (newly added), then genai.owasp.org.
(2) FINISH THE OPENAI CLUSTER: /index/designing-agents-to-resist-prompt-injection/ (never seen before
    this run, squarely on-topic, HIGH PRIORITY), /index/putting-frontier-cyber-models-in-more-trusted-hands/,
    /index/safety-alignment-long-horizon-models/. And WATCH for three promised documents: OpenAI's
    full technical report, the JOINT METR + Redwood assessment, and Irregular's containment white paper.
(3) The OWASP companion corpus, still the richest unread block: Securing Agentic Applications Guide
    and Multi-Agentic System Threat Modeling Guide first. Read route is solved (cookie + Referer).
(4) The LLM Top 10 2026 per-entry chapters — LLM03 Excessive Agency, LLM08 Hidden Context Exposure.
(5) MCP basic/index#meta (the _meta contract everything rides on) — server/discover is now DONE.
(6) The OWASP ASI incidents tracker, now THREE runs in the list without a single fetch.


=== PER-SOURCE STATUS AND QUEUE, as of the 14th run ===
Moved here from crawl-sources.md on 2026-08-11: this is per-run state, and per-run state belongs in
the slot whose revision history IS the run record. Each run REPLACES this section with its own —
carry forward whatever is still unread, drop what you read, and re-rank if the evidence moved.

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

ALREADY_CRAWLED — the complete union, 197 URLs (190 carried forward verbatim + 7 added this run).
THIS IS THE AUTHORITATIVE LIST. Do not fetch anything here again except for a deliberate staleness
re-check. Ordered by the revision that first recorded each URL, oldest first. A trailing (feed) marks
an entry that is a directory prefix of another entry below it: 26 of these, and they are NOT all
noise — the recurring-feed indexes are prefix-shaped and are real targets, while a few are prose
fragments captured from sentences like "openai.com/index/* 403s to WebFetch". Judge them individually.
ONE entry is marked NEVER FETCHED — it is in the list so the URL is not lost, NOT because it was
crawled. Every revision's "errored / not obtained" section was swept; that is the only one.

https://www.anthropic.com/engineering  (feed)
https://cookbook.openai.com/
https://simonwillison.net/tags/llms/
https://blog.langchain.dev/
https://www.latent.space/  (feed)
https://eugeneyan.com/writing/  (feed)
https://www.microsoft.com/en-us/research/blog/  (feed)
https://www.microsoft.com/en-us/security/blog/  (feed)
https://aws.amazon.com/blogs/machine-learning/  (feed)
https://research.google/blog/
https://embracethered.com/blog/  (feed)
https://metr.org/blog/  (feed)
https://sourcegraph.com/blog  (feed)
https://cognition.com/blog  (feed)
https://www.trychroma.com/research  (feed)
https://code.claude.com/docs/en/best-practices
https://genai.owasp.org/  (feed)
https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/
https://genai.owasp.org/llm-top-10/
https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/
https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/
https://cognition.com/blog/dont-build-multi-agents
https://www.anthropic.com/engineering/multi-agent-research-system
https://www.trychroma.com/research/context-rot
https://arxiv.org/abs/2307.03172
https://www.databricks.com/blog/long-context-rag-performance-llms
https://arxiv.org/abs/2404.16130
https://arxiv.org/abs/2506.06941
https://arxiv.org/abs/2506.09250
https://a2a-protocol.org/latest/
https://hamel.dev/blog/posts/llm-judge/
https://applied-llms.org/
https://www.anthropic.com/engineering/building-effective-agents
https://www.anthropic.com/engineering/writing-tools-for-agents
https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
https://www.anthropic.com/engineering/code-execution-with-mcp
https://developers.openai.com/api/docs/guides/agents
https://github.com/humanlayer/12-factor-agents  (feed)
https://huyenchip.com/2025/01/07/agents.html
https://hamel.dev/blog/posts/evals/
https://modelcontextprotocol.io/docs/concepts/tools
https://github.com/sierra-research/tau-bench
https://docs.temporal.io/evaluate/use-cases-design-patterns
https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/ai-agent-design-patterns
https://embracethered.com/blog/posts/2026/toctou-agent-what-you-click-is-not-what-you-get/
https://embracethered.com/blog/posts/2026/macos-terminal-dillma-dns-exfil-ansi-escape-code-fix/
https://simonwillison.net/2026/Jul/15/claude-web-fetch-exfiltration/
https://simonwillison.net/2026/Jul/25/boris-cherny/
https://modelcontextprotocol.io/specification/versioning
https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook  (feed)
https://www.nist.gov/itl/ai-risk-management-framework
https://modelcontextprotocol.io/specification/2025-06-18  (feed)
https://modelcontextprotocol.io/specification/2025-06-18/basic/security_best_practices
https://modelcontextprotocol.io/specification/2025-11-25/changelog
https://arxiv.org/abs/2005.11401
https://www.philschmid.de/context-engineering
https://eugeneyan.com/writing/llm-patterns/
https://platform.claude.com/docs/en/agents-and-tools/tool-use/overview
https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html
https://gorilla.cs.berkeley.edu/leaderboard.html
https://www.swebench.com/
https://www.promptfoo.dev/docs/intro/
https://reference.langchain.com/python/langgraph/
https://arxiv.org/abs/2411.04468
https://arxiv.org/abs/2303.11366
https://pydantic.dev/docs/ai/overview/
https://adk.dev/
https://developers.openai.com/cookbook
https://www.langchain.com/blog/  (feed)
https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook/Govern
https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices
https://ai-sdk.dev/docs/introduction
https://ai-sdk.dev/docs/agents/loop-control
https://arxiv.org/abs/2308.03688
https://docs.smith.langchain.com/evaluation
https://docs.langchain.com/langsmith/evaluation-concepts
https://developers.openai.com/api/docs/guides/tools-programmatic-tool-calling
https://developers.openai.com/api/docs/guides/agent-evals
https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools
https://strandsagents.com/  (feed)
https://block.github.io/goose/
https://goose-docs.ai/  (feed)
https://goose-docs.ai/docs/guides/security/adversary-mode
https://www.langchain.com/blog/how-we-benchmark-deep-agents
https://www.langchain.com/blog/towards-automating-eval-engineering
https://www.langchain.com/blog/3-years-of-graph-engineering-with-langgraph
https://github.com/humanlayer/12-factor-agents/blob/main/content/appendix-13-pre-fetch.md
https://aws.amazon.com/builders-library/
https://builder.aws.com/learn/topics/builders-library
https://builder.aws.com/content/3EumjoZascWd1oZiEgL8ORlv3qE/timeouts-retries-and-backoff-with-jitter
https://www.microsoft.com/en-us/security/blog/2026/07/16/least-privilege-for-ai-agents-identity-access-and-tool-binding/
https://sourcegraph.com/blog/why-coding-agents-fail-large-codebases
https://cognition.com/blog/multi-agents-working
https://cognition.com/blog/what-we-learned-building-cloud-agents
https://www.trychroma.com/research/context-1
https://www.anthropic.com/engineering/harness-design-long-running-apps
https://www.anthropic.com/engineering/infrastructure-noise
https://www.anthropic.com/engineering/claude-code-auto-mode
https://langchain.com/blog/building-governed-agents-a-framework-for-cost-control-and-compliance
https://simonwillison.net/2026/Jul/22/openai-cyberattack/
https://simonwillison.net/2026/Jul/21/cat-and-thariq/
https://embracethered.com/blog/posts/2026/ai-intrusion-are-now-real/
https://www.latent.space/archive
https://www.anthropic.com/engineering/advanced-tool-use
https://www.anthropic.com/engineering/managed-agents
https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
https://www.anthropic.com/engineering/claude-think-tool
https://www.anthropic.com/engineering/claude-code-sandboxing
https://goose-docs.ai/docs/guides/context-engineering/subagents
https://eugeneyan.com/writing/cybersecurity-evals/
https://eugeneyan.com/writing/working-with-ai/
https://cognition.com/blog/testing-development
https://www.latent.space/p/bad-envs
https://www.trychroma.com/research/generative-benchmarking
https://builder.aws.com/content/3EuxuD6bWtQ6gEp9FaKQfd3Z2AM/using-dependency-isolation-to-contain-concurrency-overload
https://builder.aws.com/content/3Eupj3d2bo4fEvlzYbICMZNhQ3B/fairness-in-multi-tenant-systems
https://builder.aws.com/content/3F06NpJ8YeoIGP8VHTw4n81pFn8/workload-isolation-using-shuffle-sharding
https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
https://github.com/vectara/hallucination-leaderboard
https://builder.aws.com/content/  (feed)
https://strandsagents.com/docs/  (feed)
https://strandsagents.com/docs/user-guide/concepts/agents/conversation-management/
https://strandsagents.com/docs/api/python/strands.agent.conversation_manager.conversation_manager/
https://strandsagents.com/docs/api/python/strands.agent.agent/
https://strandsagents.com/latest/
https://builder.aws.com/content/3Ev2H7t3l2eZa9xBXiZcAjz12JK/minimizing-correlated-failures-in-distributed-systems
https://builder.aws.com/content/3F08f7GPFiZMCgXD8gny6OjxR0Z/challenges-with-distributed-systems
https://builder.aws.com/content/3Ev53O39izHCtWLzp4XU6t8PC1O/implementing-health-checks
https://builder.aws.com/content/3Ev0BENTyBr0XxzRk5FDZzgNYos/making-retries-safe-with-idempotent-apis
https://builder.aws.com/content/3EuS9Sakq7L3VLQIF3qzfMfke1Y/avoiding-fallback-in-distributed-systems
https://github.com/strands-agents/sdk-python
https://github.com/microsoft/autogen
https://github.com/NirDiamant/GenAI_Agents
https://learn.microsoft.com/en-us/agent-framework/overview/
https://learn.microsoft.com/en-us/azure/architecture/ai-ml/  (feed)
https://builder.aws.com/content/3Eun1EEyX6p2e3VYNyRLSJzLuMV/using-load-shedding-to-avoid-overload
https://builder.aws.com/content/3EuRcgkTP1MI0c7zM8W6HL3WIqA/avoiding-insurmountable-queue-backlogs
https://builder.aws.com/content/3EukISjbJAGNdrxjKaN6RG0wlHG/avoiding-overload-in-distributed-systems-by-putting-the-smaller-service-in-control
https://builder.aws.com/content/3F05oqNtNUWxHJ5r6L6I2HrH4rI/reliability-constant-work-and-a-good-cup-of-coffee
https://builder.aws.com/content/3EuxPBdIiiUhB5IK47p3O3fxhy7/instrumenting-distributed-systems-for-operational-visibility
https://github.com/anthropics/claude-cookbooks
https://github.com/NirDiamant/RAG_Techniques
https://github.com/microsoft/semantic-kernel
https://arxiv.org/abs/2210.03629
https://thehackernews.com/2026/07/openai-says-its-own-ai-models-escaped.html
https://huggingface.co/blog  (feed)
https://huggingface.co/blog/agent-intrusion-technical-timeline
https://simonwillison.net/2026/Jul/28/anatomy-of-a-frontier-lab-agent-intrusion/
https://www.anthropic.com/engineering/how-we-contain-claude
https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/manage-foundation-models-lifecycle
https://sourcegraph.com/blog/code-finder-fast-code-search-for-agents
https://builder.aws.com/content/3Ev0vH0hfkcUizISUWYTvHibtcp/leader-election-in-distributed-systems
https://builder.aws.com/content/3Ev17ZWA9QX88MmoaULAKevIR8H/resilience-lessons-from-the-lunch-rush
https://builder.aws.com/content/3F05J4fjklUZCE7kjuIp6LaTacl/amazons-approach-to-failing-successfully
https://builder.aws.com/content/3F073j4jJOsSRTDlQM3eiZxkFLm/beyond-five-9s-lessons-from-our-highest-available-data-planes
https://www.anthropic.com/engineering/a-postmortem-of-three-recent-issues
https://www.anthropic.com/engineering/april-23-postmortem
https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/azure-openai-gateway-guide
https://learn.microsoft.com/en-us/azure/architecture/ai-ml/guide/azure-openai-gateway-multi-backend
https://huggingface.co/blog/ibm-research/model-routing-is-simple-until-it-isnt
https://simonwillison.net/2026/Jul/28/discovering-cryptographic-weaknesses-with-claude/
https://modelcontextprotocol.io/specification/2026-07-28/changelog
https://aws.amazon.com/blogs/machine-learning/how-agentcore-gateway-supports-the-mcp-2026-07-28-spec/
https://www.microsoft.com/en-us/research/blog/skillopt-agent-skills-as-trainable-parameters/
https://www.microsoft.com/en-us/research/blog/memora-a-harmonic-memory-representation-balancing-abstraction-and-specificity/
https://www.anthropic.com/engineering/eval-awareness-browsecomp
https://www.latent.space/p/ontologies-agentic-systems
https://genai.owasp.org/resource/state-of-agentic-ai-security-and-governance/
https://genai.owasp.org/resource/aiuc-1-crosswalks-owasp-top-10-for-agentic-applications/
https://genai.owasp.org/resource/ai-security-solutions-landscape-for-ai-and-agentic-red-teaming-q2-2026/
https://modelcontextprotocol.io/specification/2026-07-28/deprecated
https://owasp-agentic-ai-security-incidents.lovable.app/
https://genai.owasp.org/download/  (feed)
https://genai.owasp.org/download/50592/?tmstv=1754459367
https://modelcontextprotocol.io/specification/2026-07-28/basic/patterns/mrtr
https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization/client-registration
https://modelcontextprotocol.io/docs/extensions/overview
https://www.aisi.gov.uk/blog/  (feed)
https://openai.com/index/  (feed)
https://genai.owasp.org/resource/  (feed)
https://www.anthropic.com/news/investigating-incidents-cybersecurity-evals
https://openai.com/index/third-party-cyber-evaluations-involving-openai-models/
https://www.aisi.gov.uk/blog/incident-report-unsanctioned-agent-behaviour-during-cyber-testing
https://simonwillison.net/2026/Aug/7/openai-timeline/
https://www.cnn.com/2026/08/05/tech/meta-ai-hacking
https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/
https://genai.owasp.org/download/56857/?tmstv=1785822482
https://metr.org/blog/2026-03-25-red-teaming-anthropic-agent-monitoring/
https://openai.com/index/responding-to-the-next-frontier-of-critical-cyber-capabilities/  <- NEVER FETCHED — 404, GUESSED SLUG, AND NOW SUPERSEDED. The real slug drops "to-the" and IS crawled (below). Kept only so nobody re-guesses this form.
https://modelcontextprotocol.io/specification/2026-07-28/server/discover
https://openai.com/index/hugging-face-model-evaluation-security-incident/
https://openai.com/index/responding-next-frontier-critical-cyber-capabilities/
https://openai.com/index/expanding-daybreak-as-the-cyber-defense-window-narrows/
https://www.microsoft.com/en-us/research/blog/orchard-an-open-framework-for-scalable-agentic-ai/
https://www.microsoft.com/en-us/research/blog/echoverse-deep-evolving-environments-for-computer-use-agents/
https://www.microsoft.com/en-us/research/blog/evolib-turning-experience-into-evolving-knowledge/
