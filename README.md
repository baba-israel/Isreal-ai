# Nova AI (Streamlit + Groq)

A public chat app: Groq-powered answers, optional Tavily web search with source links, and PDF/TXT/MD document uploads. API keys stay server-side.

## Run locally

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows  (macOS/Linux: source .venv/bin/activate)
pip install -r requirements.txt
```

Create `.streamlit/secrets.toml` (already git-ignored):

```toml
GROQ_API_KEY = "your-new-groq-key"
GROQ_MODEL = "openai/gpt-oss-120b"
TAVILY_API_KEY = "your-tavily-key"   # optional
```

Then:

```bash
streamlit run app.py
```

## Push to GitHub

```bash
git init
git add .
git commit -m "Nova AI Streamlit app"
git branch -M main
git remote add origin https://github.com/<your-username>/nova-ai-streamlit.git
git push -u origin main
```

Check `git status` first: `.env` and `.streamlit/secrets.toml` must NOT be listed.

## Deploy on Streamlit Community Cloud

1. Go to https://share.streamlit.io and sign in with GitHub.
2. New app -> pick the repo, branch `main`, main file `app.py`.
3. Advanced settings -> Secrets, paste:

   ```toml
   GROQ_API_KEY = "your-new-groq-key"
   GROQ_MODEL = "openai/gpt-oss-120b"
   TAVILY_API_KEY = "your-tavily-key"
   ```
4. Deploy.

## Notes

- Revoke any Groq key that was ever pasted in a chat or committed to a repo, and use a fresh one.
- `TAVILY_API_KEY` is optional; without it, the Web search toggle reports that search is not configured.
- If you see `model_not_found`, change `GROQ_MODEL` in Secrets to a model your Groq account can access.
- Public-use limits: 5 MB uploads, 8,000-character messages, 40 messages per browser session. The session cap resets on refresh, so it is not real abuse protection. Set spending/rate limits in the Groq console before sharing widely.
- Scanned (image-only) PDFs are not supported; there is no OCR.
- Chats are kept only in the browser session; nothing is saved to a database.
