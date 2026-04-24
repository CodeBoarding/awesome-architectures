```mermaid
graph LR
  subgraph 1["Desktop Application"]
    1__1_1["Native Shell & IPC Bridge"]
    1__1_2["Application Layout & Navigation"]
    1__1_3["Task Orchestration & State"]
    1__1_4["Environment & Sandbox Manager"]
    1__1_5["Observability & Code Review"]
    1__1_1 -->|"Initializes the Electron window and injects the initial application state."| 1__1_2
    1__1_1 -->|"Provides the low-latency IPC transport layer for real-time task updates."| 1__1_3
    1__1_2 -->|"Triggers task lifecycle actions (create, rename, archive) based on user interaction."| 1__1_3
    1__1_3 -->|"Requests the provisioning and configuration of execution environments for specific tasks."| 1__1_4
    1__1_4 -->|"Streams raw VNC, terminal, and git diff data to the observability components."| 1__1_5
    1__1_5 -->|"Renders live agent views and review interfaces within the application's flexible panel system."| 1__1_2
  end
  subgraph 2["Orchestrator Service"]
    2__2_1["Agent Lifecycle & Environment Manager"]
    2__2_2["Repository & Native Git Engine"]
    2__2_3["Unified Transport & Sync Gateway"]
    2__2_4["Remote Execution & Worker Interface"]
    2__2_3 -->|"Forwards client commands to initiate agent spawning and environment configuration."| 2__2_1
    2__2_1 -->|"Requests repository hydration and state verification when provisioning a new sandbox."| 2__2_2
    2__2_1 -->|"Deploys and monitors the worker agent within the provisioned VM/container."| 2__2_4
    2__2_2 -->|"Synchronizes file changes and Git state directly to the sandbox filesystem."| 2__2_4
    2__2_3 -->|"Proxies real-time PTY, VNC, and browser streams from the worker to the client UI."| 2__2_4
  end
  subgraph 3["Sandbox Runtime"]
    3__3_1["VM Lifecycle Manager"]
    3__3_2["Sandbox Protocol Gateway"]
    3__3_3["Agent Execution Runtime"]
    3__3_4["State & Observability Engine"]
    3__3_1 -->|"Provisions the environment and establishes the initial connection parameters and authentication tok…"| 3__3_2
    3__3_2 -->|"Proxies control commands from the external orchestrator to the internal runtime and streams termina…"| 3__3_3
    3__3_3 -->|"Orchestrates file synchronization events and triggers visual state captures (screenshots/analysis) …"| 3__3_4
  end
  subgraph 4["AI Analysis Engine"]
    4__4_1["Review Orchestrator & Parser"]
    4__4_2["Gemini Provider Adapter"]
    4__4_3["AMP Provider Adapter"]
    4__4_4["Qwen Provider Adapter"]
    4__4_1 -->|"Delegates analysis tasks and monitors completion via file-system events and data callbacks."| 4__4_2
    4__4_1 -->|"Routes analysis requests through a managed proxy for task tracking and authentication."| 4__4_3
    4__4_1 -->|"Orchestrates Qwen-specific review flows and environment setup for ModelStudio or OpenRouter deploym…"| 4__4_4
  end
  subgraph 5["VS Code Extension"]
    5__5_1["Extension Core & UI Integration"]
    5__5_2["Terminal Session Manager"]
    5__5_3["Remote PTY Transport"]
    5__5_1 -->|"Triggers terminal reconciliation and command registration during extension activation."| 5__5_2
    5__5_2 -->|"Delegates low-level PTY operations and WebSocket connection management for specific terminal sessio…"| 5__5_3
    5__5_3 -->|"Streams terminal lifecycle events (e.g., session exit, resize) to update the high-level orchestrato…"| 5__5_2
  end
  subgraph 6["Ecosystem & Tooling"]
    6__6_1["Public Marketing & Demos"]
    6__6_2["Visual Evaluation Framework"]
    6__6_3["Devbox & Environment Management"]
    6__6_2 -->|"Supplies captured agent execution data and visual assets for use in marketing demos and product sho…"| 6__6_1
    6__6_3 -->|"Provisions and manages the sandboxed environments (devboxes/containers) that the collector monitors…"| 6__6_2
    6__6_1 -->|"Serves as the distribution point for the CMUX CLI and related developer tools via download links an…"| 6__6_3
  end
  1 -->|"sends commands and receives real-time state updates via Socket.io and IPC"| 2
  2 -->|"provisions environments and manages agent lifecycles within"| 3
  2 -->|"delegates complex code analysis and review tasks to"| 4
  3 -->|"streams live VNC and Terminal (PTY) data directly to for observability"| 1
  5 -->|"synchronizes terminal sessions and editor state with"| 3
  2 -->|"coordinates repository state and diff synchronization with"| 5
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The manaflow architecture is a high-performance, isolated AI agent orchestration platform that connects a desktop application to distributed sandbox runtimes via an orchestrator service, utilizing specialized proxies for real-time observability, a native Rust core for performance, and an AI analysis engine for complex code tasks, all integrated with VS Code for a seamless developer experience.

### Desktop Application

The primary user interface and desktop shell, managing the application lifecycle and providing a rich environment for task orchestration and observability.

- **Native Shell & IPC Bridge** — The foundational layer that manages the Electron main process, native windowing, and the underlying networking infrastructure.
- **Application Layout & Navigation** — Manages the high-level React application structure, including routing, the flexible panel system, and the core UI kit.
- **Task Orchestration & State** — Central logic for managing the lifecycle of AI tasks.
- **Environment & Sandbox Manager** — Orchestrates the execution environments where agents operate, including Docker-based VS Code instances and cloud sandboxes.
- **Observability & Code Review** — Provides specialized UI components for real-time monitoring and code verification.

### Orchestrator Service

The central backend logic responsible for agent lifecycle management, repository operations, and coordinating communication between the client and sandboxes.

- **Agent Lifecycle & Environment Manager** — Responsible for the high-level orchestration of sandboxed environments.
- **Repository & Native Git Engine** — Manages source control operations and repository state.
- **Unified Transport & Sync Gateway** — Provides a transport-agnostic communication layer that bridges the Orchestrator with the Client UI.
- **Remote Execution & Worker Interface** — Manages the "sidecar" logic that runs within the sandbox.

### Sandbox Runtime

The isolated execution environment (Docker or Cloud VMs) where AI agents perform coding tasks, featuring specialized proxies for live data streaming.

- **VM Lifecycle Manager** — Manages the provisioning, authentication, and lifecycle of the virtual machine or container instances that host the sandbox.
- **Sandbox Protocol Gateway** — A high-performance Go-based sidecar that acts as the primary entry point for low-level protocols.
- **Agent Execution Runtime** — The TypeScript-based "brain" inside the sandbox that manages the execution of agent commands.
- **State & Observability Engine** — Ensures the sandbox workspace remains synchronized with the local environment and provides visual context for the agent.

### AI Analysis Engine

A specialized service layer for performing AI-assisted code reviews, heatmap generation, and LLM provider management.

- **Review Orchestrator & Parser** — The central controller of the subsystem.
- **Gemini Provider Adapter** — Implements the Google Gemini LLM integration.
- **AMP Provider Adapter** — Manages communication with the AI Management Platform (AMP).
- **Qwen Provider Adapter** — Handles integration with Alibaba's Qwen models.

### VS Code Extension

The integration layer that allows Manaflow to synchronize terminal sessions and code diffs directly with the user's local VS Code editor.

- **Extension Core & UI Integration** — Acts as the primary entry point for the extension, handling activation, command registration, and the specialized Multi-Diff Editor UI.
- **Terminal Session Manager** — Orchestrates the mapping between VS Code's terminal UI and the remote sessions.
- **Remote PTY Transport** — Implements the low-level communication protocol for terminal data.

### Ecosystem & Tooling

Public-facing web components and internal developer tools used for evaluation, debugging, and marketing.

- **Public Marketing & Demos** — Manages the external web presence, including the landing page, interactive product demos, and client distribution channels.
- **Visual Evaluation Framework** — Orchestrates the collection and analysis of visual data from agent executions.
- **Devbox & Environment Management** — Provides the CLI and internal scripts necessary to provision, manage, and debug sandboxed execution environments.

