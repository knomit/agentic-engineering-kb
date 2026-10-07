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
