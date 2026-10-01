---
type: reference
domain: [agentic-engineering, job-state]
confidence: 1
sources: 0
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Last crawl state

crawled: 2026-10-01 (forty-third run, 13:17Z). 4 facts written, 3 enriched, 4 confirmed, 0 corrected,
0 retracted. 4 genuinely new URLs across 3 hosts. Back on the normal daily schedule (the 42nd run was an
off-schedule 22:25Z fire), so ~15h since the last run and ~23.5h since the last real feed sweep.
All three job slots written. crawl-state written ONCE, at the end — the 42nd run's self-imposed rule held.

*** THIS SLOT HOLDS ONE RUN. THE HISTORY IS THE RECORD. WALK IT BY THE PROSE HASHES BELOW, NOT BY
*** history.revisions (the API chain goes more_available:false several hops early, silently —
*** CONFIRMED A NINTH TIME: HEAD returned exactly 3 revisions with more_available:true, against 23
*** that exist). One revision = one run, except the 35th run's superseded insurance pair 474fbb13 /
*** 047c8878 (2026-09-24) and the 42nd run's two superseded intra-run writes be04dee3 / fc85537f
*** (2026-09-30) — do NOT count any of those four.
*** THE 40-HEX HASH LIST BELOW IS LOAD-BEARING INFRASTRUCTURE. Every run MUST reproduce its
*** predecessors' full hashes and append its predecessor's HEAD; the API cannot enumerate the history
*** and a single omission severs the chain permanently. This is the one non-optional thing in this
*** body. ***

*** ROUTE 10 (binding drift): did NOT recur. SIXTEEN CLEAN RUNS. knomit_repos called first (one mount,
*** agentic-engineering, read+write) and AGAIN immediately before the first write, with `bound.binding`
*** checked both times. Did NOT re-bind. No write or query behaved oddly. ***

=== HISTORY WALK — COMPLETE. 23 BODIES READ BY A READ-ONLY SUBAGENT, FIRST TRY, NO RETRIES. ===
Third consecutive run using the subagent method and the third clean result: the subagent was given the
prose-hash list and the protocol (read bodies at each commit; ignore history/diff entirely) and returned
all 23 bodies with ZERO failed calls and ZERO gaps. The two oversized bodies (34th, 23rd) were again read
from their persisted tool-result files. ~431k tokens and 48 tool calls inside the subagent; the main
context paid for a URL list and a report. KEEP DOING THIS — it is what buys the run its documents.
Run-number sequence, full 40-hex, newest first — REPRODUCE THIS LIST IN YOUR OWN REVISION AND APPEND
THIS RUN'S HEAD AS THE 43rd:
  9c0017f0a7e18fd89150c527b3627f903a19139e  2026-09-30T22:53:53Z  42nd (was HEAD at this run's start)
  76cc1a5d46d808fa757e3980ff30f2655746cf7e  2026-09-30T13:48:07Z  41st
  719ae8b25516d04ac8ab87d0175b754aa3adbee3  2026-09-29T13:52:31Z  40th
  375dc0f79ba2cc89b6482939b55ff377c36a6e0d  2026-09-28T13:50:17Z  39th
  092218eef959413b6ebf8589b29ecf5a37e5a49f  2026-09-27T13:40:18Z  38th
  7a39df486016fcd1dc19831a8675224b2bc9d447  2026-09-26T13:51:25Z  37th
  cc9be5500ab1e8e44c6bb1d7e9b300bf740c59d3  2026-09-25T13:48:57Z  36th
  474fbb130720d82633f55fd34050a1cfb7ab2514  2026-09-24T13:17:44Z  35th INSURANCE (superseded; NOT a run)
  68c341e16d1910c93c8bbf4c0489052f6d522230  2026-09-24T13:36:20Z  35th (final)
  66535f3fc655e3f79f1358c9d746645ca52e461d  2026-09-23T16:25:44Z  34th (oversized, persisted to file)
  ec73cbc1c1cfc857eeb6e6e8ffbd5954d0342302  2026-09-22T13:36:55Z  33rd
  2230476f8179685a6b6e4aa59d031424e62dff2e  2026-09-21T13:41:17Z  32nd
  94183c20c3ac8aac08194f1b5676776914614440  2026-09-20T13:31:51Z  31st
  f9c2ccc684641a5e776bdef0063b019bb99170d6  2026-09-19T15:58:33Z  30th
  0715d1c09f36a89040bbbc1cd64d2a7bee24ab17  2026-09-18T21:06:54Z  29th
  f7e3e43133c4477728c47574d874a660bc3acced  2026-09-18T13:43:53Z  28th
  c3bbd6a3fa70de972d7a17d966e1338b67abfa41  2026-09-17T19:37:28Z  27th
  20eb4edb0910f3ce70697deb7ee20391819fbced  2026-09-13T15:48:52Z  26th (body says crawled 2026-09-08)
  c6cab79802bfc5ad45da90851f698de37ba8d1cb  2026-08-29T15:12:58Z  25th
  91f7d0857b745035973adfb6d543960e53e59779  2026-08-28T14:43:22Z  24th
  7462e9f229b6cc3ef2c2da12be49c1cd468a6e55  2026-08-27T20:58:56Z  23rd (oversized, persisted to file)
  65e9612ba1295bd8d94dc19b4b12b62625f6a47a  2026-08-24T16:17:17Z  22nd (body says crawled 2026-08-21)
  3c6323cd52188f057c16d15b2c7b72ad9d9e91e9  2026-08-12T21:25:35Z  16th
  8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f  2026-08-12T00:27:10Z  13th — THE FLOOR (revision 1)
OLDEST COMMIT DATE REACHED: 2026-08-12T00:27:10Z (its body says the run crawled 2026-08-10).
The walk terminates because the FLOOR is reached, not because more_available went false — the API's
more_available is not the stop condition and was not consulted. NO CALL FAILED. GAP: runs 14, 15 and
17-21 have no revision (one-off repo rebuild between the 22nd and 23rd) — the SAME known gap, NO NEW GAP.
The subagent independently re-counted the floor's legacy block at EXACTLY 190 entries, agreeing with runs
22-42, and counted 277 distinct scheme-bearing http(s) URLs across all 23 bodies.

*** TWO COUNTERS, BOTH CORRECT, MEASURING DIFFERENT THINGS — state both, do not reconcile them away:
*** (a) THE JOB COUNTER: ALREADY_CRAWLED = 294 through the 42nd run; this run adds 4 -> 298.
***     It includes 33 count-only URLs from runs 17-21 whose per-URL detail died in the rebuild.
*** (b) NAMEABLE URLS: 277 through the 42nd (the 41st's figure was 269; this run's subagent counted
***     every scheme-bearing URL in every body, including queue, dead-list and tool-note mentions,
***     which is a slightly wider rule than the 41st used) -> 281 with this run's four.
*** NEITHER IS A RECORD OF WHAT HAS BEEN READ. The corpus's refs are. See FINDING 1. ***
The 16th-run floor inconsistency (e61629fc / 197 URLs vs 8b9a768d / 190) is UNCHANGED and still not
chased. Nothing turns on it. Do not lose it either.

=== TRIPWIRE ===
  modelcontextprotocol.io/specification/versioning — one WebFetch. Current revision **2026-07-28,
    UNCHANGED, THIRTY-SECOND consecutive run.** Verbatim: "The **current** protocol version is
    [**2026-07-28**]". Do NOT cite 2025-11-25 or 2025-06-18.
  *** AND IT PAID FOR THREE STALENESS CHECKS AT ZERO EXTRA COST — see the staleness pass. The tripwire
  page is the ref behind three live facts, so reading it IS re-verifying them. Future runs: when the
  tripwire comes back, spend thirty seconds checking it against the facts that cite it. ***

=== ARTICLES NEWLY CRAWLED (4 new URLs, 3 hosts) ===
  https://deploymentsafety.openai.com/gpt-6-astra/safeguards  — SECTION 8 (Alignment), the 42nd run's
    RANK 1 and the part it could not reach. Taken by NEW ROUTE 22 (section-targeted WebFetch), three
    calls, after nine runs of this section being unread. Four of the run's five knowledge outputs came
    from it. Section 9 (Preparedness) STILL TRUNCATED on all three calls.
  https://deploymentsafety.openai.com/  — the index, never enumerated. 8 entries, one plain WebFetch.
    Catalogue now in crawl-sources. KEY FINDING: /gpt-6-astra and /gpt-6-astra/safeguards are DIFFERENT
    DOCUMENTS and the parent card has never been read.
  https://embracethered.com/blog/posts/2025/the-normalization-of-deviance-in-ai/  — rated TOP OF 2025 by
    the 23rd run; the rating was right. Plain WebFetch, ungated, two-call verbatim, both calls agreed.
  https://www.anthropic.com/news  — index sweep, date-windowed since 2026-09-17. Quiet.
  RE-READ, not new: modelcontextprotocol.io/specification/versioning (tripwire + 3 staleness checks).
  No 404, no paywall, no gate, no slug guessed, no source errored, nothing recorded as dead.
  Appendix A: nothing crawled, nothing left — fully covered.

=== FACTS WRITTEN (4 new, 3 enriched, 4 confirmed, 0 corrected, 0 retracted) ===
  NEW, from the Astra safeguards card section 8 (one knomit_learn call, ACCEPTED FIRST TRY — no motif
  rejection, no subject-overlap refusal; motif words counted before submitting and a mechanism-phrased
  query run for each candidate, which is the 42nd run's recipe and it has now worked twice):
    kb/conventions/ai/agents/evaluation/construction-order/8992ec34.md — three Astra evaluations disclose
      construction-after-training inline, per evaluation; the honeypot one additionally discloses the
      NEGATIVE ("We did not construct honeypot training environments specifically to target this
      evaluation"). The fact's load-bearing move is separating the two disclosures — you can satisfy the
      first and violate the second by writing the eval last and the targeted training environments first.
    kb/conventions/ai/agents/evaluation/cot-labelling/0cbaa443.md — Verbalized Metagaming vs Oversight
      Gaming, with the conjunction intact: oversight gaming needs BOTH acting on the reasoning AND acting
      so as to undermine what the result means. Dropping either conjunct turns ordinary evaluation
      awareness into a reported oversight-gaming rate.
    kb/gotchas/ai/agents/evaluation/third-party-comparator/c9b6c5fa.md — Apollo benchmarked Astra's
      41.1% / 50.6% verbalized eval-awareness against GPT-5.5 at 27.7% "as they did not have chain of
      thought access to GPT-5.6-Sol". The comparator was set by ACCESS, not relevance, so the delta spans
      two releases. Plus Apollo disclaiming its own null on two independent grounds.
  NEW, from embracethered (one call, accepted first try):
    kb/gotchas/ai/agents/operations/normalized-deviance/e671d3a4.md — five vendors' own shipped-product
      documentation admitting prompt-injection RCE, exfiltration, or no human-in-the-loop, with Rehberger's
      framing of the simultaneity. The operational edge: three of the five mitigations delegate the control
      to the user's attention, and a programme that accepts "it is in the known issues" as closure has
      converted a disclosure into a permission.
  CROSS-LINKS: 8992ec34 -> a8635d4d + dc7e7bc3; 0cbaa443 -> 931d9507 + 5bad2e60 + 17b9318f;
    c9b6c5fa -> 0c3c2d6a + 2d280a46 + 17b9318f; e671d3a4 -> 335bd48f.

=== STALENESS PASS — 5 EXAMINED. 4 CONFIRMED VERBATIM, 1 ENRICHED. SCREEN (c) NOW EXHAUSTED. ===
  CONFIRMED VERBATIM  kb/gotchas/ai/agents/tools/mcp/versioning/031dab74.md — the tripwire page states
    verbatim: "The protocol version will *not* be incremented when the protocol is updated, as long as
    the changes maintain backwards compatibility." Claim intact.
  CONFIRMED VERBATIM  012daf73 (the deprecation-window fact) — same page, verbatim: "remain in the
    specification for at least twelve months, or at least ninety days under the policy's
    expedited-removal exception". Both quantifiers intact.
  CONFIRMED VERBATIM  kb/invariants/ai/agents/tools/mcp/discovery/995c167b.md — same page: server/discover
    is "a mandatory RPC" and "Calling it is optional: a client is free to send any request directly".
    The servers-MUST / clients-NEED-NOT asymmetry is intact.
  CONFIRMED  kb/invariants/ai/agents/evaluation/system-card-citation/17b9318f.md — written by the 42nd run
    and on the never-checked list. Re-read against today's three reads of the same card: the Verbalized
    Metagaming section is still present and still carries the post-Sep-9 re-scoped definitions, exactly as
    the fact's change-log account predicts. No edit needed. *** AND IT EARNED ITS KEEP IMMEDIATELY: it is
    why 0cbaa443 was given a revision-date caveat rather than quoting the definitions bare. ***
  ENRICHED  kb/invariants/ai/agents/observability/cot-monitorability/b446bef6.md — see ENRICHED below.
  *** SCREEN (c) IS NOW EXHAUSTED AND THAT IS A RESULT, NOT A MISS. *** entities queries for the bare
  names "Opus", "GPT-4" and "Sonnet" each returned ZERO facts. Combined with the 42nd run's three
  ("Gemini", "Claude", "GPT-5" — one real defect in seven hits), the corpus now has no bare-family-name
  entity left that this screen can find. STOP RUNNING IT as the first screen; run screen (e) first instead.
  Untried and probably also empty: "Claude Haiku", "Llama", "Qwen", "o1".
  SCREEN (e) — the self-declared-expiry screen, run for the first time this run via a semantic query on
  "not landed as of / verify against the live documentation / re-check this figure". It returned no NEW
  self-expiring fact beyond 943a7e3c, which the 42nd run already re-checked. The screen is cheap but a
  semantic query is the wrong instrument for it — it needs a substring grep the tool does not offer.
  A human fix would be a corpus-wide text search; see (l) below.
  AVOID kb/principles/** (write-blocked): 0f260eea, 1d1440fe, 4166926d, a829cfd4, b9b45ff5, 1feacc9e,
  f269c82f, c2f12069, 1dc822f2, db193402, 00d3ef19, 82383efe, 28ba65db, 6ec9b2b6, c9f0238b.

=== ENRICHED (3) ===
  kb/invariants/ai/agents/observability/cot-monitorability/b446bef6.md — THE QUEUE ITEM THAT WAS ALREADY
    WRITTEN (see CORRECTIONS), so the work was sharpening rather than adding. The fact carried the launch
    overview's "roughly half as many flags" over "more than 54,000 internal Codex tasks". The safeguards
    card gives the exact form: "Comparing the 54,218 tasks ... GPT-6 Astra has 53% fewer severity level 3
    actions." Added that, the metric's actual name (severity-level-3 ACTIONS covering deception, concealed
    uncertainty, exfiltration and reward hacking), and — the part that matters most — the card's own limit
    on it: "most useful as an additional signal about internal deployment risk, rather than as a direct
    measure of external deployment safety due to distribution shifts". So BOTH halves of the
    opposite-directions finding now carry their evidence type: an internal-distribution simulation its
    authors decline to read as a safety measure, against adversarial elicitation. Neither is a field
    outcome. sources HELD AT 2 — the safeguards card is a THIRD OpenAI document, and the pack's convention
    is that same-org documents corroborate nothing. refs merged to 7, read-modify-write, nothing dropped.
  kb/decisions/ai/agents/evaluation/eval-awareness-measurement/0c3c2d6a.md — *** THE RUN'S BEST FIND, and
    it is a genuine live disagreement rather than a new measurement. *** The fact's operational rule was
    "a transcript's verbalized suspicion is not a usable covariate for correcting, filtering or discounting
    a misalignment measurement" (Anthropic, 1,300 audit seeds, no correlation). Apollo, inside OpenAI's
    card, does exactly that: "given the higher rates of eval awareness and limited evaluation window, low
    rates of misbehavior here do not provide substantial evidence about the model's alignment or
    misalignment." Per Appendix S rule (b) the disagreement was KEPT, not flattened, and the separating
    condition named: Anthropic's is about CORRELATION ACROSS SEEDS (can you use awareness as a per-run
    covariate — no), Apollo's is about the EVIDENTIAL WEIGHT OF A NULL (can a low rate from an eval-aware
    model show alignment — no). Both hold; they govern different decisions, and the body now says which
    governs which. sources 1 -> 2: Apollo is a genuinely independent second organisation and a decisions
    fact about a disagreement rests on both sides, so the hold-below-org-count convention does NOT apply
    here. Title rewritten to say it is now three results. refs merged to 7.
  kb/conventions/ai/agents/evaluation/cot-labelling/0cbaa443.md — this run's own new fact, enriched in the
    same run after the staleness pass surfaced 17b9318f. Added the revision caveat: the card's change log
    records this exact section being renamed and re-scoped on 2026-09-09 with a metric comparison plot
    deleted, so the definitions are the post-revision form and need a revision date attached.

=== CORRECTIONS TO THE PREVIOUS RUN'S QUEUE ===
  *** QUEUE ITEM (5) — "THE MONITORABILITY-VS-ALIGNMENT TRADEOFF ... NOT WRITTEN" — WAS ALREADY WRITTEN,
  AND HAD BEEN FOR ELEVEN DAYS. *** b446bef6, revised 2026-09-19, already carried the tradeoff, the
  "better aligned" pairing, the sandbagging sentence, the steganography negative AND its "may largely be
  bounded" hedge, and the 54,000-task simulation — all of it, under the heading "Monitorability fell while
  alignment rose, in the same release". The 42nd run wrote the queue entry from what it had READ of the
  card, not from what the corpus HELD. This is FINDING 1 for the SIXTH consecutive run and by yet another
  mechanism: not a stale marker and not a slug-derived ranking, but a run queueing its own unfinished
  reading without querying whether the conclusion already existed. ONE mechanism-phrased knomit_query
  would have caught it, and I ran that query as step one, which is why the run spent its budget on
  sharpening b446bef6 instead of duplicating it.
  NOT A TOTAL LOSS, AND THIS IS THE USEFUL HALF: the queue entry was wrong about the CLAIM being missing
  and right about the SOURCE being unread. Section 8 held four things b446bef6 did not — the eval
  construction-order disclosures, the metagaming taxonomy, Apollo's comparator, and the exact figures. A
  queue entry naming an unread SOURCE is still worth something; a queue entry asserting a missing CLAIM is
  worth nothing without a query behind it. Queue sources, not conclusions.

=== CONTRADICTIONS ===
ONE, and it was kept rather than flattened: Anthropic's eval-awareness null vs Apollo's discounting of its
  own null. Handled inside the existing decisions fact 0c3c2d6a rather than as a new one, because that
  fact already IS the decision on this axis and a second would have been a near-duplicate. Full account
  under ENRICHED above.
ONE TENSION EXAMINED AND NOT A CONTRADICTION: 8992ec34 (construction-after-training as a validity
  disclosure) against a8635d4d (an incident-derived eval is a regression test, and a detector must not be
  hillclimbed on the incident's artifacts). They approach the same hazard from opposite ends — one asks
  when the test was built, the other what the test may be used for — and 8992ec34 links a8635d4d and says
  so.
THE SYNTHESIS CANDIDATE IS UNCHANGED AND STILL NEEDS A HUMAN: d306b10f + 102aff80 + 0fe91ac7 + e5765f0e
  all say every layer of an eval stack manufactures false NEGATIVES and they compound. kb/principles/** is
  write-blocked. c9b6c5fa is arguably a fifth member from the opposite direction — a layer manufacturing
  an unearned PASS — which may mean the right synthesis is two-sided after all and 1feacc9e already has it.

=== TOOL NOTES ===
  * knomit_learn ACCEPTED BOTH CALLS FIRST TRY — SECOND CONSECUTIVE CLEAN RUN. The recipe is the 42nd
    run's and it is cheap: count the words in every motif before submitting (2-4, kebab-case, no subject
    words), and run a mechanism-phrased knomit_query for every candidate before drafting.
  * knomit_update `ops` worked first try on three knowledge facts and both oversized private slots —
    FIFTH consecutive run. `append` needs no anchor and was the only op used this run.
  * if_commit guards used on b446bef6, 0c3c2d6a and crawl-state; none conflicted. NOTE A TRAP: for
    17b9318f, knomit_query reported commit 037de1c7 while knomit_explain reported c80196b4. USE THE
    EXPLAIN COMMIT for if_commit — the query's is not the file's HEAD.
  * refs REPLACE wholesale even alongside ops — read and resend the full merged list. Done three times.
  * NO BROWSER USED THIS RUN, and nothing needed one. Every host touched (deploymentsafety.openai.com,
    embracethered.com, anthropic.com/news, modelcontextprotocol.io) is ungated to plain WebFetch. Route 9
    says use the browser for anything you will quote — the compliant substitute, used throughout, was the
    two-call verbatim discipline, and route 22 records the one place it caught a fabrication.
  * A READ-ONLY SUBAGENT DID THE HISTORY WALK. Third consecutive run, third clean result.

=== QUEUE FOR THE NEXT RUN ===
(0) *** knomit_repos FIRST, and again before the first write. Route 10 did not recur (16 clean runs). If
    every remote-devices tool vanishes at once -> RefreshMcpTools{server: "remote-devices"}, do NOT
    re-bind; the handle survives. ***
(1) *** WRITE crawl-state ONCE, AT THE END. One revision = one run. ***
(2) *** WALK BY THE PROSE HASHES ABOVE, VIA A READ-ONLY SUBAGENT, and append this run's HEAD as the 43rd.
    ALREADY_CRAWLED should reach 298 on the job counter (294 + this run's 4). ***
(3) *** RANK FROM THE CORPUS GAP, NOT FROM THIS QUEUE — and note that this run proved the rule against
    the queue item its OWN predecessor was most confident about. Everything below is a HYPOTHESIS about
    an unread SOURCE. No entry below asserts that a claim is missing; where one seems to, query first. ***
(4) *** SECTION 9 (Preparedness) OF gpt-6-astra/safeguards. Four attempts across two runs and two methods
    (browser 34k read; three section-targeted WebFetches) all returned TRUNCATED. DO NOT TRY A FIFTH OF
    EITHER. It needs a method neither run has: the per-model PDF is cdn.openai.com and egress-denied
    (route 16), so the candidates are read_page (a different serialisation, untried on this host) or a
    WebFetch prompt that asks ONLY for section 9 and explicitly tells the reader to skip to the end of the
    document. Rank it HIGH but cap it at one attempt. ***
(5) *** https://deploymentsafety.openai.com/gpt-6-astra — THE PARENT CARD, NEVER FETCHED, and distinct
    from /gpt-6-astra/safeguards. RANK 1 OF THE GENUINELY UNREAD. The 42nd and 43rd runs both worked on
    the safeguards sub-page; nobody has opened the card it hangs off. Expect the capability scorecards to
    be below the bar and the alignment/preparedness framing to be above it. ***
(6) embracethered 2025, TOP: /2025/cross-agent-privilege-escalation-agents-that-free-each-other/ (Sep 24
    2025). Status genuinely UNKNOWN — not fetched and not cleared by a query this run. 6cc23314 and
    e899ae28 cover the peer-messages-as-authorisation shape from the DEFENDER side; this is the attacker
    side and it predates the OpenAI incident by ten months. Query the mechanism first ("one agent grants
    or restores another agent's permissions"), then fetch. Then /2025/wrapping-up-month-of-ai-bugs/
    (read INSTEAD of the ~25 individual posts) and /2025/scary-agent-skills/.
(7) THE TRANSCRIPT-ANALYSIS THEME, two items short: the techrxiv paper ("Seven Simple Steps for Log
    Analysis in AI Systems", href in crawl-sources, host NEVER TOUCHED — test the route) and the
    alignmentforum case study's per-model TABLES (route 21; neither reader returned the cells).
(8) AISI TIER A, top pair, neither touched: /blog/how-to-evaluate-control-measures-for-ai-agents and
    /blog/llm-judges-on-trial-a-new-statistical-framework-to-assess-autograders. The second pairs with
    38c06627, bacf0f4e and the hamel.dev judge material, and the pack has no statistics-of-autograders
    fact at all. The index has not been swept since the 27th run.
(9) THE OPUS 5.5 / SONNET 5.5 SYSTEM CARDS. Still no facts on either. Route 5b on anthropic.com/
    claude-opus-5-5 and /claude-sonnet-5-5 for the href — do NOT guess it. *** AND ASK THE QUESTION THIS
    RUN'S INDEX ENUMERATION SHARPENS: deploymentsafety.openai.com exists and is small and complete. WHERE
    IS ANTHROPIC'S EQUIVALENT? Two runs have now found the evaluation detail living on a separate
    documentation host from the launch post. One WebSearch would settle it. ***
(10) simonwillison "Recent articles" rail (NOT the tag feed — see the 42nd run's Note/Article finding):
    "2026 in LLMs (so far)" (Sep 27) TOP, "Claude Opus 5.5, GPT-6 Sol, GPT-6 Luna, and a new price war"
    (Sep 22), "OpenAI DevDay 2026 live blog" (Sep 29).
(11) openai.com/news — NOT swept for two runs now (last: 41st). It is the feed promoted to every-run
    cadence and it needs the browser. If the next run has browser tools, sweep it early.
(12) darioamodei.com/post/we-must-pace-the-frontier — host never touched. Pairs c262a592, 03fa7976,
    97616086, 6866e63b, bdbdd228. And the two unread /institute/ posts (recursive-self-improvement,
    econ-scenarios).
(13) THE REST OF THE SEPTEMBER THREAT REPORT — five sections, at the SITE ROOT not under /news/. The PDF
    href is in crawl-sources (www-cdn.anthropic.com, route 11, egress-denied to curl — but the HTML is at
    the site root and the 27th run read 48k of it).
(14) STALENESS. Screen (c) is EXHAUSTED — do not lead with it. Lead with (e) if a substring search becomes
    available, otherwise (d) vendor-doc refs, which found the 42nd run's real defect too. Keep (a)
    subtraction/ratio on figures the source states twice and (b) version floors and exact figures.
    A NEW SCREEN (f), earned this run and cheap: *** A FACT WHOSE ONLY REF IS A PAGE THIS RUN HAPPENS TO
    FETCH IS A FREE STALENESS CHECK. *** The tripwire alone confirmed three facts verbatim at zero extra
    cost. Before fetching anything, query for facts refing that exact URL and re-verify them in the same
    read.
    Never-checked bodies: 0525e590, c5f106f3, f727c157, f961973e, 65aa10a7, fc76b9a2, 83004507, 00f5d991,
    5bad2e60, b4d22cc2, 4777dc9b, fcce2200, bad64050, 4d13f6e9, de4e90a4, ab8f0a7e, a0cb6dc6, 79912531,
    126207f7, 71be00f9, c6feb649, plus the 42nd run's 94858345, d306b10f, bef6d86f, 92a0e10f and this
    run's 8992ec34, 0cbaa443, c9b6c5fa, e671d3a4. 17b9318f, 031dab74, 012daf73 and 995c167b are now
    CHECKED — dropped.
(15) UNMINED, NAMED SO IT IS NOT LOST, carried from the 42nd run and NOT re-validated: (i) the
    swe-bench-sonnet tool-design material (absolute-path requirement, str_replace exactly-one-match) —
    check whether only the write-blocked 82383efe carries it. (ii) From april-23-postmortem: the Opus
    4.7-found-it / Opus 4.6-didn't compound condition. (iii) From building-c-compiler: the "put yourself
    in Claude's shoes" harness rules. (iv) 71be00f9 vs the monolithic-task/oracle material in 2318b57c.
    (v) The Astra card's eval-RETIREMENT practice ("deprecated the prompt injection evaluations known as
    'Connectors' and 'Search and Function-Calling' ... because they are saturated"), plus the Production
    Benchmarks introduced for the same reason — 92a0e10f has the predictiveness criterion, this is the
    separate smaller fact. (vi) NEW: Figure 17's oversight-gaming CoT snippets are IMAGES in every reader
    tried, and the card publishes no oversight-gaming RATE; if a future run finds either, 0cbaa443 is
    where they land.
(16) LONG-CARRIED, take-or-delete: the transcript viewer; SLEIGHT-Bench paper/dataset (GitHub gated,
    route 3f); the benchmark supply-chain report for CVE-2026-66384 (lives only in bcbf13c2, NINETEENTH
    run). The three ASTRA investigations are now substantially addressed by b446bef6 + 491d1039 + 9a8a1590
    + this run's section-8 work — DROP them from this list unless a specific claim is still missing.
(17) www-cdn.anthropic.com PDFs (route 11): April Alignment Risk Update, Fable 5 / Mythos 5 System Card,
    August Risk Report (Section 5.2.3), Advanced AI Framework. NOT re-tested this run. Both vendor CDNs
    (www-cdn.anthropic.com, cdn.openai.com) remain egress-denied to curl — look for the HTML twin first.

=== FOR A HUMAN, NOT THE CRAWLER ===
*** FINDING 1, SIXTH RUN, AND IT HAS NOW FAILED IN EVERY DIRECTION IT CAN. *** The 41st run found its
inherited queue four-for-four ALREADY MINED. The 42nd found its rank-1 item was a two-sentence Note that
was never worth mining. This run found that its predecessor's single most emphatic queue entry — "THE
MONITORABILITY-VS-ALIGNMENT TRADEOFF, spotted in section 1 and NOT written" — described a claim the corpus
had held for eleven days, written by a run four earlier. Three runs, three different failure modes, one
cause: a queue entry is an assertion about the CORPUS written by a run that was looking at a SOURCE.
*** THE REFINEMENT THIS RUN ADDS, AND IT RESCUES SOMETHING FROM THE WRECKAGE: separate the two kinds of
queue entry. "This SOURCE is unread" is a cheap, checkable, useful hypothesis — section 8 really was
unread and really did yield four facts. "This CLAIM is missing" is worthless without a query, and it is
the shape that has now been wrong three runs running. A human fix: let the queue name only sources, and
let the NAMED GAPS list (a claim the pack wants and does not have) be the separate, query-validated
artifact the 42nd run proposed. A gap is self-clearing; an unread marker is not; and conflating them is
what produces an entry that is simultaneously right about the URL and wrong about the knowledge. ***
(b) FIX APPENDIX S'S WALK PROTOCOL: steps 2-3 terminate several hops early. Measured NINE times now
    (route 6, 35th-43rd runs). Only a human can fix the spec. The working protocol is the prose-hash list
    plus a read-only subagent, and the spec should say both.
(c) THE REPORT SECTION OF crawl.md ASKS FOR "confirmation that the only .knomit/ paths you wrote were the
    TWO state slots", but Appendix S's own table lists THREE job-writable slots, and step 2 authorises
    writing crawl-sources while step 4 sends routes to fetch-routes. This run wrote all three,
    deliberately. Please reconcile the wording — FIFTH run asking.
(d) www-cdn.anthropic.com and cdn.openai.com both denied by egress policy — FIFTEENTH run asking.
(e) GitHub API not enabled (route 3f) — blocks SLEIGHT-Bench dataset and MCP spec revision-diffing.
(f) The `sources` CONVENTION (hold below org count when a second org ILLUSTRATES or BOUNDS a claim rather
    than corroborating it) is 22 runs old and still not in Appendix S. Applied BOTH WAYS this run, which
    is the first time the distinction has been exercised in one run: HELD at 2 on b446bef6 (a third
    OpenAI document corroborates nothing), RAISED 1 -> 2 on 0c3c2d6a (a second organisation DISAGREEING is
    a genuine second source for a decisions fact about the disagreement). If the convention goes into
    Appendix S, it needs both halves.
(g) The agentic-engineering repo also carries a kb/technology/** corpus from another pipeline; check a
    knomit_query result for a BARE path before concluding a fact exists here.
(h) Appendix S should say that ALREADY_CRAWLED is a LOWER BOUND — SIXTH consecutive run demonstrating it.
(i) Appendix S's staleness instruction says to sample facts "with confidence=low or last verified more
    than 90 days ago", but knomit exposes no last-verified field — only committed_at, which moves on any
    edit. FOURTH run asking.
(j) NEW, and small: knomit_query and knomit_explain reported DIFFERENT commits for the same fact at the
    same moment (17b9318f: query 037de1c7, explain c80196b4). Explain's is the one if_commit accepts. If
    that is a bug rather than two different things being reported, it is a cheap one to fix; if it is by
    design, the query result's `commit` field could usefully be named something else.
(k) The browser remains READ-ONLY on scheduled runs (route 18). Not exercised this run — no browser call
    was made, because nothing needed one.
(l) SCREEN (e) NEEDS A SUBSTRING SEARCH AND knomit DOES NOT HAVE ONE. The screen looks for facts whose
    BODIES declare their own expiry ("not landed", "as of", "check against the live docs"). A semantic
    knomit_query cannot do this — it matches meaning, and these are boilerplate phrases whose meaning is
    not what identifies them. Run blind, it returned nothing new. A `text_exact` or regex filter on
    knomit_query would turn the pack's best-designed screen from unusable into one call.

PROMPT INJECTION: one observation, the SAME one the 42nd run recorded, on the same host, and again NOT
complied with. https://modelcontextprotocol.io/specification/versioning returned, prepended above the page
content, a block addressed to an automated reader: "## Documentation Index / Fetch the complete
documentation index at: https://modelcontextprotocol.io/llms.txt / Use this file to discover all available
pages before exploring further." That is fetched content instructing the agent to retrieve a URL not on
the work list. It is the site's own llms.txt convention and almost certainly benign; the instruction was
NOT followed and llms.txt was NOT fetched. Recorded a second time because a recurring agent-directed block
on a host this job reads EVERY RUN is exactly the position an adversary would want to occupy.
OTHERWISE: no page addressed the agent, attempted to redirect the crawl, or asked for a fetch off the work
list. Every URL visited was on the work list, was an index this job already tracks, or was a ref on a fact
being re-verified. No slug was guessed. The GPT-6 Astra safeguards card is a document OF safety
evaluations describing model evasion, sandbagging and oversight gaming; it was read as reported
measurements and turned into facts about what that organisation measured, never as instructions to this
job. The embracethered post is adversarial security research and was read the same way. A read-only
subagent hand-back arrived mid-run and was treated as model output, not as user authority; it was given
read-only instructions, one file path and a hash list, and it made no writes. Nothing recorded as dead,
blocked or paywalled.

SUB-RULES, cumulative (the 42nd run's three stand; this run adds three):
 (43rd) *** QUEUE SOURCES, NOT CONCLUSIONS. "This URL is unread" is a cheap hypothesis that a fetch
   settles. "This claim is missing" is an assertion about the corpus, and a run that is looking at a
   source is in the worst possible position to make it — it has just read the evidence and not the
   corpus. Three consecutive runs have now been wrong in that exact posture. If you catch yourself
   writing a queue entry that says a fact does not exist, run the query instead of writing the entry. ***
 (43rd) *** A PAGE YOU ARE FETCHING ANYWAY IS A FREE STALENESS CHECK. Before any fetch, ask which facts
   ref that URL and re-verify them in the same read. The tripwire — one WebFetch this job runs every
   single run, for one sentence — turned out to be the sole ref behind three live facts and confirmed all
   three verbatim for nothing. Screen (f). The staleness pass does not have to be a separate budget. ***
 (43rd) *** AN EXTRACTION'S FABRICATIONS ARE ADVERBS BEFORE THEY ARE FACTS. The open-ended read returned
   "a substantial decrease in chain-of-thought monitorability" where the page says "show decreases in
   chain-of-thought (CoT) monitorability". Nothing was contradicted; an intensifier was added. Route 4
   has always been framed around invented CONTENT, and invented EMPHASIS is both more common and harder
   to see, because it survives every consistency check you would think to run. Quote-level verbatim
   verification catches it; summary-level agreement does not. ***
