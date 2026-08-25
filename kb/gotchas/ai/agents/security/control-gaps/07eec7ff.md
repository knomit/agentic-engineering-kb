---
type: reference
domain: [agentic-engineering, security, governance, threat-modeling, architecture]
confidence: 0.85
sources: 1
entities: [OWASP, AIUC-1, Agentic Security Initiative, ASI07, ASI08, ASI10, AIVSS, Agent Name Service]
motifs: [enumeration-caps-discovery]
refs: ['https://genai.owasp.org/resource/aiuc-1-crosswalks-owasp-top-10-for-agentic-applications/', 'https://genai.owasp.org/download/54627/?tmstv=1779726713', 'kb://bc6eac5f37df/kb/gotchas/ai/agents/security/threat-taxonomy/coverage-blind-spots/8cf06566.md']
---
# Eight agentic control surfaces that a current AI security standard does not require at all — certifying against it does not mean you cover the agentic threat model

OWASP's Agentic Security Initiative crosswalked AIUC-1 (a security/safety/reliability standard for AI agents, six principles: Data & Privacy, Security, Safety, Reliability, Accountability, and Society) against the OWASP Top 10 for Agentic Applications, and published **eight areas the standard does not cover** that the ASI prevention guidelines treat as essential. Four (gaps 1, 2, 4, 5) have **no dedicated requirement at all**; four (3, 6, 7, 8) are partial coverage needing expansion.

This is the useful artifact for a builder regardless of whether you touch AIUC-1: it is a peer-reviewed list of agentic controls that a serious standard forgot, which means your own checklist probably forgot them too.

**1. Inter-agent communication security** (ASI07, ASI08, ASI10) — no requirement for mutual authentication, message integrity, replay protection, signed agent cards, or attested registries between agents. Excessive-autonomy controls do not cover identification, registration or mutual auth between agents and tools.

**2. Agent identity attestation and containment** (ASI03, ASI10) — no per-agent cryptographic identity, signed behavioral manifests, kill switches, credential revocation, trust zones, or reintegration checks. Also missing: controls preventing autonomy escalation, identity substitution, RBAC modification, or **memory/context boundary expansion across sessions**. Nothing constrains an agent's ability to rewrite and redeploy its own code (the AIVSS "self-modification" factor).

**3. Agentic supply chain attestation** (ASI02, ASI04) — vendor due diligence and change approval exist, but not tool manifests, prompt version control, agent dependency BOMs (AIBOM), content-hash pinning for tools and configs, or code signing for agents/tools/servers.

**4. Cascading failure containment** (ASI08) — failure *response plans* exist; architectural containment does not. Missing: **circuit breakers between planner and executor, blast-radius guardrails (quotas, progress caps), digital-twin replay testing, and independent policy enforcement separating planning from execution.**

**5. Agent tool-use infrastructure controls** (ASI02, ASI03, ASI05) — excessive-autonomy controls protect against the agent, but not against **the agent's use of a misbehaving tool**. Missing: unique identification and registration of tools including **mapping advertised versus actual capabilities**, authentication of tools to agents and servers, authorization of tool API calls, and agent-level tool-call logging. Model-activity logging does not extend to agent- or application-level activity — an observability gap over tool interactions.

**6. Runtime agent security monitoring** (ASI05, ASI10) — deployment-environment security covers interactions with the outside world, not malicious activity *inside* the agent: malicious models, malicious container images, unauthorized network calls, RCE, payload downloads, privilege escalation outside the container. **Distinct from gap 3**: supply-chain attestation is pre-deployment integrity; this is post-deployment behaviour.

**7. Resource and cost abuse controls** (ASI01, ASI10) — no AI service entitlement protection. Without it, attackers can "abuse the AI system's monetary budget by inflating API calls, escalating token consumption, impersonating clients, or creating denial-of-service conditions." Accountability requirements assign owners but do not specify **monetary responsibility for API costs**, cost-governance controls, or monitoring for abnormal usage. Theft-of-service and agent-flooding.

**8. Input/output schema controls and determinism** (ASI01, ASI06, ASI08) — data policies exist for inputs and outputs, but no **structured schemas at the agent-model boundary**, which would enable real-time guardrail enforcement and reduce non-determinism (the "principle of most determinism" countering AIVSS's non-determinism amplification factor).

**WHICH THREAT CLASSES THESE GAPS CLUSTER ON** (counted 2026-08-15 across all eight gap headings; the count is the pack's, the ASI attributions are the document's). Tallying the parenthesised entries above: **ASI10 appears in 4 of the 8 gap areas and ASI08 in 3 — more than any other entry — while ASI09 appears in none.** `8cf06566` builds on this: those same two entries are the *sparsest* in the incident tracker, so the thinnest evidence sits where the controls are most consistently missing. ASI09 is the counter-example that keeps the claim honest — it is sparse in the tracker too, yet has zero gap-area mentions, so "few incidents" does not imply "missing controls" as a general rule.

**Two scope expansions worth acting on independently:**

- **Guardrails belong in agent code, not only at the model layer.** The orchestration layer calling the model should enforce input validation *before* the call and output validation *after* the response, independent of any model-level safety mechanism — explicitly so that guardrails "survive model substitution or model-level guardrail bypass" (verbatim). If your only guardrail is a system prompt, swapping models silently removes it.
- **Data sovereignty needs an agentic definition.** Existing frameworks (GDPR, localization laws) assume static pipelines. An agent may retrieve, reason over, and act on data "across jurisdictions within a single task execution" (verbatim). The unanswered question: when an agent collects data in one region, may it use that data for inference or RAG in another? This is distinct from training-time governance, where anonymization may suffice.

**ALSO IN THIS DOCUMENT, AND NOT PREVIOUSLY RECORDED HERE:** contributor review produced **five new validated Secondary mappings across four previously unmapped requirements** — E004→ASI09, E008→ASI01, E010→ASI01 and ASI03, E017→ASI09. Each is Secondary because the requirement supplies a governance, accountability or transparency layer supporting a technical mitigation rather than implementing one. The document also records two *rejected* proposals and says why, which is the more useful half: E004→ASI06 "does not hold" because change-management scope does not address memory segmentation or cross-session access control, and E004→ASI01 for resource abuse is better handled by gap 7. **A crosswalk that shows its rejected mappings is showing you where the boundary between governance and technical control actually falls.**

**VERIFICATION (2026-08-15, 18th run).** Re-read against the primary PDF (download id 54627, 55 pages, dated 2026-05-25 — unchanged in page count and date since this fact was written). All eight gap titles, their ASI attributions, the four/four split, the six-principle list and both scope expansions confirmed against the source; the two quoted fragments confirmed verbatim. Not re-checked: whether AIUC-1 itself has since added requirements that would close any of these gaps — that would require the AIUC-1 standard, not this crosswalk.
