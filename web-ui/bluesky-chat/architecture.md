```mermaid
graph LR
  subgraph 1["Electron Main Process (Native Host)"]
    1__1_1["Application Host & Window Manager"]
    1__1_2["Secure Storage Service"]
    1__1_3["OAuth Flow Controller"]
    1__1_4["Auto-Update Manager"]
    1__1_1 -->|"Registers and exposes the IPC handlers required for the Renderer to access native encryption."| 1__1_2
    1__1_1 -->|"Triggers the creation and configuration of the isolated authentication window during login flows."| 1__1_3
    1__1_1 -->|"Initializes the update polling service during the application's ready event."| 1__1_4
    1__1_3 -->|"Forwards intercepted session tokens for encrypted persistence upon successful authentication."| 1__1_2
    1__1_4 -->|"Sends update status events (e.g., 'update-available') to the main window for user notification."| 1__1_1
    1__1_2 -->|"calls"| 1__1_1
  end
  subgraph 2["Messaging & Identity Core"]
    2__2_1["XMTP Protocol Engine"]
    2__2_2["Identity Resolution Layer"]
    2__2_3["Chat State Controller"]
    2__2_4["Session & UI Orchestrator"]
    2__2_3 -->|"triggers message sending and initializes message streams through the protocol service"| 2__2_1
    2__2_3 -->|"requests handle-to-address resolution to display human-readable names in the conversation list"| 2__2_2
    2__2_2 -->|"resolves the necessary Inbox IDs required by the engine to establish secure peer-to-peer connections"| 2__2_1
    2__2_4 -->|"bridges expose the global chat state and filtering logic to the React view layer"| 2__2_3
    2__2_4 -->|"manages the initialization and teardown of the XMTP client based on the user's authentication and o…"| 2__2_1
    2__2_1 -->|"pushes decrypted incoming messages and protocol events (like group membership changes) into the sta…"| 2__2_3
  end
  subgraph 3["UI Layer (React Frontend)"]
    3__3_1["Messaging Feed Engine"]
    3__3_2["Group Management UI"]
    3__3_3["Identity & Profile UI"]
    3__3_4["UI Infrastructure & State Safety"]
    3__3_1 -->|"Displays user identity metadata and profile avatars within individual message items in the feed."| 3__3_3
    3__3_2 -->|"Resolves member handles and renders profile summaries for administrative views and member lists."| 3__3_3
    3__3_4 -->|"Provides the virtualized state and scroll context required for efficient list rendering."| 3__3_1
    3__3_4 -->|"Injects group-specific state and administrative logic via safe context providers."| 3__3_2
    3__3_4 -->|"Manages global identity state and provides error recovery for profile-related data fetching."| 3__3_3
  end
  subgraph 4["Nostr Identity Provider"]
    4__4_1["Provider Interface & Service Orchestration"]
    4__4_2["Remote Signing (NIP-46) Engine"]
    4__4_3["Nostr Protocol & Relay Client"]
    4__4_1 -->|"Delegates the complex NIP-46 handshake and session restoration during the 'Login via Nostr Connect'…"| 4__4_2
    4__4_1 -->|"Requests user profile metadata and triggers the publication of XMTP inbox bindings to the relay net…"| 4__4_3
    4__4_2 -->|"Utilizes established relay connections and event signing capabilities to transmit and receive NIP-4…"| 4__4_3
  end
  subgraph 5["Mapping Service & Indexer"]
    5__5_1["Public API Gateway"]
    5__5_2["Identity & Persistence Core"]
    5__5_3["Jetstream Indexing Service"]
    5__5_4["Administrative & Backfill Tools"]
    5__5_1 -->|"Invokes database lookup methods to resolve DIDs and calls verification services when a client attem…"| 5__5_2
    5__5_3 -->|"Streams discovered identity mappings from the Bluesky firehose into the database using upsert opera…"| 5__5_2
    5__5_4 -->|"Performs high-volume batch inserts into the database during initial deployment or data recovery pha…"| 5__5_2
  end
  3 -->|"Subscribes to Zustand stores for real-time chat updates and triggers messaging actions"| 2
  2 -->|"Invokes IPC handlers to securely store and retrieve XMTP keys and session data using OS-level encry…"| 1
  2 -->|"Queries the lookup API to resolve Bluesky handles or DIDs into XMTP-compatible messaging addresses"| 5
  2 -->|"Delegates authentication and event signing when the user selects a Nostr-based identity flow"| 4
  5 -->|"Provides the necessary metadata (Inbox IDs) required to initialize peer-to-peer XMTP conversations"| 2
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The application architecture is a multi-layered system designed for secure, cross-protocol messaging. It centers on a Renderer-based 'Messaging & Identity Core' that orchestrates XMTP messaging and identity resolution, supported by an Electron main process for secure native storage, a React UI layer for user interaction, a Nostr provider for alternative identity, and a backend mapping service for Bluesky-to-XMTP address resolution. The flow involves the UI reacting to state changes in the core, which in turn interacts with native services, external identity providers, and remote indexers to facilitate seamless peer-to-peer communication.

### Electron Main Process (Native Host)

The foundational layer running in the Node.js environment. It manages the application lifecycle, window orchestration, and provides secure native services to the renderer process. Its primary responsibility is the "Secure Storage" bridge, ensuring that sensitive cryptographic keys are never exposed to the standard web environment.

- **Application Host & Window Manager** — The central coordinator of the Main process.
- **Secure Storage Service** — Implements the "Secure Storage" bridge by wrapping Electron's safeStorage API.
- **OAuth Flow Controller** — Manages the specialized lifecycle of authentication windows.
- **Auto-Update Manager** — A background service that monitors for new application versions.

### Messaging & Identity Core

The central engine of the application residing in the Renderer process. It orchestrates the XMTP messaging protocol, manages the global application state (Auth, Chat, Onboarding), and coordinates identity resolution between Bluesky and XMTP. It acts as the primary controller for the entire user session.

- **XMTP Protocol Engine** — The low-level transport and security layer responsible for the XMTP client lifecycle.
- **Identity Resolution Layer** — Implements the mapping logic that bridges the social layer (Bluesky/ATProto) with the messaging layer (XMTP).
- **Chat State Controller** — The primary orchestrator of messaging data, utilizing Zustand for global state management.
- **Session & UI Orchestrator** — Manages the high-level application environment, including the onboarding flow, user settings, and authentication state.

### UI Layer (React Frontend)

The visual interface of the application, built with React and Tailwind CSS. It handles complex view logic such as virtualized message lists, group administration, and profile management. It is designed to be highly reactive, reflecting real-time updates from the underlying messaging streams.

- **Messaging Feed Engine** — Manages the high-performance rendering of chat messages using virtualization.
- **Group Management UI** — Provides the interface for managing group chat memberships, metadata, and administrative actions.
- **Identity & Profile UI** — Handles the display and management of user profiles, social graphs, and identity verification.
- **UI Infrastructure & State Safety** — Provides the structural backbone for the React application, including safe context creation for the Provider Pattern and error boundaries for application resilience.

### Nostr Identity Provider

A specialized module that implements the Nostr protocol for identity and remote signing. It allows users to use Nostr as an alternative identity layer, handling NIP-46 remote signing sessions and managing the binding between Nostr pubkeys and XMTP messaging identities.

- **Provider Interface & Service Orchestration** — Acts as the primary facade for the Nostr subsystem, implementing the standard `IdentityProvider` interface to decouple the main application from Nostr-specific logic.
- **Remote Signing (NIP-46) Engine** — Dedicated to the NIP-46 (Nostr Connect) protocol, this component enables secure authentication without exposing private keys to the application.
- **Nostr Protocol & Relay Client** — The low-level data access and networking layer responsible for raw communication with the Nostr network.

### Mapping Service & Indexer

A backend infrastructure component (Cloudflare Worker) that indexes the Bluesky firehose (Jetstream). It maintains a performant SQLite/D1 database mapping DIDs to XMTP Inbox IDs, providing a REST API for the client to resolve handles to messaging addresses.

- **Public API Gateway** — The external-facing interface of the Cloudflare Worker.
- **Identity & Persistence Core** — The central logic hub responsible for database interactions and protocol-specific identity verification.
- **Jetstream Indexing Service** — An active background worker that maintains a persistent connection to the Bluesky Jetstream firehose.
- **Administrative & Backfill Tools** — A suite of maintenance utilities used for cold-starting the database and performing bulk migrations.

