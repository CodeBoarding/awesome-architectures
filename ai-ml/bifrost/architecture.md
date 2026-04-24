```mermaid
graph LR
  subgraph 1["Request Gateway & Middleware"]
    1__1_1["Gateway Core & Middleware Engine"]
    1__1_2["Plugin & Extension Framework"]
    1__1_3["Protocol & Realtime Abstractions"]
    1__1_4["Provider Translation Layer"]
    1__1_5["Management & Control Plane"]
    1__1_6["LLM Feature Validation"]
    1__1_1 -->|"uses unified schemas to normalize incoming traffic"| 1__1_3
    1__1_1 -->|"executes the plugin pipeline by invoking hooks"| 1__1_2
    1__1_1 -->|"routes normalized requests to provider adapters"| 1__1_4
    1__1_2 -->|"modifies schema objects"| 1__1_3
    1__1_5 -->|"configures and manages plugin lifecycle"| 1__1_2
    1__1_6 -->|"exercises the full request pipeline for validation"| 1__1_1
  end
  subgraph 2["AI Orchestration Engine"]
    2__2_1["Inbound Transport & Routing"]
    2__2_2["Orchestration Core & Registry"]
    2__2_3["Protocol & Schema Normalization"]
    2__2_4["Provider Adapters & Data Models"]
    2__2_5["Realtime & Stream Management"]
    2__2_1 -->|"Routes validated and authenticated requests to the central engine for processing."| 2__2_2
    2__2_2 -->|"Invokes normalization logic to convert incoming requests into internal formats and resolve tool-cal…"| 2__2_3
    2__2_2 -->|"Dispatches normalized requests to the appropriate provider adapter based on configuration and healt…"| 2__2_4
    2__2_4 -->|"Offloads chunked data and streaming connections for multiplexing and delivery to the end-user."| 2__2_5
  end
  subgraph 3["MCP & Tooling Subsystem"]
    3__3_1["MCP Management API"]
    3__3_2["MCP Tool Orchestrator"]
    3__3_3["MCP Lifecycle Services"]
    3__3_1 -->|"Registers and unregisters MCP clients that require background health monitoring and tool synchroniz…"| 3__3_3
    3__3_1 -->|"Configures the available clients and tool execution parameters (e.g., timeouts, agent depth) used d…"| 3__3_2
    3__3_3 -->|"Provides the orchestrator with up-to-date tool definitions and maintains the active connection stat…"| 3__3_2
  end
  subgraph 4["Configuration & Identity Service"]
    4__4_1["Identity & Access Management"]
    4__4_2["Administrative Configuration Service"]
    4__4_3["Environment Configuration Engine"]
    4__4_2 -->|"Triggers the re-synchronization of account metadata and provider keys when proxy configurations are…"| 4__4_1
    4__4_1 -->|"Resolves sensitive provider credentials and system-wide identity settings from environment variable…"| 4__4_3
    4__4_2 -->|"Validates and applies environment-based overrides when processing runtime configuration updates to …"| 4__4_3
  end
  subgraph 5["Observability & Telemetry"]
    5__5_1["Structured Logging Framework"]
    5__5_2["Distributed Tracing Engine"]
    5__5_3["Runtime Diagnostics & Performance Profiling"]
    5__5_2 -->|"Provides trace identifiers (RequestID) to the logging framework, ensuring that every log entry is c…"| 5__5_1
    5__5_3 -->|"Utilizes the logging framework to record diagnostic events, collector status, and runtime anomalies…"| 5__5_1
  end
  subgraph 6["Management Interface (UI & API)"]
    6__6_1["Management API Gateway (Backend)"]
    6__6_2["Provider & Workspace Management"]
    6__6_3["Observability Dashboard"]
    6__6_4["Prompt Playground"]
    6__6_5["UI Core & Access Control"]
    6__6_1 -->|"serves static assets and provides the API context to"| 6__6_5
    6__6_5 -->|"provides the navigation framework and permission context for"| 6__6_2
    6__6_5 -->|"provides the navigation framework and permission context for"| 6__6_3
    6__6_5 -->|"provides the navigation framework and permission context for"| 6__6_4
    6__6_2 -->|"sends configuration updates and routing rules to the"| 6__6_1
    6__6_3 -->|"fetches aggregated metrics and telemetry data from the"| 6__6_1
    6__6_4 -->|"executes test LLM requests through the"| 6__6_1
  end
  1 -->|"Forwards authenticated and pre-processed requests for provider-specific execution."| 2
  1 -->|"Queries account metadata and validates API keys during the ingress phase."| 4
  2 -->|"Invokes external tools and retrieves context when required by the model's execution plan."| 3
  2 -->|"Retrieves provider credentials and dynamic routing rules to determine the upstream target."| 4
  2 -->|"Emits execution traces, token usage metrics, and provider latency data."| 5
  6 -->|"Updates system configurations, provider mappings, and account permissions."| 4
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

Bifrost is a high-performance AI gateway that acts as a unified proxy for multiple LLM providers. The data flow begins at the Request Gateway, where incoming HTTP or WebSocket traffic is authenticated and processed through a plugin pipeline. Validated requests are passed to the AI Orchestration Engine, which uses the Configuration Service to resolve provider credentials and routing rules. If the model requires external context, the engine interacts with the MCP Subsystem. Throughout the lifecycle, the Observability component captures telemetry, while the Management Interface provides a comprehensive UI for system administration and monitoring.

### Request Gateway & Middleware

The entry point for all incoming traffic, responsible for protocol handling (HTTP/WebSockets), authentication, and the execution of the plugin pipeline. It manages the lifecycle of both standard RESTful requests and low-latency realtime streams.

- **Gateway Core & Middleware Engine** — The primary traffic handler that implements the middleware chain for authentication, tracing, and protocol-specific handling (HTTP/WebSockets).
- **Plugin & Extension Framework** — Manages the micro-kernel architecture, allowing dynamic extension of the request pipeline through pre-hooks, post-hooks, and stream-chunk hooks.
- **Protocol & Realtime Abstractions** — Defines the core data contracts and session abstractions that unify different AI protocols and transport methods into a common internal format.
- **Provider Translation Layer** — Implements the Strategy pattern to translate unified internal requests into provider-specific payloads for 15+ AI backends.
- **Management & Control Plane** — Provides the administrative interfaces (UI and CLI) for configuring the gateway, managing access profiles, and monitoring system logs.
- **LLM Feature Validation** — A comprehensive test suite that validates the gateway's handling of complex AI-specific logic like tool calling, streaming, and multi-turn conversations.

### AI Orchestration Engine

The core processing hub that implements the Adapter pattern to normalize interactions across 15+ AI providers. It handles request transformation, response multiplexing, and streaming data management to maintain OpenAI compatibility.

- **Inbound Transport & Routing** — Acts as the entry point for the subsystem, handling initial HTTP and WebRTC connections.
- **Orchestration Core & Registry** — The "brain" of the engine that manages the request lifecycle.
- **Protocol & Schema Normalization** — Responsible for maintaining strict OpenAI compatibility and extending functionality via the Model Context Protocol (MCP).
- **Provider Adapters & Data Models** — Implements the Adapter pattern to translate normalized Bifrost requests into provider-specific API calls (e.g., Anthropic, Gemini, Bedrock).
- **Realtime & Stream Management** — Manages the complex state and data flow for streaming responses and realtime interactions.

### MCP & Tooling Subsystem

Implements the Model Context Protocol, allowing LLMs to interact with external tools and servers. It manages tool orchestration, health monitoring of client connections, and synchronization of tool definitions.

- **MCP Management API** — Provides the HTTP interface for administrative control over MCP clients.
- **MCP Tool Orchestrator** — Manages the runtime execution of tools and the server-side implementation of the MCP protocol.
- **MCP Lifecycle Services** — Operates background processes to ensure the reliability and consistency of the MCP subsystem.

### Configuration & Identity Service

Manages the persistent state of the gateway, including user/team identities, API key whitelisting, and runtime environment configurations. It provides the metadata necessary for the engine to authenticate with upstream providers.

- **Identity & Access Management** — Defines and implements the core data models for user and team identities, managing the Account interface and enforcing access control.
- **Administrative Configuration Service** — Acts as the control plane for the gateway's runtime state, exposing an API for administrative tasks and managing hot-reloads of system settings.
- **Environment Configuration Engine** — Provides a secure mechanism for managing environment-based configurations, including parsing, type coercion, and sensitive data redaction.

### Observability & Telemetry

A cross-cutting component providing distributed tracing, performance profiling, and structured logging. It collects metrics on cost, latency, and token volume across all gateway operations.

- **Structured Logging Framework** — Provides high-performance, JSON-based structured logging across the gateway.
- **Distributed Tracing Engine** — Captures the end-to-end lifecycle of requests as they pass through the gateway's internal pipeline.
- **Runtime Diagnostics & Performance Profiling** — Monitors the health and performance of the Go runtime and the gateway process.

### Management Interface (UI & API)

The administrative portal and its backend bridge. It includes the React-based dashboard for workspace management, provider configuration via CEL (Common Expression Language) routing, and an interactive prompt playground.

- **Management API Gateway (Backend)** — The Go-based server-side infrastructure that bridges the management UI with the Bifrost core.
- **Provider & Workspace Management** — The primary "Write" interface for the gateway.
- **Observability Dashboard** — The "Read" interface of the management portal, responsible for aggregating and visualizing telemetry data.
- **Prompt Playground** — An interactive developer sandbox for testing LLM prompts and gateway configurations.
- **UI Core & Access Control** — The foundational framework of the management portal, providing the application layout, navigation, and theme.

