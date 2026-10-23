---
type: observation
domain: [agentic-engineering, security, governance, observability, evaluation]
confidence: 0.8
sources: 1
entities: [OWASP, GenAI Exploit Roundup Q3 2026, GenAI and Agentic AI Exploit Roundup, LLM Top 10 2026, Agentic Top 10 2026, 'LLM02:2026', 'LLM03:2026', CVE]
motifs: [count-overstates-independence, mapping-absorbs-unrelated-causes, missing-record-reads-absent]
refs: ['https://genai.owasp.org/2026/10/08/genai-and-agentic-ai-exploit-roundup-q3-2026/', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/security/incident-statistics/6c0c742e.md']
---
# Two read-traps in an AI-incident roundup, both of which its own authors flag: the entry count is not a count of independent attacks, and the OWASP risk IDs attached to an entry are analyst mappings that absorb conventional application flaws into LLM categories

OWASP's quarterly GenAI exploit roundups carry explicit caveats about their own structure, and both are the kind that get stripped when a figure is quoted downstream. The Q3 2026 edition states them plainly, so they are the authors' qualifications rather than this pack's reading.

**The entry count is not an attack count.** Of its seven numbered entries, three are connected components of one OpenAI campaign, three are Anthropic incidents and one is a research-demonstrated exploit family; the report says they "should not be counted as seven independent attacks". A later section adds two further multi-part items under single headings, one of which is itself one worm lineage in two waves. So any rate, trend or per-quarter comparison built by counting entries over-counts, and the over-counting is not uniform between editions.

**The taxonomy mapping is interpretation, and it pulls conventional flaws into LLM categories.** Entries label their OWASP risk IDs as analyst mappings, and the report repeatedly marks where the underlying defect was not an AI defect: of one entry, "ordinary infrastructure vulnerabilities were also central"; of a file-disclosure entry, LLM02:2026 is "an outcome-level analogue for exposed secrets; the file disclosure itself was a conventional application flaw, not an LLM disclosure bug"; of another, "SQL injection and debug-page exposure are conventional application weaknesses; they are not automatically LLM prompt-injection risks". It also warns against reading a mechanism off a symptom: "Do not infer prompt injection from task drift alone."

OPERATIONAL CONSEQUENCE when you use one of these as evidence: cite the ENTRY, not the count, and carry the entry's own attack-type field, which distinguishes a confirmed incident from a research demonstration and from an attempted campaign with no confirmed compromise. If you are arguing that a class of LLM risk is materialising in the field, check whether the entries mapped to it were caused by the LLM-specific mechanism or by an ordinary vulnerability that an agent happened to reach — the mapping does not distinguish those, and the roundup's own notes are where that distinction survives.

The report also states its scope: selected major incidents reported during the coverage period, not exhaustive, and not an official OWASP publication. A separate line is worth keeping for the same reason — "The source report lists no specific published CVE identifiers for the other six entries. This does not establish that no associated CVEs exist." An absent CVE in a roundup is missing data, not a negative finding. The pack's existing warning about agentic incident statistics ([[6c0c742e]]) is the same hazard arriving through a different document type.
