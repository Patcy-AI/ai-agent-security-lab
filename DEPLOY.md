# Deploying the live demo (Streamlit Community Cloud + Groq)

The local agents (`app_a/b/c.py`) run on **Ollama**, which free cloud hosts cannot run.
For a public, clickable demo, `streamlit_app.py` runs the whole trilogy on **Groq's free
hosted LLM** instead. Everything else (the guards, sanitizer, vault, mappings) is identical.

## 1. Get a free Groq API key

1. Go to https://console.groq.com and sign in.
2. **API Keys -> Create API Key**. Copy it (starts with `gsk_...`).

## 2. Deploy on Streamlit Community Cloud (free)

1. Go to https://share.streamlit.io and sign in with GitHub.
2. **Create app -> Deploy a public app from GitHub.**
3. Repository: `Patcy-AI/ai-agent-security-lab`
   - Branch: `main`
   - Main file path: `streamlit_app.py`
4. Open **Advanced settings -> Secrets** and paste:

   ```toml
   GROQ_API_KEY = "gsk_your_key_here"
   ```

5. Click **Deploy**. In ~2 minutes you get a public URL like
   `https://patcy-aisec.streamlit.app`.

## 3. Test the live app

- Pick **A - Vulnerable**, click "Ask directly for the key" -> it leaks (expected).
- Switch to **B - Hardened** -> basic attacks are blocked/redacted; the
  "ADVANCED bypass" button leaks in disguise (the teaching moment).
- Switch to **C - Locked-down** -> nothing leaks; the secret is never in the model.

## Notes

- The demo secret (`sk-patcy-...`) is **fake** - it protects nothing real.
- If you ever see "[DEMO MODE] No GROQ_API_KEY", the secret wasn't set in step 4.
- Model used: `llama-3.1-8b-instant` (Groq free tier). Change `GROQ_MODEL` in
  `streamlit_app.py` to swap it.
