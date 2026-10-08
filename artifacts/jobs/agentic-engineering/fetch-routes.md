---
type: observation
domain: []
confidence: 0.7
sources: 1
entities: []
refs: []
---
# agentic-engineering crawl: per-host fetch routes and tool caveats

type: reference / job-state. Per-host fetch recipes and tool caveats for the agentic-engineering crawl.

*** READ THIS FIRST. THIS SLOT IS A CONTINUATION, NOT THE WHOLE FILE. ***
ROUTES 1 THROUGH 31 AND EVERY HOST RECIPE LIVE AT THE OLD PATH AND ARE STILL FULLY READABLE:
    knomit_explain(file=".knomit/jobs/agentic-engineering/fetch-routes.md")
98,223 characters, last revision c48215b69eb6c9166ee9afbd1744d9a13f825705. READS WORK NORMALLY THERE.
WRITES DO NOT — see the migration note below. Every run must read BOTH: the old path for routes 1-31 and
the host recipes (openai.com 403 browser route, the OWASP User-Agent gate, the CDN egress denials, the
oversized-slot reading recipe, the motif validator's token limit), and this slot for route 32 onward.
Nothing was copied, so nothing was truncated in the move.

=== MIGRATION, 48th RUN (2026-10-07). THE REASON THIS SLOT EXISTS. ===
The fact tools now REFUSE every write under .knomit/. Verbatim refusal on a knomit_update to
.knomit/jobs/agentic-engineering/fetch-routes.md:
    ".knomit/jobs/agentic-engineering/fetch-routes.md is private: a path with a segment beginning with '.'
     is closed to the fact tools: .knomit/ is the system (ontology, triggers, recipes, skills) and changes
     only through git, and other dot paths are not knowledge; write an agent's working file under
     artifacts/<area>/ instead"
Reads at those paths still succeed — all three old slots were read in full this run. So the old content is
preserved and reachable; only appending is gone. The server's bind-time instructions now name
artifacts/<area>/ as the job-writable namespace, and artifacts carry the same invisibility that mattered:
excluded from knomit_query, knomit_changes, triggers, the UI and export.
THE PROPERTY THE SPEC CARED ABOUT IS PRESERVED, AND IS NOW STRONGER. The spec puts job state in a
namespace the job can write and keeps the spec itself out of the corpus, so a crawler reading untrusted
web pages cannot edit its own instructions. That still holds: the spec reaches the job only in its prompt,
and nothing normative is in this slot. .knomit/ becoming read-only also means the ontology is now beyond
the job's reach entirely, which is a tightening, not a loss.
WHAT A HUMAN NEEDS TO DO: Appendix S's "Job state" section still names the three .knomit/ paths and says
they are job-writable. That is now false for writes. The paths in the spec need changing to
artifacts/jobs/agentic-engineering/*.md, and the spec's stated rationale ("everything under
.knomit/<area>/ is structurally writable by the job") needs replacing, because it no longer describes the
server. Until the spec is edited, a run should expect the refusal, not treat it as a failure.

=== ROUTE 32 (48th run). *** THE EXTRACTION LAYER FABRICATES NUMBERS — CAUGHT IN THE ACT ON A FIGURE THIS RUN WAS ABOUT TO WRITE. ROUTE 28 IS NO LONGER A PRECAUTION, IT IS A MEASURED NECESSITY. *** ===
The open-ended WebFetch read of anthropic.com/research/glm-5-3-and-the-spread-of-advanced-cyber-capabilities
returned, as the abliteration refusal-rate drops:
    "JailbreakBench: reduced from 95% to 6%; HarmBench: reduced from 95% to 6%; StrongREJECT: 95% to 12%"
The targeted verbatim call on the SAME URL in the SAME run returned the page's actual sentence:
    "The edit took GLM-5.3's refusal rate from above 90% to about 3% and 2% on the first two benchmarks
     (JailbreakBench and HarmBench) and to 12% on the third (StrongREJECT)."
FOUR of the six numbers were wrong. 95% is a fabricated precision for "above 90%"; 6% and 6% are wrong
for 3% and 2%. ONLY THE 12% SURVIVED — which is exactly the trap, because one matching figure makes the
whole set look verified. The errors all run the SAME DIRECTION (rounder, more symmetric, more quotable),
so this is regularisation of a hedged sentence into a tidy one, not noise.
THE RULE, ABSOLUTE: *** NEVER WRITE A NUMBER THAT CAME FROM AN OPEN-ENDED EXTRACTION. *** The open-ended
call decides WHETHER a document is worth a fact and WHAT the fact is about. Every figure that lands in a
body comes from a second call asking for the sentence verbatim. One extra call per document.
DETECTION SIGNATURE, so a future run can smell it before spending the second call: suspiciously round and
suspiciously symmetric figures (95/95/95, 6/6) inside a source that hedges elsewhere ("above 90%",
"about"). A source careless enough to write 95% three times would not have written "above 90%" once.
AND THE VERBATIM CALL IS NOT ONLY A CHECK — IT IS OFTEN WHERE THE BETTER FACT IS. This run it ADDED a
datapoint the open-ended read dropped entirely ("Abliterating GLM-5.3-Flash took about 600 GPU hours") and
a success count the open-ended read of the CVP page omitted ("successfully completed 34 of the 50 tasks"),
which turned a one-sided block-rate observation into a two-sided cost measurement and made the fact.

=== ROUTE 33 (48th run). A SUMMARISING ANSWER'S *COUNT* IS UNRELIABLE; ITS *ENUMERATION* IS SOUND. ===
alignment.openai.com/misalignment-reports/, windowed-sweep prompt, one call: the answer stated "The page
documents 12 total reports spanning from January 2025 through September 2026". A second call on the same
URL asking ONLY to enumerate every entry with title, slug and date returned exactly ELEVEN, every one
already in ALREADY_CRAWLED. There was no twelfth report.
SO: when a sweep's value turns on "is there anything new", never act on a stated total — ask for the
enumeration. An enumeration can be SHALLOW (route 5) but it does not invent rows; a count does.
DEPTH-VARIES, THIRD MEASUREMENT ON ONE URL: alignment.anthropic.com's index has returned 8 entries (45th
run), 62 (46th and 47th) and 79 (48th), every time with a date window in the prompt. 79 extends 62 rather
than contradicting it, and it means NEITHER number is the archive's size. Record what one call returned on
one date; never the feed's "size".

=== ROUTE 34 (48th run). knomit_explain RETURNS A `blob` FIELD, AND IT IS THE RIGHT INSTRUMENT FOR BYTE-IDENTITY BETWEEN REVISIONS. ===
Established by this run's read-only history-walk subagent. Each explain result carries `blob` (the git blob
SHA of the body) and `size`. Two revisions with the same blob are byte-identical; this is exact, costs
nothing extra, and replaces diffing or eyeballing two bodies. Used it to settle four pairs plus the
standing 39th-run question in one pass (see crawl-state).
COROLLARY, AND IT CORRECTS A CARRIED LIST: the "four known oversized" commits are not a fixed set. d56dc137
and 68c341e1 returned INLINE this run at 48,482 chars each, while 22649951 (53,298), 66535f3f (50,309) and
7462e9f2 (52,873) persisted to file. The threshold sits near 50KB and moves. A brief that names specific
commits as oversized misleads in both directions — say "persist and extract whatever comes back as a file"
instead.

=== ROUTE 35 (48th run). THE MCP BRIDGE DROPS AND RECOVERS ON A BARE RETRY. DO NOT RE-BIND. ===
One call during the history walk failed with `dial tcp 127.0.0.1:19278: connect: connection refused`. An
immediate identical retry succeeded with the same handle. The transport is the fragile part, not the
binding. Re-binding on a connection error would be the wrong reflex and mints a second handle for nothing.
SEPARATELY, AND NOT A DRIFT: the repo CATALOGUE changed mid-run. The first knomit_repos of this run listed
5 repos; the pre-write call listed 6, with `knomit-playbooks` (034f37d5b4a5) new. The binding was unchanged
and correct both times (one mount, agentic-engineering, read+write). So knomit_repos' catalogue is live and
a new row appearing is not route 10. Check `bound.binding`, not the repo count.

=== ROUTE 36 (49th run). *** knomit_explain ANCHORED AT AN EXPLICIT `commit` RETURNED NO `history` OBJECT AT ALL -- 37 CALLS, 37 TIMES. AND THIS CONTRADICTS THE 48th RUN'S MEASUREMENT, SO BOTH ARE RECORDED. *** ===
This run's read-only subagent made 37 anchored calls of the form
    knomit_explain(file=".knomit/jobs/agentic-engineering/crawl-state.md", commit="<40-hex>")
and reported that EVERY one came back as a single node of kind "system_file" carrying `blob`, `size`,
`content` and `superseded: true`, with NO `history` key, no `revisions`, no `diff` and no
`more_available`. Not a short chain -- absent.
THE 48th RUN MEASURED THE OPPOSITE on the same path with the same kind of call, recording that
"more_available was true on every read except the floor's". Both runs used a subagent, both reported 0
failures, and both reproduced the same byte-comparisons, so neither looks careless.
THE DISAGREEMENT IS NOT RESOLVED AND MUST NOT BE FLATTENED. Two candidate explanations, neither tested:
  (a) a server change between 2026-10-07 and 2026-10-08;
  (b) the response shape differs by whether the body is served inline or persisted to a file, and the two
      runs had different oversized sets (route 34's corollary says that set moves).
WHAT TO DO, WHICH IS THE SAME EITHER WAY AND IS WHY THIS COSTS NOTHING TO LEAVE OPEN: walk by the prose
hash list, never by history.revisions. If the history object is absent the documented protocol cannot run
at all; if it is present it terminates early. The prose list is the only mechanism under both readings.
ONE CHEAP TEST FOR A FUTURE RUN: make one anchored call yourself, in the main session rather than in a
subagent, and record whether `history` is present and whether the body came back inline. That single
datapoint distinguishes (a) from (b) and would retire this route.

=== ROUTE 37 (49th run). *** THE VERBATIM CALL -- ROUTE 32'S OWN INSTRUMENT -- TRUNCATES EACH QUOTE AT ~125 CHARACTERS AND THEN PARAPHRASES THE REST WITHOUT MARKING IT AS PARAPHRASE. *** ===
Route 32 says never write a number from an open-ended extraction and to get the sentence verbatim instead.
This run measured a limit on that remedy. A single targeted call asking for nine passages from
aisi.gov.uk/blog/transect-... returned three of them cut mid-sentence with an explicit note, e.g.:
    "Rerunning the same analysis also requires retaining the transcript, category definitions, settings,"
    (truncated to the 125-character limit; the sentence continues with "custom analysis code and software
     versions.")
THE TAIL AFTER THE NOTICE IS THE SUMMARISER'S RECONSTRUCTION, NOT THE PAGE'S TEXT. It is offered in the
same breath as the verbatim part and in quotation marks. So a long "verbatim" quote is part transcription
and part exactly the thing route 32 forbids, and the seam is marked only by a parenthetical that is easy
to read past.
THE RULE: ASK FOR THE SHORT DISTINGUISHING CLAUSE, NOT THE WHOLE SENTENCE. If a claim needs a compound
condition quoted in full (and this pack's quality bar often does -- see 012daf73's "twelve months / ninety
days"), split it across two or three numbered asks of under ~120 characters each rather than one long one.
AND TREAT ANY CONTINUATION THE TOOL SUPPLIES AFTER A TRUNCATION NOTICE AS UNVERIFIED: either re-ask for
that clause on its own, or write the fact around the part that was actually returned.
THIS IS DISTINCT FROM ROUTE 31 (WebFetch stopping at 100,000 characters of the PAGE). That is a page-length
cap that announces itself and is pageable with `offset`. This is a per-QUOTE cap inside the answer, it is
not pageable, and what it hands you in place of the missing text is generated.

=== ROUTE 38 (49th run). ROUTE 32'S FABRICATION CLASS EXTENDS TO ENTITY ATTRIBUTION, AND THAT IS THE WORST SUB-CLASS YET BECAUSE IT READS AS CORROBORATED. ===
Route 32 caught fabricated NUMBERS; the 47th run's widened rule covers filenames, ranges and counts. This
run adds an organisation name. The open-ended read of
metr.org/blog/2026-10-06-ai-systems-could-cover-up-misbehavior/ reported the Inspect transcript viewer as
"developed by the UK AI Security Institute". The verbatim call returns only:
    "Meridian Labs, the team behind Inspect, patched the vulnerability within one day of reporting."
The page says nothing about who originally authored Inspect. Inspect IS widely associated with UK AISI,
which is precisely why the summariser supplied it.
*** WHY THIS SUB-CLASS IS THE DANGEROUS ONE: a fabricated number is checkable against the page and looks
*** wrong the moment you look. A fabricated attribution is checkable against the WORLD, where it is
*** plausible or even true, so a reviewer's background knowledge CONFIRMS it and the fabrication survives
*** review. The defect is not that the claim is false; it is that the SOURCE did not make it, which is
*** what a ref asserts. ***
THE RULE: verify verbatim every org-to-artifact attribution you are about to put in a body or an entities
list -- who built it, who maintains it, who funded it, who disclosed it. If the page does not say, the fact
does not say, and the body should state that the source is silent rather than leaving a gap a later run
fills in. Applied this run: 9cd59af4's enrichment names Meridian Labs as "the team behind Inspect" and adds
an explicit line telling future readers not to fill in original authorship.

=== ROUTE 39 (49th run). A "See more" / "Load more" CONTROL MAY BE A DEAD PLACEHOLDER. CHECK ITS href BEFORE QUEUEING THE DEPTH BEHIND IT. ===
www.anthropic.com/research returns 10 entries and a "See more" link. The 47th and 48th runs both inferred
real depth behind it (correctly) and queued "the See more depth" as a target (uselessly): its href is `#`.
There is no next page to fetch and no pagination parameter to guess, so two runs carried a queue item that
could never be executed as written.
THE ASK THAT SETTLES IT IN THE SAME CALL AS THE SWEEP, at no extra cost: when asking an index for its
entries, also ask "is there a See more or pagination link, and what is its target URL?". A `#`, a
`javascript:` scheme, or no href at all means the depth is client-side or absent, and the only routes
onward are (a) another page that links the older items directly, or (b) a known-slug list.
FOR THIS SPECIFIC CASE THE ANSWER IS (a) AND IT IS ALREADY IN HAND: the alignment.anthropic.com index links
17 older anthropic.com/research slugs directly. That is the route to /research depth. See crawl-sources.
GENERAL FORM, and it is the counterpart to route 5's depth-varies caution: route 5 says one call may
under-report a listing's depth. This says a visible affordance for MORE depth may not be wired to
anything. Neither the count nor the control is evidence; only a URL that resolves is.
