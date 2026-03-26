# h402 — The Human Task Protocol

> Extends x402 one layer up: from AI agents buying digital goods to AI agents hiring verified humans.

**Status:** Specification in progress — v0.1 | March 2026  
**Chain:** Base (EVM, USDC-native)  
**Compatible with:** x402 payment protocol, MCP (Model Context Protocol), EAS (Ethereum Attestation Service)

---

## The Problem

AI agents can now autonomously browse, reason, and pay for digital goods via x402.  
But some tasks cannot be completed by software:

- Physical presence (sign a document, collect a parcel, verify a location)
- Biological uniqueness (Proof of Humanity)
- Local knowledge (navigate a bureaucracy, make a call in a local language)
- Institutional legitimacy (notarized signature, licensed professional attestation)

No open protocol exists for an agent to post these tasks, find a verified human, fund an escrow, and release payment on completion — without trusting a centralized intermediary.

**h402 is that protocol.**

---

## What h402 Does

h402 is a four-layer open protocol:

| Layer | Function | Standards Used |
|-------|----------|---------------|
| **Discovery** | Find verified humans by skill, jurisdiction, reputation | MCP server + REST API + EAS attestations |
| **Engagement** | Post tasks, match workers, accept handshake | x402-compatible HTTP endpoint + AP2 Mandates |
| **Escrow** | Lock funds at acceptance, release on completion, refund on timeout | Immutable smart contract on Base, USDC |
| **Reputation** | Bidirectional on-chain task history, append-only | EAS attestation schema |

An agent that speaks x402 can post an h402 task with no additional SDK. An agent that speaks MCP can discover workers with one tool call.

---

## Protocol Design Principles

1. **The protocol never holds funds.** The escrow contract is immutable. No admin key. No proxy. No upgrade path. Agents control release.
2. **Human identity is attested, not verified by h402.** World ID, Gitcoin Passport, and professional credentials are stored as EAS attestations. h402 reads them; it does not issue them.
3. **Workers are paid at settlement, not on promise.** Escrow releases only after agent-triggered confirmation or timeout auto-refund.
4. **Third parties can build on this.** The spec is open. The reference marketplace is one implementation. Others can build against the same protocol.

---

## Repository Structure
````
h402-protocol/spec          ← You are here. Protocol specification.
h402-protocol/x402-task     ← JSON schema for h402 task posting (x402-compatible)
h402-protocol/h402-mcp      ← MCP server for worker discovery (coming)
````

---

## Specification Status

| Component | Status |
|-----------|--------|
| Task schema (x402-task) | Draft — see `/x402-task` repo |
| Discovery API spec | In progress |
| Escrow contract spec | In progress |
| Reputation schema (EAS) | Planned |
| Worker verification flow | Planned |

---

## Relation to x402

[x402](https://github.com/coinbase/x402) is Coinbase's open payment protocol enabling AI agents to pay for digital resources over HTTP using USDC on Base.

h402 extends x402 by defining what happens when the resource being paid for is a **human task** rather than a digital good. The payment mechanics are identical. The task schema, worker identity layer, and completion proof requirements are new.

An x402-aware agent requires zero modification to post an h402 task. h402 adds the task envelope on top of the existing payment flow.

---

## Reference Implementation

The reference marketplace is in development.

---

## Contributing

The spec is open for comment. Open an issue with:
- `[SCHEMA]` — comments on the task schema
- `[PROTOCOL]` — comments on the engagement/escrow flow
- `[USECASE]` — new task types or use cases

We are actively reviewing all input. First contributors will be credited in the protocol spec as founding reviewers.

---

## Contact

Protocol questions: open an issue.  
