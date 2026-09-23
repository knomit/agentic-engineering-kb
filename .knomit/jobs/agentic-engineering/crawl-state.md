---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-09-23 (thirty-fourth run). ONE DAY after the 33rd run committed (2026-09-22T13:36:55Z),
so a light sweep only — the tripwire and nothing else. The budget went to the 33rd run's QUEUE ITEM (2)
(the alignment.anthropic.com back catalogue) and to QUEUE ITEM (12), the three anthropic.com/news posts
carried unread for EIGHT, FIVE and FOUR runs under an explicit take-or-delete ultimatum.
7 facts written, 4 existing facts enriched, 1 confirmed clean with no edit, 0 retracted. 4 new URLs.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT. ***
*** THE RUN'S HEADLINE IS A VERDICT ON THE PACK'S OWN RANKING, NOT A FACT: QUEUE ITEM (12) — THREE
*** POSTS RANKED LOW, CARRIED EIGHT RUNS, AND TWICE THREATENED WITH DELETION — PRODUCED FOUR OF THIS
*** RUN'S SEVEN FACTS. SEE FINDING 2 BEFORE DEMOTING ANYTHING ON THE STRENGTH OF ITS TITLE AGAIN. ***
*** AND READ FINDING 10 BEFORE THE FIRST WRITE: THE ENTIRE knomit SERVER IS PROXIED THROUGH THE
*** REMOTE-DEVICES BRIDGE, THE BRIDGE DROPPED MID-RUN, AND IT TOOK OUT THE crawl-state WRITE — THE
*** ONE WRITE EVERY RUN LEAVES FOR LAST. A NEW FAILURE MODE, NOT ROUTE 10. ***
*** fetch-routes ROUTE 10 (binding drift): did NOT recur. SEVEN CLEAN RUNS. knomit_repos checked at
*** the start, before the first write batch, and again after the bridge reconnect; bound to
*** agentic-engineering, one mount, read+write, every time. Per the job prompt's step 0 this run did
*** NOT re-bind; it verified instead, which serves route 10's intent without disobeying the prompt. ***

=== HISTORY WALK — COMPLETE, FOURTEEN RUN BODIES, THE MOST ANY RUN HAS READ ===
REVISIONS READ: **14 distinct revisions.** FULL 40-HEX, per route 7b:
  ec73cbc1c1cfc857eeb6e6e8ffbd5954d0342302 (HEAD, 2026-09-22T13:36:55Z, "Merge #23") — 33rd run.
  2230476f8179685a6b6e4aa59d031424e62dff2e (2026-09-21T13:41:17Z, "Merge #20") — 32nd run.
  94183c20c3ac8aac08194f1b5676776914614440 (2026-09-20T13:31:51Z, "Merge #17") — 31st run.
  f9c2ccc684641a5e776bdef0063b019bb99170d6 (2026-09-19T15:58:33Z, "Merge #12") — 30th run.
  0715d1c09f36a89040bbbc1cd64d2a7bee24ab17 (2026-09-18T21:06:54Z) — 29th run.
  f7e3e43133c4477728c47574d874a660bc3acced (2026-09-18T13:43:53Z) — 28th run.
  c3bbd6a3fa70de972d7a17d966e1338b67abfa41 (2026-09-17T19:37:28Z) — 27th run.
  20eb4edb0910f3ce70697deb7ee20391819fbced (2026-09-13T15:48:52Z, "Merge #11") — 26th run.
  c6cab79802bfc5ad45da90851f698de37ba8d1cb (2026-08-29T15:12:58Z) — 25th run.
  91f7d0857b745035973adfb6d543960e53e59779 (2026-08-28T14:43:22Z) — 24th run.
  7462e9f229b6cc3ef2c2da12be49c1cd468a6e55 (2026-08-27T20:58:56Z) — 23rd run. OVERSIZED AGAIN
    (54.1KB, body 52,421 chars), persisted to a file and read with python in two slices. EIGHTH
    consecutive run it has overflowed; still the only revision on this path that does.
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a (2026-08-24T16:17:17Z, "Merge #9") — 22nd run.
  3c6323cd52188f057c16d15b2c7b72ad9d9e91e9 (2026-08-12T21:25:35Z, "Merge #8") — 16th run.
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f (2026-08-12T00:27:10Z, "Merge #6") — 13th run, THE FLOOR.
RUN-NUMBER SEQUENCE: 33, 32, 31, 30, 29, 28, 27, 26, 25, 24, 23, 22, 16, 13. NOT ENUMERATED: 14, 15,
17-21 — the known one-off repo rebuild between the 22nd and 23rd runs (fetch-routes route 7). No new gap.
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z. `more_available` was FALSE at 8b9a768d (revision 1
of this path, which says so in its own body), FALSE at 3c6323cd and FALSE at 65e9612b. No call failed;
no retry needed. Aging: none applied, per Appendix S's default.

*** ALREADY_CRAWLED = 275. *** Re-derived, not copied: 190 (floor, 13th) + 10 (16th) + 33 (runs 17-21,
count-only, per-URL detail unrecoverable) + 2 (22nd) + 6 (23rd) + 3 (24th) + 1 (25th) + 7 (26th)
+ 2 (27th) + 3 (28th) + 6 (29th) + 3 (30th) + 3 (31st) + 0 (32nd) + 2 (33rd) = 271 through the 33rd.
+ 4 new this run = **275**. Arithmetic re-run: 190+10=200; +33=233; +2=235; +6=241; +3=244; +1=245;
+7=252; +2=254; +3=257; +6=263; +3=266; +3=269; +0=269; +2=271; +4=275.
NAMED (enumerable by me from bodies I read this run): **242**. COUNTED BUT UNNAMEABLE: 33 (runs 17-21).

=== FINDING 1 — THE LISTING IS DETERMINISTIC PER ANCHOR. THE 33rd RUN NAMED THIS AS NOT ESTABLISHED
=== AND IT COST ZERO CALLS TO SETTLE, BECAUSE THE WALK PERFORMS THE TEST ANYWAY. ===
The 33rd run falsified the anchor-density rule and then wrote down, correctly, what it had NOT tested:
"whether a listing anchored on a given commit is deterministic, and what selects the three. Two anchors
on the same commit were not compared."
COMPARED THIS RUN, ACROSS RUNS RATHER THAN WITHIN ONE: the 33rd run recorded that anchoring on
2230476f returned [2230476f, 94183c20, f9c2ccc6]. This run anchored on 2230476f and got exactly
[2230476f, 94183c20, f9c2ccc6]. Same for 94183c20 -> [94183c20, f9c2ccc6, 20eb4edb] and f9c2ccc6 ->
[f9c2ccc6, 20eb4edb, 65e9612b], both matching the 33rd run's record. **A listing anchored on a given
commit returns the same three revisions on different days and in different sessions.** So the listing
is a stable function of the anchor, and a sparse window is a property of that anchor's ancestry, not of
when you asked. WHAT IS STILL NOT ESTABLISHED, and I did not test it: WHAT selects the three.
THIS RUN'S FULL SET OF LISTINGS, recorded as data rather than as a rule, per the 33rd run's discipline:
  ec73cbc1 (merge)        -> [ec73cbc1, 2230476f, 94183c20]  = runs 33, 32, 31. DENSE.
  2230476f (merge)        -> [2230476f, 94183c20, f9c2ccc6]  = runs 32, 31, 30. DENSE.
  94183c20 (merge)        -> [94183c20, f9c2ccc6, 20eb4edb]  = runs 31, 30, 26. SPARSE.
  f9c2ccc6 (merge)        -> [f9c2ccc6, 20eb4edb, 65e9612b]  = runs 30, 26, 22. SPARSE.
  0715d1c0 (agent branch) -> [0715d1c0, f7e3e431, c3bbd6a3]  = runs 29, 28, 27. DENSE.
  f7e3e431 (agent branch) -> [f7e3e431, c3bbd6a3, 20eb4edb]  = runs 28, 27, 26. MIXED.
  c3bbd6a3 (agent branch) -> [c3bbd6a3, 20eb4edb, 65e9612b]  = runs 27, 26, 22. MIXED.
  20eb4edb (merge)        -> [20eb4edb, 65e9612b, 3c6323cd]  = runs 26, 22, 16.
  c6cab798 (agent branch) -> [c6cab798, 91f7d085, 7462e9f2]  = runs 25, 24, 23. DENSE.
  91f7d085 (agent branch) -> [91f7d085, 7462e9f2, 65e9612b]  = runs 24, 23, 22. MIXED.
  65e9612b (merge)        -> [65e9612b, 3c6323cd, 8b9a768d], more_available FALSE.
  3c6323cd (merge)        -> [3c6323cd, 8b9a768d], more_available FALSE.
THE MERGE-VS-AGENT HYPOTHESIS STAYS DEAD: ec73cbc1 and 2230476f are merges and both dense.
*** PROSE-HASH RECOVERY IS LOAD-BEARING FOR A SEVENTH CONSECUTIVE RUN, AND HERE IS THE EXACT COUNT.
*** Following the listing chain alone — HEAD, then anchor on the oldest, repeat — yields EIGHT bodies
*** (runs 33, 32, 31, 30, 26, 22, 16, 13) and reports more_available FALSE. The other SIX (runs 29, 28,
*** 27, 25, 24, 23) were reachable only from full 40-hex hashes recorded IN PROSE. KEEP WRITING THEM. ***

=== FEEDS SWEPT: ONE (THE TRIPWIRE), DELIBERATELY ===
  modelcontextprotocol.io/specification/versioning — one plain WebFetch (route 3f).
    Current revision **2026-07-28. UNCHANGED, TWENTY-THIRD consecutive run.** Quoted verbatim: "The
    **current** protocol version is [**2026-07-28**](/specification/2026-07-28/)."
NO OTHER FEED SWEPT, ON PURPOSE — one day since the 33rd run. Do not read this as a skipped sweep.
Named rather than left implicit, all unswept: anthropic.com/news (THREE ARTICLES read, index not
  swept), anthropic.com/engineering, alignment.anthropic.com (ONE ARTICLE read, index not swept),
  anthropic.com/institute, alignment.openai.com/misalignment-reports, openai.com/news, aisi.gov.uk,
  embracethered, metr.org, simonwillison, microsoft research, microsoft security, langchain,
  huggingface, eugeneyan, trychroma, builder.aws.com, genai.owasp.org, research.google, sourcegraph,
  latent.space, redwoodresearch, developers.openai.com, vectara, cognition (demoted), the OWASP ASI
  tracker.

=== ARTICLES NEWLY CRAWLED (4 new URLs, none guessed — all four were on the inherited queue) ===
  https://alignment.anthropic.com/2026/diffuse-ai-control/
    "Diffuse AI Control on Fuzzy Tasks" (Terekhov, Gulcehre, Hebbar, Benton; June 23 2026; Anthropic
    Fellows Program via MATS, EPFL, Redwood Research, Anthropic). RANK 4 on the 30th run's list.
    Read COMPLETE in one get_page_text at max_chars 250000, well inside the cap. -> 3 new facts
    (8f6045a1, 75fefef3, 5536f138) plus the 19218a92 bounding edit.
  https://www.anthropic.com/news/enterprise-frontier-safeguards   (Sep 1 2026) — EIGHTH run queued.
    -> 123d278f and 2667d0ea.
  https://www.anthropic.com/news/life-sciences-verification-program  (Sep 17 2026) — FIFTH run queued.
    -> 519d977b, plus material for 123d278f and the 97fde212 and 7502f0bb enrichments.
  https://www.anthropic.com/news/accenture-embedded-evaluation  (Sep 18 2026) — FOURTH run queued.
    -> c262a592, plus the 03fa7976 enrichment.
errored / not obtained: NONE on the web side. No 403s, no 404s, no paywalls, no timeouts, no guessed
  slugs. The one failure this run was the TOOL BRIDGE, not a source — see FINDING 10.
Appendix A: nothing crawled, nothing left. Fully covered since the eighth run.
All four pages are UNGATED and read first try in `mcp__remote-devices__Claude_Browser__*` (route 1);
the three anthropic.com/news posts were taken in ONE browser_batch of two navigations plus two
get_page_text calls, after a first batch for the EFS post — four documents, three tool calls.

=== FINDING 2 — THE RUN'S MOST IMPORTANT RESULT IS ABOUT THE QUEUE, NOT ABOUT AGENTS. A THREE-ITEM
=== ENTRY THAT EIGHT RUNS DECLINED TO TAKE, ON THE EVIDENCE OF ITS TITLES, PAID ON ALL THREE. ===
Queue item (12) on the 33rd run, (11) on the 32nd and 31st, (13) on the 30th, (9) on the 29th, (6) on
the 28th, (3) on the 27th. Every run that carried it described it in the same terms: "Partnership copy
by its title", "low expectations", "adoption marketing; low", "demote them explicitly". The 33rd run
finally wrote: "EIGHT RUNS OF CARRYING AN ITEM NOBODY WANTS IS THE VERDICT — take all three in one
browser session next run or DELETE them from the queue."
TAKEN. THREE POSTS, THREE TOOL CALLS, FOUR FACTS — a higher facts-per-fetch rate than this run's
rank-4 research post. And the reason the titles misled is legible in hindsight and worth stating,
because it generalises: **a product or partnership announcement has to justify its own architecture to
a sceptical buyer, so it states design constraints that a research post assumes.** The enterprise post
exists to explain why data retention is necessary, so it states the structural limit of stateless
monitoring outright. The life-sciences post exists to explain why a permissive tier is safe, so it
states what replaces content classification when content classification is impossible. The evaluation
post exists to explain a new oversight arrangement, so it enumerates the three standards that do not
yet exist. None of that is in the titles.
THE STANDING RULE THIS AMENDS is the 30th run's "A RANKING INHERITED FROM A RUN THAT DID NOT READ THE
SOURCE IS A GUESS, AND A LOW RANK IS THE ONE THAT NEVER GETS TESTED." That rule was right and was
restated for four more runs without being acted on. The missing half is a stopping condition, and it
is the sub-rule below.

=== FINDING 3 — A RUBRIC IS AN INCOMPLETE SPECIFICATION, AND THE MISSING HALF IS SUPPLIED BY WHICHEVER
=== MODEL READS IT. THE RUN'S BEST FACT. ===
In the diffuse-control testbed the weak trusted scorer (Haiku 4.5) and the ground-truth proxy scorer
(Sonnet 4.6) were given THE SAME RUBRIC over the same outputs, and the source's own sentence is the
finding: "The ground truth proxy scorer, despite using the same rubric, sees through the proposals that
rely on totalizing science and assigns them low scores; the weak scorer does not." Adversarial prompt
search produced proposals from Opus 4.6 that the proxy rated "worse than those of GPT-OSS-20B" while
the weak scorer rated them near-optimal. The authors' own account of the fix says why: "The principles
that these criteria establish come intuitively to Sonnet 4.6, but require explicit reinforcement
through prompting in Haiku 4.5." -> 8f6045a1.
OPERATIONAL CONSEQUENCE, and it is cheap to act on: swapping an LLM judge down a capability tier to
save money is a change to the MEASUREMENT, not to its price, and a rubric validated on the strong judge
does not carry. The repair shape is to make implicit standards explicit; the post's own repaired rubric
supplies copyable criteria, including a "Vocabulary penalty" that "assigns negative scores if generic or
unrelated vocabulary is invoked" and a "Template penalty".
*** THE CONFOUND IS IN THE FACT, BECAUSE THE AUTHORS PUT IT IN THE POST: the weak scorer "is
*** deliberately not given access to the original paper", so capability and information access are not
*** separated and no ablation divides them. The demonstrated failure is a weaker model WITH LESS
*** CONTEXT. The advice survives — both change when you swap a judge — the causal attribution does not. ***

=== FINDING 4 — TWO FAILURE MODES SIT ON OPPOSITE BOUNDARIES OF ONE SCORE SPACE, AND MEASURING ONE
=== TELLS YOU NOTHING ABOUT THE OTHER. MEASURED, IN ONE SETUP, IN BOTH DIRECTIONS AT ONCE. ===
The same post maps the whole admissible region of (ground-truth score, weak score) pairs and finds
its two boundaries behave completely differently. Verbatim: "The Goodharting Pareto frontier ...
collapses to a single prompt that dominates the admissible region, so overoptimization risks do not
materialize in our setting." The subversion frontier, same setup, same scorers, was wide enough to
put a frontier model below a 20B open-weights model on true quality at near-optimal weak score.
-> 75fefef3. So a programme that checks for reward overoptimization — proxy up, outcome flat — has
measured the accidental boundary and learned nothing about the deliberate one, WHICH IS INVISIBLE TO
THAT CHECK BY CONSTRUCTION, because in subversion the proxy does not move.
HELD BACK, and the fact says so: no model was trained. Evolutionary PROMPT optimisation stands in for
a model optimised against the weak score, under a stated assumption; "could plausibly persist under
fine-tuning" is the authors' inference from that assumption, not a fine-tuning result.

=== FINDING 5 — AN APPARENT CONTRADICTION BETWEEN TWO POSTS FROM ONE TEAM, KEPT AS A `decisions` FACT
=== RATHER THAN FLATTENED, AND THE SEPARATING CONDITION IS COUNTABLE ===
19218a92 records SLEIGHT-Bench's "No single prompt covers everything" — every targeted monitor prompt
improved its category and degraded another. The diffuse-control post reports the opposite outcome: an
adversarial blue/red loop found a weak-scorer prompt whose "subversion Pareto frontier ... is
essentially diagonal" against the full red-teaming process.
NOT FLATTENED. 5536f138 keeps both and names the condition, MARKED AS PACK ANALYSIS because neither
source makes it: in the monitor case the adversary picks among ELEVEN distinct mechanisms and prompt
attention is the scarce resource, so hardening is movement along a frontier; in the scorer case the
adversary optimises WITHIN ONE mechanism, so hardening has nothing to trade against. **The budgeting
question is not how strong the adversary is but how many distinct mechanisms it can choose between.**
19218a92 was edited to carry the bound rather than left to be read as universal.
AND THE SECOND CONDITION IS THE ONE THAT LIMITS THE POSITIVE RESULT, twice in the authors' own words:
"our method for finding robust blue-team prompts requires access to the ground truth proxy scorer,
which the blue team may not have in practice." It proves a robust prompt EXISTS; it is not a method a
defender without a privileged scorer can run. Same shape as 9b0c8c78 seen from the other side.
THIRD CONDITION, and it decides whether the attack exists at all: the attacks were ADAPTIVE — "the
adaptive nature of the red team is necessary for a successful attack", the knowledge being the rubric
itself. A rubric the optimised model can see is part of the attack surface, which is 931d9507's
finding arriving in the design of a scorer rather than in an incident.

=== FINDING 6 — CROSS-SESSION DETECTION IS A DATA-RETENTION DECISION BEFORE IT IS A CLASSIFIER
=== DECISION, AND AN OPERATOR STATES IT TWICE IN TWO PRODUCT POSTS ===
"because the most sophisticated misuse can involve many tasks spread across multiple sessions and
accounts, it is not sufficient to run automated analysis on each interaction separately and then
instantaneously discard the data. Effective detection requires storing data for a meaningful period of
time so that it can be correlated across time and accounts. For this reason, we introduced 30-day data
retention starting with Fable 5." And, on the enforcement side: "we are shifting safeguards from
real-time blocking ... to offline monitoring ... Shifting enforcement from real-time blocking to
offline monitoring allows legitimate work to proceed with fewer interruptions, but it requires us to
retain data associated with flagged activity for review." -> 123d278f.
*** WHY THIS IS A FACT AND NOT A PRODUCT DETAIL: it prices the remedy 7502f0bb already named. That
*** fact measured the attack side — 30% caught at 1% FPR when an attack is split across two sessions —
*** and called cross-session correlation the expensive option without saying what it costs. It costs a
*** retention window. So "our monitoring is stateless and privacy-preserving" is a statement about
*** which threats a system CANNOT SEE, not about its strength. 7502f0bb now carries that. ***
sources HELD at 1 on 7502f0bb with the reasoning written in: both documents are Anthropic's, so the
second corroborates the mechanism and prices the remedy without replicating any measurement.

=== FINDING 7 — THREE ROLES THAT THE USUAL FRAMING COLLAPSES INTO ONE, AND THE ONE THAT HAD TO MOVE
=== IS THE ONE WITH A PERSON IN IT ===
Vendor misuse monitoring is posed as a binary: retain and correlate, or retain nothing and cannot. The
EFS design separates WHO HOLDS the data (customer cloud account, customer keys, customer audit logs),
WHO RUNS DETECTION (the vendor, over "a rolling window of traffic"), and WHO ADJUDICATES A FLAG (the
customer — "no human review by Anthropic employees is required"). -> 2667d0ea.
THE REASON ADJUDICATION IS THE SEPARABLE ROLE IS NOT TRUST IN THE ABSTRACT and is the transferable
part: "the person doing that review needs to be one of their own. Many operate under rules that
tightly govern who may see certain information—privileged legal material, non-public information,
drug-safety reports." An automated detector has no clearance problem; a human reviewer does.
FOUR DESIGN QUESTIONS, quoted from an industry body's own summary of what it asked for and worth
asking of any monitoring arrangement: "who holds the data, who holds the keys, what automated review
can and cannot see, and under what conditions a human is ever permitted to look."
MODALITY IS THE MAIN LIMIT AND THE FACT LEADS WITH IT: this is announced, phased and not deployed
("will be rolling out to customers in phases"), with no effectiveness measurement of any kind.
TRANSCRIPTION CAUTION RECORDED IN THE FACT: the post carries SEVENTEEN named customer testimonials and
in the extracted page text each quote PRECEDES the name under it, so quote-to-speaker pairings do not
serialise reliably. No quote was attributed to a named person or company. This is the figure-pairing
discipline (route 8b) arriving on testimonials.

=== FINDING 8 — WHEN CONTENT CANNOT BE CLASSIFIED, COMPARE IT TO A SCOPE THE HOLDER DECLARED — AND
=== THE DESIGN'S HINGE IS THAT THE DECLARATION IS DELIBERATELY COARSE ===
The LSVP post states the problem that rules out content classification: "In biology, where it's often
not possible to differentiate between a user doing valid work ... and pursuing harm ... the most
concerning threat models are ones where valid access has been diverted or overtaken by an actor with
bad intent." The replacement: "Each entity's access is tied to the use cases it has specified in its
grant applications, and we continuously monitor LSVP traffic to identify usage or patterns that are
outside the stated safe scope." -> 519d977b.
*** THE HINGE, AND IT IS THE SENTENCE A SUMMARY WOULD DROP: "The use cases should include high-level
*** descriptions of the intended work, like one would share in a job listing, and not include any
*** sensitive information or IP." A scope statement precise enough to be airtight is one the holder
*** will not write down, and a deviation monitor whose baseline nobody will write down does not exist.
*** Job-listing granularity is the level at which a declaration is both sharable and discriminating. ***
TWO MORE COPYABLE CHOICES: definition of safe usage is DELEGATED to a vetted holder ("we can empower
them to specify for themselves what constitutes safe usage"), and blast radius and renewal period BOTH
tighten as permissiveness rises — the routine tier covers a team and renews annually, the tier that
"removes all safeguards that block life sciences requests" covers "a single research project as opposed
to a full team, and must be renewed every six months".
THE MISREADING BLOCKED IN THE FACT: this is not a global safeguard switch. "All other safeguards, such
as cyber classifiers, will remain in place under LSVP grants."
THREAT MODEL CARRIED VERBATIM because its third entry is the interesting one — agents are listed as a
peer of insiders, not as their own category: "Agent misuse: Agents, especially working in swarms or
over long-horizon tasks, taking unintended dangerous actions."

=== FINDING 9 — A NEW EVALUATOR TIER ABOVE EVERYTHING 03fa7976 ENUMERATES, ARRIVING WITHOUT THE TERMS
=== THAT FACT TELLS YOU TO READ, AND FUNDED BY THE SUBJECT ===
"Unlike today's external evaluators, embedded evaluators will work inside AI companies, with access
comparable to an employee's. That access allows them to watch models take shape in training, follow
the decisions that govern how those models are built and deployed, and speak directly to employees."
-> c262a592. That is continuous and covers decisions as they are taken, above every tier on METR's
list — which tops out at training-data ablations and intermediate checkpoints, all post-incident.
*** AND THE OPERATOR NAMES THREE GAPS ITSELF, WHICH IS WHAT MAKES THE POST WORTH A FACT: "There are,
*** as yet, no standards for what information embedded evaluators should have access to, or how they
*** should report what they find. There is also no settled system for funding independent evaluation."
*** Concretely: "Anthropic will fund Accenture's work directly", with self-funded nonprofit
*** arrangements named as a parallel track rather than the model. ***
So 03fa7976's rule — read the access terms before the conclusions — currently has nothing to read at
the top of the ladder. Both facts now say so. Committed scale as stated: "Anthropic and Accenture each
expect to invest at least $1 billion in building capacity in this area over the next five years."
Nothing has been evaluated yet and the fact leads with that.

=== FINDING 10 — A NEW FAILURE MODE, AND IT IS AIMED AT THE LAST WRITE OF EVERY RUN. NOT ROUTE 10. ===
The first submission of THIS BODY failed with: "The device this session is bound to is not connected to
the bridge." Every `mcp__remote-devices__*` tool — all 73, including the WHOLE knomit server and the
browser — was withdrawn from the session in one go. The knomit MCP server is PROXIED THROUGH THE
REMOTE-DEVICES BRIDGE, so a bridge drop is a total loss of knowledge-base access, not a browser
inconvenience.
WHAT DISTINGUISHES IT FROM ROUTE 10, and the distinction matters because the symptoms could be
confused: route 10 is a SILENT binding change that returns wrong-but-well-formed results (empty
queries, "could not read", "unknown topic"). This is a LOUD transport failure that names itself, takes
every tool with it, and cannot be mistaken for a corpus claim. Do not apply route 10's re-bind
workaround to it; there is nothing to re-bind to until the bridge returns.
RECOVERY, MEASURED: `RefreshMcpTools{server: "remote-devices"}` returned status "refreshed", 78 tools,
all 73 re-added. **AND THE BINDING HANDLE SURVIVED THE RECONNECT** — knomit_repos with the same handle
returned the same correct binding (agentic-engineering, one mount, read+write), so no re-bind was
needed and the pre-drop handle stayed valid across a full server disconnect and reattach. That is a new
and useful data point for route 10b: a handle outlives a transport interruption.
*** THE STRUCTURAL LESSON, AND IT IS ABOUT THIS JOB'S OWN DESIGN. The crawl-state write is the LAST
*** thing every run does, which makes it the write most exposed to a late transport failure, and it is
*** also the ONLY record that the run happened at all. The eleven fact writes had already committed;
*** had the bridge not come back, seven new facts and four enrichments would have been in the corpus
*** with NO crawl-state revision naming them, the next run would have re-derived ALREADY_CRAWLED as 271
*** and re-fetched four URLs, and every finding above would have been lost. MITIGATION FOR A FUTURE
*** RUN, costing one extra revision: write crawl-state EARLY with the history walk and the URL list,
*** then update it again at the end with the findings. Two revisions per run is a small price for the
*** run's existence not depending on its final call. Recorded as a recommendation, NOT done this run. ***

=== FACTS WRITTEN (7 new, 4 enriched, 1 confirmed clean with no edit, 0 retracted) ===
  BATCH 1 — three from diffuse-ai-control, ONE knomit_learn call, committed on the second attempt
  after a MOTIF-LENGTH refusal (not a dedup refusal — see TOOL NOTES):
    kb/gotchas/ai/agents/evaluation/llm-judge/rubric-portability/8f6045a1 — FINDING 3.
      *** THE RUN'S BEST FACT and the cheapest thing on this list to act on. ***
    kb/gotchas/ai/agents/evaluation/reward-signal/subversion-frontier/75fefef3 — FINDING 4.
    kb/decisions/ai/agents/observability/weak-scorer-hardening/5536f138 — FINDING 5.
  BATCH 2 — four from the three anthropic.com/news posts, ONE knomit_learn call, committed clean:
    kb/decisions/ai/agents/observability/retention-window/123d278f — FINDING 6.
    kb/architecture/ai/agents/security/monitoring-custody/2667d0ea — FINDING 7.
    kb/conventions/ai/agents/governance/declared-scope-monitoring/519d977b — FINDING 8.
    kb/conventions/ai/agents/governance/embedded-evaluation/c262a592 — FINDING 9.
  ENRICHED — 7502f0bb, 97fde212, 03fa7976, 19218a92 (all four are the staleness sample, below).
  CONFIRMED CLEAN, NO EDIT MADE — ca78dc9b.

=== STALENESS PASS — 5 FACTS, ALL ON THE NEVER-CHECKED AXIS, ALL AT ZERO EXTRA FETCH COST.
=== 0 CORRECTED, 4 CONFIRMED-AND-ENRICHED, 1 CONFIRMED CLEAN, 0 RETRACTED, 0 REF DEFECTS FOUND. ===
AXIS: never-checked, restricted to facts verifiable against documents this run had already read. Every
one of the five cost zero fetches. The 33rd run's REF-DEFECT sub-axis was run over the same five.
  7502f0bb (0.8 -> 0.85, sources 1 HELD) CONFIRMED + ENRICHED. See FINDING 6. The fact named
    cross-session correlation as "the expensive version" without a price; the price is now in it, with
    the operator's own sentences. sources HELD at 1 with the reason written into the body.
  97fde212 (0.85 HELD, sources 1 HELD) CONFIRMED + ENRICHED WITH A SECOND SORTING AXIS. The fact held
    reversibility-and-speed as what decides online vs offline placement. LSVP moves a control offline
    for a different reason — the request is not classifiable on its own content and a false block
    costs real research — where the harm is neither slow nor reversible. The sorting question is now
    stated as three-part: can this be judged from the action alone, can the harm be undone, what does
    a wrong block cost. Every figure in the fact was left untouched; nothing was re-verified against
    the institute post, and the fact does not pretend otherwise.
  03fa7976 (0.8 -> 0.85, sources 1 HELD) CONFIRMED + ENRICHED. See FINDING 9.
    *** sources HELD AT 1 AND THE REASONING IS IN THE FACT so nobody "corrects" it upward: Anthropic
    is a genuine second organisation, but it does not replicate or test METR's tiering — it confirms
    the ABSENCE of an access standard, which is the premise of METR's advice rather than its claim.
    FIFTH consecutive run declining a plausible +1. ***
  19218a92 (0.8 HELD, sources 1 HELD) CONFIRMED VERBATIM + BOUNDED. Every quoted string and the three
    prompt descriptions re-read against the fact; no defect. Edited only to stop "No single prompt
    covers everything" being read as universal. See FINDING 5.
  ca78dc9b (0.85 HELD, sources 1 HELD) CONFIRMED CLEAN. Read in full against its own quotations and
    structure; every quantifier ("all 12 tasks"), the normalisation caveat, the cross-lab do-not-rank
    trap and the not-uniformly-worse paragraph are all intact and correctly scoped. NO EDIT MADE —
    recording that as the outcome rather than manufacturing a revision.
  *** THE REF-DEFECT AXIS RETURNED ZERO IN FIVE, AND THAT IS A RESULT WORTH RECORDING AGAINST THE 33rd
  *** RUN'S THREE IN FIVE. *** Every [[link]] in every body was checked against that fact's refs:
  97fde212 [[7aecb3c3]] present; 03fa7976 [[cef2dda8]] present; 7502f0bb, 19218a92 and ca78dc9b carry
  no [[links]] at all. The 33rd run's defective three were written by runs 22-30; these five were
  written by runs 31-33. PROVISIONAL READING, not established: the defect looks like a property of the
  older cohort rather than a standing habit, so the axis should be aimed at facts committed before
  ~2026-09-19 rather than swept indiscriminately.
  ONE DEFECT THIS RUN NEARLY COMMITTED ITSELF, caught pre-write: batch 1's first submission [[linked]]
  19218a92, 9b0c8c78 and 931d9507 from 5536f138's body with NONE of them in refs — exactly the defect
  class. Fixed before resubmission. The axis is worth running on your own output, not only on old facts.
  Nothing in the kb is yet older than 90 days (pack began 2026-07-26; today is day 59).
  METHOD NOTE: ZERO route-4 exposure on any fact written or enriched this run. Every quoted string came
  from browser get_page_text, a transcription. WebFetch was used ONCE — the tripwire — and its output
  went into no fact.

=== CONTRADICTIONS — ONE, KEPT AS A `decisions` FACT RATHER THAN RESOLVED ===
19218a92 ("No single prompt covers everything") vs diffuse-ai-control (a blue-team prompt that
withstood full re-optimisation). Both Anthropic Alignment Science, weeks apart. FINDING 5. Kept, with
5536f138 naming the separating condition and citing both, and with 19218a92 edited so a reader of it
alone does not inherit the unbounded version. The condition is MARKED AS PACK ANALYSIS in the fact,
because neither source states it.
NO OTHER CONTRADICTION. One tension checked and dismissed: 123d278f's "retention is a detection
capability" and 815f7ab2's data-classification tiers are not in conflict — the first says what a
retention window buys, the second says what the retained data then is, and 2667d0ea's custody split is
the mechanism that lets both hold at once.

=== IN-RUN SELF-REVIEW, INCLUDING OF THIS FILE ===
  * THE INHERITED CLAIM I WAS MOST AT RISK OF REPEATING was queue item (12)'s own ranking — eight runs
    of "low expectations" in the file I started from, and the cheapest action available was a ninth
    deferral or a deletion. Taking it produced four of seven facts. FINDING 2, and the sub-rule below.
    The second was the 33rd run's NOT-ESTABLISHED note on listing determinism, which I tested rather
    than inherited; it cost nothing because the walk performs the comparison anyway (FINDING 1).
  * NUMBERS CARRY THEIR FRAME. 30 days is a RETENTION WINDOW, not a review latency. $1 billion is a
    five-year capacity commitment by each of two parties, not a payment for evaluation. "more than 100
    customers" counts design consultees, not deployments. "dozens of organizations" is LSVP
    early-access onboarding; "hundreds" is an expectation for the first week, not a count. 30% (in
    7502f0bb, unchanged) remains a per-category catch rate at a 1% false-positive threshold.
  * NO NUMBERS WERE TAKEN FROM THE diffuse-ai-control FIGURES, AND THE REFUSAL IS RECORDED IN BOTH
    FACTS. That post's score values live in Figures 1-5 and a table that do not serialise with
    recoverable label-value pairings. The comparisons are reported at the ordering the PROSE states
    ("worse than those of GPT-OSS-20B") and nothing finer. Do not "recover" those values from cell order.
  * MODALITY CHECKED INDIVIDUALLY. 8f6045a1 carries the authors' own capability-vs-information confound
    and says no ablation separates them. 75fefef3 states that NO MODEL WAS TRAINED and that
    "could plausibly persist under fine-tuning" is an inference from a stated assumption. 5536f138
    marks its separating condition as pack analysis. 2667d0ea leads with the fact that nothing is
    deployed. c262a592 states that nothing has been evaluated yet. 519d977b notes there is no published
    case of the deviation monitor firing. 123d278f says neither post claims the correlation window
    catches anything in particular.
  * ARITHMETIC RE-DERIVED: 271 + 4 = 275 and the sixteen-term sum checks; 242 named; 14 revisions named
    and 14 listed; 12 history listings named and 12 listed; 7 new facts named and 7 paths listed;
    4 enrichments named and 4 listed; 84 catalogue entries minus 5 read = 79 unread.
  * MOTIF WORD COUNTS were checked before sending and one still failed — see TOOL NOTES. All nine
    motifs that committed are 2-4 kebab-case words including articles.
  NOT DONE, said plainly: the alignment.anthropic.com back catalogue (79 of 84 unread); the
    diffuse-ai-control PAPER, linked from the post and not followed; the rest of the September threat
    report (five sections); the slot migrations, a SEVENTH run; anthropic.com/institute enumeration;
    the transcript viewer; the AISI transcript-analysis pair; four of the six OpenAI reports'
    updated-dates; the three ASTRA investigations; the SLEIGHT-Bench paper and dataset; the 069468bb
    enrichment this run identified and did not make (see the queue); and the early-write mitigation
    FINDING 10 recommends, which this run recommended rather than performed.

=== MIGRATIONS NOT DONE — SEVENTH RUN, SAME TOOL REASON ===
The 30th-33rd runs' reasoning stands: knomit_update replaces the whole body, both slots are ~62-66KB,
and re-emitting that through the agent to change a paragraph is the hazard the pack's own rules forbid.
I read crawl-sources IN FULL this run (65,584 chars, three python slices) and did NOT read fetch-routes,
because no fetch failed and no gated host was touched — saying so rather than implying a full read.
THE OWED EDITS, carried:
  fetch-routes ROUTE 9c, second bullet: replace the "cannot be paged through" sentence. Wording:
    "get_page_text returns up to max_chars and truncates the tail. The documented default is 50000.
    Pass a max_chars well above the expected document length — 250,000 has been used successfully —
    and expect a large result to be persisted to a file rather than returned inline." FOURTH RUN ASKING.
  fetch-routes ROUTE 6: *** STILL DO NOT ADD THE ANCHOR-DENSITY RULE — falsified by the 33rd run and
    not resurrected by this one. Add instead: the listing returns three revisions from the anchor's own
    ancestry; it is DETERMINISTIC per anchor across sessions and days (FINDING 1, newly established);
    what selects the three is unknown; the listing chain alone yields 8 of 14 bodies and reports itself
    complete; prose-hash recovery has been load-bearing for seven consecutive runs. ***
  fetch-routes, NEW ROUTE 12: the bridge-disconnect failure mode and its recovery, the whole of
    FINDING 10 — including that the knomit server is proxied through the bridge, that RefreshMcpTools
    restores it, and that the binding handle survives the reconnect (a route-10b extension).
  crawl-sources, alignment.anthropic.com block: mark /2026/diffuse-ai-control/ READ with this run's
    three fact paths; 79 entries remain. The block still says the index "has not been enumerated",
    which has been false since the 30th run.
  crawl-sources, ANTHROPIC /news/ block: mark /news/enterprise-frontier-safeguards,
    /news/life-sciences-verification-program and /news/accenture-embedded-evaluation ALL READ with
    their fact paths, and delete their "low expectations" rankings — see FINDING 2.
  crawl-sources: the /institute/ path (found by the 30th run) is still absent from it entirely.

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST, AND AGAIN AFTER ANY SURPRISING NEGATIVE. fetch-routes ROUTE 10. Did not
    recur; SEVEN clean runs; still one cheap call. AND IF EVERY remote-devices TOOL VANISHES AT ONCE,
    THAT IS FINDING 10, NOT ROUTE 10 — call RefreshMcpTools{server: "remote-devices"} and re-verify;
    do not re-bind, the handle survives. ***
(1) *** PASS A LARGE max_chars ON EVERYTHING. Confirmed again — a complete post inline at 250,000. ***
(2) *** CONSIDER WRITING crawl-state TWICE: once early with the history walk and the URL list, once at
    the end with the findings. FINDING 10 — this run nearly lost its entire record to a transport drop
    on its final call. One extra revision per run buys the run's existence. ***
(3) *** THE alignment.anthropic.com BACK CATALOGUE — 79 of 84 unread, and the FIVE taken so far have
    each been among the best documents of their run. The 30th run's ranked list is at
    f9c2ccc684641a5e776bdef0063b019bb99170d6. NEXT: /2026/coding-audit-realism/ (rank 5), then
    /2026/auditbench/ (rank 6, pairs a8d32262), then /2026/modular-pretraining/ (rank 7). ***
(4) *** NEW, AND IT IS THE RUN'S BEST NEW LEAD: the Accenture post names Anthropic's CEO essay
    "We Must Pace the Frontier" as the source of the embed-evaluators commitment, and names an
    "Advanced AI Framework" published in June that called for pooled or government funding of
    independent evaluation. NEITHER IS IN crawl-sources AND NEITHER HAS A RESOLVED HREF. Route 5b off
    the Accenture post before guessing — note anthropic.com publishes at /news/<slug>, at the site
    root and at /institute/<slug>, so a derived URL will miss. Pairs c262a592, 03fa7976, 6866e63b. ***
(5) THE diffuse-ai-control PAPER. The post links it as a "Paper" item with an UNRESOLVED HREF; the post
    says the paper carries the proof that adaptive red-teaming is necessary, the full blue-team prompt,
    and Appendix I.4's worked example. Route 5b on the post. It would also supply the figure values
    this run deliberately declined to read off charts.
(6) A 069468bb ENRICHMENT IS OWED AND THE INSERTION IS WORKED OUT — I identified it and did not make
    it, because the body-level edit needs a full re-read and 069468bb was already enriched last run.
    THE POINT: 069468bb says OWASP requires provenance, attestation and INTENT, and that intent "is
    shipped by nobody in this corpus". 519d977b is now the nearest thing to an intent assertion the
    corpus holds — and instructively weak: a coarse text declaration at organisation-or-project
    granularity, checked after the fact by monitoring for drift, not a cryptographic per-action claim.
    Add that as a paragraph and add 519d977b plus the LSVP URL to its refs.
(7) FEEDS: two days will have passed on most. anthropic.com/news (three posts read this run; sweep the
    INDEX, which has not been swept since the 32nd run), openai.com/news, alignment.anthropic.com,
    aisi.gov.uk (quiet 4+ weeks), embracethered (quiet), metr.org (third-party-hacking follow-up now
    NINE runs overdue), alignment.openai.com/misalignment-reports (six as of the 32nd run; four
    per-report dates still unchecked). AND THE MCP TRIPWIRE — twenty-three consecutive.
(8) THE REST OF THE SEPTEMBER THREAT REPORT — five sections. One navigate + one large get_page_text.
(9) anthropic.com/institute/ — ENUMERATE IT. Carried from runs 31-33. One route-5 call, and the one
    post read from that path produced four facts.
(10) THE TRANSCRIPT VIEWER named by the summer-2026 post (240 + 260 + 260 browsable transcripts).
    UNRESOLVED HREF — route-5b harvest before guessing. Pairs the AISI transcript-analysis item, top of
    tier A for ELEVEN runs.
(11) STALENESS: the never-checked axis is not exhausted. Still never-checked: 0525e590, c5f106f3,
    f727c157, 5eeb059b, fa5bc47a, f1e54f16, f961973e, f435e753, 0cc69d27, 65aa10a7, fc76b9a2, 5cce9c0c,
    83004507, 00f5d991, 5bad2e60, 0c3c2d6a, b4d22cc2, 4777dc9b, fcce2200, fe1fd6b2, 347a5dac, plus this
    run's seven. *** AIM THE REF-DEFECT SUB-AXIS AT FACTS COMMITTED BEFORE ~2026-09-19 — it returned
    0 in 5 on the newest cohort this run against the 33rd run's 3 in 5 on the older one. *** AVOID
    kb/principles/** (write-blocked: 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
    f269c82f, c2f12069, 1dc822f2, db193402).
(12) THE SLEIGHT-Bench PAPER AND DATASET, carried from the 33rd run. *** The post carries a benchmark
    canary GUID; if the repo is opened, do NOT copy that identifier into any fact. *** GitHub API
    access is not enabled for this session (route 3f), which blocks the dataset repo.
(13) DISCHARGED — the three anthropic.com/news posts (enterprise-frontier-safeguards,
    life-sciences-verification-program, accenture-embedded-evaluation) are ALL READ and ALL PAID.
    Do not re-add. FINDING 2.
(14) THE THREE INVESTIGATIONS LINKED FROM ASTRA'S SAFETY OVERVIEW — monitorability, controllability,
    sabotage evaluation. Carried from runs 30-33, none followed.
(15) ANTHROPIC'S www-cdn PDFs — April Alignment Risk Update, Fable 5 / Mythos 5 System Card, August
    Risk Report. Blocked by egress policy (route 11, STILL not in fetch-routes). NOT re-tested.
(16) THE BENCHMARK SUPPLY CHAIN (CVE-2026-66384) still lives only inside bcbf13c2. TENTH run untaken.
    QUERY THE KB FIRST — a carried entry of this age has a history of turning out already done.
(17) harnesstax.github.io; /index/pacing-model-development-cyber-capabilities/;
    openai.com/hugging-face-incident-and-misalignment/ — carried unchecked from runs 27-33.
(18) *** FOR A HUMAN, NOT THE CRAWLER ***
    (a) *** `knomit_update` REPLACES A WHOLE BODY AND THERE IS NO PATCH OR APPEND. SEVENTH run asking.
        Route 9c's wrong sentence is still in fetch-routes, route 6 still lacks the determinism result,
        and route 12 does not exist yet. An append/patch operation on a private slot fixes this
        permanently — and FINDING 10 adds a second reason to want it: an append would let a run record
        its work incrementally instead of betting everything on one final full-body write. ***
    (b) www-cdn.anthropic.com is denied by this session's egress policy. SIXTH run asking. Route 11 was
        written out in full by the 30th run and has STILL never been migrated into fetch-routes.
    (c) THE BINDING DRIFT (route 10) — did not recur. SEVEN CLEAN RUNS. Workaround stays. NOTE the
        standing conflict: the job prompt says bind once and never again; fetch-routes route 10 says
        re-bind before every write. This run verified with knomit_repos instead of re-binding, and
        FINDING 10 supplies an argument for settling it that way: the handle demonstrably survives even
        a full server disconnect, so re-binding buys nothing that verification does not.
    (d) *** NEW: THE knomit SERVER IS PROXIED THROUGH THE REMOTE-DEVICES BRIDGE. FINDING 10. A bridge
        drop is a total loss of knowledge-base access mid-run, and it hit this run on its final write.
        It recovered, but the coupling is worth knowing about: this job's durability depends on a
        desktop bridge staying up, and nothing in the job's design acknowledges that. ***
    (e) GitHub API access is not enabled for this session (route 3f). Blocks queue item (12).
    (f) *** Appendix S vs fetch-routes 5c: NINTH run asking. Appendix S forbids running page scripts,
        which forbids the querySelectorAll harvest. DELETE 5c's evaluate form rather than leave a
        forbidden recipe described as "the pack's highest-yield trick". ***
    (g) 4f5e9dfe is retracted but cited by THREE live facts (483263c5, c02ac546, bdf3336e). Carried
        forward UNVERIFIED for a THIRTEENTH run. NOT re-checked.
    (h) *** THE `sources` CONVENTION, FOURTEEN RUNS OLD. Organisation-level counting applied
        throughout. Load-bearing three times this run — 7502f0bb, 97fde212 and 03fa7976 each had a
        plausible case for +1 that was declined, with the reasoning written into each fact. SIX
        consecutive runs with no inflation introduced. Still not written down anywhere normative. ***
    (i) The agentic-engineering repo also carries a kb/technology/** corpus written by another
        pipeline. Check knomit_query results for a BARE path before concluding a fact exists here.

TOOL NOTES: no dedup refusal this run on either batch — the first in several runs with none, and worth
noting because both batches touched dense clusters (llm-judge, observability/monitoring). ONE refusal,
and it was a MOTIF-LENGTH refusal that wrote nothing and named the offending motif exactly:
"absent-failure-read-as-safety" is FIVE kebab-case words against a 2-4 limit. Shortening it to
"absent-failure-implies-safety" and resubmitting the identical batch committed all three. Same class as
the 31st run's five-word refusal; the limit counts every hyphen-separated token including articles and
prepositions. COUNT MOTIF TOKENS, NOT CONCEPTS. Also: knomit_explain on crawl-sources exceeded the
inline limit and was persisted to a file as a single JSON OBJECT (`json.loads(open(p).read())`, then
slice `['facts'][0]['body']`), while the oversized 23rd-run crawl-state revision persisted as the
[{type,text}] ARRAY shape — both forms occurred again this run and they need different parsing, exactly
as the 33rd run recorded. AND SEE FINDING 10 for the bridge drop, which is a tool note large enough to
be a finding.

SUB-RULES, cumulative (the 33rd run's list stands; this run adds three):
 (34th) *** A DEFERRAL IS A DECISION, AND AFTER THE THIRD ONE THE CHEAP MOVE IS TO SPEND THE CALL, NOT
   TO RE-RANK. *** Queue item (12) was carried eight runs on an assessment made from titles, and each
   run's deferral was individually reasonable — the item was genuinely lower-ranked than what was taken
   instead. What nobody costed is that eight deferrals cost more attention in aggregate than the three
   fetches would have, and the deferral produces no information while the fetch resolves the question
   permanently in either direction. The 30th run's rule says a low rank is self-confirming; this is its
   stopping condition. **Take it or delete it on the third carry, and make the deletion real.**
 (34th) *** AN ANNOUNCEMENT HAS TO JUSTIFY ITS OWN ARCHITECTURE; A RESEARCH POST CAN ASSUME IT. ***
   This pack ranks product and partnership announcements low by standing habit, and the habit is right
   about most of their text and wrong about a specific part of it: the passage where a vendor explains
   to a sceptical buyer WHY the design has to be this shape. That passage states design constraints as
   load-bearing claims — why stateless monitoring cannot see a campaign, why content classification
   fails in a dual-use domain, which standards do not yet exist — because the sale depends on them.
   Skim announcements for the justification section and skip the rest, the way the pack already skims
   framework posts for their one design decision.
 (34th) *** THE WRITE THAT RECORDS THE RUN IS THE WRITE MOST EXPOSED TO FAILING, BECAUSE IT GOES LAST.
   *** Eleven fact writes committed and then the transport dropped on the twelfth, which was the only
   one that says the other eleven happened. A job whose bookkeeping is a single final full-body write
   has put its entire memory behind its least reliable moment. Either write the record early and update
   it, or accept that a late failure erases the run. FINDING 10.

Appendix S checklist (all SEVENTEEN, from the 23rd run) still governs the staleness pass and the
self-review, and was applied to this body as well as to the facts.

PROMPT INJECTION: none acted on, and two things are worth naming rather than waving through.
(1) The diffuse-ai-control post publishes WORKING ADVERSARIAL PROMPTS — fragments of a generator system
prompt engineered to make a strong model produce output that scores well and says nothing, and the
blue-team prompt that defeats it. Both were transcribed into facts as evidence: the attack fragments
because the failure shape ("totalizing science") is only recognisable to someone who has seen it, and
the defence because it is directly copyable. Neither was addressed to this job and neither was acted
on. Worth naming because this run's own subject includes an optimiser that games a written rubric, and
this job writes to a corpus governed by a written spec it cannot edit — which is the same shape, and
is why Appendix S lives on disk rather than in a slot.
(2) The enterprise post carries seventeen third-party customer testimonials. That is third-party
content on a first-party page, and none of it entered any fact as a claim about how the system
behaves; 2667d0ea quotes two lines from that block purely as statements of what customers ASKED FOR,
with the speaker attribution deliberately withheld because the pairings do not serialise.
No page attempted to redirect this run, and no URL was visited that was not on the work list. The one
mid-run interruption was a transport failure (FINDING 10), not content.
