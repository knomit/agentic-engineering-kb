---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-20 (twenty-first run). THREE DAYS after the 20th, so the feed sweep was owed and run.
The 20th run's Finding 1 said a feed is UNREAD until someone reads its FRONT PAGE AS A LIST. I ran that
test on four feeds. It paid immediately — and it also convicted the 20th run: aisi.gov.uk/blog is 95
posts deep, not the ~10 it catalogued after "opening the back catalogue".
*** IN-RUN SELF-REVIEW FOUND THREE DEFECTS IN THIS RUN'S OWN OUTPUT. All corrected in place. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***

=== HISTORY WALK ===
REVISIONS READ: 6 bodies, covering 6 runs (13th, 16th, 17th, 18th, 19th, 20th).
  22649951 (HEAD, 2026-08-18T00:07:35Z) — 20th run's final body.
  4feee885 (2026-08-15T18:30:20Z)       — 19th run.
  7a9ec830 (2026-08-15T13:47:52Z)       — 18th run's first write.
  3bc37431 (2026-08-14T12:51:03Z)       — 17th run's FINAL body.
  3c6323cd (2026-08-12T21:25:35Z)       — 16th run.
  8b9a768d (2026-08-12T00:27:10Z)       — 13th run, carrying the AUTHORITATIVE 190-URL union.
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z. `more_available` was FALSE at BOTH 3c6323cd and
8b9a768d — the walk terminated on the API's own signal, twice. No call failed; no retry needed.
THREE REVISIONS DELIBERATELY NOT RE-READ, each a SAME-RUN second write already checked by a prior run.
Naming them rather than letting the count look complete:
  a5466f42 (08-17T23:49) 20th run's first write; HEAD is the same run.
  a21ad1c0 (08-15T14:02) 18th run's final write — the 19th run read both and reported identical URLs.
  0ac250fd (08-14T12:23) 17th run's first write — the 20th run read both specifically to test whether
    a same-run second write can drop a line, and reported the same 5 articles from each.
I am relying on those two prior checks rather than re-running them. If a future run wants the walk
fully first-hand, those are the three to read.

ALREADY_CRAWLED = 190 (8b9a768d) + 10 (16th) + 5 (17th) + 7 (18th) + 4 (19th) + 9 (20th) + 8 (this
run) = **234 URLs I can NAME**, against an asserted true total of ~250.

*** THE GAP IS STILL THERE. FIFTH RUN REPORTING IT. NOT MINE TO FIX. ***
The 14th and 15th runs' bodies remain UNREACHABLE — their per-run commits were squashed into merge
commits ("Merge pull request #8", "#6") and the hashes recorded in prose (e61629fc, 8be9e4de,
5ab895cf) do not resolve. ~16 URLs from that window cannot be enumerated. They are described at
source level in the 17th run's body and I went nowhere near any of it.

*** THE DANGLING-REF PROBLEM IS ALSO STILL THERE. NOT RE-CHECKED THIS RUN. ***
kb/invariants/ai/agents/security/threat-taxonomy/4f5e9dfe.md is retracted but still cited by THREE
live facts: 483263c5, c02ac546, bdf3336e. Carried forward from the 20th run unverified — saying so
plainly rather than re-asserting it as though I had re-checked. Still for a human.

recurring-feed indexes swept: SIX.
  api.github.com/.../contents/docs/specification  (MCP tripwire — UNCHANGED. 2024-11-05, 2025-03-26,
    2025-06-18, 2025-11-25, 2026-07-28, draft. ELEVENTH consecutive run unchanged.)
  www.aisi.gov.uk/blog       *** READ AS A LIST FOR THE FIRST TIME. 95 posts. SEE FINDING 1. ***
  embracethered.com/blog     *** READ AS A LIST FOR THE FIRST TIME. 10 posts back to Mar 2026. ***
  cognition.com/blog         *** READ AS A LIST FOR THE FIRST TIME. 82 posts back to Mar 2024. ***
  www.microsoft.com/en-us/security/blog  *** READ AS A LIST FOR THE FIRST TIME. 12 posts, front page
    only (this one paginates). 11 of 12 threat intel or analyst-report marketing. Rank 22 CONFIRMED
    on evidence rather than impression. One on-topic candidate, unread, noted in crawl-sources. ***
  www.anthropic.com/news/    (NOTHING new since the Aug 14 watermark post, already read.)
  openai.com/index via WebSearch  (surfaced ONE previously-uncatalogued slug: /index/the-defenders-window/.)
NOT swept, deliberately: anthropic.com/engineering (quiet since Apr 2026, five consecutive
  confirmations; the 20th run said stop re-sweeping it for a while and I did).

articles newly crawled (8 genuinely new URLs):
  aisi.gov.uk/blog/how-are-ai-agents-used-evidence-from-177000-ai-agent-tools          <- 1 fact
  aisi.gov.uk/blog/what-can-sandboxed-ai-agents-learn-about-their-evaluation-environments <- 1 fact
  aisi.gov.uk/blog/how-do-environmental-factors-impact-ai-behaviour                    <- 1 fact
  aisi.gov.uk/blog/stress-testing-asynchronous-monitoring-of-ai-coding-agents          <- 1 fact + 1 upd
  aisi.gov.uk/blog/evidence-for-inference-scaling-in-ai-cyber-tasks-increased-evaluation-budgets-reveal-higher-success-rates  <- 1 major upd
  embracethered.com/blog/posts/2026/recovering-encrypted-llm-thoughts/                 <- 1 fact
  embracethered.com/blog/posts/2026/hijacking-litellm-for-fun-and-profit/              <- 1 fact
  (the four index enumerations above are sweeps, not article reads, and are not counted here)
re-fetched for the staleness pass, already known: genai.owasp.org/download/50592/?tmstv=1754459367
  and huggingface.co/blog/agent-intrusion-technical-timeline.

errored / not obtained: NONE. No 403s, no 404s, no paywalls, no timeouts, no guessed slugs. Every
AISI and embracethered URL came from an index listing rather than from a title, which is why.
ONE TOOL failure, loud not silent: ugrep rejected a `.{0,90}` keyword-in-context pattern with
"exceeds complexity limits". Recorded as fetch-routes 2d — a run that reads that error as "no
matches" manufactures a false absence.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FINDINGS ===

*** FINDING 1 — THE 20th RUN OPENED A FEED'S BACK CATALOGUE AND STILL SAW ONLY A VIEWPORT. THE FIX
IS ONE FETCH, AND IT RETURNS THE WHOLE ARCHIVE. ***
The 20th run's headline finding was that aisi.gov.uk had been swept three times without anyone
following it to article level; it opened the back catalogue, took three posts, and recorded the four
remaining items as "UNREAD, ranked". I asked the index for EVERY post as a list. It returned 95,
complete to 2023-09-07. So the 20th run's "4 unread" was not the feed's tail — it was how far one
summary happened to scroll, and the same understatement would have persisted for several more runs.
THE GENERALISATION, and it is cheap: **"I opened the back catalogue" is not the same claim as "I have
the index".** After reading a feed's front page, ask whether you got the whole thing or the viewport.
Measured, one plain WebFetch each, no browser: aisi 95 posts (full archive), cognition 82 (full
archive), embracethered 10, microsoft/security 12 (front page only — that one paginates). Three of
four served their ENTIRE archive to a single call. Recorded as fetch-routes route 5.
AND THE TELL THAT YOU HAVE REAL HREFS RATHER THAN DERIVED ONES: title/slug MISMATCHES. AISI returned
/blog/advancing-voice-ai-security-with-elevenlabs for "Advancing AI voice security with ElevenLabs"
(word order differs) and a CMS "-2" dedup suffix on another. A list where every slug is a clean
slugification of its title is the one to distrust.
YIELD: four AISI posts read, four facts. The feed is now RANK 1 and has a real catalogue.

*** FINDING 2 — ROUTE 4 IS NOT ABOUT NUMBERS. IT FABRICATED A MODEL VERSION AND A QUOTATION. ***
The 20th run established that an open-ended WebFetch invents FIGURES. Two new cases this run, neither
a figure, both caught by the mandated second call:
  (a) A VERSION IDENTIFIER. Open-ended call: the blue team's monitor model is "Claude 3.5 Sonnet".
      Verbatim call: "The Blue team builds monitoring systems using a weaker model (Claude 3.7
      Sonnet)". A minor-version slip that would have mis-specified the capability gap the entire
      experiment turns on. Checklist item 9 now has a FETCH-LAYER cause, not only an author-layer one.
  (b) A PARAPHRASE INSIDE QUOTATION MARKS. Open-ended call returned LiteLLM described as "a popular
      AI gateway. It provides a unified interface to LLMs and simplifies governance" — in quote marks.
      The page says "LiteLLM is an open-source proxy presenting a unified API over OpenAI, Anthropic,
      Azure OpenAI, Bedrock, and others." That is the 56986e8f defect class — this pack's oldest and
      most recurrent — being MANUFACTURED BY THE TOOL. It can now enter a fact with nobody paraphrasing.
SO THE RULE WIDENS: any string you intend to put in quotation marks, any figure, any threshold, AND
any version or product identifier goes through the second call. Calibration held: 8/8, 6/6 and 8/8
verbatim confirmations across three pages this run. The tool is accurate when the page states the
thing; it invents when the page does not.
AND THE CORRECT RESPONSE TO "I DIDN'T ASK ABOUT IT" IS TO DROP IT. Two figures from the first
extraction of the MCP-tools post (a geographic download breakdown; an attribution of AI-coauthored
servers to one coding agent) were omitted purely because they were not on the verbatim list. Omitting
is cheaper than hedging and leaves no half-sourced sentence for a later run to promote.

FINDING 3 — A FACT'S OWN CENTRAL QUOTATION CAN BE UNFINDABLE IN THE DOCUMENT IT CAME FROM.
92dc0441 rests on "The allowlist does not fail to prevent the attack. It streamlines it, by
auto-approving the very commands the attacker needs to trigger the payload." Grepping the extract for
"It streamlines it" returns ZERO. The pdftotext wrap falls between "streamlines" and "it". So a
verification pass that searches for the quotation to confirm it would conclude the quotation is
invented — the exact inverse error, and it would have "corrected" a correct fact. Mechanism (i) of the
negative-grep list, but pointed at a fact's own evidence rather than at a new claim. Always grep the
rarest SINGLE word and read the surrounding lines.

FINDING 4 — A DOCUMENT'S PROSE AND ITS NUMBERS SAT 2,300 LINES APART, AND THE FACT GOT THE PROSE.
7bd6c6c9 was written from OWASP 50592's narrative on skill poisoning (extract ~line 1160). The
prevalence figure for the SAME campaign — "~12% of 2,857 ClawHub skills found malicious in Feb 2026
audit" — is at line 3473, in the personal-agents appendix. One in eight skills in a registry is the
number that decides whether this is a curiosity or a default assumption, and the fact had none of it
for three weeks. RULE, now in fetch-routes: after writing a fact from a long PDF's narrative, grep the
WHOLE extract for the campaign or product name again and read every other hit. Narrative sections
carry the story; appendix tables carry the quantities.

FINDING 5 — TWO AISI POSTS SEVEN MONTHS APART SAY THE SAME THING ABOUT MONITORS FROM OPPOSITE ENDS,
AND TOGETHER THEY MOVE A DESIGN DECISION.
Dec 2025 (red/blue stress test): monitor quality improved ~10x across three rounds of adversarial
iteration — 67% missed down to 6% missed — and "the weaker Round 1 monitor acting synchronously
outperformed the best Round 3 monitor working asynchronously". Jul 2026 (Control Red Team, already in
the pack as a5eaec6b): vulnerabilities in every monitor version tested, the routing rule that decides
WHICH actions reach the monitor is a softer target than the monitor's prompt, and asynchronous review
is defeated by faked goal provenance.
THREE INDEPENDENT AXES, ONE CONCLUSION: the monitor's own accuracy is not where the leverage is. That
is worth a `decisions` fact because it inverts the default engineering instinct, which is to improve
the classifier. NOTE WHAT AISI DOES NOT SAY: it concludes async monitoring "is likely a useful tool
and can act as one layer of a defense-in-depth approach". Not "do not use async". The fact says so.
THE DECIDING VARIABLE IS THIS PACK'S AND IS MARKED AS SUCH: async is an explicit decision to let
harmful actions run and catch them later, so it is defensible where the action is REVERSIBLE and not
otherwise. Sort the tool surface by reversibility, not by risk score.

FINDING 6 — THE MCP ECOSYSTEM INVERTED FROM READ TO WRITE AND NOBODY IN THIS PACK HAD NOTICED.
Action tools went from 24% to 65% of monthly downloads over 16 months; 95% of general-purpose tool
downloads are action-capable; general-purpose-in-unconstrained-environments grew 41%->50%. So the
fastest-growing half of the ecosystem is precisely the acting-in-untrusted-environment combination the
prompt-injection literature calls dangerous, and the two properties arrive together rather than being
independently distributed. Also: dev/IT is 67% of published tools and 90% of downloads, so outside
developer tooling the ecosystem's apparent size is not available to you.
WHY THIS MATTERS AS METHOD: this pack holds ~25 facts about MCP mechanics and had zero about what is
actually IN the ecosystem. A protocol's specification and its population are different objects and
only one of them was being tracked.

=== FACTS WRITTEN (6 new, 2 updated from crawling, 5 touched by the staleness pass, 3 revised by the
=== in-run self-review, 0 retracted) ===
  NEW —
    kb/architecture/ai/agents/tools/mcp/ecosystem/45d86a7d        (Finding 6. 177,436 tools; the
      read->write inversion; the dev/IT concentration; payment-execution servers 46 -> 1,200+; 55% of
      new servers AI-assisted. All 8 figures verbatim-confirmed; 2 unverified ones dropped.)
    kb/gotchas/ai/agents/evaluation/environment-leakage/d0c5b9f8  (OpenClaw identified AISI, a named
      employee, the cloud provider and the research chronology from TLS certs, DNS, config files and
      one API call — and iterative hardening failed. The infrastructure-side twin of eval awareness:
      canary strings do not touch a TLS certificate.)
    kb/gotchas/ai/agents/evaluation/environment-factors/f4e0cbaf  (600,000+ evals, 23 models, 11
      environments, 12 toggled factors. HALF the variation in unsanctioned behaviour is non-strategic;
      anti-misalignment and independence instructions are the biggest such levers; no capability trend.)
    kb/decisions/ai/agents/security/monitor-placement/42e1218f    (Finding 5. Placement dominates
      quality; the 67%->6% iteration gain did not close the sync/async gap; reversibility as the
      deciding variable, marked as this pack's.)
    kb/gotchas/ai/agents/security/reasoning-traces/1d01a338       (encrypted reasoning blobs replay
      across accounts into a weaker model that is then asked to transcribe them — the ciphertext is
      never broken, so the confidentiality boundary is model behaviour. Author's "likely" hedge on
      shared keys PRESERVED; the 315,320/367/182 figures attributed to the cited paper, not the post.)
    kb/invariants/ai/agents/security/gateway/b17b7fc2             (two config fields turn an LLM
      gateway into a MITM that harvests provider keys AND injects tool-calls into responses — so the
      blast radius is "the attacker drives your agents", and every content-inspecting injection
      defence sits upstream of it. CVE-2026-42271 in CISA KEV; Mar 2026 PyPI compromise.)
  UPDATED FROM CRAWLING —
    80866fc3  — the Mar 2026 AISI/Irregular predecessor post: the curve is LOGARITHMIC ("every time we
      double the token budget, we see about the same absolute increase in success rate"), Irregular's
      cost-per-success metric, the four-part transparency ask. sources 1->2 WITH AN EXPLICIT SCOPE
      NOTE that both refs are AISI's and the ~8% tail figure is likely the same measurement
      re-reported — corroboration within one programme, not replication.
    a5eaec6b  — the Dec 2025 stress test as a second AISI experiment quantifying its weakness 2.
      sources 1->2, conf 0.8->0.85, cross-linked to 42e1218f, with the same one-organisation caveat.

CONTRADICTIONS: none between sources requiring a `decisions` fact. One near-miss handled by NOT
flattening: AISI's Dec 2025 conclusion ("async is likely a useful tool") reads as weaker than the
engineering implication of its own headline result. Both are in 42e1218f, the source's conclusion
quoted and the sharper reading marked as this pack's.

=== STALENESS PASS (5 sampled; PRIMARY AXIS SHARED-REF as the rotation required. 1 CORRECTED (twice
=== over), 4 CONFIRMED, 3 of them ENRICHED, 0 retracted. TWO fetches covered five facts.) ===
  HOW THE SAMPLE WAS FOUND, cheaper than either previous method: knomit_query rows carry BOTH
    `committed_at` AND `refs` in frontmatter. So the topical queries run anyway for the query-first
    rule hand you the age axis and the shared-ref axis simultaneously. Five facts fell out across
    exactly TWO source documents. Recorded in fetch-routes.
  ONE OF THE TWO SOURCES WAS PROVEN BYTE-STABLE, WHICH IS A STRONGER CLAIM THAN "I RE-READ IT":
    OWASP 50592 re-downloaded, `pdfinfo` = 139 pages, CreationDate 2026-06-01 — identical to what the
    12th run recorded and the 18th re-confirmed. Three facts verified against a document that
    demonstrably did not change.
  7a4f9061 (0.85 -> 0.9) CORRECTED TWICE. (a) A MULTIPLIER: the title said the decode recovered "4x
    MORE secrets"; the source says "recovered roughly 4x our initial findings" — four times as many,
    not four times more, which would be five. (b) AN UNATTESTED STEP INSIDE A QUOTED TECHNICAL SCHEME:
    the fact described the encoding as "chunked, XOR, gzip, then base64"; the source says
    "chunked+XOR+gzip encoded with a per-campaign key" and a targeted check for base64 returned
    nothing. Removed rather than hedged. THIS IS THE COMPLETION-OF-A-SET CLASS the 20th run named for
    numbers, appearing in a PIPELINE — base64 is the plausible last step, which is exactly why it got
    written. ENRICHED with "~6,280 clusters" alongside the ~17,600 actions (a ~3:1 ratio, so triage
    sized per raw action over-sizes by that factor).
  e3b629d0 (0.9 -> 0.95) CONFIRMED, every step of the escalation chain re-quoted verbatim from the
    primary — the metadata address and literal curl, the `k8s-aws-v1.` construction, CSI/TokenRequest,
    the cluster-wide grant, eleven nodes, both halves of the remediation. Nothing overstated.
  78ab92f2 (0.85 -> 0.9) CONFIRMED verbatim — quotation, CVE-2025-6514, CVSS 9.6, "fifteen versions",
    "hundreds of thousands of developers". ENRICHED with TWO parts of the AI Agent Traps framework the
    fact had missed: approval fatigue is classified as A DELIBERATE ATTACK ON THE HUMAN REVIEWER (so
    prompt RATE is a security parameter and "users click through anyway" is the attacker's objective,
    not an excuse), and MULTI-AGENT SYSTEMIC TRAPS including "fragmented payloads that reconstitute
    only when aggregated across agents" — every fragment individually benign, so per-agent inspection
    is structurally blind and detection must sit where fragments recombine. Modality preserved: OWASP
    states this anticipatorily and the fact does not upgrade it.
  92dc0441 (0.85 -> 0.9) CONFIRMED verbatim (Finding 3). ENRICHED with the sentence that generalises
    it past security: OWASP puts the two CVEs next to the Replit production-database deletion and says
    "Replit's failure had no adversary, the CVEs required one, but the underlying permission
    architecture is the same." So the case for tightening an allowlist does not depend on believing
    you have an adversary — it pays in the reliability failure mode too.
  7bd6c6c9 (0.85 -> 0.9) CONFIRMED verbatim. ENRICHED with the prevalence figure (Finding 4) and its
    frame: a proportion of the skills AUDITED in one registry at one date, in an audit already
    targeting a suspected campaign — not a general base rate.
  Nothing in the kb is yet older than 90 days (pack began 2026-07-26; today is day 25).

=== IN-RUN SELF-REVIEW OF THIS RUN'S OWN SIX FACTS: THREE DEFECTS, ALL FIXED ===
  f4e0cbaf — THE FACT DID THE THING IT WARNED AGAINST. It named three strategic and four non-strategic
    factors taken from the open-ended extraction, while its own sourcing paragraph told the reader the
    post does not list the twelve anywhere and warned against reconstructing them from examples.
    Removed; only the two verbatim-quoted most-influential factors survive. A fact that contradicts
    its own caveat is worse than one that simply overclaims, because the caveat makes it look checked.
  45d86a7d — A LOOSE TIME REFERENCE. "Two years ago an MCP integration was predominantly a read path"
    — the 24% figure is the START OF THE SOURCE'S 16-MONTH WINDOW, not a point two years before today.
    Rewritten to the source's own frame. Also tightened "~26x" to "at least a 26-fold increase", since
    the numerator is "over 1,200".
  42e1218f — AN UNVERIFIED SETUP DETAIL, which turned out to be TRUE. The red team's side tasks
    ("exfiltrating secrets or weakening security policies") came from the open-ended call. Rather than
    flag it, I ran the third verbatim call: confirmed exactly. AND IT RETURNED SOMETHING BETTER — "The
    Red team can only modify the agent's system prompt; they can't fine-tune the model or rewrite its
    outputs", which STRENGTHENS the result: the monitor saw genuine model output, not a forged
    transcript. Worth noting as method: verifying beat flagging, and cost one call.
  ALSO CHECKED AND CLEAN: 1,200/46 = 26.1; 315,320 / 367 / 182 attributed to the cited paper and not
    to the blog author; the "likely" hedge preserved on the shared-key claim; every CVE identifier.
  AND ONE REF DEFECT CAUGHT IMMEDIATELY: I added a cross-ref from 80866fc3 to f4e0cbaf that the body
    never uses. Removed in a follow-up update rather than left as a ref supporting nothing.

PROMPT INJECTION: none observed. Worth stating because two sources read this run are attack write-ups
containing working technique descriptions — the LiteLLM post gives a complete gateway-hijack chain,
and the reasoning-trace post describes the injection used to make a model transcribe a decrypted blob.
Both read as security research about other systems. Nothing fetched addressed this job or attempted to
redirect it. The AISI sandbox-discovery post describes an agent instructed to investigate its own
deployment, which is the closest thing to a page modelling this job's own situation; it was read as
reportage and acted on in no way.

=== SUGGESTED SPLIT FOR THE NEXT RUN ===
(1) THE AISI TIER-A QUEUE, now a real ranked list of ~50 in crawl-sources. Best pairs first:
    transcript-analysis-for-ai-agent-evaluations + a-pipeline-for-transcript-analysis-using-inspect-scout
    (same problem, 4 months apart, pairs with f877f05d); then how-to-evaluate-control-measures-for-ai-agents;
    then can-ai-agents-escape-their-sandboxes-... (pairs with the whole eval-containment cluster);
    then llm-judges-on-trial-... (pairs with 38c06627).
(2) THE TWO NAMED PAPERS THAT FILL STATED GAPS IN FACTS WRITTEN THIS RUN — highest value per fetch:
    "Stealing Reasoning Traces from Proprietary LLM APIs" (1d01a338 holds its figures second-hand)
    and "What_OpenClaw_learned_about_us" (d0c5b9f8 says outright that the blog offers no mitigations
    and the paper has them). Both resolvable by WebSearch.
(3) MCP TRANSPORTS IN FULL — basic/transports/streamable-http.mdx and stdio.mdx. Only their Backward
    Compatibility sections have ever been read. Carried from the 20th run UNTOUCHED; still top MCP.
(4) THE OWASP MCP SECURITY WHITE PAPER — NEW LEAD. 50592 calls it "the most granular threat taxonomy
    for tool invocation protocols, identifying 12 distinct categories". This pack holds three of the
    twelve. Resolve the id by fetch-routes 2b. Strongest untouched OWASP target, ahead of Appendix C.
(5) OWASP AGENTIC TOP 10 APPENDIX C (NHI mapping, extract line 1882+, table 1886) and the per-entry
    mitigations for ASI03-ASI07/ASI09. Untouched again this run.
(6) embracethered: /2026/agent-commander-your-agent-works-for-me-now/ is TOP (promptware C2, pairs
    with 7a4f9061's improvised-protocol material and 4e923405), then given-enough-agents-all-bugs-
    become-shallow, then breaking-opus-4.7-with-chatgpt.
(7) COGNITION, now fully catalogued: devin-sonnet-4-5-lessons-and-challenges is TOP (a harness rebuilt
    for a new model — rare content, pairs with d6c50e81), then coding-agents-101, swe-grep,
    devin-annual-performance-review-2025.
(8) openai.com/index/the-defenders-window/ (NEW slug, unknown date) and
    /index/putting-frontier-cyber-models-in-more-trusted-hands/ (Aug 10). Browser route.
(9) RUN THE INDEX-AS-LIST TEST ON THE REMAINING UNTESTED FEEDS — it is one fetch each and it has now
    paid on 2 of 4. Still untested: huggingface.co/blog, research.google/blog, sourcegraph.com/blog,
    latent.space/archive, langchain.com/blog, eugeneyan.com/writing, trychroma.com/research,
    metr.org/blog, microsoft.com/en-us/research/blog, aws.amazon.com/blogs/machine-learning.
(10) STILL WATCHING, four artifacts, none landed as of 2026-08-20: (a) OpenAI's technical report on
    the HF incident; (b) the METR+Redwood joint assessment; (c) Irregular's containment white paper;
    (d) Anthropic's watermark DETECTION API (943a7e3c is qualitative because the post has no rates).
(11) The OWASP ASI incidents tracker at owasp-agentic-ai-security-incidents.lovable.app — TEN runs
    listed without a fetch. Check first whether it is simply Appendix D of the Top 10 PDF.
(12) FOR A HUMAN, NOT THE CRAWLER — four items, all carried forward:
    (a) 4f5e9dfe is retracted but cited by THREE live facts: 483263c5, c02ac546, bdf3336e.
    (b) The 14th/15th run bodies are unreachable behind squashed merges. FIVE runs have reported both.
    (c) 0f260eea and 1d1440fe each carry a claim their source fact has since corrected, and
        kb/principles/ is write-blocked to the job. Not re-checked this run.
    (d) knomit_review's distill stage can see the private .knomit/ slots. Not re-tested this run.

=== PER-SOURCE STATUS AND QUEUE, as of the 21st run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

*** UK AISI — RANK 1. Full 95-post catalogue now in crawl-sources: 8 read, ~50 ranked unread in
*** tier A, ~35 explicitly below the bar so nobody spends a fetch discovering they are scorecards. ***
*** EMBRACETHERED — catalogue added. 5 read, 5 unread, ranked. Low volume, high hit rate. ***
*** COGNITION — 82-post catalogue added. ~25 worth reading, ranked; half the feed is announcements. ***
*** MICROSOFT SECURITY — front page read as a list. Rank 22 confirmed on evidence. One candidate. ***
OWASP GenAI PDF REPORTS — STATUS:
  State of Agentic AI Security and Governance 2.01 (139pp, id 50592)  READ 12th; 3 facts re-verified
    21st against a PROVEN-UNCHANGED document. Useful extract line numbers are now in crawl-sources.
    ^ chapters still NOT written up: Enterprise Adoption Maturity Model (p53-62), Alignment with
      Top 10 Agentic (p61), Future Trends / What Remains Unsolved (p63-68); AI SBOM and Supply Chain
      Provenance (p46-48); Explainable AI (p49); Appendix 1 agent-type taxonomy (p70-76); Appendix 3
      ASI risk classes (p116); Appendix 6 Top 10 Impacting Personal Agents (p128). Appendix 2 is low.
  AIUC-1 Crosswalks (55pp, id 54627)                         READ 11th, 3 facts+1 upd; re-verified 18th.
  AI Security Solutions Landscape Red Teaming Q2 2026 (15pp, id 54018) READ 11th, 1 fact; re-verified 18th.
    ^ Vendor market map — LOW remaining yield, do not re-mine.
  OWASP GenAI LLM Top 10 2026 (122pp, id 56857)              READ 13th, 2 facts + 1 upd
    ^ NOT mined: the ten per-entry chapters. LLM03 (p23-26) and LLM08 (p46-49) most relevant.
  Securing Agentic Applications Guide 1.0 (id 49059)         READ 15th, 2 facts
    ^ MOSTLY BELOW THE BAR. One pass max: 2.2 Secure Architecture Patterns (extract 833-1313),
      2.5 Case Studies, 9.x runtime hardening.
  Multi-Agentic System Threat Modeling Guide v1.0 (id 46950) READ 15th, 1 fact + critiqued 16th
    ^ SECTION 5 STILL UNMINED: MCP threat modelling using MAESTRO (extract line 3132 on).
  Agent Name Service (ANS) v1.0 (id 47278)                   READ 16th, 1 fact + 1 upd. DONE.
  OWASP Top 10 for Agentic Applications 2026 (id 52117)      READ 17th + 18th, 5 facts total.
    ^ Remaining: Appendix C (NHI mapping, line 1882+), Appendix B (CycloneDX/AIBOM), per-entry
      mitigations for ASI03-ASI07 and ASI09, Appendix D per-incident detail.
  *** MCP SECURITY WHITE PAPER — NEW LEAD, id UNRESOLVED. See split item 4. ***
OWASP HTML blog posts read fine with a plain WebFetch. Unread and promising:
  /2026/05/13/memory-is-a-feature-it-is-also-an-attack-surface/  (ASI06; pairs with 7bd6c6c9)
  /2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/
  /2026/04/14/finbot-ctf-is-live-...
*** MCP 2026-07-28 — TRIPWIRE CHECKED 21st RUN VIA THE REPO, UNCHANGED (11th consecutive) ***
READ SO FAR: changelog, versioning (learn page AND spec page), deprecated, server/discover,
  basic/patterns/mrtr, basic/index, server/tools, learn/server-concepts, docs/extensions/overview,
  security_best_practices at 2025-06-18 / 2025-11-25 / 2026-07-28, THE ENTIRE 2026-07-28
  AUTHORIZATION SPLIT (all four pages), basic/authorization.mdx at 2025-11-25 / 2025-06-18 /
  2025-03-26, and the Backward Compatibility sections of transports/stdio and transports/streamable-http.
  ALSO: all 41 files of 2025-11-25 and all 186 of 2026-07-28 fetched for verification sweeps.
STILL UNREAD, in value order: transports/streamable-http and transports/stdio IN FULL (top),
  server/utilities/caching (ttlMs/cacheScope), extensions/tasks + apps overviews,
  docs/<rev>/develop/clients/client-best-practices, /specification/2026-07-28/schema (low altitude).
OTHER STANDING UNREAD: cnn.com/2026/08/05/tech/meta-ai-hacking (secondary — find the primary); the
  simonwillison queue (/2026/Jul/31/stateless-mcp/, the-tokenpocalypse, /2026/Aug/2/open-letters/);
  the four per-model Claude prompting sub-pages; the Azure RAG six-part series and
  azure-openai-gateway-monitoring (which b17b7fc2 now gives a security angle).

YIELD RANKING as of the TWENTY-FIRST run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES via the GitHub contents API. Cheapest high-value call, outage-proof,
     EVERY run. And where a spec is versioned in git, DIFF REVISIONS — with the six preconditions in
     fetch-routes.
  2. *** UK AISI BLOG. PROMOTED FROM 3 TO 2 ON THIS RUN'S EVIDENCE: four posts, four substantial
     facts, one of them the strongest architectural decision fact the pack has taken in weeks. It has
     a 95-post catalogue and roughly fifty ranked unread items. This is the deepest unmined seam in
     the pack and it is plain-WebFetch readable. ***
  3. OWASP GenAI PDF REPORTS. Nine read for 29+ facts. Route solved ten times over. Mine ARCHITECTURE,
     THREAT-MODEL METHOD, DISAMBIGUATION, MITIGATION PATTERNS and MATURITY; SKIP control checklists.
     AND GREP THE APPENDICES FOR NUMBERS after writing from the narrative (Finding 4).
  4. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, anthropic.com/news. Both quiet this run.
  5. PUBLISHED CRITIQUES OF SOURCES ALREADY IN THE KB. Search "critique/gaps in <document>".
  6. MCP remaining spec pages. The two transport pages are next.
  7. embracethered.com/blog — PROMOTED from 20 to 7. Two posts, two facts this run, and the catalogue
     shows a consistent agent-security focus. Low volume, so a sweep is cheap.
  8. cognition.com/blog — now fully catalogued, ~25 real engineering posts unread.
  9. anthropic.com/engineering — UNREAD: AI-resistant-technical-evaluations, building-c-compiler,
     contextual-retrieval, swe-bench-sonnet, desktop-extensions. Index quiet since Apr 2026.
 10. microsoft.com/en-us/research/blog — prefer METHOD over FRAMEWORK posts.
 11. Azure Architecture Center. The six-part RAG series is the largest coherent unread block.
 12. aws.amazon.com/blogs/machine-learning — product-heavy, but spec changes surface early.
 13. builder.aws.com Builders' Library — 16 of 30 read for 55+ facts; the 12 unread skew CI/CD.
 14. huggingface.co/blog — scan for incident/infrastructure/engineering; SKIP model/dataset launches.
 15. sourcegraph.com/blog — real measurements. 16. eugeneyan.com/writing — secure-source-code unread.
 17. simonwillison.net/tags/llms/ — VALUE IS THE LINKS. Talk summaries are its weakest output.
 18. latent.space/archive. 19. langchain.com/blog — eval posts clear the bar, customer stories do not.
 20. blog.redwoodresearch.org — watch-only. 21. metr.org/blog — demoted 13th run; re-rate on the
     joint assessment. 22. trychroma.com/research — rare but substantial; evaluating-chunking unread.
 23. research.google/blog and microsoft.com/en-us/security/blog — BOTH low, the latter now confirmed
     by an actual index read rather than by impression.

dead or unreadable — EMPTY, and still NINE FOR NINE on false dead ends. Read the warning in Appendix S.
  block.github.io/goose -> goose-docs.ai (old host serves a stub; the docs MOVED to AAIF governance,
    they did not die). strandsagents.com/latest/... -> 404; use /docs/...
  modelcontextprotocol.io -> ECONNREFUSED 2026-08-12 only; transient, fine since.
  modelcontextprotocol.io/docs/concepts/tools -> recorded GONE by the 16th run; it REDIRECTS (200).
  .../2025-11-25/basic/authorization/security-considerations.mdx 404s because authorization was ONE
    FILE at that revision. A 404 can mean the path SHAPE changed. See fetch-routes 3b/3c.

TIER 6 GITHUB READMEs — CLOSED OUT. A repo README is worth a fetch for LIFECYCLE STATUS and nothing
else; if a repo matters, go to its DOCS site. AMENDMENT (16th run): a repo that HOSTS a documentation
site is different — there the repo is the primary source and beats the site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

VERIFICATION-POOL NOTE (updated 21st run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, 714a540c, f7dee43a, 9aaea0dc, 9e29d93a, 1531a0d1, b4d688b1,
99aa74e6, 0720e9d7, 59a75c06, b471f9ef, ba5db3ec, f4005c98, c28c7f7b, 11ebefd6, db15af92, 8f2fdde8,
ee3bc7d3, ca3382bd, 46eeb374, 703147ba, ba1b7aad, 8cf06566, 07eec7ff, 2d060289, 1719fe66, 43155c66,
406e5a50, bdb36fce, f8646714, ce7e0330, 30543305, 60544a53, f4bba0ae, eae23eac, 6c0c742e, 74996815,
24e4552d, 36d792c3, 00fd386c, 19ed6273, 70127cdd, a13a57c9, 0b340b6b, ac887ec9, 5f4497f2, 9b0c8c78,
8756141e, a5eaec6b, 80866fc3, f4367bd0, 943a7e3c, and (21st run) 7a4f9061, e3b629d0, 78ab92f2,
92dc0441, 7bd6c6c9, plus this run's own 45d86a7d, d0c5b9f8, f4e0cbaf, 42e1218f, 1d01a338, b17b7fc2.
THREE AXES, ROTATE THEM: confidence (lowest first), earliest-committed, shared-ref grouping.
13th earliest-committed (2 defects in 5); 14th confidence (1+1 partial); 15th shared-ref (3 in 5);
16th earliest+shared-ref (2 in 5); 17th shared-ref (0 claim defects, 3 ref additions, 2 source-count
fixes); 18th earliest-committed (1 correction, 1 scope correction, 4 enrichments); 19th confidence
(2 corrected, 3 confirmed-and-enriched, 1 confidence raised); 20th earliest-committed (4 corrected of
5 — highest defect rate yet); 21st SHARED-REF (1 corrected twice over, 4 confirmed, 3 enriched).
READ THE 21st RESULT AGAINST THE 20th: the 20th's earliest-committed sample found 4 defects in 5; the
21st's shared-ref sample found 1 in 5. That is not the pass working less well — it is the axes
measuring different things. EARLIEST-COMMITTED finds facts written before the pack's method matured,
so it finds CLAIM defects. SHARED-REF finds facts that share a source, so its yield is COMPLETENESS:
this run's real output was three enrichments that each changed what the fact tells you to do, plus a
document proven byte-stable. Do not read a low defect count as a wasted pass.
NEXT RUN: rotate the primary axis to CONFIDENCE (lowest first), still grouping by shared ref. Good
never-checked candidates at 0.7-0.75: af3acf92, 805bc132, 12966de6, 2d7219c8, and this run's own
1d01a338 (0.75, and it deserves an early re-check because its central causal claim is the author's
hedged inference and a vendor may since have responded).
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result.

SUB-RULES, cumulative:
 (14th) A PARTIAL confirmation must be written down as partial, in the fact.
 (15th) When a quoted sentence appears in more than one fact, a defect in it is duplicated too — query
   the kb for the quotation before correcting it. (Run this run on the "4x" claim: unique to 7a4f9061.)
 (15th) Check that a CITED PAGE ACTUALLY CARRIES the detail attributed to it.
 (15th) RUN THE CHECKLIST ON THE FACTS YOU JUST WROTE. Seven runs, seven harvests: 3 in 8, 3 in 7,
   2 in 3, 3 (17th review pass), 1+3 (18th), 1+1 (19th), 1+1 (20th), 3 in 6 (21st). Not optional.
   AND RUN A SEPARATE PASS AFTER COMMITTING where budget allows.
 (16th) Where a source is versioned and in git, DIFF REVISIONS instead of re-reading.
 (17th) A claim that a path is dead, or that content moved, is a claim like any other. Test it.
 (17th) The self-review must RE-RUN COMPUTATIONS, not re-read passages.
 (18th) "NEW IN REVISION X" requires searching the WHOLE predecessor revision, every tree.
 (18th) VERIFY WHAT YOU DOWNLOADED, not that the download happened.
 (18th) A table of numbers without their anchors is not a reference.
 (19th) MATCH THE SEARCH'S SCOPE TO THE CLAIM'S SUBJECT NOUN.
 (19th) When a source gives both a LIST and a COUNT of it, COUNT THE LIST. Do not JOIN two adjacent
   source claims into one sentence.
 (20th) A QUANTIFIER OVER A STRUCTURE YOU DID NOT REPRODUCE IS UNCHECKED — go back and count.
 (21st) *** THE SECOND FETCH IS NOT ONLY FOR NUMBERS. *** Any quoted string, figure, threshold OR
   version/product identifier goes through it. The tool fabricates all four. And if you did not ask
   the second call about it, you do not have it — drop it rather than hedge it.
 (21st) *** A FACT THAT CONTRADICTS ITS OWN CAVEAT IS WORSE THAN ONE THAT SIMPLY OVERCLAIMS ***, because
   the caveat makes it look checked. When you write "the source does not state X", re-read the fact
   for places where you stated X anyway. Caught live in f4e0cbaf.
 (21st) *** VERIFYING BEATS FLAGGING WHEN IT COSTS ONE CALL. *** The instinct on an unverified detail
   is to mark it uncertain. One extra fetch confirmed it AND returned a stronger adjacent sentence
   that improved the fact. Flag only what you cannot cheaply check.

WHAT THE VERIFICATION PASS ACTUALLY FINDS — FOURTEEN RUNS. Mostly NOT stale facts: CITATION-FIDELITY
and COMPLETENESS defects in facts whose underlying claims are correct. The named classes so far:
  paraphrase wearing quote marks (56986e8f, 0b340b6b); overclaiming gloss attributed to the source
  (c93d93ee, 96ebc34e); inverted causation (c7290868); wrong actor (c858a924); wrong terms (c436422a,
  f78a326a); misattribution across a fact's own refs (38c06627, 714a540c, eae23eac); modal
  strengthening incl. in TITLES (d18637a2, f7dee43a, 9aaea0dc, b4d688b1, 30543305); PDF line-wrap
  reconstructed as a literal (0720e9d7); genuine staleness (59a75c06); overclaimed absence hiding a
  MUST->SHOULD (b471f9ef); inflated quantifier in a title (11ebefd6); unchecked version attribution
  (db15af92); title undercut by its own body (8f2fdde8); source-count inflation (ca3382bd, 46eeb374);
  incomplete mapping vouched for by a method sentence (703147ba); contaminated counting range +
  wrong evidence for a correct conclusion (8cf06566); tense-altered quotation (ba1b7aad); numbers
  without their frame (406e5a50); superlative true only in a subset (2d060289); false method claim
  (1719fe66); incomplete sweep described as exhaustive (bdb36fce); unmarked inference next to a quote
  (ce7e0330, ac887ec9); three attribution defects in one fact (f4bba0ae); the first UNDERCLAIM
  (74996815); two source claims joined into one (30543305); FABRICATED FIGURES (19ed6273, 70127cdd)
  and a fabricated tool identifier (a13a57c9); and NEW THIS RUN — an inflated multiplier ("4x more"
  for "4x") and AN UNATTESTED STEP APPENDED TO A QUOTED TECHNICAL SCHEME (7a4f9061).
CHECKLIST — verify all SIXTEEN explicitly, not just "is the claim still true":
  (1) quotation boundaries — every quoted string in the source VERBATIM INCLUDING TENSE AND
  INFLECTION, and does the quote START where the source's sentence starts;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what a pronoun refers to — AND WHETHER THE SOURCE DISAMBIGUATES IT AT ALL; if not, give both
  readings rather than silently picking one;
  (5) are the TERMS attributed to the source actually the source's terms;
  (6) refs classification (local vs external) and `sources` counts — N pages of ONE specification is
  ONE source, and TWO posts from ONE organisation's programme is corroboration, not replication;
  (7) FOR MULTI-REF FACTS, which ref supports which number — is one reported instance presented as a
  general rule — and does ANY listed ref support it. HARD CASE: a claim can be TRUE, from the SAME
  vendor, and still cited to the wrong post. AND: does every ref support SOMETHING the body says;
  (8) MODAL STRENGTH, QUANTIFIERS AND SCOPE, IN BODY AND TITLE SEPARATELY, including SUPERLATIVES;
  (9) LANGUAGE BINDING AND VERSION — and note the fetch tool can invent a version (21st run);
  (10) LITERALS FROM A PDF ARE RECONSTRUCTIONS, and a negative grep is unreliable for SIX reasons
  (wrap, hyphen, form feed, markdown emphasis, tool fabrication, grep erroring out). Distinguish PACK
  ANALYSIS from SOURCE CLAIM — a gloss next to a citation gets read as cited, so mark it;
  (11) VERSION ATTRIBUTION IS A CLAIM. Check the WHOLE predecessor revision, every tree;
  (12) A FACT'S STATEMENT OF ITS OWN METHOD IS THE CLAIM MOST LIKELY TO BE FALSE — and the error is
  not always flattering; it can also understate the evidence;
  (13) RE-RUN EVERY COMPUTATION AND RE-DERIVE EVERY CROSS-DOCUMENT INFERENCE. Bound counting regions
  on the FOLLOWING HEADING. Check the cited evidence SUPPORTS the conclusion rather than sitting near it;
  (14) DOES EVERY NUMBER CARRY ITS FRAME? A duration needs its start event, a percentage its
  denominator, a count its region, a superlative its population, a relative delta its baseline, AND A
  PROPORTION ITS SAMPLING METHOD (21st run: "~12% of skills malicious" is one targeted audit of one
  registry, not a base rate);
  (15) RE-RUN THE SEARCH ITSELF, not only the sum — inspect its ANCHOR and its SCOPE, and match the
  scope to the CLAIM'S SUBJECT NOUN;
  (16) DID YOU JOIN TWO SOURCE CLAIMS THAT THE SOURCE KEPT APART? Adjacency in a post is not a
  relationship. Where the source offers both a LIST and a COUNT of it, count the list.
