---
type: reference
domain: [agentic-engineering, security, threat-modeling]
confidence: 0.85
sources: 4
entities: [OWASP, ASI01, ASI06, ASI09, ASI10, EchoLeak, AIUC-1, OWASP Top 10 for LLM Applications]
refs: ['https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/', 'https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/', 'https://genai.owasp.org/llm-top-10/', 'https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/', 'https://genai.owasp.org/resource/aiuc-1-crosswalks-owasp-top-10-for-agentic-applications/']
---
# OWASP Top 10 for Agentic Applications (ASI01-ASI10) is the agent-specific list, distinct from the LLM Top 10

Released December 2025 as the first peer-reviewed framework aimed specifically at autonomous agents, developed with 100+ contributors. It sits alongside, not inside, the OWASP Top 10 for LLM Applications — the LLM list covers model-application risks, this one covers risks that only exist once the system acts, holds state, and talks to other agents. The earlier "Agentic AI — Threats and Mitigations" T1-T15 taxonomy continues as a synchronized v1.1 companion rather than being replaced, so a citation to "the OWASP agentic threats" is ambiguous — name which.

*** THE SISTER LIST MOVED: USE THE 2026 EDITION (updated 2026-08-09) ***
This fact previously paired ASI with "LLM01-LLM10, 2025". The LLM Top 10 2026 was published 2026-08-03 and renumbered heavily — most relevantly, Excessive Agency climbed to LLM03:2026, which OWASP calls "the most consequential move on the list, because the vote and the record agree that agentic deployments are where the damage is landing". Do not cite 2025 LLM identifiers as current; see the separate fact on the 2026 edition for the full mapping.
The 2026 edition also replaces the informal "sits alongside" framing above with a STATED HAND-OFF RULE, which is more useful than either list's contents: "This list owns the risk when the model is a component inside your application. The moment that model becomes an actor, with tools it can call, memory it carries between sessions, and consequences it sets in motion downstream, the risk moves to the OWASP Agentic Top 10." Three triggers — callable tools, cross-session memory, downstream consequences — decide which list applies, and OWASP is explicit that they are complements rather than alternatives: "neither one covers that ground alone."

The categories, each with a real incident cited as its exemplar, and the named sub-techniques from the May 2026 crosswalk:

- **ASI01 Agent Goal Hijack** — hidden prompts redirect the agent's objective (EchoLeak). Sub-techniques: gradual plan injection through subtle sub-goals, direct instruction injection overriding original objectives, reflection loop traps.
- **ASI02 Tool Misuse and Exploitation** — legitimate tools driven to destructive ends (Amazon Q). Sub-techniques: parameter pollution, tool chain manipulation, automated abuse of granted permissions. Note the framing: unsafe use arises from "ambiguous prompts, misalignment, or manipulated input" — so an ambiguous tool description is a security defect, not only a quality one.
- **ASI03 Identity & Privilege Abuse** — agents inheriting high-privilege identities. Sub-techniques: dynamic permission escalation, cross-system exploitation due to inadequate scope enforcement, **shadow agent deployment that inherits legitimate credentials**.
- **ASI04 Agentic Supply Chain** — dynamically composed tools and plugins poisoned at runtime (GitHub MCP exploit). Amplified specifically because "autonomous agents reuse compromised data and tools repeatedly and at scale" — the reuse is what turns one compromise into many.
- **ASI05 Unexpected Code Execution** — natural-language paths into RCE (AutoGPT). "RCE delivered via prompts rather than traditional exploits."
- **ASI06 Memory & Context Poisoning** — persistent stores, embeddings and RAG databases altered so behaviour changes across sessions (Gemini memory attack). Sub-techniques: gradual poisoning through repeated interactions, corrupting shared memory in multi-agent systems.
- **ASI07 Insecure Inter-Agent Communication** — spoofed identities, replayed messages, tampering between agents.
- **ASI08 Cascading Failures** — a false signal amplified through an automated pipeline. Sub-techniques: false data accumulating in long-term memory, **hallucinated API endpoints causing data leaks**, self-reinforcing false information.
- **ASI09 Human-Agent Trust Exploitation** — confident explanations inducing an operator to approve harm; decision-fatigue attacks. Sub-techniques: AI-powered invoice fraud replacing vendor details, AI-driven phishing, misinformation through trusted agent interfaces. The crosswalk adds **"fake explainability"** — agents fabricating convincing rationales to gain approval for unsafe actions.
- **ASI10 Rogue Agents** — misalignment, concealment, self-directed behaviour (Replit meltdown). Sub-techniques: malicious workflow injection, impersonating approval agents, orchestration hijacking for fraudulent transactions, coordinated agent flooding.

Two entries deserve attention because they have no analogue in pre-agent security. ASI09 says your human-in-the-loop control is itself an attack surface — an approval gate a tired operator clicks through is not a control, which is why approval-prompt volume is a security parameter and not just UX. And ASI06 makes persistent memory a durable attack surface: a poisoned memory survives the session that planted it, so anything written to long-term memory needs the same scrutiny as untrusted input, every time it is read back.

Named mitigation direction: treat agents as managed non-human identities with scoped, time-bounded credentials that are revoked when context changes, and require human approval for high-risk actions.

CORROBORATION (2026-07-30): the May 2026 AIUC-1 crosswalk independently reproduces this list with identical category names and exemplars, which confirms the taxonomy is stable rather than being restated differently per document. The crosswalk also shows how unevenly the ten are covered by an existing standard — ASI07, ASI08 and ASI10 are where the control gaps cluster, and they are precisely the multi-agent and persistence-dependent entries. The LLM Top 10 2026 carries its own ASI coverage matrix in Appendix A, giving a second independent mapping between the two lists.
