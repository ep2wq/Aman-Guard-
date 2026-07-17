# AmanGuard AI engine (FastAPI + OpenAI). Build context: this AI/ folder.
# Used by the root docker-compose.yml AND by the Railway "ai-engine" service
# (Root Directory = AI, Dockerfile Path = Dockerfile).
#
# Binds :: (IPv6 wildcard), NOT 0.0.0.0 — Railway's private network is
# IPv6-only, so an IPv4-only bind is unreachable from the backend. On Linux
# :: accepts IPv4 too (net.ipv6.bindv6only=0), so docker-compose still works.
#
# $PORT is injected by Railway; 8000 locally. Shell form so it expands.
#
# SECRETS: OPENAI_API_KEY and AI_SERVICE_KEY come from the environment only.
# AI/.dockerignore keeps AI/.env out of the image, and only phishingGPT.py is
# copied — the key is never baked into a layer.

FROM python:3.12-slim
WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY phishingGPT.py .

EXPOSE 8000
CMD ["sh", "-c", "uvicorn phishingGPT:app --host :: --port ${PORT:-8000}"]
