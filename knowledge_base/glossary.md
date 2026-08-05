# AI security glossary — terms Patcy AISec uses

**Prompt injection** — getting an LLM to follow attacker instructions instead of its own. *Direct*: the user types the attack. *Indirect*: the attack is hidden in content the model reads (a document, email, web page).

**Jailbreak** — a prompt crafted to bypass a model's safety rules or role, often via role-play, hypotheticals, or encoding.

**RAG (Retrieval-Augmented Generation)** — an agent that answers using documents fetched from a knowledge store at query time. The retrieval step is an attack surface: poisoned documents can carry hidden instructions.

**System prompt** — the hidden instructions that define an agent's behavior, rules, and tools. Leaking it exposes the whole attack surface (LLM07).

**Least privilege** — giving a component only the access it needs. For agents: don't give the model secrets, tools, or data it doesn't require.

**Data minimization** — not placing sensitive data in the model's context (or its retrieval corpus) in the first place. The strongest disclosure control: you can't leak what the model never held.

**Guardrail** — a control that inspects input or output (a prompt-injection filter, an output/DLP scanner). Valuable but pattern-based, so bypassable by rewording or encoding — a first layer, not the last.

**Context sanitization / "spotlighting"** — treating retrieved content as untrusted *data*, stripping instruction-shaped text, and telling the model not to obey it. The specific fix for indirect prompt injection.

**Output filtering / DLP** — scanning the model's reply for secrets or PII and redacting them, regardless of how the model was tricked. Catches leaks but only what it's told to look for.

**Excessive agency** — an agent able to take consequential actions (send, pay, file, delete) without authorization or human oversight (LLM06).

**Human-in-the-loop** — requiring a person to approve irreversible or high-impact actions. The core control for excessive agency: read and draft freely; act only with approval.

**Secret vault** — a server-side store that releases a credential only to an authenticated tool, so the credential is never in the model's context.

**MITRE ATLAS** — a knowledge base of real adversarial techniques against AI systems, the AI counterpart to MITRE ATT&CK.

**Denial of wallet** — a request engineered to run up compute or token cost (LLM10 Unbounded Consumption).
