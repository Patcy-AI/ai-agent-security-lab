# AI Agent Security Lab (Patcy AISec) — Compliance & AI Governance
### Flagship 1 · governing a RAG agent to an enterprise bar
*A RAG chatbot doesn't carry PCI/GLBA scope the way a bank app does — its compliance story is almost entirely **AI-native governance**: NIST AI RMF, EU AI Act, ISO/IEC 42001, OWASP LLM Top 10, MITRE ATLAS, and the data-protection rules that apply once it touches any personal or confidential data.*

> Scope note: research/portfolio build on synthetic data and a fake secret. This shows the control-to-framework mapping a real assessment would use.

---

## 1. Why governance is the whole story for a RAG agent

The risk in a RAG agent isn't a card number in a database — it's that the agent **acts on untrusted data** and can be steered into disclosing secrets or misbehaving. Governance frameworks exist precisely to manage that: identify the risk, put controls in place, and *continuously evaluate* that they still work. This lab is a worked example of that loop.

## 2. NIST AI Risk Management Framework (AI RMF 1.0)

| Function | How the lab addresses it |
|---|---|
| **Govern** | This document + threat model: named risks, named owner, documented controls |
| **Map** | Assets, trust boundaries (esp. the RAG data boundary), and attacker personas identified |
| **Measure** | The A/B/C harness *is* the measurement: the same attack playbook run at three maturities, with pass/fail per stage — reproducible, quantified evidence |
| **Manage** | Layered defenses (B) plus the architectural fix (C); residual risk (filter bypass) documented and mitigated by data minimization |

The A→B→C ladder is a textbook NIST "Measure + Manage" artifact: you can *point to* the exact stage where each risk is reduced and where it's eliminated.

## 3. EU AI Act
- A general support chatbot is typically **limited-risk** (transparency obligations: tell users they're talking to AI). It climbs toward **high-risk** only if it gates access to essential services. Either way, the Act rewards the controls the lab already shows: robustness against manipulation, logging/traceability, and human oversight of privileged actions (the authenticated staff tool in Agent C).
- **Transparency:** the demo is clearly labelled as an AI agent and a security lab.

## 4. ISO/IEC 42001 (AI Management System)
Provides the process wrapper: a documented AI risk assessment (threat model), a defined set of controls (the three defenses + the vault), and a continuous evaluation mechanism (the attack harness). The lab is a miniature but complete AIMS control loop.

## 5. Data protection (when real data is involved)
Although the secret here is synthetic, the same design generalizes: **data minimization** (GDPR Art. 5(1)(c)) is *literally the Agent C fix* — don't put in the model what it doesn't need. If a production version retrieved personal data, output filtering would extend to PII redaction (Presidio / LLM Guard), satisfying Art. 32 security-of-processing.

## 6. OWASP LLM Top 10 & MITRE ATLAS
Full mapping lives in `ATTACK_CATALOG.md`: LLM01 (direct + indirect injection), LLM02 (info disclosure), LLM07 (system-prompt leakage), LLM08 (RAG/embedding weakness), plus ATLAS techniques for prompt injection, exfiltration, and defense evasion. This is the AI-native equivalent of a CVE/CWE mapping and is what an LLM-security reviewer looks for first.

## 7. AI governance artifacts

**Model/System card (summary):**
- *Purpose:* answer customer support questions from a trusted knowledge base.
- *Data:* support documents (must be provenance-controlled); **no secret in the model** (Agent C).
- *Guardrails:* input guard, context sanitization (data≠instructions), output filtering, server-side vault for privileged data.
- *Human oversight:* privileged data release requires an authenticated staff action; the model can't self-authorize.
- *Known limitations:* pattern-based guards are bypassable (documented); the load-bearing control is data minimization.

**Risk register (top items):** indirect prompt injection via poisoned documents (mitigated: sanitizer + provenance control) · direct injection/jailbreak (mitigated: input guard; residual: bypass → covered by output filter + vault) · secret exfiltration (eliminated in C: nothing to leak) · unbounded consumption (mitigated: rate limit).

**Continuous evaluation / incident response:** the A/B/C attack harness is the detective control and the regression gate; in production this pairs with output monitoring and alerting on canary/secret patterns in generated text.

## 8. Demo → production gap (honest)
Production would add: managed guardrail tooling (LLM Guard, Llama Guard, Rebuff), retrieval-source allow-listing and provenance, PII detection/redaction on outputs, request logging to a SIEM, and a formal EU AI Act classification. The **control model is already correct** — production is hardening and evidence.

---

## The portfolio line
> *"The lab is a complete AI-governance loop in miniature: NIST AI RMF's Map-Measure-Manage, realized as a three-stage attack harness, with every attack tagged to OWASP LLM Top 10 and MITRE ATLAS — and the headline lesson that data minimization is the one control an attacker can't bypass."*
