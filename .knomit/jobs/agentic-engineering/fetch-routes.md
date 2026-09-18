---
type: process
domain: [agentic-engineering, job-state]
confidence: 1
sources: 1
entities: [agentic-engineering]
refs: ['https://github.com/knomit/knomit']
---
# Per-host fetch routes and tool caveats

*** HOW TO FETCH THINGS THAT DO NOT FETCH NORMALLY. ***
Per-host recipes and tool caveats. Split out of crawl-sources.md on 2026-08-11, where they were
tangled with the source list and with per-run status.

READ THIS BEFORE RECORDING ANY SOURCE AS BLOCKED, PAYWALLED OR DEAD. The standing rule that governs
that decision lives in spec.md (Appendix S) — "never declare a source dead", with the six routes to
exhaust first. This file is the concrete how-to behind it.

Scope: durable operational knowledge. It changes when a WEBSITE changes, not when a run happens.
Do not put run status, queues or rankings here — those go in crawl-state.md.

*** ====================================================================================== ***
*** ROUTE 10. THE SESSION BINDING CAN REVERT MID-RUN, AND EVERY knomit CALL AFTER THAT     ***
*** SILENTLY ADDRESSES THE WRONG REPOS. IT PRESENTS EXACTLY AS "THE CORPUS HAS BEEN WIPED". ***
*** MIGRATED IN FROM THE 27th RUN'S crawl-state ON THE 28th RUN. READ THIS FIRST.          ***
*** ====================================================================================== ***
The job prompt says to bind once and not call knomit_bind again for the rest of the run. THAT
INSTRUCTION ASSUMES THE BINDING HOLDS. On the 27th run it did not. Measured, in order:
  1. knomit_bind{repo: agentic-engineering} -> correct binding, one mount, read+write. All three
     state slots read normally at this point.
  2. Some calls later, WITH NO INTERVENING BIND: five path-scoped knomit_query calls
     (kb/incidents/ai/agents, kb/architecture/ai/agents, kb/gotchas/ai/agents,
     kb/conventions/ai/agents, kb/invariants/ai) ALL returned ZERO facts.
  3. knomit_explain on two exact fact paths the 26th run recorded writing -> "could not read".
     Then knomit_explain on the job's OWN state slot -> "could not read".
  4. knomit_query sort=recent returned 15 facts, all under kb/technology/**, committed today — a
     corpus this pack does not own.
  5. knomit_repos -> "bound": {"binding": "knomit-positioning", ...}. THE LENS, NOT THE REPO. That
     lens mounts core, knomit-io-kb and knomit-kb, and does NOT mount agentic-engineering at all.
     That is the whole explanation for steps 2, 3 and 4.
  6. Re-binding restored everything immediately. THE CORPUS WAS INTACT THE ENTIRE TIME.
IT RECURRED that run in a different costume: a knomit_learn was rejected with
`validate path: unknown topic "incidents"` — which is drift, since core's ontology has no
"incidents" topic. Re-binding and resubmitting the identical call committed all six facts.

*** WHY THIS IS THE MOST DANGEROUS FAILURE MODE THIS JOB HAS HIT. *** Four of this pack's own
standing rules fire on the symptom and all four point the wrong way. An empty scoped query looks
like "this pack holds nothing here", which is the reading that LICENSES WRITING DUPLICATES.
"could not read" on an exact path looks like the route-7 history problem. A repo full of unfamiliar
kb/technology facts looks like the corpus having been replaced. And a tidy causal story was
available and tempting: knomit-kb carries a fact describing a knomit 0.5.3 defect whose two named
symptoms are EXACTLY "query never lists it" and explain failing with "could not read". It matched
perfectly and it was not the cause. Only a sixth measurement — knomit_repos, which nothing
required — separated them.

*** WHAT EVERY RUN MUST DO, and it costs one cheap call: ***
  (a) CALL knomit_repos AND CHECK `bound.binding` BEFORE BELIEVING ANY NEGATIVE RESULT. An empty
      query, a "could not read", or an "unknown topic" error is a BINDING claim until knomit_repos
      says otherwise. Never record a corpus-state finding without that check in the same breath.
  (b) RE-BIND BEFORE EVERY WRITE. The prompt's bind-once rule is overridden by observation here;
      re-binding to the SAME repo serves its intent (never switch repos mid-run) and costs one call.
  (c) A REFUSAL NAMING AN ONTOLOGY TOPIC THE PACK OWNS ("unknown topic incidents") IS DRIFT, NOT A
      SCHEMA ERROR. Re-bind and resubmit the identical call before editing anything.

*** 10b. THE 27th RUN'S COMMIT-RESOLUTION FINDING WAS VOID, AND THE 28th RUN RE-RAN IT CLEANLY. ***
The 27th run tried five full 40-hex commits on crawl-state and got "could not read" on all five,
which looked like a decisive finding that recorded commits stop resolving. It correctly voided its
own result because the binding drift was active across an unknown part of that sequence.
THE RE-TEST, 28th run, with knomit_repos verified before and after and no drift in between: ALL
FIVE RESOLVED AND RETURNED FULL BODIES — 3c6323cd52188f057c16d15b2c7b72ad9d9e91e9,
8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f, c6cab79802bfc5ad45da90851f698de37ba8d1cb,
91f7d0857b745035973adfb6d543960e53e59779 and 7462e9f229b6cc3ef2c2da12be49c1cd468a6e55.
CONCLUSION, now established rather than suspected: **a full 40-hex commit recorded by an earlier run
resolves reliably. A "could not read" on one is a binding claim, not a history claim.** This closes
the question runs 23-27 kept re-opening in one form or another.
FOR THE OPERATOR: the cause of the drift itself is still not established. It was not observed to
correlate with any particular tool, and no call was made that would switch the binding.
knomit-positioning appears to be the session default the binding falls back to.

*** ====================================================================================== ***
*** ROUTE 9. THE BROWSER IS NOT A 403 WORKAROUND. IT IS THE DEFAULT ROUTE FOR ANY PAGE YOU ***
*** WILL TAKE A NUMBER OR A QUOTATION FROM. 26th RUN, MEASURED ACROSS THREE HOSTS.        ***
*** ====================================================================================== ***
Route 1 introduced a browser MCP server because openai.com 403s to WebFetch. The 26th run used it on
THREE hosts, only one of which is gated:
  openai.com        — gated (route 1). Browser required.
  www.anthropic.com — NOT gated. WebFetch works fine. Browser used anyway.
  metr.org          — NOT gated. WebFetch works fine. Browser used anyway.
All three returned full article text first try.
28th-RUN ADDITION: alignment.anthropic.com and alignment.openai.com are both NOT gated and both read
fine in the browser first try. openai.com/index/<slug> still needs the browser.

*** WHY DO THIS ON A HOST THAT IS NOT GATED: ROUTE 4. *** `WebFetch` answers a prompt with a small
fast model, so everything it returns is an EXTRACTION and can be fabricated. A browser text read
(`get_page_text`, or an innerText evaluate where scripting is permitted) is a TRANSCRIPTION — no
model in the loop — so every figure and quoted string taken from it is safe by construction, and the
two-call verbatim discipline is unnecessary.
MEASURED ON THE 26th RUN: roughly forty quoted strings and twenty-five figures were written into
facts from browser text with ZERO route-4 exposure. The only WebFetch calls were index sweeps (where
the output is a list of hrefs, not a claim) and ONE deliberate verbatim verification call.
COST COMPARISON, which is the reason this is now the default and not merely permitted:
  WebFetch on a claim-bearing page = 1 open-ended call + 1 verbatim call = 2 calls, still an extraction.
  Browser                          = 1 navigate + 1 text read           = 2 calls, and it is a transcription.
Same call count, strictly stronger evidence. THE RULE: if you intend to QUOTE it or take a NUMBER
from it, load it in the browser. Use WebFetch for index sweeps and for "is there anything new here".
CAVEAT: the browser is not free — it needs a live browser MCP server, and route 1 records that WHICH
server is live varies between runs. Check, do not hardcode. And browser text loses table structure
the same way pdftotext does; the form-feed rule does not apply but the pairing caution does.

*** 9b. openai.com/index/ NOW REDIRECTS TO openai.com/news/. 26th run. *** Navigating to
`https://openai.com/index/` lands on `https://openai.com/news/`. THIS IS A LANDING-PAGE CHANGE ONLY
— individual post URLs are STILL `/index/<slug>` and resolve normally; nothing needs re-slugging.
/news/ is now where the newest-first listing lives. Do not read the redirect as posts having moved.

*** 9c. TWO BROWSER READER CAVEATS, 27th RUN, BOTH COST A RUN TIME IF UNKNOWN. ***
  * `read_page` returned "(empty page)" with "Viewport: 0x0", and a click by ref then failed with
    "entirely outside the viewport". `get_page_text` on the SAME tab at the SAME moment returned the
    full article. AN EMPTY read_page IS NOT EVIDENCE THE PAGE FAILED TO LOAD — try the other reader.
    This is the same family as route 3c (a 404 body written to a file) and route 2d (a grep that
    errored): the tool's failure wears the costume of the data's absence.
  * `get_page_text` caps at max_chars and truncates the TAIL with no offset parameter, so a document
    longer than the cap cannot be paged through with it. Hit at 48,000 chars on the September threat
    report and again on the reward-seeker post. The compliant fallbacks are the PDF (route 5b for the
    href, then curl + pdftotext) or `read_page`, which returns a different serialisation.

*** ====================================================================================== ***
*** ROUTE 8. A CDN ASSET URL THAT WORKED YESTERDAY CAN 404 TODAY. THE DOCUMENT IS NOT GONE  ***
*** — THE FILENAME CHANGED. 25th RUN, HIT LIVE ON THE PACK'S MOST-CITED PDF.               ***
*** ====================================================================================== ***
MEASURED, 25th run. The 24th run fetched OpenAI's Hugging Face technical report successfully and
recorded its URL into TEN facts. One day later the identical URL returned **HTTP 404 with an Azure
blob-storage XML body**: `<Error><Code>BlobNotFound</Code>`. Two curl attempts, same result.

THE DIFFERENCE WAS ONE CHARACTER IN THE FILENAME:
  DEAD: .../OpenAI-Hugging%20Face%20Incident-Technical-Report.pdf   (space after "Hugging")
  LIVE: .../OpenAI-Hugging-Face%20Incident-Technical-Report.pdf     (HYPHEN after "Hugging")
The UUID path segment was unchanged; only the leaf filename was re-normalised. `pdfinfo` on the
recovered file returned 38 pages, CreationDate 2026-08-26 — byte-identical fingerprint to the 24th
run's. **The document did not change. Only its URL did.**

RECOVERY, and it took one call: an href harvest on the page that links it, filtering for
`pdf|cdn\.openai`. The page's links had been updated to the new filename. This is route 5b/5c's core
rule arriving in a new place: **ask the PAGE for the href; never trust a recorded asset URL to still
resolve.**

THREE ACTIONS THIS IMPLIES, all cheap:
 1. A 404 on a `cdn.openai.com` (or any CDN) asset is a FILENAME claim, not a withdrawal claim. Do
    not record the document as retracted, superseded, or paywalled. Re-harvest the href first.
 2. The XML error body is the tell. `file <name>.pdf` reporting "XML 1.0 document text" means you
    downloaded an error page under a .pdf name — exactly the failure shape route 2 warns about for
    OWASP's HTML "No Access" page. ALWAYS run `file` on a downloaded binary.
 3. *** WHEN AN ASSET URL MOVES, THE CORPUS IS NOW WRONG, NOT JUST YOUR FETCH. *** Query the kb for
    the stale URL and repair every fact that carries it. The 25th run found TEN: bcbf13c2, 931d9507,
    a0d01236, 2dfac716, fe10df26, 02f74ac7, cef2dda8, 6cc23314, 757df748, 23efa1db. Each repair is a
    read-modify-write of the FULL refs list (knomit_update REPLACES refs), so budget one call each.
GENERALISE THE HABIT: whenever you re-fetch a previously recorded asset and it fails, assume URL rot
before assuming source death, and assume the corpus inherited the bad URL.
*** STATUS: the hyphenated URL has NOT been re-tested since 2026-08-29. Treat it as the
*** recorded-good form, unverified since that date, rather than as re-confirmed. ***

*** 8b. TRANSCRIPT-ANALYSIS REPORTS MARK PARAPHRASED CHAIN-OF-THOUGHT. QUOTING A PARAPHRASE AS
*** VERBATIM IS THE ROUTE-4 DEFECT CLASS ARRIVING FROM A TRANSCRIPTION RATHER THAN AN EXTRACTION. ***
The METR + Redwood Hugging Face report states its own convention explicitly, and it is easy to miss
because the document is otherwise a clean pdftotext transcription:
  "We indicate paraphrasing with {curly braces} ... <angle brackets> within the paraphrase"
   for parts METR could not interpret.
It also says it "limited raw CoT to thirty snippets, so some snippets are paraphrased."
SO, READING THE REPORT:
  "double quotes"  = raw, verbatim agent text. SAFE to quote.
  {curly braces}   = METR's PARAPHRASE. The wording is METR's, not the agent's. NEVER present as a quote.
  <angle brackets> = METR is unsure what this part meant. Do not build a claim on it.
  '‘single quotes’' also appear and are ambiguous — prefer a double-quoted instance if one exists.
THE WIDER RULE: route 4 says a transcription is safe from FABRICATION because no model is in the
loop. That remains true — but a transcription faithfully reproduces the SOURCE'S OWN hedging
markers, and dropping those is a defect YOU commit, not one the tool commits. Before quoting from any
report that analyses transcripts, grep it for "paraphras" and find out what its convention is.
*** 26th-RUN EXTENSION, SAME FAMILY, DIFFERENT MARKER: A VENDOR POST'S FOOTNOTES CARRY THE
*** RETRACTIONS. *** Anthropic's 2026-08-31 alignment/security post states in a footnote that its
technical mitigations against accidentally training on chain-of-thought "have not been wholly
sufficient", and in another that its new classifier was verified against the July incidents. Neither
is in the body. Browser text DOES capture footnotes, at the very end of the page, well after what
looks like the end of the article. READ TO THE ACTUAL END OF THE TEXT, not to the last heading.
*** 28th-RUN EXTENSION: A RESEARCH POST'S FIGURES SERIALISE AS LABELS-AFTER-VALUES OR
*** VALUES-AFTER-LABELS AND THE ORDER IS NOT STABLE WITHIN ONE PAGE. *** On the Anthropic
reward-seeker post the behavioural-audit chart serialised as value-pairs THEN the six dimension
labels, while the cyberattack chart interleaved variant headings BETWEEN its rows. Both are
recoverable, and neither is recoverable from cell order alone. THE DISCIPLINE THAT WORKED: pair on
the PROSE. The post says the model "appears slightly more aligned than the Init in overall
misalignment", and lower means more aligned, which is what fixes 4.20 to the model and 4.34 to the
init. Where prose does not disambiguate a pairing, say so in the fact rather than picking — the 28th
run did this for two hint-variant rates, and the fact carries the caveat.

*** ====================================================================================== ***
*** ROUTE 7. THE RUN-NUMBER SEQUENCE IS THE INTEGRITY CHECK ON THE HISTORY WALK. RUN IT     ***
*** EVERY TIME. THE ONE GAP ON RECORD HAS A KNOWN CAUSE AND IS NOT AN ONGOING MECHANISM.    ***
*** CORRECTED 26th RUN — READ THIS WHOLE ENTRY BEFORE REPEATING ANYTHING ABOUT "SQUASHING". ***
*** ====================================================================================== ***
*** THE CORRECTION FIRST, because runs 23-26 all wrote the wrong version of this. ***
Runs 23, 24, 25 and 26 each recorded that "the revision history is being squashed", that per-run
writes survive "only until the next PR merge", and that seven runs were permanently lost. THAT
DIAGNOSIS WAS WRONG, and it was an inference presented as a measurement.

WHAT IS ACTUALLY TRUE, per the repo owner (2026-09-08): **the repository was rebuilt between the
22nd and 23rd runs, and some run revisions were lost in that rebuild.** It is a ONE-OFF HISTORICAL
EVENT, not a mechanism that operates every merge. From the 22nd run onwards the history has behaved
correctly. `knomit_update` retains the revision it writes.
*** 28th-RUN CONFIRMATION, THE STRONGEST YET: a single walk read EIGHT distinct run bodies — runs
*** 27, 26, 25, 24, 23, 22, 16 and 13 — every one addressable by its full 40-hex commit, across
*** many intervening merges. Runs 22 onwards are all individually retrievable. The gap is confined
*** to runs 14-15 and 17-21 and has not grown since it was created. STOP RE-LITIGATING IT. ***

WHY FOUR RUNS IN A ROW GOT IT WRONG, because the failure mode is instructive:
  * The observation was real — the 22nd run read seven bodies including runs 17-21; the 23rd run
    could not enumerate them.
  * The surviving OLDER commits on this path all happened to be merge commits, which is what the
    post-rebuild state looks like. Every run since read that pattern as a causal mechanism and
    predicted it would recur. It did not recur — and each run then explained the non-recurrence away
    ("no merge has landed yet") instead of treating it as disconfirmation.
  * NOBODY EVER TESTED WHETHER THE REVISIONS EXISTED. The only test attempted was passing 8-char
    prefixes to `knomit_explain`, which 7b below shows is uninformative in both directions.
  * THE DEFECT CLASS IS THE PACK'S OWN: an overclaimed absence, inherited from job state and
    re-asserted without verification. "Not enumerated by the listing" is an observation; "lost" is a
    claim.

*** AND ONE APPARENT GAP IS NOT A GAP AT ALL. *** `more_available: false` at
8b9a768debcfa982f4ec2a8155c1bc9195c0bb0f is CORRECT and expected: that commit is REVISION 1 OF THIS
PATH. Its own body says so — "never expect RevisionsBefore to reach past this point — it keys on an
exact path and does not follow renames." The state used to live at other paths, and that history is
NOT lost, merely elsewhere:
  kb/meta/jobs/agentic-engineering/crawl-state/037911b0.md    14 revisions
  kb/meta/jobs/agentic-engineering/crawl-state/d57d2b90.md     2 revisions
  kb/meta/jobs/agentic-engineering/crawl-sources/fa385bda.md  18 revisions
If a future run ever genuinely needs pre-13th-run URL detail, explain THOSE paths. It should not need
to: the 13th run wrote the full 190-URL union into its body precisely so nobody has to.

*** WHAT TO ACTUALLY DO, and it costs nothing: READ THE RUN NUMBERS AND REPORT THEM. *** Every body
opens "crawled: <date> (Nth run)". Report the sequence you got and any gap in it. `more_available` is
a statement about the listing, not about the data, so it is not by itself evidence of completeness.
A gap is a prompt to investigate, NOT a finding of loss.
KNOWN GAP, cause established, do not re-litigate: runs 14-15 and 17-21 are not enumerated on this
path. Runs 22 onwards are fine and have stayed fine.

*** 7b. SHORT COMMIT HASHES DO NOT RESOLVE. `knomit_explain` NEEDS THE FULL 40-HEX. ***
  knomit_explain(commit="4cce7781") -> "could not read ... at 4cce7781"
ISOLATED PROPERLY: the same call with a KNOWN-GOOD commit's short prefix fails identically —
knomit_explain(commit="3c6323cd") errors, while the full
3c6323cd52188f057c16d15b2c7b72ad9d9e91e9 succeeds. So a short-hash failure tells you NOTHING about
whether the commit exists. Do not read it as evidence of absence, and do not read it as evidence of
presence.
*** ACTION FOR EVERY FUTURE RUN, one line, costs nothing: when recording commits in a crawl-state
body, WRITE THE FULL 40-HEX HASH. *** (Adopted 23rd run; held 24th-28th.) The 28th run's re-test
(route 10b) is what made this pay: five full hashes recorded by earlier runs all resolved, which
settled a question that had been open since the 23rd.

*** ====================================================================================== ***
*** ROUTE 6. THE HISTORY WALK SKIPS ONE BODY PER HOP IF YOU ANCHOR ON THE OLDEST REVISION. ***
*** 22nd run. THIS ONE IS REAL, MEASURED, AND STILL BITES.                                 ***
*** ====================================================================================== ***
Appendix S says: take the OLDEST commit in `history.revisions` and call knomit_explain again with it.
That advances the window correctly, but it does NOT read every revision, and the shortfall is invisible.
EACH CALL RETURNS THE ANCHOR PLUS THE TWO NEXT-OLDER, AND ANCHORING ON THE OLDEST ADVANCES BY TWO. So
the MIDDLE entry of every listing is NAMED but its BODY IS NEVER FETCHED. Skipped without
intervention on the 22nd run: 22649951, 4feee885, 7a9ec830, 0ac250fd — and 4feee885 WAS THE ENTIRE
19th RUN.
THE RULE: **the revision LIST is the work list, not the anchor chain.** After each call, add all
returned commits to a to-read set; then read every one whose body you have not already seen.
25th-RUN CONFIRMATION: HEAD returned [91f7d08, 7462e9f2, 65e9612b]. Anchoring on 65e9612b would have
skipped 7462e9f2 — the entire 23rd run.
26th-RUN CONFIRMATION, and the miss would have been two runs: HEAD returned [c6cab798, 91f7d085,
7462e9f2]; anchoring on 7462e9f2 would have skipped 91f7d085 (24th), and that call's listing would
then have skipped 65e9612b (22nd).
*** 28th-RUN EXTENSION, AND IT IS A NEW SHAPE OF THE SAME PROBLEM. *** At HEAD the listing was
[c3bbd6a3, 20eb4edb, 65e9612b] — it skips over the 25th, 24th and 23rd runs entirely, because the
listing is not dense. Anchoring on 65e9612b reached only [65e9612b, 3c6323cd, 8b9a768d] and
more_available went FALSE, which would have ended the walk at SIX run bodies while three were
unread. THE ONLY THING THAT RECOVERED THEM was taking the full 40-hex hashes that PRIOR BODIES
RECORDED IN PROSE and explaining each one directly. So the work list is not just "every commit the
listings return" — it is that UNION the commits named inside the bodies you read. The 26th run's
body names c6cab798, 91f7d085 and 7462e9f2; all three resolved. This is the second reason route 7b's
full-hash rule matters, and it is why the walk is only complete when the run-number sequence is
contiguous or its gaps are explained.

*** ====================================================================================== ***
*** ROUTE 4. THE TOOL ITSELF CAN INVENT THINGS. THE MOST IMPORTANT ENTRY IN THIS FILE FOR  ***
*** FACT QUALITY. 20th run; SCOPE WIDENED BY THE 21st, 22nd AND 23rd. READ BEFORE WRITING  ***
*** ANY FIGURE, QUOTATION OR IDENTIFIER INTO ANY FACT.                                     ***
*** SEE ROUTE 9: THE CHEAPEST WAY TO AVOID ALL OF THIS IS TO USE THE BROWSER INSTEAD.      ***
*** ====================================================================================== ***
`WebFetch` answers a prompt against the page using a SMALL FAST MODEL. That model will FILL GAPS
WITH PLAUSIBLE VALUES when the prompt invites a narrative summary. This is not a page problem, not a
fetch failure, and not something the 404-body guard or any download check can catch — the fetch
succeeded and the prose reads perfectly.

ISOLATED CLEANLY, 20th run: SAME URL, two calls, only the PROMPT differed.
  Call 1, open-ended ("extract the full substance ... any specific numbers") returned:
    "a monitor suspicion score of 3 out of 100 within 5,000 queries, compared to Best-of-N baseline
     scores of 14-18 across three runs of 150,000 queries each"
  Call 2, verbatim-demanding ("Quote VERBATIM ... or say NOT STATED") returned:
    "In one run, the evolutionary algorithm achieved a score of 3 in under 5k steps"
    "BoN scores of 14, 15 and 18"      Query count for BoN: **NOT STATED**
THREE FABRICATIONS IN ONE SENTENCE: (i) "out of 100" — a scale maximum the page never gives; (ii)
"across three runs of 150,000 queries each" — an entire baseline budget, invented, and it was the
denominator the whole efficiency comparison rested on; (iii) "queries" for the source's "steps".

*** THE 21st RUN WIDENED THE CLASS TWICE, AND NEITHER NEW CASE IS A NUMBER. ***
  (iv) A VERSION IDENTIFIER. Open-ended reported "Claude 3.5 Sonnet"; verbatim returned "Claude 3.7
       Sonnet". A minor-version slip that would have mis-specified the capability gap under test.
  (v)  A PARAPHRASE ARRIVING INSIDE QUOTATION MARKS, on the LiteLLM post.
SO THE RULE IS NOT "VERIFY NUMBERS". IT IS: ANY STRING YOU INTEND TO PUT IN QUOTATION MARKS, ANY
FIGURE, ANY THRESHOLD, AND ANY VERSION OR PRODUCT IDENTIFIER GOES THROUGH THE SECOND CALL.

*** 22nd-RUN ADDITION: THE SECOND CALL ALSO CATCHES THE OPPOSITE ERROR — AN OPEN-ENDED CALL
*** REPORTING SOMETHING AS ABSENT THAT IS PRESENT, WHICH PRODUCES AN UNDERCLAIM. ***
On the Echoverse post an open-ended read left the impression that live-web transfer was described
qualitatively; a targeted call returned the figures and, asked directly whether the post says
transfer was unmeasured, answered NOT STATED. So the second call is an ABSENCE filter as well as a
fabrication filter, and ASKING THE NEGATIVE QUESTION EXPLICITLY ("does the source state anywhere that
X was NOT measured?") is what separates "the page does not say it" from "I did not see it".
*** 26th-RUN CONFIRMATION OF THE ABSENCE FILTER, ON A STALENESS CHECK: asked whether the latent.space
*** bad-envs post marks its 5% threshold as a rule of thumb rather than a measurement, the verbatim
*** call answered that it does NOT caveat it either way. That negative is what turned 0fe91ac7's flat
*** "the threshold, stated directly" into "stated with no derivation". ASK THE NEGATIVE QUESTION
*** DURING STALENESS PASSES TOO. ***

*** 23rd-RUN ADDITION (vi): THE OPEN-ENDED CALL DROPS QUALIFYING CLAUSES AND INVERTS AGENCY, AND
*** BOTH SURVIVE A PLAUSIBILITY CHECK BECAUSE THE RESULT READS AS A CLEANER FINDING. ***
Three measured cases in one run:
  * A DROPPED MODAL SCOPE. Open-ended on the embracethered Auto Mode post gave "60-80% success
    rates"; verbatim gave "I got attack success rates up to 80% using a small sample size". The
    range was invented AND the small-sample caveat was dropped.
  * AGENCY INVERTED. The same open-ended call listed `python3 -I` under "Recommended Mitigations".
    Verbatim: "The child uses `python3 -I -c ...` to avoid recursively falling for the same shadowing
    attack" — it is what the ATTACKER's payload does. A defensive recommendation was manufactured
    out of an attacker technique, which is the most dangerous single error class in this pack.
  * A CLAUSE THAT REVERSES A CLAIM'S SCOPE. On the AISI sandbox-escape post, both calls agreed models
    escape misconfigurations "reliably". Only a THIRD, targeted call surfaced the full sentence:
    "Advanced models can reliably escape common misconfigurations **when prompted to do so**." That
    turns a behaviour claim into an elicited-capability claim.
THE LESSON: ENUMERATE THE QUALIFIERS, NOT ONLY THE FACTS. Ask for the WHOLE SENTENCE containing a
claim, not for confirmation that the claim appears.

*** 24th-RUN ADDITION: THE TWO SIDES OF A COMMISSIONED-REPORT PAIR HAVE DIFFERENT EXPOSURE. ***
A PDF you pdftotext is a TRANSCRIPTION and its quotes are safe; the vendor's BLOG POST fetched via
WebFetch is an EXTRACTION and invents editorial framing. When both exist, quote the PDF and treat the
blog summary's "agreement/disagreement"-style claims as unverified.
*** 25th-RUN QUALIFICATION, SEE 8b ABOVE: a transcription is safe from FABRICATION but faithfully
*** reproduces the source's own hedging markers. Dropping those is your defect, not the tool's. ***

NOTE THE BIAS, because it is what makes this dangerous: every invention made the account MORE
COMPLETE AND MORE QUOTABLE. Fabrication here is not random noise, it is narrative gap-filling, so the
invented detail is exactly the one that makes a fact worth writing. It will pass a plausibility check
because plausibility is what produced it.
*** AND THE SAME BIAS OPERATES ON THIS FILE, NOT ONLY ON FETCHED PAGES — SEE THE ROUTE 7
*** CORRECTION, AND ROUTE 10's knomit-0.5.3 near-miss. A tidy causal mechanism is more quotable than
*** an untidy observation, and runs have repeatedly preferred the quotable one. Apply route 4's
*** discipline to the bookkeeping. ***

THE RULE, and it is cheap enough that there is no excuse:
  * NEVER write a number, a quotation, a named threshold or a version identifier into a fact from an
    OPEN-ENDED WebFetch.
  * Run a SECOND call on the same URL whose prompt says: "Quote VERBATIM the exact sentences that
    state each of these, or say NOT STATED if absent", enumerating each item you intend to use.
    The "or say NOT STATED" clause is load-bearing.
  * Anything the second call marks NOT STATED does not go in the fact.
  * IF YOU DID NOT ASK THE SECOND CALL ABOUT IT, YOU DO NOT HAVE IT. But VERIFYING IS CHEAPER THAN
    DELETING — prefer one more call to a deletion.
  * CALIBRATION, so this is not read as "WebFetch is unreliable": the two-call pattern confirmed 7/7
    and 8/8 figures on two pages and 8/8 quoted strings on a third in the 20th run, 8/8, 6/6 and 8/8
    across three pages in the 21st, 10/10 and 8/9 on one arXiv paper plus 5/5 on Echoverse in the
    22nd, in the 23rd 8/8 on the AISI optstop post and 7/7 on the embracethered post, in the 26th
    4/4 on the latent.space bad-envs post, and in the 28th 3/3 on the MCP versioning page when the
    same page was re-read in the browser. The tool is accurate when the page states the thing. It
    invents when the page does NOT.
  * THIS IS ALSO RETROSPECTIVE. When verifying an old fact, the detail most likely to be fabricated
    is the one that COMPLETES A SET.

*** ====================================================================================== ***
*** ROUTE 5. READING AN INDEX AS A LIST IS ONE PLAIN WebFetch AND IT RETURNS THE WHOLE     ***
*** ARCHIVE. 21st run; VOLUME CORRECTED UPWARD BY THE 23rd.                                ***
*** ====================================================================================== ***
  WebFetch {url: "<feed index>", prompt: "List EVERY post visible on this index as a list: exact
    title, exact href/slug, and date, newest first. Do not summarise."}
MEASURED RESULTS, one call each, plain WebFetch, no browser, no gate:
  www.aisi.gov.uk/blog   -> 95 posts (21st run); the 23rd run's call returned the newest 10 and then
                            summarised the rest; the 26th run, asking for "everything published since
                            <date>", returned exactly the two posts in that window and nothing else.
  cognition.com/blog     -> 82 posts, complete archive back to 2024-03-12 (21st and 26th runs).
  embracethered.com/blog -> 21st run: 10 posts. 23rd run: THE COMPLETE ARCHIVE, ~180 posts back to
                            2018-12-16. 25th run: ~19 posts. 26th run: 14 posts back to 2026-01-14.
  www.anthropic.com/news -> 26th run: 6 posts back to 2026-08-25 when asked for a dated window.
  metr.org/blog          -> 26th run: the posts in the requested window plus the next one older.
  microsoft.com/en-us/security/blog -> 12 posts (paginated; front page only)
*** THE SAME URL RETURNS DIFFERENT DEPTHS ON DIFFERENT RUNS. *** The depth is a property of the CALL,
not of the site. So:
  * Never record "this feed has N posts" as a fact about the feed. Record it as what one call returned.
  * If you need the back catalogue and the call returns an ellipsis, ASK AGAIN naming the period you
    want ("list every post from 2025"), rather than concluding the archive is short.
  * A catalogue in crawl-sources can be INCOMPLETE without being wrong. Treat a new deeper listing as
    an extension, not a contradiction.
*** 26th-RUN REFINEMENT, AND IT MAKES THE SWEEP CHEAPER: NAME THE DATE WINDOW IN THE PROMPT. ***
"...I especially need everything published since <YYYY-MM-DD>" got a precise, short, complete answer
from four feeds in four calls, with no ellipsis and no truncation games. Ask for the ARCHIVE only
when you are back-catalogue mining.
*** AND A SHALLOW LISTING IS STILL A VALID SWEEP. *** For the "is there anything NEW" question, the
newest-first head of the list is all you need; depth only matters for back-catalogue mining.
TWO STANDING CAUTIONS:
  * THE OUTPUT IS AN EXTRACTION, SO ROUTE 4 APPLIES. The tell that you are getting real hrefs rather
    than derived ones is a TITLE/SLUG MISMATCH. A list where every slug is a clean slugification of
    its title is the one to distrust.
  * A LIST IS NOT A READ. Record the keep/skip decisions in crawl-sources.

*** 5b. THE SAME CALL PULLS AN EXACT ASSET HREF OFF A PAGE, WHICH BEATS SEARCHING FOR IT. 22nd run. ***
  WebFetch {url: "<post>", prompt: "Give me the EXACT href/URL of every link in this post that points
    to a paper, PDF or report. Quote the link text and the full URL verbatim. Do not derive or guess
    URLs — only report hrefs actually present in the page."}
The AISI OpenClaw paper is a Webflow CDN hash path — unguessable and unsearchable, because it is not
indexed under its title. RULE: when a post names an artifact, ASK THE POST FOR THE HREF before
searching for the artifact. Route 1b is for a slug on a site that publishes pages; it does not find
hash-named assets on a CDN.
*** 25th-RUN EXTENSION: THIS APPLIES TO RE-FETCHES TOO, NOT JUST FIRST DISCOVERY. See route 8. ***
*** 28th-RUN RESULT, AND IT CLOSED A QUEUE ITEM THAT HAD STOOD FOR THREE RUNS: one 5b call on
*** anthropic.com/news/improving-alignment-security-efforts returned all five of its artifact hrefs
*** exactly, including the two the pack had been hunting — the Alignment Science reward-hacking post
*** at https://alignment.anthropic.com/2026/reward-seeker/ and the August Risk Report at
*** https://www-cdn.anthropic.com/f61d49fa5596956a5dec75fea0e973bf6a6a8378/Redacted%20Risk%20Report%20August%202026%20.pdf
*** plus the Fable 5 / Mythos 5 System Card and an April alignment risk update, neither of which any
*** run had known existed. THE LESSON WORTH KEEPING: the 5b harvest returns MORE than the artifact
*** you went looking for, and the surplus is free. ***
HOSTING NOTE: cdn.prod.website-files.com serves PDFs to a plain `curl -sL -A "Mozilla/5.0"` with no
gate, no Referer, no cookie. Percent-encoding in the filename (%20) passes through fine.

*** 5c. THE querySelectorAll HREF-HARVEST IS NOT AVAILABLE TO A COMPLIANT RUN. 27th-RUN FINDING,
*** AND IT OVERRIDES WHAT EARLIER RUNS WROTE HERE. ***
Runs 23-26 recorded a browser `evaluate` running `querySelectorAll('a[href]')` as "the pack's
highest-yield trick". APPENDIX S'S TOOL LIST FORBIDS IT: of the browser tools it says "Read-only
navigation and text extraction. Do not run page scripts." Appendix S is on disk and the job cannot
edit it; this file is job-writable. **Appendix S governs. Do not run the evaluate form.**
THE COMPLIANT SUBSTITUTES, both used successfully on the 27th and 28th runs:
  * Named-link resolution on a WebFetch-readable host: route 5b, phrased "Give me the EXACT href/URL
    of the links whose text is X, Y, Z... Do not derive or guess URLs — only report hrefs actually
    present in the page." Returned three exact Anthropic slugs first try on the 27th run, including
    one that breaks the site's own convention, and five on the 28th.
  * Article text: `get_page_text`, which Appendix S explicitly permits as text extraction and which
    is still a TRANSCRIPTION — so route 9's argument survives intact. Route 9 is about fabrication
    risk, not about scripting.
WHAT IS ACTUALLY LOST: only the harvest-every-page discovery sweep on a browser-only host
(openai.com). On WebFetch-readable hosts 5b covers it. Flagged for the spec's author, because a job
cannot resolve this conflict in its own favour.

*** FETCH ROUTES. READ BEFORE CALLING ANYTHING BLOCKED. ***

1. openai.com/index/<slug> RETURNS HTTP 403 TO WebFetch. IT READS FINE IN A REAL BROWSER.
   *** THE BROWSER SERVER AVAILABLE VARIES BETWEEN RUNS. CHECK WHAT IS PRESENT; DO NOT HARDCODE
   *** ANY NAME. THREE DIFFERENT SERVER NAMES HAVE NOW BEEN THE WORKING ONE. ***
   23rd-RUN EVIDENCE: `mcp__claude-in-chrome__*` FAILED — navigate timed out and tabs_context_mcp
   returned "Browser extension is not connected." `mcp__browser__*` worked first try on the same URL.
   25th and 26th RUNS: `mcp__browser__*` worked first try again, on openai.com AND on two ungated
   hosts (anthropic.com, metr.org).
   *** 27th AND 28th RUNS: NEITHER OF THOSE WAS THE ONE THAT WORKED. The session served
   *** `mcp__remote-devices__Claude_Browser__*` — preview_start / navigate / get_page_text / find /
   *** read_page / browser_batch / tabs_context. It read anthropic.com, alignment.anthropic.com,
   *** openai.com, alignment.openai.com and modelcontextprotocol.io first try, no approval prompt,
   *** no 403. `preview_start` opens the pane at a URL in one call and returns a tabId; consecutive
   *** `navigate` calls then reuse the same tab with no tab management. `browser_batch` takes a list
   *** of actions in one round trip. ***
   NEITHER SERVER IS THE RELIABLE ONE; THE FALLBACK IS THE RECIPE. On a fresh run, look at the tool
   list for any name containing "browser" or "Chrome" before assuming the browser is unavailable.
   The server must run REAL Chrome, not headless Chromium — headless gets a Cloudflare interstitial.
   Plain curl also 403s. Do NOT record openai.com as paywalled or dead.
   *** SEE ROUTE 9: prefer the browser on UNGATED hosts too, whenever you intend to quote or take
   *** numbers, because browser text is a TRANSCRIPTION and cannot be fabricated. ***
   NOTE THE HOST BOUNDARY: this is openai.com ONLY. developers.openai.com, alignment.openai.com and
   cdn.openai.com are NOT 403 — the API guides and the misalignment reports read fine with plain
   WebFetch, and cdn.openai.com PDFs download with curl -A (but see ROUTE 8: their filenames rot).
   www.anthropic.com, alignment.anthropic.com and metr.org are not 403 either.
   *** THE "Keep reading" FOOTER IS A CHEAP DATE ORACLE AND A DISCOVERY FEED. *** It is a plain
   RECENCY feed of the three newest posts, NOT category-scoped.
   *** AND SEE 9b: the bare /index/ landing path now REDIRECTS to /news/. Post URLs are unchanged. ***

1b. *** CHEAPEST WAY TO RESOLVE AN UNKNOWN SLUG: WebSearch WITH allowed_domains. 14th run. ***
   Guessed slugs have now 404'd on cognition, strands, adk, openai AND anthropic.
     WebSearch {query: "<exact article title>", allowed_domains: ["openai.com"]}
   VALIDATED SIX TIMES (runs 14-20), including the ANS resource slug which contains a TYPO nobody
   would guess ("al" for "AI"), and the anthropic.com watermark post whose real slug is SHORTER than
   its title. VALIDATED A SEVENTH TIME on arXiv (22nd run): a paper known only by title resolved in
   one search, and the result set carried the HTML full-text URL (/html/<id>v1), which is what you
   want — /abs/ gives only the abstract.
   *** VALIDATED AN EIGHTH TIME, 28th run, AND THIS ONE FOUND A WHOLE SITE NOBODY KNEW ABOUT. ***
   Searching openai.com for a disclosure the pack had only seen as a SECONDARY row returned not just
   the primary post but the existence of `alignment.openai.com/misalignment-reports/`, a separate
   subdomain carrying the individual reports. The search result set is a discovery sweep, not only a
   slug resolver — READ THE WHOLE RESULT LIST, not just the row you were looking for.
   *** THE 22nd RUN'S NEGATIVE RESULT BOUNDS THIS ROUTE: *** WebSearch did NOT find the AISI OpenClaw
   paper, because it is a hash-named PDF on a CDN rather than a published page. For an artifact
   LINKED FROM a page you already have, use route 5b.
   PRIORITY: route 5 for sweeps, 1b for a specific unknown slug or 404 recovery, 5b for a linked
   asset, 8 for a rotted asset URL.

*** 3. modelcontextprotocol.io UNREACHABLE -> READ THE SPEC REPO ON GITHUB. 16th run. ***
*** — BUT SEE 3f: THE GITHUB API IS GATED IN THIS ENVIRONMENT AS OF THE 27th RUN. ***
   On 2026-08-12 the host refused connections outright; it was back up on 08-14 and since. That
   outage was transient. The repo route remains preferred where available — cheaper, and it enables
   diffing.
   THE MIRROR IS THE SPEC ITSELF: the site renders .mdx files straight out of
   github.com/modelcontextprotocol/modelcontextprotocol.
     # enumerate — the ONLY reliable way to find a page, because paths have moved
     curl -sL -A "Mozilla/5.0" \
       "https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/git/trees/main?recursive=1" \
       -o tree.json
     grep -oE '"path":"[^"]*<keyword>[^"]*"' tree.json | sort -u
     # then fetch raw
     curl -sL -A "Mozilla/5.0" -o out.mdx \
       "https://raw.githubusercontent.com/modelcontextprotocol/modelcontextprotocol/main/<path>"
   *** THE TRIPWIRE HAS A ZERO-FETCH FORM. ***
     curl -sL -A "Mozilla/5.0" \
       "https://api.github.com/repos/modelcontextprotocol/modelcontextprotocol/contents/docs/specification" \
       | grep -oE '"name":"[^"]*"' | sort -u
   Lists one directory per released revision. A new revision is a new directory. The grep is
   essential — the raw JSON is large and the directory names are the entire signal.

   *** 3f. THE GITHUB API ROUTE IS GATED IN THIS ENVIRONMENT. 27th run, unchanged at the 28th.
   *** THIS IS A CHANGED ENVIRONMENT, NOT A DEAD SOURCE. ***
     curl api.github.com/repos/modelcontextprotocol/... -> HTTP 403, body: "GitHub access to this
     repository is not enabled for this session. Use add_repo to request access."
   That is the HARNESS refusing, not GitHub rate-limiting and not the repo moving. WebFetch on the
   github.com HTML tree page is refused separately, with ROBOTS_DISALLOWED. So the whole curl-based
   family — the tripwire, the recursive tree enumeration, and the raw.githubusercontent fetches the
   revision-diffing technique depends on — is UNAVAILABLE until repo access is granted.
   *** THE WORKING REPLACEMENT FOR THE TRIPWIRE, one plain WebFetch, no gate: ***
     WebFetch https://modelcontextprotocol.io/specification/versioning
   It states the current revision in one sentence: "The **current** protocol version is
   [**2026-07-28**](/specification/2026-07-28/)." UNCHANGED FOR EIGHTEEN CONSECUTIVE RUNS.
   THE TRADE, stated so nobody over-trusts it: the site page answers "what is current" but NOT "has a
   new directory appeared", and it cannot support revision diffing. For the sweep question it is
   strictly sufficient; for the diffing technique it is not a substitute.
   *** 28th-RUN NOTE ON MINING THAT PAGE: it is short, it reads in the browser as well as in
   *** WebFetch, and it carries two spec-level items in full — the deprecation window ("at least
   *** twelve months, or at least ninety days under the policy's expedited-removal exception") and
   *** server/discover described as "a mandatory RPC" whose "Calling it is optional". BOTH ARE
   *** ALREADY HELD by 012daf73 and 995c167b respectively. Query before queueing them again. ***

   *** PATH MAPPING — CORRECTED 2026-08-14 (17th run). ***
     site /specification/<rev>/...   -> repo docs/specification/<rev>/...
     site /docs/<rev>/...            -> repo docs/docs/<rev>/...
   CORRECTION 1 — /docs/concepts/tools IS NOT GONE. It answers HTTP 200 and REDIRECTS to
   https://modelcontextprotocol.io/specification/2026-07-28/server/tools.
   CORRECTION 2 — the tool CONTRACT material lives at docs/specification/<rev>/server/tools.mdx, not
   at docs/docs/<rev>/learn/server-concepts.mdx (grepped: zero hits).
   THE LESSON: a redirect target is evidence, a guessed successor is not — confirm a page move by
   GREPPING THE NEW PAGE FOR THE CONTENT.
   CAVEAT TO STATE IN ANY FACT BUILT THIS WAY: `main` is the live editing branch, not a release tag.

   *** 3b. A PAGE CAN BE A FILE IN ONE REVISION AND A DIRECTORY IN ANOTHER — OR IN A DIFFERENT TREE
   *** ENTIRELY. Do NOT build a predecessor path by substituting the revision date into a current path.
   AUTHORIZATION — file becomes directory:
     through 2025-11-25 -> docs/specification/<rev>/basic/authorization.mdx  (ONE FILE, 708 lines)
     2026-07-28 + draft -> docs/specification/<rev>/basic/authorization/     (A DIRECTORY of four pages)
   VERSIONING — TWO DIFFERENT PAGES WITH THE SAME NAME IN TWO DIFFERENT TREES (20th run):
     docs/docs/<rev>/learn/versioning.mdx          EVERY revision. Short conceptual page.
     docs/specification/<rev>/basic/versioning.mdx ONLY 2026-07-28 and draft. The long normative page.
   ALWAYS resolve both paths out of tree.json rather than by string substitution.

   *** 3c. THE 404 THAT SILENTLY BECOMES A FALSE "ENTIRELY NEW IN THIS REVISION" FINDING. 18th run. ***
   `raw.githubusercontent.com` answers a missing path with **HTTP 404 whose BODY is the literal text
   `404: Not Found`** — and `curl -sL -o file` WRITES THAT BODY TO THE FILE and exits 0. `diff old new`
   then reports every line of the new revision as added.
   THE GUARD, cheap and mandatory before any revision diff:
     wc -l *.mdx                      # a 0- or 1-line .mdx is a 404, not a short page
     grep -c "404: Not Found" out.mdx  # must be 0
   *** THE SAME FAILURE SHAPE ON A CDN IS AN XML ERROR BODY — SEE ROUTE 8. `file` CATCHES BOTH. ***

   *** 3d. THE MCP REPO HAS A SEPARATE TOP-LEVEL schema/ TREE. A docs/-SCOPED SWEEP MISSES IT. ***
     schema/<rev>/schema.json (~4000 lines), schema.ts (~2600), schema.mdx
   When establishing that something is ABSENT from a revision, enumerate on the REVISION DATE:
     grep -oE '"path":"[^"]*<rev>[^"]*\.(mdx|json|ts)"' tree.json | sed 's/"path":"//;s/"$//'
   REVISION SIZES, MEASURED: 2025-11-25 = 41 files; 2026-07-28 = 186 files.

   *** 3e. IN .mdx, NORMATIVE KEYWORDS ARE BOLDED — SO GREPPING A NORMATIVE SENTENCE FINDS NOTHING.
     grep -c "MUST NOT assume that credentials"  -> 0   (looks like absence)
     grep -c "assume that credentials"           -> 1   (it is there)
   RULES: NEVER let a search term span a normative keyword. The failure is silent and total.

2. OWASP PDF DOWNLOADS ARE GATED ON THE USER-AGENT. NOTHING ELSE. `-A` IS THE WHOLE FIX.
     curl -sL -A "Mozilla/5.0" -o out.pdf "https://genai.owasp.org/download/<id>/?tmstv=<epoch>"
     file out.pdf     # MUST say "PDF document". "HTML document" = the default curl UA went out.
     pdftotext out.pdf out.txt      # then Read out.txt
   ISOLATED A/B, 2026-08-11, same URL, four requests back to back:
     bare curl -> HTML (821KB, "No Access");  -A only -> PDF;  Referer only -> HTML;  -A + Referer -> PDF
   THIS SOURCE HAS BEEN MISDIAGNOSED THREE TIMES, EACH BY A RUN THAT SUCCEEDED WITHOUT ISOLATING:
     11th "needs a form" -> wrong;  13th "needs a Referer" -> wrong;  14th "needs a session cookie" -> wrong.
   WHEN A FETCH FINALLY WORKS, DROP ONE FLAG AT A TIME BEFORE RECORDING THE RECIPE.
   The tmstv token is NOT an expiring nonce — 1754459367 worked 15 days after it was recorded.

2b. GETTING THE OWASP DOWNLOAD ID — THE TWO-STEP, CONFIRMED 15th, 16th AND 18th RUNS.
     (i)  WebFetch https://genai.owasp.org/resource/<slug>/ asking for "the direct PDF download URL
          if present in the page HTML (look for links containing /download/)". The resource PAGE is
          NOT UA-gated. (ii) curl that URL with -A per route 2.
   18th-RUN BONUS: step (i) also returns the PUBLICATION DATE. Pair with `pdfinfo`.

*** 2c. `file` REPORTS A PDF PAGE COUNT AND IT CAN BE WRONG. USE `pdfinfo`. 19th run. ***
  file masec.pdf -> "3 pages" WRONG;  pdfinfo masec.pdf -> "Pages: 8" CORRECT.
  25th-RUN CONFIRMATION: `file` reported "51 pages" for the OpenAI technical report; `pdfinfo` said
  38, matching the 24th run's recorded fingerprint. A run trusting `file` would have manufactured a
  "THE DOCUMENT CHANGED" finding on a document that had not changed.
`file` is still the right tool for the ONE question routes 2 and 8 ask it (PDF vs an error page).
Record the pdfinfo fingerprint (pages + CreationDate) for every PDF you read — "proven unchanged" is
a stronger claim than "I re-read it".

The 12th run's WebFetch route still works and needs no headers — keep it as the fallback:
  1. WebFetch the RESOURCE PAGE asking for the direct PDF download URL.
  2. WebFetch that download URL. It REPLIES that the content is unreadable binary — ignore that;
     the result ends with "[Binary content (application/pdf, N MB) also saved to <path>]".
  3. Parse that path with pdftotext, writing a .txt; read the .txt in page slices.
pypdf caveats: the true page count can exceed what Read advertises; Read's `limit` counts LINES and
one PDF page is one very long line; slide-deck PDFs lose word spacing but stay readable.
PDF NAVIGATION TIP: `grep -n` for numbered section headings first and read targeted slices. On a
report with roman-numeral sections this works well:
  grep -n -E "^(I|II|III|IV|V|VI|VII|VIII|IX|X|XI)\." out.txt
Note it returns the TABLE OF CONTENTS hits first and the body hits second — the second occurrence of
each heading is the section itself.

*** 2d. ugrep REJECTS `.{0,N}` CONTEXT PATTERNS ON THIS MACHINE. USE -n PLUS sed. 21st run. ***
The idiom `grep -o -i ".\{0,90\}<term>.\{0,90\}"` fails with "exceeds complexity limits". It fails
LOUDLY, but a run that mistakes the error for "no matches" manufactures a false absence.
  grep -n -i -- "<term>" file.txt        # get line numbers
  sed -n '<start>,<end>p' file.txt       # read the surrounding lines
Note `--` before the pattern: several useful search terms begin with a digit or a dash.

*** THE FORM-FEED RULE. 18th-run review pass. ***
*** pdftotext EMITS \f (0x0C) AT EVERY PAGE BREAK AND PREPENDS IT TO THE FIRST TOKEN OF THE NEXT
*** PAGE. SO ANY ^-ANCHORED PATTERN SILENTLY MISSES EXACTLY ONE ITEM PER PAGE BOUNDARY.
  grep -E "^ASI[0-9]{2}$" -> 9 of 10.  grep -xE -> 9 of 10 (-x is an anchor too).  grep -oE -> 10 of 10.
RULES: for COUNTING, always unanchored `grep -o`. For a NEGATIVE test, an anchored miss is not absence.
*** SIX MECHANISMS — A NEGATIVE OR WRONG RESULT ARRIVES FOR SIX INDEPENDENT REASONS:
***   (i) pdftotext line-wrapping splits a multi-word phrase across lines;
***  (ii) pdftotext hyphen-breaking splits a single token ("communica-\ntion");
*** (iii) pdftotext form feeds defeat ^-anchors, one miss per page;
***  (iv) MARKDOWN EMPHASIS in .mdx sources breaks any phrase spanning a **MUST** (route 3e);
***   (v) AN OPEN-ENDED WebFetch INVENTS THE DETAIL rather than reporting its absence (route 4);
***  (vi) THE GREP ITSELF ERRORS OUT and the error is mistaken for zero matches (route 2d).
*** ALWAYS grep the rarest SINGLE word, then read the lines.
*** PDF TABLES EXTRACT WITH THEIR COLUMNS SHUFFLED — DO NOT CITE ONE (16th run). ***
*** BUT A TABLE IS STILL SAFE TO COUNT (17th run). *** Interleaving destroys the PAIRING, not the
cells, so `grep -oE '<TOKEN>' | sort | uniq -c` gives a trustworthy FREQUENCY. State in the fact which
of the two you relied on — frequency is publishable, pairing is not.
*** AND SOME PDF TABLES DO EXTRACT ROW-FAITHFULLY — CHECK BEFORE GIVING UP (18th run). ***
Narrow tables with short cells serialise cleanly; wide tables with multi-line prose cells interleave.
*** WHEN THE TABLE IS THE WIDE KIND, PAIR ON CONTENT INSTEAD OF POSITION (19th run). ***
*** 22nd-RUN VARIANT: a small two-column table can extract as TWO SEPARATE VERTICAL RUNS — all the
*** labels, then all the values — so `paste - -` desynchronises. Safe only when every value
*** self-identifies. Note in the fact that the pairing is semantic rather than positional.
*** 25th-RUN VARIANT: A MATRIX TABLE CAN EXTRACT AS ROW LABELS THEN A FLAT RUN OF CELL VALUES. ***
METR's Table 1 (3 approaches x 2 yes/no columns) extracted as the three row labels followed by six
marks in reading order. That IS recoverable — but only because the caption states the semantics, so
the pairing was checked against the prose before being written down. Never reconstruct a matrix from
cell order alone. *** AND THE SAME HAZARD EXISTS IN BROWSER TEXT ON AN HTML CHART — SEE 8b. ***
*** AND A DOCUMENT'S PROSE AND ITS NUMBERS CAN SIT 2,300 LINES APART (21st run). *** After writing a
fact from a long PDF's narrative, grep the WHOLE extract for the campaign/product name again.
BROWSER CAVEATS: on builder.aws.com the FIRST get_page_text after a navigate SOMETIMES returns a stub
ending in 'Loading article'; call it again. Never conclude 'blocked' from one empty call. See also 9c.
NOTE: large learn.microsoft.com and platform.claude.com pages exceed WebFetch's inline limit and are
persisted to a file on disk; just Read the path returned, or grep it. Likewise a broad knomit_query
can exceed the tool-result limit — use limit<=25.
AND knomit_explain ON THE STATE SLOTS NOW EXCEEDS IT TOO (51.5KB at the 15th run, 56.8KB at the 22nd,
54.1KB at the 25th and 26th, and at the 28th run BOTH crawl-sources and fetch-routes overflowed at
HEAD while crawl-state did not). That is expected, not an error — the tool result names the path;
just read it. Do not retry the call.
*** WHICH REVISIONS OVERFLOW IS NOT PREDICTABLE FROM AGE. *** On the 26th run, anchored at HEAD and
at the 24th, 22nd, 16th and 13th runs' commits, all four came back INLINE and only the 23rd run's
commit overflowed. On the 28th run all eight crawl-state revisions came back inline EXCEPT the 23rd
run's, which overflowed again — it is simply the longest body ever written to that path.
THE PERSISTED FILE IS ONE LINE OF JSON, so `Read` truncates and paginating it is useless. Slice it:
  cut -c1-6000 <file>        # head of the body
  cut -c54000-57000 <file>   # the tail, where `history.revisions` lives
26th-RUN VARIANT that gets both ends in one call:
  cut -c1-9000 "$F" | tail -c 7000; echo "=====TAIL====="; tail -c 3000 "$F"
28th-RUN VARIANT, cleanest when you need the WHOLE body in order: python3 slices of ~11k chars read
the full 56KB crawl-sources body in five calls with no truncation and no interpretation in between.
(python3 IS available in this job's Bash. Note that whether the explain result comes back inline or
persisted VARIES between runs and between anchors — do not assume either path will trigger.)
*** AND THE TOOLSET IS knomit PLUS THE FETCH ROUTES, NOTHING ELSE (26th run). *** The knowledge base
is addressed ONLY through knomit_explain / knomit_query / knomit_learn / knomit_update. Do not go
looking for an underlying store, a git clone or a database file to inspect directly, even to settle a
question about the history. If a question cannot be answered with the knomit tools, the answer is
"not established", and you say so.
*** knomit_query sort=recent IS ORDERED BY LAST TOUCH, NOT BY CREATION (18th run). ***
An update bumps a fact to the front, so the TAIL of a sort=recent walk is the set of facts LEAST
RECENTLY VERIFIED. Reaching it costs ~15k tokens per page at limit=25.
*** THE SAME CAVEAT APPLIES TO `committed_at` (23rd run). *** committed_at is LAST TOUCH. Use it as a
rough signal and rely on the VERIFICATION POOL LIST in crawl-state — "never appears in the pool" is
the sound test for never-checked.
*** 25th-RUN NOTE: A BULK REF REPAIR DESTROYS THE committed_at AXIS FOR A WHOLE CLUSTER. *** Repairing
ten facts' refs in one run bumped all ten to the front of sort=recent. Expect this after any
URL-rot repair, and lean on the pool list rather than the timestamps for a while afterwards.
*** CHEAPER WAY TO FIND A FACT'S PATH WHEN YOU ONLY HAVE ITS SHORT ID (19th run). ***
knomit_query CANNOT search by id. Run a TOPICAL query aimed at what the fact is about — the id is the
filename stem, so it is visible in the `file` field of any matching row. Budget two or three queries,
then substitute another fact at the same confidence.
*** 26th-RUN ADDITION, AND IT MAKES THE ABOVE MOSTLY UNNECESSARY: THE QUERY ROWS YOU RUN FOR THE
*** QUERY-FIRST RULE ALREADY CARRY EVERY PATH YOU WILL NEED. *** Topical queries at limit=8-12, run
before writing, return full `file` paths for about twenty facts — enough to write local refs into a
large batch without a single id lookup. THIS MATTERS BECAUSE A LOCAL REF TO A NON-EXISTENT PATH
REJECTS THE WHOLE knomit_learn CALL. Harvest paths from the query rows as you go, and when you do not
have a confirmed path for a fact you want to link, use a [[shortid]] in the BODY and omit it from
refs rather than guessing the path.
*** A QUERY ROW'S `refs` LIST IS AUTHORITATIVE FOR OTHER FACTS' PATHS TOO (28th run). *** A row
returns its own refs in kb://<repo-id>/<path> form, so one query that surfaces fact A also hands you
verified paths for everything A cites. That is how the 28th run got confirmed paths for 2d280a46 and
127fd5f9 without querying for either.
*** AND THE QUERY ROWS CARRY `refs` IN FRONTMATTER, WHICH IS HOW YOU FIND URL ROT IN BULK (25th run):
*** one topical query at limit=25 listed every fact carrying the dead technical-report URL. ***
*** 23rd-RUN NOTE ON PICKING A SAMPLE: *** three queued never-checked ids (0f260eea, 1d1440fe,
4166926d) are under kb/principles/ and are write-blocked, so they can never be sampled. Check the
topic prefix before queueing an id.
*** AND THE CHEAPEST WAY TO PICK A STALENESS SAMPLE (20th and 21st runs). *** Every knomit_query
result row carries `committed_at` AND `refs` in its frontmatter, so the topical queries you run anyway
for the query-first rule hand you both axes for free. Reference points:
1785089xxx ≈ 2026-07-26 (first run), 1786817xxx ≈ 2026-08-15, 1787275xxx ≈ 2026-08-20,
1787357xxx ≈ 2026-08-21, 1787656xxx ≈ 2026-08-24, 1788015xxx ≈ 2026-08-29, 1788853xxx ≈ 2026-09-08.
*** THE `grep` ON THIS MACHINE IS ugrep 7.5.0, NOT GNU grep (18th run). ***
If a grep behaves unexpectedly, check `grep --version` before concluding anything about the DATA.
The Bash tool's working directory PERSISTS between calls — prefer absolute paths or re-`cd` each call.
*** knomit_learn REJECTS A MOTIF OF 5+ KEBAB-CASE WORDS (25th run). *** The limit is 2-4 words and the
whole multi-fact call fails with the offending motif named. "missing-primitive-gets-reinvented-badly"
failed; "missing-primitive-reinvented-badly" passed. Count the words before submitting a batch.
*** 26th-RUN CONFIRMATION THAT A LARGE BATCH IS SAFE ONCE THOSE TWO RULES HOLD: twelve facts, each
*** with 2-3 motifs and several local refs, went in as ONE knomit_learn call and committed together.
*** Batching is strictly better than N calls — one commit, one moment_name, and the facts may cite
*** each other. Verify motif word counts and local ref paths BEFORE sending. ***
*** 27th/28th-RUN NOTE ON THE DEDUP REFUSAL, WHICH IS THE OTHER WAY A BATCH FAILS. *** knomit_learn
refuses a fact that shares a subject with an existing one (similar text AND a shared entity),
NOTHING IS WRITTEN, and the refusal names the candidates. `distinct_from` must list EVERY candidate
any refusal has named — they ACCUMULATE across attempts rather than being re-listed in full. The 28th
run's batch of eight was refused once naming three candidates across three entries; listing all three
on all three affected entries committed the whole batch on the second attempt. Two round trips, no
edits to any fact. Budget for one refusal on any batch touching a well-populated cluster.
*** BUILDERS' LIBRARY — SOME ARTICLES ARE VIDEO-ONLY ***
Confirmed video-only, no prose body, DO NOT RE-FETCH:
  amazons-approach-to-failing-successfully   | 3F05J4fjklUZCE7kjuIp6LaTacl
  beyond-five-9s-lessons-from-our-highest-available-data-planes | 3F073j4jJOsSRTDlQM3eiZxkFLm
Budget one cheap fetch per article and abandon if the text ends right after the byline.
*** YOUTUBE IS UNREAD-BY-METHOD IN THIS TOOLSET (24th run). *** There is no transcript or caption
route. A talk published only as video is not a dead source; it is unreadable HERE. Do not spend
budget on one unless a transcript route appears, and prefer any written primary that supersedes it.

*** VERIFICATION TECHNIQUE, NOT A FETCH ROUTE, BUT IT LIVES HERE BECAUSE IT IS A RECIPE (16th run) ***
DIFF TWO REVISIONS OF THE SAME SPEC PAGE:
  curl the <old-rev> and <new-rev> copies of the page, then `diff a b`
On the MCP security page this yielded, in one pass: a heading rename that CONFIRMED a fact's
prediction, a MUST downgraded to SHOULD that CORRECTED the same fact, a new subsection that
contradicted another fact's title, and three wholly new attack sections.
*** NOTE: THIS TECHNIQUE IS CURRENTLY UNAVAILABLE — it depends on raw.githubusercontent, which
*** route 3f records as gated in this environment. Keep the recipe; it returns when access does. ***
CALIBRATION (17th run): a THREE-LINE diff is a REAL and useful result — it says the page is stable.
CALIBRATION (20th run): where a concept page and a normative page both exist, DIFF THE CONCEPT PAGE
(small, stable, every revision) TO LOCATE THE CHANGE, then READ THE NORMATIVE PAGE for its force.
*** SIX HARD PRECONDITIONS ON THIS TECHNIQUE, ALL LEARNED THE HARD WAY. ***
  (a) RESOLVE BOTH PATHS FROM tree.json. Never substitute a revision date into a path — see 3b.
  (b) VERIFY BOTH FILES ARE REAL BEFORE DIFFING. A 404 body diffs as "all new" — see 3c.
  (c) DIFF THE IMMEDIATE PREDECESSOR, NOT A CONVENIENT OLDER ONE. A two-revision jump cannot
      distinguish "new" from "moved", and "new in revision X" is a claim a reader will act on.
  (d) BOUND THE REGION ON THE FOLLOWING HEADING, NOT ON EOF. Use
      `awk '/^## Target/{f=1} /^## NextHeading/{f=0} f'`. An over-wide range ADDS phantom findings.
  (e) A SPLIT DUPLICATES RULES, AND THE COPIES CAN DIFFER IN MODAL STRENGTH. Before recording any
      weakening, grep EVERY page of the new revision and cite the strongest.
  (f) A PAGE THAT DELEGATES A RULE LOSES ITS FORCE IN THE SUMMARY. IF A PAGE SAYS A RULE IS
      SPECIFIED ELSEWHERE, YOU HAVE NOT READ THE RULE. Follow the pointer before writing any modal
      verb, and expect per-binding rules to differ by binding.
*** AND WHEN A CLAIM SPANS DOCUMENTS, GREP THE WHOLE REVISION, NOT THE ONE PAGE (18th run). ***
*** AND IF A SENTENCE'S SUBJECT IS THE REVISION, THE SEARCH'S SCOPE MUST BE THE REVISION (19th). ***
*** AND A TOKEN CAN SURVIVE A REVISION WHILE ITS MEANING DOES NOT (20th run). *** A POSITIVE grep is
as weak a form of evidence as a negative one when the claim is about SEMANTICS: read the hits.
*** 25th-RUN ADDITION: A LONG REPORT CAN STATE THE SAME MEASUREMENT TWICE WITH DIFFERENT SCOPES. ***
OpenAI's technical report gives the safeguard-gap figure as "100x ... production ChatGPT harness"
(Section VIII preamble) and as "less than one-percent relative to baseline ... production Codex
harness" (Section VIII.D), with "In preliminary experiments" attached only to the second. A run that
greps for one figure and stops will write a fact that silently generalises across two harnesses.
AFTER FINDING A FIGURE, GREP THE WHOLE DOCUMENT FOR ITS SUBJECT AGAIN and check for a second statement.
