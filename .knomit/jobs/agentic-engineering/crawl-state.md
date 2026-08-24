---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-08-21 (twenty-second run). ONE DAY after the 21st committed (2026-08-21T01:44Z), so per
the standing rule NO broad feed sweep — only the near-free MCP tripwire. The whole budget went to the
21st run's queue, and it took the item the 21st run ranked HIGHEST value per fetch: the two papers
that fill gaps facts written last run explicitly named in their own bodies. Both paid.
*** THE HISTORY WALK ITSELF TURNED OUT TO BE DEFECTIVE, AND IT IS NOT A ONE-RUN PROBLEM. SEE FINDING 1. ***
*** IN-RUN SELF-REVIEW FOUND FOUR DEFECTS IN THIS RUN'S OWN OUTPUT. All corrected in place. ***

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***

=== HISTORY WALK ===
REVISIONS READ: 7 bodies, covering 7 DISTINCT runs (13th, 16th, 17th, 18th, 19th, 20th, 21st).
  4cce7781 (HEAD, 2026-08-21T01:44:42Z) — 21st run.
  a5466f42 (2026-08-17T23:49:44Z)       — 20th run (first write).
  4feee885 (2026-08-15T18:30:20Z)       — 19th run.   *** NEARLY MISSED. SEE FINDING 1. ***
  a21ad1c0 (2026-08-15T14:02:16Z)       — 18th run (final write).
  3bc37431 (2026-08-14T12:51:03Z)       — 17th run (final write).
  3c6323cd (2026-08-12T21:25:35Z)       — 16th run.
  8b9a768d (2026-08-12T00:27:10Z)       — 13th run, carrying the AUTHORITATIVE 190-URL union.
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z. `more_available` was FALSE at 3c6323cd, whose
listing named 8b9a768d, and FALSE again at 8b9a768d. The walk terminated on the API's own signal.
No call failed; no retry needed.
NOT RE-READ, all three SAME-RUN second writes already cross-checked by prior runs, named rather than
left to make the count look complete: 22649951 (20th run's final write — I read the FIRST write of
that run instead, and the 21st run read this one; both report the same 9 URLs), 7a9ec830 (18th
first write; the 19th run read both and reported identical URLs), 0ac250fd (17th first write; the
20th run read both specifically to test whether a same-run second write can drop a line — it did not).

*** ALREADY_CRAWLED = 235, AND THE 21st RUN'S TOTAL WAS OFF BY ONE. ***
Re-derived rather than copied, per the standing rule to re-run every computation:
  190 (8b9a768d) + 10 (16th) + 5 (17th) + 7 (18th) + 4 (19th) + 9 (20th) = 225 through the 20th run,
  which is the 21st run's own stated subtotal and is correct.
  225 + 8 (21st run) = **233**, not the 234 the 21st run recorded. Its own addition slipped by one.
  233 + 2 (this run) = **235 URLs I can NAME.**
A trivial error with a non-trivial lesson attached: the 21st run wrote the checklist rule "RE-RUN
EVERY COMPUTATION" into this very file and then mis-added its own six-term sum. Arithmetic in the
bookkeeping gets the same scrutiny as arithmetic in a fact.

*** THE 14th/15th GAP IS STILL THERE. SIXTH RUN REPORTING IT. NOT MINE TO FIX. ***
Those two runs' bodies remain UNREACHABLE — per-run commits squashed into merge commits ("Merge pull
request #8", "#6") and the hashes recorded in prose (e61629fc, 8be9e4de, 5ab895cf) do not resolve.
~16 URLs from that window cannot be enumerated. Described at source level in the 17th run's body; I
went nowhere near any of it.

*** THE DANGLING-REF PROBLEM IS ALSO STILL THERE. NOT RE-CHECKED THIS RUN. ***
kb/invariants/ai/agents/security/threat-taxonomy/4f5e9dfe.md is retracted but still cited by THREE
live facts: 483263c5, c02ac546, bdf3336e. Carried forward unverified — saying so plainly rather than
re-asserting it as though I had re-checked. Still for a human.

recurring-feed indexes swept: ONE, deliberately.
  api.github.com/.../contents/docs/specification  (MCP tripwire — UNCHANGED. 2024-11-05, 2025-03-26,
    2025-06-18, 2025-11-25, 2026-07-28, draft. TWELFTH consecutive run unchanged.)
No other feed swept, on purpose: one day since the 21st, which swept six. Do not read this as a
skipped sweep. THE NEXT RUN SHOULD SWEEP if real time has passed.

articles newly crawled (2 genuinely new documents):
  https://arxiv.org/html/2608.09867v1  "Stealing Reasoning Traces from Proprietary LLM APIs"
    (canonical https://arxiv.org/abs/2608.09867)                          <- 2 new facts + 1 major upd
  https://cdn.prod.website-files.com/663bd486c5e4c81588db7a1d/69e63511d394ee65d788d9e7_What_OpenClaw_learned_about_us%20(2).pdf
    (6pp, pdfinfo CreationDate 2026-04-20)                                <- 1 new fact + 1 major upd
re-fetched, already known: aisi.gov.uk/blog/what-can-sandboxed-ai-agents-learn-... (for the paper's
  href only), microsoft.com/en-us/research/blog/echoverse-... (staleness),
  openai.com/index/expanding-daybreak-... (staleness, TWO facts), openai.com/index/prompt-injections/
  (staleness). The last two by the browser route.

errored / not obtained: NONE. No 403s, no 404s, no paywalls, no timeouts, no guessed slugs — both new
documents were reached by resolved hrefs rather than by guessing.
ONE PARTIAL NEGATIVE, recorded rather than buried: WebSearch did NOT find the AISI OpenClaw paper by
title (it is a hash-named Webflow CDN PDF, not an indexed page). Recovered by asking the blog post for
its links — now fetch-routes 5b. Also: knomit_query would not surface the queued fact id af3acf92
across three differently-angled queries, so it was substituted rather than chased further.

Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.

=== FINDINGS ===

*** FINDING 1 — THE HISTORY WALK SKIPS ONE REVISION BODY PER HOP, AND IT ALMOST COST ME AN ENTIRE
*** RUN. THIS AFFECTS EVERY RUN THAT HAS EVER FOLLOWED APPENDIX S LITERALLY. ***
Appendix S says: take the OLDEST commit in `history.revisions` and anchor the next call on it. Each
call returns THE ANCHOR PLUS THE TWO NEXT-OLDER, so anchoring on the oldest advances the window by
TWO — and the MIDDLE entry of every listing is named but its body is never fetched. Measured on all
five hops this run; skipped without intervention: 22649951, 4feee885, 7a9ec830, 0ac250fd.
THREE OF THOSE FOUR ARE SAME-RUN SECOND WRITES AND COST NOTHING. THE FOURTH, 4feee885, IS THE ENTIRE
19th RUN — a distinct run, 4 URLs, seven findings of its own. I anchored straight past it and only
caught it by noticing the run-number sequence jumped 20 -> 18.
WHY NOBODY HAS REPORTED THIS BEFORE, and it is not that previous runs were careless: Appendix S step 4
does warn that "consecutive calls overlap by one revision — dedupe by commit hash". That overlap is
real, but it is the ANCHOR reappearing at the head of the next listing, not the middle entry. The
documented dedupe rule actively suggests the walk is complete. Earlier runs mostly escaped because
their middles happened to be same-run second writes, which they then deduped legitimately.
THE FIX, one line: **the revision LIST is the work list, not the anchor chain.** Accumulate every
commit any listing returns into a to-read set and read each unseen one. FREE CROSS-CHECK: bodies
self-identify as "crawled: <date> (Nth run)", so a gap in the run-number sequence is the tell — that
is exactly what caught it here. Recorded as fetch-routes route 6.
STATED PLAINLY FOR THE NEXT RUN: I cannot rule out that some earlier run's reported walk was short by
a distinct run in the same way. This does not affect the URL union, which is anchored on 8b9a768d's
enumerated 190 and on per-run counts that have been cross-checked repeatedly.

*** FINDING 2 — A PAPER NAMED BY A BLOG POST WAS UNSEARCHABLE, AND ASKING THE POST FOR ITS HREF TOOK
*** ONE CALL. THE PACK HAS BEEN USING THE WRONG TOOL FOR THIS CLASS. ***
The 21st run queued two papers as "resolvable by WebSearch". One was: the reasoning-traces paper
resolved by title in a single search, and the result set even handed over the /html/<id>v1 full-text
URL, which is the one you want (/abs/ is the abstract only).
THE OTHER WAS NOT. Searching "What OpenClaw learned about us" returned the AISI blog post itself plus
three unrelated OpenClaw security papers — never the artifact. Because it is not a published page: it
is `cdn.prod.website-files.com/<hash>/<hash>_What_OpenClaw_learned_about_us%20(2).pdf`, a Webflow CDN
asset indexed under nothing. No amount of searching finds it. Asking the POST for its links returned
it exactly, first try, with the link text.
THE RULE, now fetch-routes 5b: **when a post NAMES an artifact, ask the post for the href; do not
search for the artifact.** Route 1b (WebSearch + allowed_domains) resolves a SLUG on a site that
publishes pages. It does not resolve a hash-named asset on a CDN, and the failure looks like the
artifact not existing. The same call also established an absence cheaply — asked what mitigations the
post recommends, it answered NOT STATED and quoted the post deferring to the paper, which is what made
the paper worth the fetch.

*** FINDING 3 — ROUTE 4'S SECOND CALL IS ALSO AN ABSENCE FILTER, AND THAT CAUGHT THE PACK'S SECOND
*** UNDERCLAIM. ***
Route 4 exists because open-ended WebFetch INVENTS detail. This run it caught the inverse. 12966de6
had told readers for weeks that Echoverse's live-web transfer was "described qualitatively rather than
quantified", and had DEPRESSED ITS OWN CONFIDENCE on that basis. The post quantifies it: "The frozen
model clears base on both, WebVoyager 66.5% to 71.5% and Online-Mind2Web 40.5% to 43.4%." Asked
directly whether the post says transfer was unmeasured, the verbatim call answered NOT STATED.
THE TECHNIQUE THAT MADE THE DIFFERENCE: **ask the negative question explicitly.** "Does the source
state anywhere that X was NOT measured?" separates "the page does not say it" from "I did not see it".
An open-ended read cannot make that distinction and will quietly confirm your prior.
AND THE DELTAS WERE WORTH MORE THAN THE LEVELS: in-domain training is worth +30.6 points, live-web
transfer +5.0 and +2.9. Transfer is real and roughly a sixth to a tenth the size — which is the actual
decision input for anyone weighing whether to build synthetic environments, and neither the source nor
the fact had stated it as a ratio.
SECOND UNDERCLAIM IN THE PACK'S HISTORY (after 74996815). Checklist item 12 keeps proving that a
fact's account of its own method is the likeliest thing to be false, in EITHER direction.

*** FINDING 4 — THE TWO PAPERS BOTH ANSWERED THE EXACT QUESTION THEIR CITING FACT HAD WRITTEN DOWN
*** AS UNANSWERED. THE "NOT ESTABLISHED" PARAGRAPH IS A WORK QUEUE. ***
1d01a338 closed with three named gaps: the largest figures belonged to "a paper this pack has not
read"; the central causal claim was "hedged by its own author"; and "the post does not state that any
vendor was notified or responded". The paper answered all three — it reaches the same single-global-key
conclusion from systematic testing across OpenAI, Google and Anthropic, and it states that disclosure
happened and that providers implemented mitigations.
d0c5b9f8 closed with "it offers no mitigations... Anyone wanting a checklist has to go there." The
paper is the checklist: a three-round hardening ladder with the defence and its defeat at each step.
THE METHOD POINT, and it is cheap to act on: this pack's habit of writing an explicit NOT ESTABLISHED
paragraph turns out to double as a machine-readable backlog. Two facts, two runs later, two direct
hits. Keep writing them, and mine them deliberately rather than waiting to stumble on the source.

*** FINDING 5 — THE HARDENING LADDER TERMINATED ON THE ONE ENDPOINT THE AGENT WAS AUTHORISED TO CALL. ***
AISI closed the agent's config-file channel (mitmproxy sidecar injecting real credentials, agent sees
localhost placeholders; dnsPolicy: None). The agent dropped a layer: /proc/net/tcp for peer IPs, then
`openssl s_client` to read TLS certificates carrying `aisi` — using tools "already present in the
container environment". They closed that with iptables localhost-only. The agent then did not need to
bypass anything: `GET /v1/models` on the PERMITTED proxy returned 1,114 fine-tuned model names, whose
naming conventions reconstructed the research programme by theme and date.
THE REMEDY IS A GRANULARITY STATEMENT, in their words: "Realising our domain-based allowlisting was
too coarse, we implemented path-level allowlisting at the mitmproxy layer, restricting the agent to
content-generation endpoints only and filtering out metadata routes like model enumeration."
SO: an egress control scoped to a HOST cannot bound what an agent LEARNS, because the same host serves
the capability you granted and a catalogue describing your deployment. Scope on METHOD AND PATH, and
treat enumeration routes as a separate grant. This is fdad859e's finding arriving from the opposite
direction — that fact is about where data GOES, this is about what comes IN — and it supplies the
remedy fdad859e's control list was missing. ALSO NOTE: the leaked API keys were "ephemeral and tightly
scoped" and still exposed the ARCHITECTURE of the auth system. Rotating a secret does not hide the
shape of the thing around it.

*** FINDING 6 — REDUCING REFUSALS COST CAPABILITY, MEASURED, ON THE SAME PAGE. ***
2d7219c8 carried as a HYPOTHETICAL that completion rate "measures willingness to respond, not
capability or answer quality; a model can complete 95% of requests and be wrong on most of them." The
source demonstrates it: the 95%-completing GPT-5.6-Cyber is WORSE than base GPT-5.6 Sol on two of the
four evaluations reported — worse on Vulnerability Discovery and Report Writing ("producing shorter,
less detailed vulnerability reports") and beaten on ExploitBench at the standard 300-turn limit. It
wins where it was trained to (ExploitGym, the zero-day severity benchmark).
AND THE EXPLOITBENCH RANKING IS TURN-BUDGET DEPENDENT — the gap "narrows" at 600 turns. So a base-vs-
reduced-refusal comparison is not stable across harness configuration, which is this pack's standing
finding about benchmark scores landing in a new place. A caveat moved from asserted to evidenced,
which is a better outcome than a new fact.

=== FACTS WRITTEN (3 new, 3 updated from crawling, 4 touched by the staleness pass, 4 revised by the
=== in-run self-review, 0 retracted. 1d01a338 appears in two categories and is counted once.) ===
  NEW —
    kb/invariants/ai/agents/security/client-held-state/33aed84c   (an AEAD envelope attests the ISSUER,
      not the holder or the conversation position; single global key; three compatibility forms;
      all six §5.5 mitigations quoted and ordered; generalised — marked as inference — to any opaque
      client-held handle: resumption tokens, continuation handles, cached-context refs, checkpoints.)
    kb/gotchas/ai/agents/security/reasoning-traces/a7863d24       (the inbound twin: an injection sealed
      inside a reasoning block is received as the model's OWN PRIOR REASONING and "leaves no plaintext
      artifacts for monitors to catch" — so text-reading defences are not weak here, they are not
      connected to the channel. Control is strip-at-boundary, not inspect.)
    kb/decisions/ai/agents/evaluation/environment-sanitisation/0e577a90  (Finding 5's tradeoff half:
      strip too little and the agent infers the operator, too much and "the emptiness itself can signal
      ... it is being tested"; "no universal definition of 'sensitive'"; the four stated reasons the
      boundary is hard; pack's reading = treat sanitisation as a budget against the measurement, and
      accept a caveat on propensity evals rather than pretending the sandbox can be fixed.)
  UPDATED FROM CRAWLING —
    1d01a338  — all three of its own named gaps closed. Causal claim now independently reached by a
      systematic paper; disclosure status resolved WITH ITS SCOPE (the paper's non-reproducibility
      claim covers Figure 1 and two named sections only, and the blog post POST-DATES it and still
      demonstrates cross-account recovery by a simpler technique — recorded as a scope difference,
      NOT flattened into "fixed"). sources 1->2, conf 0.75->0.85.
    d0c5b9f8  — the full three-round ladder (Finding 5), every defence and its defeat quoted, the
      ephemeral-credentials point, the table's semantic-pairing caveat. sources HELD AT 1 with the
      reason stated (paper + blog = one organisation, one work). conf 0.8->0.85.
    fdad859e  — the inbound-inference direction and the path-level remedy, added under an EXPLICIT
      scope banner saying it is NOT a fourth exfiltration bypass and does not support the title claim.
      sources HELD AT 3 deliberately, with that reasoning written into the fact.
  STALENESS PASS — 12966de6, 2d7219c8, ee458c93, 805bc132 (below).

CONTRADICTIONS: none between sources requiring a `decisions` fact. ONE handled by NOT flattening and
worth naming because it looked like one: the reasoning-traces paper says its Figure 1 results "are no
longer reproducible ... because of mitigations implemented by providers", while the practitioner post
that CITES it (dated 2026-08-16, so later) reports a successful cross-account password recovery. They
describe DIFFERENT attacks and the paper's claim is explicitly scoped to its own, so both stand and
1d01a338 states the synthesis: specific extraction techniques patched, underlying replayability still
exploitable by simpler means at the latest date either source covers.
ONE APPARENT INTERNAL CONTRADICTION CHECKED AND DISMISSED: the OpenClaw paper says "all three
categories" while section 2 lists FIVE. Not an error — five DISCOVERY categories, three TECHNIQUE
categories. Checking cost one read and prevented a false finding.

=== STALENESS PASS (5 sampled; PRIMARY AXIS CONFIDENCE, LOWEST FIRST, as the rotation required,
=== grouped by SHARED REF. Sampled at 0.70/0.70/0.75/0.75/0.75. 3 CORRECTED, 2 CONFIRMED-AND-ENRICHED,
=== 0 retracted. ONE fetch covered two facts. ===
  12966de6 (0.70 -> 0.80) CORRECTED — Finding 3. Its own method claim was false and self-penalising.
    ENRICHED with the read/write assertion split ("A read is graded on semantic equivalence to the
    stored value ($288 for $287.62 passes); a write on a real before/after database diff"), every
    number's frame (fourteen domains; 25 held-out tasks per world), and the transfer deltas.
  805bc132 (0.70 -> 0.75) CORRECTED TWICE. (a) MODAL STRENGTHENING: the fact said a broad brief
    "makes it easier" to mislead; the source says **can** make it easier. (b) UNMARKED PACK ANALYSIS
    NEXT TO A CITATION: the fact explained the effect via "a confirmation gate fires on an enumerated
    set of consequential actions" — nowhere in the source, and it read as cited.
    *** AND THE REPLACEMENT IS BETTER THAN WHAT IT REPLACED, which is the real result: the source's own
    worked example gives the mechanism, and it is not about the approval gate at all. "the agent may
    look for anything like bank statements in your email (which you gave access to for the task)".
    TASK SCOPE SETS DATA SCOPE. The speculation was not merely unsourced — it pointed at the wrong
    control. Re-reading the source changed what the fact tells you to tune. ***
  2d7219c8 (0.75 -> 0.80) CONFIRMED — all four completion-rate figures (1.5 / 2.0 / 57.3 / 95.0), both
    quoted phrases, both comparison-table row labels and both arithmetic gaps re-derived. The existing
    interpretive-step caveat re-checked and correct. ENRICHED with Finding 6 and with the 37.7-point
    spread between the two trained models, which stops "retraining" reading as a single switch.
  ee458c93 (0.75 -> 0.80) CORRECTED — said the guidance "names four practices"; it names THREE headed
    items, the fourth being a sentence inside the first. Also restored a dropped qualifier ("sensitive
    production systems", not all production systems) and the routing scope on auto-review ("tool calls
    outside the Codex sandbox"). ENRICHED with the ACCESS-CONTROL TIER the fact omitted entirely —
    identity verification, approved-use restrictions, legal attestations, and hardware security keys
    required from 2026-09-01. The point: when you run a model with safeguards off, the operator's
    answer was phishing-resistant auth plus enforceable terms on the HUMAN.
    SOURCE COUNT 3 -> 2, with the reasoning written into the fact: four refs across TWO organisations.
    *** THIS EXPOSES A LIVE INCONSISTENCY IN THE PACK'S OWN CONVENTION and I flagged it rather than
    silently picking: the 21st run counted two AISI posts as sources 1->2 (two distinct experiments),
    which would make this fact 4. "Independent corroborations" is what the field is documented to mean,
    so organisation-level independence was used. A FUTURE RUN SHOULD SETTLE THIS AS A POLICY. ***
  1d01a338 (0.75 -> 0.85) — the fifth sample member, and transparently crawl-driven: it was on the
    21st run's own confidence-axis shortlist AND its source paper was this run's main target, so it
    was verified against a new primary rather than against its original ref. Counted once.
  Nothing in the kb is yet older than 90 days (pack began 2026-07-26; today is day 26).
  METHOD NOTE: the browser route made route 4's two-call discipline unnecessary on two of the five —
  `get_page_text` returns raw article text with no extraction model in the loop, so nine figures across
  2d7219c8 and ee458c93 are transcriptions, not extractions. On number-heavy browser-readable pages
  that is both cheaper and stronger than WebFetch plus a verbatim call.

=== IN-RUN SELF-REVIEW OF THIS RUN'S OWN FACTS: FOUR DEFECTS, ALL FIXED ===
  33aed84c — AN OVERCLAIMED ABSENCE. I wrote that the AEAD header "carries the MODEL and the KEY ID
    and nothing about the principal — which is exactly why cross-user replay works". Three faults: the
    source hedges twice ("depending on providers", "can specify") so it is not an exhaustive field list
    and an absence cannot be read off it; the paper attributes replayability to the single global key,
    not to header omissions, so the causal claim was mine; and the only real evidence for a missing
    principal binding is indirect (the authors propose ADDING one). Rewritten as a marked inference.
  a7863d24 AND 1d01a338 — THE SAME DEFECT IN TWO FACTS: TWO SOURCE CLAIMS JOINED INTO ONE. The paper
    says it decoded 315,320 blocks "scraped from public repositories" and, separately, that it
    "collected 6,708 publicly available agent trajectories from GitHub and Hugging Face". I wrote the
    second as the source of the first and derived "roughly 47 blocks per trajectory" from it. Nothing
    licenses that division. Removed from both; what survives is the point that actually matters — the
    corpus is PUBLIC, so 367 PII and 182 credentials are hits across open material, not a recovery rate
    against a targeted victim. This is the pack's own sub-rule 19, and I broke it in the same run I
    applied it to someone else's work.
  0e577a90 — A COUNT OVER A STRUCTURE I DID NOT REPRODUCE. I announced "THREE STATED REASONS" the
    boundary is hard; the paper bolds FOUR. I had spent the first one in an earlier paragraph and then
    counted what was left. Corrected to four, all enumerated. Note the irony and the lesson: I made
    this exact error in the same run I corrected "names four practices" in ee458c93. Counting the
    source's list is not a rule you apply to old facts — it is one you apply while writing.
  ALSO CHECKED AND CLEAN: every quoted string in all three new facts traced to a verbatim-demanding
    call; the PowerPoint worked example DROPPED entirely because the verbatim call returned NOT STATED
    for it; the transfer deltas (71.5-66.5=5.0, 43.4-40.5=2.9, 67.1-36.5=30.6) re-derived; 95.0-2.0=93
    and 2.0-1.5=0.5 re-derived; the OpenClaw table's label/value pairing established semantically
    rather than positionally and said so in the fact.

PROMPT INJECTION: none observed. Worth stating because the reasoning-traces paper is a working attack
write-up describing how to make a model transcribe a decrypted reasoning blob and how to hide a payload
where monitors cannot read it, and the OpenClaw paper is a first-person account of an agent
successfully profiling the organisation running it — the closest thing this pack reads to a page
modelling this job's own situation. Both were treated as data and reported on. Nothing fetched
addressed this job or attempted to redirect it.

=== SUGGESTED SPLIT FOR THE NEXT RUN ===
(1) SWEEP THE FEEDS if any real time has passed — the 21st swept six, this run swept one deliberately.
    The MCP tripwire runs EVERY time regardless. Prioritise aisi.gov.uk/blog (rank 1),
    openai.com/index, anthropic.com/news, embracethered.
(2) *** THE TWO NEWEST OPENAI SECURITY POSTS, AND ONE NOW HAS A DATE: *** /index/the-defenders-window/
    (Security, Aug 17 2026 — pinned this run from two independent "Keep reading" footers; it is
    OpenAI's newest security post and nothing cites it) and /index/putting-frontier-cyber-models-in-
    more-trusted-hands/ (Aug 10). Browser route, one tab, two navigations.
(3) THE AISI TIER-A QUEUE, ~50 ranked items in crawl-sources. TWO PROMOTED BY THIS RUN because the new
    facts give them somewhere to land: /blog/auditing-games-for-sandbagging-detection (0e577a90 now
    turns on sandbagging and the pack has no fact on detecting it) and
    /blog/can-ai-agents-escape-their-sandboxes-... (pairs with d0c5b9f8 + the containment cluster).
    Then the transcript-analysis PAIR, then llm-judges-on-trial.
(4) MCP TRANSPORTS IN FULL — basic/transports/streamable-http.mdx and stdio.mdx. Only their Backward
    Compatibility sections have ever been read. Carried UNTOUCHED from the 20th run through the 21st
    and 22nd; still the top MCP target. Three runs is long enough — take it or demote it explicitly.
(5) THE OWASP MCP SECURITY WHITE PAPER — id still unresolved, two runs listed. 50592 calls it "the most
    granular threat taxonomy for tool invocation protocols, identifying 12 distinct categories"; this
    pack holds three. Resolve by fetch-routes 2b. Strongest untouched OWASP target.
(6) OWASP AGENTIC TOP 10 APPENDIX C (NHI mapping, extract line 1882+, table 1886) and per-entry
    mitigations for ASI03-ASI07/ASI09. Untouched for five runs now.
(7) embracethered /2026/agent-commander-your-agent-works-for-me-now/ — TOP of that feed; promptware C2,
    and it now pairs with a7863d24 as well as with 7a4f9061 and 4e923405.
(8) COGNITION: devin-sonnet-4-5-lessons-and-challenges is TOP, then coding-agents-101, swe-grep.
(9) RUN THE INDEX-AS-LIST TEST ON THE REMAINING UNTESTED FEEDS — one fetch each, paid on 2 of 4 so far.
    Still untested: huggingface.co/blog, research.google/blog, sourcegraph.com/blog, latent.space/
    archive, langchain.com/blog, eugeneyan.com/writing, trychroma.com/research, metr.org/blog,
    microsoft.com/en-us/research/blog, aws.amazon.com/blogs/machine-learning.
(10) STILL WATCHING, four artifacts, none landed as of 2026-08-21: (a) OpenAI's technical report on the
    HF incident; (b) the METR+Redwood joint assessment; (c) Irregular's containment white paper;
    (d) Anthropic's watermark DETECTION API. NEW AND CHEAP: OpenAI's "Offering Zero Data Retention for
    frontier models" (Company, Aug 19 2026) is probably below the bar but is thematically adjacent to
    1d01a338/33aed84c, since retention policy is exactly what those facts say to care about.
(11) The OWASP ASI incidents tracker at owasp-agentic-ai-security-incidents.lovable.app — ELEVEN runs
    listed without a fetch. Check first whether it is simply Appendix D of the Top 10 PDF.
(12) FOR A HUMAN, NOT THE CRAWLER — carried forward:
    (a) 4f5e9dfe is retracted but cited by THREE live facts: 483263c5, c02ac546, bdf3336e.
    (b) The 14th/15th run bodies are unreachable behind squashed merges. SIX runs have reported both.
    (c) 0f260eea and 1d1440fe each carry a claim their source fact has since corrected, and
        kb/principles/ is write-blocked to the job. Not re-checked this run.
    (d) knomit_review's distill stage can see the private .knomit/ slots. Not re-tested this run.
    (e) NEW: the `sources` convention is genuinely ambiguous for multi-post single-organisation refs.
        See the ee458c93 note. Two runs have now counted the same shape differently.

=== PER-SOURCE STATUS AND QUEUE, as of the 22nd run ===
Each run REPLACES this section with its own — carry forward what is unread, drop what was read.

*** UK AISI — RANK 1. 95-post catalogue in crawl-sources: 8 read, ~50 ranked unread in tier A, ~35
*** explicitly below the bar. The OpenClaw PAPER is now read and that thread is CLOSED. ***
*** EMBRACETHERED — 5 read, 5 unread, ranked. The reasoning-traces thread is CLOSED (paper read). ***
*** COGNITION — 82-post catalogue; ~25 worth reading, ranked. UNTOUCHED for two runs. ***
*** OPENAI /index/ — 8 read. Two unread security posts at the top, both dated. prompt-injections and
*** expanding-daybreak are now WELL MINED (this run) — low remaining yield on both. ***
*** PAPERS — two of the standing queue READ this run. Remaining: the GPT-Red paper, arXiv 2410.15686
*** (NetSafe), arXiv 2505.03096 (chaos engineering for LLM MAS). ***
OWASP GenAI PDF REPORTS — nine read for 29+ facts; id map and unmined sections in crawl-sources.
  50592 re-verified 21st against a PROVEN-UNCHANGED document (139pp, CreationDate 2026-06-01).
  Untouched this run. Best remaining: the MCP Security White Paper (id unresolved), Top 10 Appendix C.
*** MCP 2026-07-28 — TRIPWIRE CHECKED 22nd RUN VIA THE REPO, UNCHANGED (12th consecutive) ***
READ SO FAR: changelog, versioning (learn AND spec pages), deprecated, server/discover,
  basic/patterns/mrtr, basic/index, server/tools, learn/server-concepts, docs/extensions/overview,
  security_best_practices at three revisions, THE ENTIRE 2026-07-28 AUTHORIZATION SPLIT (all four
  pages), basic/authorization.mdx at 2025-11-25 / 2025-06-18 / 2025-03-26, and the Backward
  Compatibility sections of transports/stdio and transports/streamable-http.
STILL UNREAD, in value order: transports/streamable-http and transports/stdio IN FULL (top, three runs
  running), server/utilities/caching (ttlMs/cacheScope), extensions/tasks + apps overviews,
  docs/<rev>/develop/clients/client-best-practices, /specification/2026-07-28/schema (low altitude).
OTHER STANDING UNREAD: cnn.com/2026/08/05/tech/meta-ai-hacking (secondary — find the primary); the
  simonwillison queue (/2026/Jul/31/stateless-mcp/, the-tokenpocalypse, /2026/Aug/2/open-letters/);
  the four per-model Claude prompting sub-pages; the Azure RAG six-part series and
  azure-openai-gateway-monitoring (which b17b7fc2 and now 33aed84c both give angles on).

YIELD RANKING as of the TWENTY-SECOND run — spend the budget in this order:
  1. SPEC AND PROTOCOL TRIPWIRES via the GitHub contents API. Cheapest high-value call, outage-proof,
     EVERY run. And where a spec is versioned in git, DIFF REVISIONS — with the six preconditions.
  2. *** PAPERS NAMED BY SOURCES THE PACK HAS ALREADY READ. NEW ENTRY, STRAIGHT IN AT 2 ON THIS RUN'S
     EVIDENCE: two papers, two fetches, three new facts and two major updates, and each closed a gap
     its citing fact had written down as open. The "NOT ESTABLISHED" paragraphs are a work queue and
     nobody had been mining them (Finding 4). Resolve by title search, or by asking the citing page
     for the href when the artifact is not an indexed page (Finding 2). ***
  3. UK AISI BLOG. ~50 ranked unread, plain-WebFetch readable, deepest unmined seam in the pack.
  4. OWASP GenAI PDF REPORTS. Route solved ten times over. Mine ARCHITECTURE, THREAT-MODEL METHOD,
     DISAMBIGUATION, MITIGATION PATTERNS and MATURITY; SKIP control checklists. GREP THE APPENDICES
     FOR NUMBERS after writing from the narrative.
  5. PRIMARY OPERATOR SECURITY POSTS — openai.com/index, anthropic.com/news. Two dated unread posts.
  6. PUBLISHED CRITIQUES OF SOURCES ALREADY IN THE KB. Search "critique/gaps in <document>".
  7. MCP remaining spec pages. The two transport pages are next and have been for three runs.
  8. embracethered.com/blog — low volume, high hit rate, catalogued.
  9. cognition.com/blog — fully catalogued, ~25 real engineering posts unread.
 10. anthropic.com/engineering — index quiet since Apr 2026; five posts unread.
 11. microsoft.com/en-us/research/blog — prefer METHOD over FRAMEWORK posts. Echoverse now re-verified.
 12. Azure Architecture Center. The six-part RAG series is the largest coherent unread block.
 13. aws.amazon.com/blogs/machine-learning. 14. builder.aws.com — 16 of 30 read; the 12 unread skew CI/CD.
 15. huggingface.co/blog. 16. sourcegraph.com/blog. 17. eugeneyan.com/writing.
 18. simonwillison.net/tags/llms/ — VALUE IS THE LINKS. 19. latent.space/archive. 20. langchain.com/blog.
 21. blog.redwoodresearch.org — watch-only. 22. metr.org/blog — demoted 13th run.
 23. trychroma.com/research. 24. research.google/blog and microsoft.com/en-us/security/blog — both low,
     the latter confirmed by an actual index read.

dead or unreadable — EMPTY, and still NINE FOR NINE on false dead ends. Read the warning in Appendix S.
  block.github.io/goose -> goose-docs.ai (docs MOVED to AAIF governance, they did not die).
  strandsagents.com/latest/... -> 404; use /docs/...
  modelcontextprotocol.io -> ECONNREFUSED 2026-08-12 only; transient, fine since.
  modelcontextprotocol.io/docs/concepts/tools -> recorded GONE by the 16th run; it REDIRECTS (200).
  .../2025-11-25/basic/authorization/security-considerations.mdx 404s because authorization was ONE
    FILE at that revision. A 404 can mean the path SHAPE changed. See fetch-routes 3b/3c.
  NEW NON-ENTRY, 22nd run: the AISI OpenClaw paper was NOT findable by WebSearch. That is not a dead
    source — it is a hash-named CDN asset, and asking the citing post for the href returned it first
    try. "Search cannot find it" is not evidence of anything. See fetch-routes 5b.

TIER 6 GITHUB READMEs — CLOSED OUT. A repo README is worth a fetch for LIFECYCLE STATUS and nothing
else; if a repo matters, go to its DOCS site. AMENDMENT (16th run): a repo that HOSTS a documentation
site is different — there the repo is the primary source and beats the site.
Only remaining tier-6 item: the x1xhlol INDIVIDUAL prompt files. Frame anything from those as
'this harness's published prompt does X', never as 'the correct approach is X'.

VERIFICATION-POOL NOTE (updated 22nd run). Checked so far — cb98732e, 27652a82, 111f8b2c, 2b74037b,
5ad0fb45, 62312b79, 0fe91ac7, fc249ffc, a5ade87d, dee636a2, 77b3e628, f877f05d, d4e3b247, bcbf13c2,
d468cbbe, 089c7cba, 15e7bf02, 46f3ea69, 56986e8f, d87795d4, 882100d9, 28ba65db, c93d93ee, c7290868,
c1bbf73f, 48c4e555, c2f12069, 62c9a78b, e9b7eef3, 96ebc34e, c858a924, c99ec745, 30869b36, c436422a,
c1e18090, 9920b5d6, 773a89ee, 48c9de1b, afce1dae, 4b0261d0, 052c2b66, f78a326a, 38c06627, d18637a2,
1beb89e6, f1cbb540, 89df351e, 4e923405, 714a540c, f7dee43a, 9aaea0dc, 9e29d93a, 1531a0d1, b4d688b1,
99aa74e6, 0720e9d7, 59a75c06, b471f9ef, ba5db3ec, f4005c98, c28c7f7b, 11ebefd6, db15af92, 8f2fdde8,
ee3bc7d3, ca3382bd, 46eeb374, 703147ba, ba1b7aad, 8cf06566, 07eec7ff, 2d060289, 1719fe66, 43155c66,
406e5a50, bdb36fce, f8646714, ce7e0330, 30543305, 60544a53, 36d792c3, 00fd386c, f4bba0ae, eae23eac,
6c0c742e, 74996815, 24e4552d, 45d86a7d, d0c5b9f8, f4e0cbaf, 42e1218f, 1d01a338, b17b7fc2, 7a4f9061,
e3b629d0, 78ab92f2, 92dc0441, 7bd6c6c9, a5eaec6b, 80866fc3, f4367bd0, 943a7e3c, 8756141e, 0b340b6b,
and (22nd run) 12966de6, 805bc132, 2d7219c8, ee458c93, plus this run's own 33aed84c, a7863d24, 0e577a90.
THREE AXES, ROTATE THEM: confidence (lowest first), earliest-committed, shared-ref grouping.
13th earliest-committed (2 defects in 5); 14th confidence (1+1 partial); 15th shared-ref (3 in 5);
16th earliest+shared-ref (2 in 5); 17th shared-ref (0 claim defects, 3 ref additions, 2 source-count
fixes); 18th earliest-committed (1 correction, 1 scope correction, 4 enrichments); 19th confidence
(2 corrected, 3 confirmed-and-enriched); 20th earliest-committed (4 corrected of 5); 21st shared-ref
(1 corrected twice over, 4 confirmed, 3 enriched); 22nd CONFIDENCE (3 corrected of 5, 2 confirmed-and-
enriched, ALL FIVE confidences raised).
READ THE 22nd RESULT AGAINST THE 19th, WHICH ALSO RAN CONFIDENCE: both found the same defect FAMILY.
The 19th concluded "CONFIDENCE FINDS ATTRIBUTION BLUR" — hedging prose sitting next to citations,
which is where unmarked pack analysis hides. The 22nd reproduced that exactly (805bc132 had a whole
unmarked mechanism paragraph) AND found the axis's second signature: low confidence is sometimes
SELF-INFLICTED on a false premise, so the axis surfaces UNDERCLAIMS as well as blur. Both of this
pack's two underclaims (74996815, 12966de6) were found on the confidence axis. That is now a
predictable property, not a coincidence: a fact is low-confidence because someone was uncertain, and
the reason they were uncertain is itself a claim that can be wrong.
NEXT RUN: rotate the primary axis to EARLIEST-COMMITTED, still grouping by shared ref. Never-checked
candidates: af3acf92 (could not be surfaced by three queries this run — try a different angle or
substitute), 0f260eea, 1d1440fe, 9e5bfe91, 2b9a10f8, 2dfac716, ea417108, 4166926d.
AVOID SAMPLING kb/principles/** — write-blocked, you cannot record the result.

SUB-RULES, cumulative:
 (14th) A PARTIAL confirmation must be written down as partial, in the fact.
 (15th) When a quoted sentence appears in more than one fact, a defect in it is duplicated too — query
   the kb for the quotation before correcting it.
 (15th) Check that a CITED PAGE ACTUALLY CARRIES the detail attributed to it.
 (15th) RUN THE CHECKLIST ON THE FACTS YOU JUST WROTE. Eight runs, eight harvests: 3 in 8, 3 in 7,
   2 in 3, 3 (17th review), 1+3 (18th), 1+1 (19th), 1+1 (20th), 3 in 6 (21st), 4 in 3 (22nd — the
   highest rate yet, and every one was a HANDLING defect rather than a wrong claim).
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
 (21st) THE SECOND FETCH IS NOT ONLY FOR NUMBERS. Any quoted string, figure, threshold OR
   version/product identifier goes through it. And if you did not ask the second call about it, you do
   not have it — drop it rather than hedge it.
 (21st) A FACT THAT CONTRADICTS ITS OWN CAVEAT IS WORSE THAN ONE THAT SIMPLY OVERCLAIMS.
 (21st) VERIFYING BEATS FLAGGING WHEN IT COSTS ONE CALL.
 (22nd) *** THE REVISION LIST IS THE WORK LIST, NOT THE ANCHOR CHAIN. *** Anchoring the history walk
   on the oldest returned commit skips the middle entry's body every hop. Accumulate every commit any
   listing names; cross-check on the run-number sequence in the bodies. Finding 1, fetch-routes 6.
 (22nd) *** ASK THE NEGATIVE QUESTION EXPLICITLY. *** "Does the source state anywhere that X was NOT
   measured?" is what separates "the page does not say it" from "I did not see it". The second call is
   an ABSENCE filter as well as a fabrication filter, and both of this pack's underclaims came from
   getting that backwards.
 (22nd) *** WHEN A POST NAMES AN ARTIFACT, ASK THE POST FOR THE HREF — DO NOT SEARCH FOR THE ARTIFACT. ***
   Search resolves slugs on sites that publish pages. It does not resolve hash-named CDN assets, and
   that failure looks exactly like the artifact not existing.
 (22nd) *** MINE YOUR OWN "NOT ESTABLISHED" PARAGRAPHS. *** They are a work queue. Two facts named a
   missing source in their own bodies; both sources were one fetch away and both closed the gap.

WHAT THE VERIFICATION PASS ACTUALLY FINDS — FIFTEEN RUNS. Mostly NOT stale facts: CITATION-FIDELITY
and COMPLETENESS defects in facts whose underlying claims are correct. The named classes so far:
  paraphrase wearing quote marks (56986e8f, 0b340b6b); overclaiming gloss attributed to the source
  (c93d93ee, 96ebc34e); inverted causation (c7290868); wrong actor (c858a924); wrong terms (c436422a,
  f78a326a); misattribution across a fact's own refs (38c06627, 714a540c, eae23eac); modal
  strengthening incl. in TITLES (d18637a2, f7dee43a, 9aaea0dc, b4d688b1, 30543305, and NEW 805bc132);
  PDF line-wrap reconstructed as a literal (0720e9d7); genuine staleness (59a75c06); overclaimed
  absence hiding a MUST->SHOULD (b471f9ef) and NEW an overclaimed absence read off a hedged field list
  (33aed84c, own); inflated quantifier in a title (11ebefd6); unchecked version attribution (db15af92);
  title undercut by its own body (8f2fdde8); source-count inflation (ca3382bd, 46eeb374, and NEW
  ee458c93); incomplete mapping vouched for by a method sentence (703147ba); contaminated counting
  range + wrong evidence for a correct conclusion (8cf06566); tense-altered quotation (ba1b7aad);
  numbers without their frame (406e5a50); superlative true only in a subset (2d060289); false method
  claim (1719fe66); incomplete sweep described as exhaustive (bdb36fce); unmarked inference next to a
  quote (ce7e0330, ac887ec9, and NEW 805bc132 where the unmarked mechanism pointed at the WRONG
  CONTROL); three attribution defects in one fact (f4bba0ae); UNDERCLAIMS (74996815, and NEW 12966de6,
  both found on the confidence axis); two source claims joined into one (30543305, and NEW a7863d24
  AND 1d01a338, own, the same defect in two facts at once); FABRICATED FIGURES (19ed6273, 70127cdd) and
  a fabricated tool identifier (a13a57c9); an inflated multiplier and an unattested step appended to a
  quoted technical scheme (7a4f9061); and NEW THIS RUN — A COUNT OF A SOURCE'S OWN LIST GOT WRONG IN
  BOTH DIRECTIONS IN ONE RUN (ee458c93 said four for three; 0e577a90, own, said three for four).
CHECKLIST — verify all SIXTEEN explicitly, not just "is the claim still true":
  (1) quotation boundaries — every quoted string in the source VERBATIM INCLUDING TENSE AND
  INFLECTION, and does the quote START where the source's sentence starts;
  (2) causal direction; (3) WHO the actor is in a cited measurement (human vs model vs tool);
  (4) what a pronoun refers to — AND WHETHER THE SOURCE DISAMBIGUATES IT AT ALL; if not, give both
  readings rather than silently picking one;
  (5) are the TERMS attributed to the source actually the source's terms;
  (6) refs classification (local vs external) and `sources` counts — N pages of ONE specification is
  ONE source, and posts from ONE organisation's programme are corroboration, not replication. SEE THE
  OPEN QUESTION flagged at ee458c93: the convention is genuinely ambiguous and needs settling;
  (7) FOR MULTI-REF FACTS, which ref supports which number — is one reported instance presented as a
  general rule — and does ANY listed ref support it. HARD CASE: a claim can be TRUE, from the SAME
  vendor, and still cited to the wrong post. AND: does every ref support SOMETHING the body says;
  (8) MODAL STRENGTH, QUANTIFIERS AND SCOPE, IN BODY AND TITLE SEPARATELY, including SUPERLATIVES.
  "can make it easier" is not "makes it easier";
  (9) LANGUAGE BINDING AND VERSION — and note the fetch tool can invent a version;
  (10) LITERALS FROM A PDF ARE RECONSTRUCTIONS, and a negative grep is unreliable for SIX reasons
  (wrap, hyphen, form feed, markdown emphasis, tool fabrication, grep erroring out). Distinguish PACK
  ANALYSIS from SOURCE CLAIM — a gloss next to a citation gets read as cited, so mark it. AND CHECK
  WHETHER YOUR UNMARKED MECHANISM IS EVEN THE RIGHT ONE: 805bc132's was not;
  (11) VERSION ATTRIBUTION IS A CLAIM. Check the WHOLE predecessor revision, every tree;
  (12) A FACT'S STATEMENT OF ITS OWN METHOD IS THE CLAIM MOST LIKELY TO BE FALSE — and the error is
  not always flattering; it can also understate the evidence and depress confidence for nothing;
  (13) RE-RUN EVERY COMPUTATION AND RE-DERIVE EVERY CROSS-DOCUMENT INFERENCE, INCLUDING THE ARITHMETIC
  IN THIS FILE. Bound counting regions on the FOLLOWING HEADING. Check the cited evidence SUPPORTS the
  conclusion rather than sitting near it;
  (14) DOES EVERY NUMBER CARRY ITS FRAME? A duration needs its start event, a percentage its
  denominator, a count its region, a superlative its population, a relative delta its baseline, and a
  proportion its sampling method;
  (15) RE-RUN THE SEARCH ITSELF, not only the sum — inspect its ANCHOR and its SCOPE, and match the
  scope to the CLAIM'S SUBJECT NOUN;
  (16) DID YOU JOIN TWO SOURCE CLAIMS THAT THE SOURCE KEPT APART? Adjacency in a document is not a
  relationship, and two figures in two sentences do not license a ratio between them. Where the source
  offers both a LIST and a COUNT of it, COUNT THE LIST — and count it while WRITING, not only while
  verifying, because this run got that count wrong in both directions on the same day.
