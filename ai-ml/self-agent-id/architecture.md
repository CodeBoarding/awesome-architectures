```mermaid
graph LR
  1["Agent Identity Controller"]
  2["DID Infrastructure & Discovery"]
  3["Verifiable Credential (VC) Engine"]
  4["Cryptographic Security & Vault"]
  5["Secure Agent Communication (DIDComm)"]
  1 -->|"Requests key generation and payload signing"| 4
  1 -->|"Triggers DID registration and peer resolution"| 2
  1 -->|"Initiates credential issuance and verification flows"| 3
  1 -->|"Passes application data for secure transport"| 5
  3 -->|"Resolves issuer DIDs to verify credential signatures"| 2
  3 -->|"Uses keys to sign issued credentials"| 4
  5 -->|"Accesses keys for message encryption (packing)"| 4
  2 -->|"Uses public keys to validate DID Document integrity"| 4
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The `self-agent-id` framework operates as a decentralized identity stack for autonomous agents, where the Agent Identity Controller acts as the central orchestrator. The flow begins with the Cryptographic Security & Vault component generating and securing the root keys, which are then used by the DID Infrastructure & Discovery component to register the agent's identity. Once established, the Verifiable Credential (VC) Engine manages the issuance and verification of claims for trust-less interactions, while the Secure Agent Communication (DIDComm) component utilizes the agent's identity and cryptographic keys to ensure end-to-end privacy and authenticity during peer-to-peer data exchange.

### Agent Identity Controller

The primary entry point and coordinator for the agent. It manages the high-level lifecycle of the agent's identity, delegating specific tasks like signing, resolving, and messaging to specialized sub-components.

### DID Infrastructure & Discovery

Handles the translation of Decentralized Identifiers (DIDs) into actionable DID Documents. It manages interactions with external registries and ledgers to register the agent and discover peers.

### Verifiable Credential (VC) Engine

Manages the lifecycle of verifiable claims. It supports standard W3C Verifiable Credentials and OIDC4VC flows, allowing agents to prove attributes to one another without centralized intermediaries.

### Cryptographic Security & Vault

The "Root of Trust" for the framework. It provides low-level cryptographic primitives for key generation and signing, while ensuring that private keys and secrets are stored securely in an encrypted vault.

### Secure Agent Communication (DIDComm)

Implements the DIDComm messaging protocol. It handles the packing (encryption/signing) and unpacking of messages, enabling secure, asynchronous communication between agents.

