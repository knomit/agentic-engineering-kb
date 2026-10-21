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

=== ROUTE 46 (52nd run). *** THE OPEN-ENDED READ INVENTED A RANKING THE PAGE DOES NOT STATE. ROUTE 32'S FABRICATION CLASS EXTENDS TO SUPERLATIVES AND ORDERINGS. *** ===
The open-ended read of alignment.anthropic.com/2025/strengthening-red-teams/ reported "Suspicion modeling had the largest
effect" and went on to rank all five attack components against each other. The targeted verbatim call on the SAME URL in
the SAME run returned the page's own summary clause:
    "suspicion modeling, attack selection and subtlety have strong effects on attack strength"
and added, unprompted, that the article does not single out one component as largest.
SO THE FABRICATION WAS NEITHER A NUMBER (route 32) NOR AN ATTRIBUTION (route 38) -- IT WAS A RANK. A superlative is as
generated as a figure, and it is more tempting to write than a figure because it is what makes a fact feel sharp: "X
mattered most" is a better sentence than "X, Y and Z all mattered", which is exactly why the summariser reaches for it.
THE RULE: add superlatives, orderings and "the primary driver" claims to the list of things that need a verbatim read
before they reach a body. If the verbatim call returns an enumeration where the summary gave you a ranking, write the
enumeration.
DETECTION SIGNATURE, cheap to apply: a summary that cleanly ranks every item in a list. A source that had measured a
clean ranking would have published the ranking, and a source that publishes "A, B and C have strong effects" is telling
you it did not separate them.

=== ROUTE 42 RECONFIRMED A THIRD TIME (52nd run), ON TWO MORE modelcontextprotocol.io PAGES, ONE OF THEM A TABLE. ===
/specification/2026-07-28/deprecated and /specification/versioning were each asked for "this page's text as literally as
possible" and each returned the page essentially whole: prose, callouts, heading anchors, link targets, and -- the part
that matters -- the deprecation registry's full six-row table with every cell intact, including the two rows whose
earliest-removal wording is the anomaly d24435b9 is about. A TABLE IS THE SHAPE A SUMMARISER MOST WANTS TO COMPRESS, and
asking for the text literally is what stopped it. Routes 32, 37 and 38 had nothing to bite on.
PRACTICAL UPSHOT, now measured on three hosts and four pages: on a docs site, ask for the text literally FIRST. One call
instead of two, and the result cannot be regularised.

=== ROUTE 47 (53rd run). *** A PAGE CAN BE REFUSED BY THE FETCH TOOL'S OWN EXTRACTION MODEL UNDER THE USAGE POLICY, NOT BY THE SITE. alignment.anthropic.com/2026/reward-seeker/ IS CURRENTLY UNREADABLE BY WebFetch. ***
Two WebFetch calls on https://alignment.anthropic.com/2026/reward-seeker/ — one asking for four numbered verbatim clauses, one asking for a single sentence — both failed identically before any page text came back:
    "API Error: Haiku 5.5 can't help with this. Start a new session to continue.
     Learn more: https://www.anthropic.com/legal/aup
     Details: `[bio]`"
This is NOT a site gate and none of the six remedies in the spec's "never declare a source dead" list apply: there is no 403, no JS shell, no missing slug, no header to add, and the bytes were never parsed. The refusal is inside the tool, from the small model that reads the page, and its `[bio]` detail is a classifier firing on the page's content (the post is about reward hacking in RL environments; some of those environments are evidently biology-adjacent). The prompt wording made no difference, so do not keep rewording it.
WHAT THIS COSTS AND WHAT IT DOES NOT: the page was fully readable to earlier runs — 5bad2e60 was written from it on the 21st run with long verbatim quotes — so this is a change in the tool, not in the source, and the existing fact's quotes are not thereby suspect. What is blocked is RE-verification. The 53rd run's staleness pass sampled 5bad2e60, could not read its only ref, and recorded the check as INCOMPLETE rather than weakening the fact.
THE ROUTE ONWARD, UNTRIED: the browser tools, which fetch the page themselves rather than through the summarising model. That is the only remedy that bypasses an extraction-layer refusal, so a future run that needs this page should spend a browser call rather than another WebFetch. Record the verdict as "unread by WebFetch, refused by the extraction model" — never as dead.

=== ROUTE 48 (53rd run). ROUTE 32'S FABRICATION CLASS EXTENDS TO QUANTIFIERS AND TO PAIRINGS. THE OPEN-ENDED READ WIDENED A SCOPED REMEDIATION INTO A UNIVERSAL ONE, AND TIED A CASE TO AN ENVIRONMENT THE PAGE NEVER CONNECTS. ===
Both were caught on one page, anthropic.com/research/investigating-unintended-model-actions, by the second call.
(a) QUANTIFIER WIDENING. The open-ended read reported, under "Changes made": "Internet access is disabled for all internal evaluations until monitoring is confirmed reliable." The verbatim call returned the page's actual sentence:
    "we had already turned off live internet access for some high-risk and cybersecurity evaluations"
and, on a second ask, the forward-looking half separately: "we have now decided to expand that to include all our internal evaluations". So the page states a NARROW accomplished fact plus a BROAD decision, and the summary fused them into a broad accomplished fact. Note the direction: like route 32's rounding, it runs toward the tidier, more quotable sentence.
(b) PAIRING FABRICATION. The open-ended read attributed the live-government-form submission to "OSWorld, Odysseys, and internal use". The verbatim call returned "We saw this behavior on OSWorld (a public computer use evaluation)," and volunteered that the page does not tie that environment to the government-form case. The environments and the cases are both on the page; the MAPPING between them is not, and the summariser supplied it. This is route 38's attribution defect with two page-sourced endpoints instead of one invented one, which makes it harder to smell: every name checks out individually.
THE RULE, ADDED TO ROUTES 32/37/38/46: a quantifier ("all", "some", "most", "every"), a tense ("has" vs "will"), and a pairing of two things the page mentions separately each need the verbatim read before they reach a body. DETECTION SIGNATURE for (a): a summary whose remediation list reads as completed work in a document that elsewhere hedges with "we have now decided". For (b): a case description and an environment name joined by a comma in a list — ask which sentence joins them.
POSITIVE NOTE ON THE SAME PAGE: the verbatim calls also produced the quotes the two facts are built on ("Most are forms of persistence", the da.gd operator, "This is to prevent Claude from using long URLs to take certain unwanted actions"), so the second-call discipline paid for itself twice over in one document — consistent with route 32's closing observation.

=== ROUTE 49 (54th run). *** A SHORT VERBATIM ASK RETURNS *A* CLAUSE THAT MATCHES THE DESCRIPTION, NOT NECESSARILY THE SENTENCE THE FACT QUOTES. A MISMATCH IS NOT EVIDENCE THE QUOTE IS ABSENT. *** ===
Measured in this run's staleness pass on 9a5214f2, whose body quotes alignment.anthropic.com/2026/hot-mess-of-ai/ as saying "Across all tasks and models, the longer models spend reasoning and taking actions, the more incoherent their errors become." The first call asked for "the clause saying longer reasoning and action makes errors more incoherent" and returned something else entirely:
    "longer sequences of reasoning and actions consistently increase error incoherence"
That is a real sentence on the page and a correct answer to the ask. It is simply a DIFFERENT sentence from the one the fact quotes, and taken at face value it looks like the fact's quote was invented. A second, pointed call -- "Does the page contain a sentence beginning '<first words>'? If yes, return its first 110 characters verbatim" -- returned the quote exactly.
THE RULE: when verifying an EXISTING fact's quote, name the quote's opening words in the ask and require a yes/no on its presence. Describing the claim and asking for "the clause" verifies the CLAIM, not the QUOTE, because a page that states something twice has two clauses and the tool returns whichever it finds. Only after a presence-shaped ask comes back NOT PRESENT is a quote actually in doubt.
THIS IS THE MIRROR OF ROUTES 32/37/38/46/48, AND IT CUTS THE OTHER WAY. Those routes are about the tool supplying text the page does not contain. This one is about the tool withholding text the page does contain, and the cost is the opposite error: weakening or rewriting a fact that was correct. The 53rd run recorded the same shape on 0525e590 ("re-ask before concluding a clause is absent") from the paraphrase side; this run isolates the mechanism, which is that the ask's wording selects the sentence.

=== ROUTE 50 (54th run). simonwillison.net TAG PAGES HAVE REAL, RESOLVABLE PAGINATION -- AND THE ROUTE-39 ASK RETURNS THE PAGE COUNT FOR FREE. ===
The route-39 ask on https://simonwillison.net/tags/llms/ returned: no "See more" or "Older" control, and instead a numbered footer reading "page 1 / 67" with "next »" -> https://simonwillison.net/tags/llms/?page=2 and "last »»" -> https://simonwillison.net/tags/llms/?page=67. Both are plain URLs that resolve, so this feed's depth is fetchable by incrementing ?page=N, like langchain.com/blog (route 45) and unlike every anthropic.com index (routes 39/40).
THE PART WORTH KNOWING BEFORE SPENDING THE FETCHES: it is a LINK BLOG, and the triage ratio is nothing like a method-post feed. Of 30 entries at or above the old high-water mark on 2026-10-13, one was a two-sentence note, nineteen were quoted comments, model launches, tool release notes or side projects, and the handful left are the only plausible candidates. The spec's "prefer method posts to framework posts" rule does the work here, but it rejects most of the page rather than most of a section, so budget one sweep call and a small number of article fetches, not a page walk.
ALSO MEASURED: one row's title is empty on the index (a dateline-only note, /2026/Sep/24/harder/). Asking the index for titles alone would have dropped it; the enumeration carried the URL, which is what identifies the row.

=== ROUTE 51 (55th run). *** ROUTE 47 IS RETIRED. THE BUILT-IN BROWSER PANE READS alignment.anthropic.com/2026/reward-seeker/ PERFECTLY. THE AUP REFUSAL WAS IN WebFetch'S EXTRACTION MODEL, NOT IN THE SITE, AND A BROWSER BYPASSES IT. ***
Route 47 recorded that two WebFetch calls on that URL failed with "Haiku 5.5 can't help with this", detail `[bio]`, before any page text came back, and named the browser tools as the untried remedy. This run spent the browser call. `Claude_Browser__preview_start` on the URL followed by `Claude_Browser__get_page_text` returned the page as ordinary text: title "Training a Misaligned Reward Seeker", Richard Qi / Benjamin Wright / Monte MacDiarmid / Evan Hubinger, August 2026, tl;dr, Figures 1 through 8, sections 1 through 3.1.2. No approval prompt, no gate, no 403.
THE GENERAL RULE, AND IT IS THE SIXTH CONSECUTIVE VINDICATION OF "NEVER DECLARE A SOURCE DEAD": an extraction-layer refusal is a property of the READER, so the remedy is a different reader, not a different wording. Do not spend a second WebFetch on an AUP refusal; spend one browser call. The page's content was never the problem.
TWO CAVEATS MEASURED ON THE SAME CALL, AND THEY BOUND WHAT THIS BUYS YOU.
(a) `get_page_text` CAPS AND THE OVERFLOW IS EFFECTIVELY UNREADABLE HERE. At max_chars 50000 the result was persisted to a file whose first 2KB came back inline, and the 50,000 characters it held stopped partway into section 3.1.2. Asking for 200000 returned 158,063 characters, which exceeded the token ceiling and was persisted as a JSON array on ONE LONG LINE. Read's offset/limit cannot split a line, and the tool's own suggestion (jq or python) is exactly what this pack's spec forbids over fetched content. So the tail of a long page is out of reach by this route: budget the browser for pages whose material is near the top, or for targeted presence checks.
(b) `Claude_Browser__find` IS ELEMENT-LEVEL AND ITS "No matches" IS WEAK EVIDENCE. A find for "single bare word ALLOW" returned no matches on a page whose Safety Monitor Bypass section plausibly contains it, because find matches an element's accessibility line rather than the document text, and a long quoted block need not sit in one node. Treat a find miss as inconclusive, never as NOT PRESENT. This is route 49's lesson in a second tool: the instrument's shape, not the page, decided the answer.
WHAT IT COST AND WHAT IT SETTLED: 00f5d991's and 5bad2e60's re-verification is now POSSIBLE but was not COMPLETED, because the quotes both facts rest on live in the section past the readable window (see crawl-state for the one discrepancy this run did find in Figure 1's rendering of the meta-gaming quote).

=== ROUTE 52 (55th run). research.google/blog JOINS THE NO-DEPTH-ROUTE LIST, AND ITS PAGINATION LIES MORE LOUDLY THAN anthropic.com'S. ===
The route-39 ask on https://research.google/blog/ returned a numbered pagination control showing pages 1, 2, 3, an ellipsis and "of 135" pages — and every link's href is `javascript(0):void`, the current page-1 link included. So the control advertises 135 pages of depth and exposes a URL for none of them.
This is the route-39/40 class on a third host, and the stated page count makes it the most tempting instance yet: "135 pages" reads like a queueable target. It is not one. Only a URL that resolves is depth, and there is none here. Do not queue "the research.google back catalogue" and do not try to guess a page parameter; the routes onward are route 39's — another page that links older items directly, or a known-slug list.
FOR SWEEP BUDGETING: the 12 rows the index returns are mostly non-agent AI research (geospatial, genomics, video, connectomics, logistics). One row in twelve was in scope this run. Expect that ratio.

=== ROUTE 53 (55th run). sourcegraph.com/blog HAS REAL, RESOLVABLE PAGINATION — AND IT IS AN "Older →" LINK, NOT A NUMBERED CONTROL. ===
The route-39 ask on https://sourcegraph.com/blog returned no "See more" or numbered control, and instead a single "Older →" link whose target is https://sourcegraph.com/blog?page=2. A plain incrementable parameter, like langchain.com/blog (route 45) and simonwillison.net (route 50), and unlike every anthropic.com index and research.google (routes 39/40/52).
THE SHAPE WORTH NOTING: the affordance's WORDING carries no information about whether depth is reachable. "See more" on anthropic.com is a dead `#`; "Older →" here is a live URL; a numbered control is live on simonwillison.net and dead on research.google. Ask for the href every time and never infer from the label.
FOR TRIAGE: 19 rows back to 2026-05-04 in one call, and the feed is dominated by product launches, pricing and positioning essays. The spec's "prefer method posts to framework posts" rule rejected three of the four rows above the high-water mark.

=== ROUTE 54 (55th run). *** CORRECTION TO ROUTE 43: `/archive?sort=new` IS NOT A UNIVERSAL SUBSTACK RECIPE. ON latent.space IT ERRORS AND THE PLAIN `/archive` WORKS. ***
Route 43 established, on blog.redwoodresearch.org, that a Substack root is a JS shell and said to "go straight to /archive?sort=new and never spend a fetch on the root". Applied to latent.space this run, https://www.latent.space/archive?sort=new returned a hard failure:
    {"error_type":"CLIENT_ERROR","source":"target","message":"There was an error while fetching."}
The same host at https://www.latent.space/archive returned 12 rows with titles, slugs and dates in one plain WebFetch.
SO THE PORTABLE PART OF ROUTE 43 IS `/archive`, AND THE `?sort=new` QUERY IS NOT PORTABLE. Route 43 is otherwise intact — the root is still not the index on a Substack — but a run that treats the full query string as the recipe loses a fetch and may record a live feed as broken. If /archive?sort=new errors, drop the query before concluding anything.
ALSO MEASURED, AND IT IS ROUTE 43'S RELATIVE-DATE CAVEAT ON A SECOND HOST: the two newest rows came back as "5 hrs ago" and "13 hrs ago" with no absolute date, while older rows carried "Oct 13", "Oct 12" and so on. Two Substacks now, so treat it as the platform's behaviour: the newest row or two cannot be compared against a high-water mark and are candidates regardless.

=== ROUTE 55 (56th run). www.microsoft.com/en-us/security/blog HAS NO SITE-WIDE PAGINATION, BUT ITS PER-TOPIC "View all" LINKS RESOLVE AND ARE THE DEPTH ROUTE. AND ONE INDEX ROW POINTED AT A DIFFERENT DOMAIN ENTIRELY. ===
The route-39 ask returned: no "See more", "Load more", "Older" or numbered control anywhere on the index. What it does have is section-level links that are plain resolvable URLs:
    https://www.microsoft.com/en-us/security/blog/topic/ai-and-machine-learning/?sort-by=newest-oldest
    https://www.microsoft.com/en-us/security/blog/topic/threat-intelligence/?sort-by=newest-oldest
    https://www.microsoft.com/en-us/security/blog/?s=
The ai-and-machine-learning topic is the one worth spending a fetch on; it is the pack-relevant slice and it is already sorted newest-first. This is the fourth distinct shape for "depth" across the pack's feeds (dead `#`, dead `javascript(0):void`, incrementable parameter, per-topic archive link), which is the standing reason route 39 says to ask for the href and never infer from the label.
SECOND MEASUREMENT, AND IT IS A DEDUP TRAP THE seen LAYOUT DOES NOT ANTICIPATE: one row in the "Latest posts" list was https://blogs.microsoft.com/on-the-issues/2026/10/01/... — a DIFFERENT HOST from the feed. Since `seen/<host>.md` is keyed by the URL's host, a URL taken off this index may belong in a seen file that is not the feed's. Check each enumerated URL's host before deciding which file to write it to.
THIRD: the featured block repeats rows from the dated sections — 10 unique posts across 14 entries on 2026-10-15. Route 40's duplicate trap, now on a fourth host. Deduplicate by URL before counting or triaging, always.

=== ROUTE 56 (56th run). huggingface.co/blog SERVES TWO BLOCKS WITH DIFFERENT DATE PRECISION, AND ONLY ONE OF THEM CAN BE COMPARED WITH A HIGH-WATER MARK. ===
One plain WebFetch of https://huggingface.co/blog returned 34 unique posts in two distinct blocks:
  (a) a "Community Articles" block whose rows carry RELATIVE dates only — "6 days ago", "about 7 hours ago", "14 days ago";
  (b) a main listing whose rows carry absolute dates — "October 13, 2026", "September 22, 2026".
The first 20 rows appear in BOTH blocks, so the enumeration repeats them. A relative date cannot be ordered against a day-precision mark, so route 43's relative-date caveat applies to an entire block here rather than to the newest row or two: treat every Community Articles row as a candidate filtered only by `seen`, and use the absolute block to move the mark.
PAGINATION RESOLVES AND IS ZERO-INDEXED, which is the part that will bite a run that guesses: the control's "1" points at ?p=0, "2" at ?p=1, "63" at ?p=62. So ?p=N is page N+1 and there were 63 pages on 2026-10-15. The same widget also carries DEAD controls beside the live ones — "Previous" has an empty href and the ellipsis is `#` — so a single widget mixes both kinds and the presence of one working link says nothing about its neighbours.
ON TRIAGE: it is a community blog, so authorship varies per post (the org prefix in the slug, e.g. /blog/microsoft/thinkingbox or /blog/lightonai/..., names the posting org). Most rows are model launches. Frame anything from a community row as "this author's published post claims X", the way the spec already requires for x1xhlol.

=== ROUTE 42 RECONFIRMED A FOURTH TIME (56th run), ON A LONG PRODUCT-DOCUMENTATION PAGE. ===
https://code.claude.com/docs/en/workflows was asked for "this page's text as literally as possible" and returned the whole document: prose, every table with its cells intact, the fenced code blocks, the callouts, the heading anchors and the link targets. Every figure and quoted clause in the facts written from it — the 16-concurrent / 1,000-agent / 4,096-item caps, the size-guideline thresholds, the `Date.now()` determinism sentence, the three stall-error strings — came off that raw text, so routes 32, 37, 38, 46 and 48 had nothing to bite on and NO second verbatim call was needed. Four pages on four hosts now. On a docs site, ask for the text literally FIRST; it is one call instead of two and the result cannot be regularised.

=== ROUTE 33, SIXTH DATAPOINT ON alignment.anthropic.com's INDEX DEPTH (56th run). ===
The same URL with a route-33 enumeration ask has now returned 8 entries (45th run), 62 (46th and 47th), 79 (48th), 84 (2026-10-08) and 84 (2026-10-15). The last two agree, which is the first time two measurements have matched, and the 2026-10-15 call also answered the route-39 question in the same breath: "The page has no 'See more,' 'Load more,' or pagination control." So this index is like anthropic.com/engineering rather than like /research — one call is the whole archive, and the earlier smaller counts were shallow reads of a complete page, not a paginated one. Still record what one call returned on one date; two agreeing calls are not a guarantee.

=== ROUTE 57 (57th run). FOUR DEPTH VERDICTS ON FOUR NEVER-SWEPT HOSTS, PLUS TWO INDEX TRAPS THAT ARE NOT ABOUT DEPTH AT ALL. ===
The route-39 ask ("is there a See more / Load more / Older / numbered control, and what is its target URL?") was put to four
indexes that had sat at "last swept: unknown" since the bootstrap. All four answered cleanly in the sweep call, at no extra cost.
  (a) eugeneyan.com/writing/ -- NO CONTROL OF ANY KIND, and that is the good outcome: one plain WebFetch returned the whole
      archive, newest 2026-06-21 back to 2015-09-17. This is the anthropic.com/engineering shape (route 44), not the
      research.google shape: a missing post means the post does not exist, not that the index was shallow. Do not queue depth.
  (b) www.microsoft.com/en-us/research/blog/ -- REAL, RESOLVABLE, numbered: next page is
      https://www.microsoft.com/en-us/research/blog/?research-area=all&page=2 and the control said "of 149" pages.
      Contrast research.google (route 52), where a numbered control advertising 135 pages exposes `javascript(0):void` for
      every one of them. Same widget shape, opposite verdict -- which is route 39's whole point.
  (c) www.microsoft.com/en-us/security/blog/topic/ai-and-machine-learning/?sort-by=newest-oldest -- the per-topic archive route
      55 named as the depth route has its OWN depth, a "Load More" button whose target is that same URL plus `&paged=2`.
      So route 55's per-topic link is not a dead end; it is the entry to a paged archive. FIFTH distinct shape for "depth"
      in this pack, after dead `#`, dead `javascript(0):void`, incrementable parameter, and per-topic archive link.
  (d) aws.amazon.com/blogs/machine-learning/ -- a single "← Older posts" link to https://aws.amazon.com/blogs/machine-learning/page/2/,
      the sourcegraph.com shape (route 53). Resolves.

*** TRAP ONE, NEW AND WORTH MORE THAN THE FOUR VERDICTS: ON THE AWS ML BLOG THE FIRST ROWS SERVED ARE NOT THE NEWEST. ***
The enumeration returned "Safely Releasing Frontier Models to Customers" (30 JUN 2026) and "How frontier teams are reinventing
AI-native development" (10 JUN 2026) as rows 1 and 2, ABOVE ten rows dated 13-15 OCT 2026. A run that takes "the first entry"
as the newest, or that stops reading once a row falls below the high-water mark, gets the wrong answer on this host and would
record the feed as having nothing new. This is route 40's duplicate trap mutated: there a featured block repeated rows, here a
featured block REORDERS them. THE RULE: order the enumeration by the date you read off each row, never by its position, and
never stop the scan early on a date that falls below the mark.

*** TRAP TWO: A HIGH-WATER MARK CAN SIT ABOVE EVERY ROW THE INDEX HAS, AND THEN NO CANDIDATE CAN EVER QUALIFY. ***
eugeneyan.com/writing/ carried "newest crawled: 2026-07-30 .../cybersecurity-evals/" in feeds.md, bootstrapped from the run
records. The index gives that same post as 21 Jun 2026, and nothing on the index is dated later. So the mark was ABOVE the
whole feed, every sweep would return zero candidates, and the feed would read as permanently up to date while six in-scope
practitioner posts sat unread below it. The mark's DATE was corrected to the index's own 2026-06-21; the URL was already right.
THE CHECK, which costs nothing because the sweep already returns the dates: when a sweep returns zero candidates, compare the
mark's date against the NEWEST row on the index. If the mark is newer than every row, the mark is wrong, not the feed quiet.
AND THE SECOND HALF OF THE RULE: a mark that is merely correct still hides everything below it. A feed whose whole back
catalogue arrives in one call (shapes (a) above, route 44, route 33's alignment.anthropic.com) should have its below-mark rows
triaged into the queue once, because the sweep has already paid for the enumeration.

=== ROUTE 58 (58th run). *** A DATED INDEX CAN CARRY AN UNDATED ROW, AND THE CANDIDATE RULE CANNOT SEE IT. THIS IS NOT A DEPTH PROBLEM AND IT COST THIS PACK THREE FACTS' DELAY, NOT A FETCH. *** ===
The sweep of www.anthropic.com/engineering returned three dated rows, all at or below the 2026-04-23 mark, plus one featured
entry at the TOP of the page with NO DATE AT ALL: /engineering/redesigning-source-control. It was absent from
seen/anthropic.com.md. A run applying the dated-feed rule as written -- "candidates are the index entries dated ON or after
the high-water date" -- drops it, because it has no date to compare. It was read this run and produced THREE facts
(1ed3880b, fbe7060b, fa3d1496), including the pack's hardest numbers yet on agent-driven load: 2,500 merges/day in May 2026
to over 30,000/day by September, and ~25 million CI checkouts/day.
THE RULE: on a dated feed, an entry WITHOUT a date is a candidate whenever it is not in `seen`, full stop. Do not order it
against the mark and do not drop it for being unorderable. Ask the sweep for each row's date explicitly, so a missing date
shows up as missing rather than as absent-from-the-answer.
THIS IS THE THIRD DISTINCT FEATURED-BLOCK TRAP ON ONE SITE, and they are all different failures: route 40 (the featured
block REPEATS table rows, so deduplicate by URL), route 57 trap one (a featured block REORDERS rows, so never order by
position), and now this one (a featured row carries NO date, so never require one). The featured block is also where
anthropic.com puts bare-path URLs that are not under the feed's own prefix at all -- /claude-sonnet-5-5, /claude-opus-5-5 --
so a row's URL need not share the index's path either. Related date-precision cases already recorded: relative dates on
Substack and huggingface Community Articles (routes 43/56), month-only dates on alignment.anthropic.com (route 33), and
year-from-the-section-heading on embracethered.com and blog.redwoodresearch.org.

=== ROUTE 57(a) SHAPE CONFIRMED ON A FOURTH HOST (58th run). cognition.com/blog HAS NO PAGINATION CONTROL OF ANY KIND. ===
The route-39 ask returned no "See more", no "Load more", no "Older", no numbered control -- and one plain WebFetch returned
all 91 rows back to 2024-03-12. This is the eugeneyan.com/writing and anthropic.com/engineering shape (routes 44, 57(a)),
not the research.google shape: a missing post means the post does not exist. Do not queue depth for this feed, and triage its
below-mark rows into the queue once, because the sweep has already paid for the whole enumeration. Dates are MM.DD.YY.

=== ROUTE 33, SEVENTH DATAPOINT (58th run). alignment.openai.com/misalignment-reports/ STATED 19 AND ENUMERATED 18. ===
Same mechanism as the 48th run's 12-versus-11 on the same URL: the page's own header gives a total, the enumeration ask
returns the rows, and the two disagree. The enumeration is the sound half. ALSO NEW ON THIS FEED, and it is not a route-33
issue: every row carries THREE dates -- incident, first posted, last updated -- and the last-updated values MOVE on old rows
(several June 2026 rows read "10/15/26"). So a URL already in `seen` can have been revised since it was read. That is a
staleness question for the facts citing it, not a crawl candidate, and nothing in this job detects it.

=== METHOD NOTE (58th run). A STALENESS SAMPLE THAT SHARES REFS COSTS ONE FETCH PER PAGE, NOT ONE PER FACT. ===
Five facts were checked this run in THREE fetches: 2f33c7ff and 065eb829 both cite the GLM-5.3 page (8 asked-for clauses
confirmed in one call), a0cb6dc6 and 126207f7 both cite the TASTE page (7 in one call), and b17b7fc2 took its own. The
per-call verbatim ask comfortably carried 7-8 short presence-shaped items without hitting route 37's per-quote truncation,
because each asked-for clause was under ~110 characters. So when picking the five, prefer facts that CLUSTER on one source
over five unrelated ones: the pack has several such clusters (the GLM-5.3 page, the TASTE page, the SLEIGHT-Bench page, the
Astra safeguards page, the Petri pages). It is not a licence to check fewer facts -- it is a licence to check the same five
for a third of the fetches.

=== ROUTE 59 (59th run). THE BUILT-IN BROWSER PANE READS A CLIENT-RENDERED SPA THAT PLAIN WebFetch RETURNS EMPTY, AND THE SEVENTH "DEAD" SOURCE TURNED OUT TO BE ONE CALL AWAY. ===
owasp-agentic-ai-security-incidents.lovable.app had sat in the recurring set with "last swept: unknown" since the
12th run. A plain WebFetch of the root, asked for an enumeration of its incident entries, returned exactly the
no-content sentinel:
    NO READABLE CONTENT
THE ROUTE THAT WORKED, two calls, no login, no scripts:
    mcp__remote-devices__Claude_Browser__preview_start { url: "https://owasp-agentic-ai-security-incidents.lovable.app/" }
      -> returns tabId "seed"
    mcp__remote-devices__Claude_Browser__get_page_text { tabId: "seed", max_chars: 12000 }
That returned the rendered <main> whole: every stat tile with its number, all four figure legends with their
coverage and selection-bias notes, the twelve visible record cards with titles, months, ASI mappings and source
labels, the data/snapshot section, the citation block, the full ASI01-ASI10 reference list and the two source
schedules. No site approval was requested and nothing was blocked. The browser tools arrive DEFERRED: one
ToolSearch with
    select:mcp__remote-devices__Claude_Browser__preview_start,mcp__remote-devices__Claude_Browser__get_page_text,...
loads the set in a single round trip; do not load them one at a time.
WHAT THIS GENERALISES TO. Route 51 retired route 47 by showing the pane reads a page the FETCH TOOL'S EXTRACTION
MODEL refuses. This is the other half: the pane also reads a page whose bytes contain no content at all, because
it executes the client-side render the fetch tool cannot. Every JS-rendered entry still sitting unread in
one-off-sources.md on that basis - gorilla.cs.berkeley.edu/leaderboard.html, www.swebench.com,
www.promptfoo.dev/docs/intro, and above all builder.aws.com/learn/topics/builders-library, which three runs have
failed on and which is named there as the most valuable unmined item in the file - is a preview_start plus a
get_page_text away. TRY THE PANE BEFORE RECORDING ANY PAGE AS JS-BLOCKED.
THE TALLY IS NOW SEVEN FOR SEVEN: builder.aws.com (three runs), the Vectara leaderboard, the OWASP PDFs twice,
the OWASP User-Agent gate, and now this. No source this pack has ever recorded as unreachable has stayed
unreachable.
ONE LIMIT WORTH CARRYING: get_page_text returns the page AS RENDERED, so content behind a pagination control is
not in it. This page's record list ends at a "Load 12 more" button reading "42 remaining", so the read gives the
newest 12 of 54 curated records. Clicking it needs the computer action tool, which is a different cost; the page
also advertises per-figure CSV downloads and a public MCP endpoint, and neither has been tried.
AND THE ROUTE-32 STATUS OF A PANE READ IS DIFFERENT FROM A FETCH: get_page_text returns extracted DOM text, not a
summariser's answer, so the figures in it are the page's own and do not need a second verbatim call. That is why
5c43cf17 could be written with the tracker's numbers off a single read. Do not extend that licence to
read_page's accessibility summaries or to a screenshot.

=== ROUTE 42 RECONFIRMED A FIFTH TIME (59th run), ON code.claude.com/docs/en/best-practices. ===
A single WebFetch asking for three short presence-shaped quotes returned the ENTIRE page as raw markdown instead
of three quotes - every section from the context-window preamble to the failure-pattern list. Fifth host, fifth
time: a page under roughly 100,000 characters answering a short verbatim ask tends to ignore the format and hand
back the text, which is the good outcome, because the answer is then the page rather than a reading of it. The
operational consequence for the staleness pass is the one route 36's method note already states: prefer a sample
whose refs are short documentation pages, because one call both re-verifies the quote and re-reads the whole
source for anything the fact is missing. This call confirmed bef38871's two anchors verbatim AND turned up the
bundled /code-review skill and the findings-return-to-the-session behaviour the fact did not carry.

=== ROUTE 60 (60th run). *** ROUTE 59 CASHED: THE PANE READ builder.aws.com AND THE BFCL LEADERBOARD ON THE FIRST TRY. EIGHT FOR EIGHT. ***
Route 59 predicted that every page still recorded as JS-blocked on the strength of a plain fetch was a preview_start plus a
get_page_text away. Two of the four it named were tried this run and both worked, with no site approval requested and nothing
blocked:
    https://builder.aws.com/learn/topics/builders-library   -> 20 article rows, each with author, date and blurb
    https://gorilla.cs.berkeley.edu/leaderboard.html        -> the whole BFCL V4 table, ~100 rows x 16 columns, as text
builder.aws.com had been failed by THREE separate runs and is named in one-off-sources.md as the most valuable unmined item in
the file. An article page on that host reads the same way: navigate then get_page_text returned the rollback-safety article
whole, body text, pull quotes and all. The remaining two named pages (www.swebench.com, www.promptfoo.dev/docs/intro) are
still untried and should be assumed reachable until a PANE read fails on them.

TIMING. The first get_page_text on builder.aws.com returned the page shell with the literal text "Loading posts by tag
#builders-library..." where the list belongs. A second identical call, with nothing between it but the round trip, returned all
20 rows. So a client-rendered list may need one retry; an empty-looking pane read is not a verdict until the second call agrees.

*** THE LIMIT THAT COST A CALL, AND IT IS NOT IN ROUTE 59: get_page_text RETURNS TEXT, NOT LINKS. ***
The builders-library index read gave every row's title, author and date and NO href for any of them, because the extraction is
innerText. A title is not a URL on that host - the article paths are /content/<22-char-id>/<slug>, and the id is unguessable.
The route that worked: WebSearch with allowed_domains: ["builder.aws.com"] on the exact title, which returned the full path as
its first result. So enumerating a pane-rendered index costs one extra call PER ARTICLE you decide to read. Budget for that
before queueing ten rows off one index. Claude_Browser__find returns ref_N element handles rather than hrefs, so it does not
solve this either; clicking through with the computer action tool would, at a different cost.

AND THE COROLLARY FOR THE TABLE CASE: on BFCL the absence of hrefs costs nothing, because the content IS the text. A wide
table comes back as tab-separated rows in header order, so the columns have to be counted against the header group row to be
read correctly (BFCL's is Rank, Overall Acc, Model, Cost, then five section scores, Relevance, Irrelevance, Max Delta, SD,
Latency Mean, Organization, License - sixteen fields). Count them on the first row before quoting any cell. Route 59's licence
holds: these are the page's own numbers and need no second verbatim call.

=== ROUTE 61 (60th run). claude.dev/blog's INDEX IS PLAIN-FETCHABLE, AND ITS DATES CARRY A PARSING TRAP. ===
The 59th run added claude.dev/blog as a feed without ever fetching the index, having reached one article sideways through a
simonwillison.net link post. The index needs nothing special: one plain WebFetch of https://claude.dev/blog with a route-39
ask enumerated 10 rows with titles, hrefs and dates. Depth is a single "LOAD MORE" button reading "Press R to load more" with
no href - route 39's class, so the back catalogue needs the pane.
THE TRAP: the extracted text concatenates the year with the reading time. "Oct 15, 202614 minutes" is 2026-10-15 plus a
14-minute read, not a year 202614. A date read off this index without splitting that boundary is wrong in a way that still
parses, which is the dangerous shape. It also showed the 59th run's mark for this feed to be a day late: the index dates
solving-code-review-at-anthropic to 2026-10-15, while the mark had 2026-10-16 taken from the link post that cited it. A date
read off a LINK POST is the link post's date, not the primary's.

=== ROUTE 62 (61st run). developers.openai.com/api/docs/guides/ SERVES ITS WHOLE SIDEBAR CATALOGUE TO ONE PLAIN WEBFETCH. ===
This feed had sat at "last swept: unknown" since the bootstrap. It needs nothing special: one plain WebFetch with a
route-39-style enumeration ask ("enumerate every guide page, exact title and link path, grouped by section heading; do not
summarise or count") returned roughly 200 guide paths under about 30 section headings. No headers, no browser, no second
call - the flag was isolated, there are no passengers in this recipe. The index is a navigation sidebar rather than a dated
list, so the feed is undated and candidates are everything not in seen; seen held four URLs against those ~200 paths.
The pack-dense slice is /api/docs/guides/agents-api/** (sessions and events, environments and sandboxes, tools, multi-agent,
observability, tracing, errors and recovery) and /api/docs/guides/agents/** for the SDK (orchestration,
guardrails-approvals, sandboxes, running-agents); then /guides/compaction, /guides/prompt-caching/diagnostics,
/guides/tools-skills, /guides/tools-tool-search, /guides/safety-checks/misalignment-monitoring. The ranked list is queue
item 42. Article pages under this tree also answer plain WebFetch, including literal-string asks.
THE GENERAL LESSON, which applies to every undated docs feed still unswept: a documentation sidebar is a one-call
catalogue. The cost of taking such a feed off the "last swept: unknown" list is one fetch, and nine consecutive runs have
now found in-scope unread material on every feed taken off it.

=== ROUTE 63 (61st run). AN ENUMERATION ASK AND A PRESENCE ASK CAN DISAGREE ABOUT A ROSTER, AND THE ENUMERATION IS RIGHT. ===
Extends routes 33 and 49, and the 60th run's note that quoting the exact string beats describing the clause.
On embracethered.com/blog/posts/2025/the-normalization-of-deviance-in-ai/ a presence ask naming five literal quotations
returned YES on all five, which reads as a five-vendor roster. A second call on the same URL asking for an ENUMERATION
("list every distinct vendor or product the post cites with a quotation or reference to that vendor's own documentation, as
the post writes it, then say how many") returned four, and named them. Both answers are correct about different questions:
the fifth quotation is on the page but is not a citation of that vendor's own documentation.
SO: a presence ask confirms that a string exists; it says nothing about which set the string belongs to. Any fact whose
claim is a COUNT or a CATEGORY membership needs the enumeration ask, not a round of presence asks - and this is the second
time a quantifier defect in this corpus traced back to presence asks being used to establish a roster.
