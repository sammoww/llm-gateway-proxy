\## Architecture Overview



```mermaid

flowchart TD

&#x20;   Client(\[Client Application]) -->|Incoming Prompt| Gateway



&#x20;   subgraph Gateway \[LLM Gateway \& Guardrail Proxy]

&#x20;       direction TB

&#x20;       G1\[1. Inbound Guardrail<br/>Scans for Prompt Injections]

&#x20;       C2\[(2. Semantic Cache<br/>ChromaDB Vector Lookup)]

&#x20;       S3{3. Schema Enforcer<br/>Pydantic + Instructor}

&#x20;       T4\[4. Telemetry Logger<br/>Metrics \& Observability]



&#x20;       G1 -->|If Safe| C2

&#x20;       C2 -->|Cache Miss| S3

&#x20;       S3 -->|Validated Payload| T4

&#x20;       C2 -.->|Cache Hit| T4

&#x20;   end



&#x20;   Gateway -->|API Request| LLM(\[Cloud LLM Provider])

&#x20;   LLM -->|Raw LLM Output| S3

&#x20;   

&#x20;   T4 -->|Structured JSON| Client



&#x20;   style Gateway fill:#f8f9fa,stroke:#dee2e6,stroke-width:2px

&#x20;   style G1 fill:#ffe8e8,stroke:#ffc9c9,stroke-width:2px

&#x20;   style C2 fill:#e8f4ff,stroke:#b8daff,stroke-width:2px

&#x20;   style S3 fill:#e8ffef,stroke:#c3e6cb,stroke-width:2px

&#x20;   style T4 fill:#fff3e8,stroke:#ffe8ba,stroke-width:2px

```

