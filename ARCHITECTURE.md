# h402 Protocol Architecture

## Four-Layer Stack
````
┌─────────────────────────────────────────────────────┐
│  AGENT (Claude / GPT / any LLM with tool use)       │
└─────────────────┬───────────────────────────────────┘
                  │ x402-compatible HTTP request
                  │ + h402 task envelope
                  ▼
┌─────────────────────────────────────────────────────┐
│  DISCOVERY LAYER                                    │
│  h402-mcp: find_worker(task_type, jurisdiction)     │
│  Returns: worker_id, price, credentials, ETA        │
│  Identity: EAS attestations (World ID, Gitcoin)     │
└─────────────────┬───────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────┐
│  ENGAGEMENT LAYER                                   │
│  Task post → worker match → acceptance handshake    │
│  Auth: x402 payment + AP2 mandate (enterprise)      │
│  Funds lock at acceptance only                      │
└─────────────────┬───────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────┐
│  ESCROW LAYER                                       │
│  Immutable contract on Base. USDC.                  │
│  Release: agent-triggered on proof verification     │
│  Refund: auto on timeout. No admin key.             │
└─────────────────┬───────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────┐
│  REPUTATION LAYER                                   │
│  EAS attestations. Append-only. On-chain.           │
│  Bidirectional: agent rates worker, worker rates    │
│  task quality. Readable by any protocol builder.    │
└─────────────────────────────────────────────────────┘
````

