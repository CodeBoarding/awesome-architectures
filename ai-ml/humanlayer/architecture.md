```mermaid
graph LR
  subgraph 1["CodeLayer IDE & CLI"]
    1__1_1["Connectivity & Data Access"]
    1__1_2["IDE & CLI Core Orchestrator"]
    1__1_3["HITL Session Manager"]
    1__1_4["Collaborative Response Editor"]
    1__1_5["Desktop & UI Shell"]
    1__1_2 -->|"Uses the SDK to perform session operations and synchronize state with the remote daemon."| 1__1_1
    1__1_2 -->|"Drives the high-level session state and provides the data context for approval workflows."| 1__1_3
    1__1_3 -->|"Embeds the editor to allow users to modify agent responses during the review phase."| 1__1_4
    1__1_3 -->|"Sends final user decisions (approve/reject/continue) back to the daemon via the RPC client."| 1__1_1
    1__1_5 -->|"Triggers OS notifications and manages focus scopes for global hotkeys related to approval actions."| 1__1_3
    1__1_2 -->|"Utilizes the design system primitives and native bridge for window management and system-level inte…"| 1__1_5
  end
  subgraph 2["API & SDK Bridge"]
    2__2_1["API Server Infrastructure"]
    2__2_2["API Protocol Handlers"]
    2__2_3["Go Client SDK"]
    2__2_3 -->|"Initiates REST and SSE connections to the daemon's API endpoints to perform operations like session…"| 2__2_1
    2__2_1 -->|"Dispatches validated HTTP requests to specific operation handlers based on the routing table define…"| 2__2_2
  end
  subgraph 3["HLD Orchestration Engine"]
    3__3_1["Session Execution & Discovery"]
    3__3_2["HITL Approval Gate"]
    3__3_3["Daemon Core & Transport"]
    3__3_1 -->|"Requests authorization for sensitive tool executions and pauses agent progress."| 3__3_2
    3__3_2 -->|"Notifies of human decisions (approve/reject) to resume or terminate agent tasks."| 3__3_1
    3__3_3 -->|"Triggers session initialization and monitors execution health via RPC handlers."| 3__3_1
    3__3_3 -->|"Synchronizes approval states and user decisions with external clients via RPC and SSE."| 3__3_2
    3__3_1 -->|"Publishes session status changes and conversation events to the internal Event Bus."| 3__3_3
  end
  subgraph 4["Agent Execution Layer"]
    4__4_1["Agent Runtime & Process Manager"]
    4__4_2["HITL Approval & Inspection Engine"]
    4__4_3["Session Control & Visibility UI"]
    4__4_4["Communication & State Substrate"]
    4__4_5["Simulation & Demo Environment"]
    4__4_3 -->|"Triggers session creation and process control"| 4__4_1
    4__4_1 -->|"Emits agent tool-use requests to be processed into approval events"| 4__4_2
    4__4_2 -->|"Provides enriched approval data and diffs for rendering in the conversation stream"| 4__4_3
    4__4_4 -->|"Provides the API and data layer for persisting session state"| 4__4_1
    4__4_4 -->|"Synchronizes session and approval state to the frontend"| 4__4_3
    4__4_5 -->|"Replaces the live backend with mock data for demo purposes"| 4__4_3
    4__4_1 -->|"calls"| 4__4_3
    4__4_1 -->|"calls"| 4__4_5
    4__4_3 -->|"calls"| 4__4_4
    4__4_3 -->|"calls"| 4__4_5
    4__4_4 -->|"calls"| 4__4_2
    4__4_4 -->|"calls"| 4__4_5
    4__4_5 -->|"calls"| 4__4_4
  end
  subgraph 5["State & System Infrastructure"]
    5__5_1["Local-First Persistence & Sync"]
    5__5_2["System Runtime & Environment"]
    5__5_3["Development & Validation Infrastructure"]
    5__5_1 -->|"Persists system-level configurations and debug states into the local-first database to ensure setti…"| 5__5_2
    5__5_3 -->|"Mocks CRDT-based data structures and document operations to validate state transitions and synchron…"| 5__5_1
    5__5_3 -->|"Simulates window events and intercepts system logs to verify the application's response to environm…"| 5__5_2
  end
  1 -->|"Initiates session commands, workspace scans, and approval decisions via JSON-RPC."| 2
  2 -->|"Dispatches validated client requests to the session and approval managers."| 3
  3 -->|"Orchestrates the lifecycle of AI agent processes and provides execution context."| 4
  4 -->|"Submits tool-use requests that require human-in-the-loop validation."| 3
  3 -->|"Persists session history, approval logs, and publishes events to the internal bus."| 5
  5 -->|"Synchronizes reactive application state and session snapshots via local-first CRDTs."| 1
  3 -->|"calls"| 2
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The system architecture represents a Human-in-the-loop (HITL) AI development platform where the CodeLayer IDE/CLI initiates requests through an API bridge to the HLD Orchestration Engine. This engine manages AI agent lifecycles and approval workflows, interacting with the Agent Execution Layer to process tool-use requests. The entire system relies on a State & System Infrastructure layer for persistence and synchronization, which feeds back into the IDE to maintain a reactive, local-first user experience.

### CodeLayer IDE & CLI

The primary user interface tier, providing the React-based desktop environment and the TypeScript CLI. It serves as the command center for developers to interact with AI agents, manage workspace context, and perform real-time code editing.

- **Connectivity & Data Access** — Manages the low-level JSON-RPC communication and subscription logic between the IDE/CLI and the HumanLayer Daemon (HLD).
- **IDE & CLI Core Orchestrator** — The central logic hub that manages the application lifecycle and global state synchronization.
- **HITL Session Manager** — Orchestrates the Human-in-the-loop workflow by managing session navigation, approval states, and keyboard-driven interaction patterns.
- **Collaborative Response Editor** — A specialized rich-text editing environment built on Tiptap/ProseMirror that allows developers to modify AI-generated code and responses.
- **Desktop & UI Shell** — Provides the native desktop integration and the visual design system.

### API & SDK Bridge

The communication gateway that defines the contract between the HumanLayer Daemon (HLD) and its clients. It handles protocol translation (JSON-RPC/SSE), request routing, and provides native SDKs for internal and external integration.

- **API Server Infrastructure** — Manages the HTTP server lifecycle, Gin-based routing, and OpenAPI specification metadata.
- **API Protocol Handlers** — Consists of generated wrappers that translate incoming HTTP requests into structured calls for the HLD core services.
- **Go Client SDK** — A native Go library providing high-level abstractions for REST and SSE-based communication with the daemon.

### HLD Orchestration Engine

The core logic layer of the daemon responsible for session management, environment discovery, and the Human-in-the-loop (HITL) approval workflow. It acts as the policy enforcement point for all agent actions.

- **Session Execution & Discovery** — Manages the active lifecycle of agent sessions, including environment scanning, LLM client initialization, and execution monitoring.
- **HITL Approval Gate** — Acts as the policy enforcement point for the orchestration engine.
- **Daemon Core & Transport** — Provides the foundational infrastructure for the daemon, including the bootstrap process, graceful shutdown, and the communication layer.

### Agent Execution Layer

A specialized integration layer that wraps the Claude Code agent. It manages the underlying agent processes, monitors their output, and translates agent tool-use requests into system-level approval events.

- **Agent Runtime & Process Manager** — Manages the lifecycle of the Claude Code agent process.
- **HITL Approval & Inspection Engine** — The core logic for Human-in-the-loop workflows.
- **Session Control & Visibility UI** — Provides the user interface for initiating agent sessions and monitoring their progress.
- **Communication & State Substrate** — The underlying infrastructure that connects the frontend to the backend daemon.
- **Simulation & Demo Environment** — A specialized layer for running the execution environment in a simulated mode.

### State & System Infrastructure

The foundational layer providing local-first data persistence, real-time state synchronization (CRDTs), and cross-cutting services like observability, logging, and testing infrastructure.

- **Local-First Persistence & Sync** — Manages the core data models and real-time synchronization logic.
- **System Runtime & Environment** — Provides the operational context for the application, managing the lifecycle of the desktop environment and system-wide observability.
- **Development & Validation Infrastructure** — A dedicated layer for ensuring system reliability and accelerating UI development.

