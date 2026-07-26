---
type: reference
domain: [agentic-engineering, security, threat-modeling]
confidence: 0.75
sources: 2
entities: [OWASP, ASI01, EchoLeak, OWASP Top 10 for LLM Applications]
refs: ['https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/', 'https://genai.owasp.org/llm-top-10/', 'https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/']
---
# OWASP Top 10 for Agentic Applications (ASI01-ASI10) is the agent-specific list, distinct from the LLM Top 10

Released December 2025 as the first peer-reviewed framework aimed specifically at autonomous agents, developed with 100+ contributors. It sits alongside, not inside, the OWASP Top 10 for LLM Applications (LLM01-LLM10, 2025) — the LLM list covers model-application risks, this one covers risks that only exist once the system acts, holds state, and talks to other agents. The earlier "Agentic AI — Threats and Mitigations" T1-T15 taxonomy continues as a synchronized v1.1 companion rather than being replaced, so a citation to "the OWASP agentic threats" is ambiguous — name which.

The categories, each with a real incident cited as its exemplar:
- ASI01 Agent Goal Hijack — hidden prompts redirect the agent's objective (EchoLeak)
- ASI02 Tool Misuse — legitimate tools driven to destructive ends (Amazon Q)
- ASI03 Identity & Privilege Abuse — agents operating outside intended scope, especially via delegation chains
- ASI04 Agentic Supply Chain — dynamically composed tools and plugins poisoned at runtime (GitHub MCP)
- ASI05 Unexpected Code Execution — natural-language paths into RCE (AutoGPT)
- ASI06 Memory & Context Poisoning — persistent stores altered so behaviour changes across sessions (Gemini memory attack)
- ASI07 Insecure Inter-Agent Communication — spoofed messages misdirecting agent clusters
- ASI08 Cascading Failures — a false signal amplified through an automated pipeline
- ASI09 Human-Agent Trust Exploitation — confident explanations inducing an operator to approve harm; decision-fatigue attacks
- ASI10 Rogue Agents — misalignment, concealment, self-directed behaviour (Replit)

Two entries deserve attention because they have no analogue in pre-agent security. ASI09 says your human-in-the-loop control is itself an attack surface — an approval gate a tired operator clicks through is not a control, which is why approval-prompt volume is a security parameter and not just UX. And ASI06 makes persistent memory a durable attack surface: a poisoned memory survives the session that planted it, so anything written to long-term memory needs the same scrutiny as untrusted input, every time it is read back.

Named mitigation direction: treat agents as managed non-human identities with scoped, time-bounded credentials that are revoked when context changes, and require human approval for high-risk actions.
