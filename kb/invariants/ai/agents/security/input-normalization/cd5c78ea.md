---
kind: pragmatic
type: policy
domain: [agentic-engineering, security, prompt-injection, guardrails, tools]
confidence: 0.8
sources: 1
entities: [Microsoft, ASCII smuggling, Unicode Tags block, U+E0000, U+E007F, U+E0020, TAG SPACE, prompt injection, normalization, tokenizer, zero-width space, homoglyph, Microsoft Defender for Office 365, flag emoji]
motifs: [normalization-order-decides-outcome, benign-use-shares-mechanism]
refs: ['https://www.microsoft.com/en-us/security/blog/2026/09/03/ascii-smuggling-crosses-over-from-ai-prompt-injection-to-phishing-evasion/', 'kb://bc6eac5f37df/kb/invariants/ai/agents/security/output-handling/9e5bfe91.md', 'kb://bc6eac5f37df/kb/invariants/ai/agents/security/instruction-hierarchy/99aa74e6.md']
---
# Invisible Unicode tag characters smuggle instructions past a model and keywords past a matcher — normalize before analysis, but never alert on the whole block, because regional flag emoji legitimately use it

The Unicode Tags block — "the Unicode Tags block, U+E0000 to U+E007F" — holds a shadow copy of printable ASCII (U+E0041 mirrors "A"), was intended for language tagging, is largely deprecated, and is not rendered by most fonts and interfaces. Microsoft documents it being abused in BOTH directions, and the two directions have different victims.

TOWARD THE MODEL (the long-known prompt-injection use): an attacker encodes instructions in tag characters inside a web page, document or email. A person sees nothing unusual; an assistant that receives the raw text can decode them and may follow them. The source is explicit that what happens next depends on the assistant's permissions and safeguards, not on the encoding.

TOWARD THE DETECTOR (the campaign this account documents): one invisible character is spliced inside a keyword — "⟨U+E0020⟩ represents the invisible Unicode TAG SPACE inserted between letters" — so a finance word such as "funding" still reads normally to the recipient while a literal or regex match fails, because the string is no longer contiguous, and an ML classifier's tokenizer may split the word into unfamiliar sub-tokens.

THE ORDERING IS THE WHOLE CONTROL, FOR BOTH DIRECTIONS AT ONCE. Stripping or folding the tag block, together with other zero-width and invisible code points, BEFORE any keyword, signature, regex or tokenizer logic runs defeats the technique — the source's own words for the effect are "so that splicing them into a word no longer defeats the match". It follows that the technique only works where raw text reaches the matcher or the tokenizer with the characters intact, so the same normalization has to sit upstream of model ingestion and not only in the mail or keyword path. The source notes implementations vary, which means "does my pipeline normalize before it matches" is answered by testing that pipeline.

WHAT THIS DOES NOT MEAN: it is not a licence to treat any tag-block code point as malicious. The England, Scotland and Wales subdivision flag emoji are built from tag characters — "those emojis are encoded using tag characters" — so a naive tag-block signature produces false positives. Outside known legitimate uses these code points are rare in ordinary text, so presence is an anomaly signal to feed a detection, never a block on its own.

SCOPE. The Unicode facts are not vendor-specific. The volumes are: the measurements come from one vendor's mail-security telemetry for a hunting signature written to catch tag-character content, and the account states the technique was one component of the campaign, used for a bounded period, with most flagged messages caught by layers that do not depend on tag characters at all. Tag characters are also one of several long-standing invisible-character evasions alongside zero-width spaces and homoglyphs; the tag block is simply the one pipelines handle least consistently.
