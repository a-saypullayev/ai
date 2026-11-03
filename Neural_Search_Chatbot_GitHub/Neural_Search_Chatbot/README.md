# Neural Search Chatbot

Responsive AI chat website with FastAPI, optional DuckDuckGo web search, clickable sources, and an OpenAI-compatible model endpoint.

## Important architecture
This repository contains the app, **not model weights**. It can connect to local Ollama or a cloud inference API. To keep the chatbot available while your laptop is off, configure a cloud model provider. Do not point a cloud deployment at `127.0.0.1:11434`; that refers to the cloud container, not your laptop.

## Run locally with Ollama (Windows)
Install Python 3.11+, ensure Ollama is running, then in this folder:
```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
$env:AI_BASE_URL="http://127.0.0.1:11434/v1"
$env:AI_API_KEY="ollama"
$env:AI_MODEL="qwen3.5:4b"
uvicorn app.main:app --reload --port 8000
```
Open http://127.0.0.1:8000

## Deploy
1. Create a GitHub repository and upload the ZIP contents.
2. Deploy as a Docker service on Railway, Render, or another Docker host.
3. Set `AI_BASE_URL`, `AI_API_KEY`, and `AI_MODEL` in the host environment settings using your cloud inference provider's exact values. Keep keys secret.
4. Deploy. The app listens on the platform's `PORT`.

## Features
- Web search toggle; search results are passed as reference context.
- Clickable source links.
- Conversation context for the current browser session.
- Docker deployment support.

## Before going public
Add authentication, rate limiting, usage limits, and persistent storage. User prompts are sent to your configured AI provider. Search queries are sent to DuckDuckGo only when web search is enabled. Chat history is not saved after a browser refresh.
