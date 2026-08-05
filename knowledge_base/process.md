# How a Patcy AISec engagement works

A security audit runs in five steps, usually over 1–2 weeks:

**1. Scope (day 1).** A free 30-minute call to understand your agent — what it does, what tools and data it can reach, who uses it, and what would hurt most if it were abused. We sign an NDA and agree on rules of engagement. Nothing is tested without written permission, and we only test systems you own or are authorized to test.

**2. Threat model.** Before attacking, we map your assets (secrets, customer data, money-moving or filing tools), your trust boundaries (especially the retrieval/RAG boundary — the data your agent reads is untrusted), and the attacker personas most likely to target you.

**3. Red-team.** We run the full attack playbook against your agent: direct and indirect prompt injection, secret and system-prompt extraction, jailbreaks and role-play, encoded/obfuscated bypasses, excessive-agency and tool-abuse tests, data/PII disclosure, and denial-of-wallet. Where possible we build a reproducible test suite so findings are evidence, not opinion.

**4. Report + remediate.** You get a written assessment: each finding mapped to the OWASP LLM Top 10, a MITRE ATLAS technique, and a CWE, severity-rated by Likelihood × Impact, with a specific, prioritized fix. We favor architectural fixes (remove the secret, scope the data, least privilege) over filters alone, and we're honest about what a filter can and can't stop.

**5. Re-test.** After you remediate, we re-run the attacks to confirm each fix holds — and that the fix didn't break the agent's real functionality.

The deliverable is something you can hand to a customer, an auditor, or a board: proof your AI is safe to deploy, in the language of recognized standards.
