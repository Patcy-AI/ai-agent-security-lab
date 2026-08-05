# The OWASP Top 10 for LLM Applications (2025) — plain-English guide

Patcy AISec audits AI agents against this list. Here is each risk, what it means, and how we test for it.

**LLM01 — Prompt Injection.** The model can't reliably tell instructions from data, so attacker text can override its rules. *Direct* injection is the user typing "ignore your instructions." *Indirect* injection is the dangerous one: a hidden instruction planted inside a document, email, or web page the agent later reads. We test with direct overrides, role-play framings, encoded payloads, and poisoned retrieved documents.

**LLM02 — Sensitive Information Disclosure.** The model reveals data it shouldn't — secrets, API keys, credentials, other users' PII, internal infrastructure. Usually a symptom of putting sensitive data in the model's context, or of missing output controls. We test extraction of secrets, cross-record data, and PII.

**LLM03 — Supply Chain.** Risk from the components you didn't write — a compromised base model, a poisoned dependency, a tampered prompt, a planted backdoor trigger. We review model and dependency provenance, pinned versions, and prompt/code integrity.

**LLM04 — Data and Model Poisoning.** Attacker-controlled content in training data, fine-tuning sets, or a retrieval store changes the model's behavior. We test poisoned knowledge-base documents and attacker-controlled stored fields.

**LLM05 — Improper Output Handling.** The application trusts the model's output and acts on it unsafely — building SQL, shell commands, or HTML from model text. We test injection *through* the model into downstream systems.

**LLM06 — Excessive Agency.** The agent can take actions (send email, move money, call tools) without adequate authorization or human oversight. We test whether the agent will perform privileged or irreversible actions it shouldn't.

**LLM07 — System Prompt Leakage.** The agent discloses its hidden system prompt — its rules, tool inventory, and any secrets embedded in it — handing an attacker the map of the whole system. We test prompt-extraction phrasings.

**LLM08 — Vector and Embedding Weaknesses.** Weaknesses in the RAG layer: unsanitized retrieved content, embedding inversion, cross-tenant retrieval leakage. Closely tied to indirect prompt injection. We test the retrieval pipeline as an attack surface.

**LLM09 — Misinformation.** The model states confident, ungrounded, or fabricated facts — a real harm in regulated domains like finance or health. We test whether the agent invents facts instead of grounding or abstaining.

**LLM10 — Unbounded Consumption.** Requests engineered to exhaust compute, tokens, or budget ("denial of wallet"), or to enable model extraction. We test oversized and repetitive requests against rate and size limits.

**How Patcy AISec uses this:** every finding in our assessments is mapped to one of these categories, plus a MITRE ATLAS technique and a CWE, with severity scored by the OWASP Risk Rating Methodology (Severity = Likelihood × Impact). Ask us "how do you test for LLM01?" and we'll walk you through it.
