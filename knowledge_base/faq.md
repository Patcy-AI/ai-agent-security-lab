# Patcy AISec — frequently asked questions

**What exactly do you secure?** AI agents and LLM applications — support chatbots, RAG assistants, internal copilots, and agents that call tools or move data. We work at the model/prompt layer (injection, extraction, jailbreaks) and the application layer (authorization, output handling, tool abuse).

**How is attacking an AI different from normal pen-testing?** An AI agent has two attack surfaces normal software doesn't: its *input* can be instructions (a sentence can hijack it), and its *output* is trusted and often acted on. On top of that, the data it *reads* — retrieved documents, emails, memos — can carry hidden instructions. We test all of these.

**Do you sign NDAs?** Always, before any engagement begins.

**How do you handle our data?** We test against a staging copy or synthetic data wherever possible, never exfiltrate real customer data, and delete engagement data on completion. Rules of engagement are agreed in writing up front.

**What tools do you use?** Industry red-team tooling — garak, promptfoo, and PyRIT for automated probing — plus manual testing and reproducible custom attack suites. For defenses we work with LLM Guard, Rebuff, Meta Prompt Guard, Llama Guard, and Presidio, and we advise when a filter isn't enough and an architectural fix is required.

**Which models and stacks do you support?** Open models (Llama, Qwen, Mistral, via Ollama or hosted) and hosted APIs (OpenAI, Anthropic, Groq). Any stack — FastAPI, LangChain, RAG over Postgres/pgvector, Supabase, and more.

**Can you fix an agent that's already leaking data?** Yes. We run an audit, identify the leak (usually prompt injection, a secret placed in the prompt, or over-scoped retrieval), and harden it — ideally by removing the exposure architecturally, not just filtering it.

**How long does an audit take?** Typically 1–2 weeks depending on scope, including the written report and a re-test after you remediate.

**What standards do you map to?** OWASP Top 10 for LLM Applications (2025), MITRE ATLAS, CWE, the OWASP Risk Rating Methodology, and — for governance — NIST AI RMF, the EU AI Act, and ISO/IEC 42001.

**Do you work with small teams?** Yes — startups through enterprise. We scope to your size and risk.

**How do we start?** Book a free 30-minute scoping call at hello@patcyaisec.com. Hours: Mon–Fri, 9am–6pm.
