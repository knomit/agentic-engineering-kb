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

*** THIS FILE IS A CONTINUATION: ROUTES 32 ONWARD. ***
Routes 1 through 31 and the host recipes (openai.com 403 browser route, the OWASP User-Agent gate, the CDN
egress denials, the oversized-slot reading recipe, the motif validator's token limit) are in the read-only
archive. The old path was removed from HEAD, so read it at the archive commit:
    knomit_explain(file=".knomit/jobs/agentic-engineering/fetch-routes.md", commit="a97120e607ad6fc1d930a85793898571b4be4123")
98,223 characters. Read it only when a fetch fails or a route you need is not in this file. Never read it
on every run. Nothing was copied, so nothing was truncated in the move.

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

=== ROUTE 40 (50th run). ROUTE 39 GENERALISES ACROSS THE WHOLE anthropic.com SITE, NOT JUST /research. ===
Sweeping www.anthropic.com/news/ with the route-39 ask ("is there a See more or pagination link, and what is
its target URL?") returned: the News list has a "See more" link and its target is "#". Same placeholder as
/research. So the depth behind anthropic.com listings is client-side on at least two sections, and there is
no pagination parameter to guess on either. Do not queue "the See more depth" for any anthropic.com index.
The routes onward are the ones route 39 names: another page that links the older items directly (the
alignment.anthropic.com index links 17 older /research/ slugs), or a known-slug list.
ALSO MEASURED ON THAT SWEEP: the same index returns an item in BOTH a featured block and the dated list, so
one post can appear twice in an enumeration with identical URL and date. Deduplicate by URL before counting
anything, and remember route 33 -- ask for the enumeration, never the count.
AND THE DATED LIST IS NOT THE WHOLE FEED: Claude Haiku 5.5 (Oct 7) appeared only in the featured section,
not in the dated News list, and its URL is at the SITE ROOT (/claude-haiku-5-5), not under /news/. A sweep
that reads only the dated rows misses model launches entirely.

=== ROUTE 41 (50th run). deploymentsafety.openai.com/gpt-6-astra/safeguards IS 109,623 CHARACTERS AND EXCEEDS THE FETCH CAP -- BUT THE APOLLO SECTION IS INSIDE THE FIRST 100,000. ===
A targeted verbatim call on that URL returned its three asked-for quotes and then the route-31 notice:
    "this page's text is 109623 characters long and the answer above covers only characters 0 to 100000;
     the final 9623 were not read -- to read on, call WebFetch again with the same url and offset: 100000."
So the page is pageable and the cap announced itself, exactly as route 31 says. The operational point for
this specific URL: the "External Evaluations for Alignment - Apollo Research" section is reachable in ONE
plain call with no offset, and the queue's long-standing "Section 9 (Preparedness), capped at one attempt"
item is most likely in the unread 9,623-character tail -- so spend that one attempt with offset: 100000
rather than on a fresh no-offset call, which will return the same first 100k again.

=== ROUTE 42 (50th run). A SHORT PAGE MAY IGNORE THE VERBATIM-QUOTE FORMAT AND RETURN THE RAW PAGE TEXT INSTEAD. THAT IS THE GOOD OUTCOME, NOT A FAILED CALL. ===
modelcontextprotocol.io/specification/versioning was asked for two numbered quotes under 110 characters each
and instead returned the page's prose essentially whole, headings, callouts and link targets included. The
asked-for facts were in it and the current revision (2026-07-28) was readable directly off the page text.
WHY THIS MATTERS GIVEN ROUTES 32, 37 AND 38: those routes exist because the extraction layer REGULARISES
and FABRICATES when it summarises. Raw page text is the one return shape that cannot do either. So when a
verbatim ask comes back as the page itself, treat it as the strongest possible evidence, not as the tool
misbehaving, and do not re-ask in the hope of a tidier answer -- a tidier answer is a worse one.
It also means the ~125-character per-quote truncation of route 37 does not bite on short pages: ask a short
page for the clause and you may get the surrounding paragraphs for free.

=== ROUTE 43 (51st run). A SUBSTACK ROOT IS A JS SHELL; `/archive?sort=new` IS SERVER-RENDERED AND RETURNS THE FULL LIST. ===
blog.redwoodresearch.org/ returned only the blog title, tagline, subscriber banner and a subscribe form, plus the text "This site requires
JavaScript to run correctly." Zero entries. The same host at https://blog.redwoodresearch.org/archive?sort=new returned twelve rows with
titles, slugs and dates in one plain WebFetch, no browser needed.
SO: for any Substack-hosted feed, the root is not the index. Go straight to /archive?sort=new and never spend a fetch on the root, and never
record a Substack as JS-blocked on the strength of its root alone. This is the cheapest instance yet of the "never declare a source dead"
rule: one path change, no headers, no browser.
ONE CAVEAT MEASURED ON THE SAME CALL: the newest row's date came back as a RELATIVE string ("8 hrs ago") with no absolute date, while every
older row carried "Oct 5", "Sep 25" and so on. A relative date cannot be compared against a high-water mark, so treat such a row as a
candidate regardless of the mark rather than trying to resolve it from the index.

=== ROUTE 44 (51st run). anthropic.com/engineering NEEDS NO DEPTH ROUTE AT ALL — IT IS THE ONE anthropic.com SECTION THAT IS NOT PAGINATED. ===
Routes 39 and 40 established that /research and /news both show a "See more" control whose href is `#`, so their depth is client-side and
unreachable. /engineering is different in the opposite direction, and the route-39 ask settled it in the sweep call: "No 'See more' link or
pagination control appears on this page." The index returned twenty-five dated entries in one call, from 2024-09-19 (contextual-retrieval)
through 2026-04-23 (april-23-postmortem) — i.e. the WHOLE back catalogue, oldest post included.
THE OPERATIONAL POINT: one plain WebFetch of /engineering is a complete enumeration, so a sweep of it is never partial and a missing article
there means the article does not exist, not that the index was shallow. Do not queue depth behind it and do not treat route 5's depth-varies
caution as applying to it. Contrast /research and /news, where the opposite holds.
ALSO FOUND ON THAT SWEEP: /engineering/claude-code-best-practices (2025-04-18) is on the index and was not in `seen`, which is a different
URL from the code.claude.com/docs/en/best-practices page the pack already reads. It is below the feed's high-water mark so it was never a
candidate; it is now skip-marked so it stops reappearing as an apparent gap.

=== ROUTE 45 (51st run). langchain.com/blog HAS REAL PAGINATION WITH A RESOLVABLE TARGET — THE FIRST QUEUED "DEPTH" ITEM IN A WHILE THAT IS ACTUALLY EXECUTABLE. ===
The route-39 ask on www.langchain.com/blog/ returned a numbered pagination control whose next-page target is
`https://www.langchain.com/blog?8457a1db_page=2`. That is a URL that resolves, not a `#` placeholder, so unlike every anthropic.com index the
depth behind this feed can be fetched by incrementing the parameter. The parameter name is opaque and site-generated: copy it verbatim off the
index rather than reconstructing it, and re-read it off the index if it ever 404s.
SECOND MEASUREMENT ON THE SAME CALL, AND IT IS ROUTE 40'S DUPLICATE TRAP ON A DIFFERENT HOST: the index serves several entries twice, once in
a featured block and once in the dated list, with identical URL and date. Deduplicate by URL before counting or triaging. Route 40 recorded
this for anthropic.com/news; two hosts now, so assume it of any index with a featured block.
THIRD, AND IT IS WHY THIS FEED IS WORTH THE PAGINATION: the dated list is dominated by product release notes. The spec's "prefer method posts
to framework posts" rule did the triage work here — two method posts out of nineteen rows produced three facts, and eight release notes were
skip-marked without being read.

=== ROUTE 42 RECONFIRMED (51st run), ON A SECOND HOST AND A LONGER PAGE. ===
modelcontextprotocol.io/community/feature-lifecycle was asked for "this page's text as literally as possible" and returned the entire policy —
prose, the three state tables, the roles table, heading anchors and link targets — not a summary. Every figure and definition in the fact
written from it (8b0f7afe) came off that raw text, so routes 32, 37 and 38 had nothing to bite on. Route 42 said a SHORT page may do this;
this page is a full policy document and did it too. PRACTICAL UPSHOT: on a docs-site page, asking for the text literally is worth trying
BEFORE the numbered-verbatim-clause format, because when it works it costs one call instead of two and the result cannot be regularised.
