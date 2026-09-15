\# LLM Gateway \& Guardrail Proxy



A high-performance middleware proxy sitting between application clients and LLM providers. Designed to enforce deterministic security guardrails, reduce API costs via semantic caching, and guarantee structured JSON outputs.



\---



\## Architecture Overview



```text

&#x20;Client Request

&#x20;      │

&#x20;      ▼

┌─────────────────────────────────────────────────────────────┐

│                      LLM GATEWAY PROXY                      │

│                                                             │

│  1. Inbound Guardrail   ──► Scans \& strips prompt injections│

│  2. Semantic Cache      ──► Vector lookup (ChromaDB)       │

│  3. Schema Enforcer     ──► Instructor + Pydantic validation │

│  4. Telemetry Logger    ──► SQLite metrics tracking         │

└──────────────────────────────┬──────────────────────────────┘

&#x20;                              │

&#x20;                              ▼

&#x20;                      Cloud LLM Provider

