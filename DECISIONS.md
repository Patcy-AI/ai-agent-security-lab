# DECISIONS.md - Why this system is built the way it is

This documents the engineering and security decisions across the three agents, so anyone
(including future me) can understand the trade-offs. This is a defensive-research lab: a real
RAG support agent, attacked and then hardened in three stages.

## The core question
How do you stop an AI agent from leaking a secret it holds? We answer it by building the SAME
agent three ways and testing the SAME attacks against each. Same attacks, different design =
a controlled experiment. Any difference in outcome is caused by the design, not luck.

## Why keyword retrieval instead of vector embeddings
The knowledge base is tiny (a handful of short docs). A full vector database (embeddings +
similarity search) would load a SECOND model (an embeddings model) alongside the chat model,
which was slow and memory-heavy on the target hardware. Decision: use lightweight keyword
retrieval. It still retrieves the relevant doc and injects it into the prompt - which is the
exact surface indirect prompt injection exploits - so the security lesson is identical, at a
fraction of the cost. Trade-off documented: for a large KB, switch to a vector store.

## Why a local model (Ollama, llama3.2:3b)
Free, private, offline, and safe to attack because we own it. 3B chosen over 8B after an
out-of-memory failure on 8B - a real deployment-constraint decision (the SLM-vs-LLM trade-off).

## Agent A - Vulnerable (baseline)
Decision: put the API key directly in the system prompt, add no guards, and dump retrieved
docs into the prompt verbatim. Purpose: establish the baseline and prove the attacks work.
Result: leaks the key to a direct ask AND to an indirect injection hidden in a retrieved doc.

## Agent B - Hardened (defense in depth)
Decisions and why:
- Keep the key in context but add a strong "never reveal" instruction. Weak on its own (models
  can be talked around instructions), so it is only layer one.
- Input guard (regex prompt firewall): blocks obvious injection phrasing BEFORE the model sees
  it. Limitation: bypassable by rewording - which is exactly why we add more layers.
- Context sanitizer: strip hidden instructions (HTML comments, "system notice" lines) out of
  RETRIEVED data, and tell the model CONTEXT is untrusted DATA, not commands. This defeats the
  indirect injection that broke Agent A.
- Output canary (regex): scan the model's reply and REDACT the key pattern if it ever appears.
  This is the highest-value layer because it catches a leak regardless of HOW the model was
  fooled (even a successful jailbreak cannot exfiltrate the key).
Result: resists the attacks that broke Agent A; a determined attacker's job is far harder.

## Agent C - Locked-down (the strongest control is architectural)
Decision: stop trusting the model with the secret at all. The key is REMOVED from the model's
context and stored in a server-side vault, released only by an authenticated staff-only tool
(get_escalation_code(staff_token)). A normal user has no token, so the tool always denies them.
Defense in depth from Agent B is kept as backup. Principle: data minimization / least privilege
- you cannot leak what the model was never given. This is the same reason real systems keep
secrets in a vault (e.g., a secrets manager) behind IAM, not in application prompts.
Result: throw every attack at it; the key is not present to leak.

## The through-line (the one lesson)
Instructions are a weak control. Filters help but are bypassable. The strongest control is
architectural: least privilege + data minimization + treating all ingested data as untrusted.
Layer them (defense in depth) and a jailbreak that fools the model still fails to exfiltrate
the secret.

## Frameworks this maps to
OWASP Top 10 for LLM Applications (LLM01 Prompt Injection, LLM02 Sensitive Info Disclosure,
LLM06 Excessive Agency, LLM08 Vector/Embedding Weaknesses), MITRE ATLAS, NIST AI RMF.
