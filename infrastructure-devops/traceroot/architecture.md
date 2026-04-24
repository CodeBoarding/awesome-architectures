```mermaid
graph LR
  subgraph 1["Ingestion & Processing Engine"]
    1__1_1["Ingestion Gateway"]
    1__1_2["Processing & Persistence Worker"]
    1__1_3["Enrichment & Transformation Engine"]
    1__1_4["Shared Domain & Infrastructure"]
    1__1_1 -->|"Triggers asynchronous Celery tasks after successfully persisting raw data to S3"| 1__1_2
    1__1_2 -->|"Invokes transformation logic to map OTel attributes to the ClickHouse schema and calculate LLM metr…"| 1__1_3
    1__1_2 -->|"Utilizes ClickHouse client configurations and batch-processing settings"| 1__1_4
    1__1_3 -->|"References domain-specific Enums and Pydantic models for data normalization"| 1__1_4
    1__1_1 -->|"Accesses S3 connection settings and validates incoming requests against shared schemas"| 1__1_4
    1__1_2 -->|"calls"| 1__1_1
  end
  subgraph 2["Analytics & Query Service"]
    2__2_1["Analytical Query Engine"]
    2__2_2["Live Trace Streamer"]
    2__2_3["Operational Analytics & Data Access"]
    2__2_2 -->|"verifies trace completion to signal switch to historical path"| 2__2_1
    2__2_1 -->|"relies on managed client to execute queries"| 2__2_3
    2__2_2 -->|"uses client for persistence status checks"| 2__2_3
    2__2_3 -->|"calls"| 2__2_1
  end
  subgraph 3["AI Agent & Assistant System"]
    3__3_1["AI Assistant Frontend Interface"]
    3__3_2["Agent Orchestration & Session Management"]
    3__3_3["Agent Capabilities & Trace Analysis Tools"]
    3__3_4["Sandboxed Execution Engine"]
    3__3_1 -->|"Sends user queries via REST/SSE and receives streamed agent thoughts and tool outputs."| 3__3_2
    3__3_2 -->|"Selects and executes specific tools based on the LLM's plan to fulfill a user request."| 3__3_3
    3__3_3 -->|"Forwards shell commands and file system operations to be executed within the isolated container env…"| 3__3_4
    3__3_2 -->|"calls"| 3__3_4
    3__3_4 -->|"calls"| 3__3_3
  end
  subgraph 4["Web UI & Visualization"]
    4__4_1["Application Framework & Shell"]
    4__4_2["Trace Analysis & Visualization"]
    4__4_3["AI Observability Assistant"]
    4__4_4["Data Models & API Gateway"]
    4__4_5["Platform Administration & Commercial"]
    4__4_2 -->|"consumes domain models and API clients to fetch and calculate metrics for trace data"| 4__4_4
    4__4_3 -->|"accesses active trace context to provide relevant AI-driven insights and explanations"| 4__4_2
    4__4_3 -->|"integrates into the global layout via the LayoutContext to manage panel visibility"| 4__4_1
    4__4_2 -->|"utilizes the core component library and layout shell for consistent data presentation"| 4__4_1
    4__4_5 -->|"uses the API client and shared models to perform CRUD operations on projects and workspaces"| 4__4_4
    4__4_1 -->|"calls"| 4__4_2
    4__4_2 -->|"calls"| 4__4_3
  end
  subgraph 5["Platform & Enterprise Services"]
    5__5_1["Identity & Platform Foundation"]
    5__5_2["Workspace & Project Governance"]
    5__5_3["Enterprise Billing & Usage Metering"]
    5__5_1 -->|"Provides the authenticated user context and security tokens required to create and manage organizat…"| 5__5_2
    5__5_2 -->|"Supplies workspace metadata and usage events (e.g., AI runs) that are metered for billing purposes."| 5__5_3
    5__5_3 -->|"Enforces feature availability, seat limits, and project-level restrictions based on the workspace's…"| 5__5_2
  end
  subgraph 6["Infrastructure & DevOps"]
    6__6_1["Local Development Orchestrator"]
    6__6_2["Database Migration Engine"]
    6__6_3["System Health Monitoring"]
    6__6_1 -->|"Triggers schema migrations as a prerequisite step during the ensure_infra phase of environment setu…"| 6__6_2
    6__6_1 -->|"Orchestrates the startup of services that expose health endpoints, ensuring the environment is read…"| 6__6_3
    6__6_2 -->|"Indirectly impacts health status; successful migrations are often a prerequisite for the health_che…"| 6__6_3
  end
  1 -->|"Persists processed telemetry data into ClickHouse for analytical retrieval."| 2
  4 -->|"Queries trace and session data to populate dashboards and visualization components."| 2
  4 -->|"Manages user authentication, workspace settings, and project configurations."| 5
  3 -->|"Fetches trace context and historical data to provide context for AI-driven analysis."| 2
  5 -->|"Validates API keys and enforces project-level ingestion limits."| 1
  5 -->|"Monitors usage and enforces billing-related restrictions on AI agent runs."| 3
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

This system architecture represents a comprehensive observability and AI-driven analysis platform. The main flow begins with the ingestion of telemetry data, which is processed and stored in ClickHouse, followed by an analytical layer that serves this data to a web-based visualization interface and an AI-powered assistant system, all governed by a centralized platform and enterprise services layer for security, billing, and administration.

### Ingestion & Processing Engine

Handles the high-volume telemetry data flow, from receiving OTLP protobuf data via the public API to asynchronous processing and batch insertion into ClickHouse.

- **Ingestion Gateway** — Acts as the entry point for all external telemetry.
- **Processing & Persistence Worker** — The orchestration layer for background tasks.
- **Enrichment & Transformation Engine** — The domain-specific logic layer that normalizes generic OpenTelemetry spans into LLM-aware entities.
- **Shared Domain & Infrastructure** — Provides the foundational configuration and data structures used across the engine.

### Analytics & Query Service

The analytical read-path of the platform, responsible for executing complex ClickHouse queries to serve trace, session, and user data to the frontend.

- **Analytical Query Engine** — The core engine for historical data retrieval.
- **Live Trace Streamer** — Provides immediate visibility into traces currently being processed.
- **Operational Analytics & Data Access** — Manages the underlying infrastructure for data access and provides platform-level usage metrics.

### AI Agent & Assistant System

Orchestrates AI-driven workflows, combining backend agent execution in sandboxed environments with a frontend chat interface for interactive trace analysis.

- **AI Assistant Frontend Interface** — Manages the user-facing chat experience, including message input, model configuration, and real-time streaming of agent responses and execution traces.
- **Agent Orchestration & Session Management** — The "brain" of the subsystem that manages the lifecycle of AI agents, session persistence, token usage, and the core execution loop that processes LLM outputs.
- **Agent Capabilities & Trace Analysis Tools** — A collection of functional tools that the agent uses to interact with the external world and the platform's data, such as shell commands, git operations, and OTel trace queries.
- **Sandboxed Execution Engine** — Provides isolated environments (Docker, Daytona) for executing code and commands generated by the agent, managing lifecycle, resource cleanup, and process signals.

### Web UI & Visualization

The primary user interface for the platform, featuring specialized components for rendering hierarchical span trees and managing real-time trace updates.

- **Application Framework & Shell** — Provides the structural foundation and reusable UI primitives for the entire platform, managing global layout context and sidebar states.
- **Trace Analysis & Visualization** — The core engine for rendering complex hierarchical span trees, managing real-time trace updates, and synchronizing view state with the URL.
- **AI Observability Assistant** — An interactive, LLM-powered sidecar that provides contextual analysis of traces, managing streaming chat interfaces and specialized rendering for tool calls.
- **Data Models & API Gateway** — Defines shared domain models and provides the communication layer between frontend and backend services, including cost calculation and security-boundary API routes.
- **Platform Administration & Commercial** — Handles transactional aspects of the platform, including workspace membership, project settings, API key management, and billing.

### Platform & Enterprise Services

Manages the administrative control plane, including identity management, project/workspace configuration, and enterprise billing logic.

- **Identity & Platform Foundation** — Manages the user authentication lifecycle, social identity provider integrations (Google/GitHub), and the foundational infrastructure services that support the platform's administrative operations.
- **Workspace & Project Governance** — Handles the hierarchical management of workspaces and projects, including membership control, security settings (API keys), and the configuration of external LLM model providers.
- **Enterprise Billing & Usage Metering** — Defines enterprise plan logic and entitlements while executing background jobs to meter platform usage (via ClickHouse) and synchronize billing data with external payment processors.

### Infrastructure & DevOps

Provides the foundational tooling for environment setup, database migrations, and system-wide health monitoring.

- **Local Development Orchestrator** — Manages the end-to-end lifecycle of the local development environment.
- **Database Migration Engine** — Encapsulates the logic for evolving the ClickHouse database schema.
- **System Health Monitoring** — Defines the standard protocols for service health and readiness.

