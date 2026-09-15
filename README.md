\## Architecture Overview



```mermaid

flowchart TD

&#x20;   Client(Client Application) -->|Incoming Prompt| Gateway



&#x20;   subgraph Gateway \[LLM Gateway and Guardrail Proxy]

&#x20;       direction TB

&#x20;       G1\[1. Inbound Guardrail: Scans Injections]

&#x20;       C2\[2. Semantic Cache: Vector Lookup]

&#x20;       S3\[3. Schema Enforcer: Validation]

&#x20;       T4\[4. Telemetry Logger: Metrics]



&#x20;       G1 -->|If Safe| C2

&#x20;       C2 -->|Cache Miss| S3

&#x20;       S3 -->|Validated Payload| T4

&#x20;       C2 -.->|Cache Hit| T4

&#x20;   end



&#x20;   Gateway -->|API Request| LLM(Cloud LLM Provider)

&#x20;   LLM -->|Raw LLM Output| S3

&#x20;   

&#x20;   T4 -->|Structured JSON| Client

```

