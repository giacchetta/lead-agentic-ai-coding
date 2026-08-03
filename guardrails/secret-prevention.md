# Guardrails: Secret Leakage Prevention

- ❌ **NO HARDCODED SECRETS**: Never insert API keys, bearer tokens, or database credentials directly into source code.
- ✅ **USE ENV VARIABLES**: Reference variables via standard environment mechanisms (`process.env`, `os.getenv`, etc.).
