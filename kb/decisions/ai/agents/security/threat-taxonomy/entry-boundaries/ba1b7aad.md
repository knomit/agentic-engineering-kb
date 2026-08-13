---
type: process
domain: [agentic-engineering, security, threat-modeling, incident-response, multi-agent]
confidence: 0.85
sources: 1
entities: [OWASP, ASI01, ASI04, ASI06, ASI07, ASI08, ASI10, cascading failures, blast radius, fan-out]
refs: ['https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/', 'https://genai.owasp.org/download/52117/?tmstv=1765059207']
---
# Four of the OWASP agentic top ten are the same incident at different stages, not four different attacks — and the document gives an explicit rule for which one to file it under

The most useful thing in the OWASP Agentic Top 10 is not the list of ten — it is the disambiguation prose each entry carries, because several entries describe THE SAME EVENT AT A DIFFERENT STAGE OF ITS LIFE. Read as ten separate attacks the list looks redundant; read as a stage axis it becomes a filing rule.

**The stage axis** (the individual boundary rules below are the document's; grouping them as one axis is this pack's reading, not a claim the document makes):
- **Compromise / origin** — ASI01 Goal Hijack, ASI04 Supply Chain, ASI07 Inter-Agent Communication. The attacker acts.
- **Persistence** — ASI06 Memory & Context Poisoning. The compromise outlives the session that planted it.
- **Propagation** — ASI08 Cascading Failures. It spreads.
- **Post-drift behaviour** — ASI10 Rogue Agents. Behavioural integrity is gone and governance, not intrusion, is the problem.

**The boundary rules, close to the document's wording:**
- ASI01 covers the attacker DIRECTLY altering goals, instructions or decision pathways, "regardless of whether the manipulation occurs interactively or through pre-positioned inputs". It is distinguished from LLM01 prompt injection by scope: LLM01 alters a single model response, ASI01 redirects goals, planning and multi-step behaviour.
- ASI06 covers "the persistent corruption of stored context or long-term memory", and explicitly EXCLUDES one-time input prompts, which stay under LLM01. The document notes memory poisoning frequently LEADS TO ASI01 — so the two chain rather than compete.
- ASI10 covers "the loss of behavioral integrity and governance once the drift begins, not the initial intrusion itself", and names prompt injection, ASI01 and ASI04 as things that can INITIATE the divergence without being it.
- ASI08 is "the propagation and amplification of an initial fault — not the initial vulnerability itself".

**The explicit tie-breaker, and it is the operational core of all this.** For ASI08 the document states the test outright: file the initial defect under ASI04, ASI06 or ASI07 when it is a direct compromise — a tainted dependency, poisoned memory, a spoofed message — and "apply ASI08 only when that defect spreads across agents, sessions, or workflows, causing measurable fan-out or systemic impact beyond the original breach". Measurable fan-out is the threshold, not severity.

**ASI08's named detection hooks**, which are what make the propagation stage observable rather than theoretical: rapid fan-out where one faulty decision triggers many downstream agents or tasks in a short time; cross-domain or cross-tenant spread beyond the original context; oscillating retries or feedback loops between agents; downstream queue storms; and repeated identical intents. These are ordinary distributed-systems symptoms, which is the point — the propagation stage is detectable with telemetry you may already have, whereas the origin stage generally is not.

**Why this changes what you build.** A single real agentic incident will legitimately touch four entries, so an incident-classification scheme that forces one label per incident will lose information, and coverage counted as "we have a control for ASI01" says nothing about whether you can contain the same event once it persists, spreads or outlives the intrusion. The remedies differ by stage and do not substitute: input validation addresses origin, memory hygiene addresses persistence, circuit breakers and blast-radius caps address propagation, and behavioural monitoring plus kill switches address post-drift. What this does NOT mean is that the four entries are duplicates to be collapsed — they are deliberately separate because each has its own control set.
