# Crossplatform shared Backend for Faro

- FastAPI — main server
- LangChain — Agentic orchestration
- Qdrant / ChromaDB / Faiss — Vector DB (pluggable) (Not decided yet)
- Rust microservice — scanner / analyzer (like yazi)
- Pydantic v2 (pydantic-settings) — Config
- Docker + UV — Packaging & management

## Repo structure

```bash
backend/
├── api/                  # All FastAPI routes
│   ├── __init__.py
│   ├── routes/
│   │   ├── search.py     # Search endpoint
│   │   ├── ingest.py     # Upload docs, process
│   │   ├── chat.py       # Optional QA/chat route
│   │   └── health.py     # /ping or /healthz
│   └── deps.py           # Dependency injections (db, clients, etc.)

├── agents/               # LangChain agents + tools
│   ├── __init__.py
│   ├── base.py
│   ├── tools/
│   │   ├── file_lookup.py
│   │   └── web_search.py
│   └── runtime.py        # Setup + execute agents

├── core/                 # Core system utilities
│   ├── __init__.py
│   ├── config.py         # Pydantic settings (env)
│   ├── logging.py
│   └── schemas.py        # Common Pydantic models

├── vectorstore/          # Qdrant/Chroma/Faiss setup
│   ├── __init__.py
│   ├── init.py           # Initialize DB connection
│   ├── ingest.py         # Load + embed docs
│   └── query.py          # Search against vector db

├── services/             # External service clients (Rust, Web, etc.)
│   ├── __init__.py
│   ├── rust_scanner.py   # Interact with Rust microservice
│   └── web_scraper.py    # For future: scrape pages / docs

├── utils/                # Generic utility functions
│   ├── __init__.py
│   ├── file_utils.py
│   └── text_utils.py

├── main.py               # Entrypoint (FastAPI app)
├── pyproject.toml
├── Dockerfile
├── .env (Root)
└── README.md

```
