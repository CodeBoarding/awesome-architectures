```mermaid
graph LR
  subgraph 1["System Orchestrator"]
    1__1_1["Bootstrapping & Lifecycle Manager"]
    1__1_2["Configuration & Validation Engine"]
    1__1_3["API Registration & Connectivity"]
    1__1_4["Subsystem Assembler"]
    1__1_1 -->|"Initiates the ingestion and security validation of system settings and action definitions."| 1__1_2
    1__1_2 -->|"Provides validated action schemas and metadata for remote backend synchronization."| 1__1_3
    1__1_2 -->|"Supplies operational parameters and validated settings for component instantiation."| 1__1_4
    1__1_3 -->|"Passes the authenticated API client for use in poller and reporter initialization."| 1__1_4
    1__1_4 -->|"Hands over running service handles and contexts for lifecycle management and graceful shutdown."| 1__1_1
    1__1_1 -->|"calls"| 1__1_4
    1__1_4 -->|"calls"| 1__1_2
    1__1_4 -->|"calls"| 1__1_3
  end
  subgraph 2["Connectivity & Dispatcher"]
    2__2_1["Polling Engine"]
    2__2_2["API Communication Gateway"]
    2__2_3["Task Dispatcher"]
    2__2_1 -->|"Triggers requests to fetch pending deliveries and updates the status of events to 'running' to clai…"| 2__2_2
    2__2_1 -->|"Submits successfully claimed events to the worker pool for asynchronous execution."| 2__2_3
    2__2_3 -->|"Workers utilize the client to report final execution results and logs back to the Rootly platform."| 2__2_2
    2__2_2 -->|"calls"| 2__2_1
    2__2_2 -->|"calls"| 2__2_3
  end
  subgraph 3["Execution & Observability Engine"]
    3__3_1["Execution Orchestrator"]
    3__3_2["Script & Git Manager"]
    3__3_3["HTTP Action Executor"]
    3__3_4["Observability & Metrics"]
    3__3_5["Outcome Reporter"]
    3__3_1 -->|"Delegates script-based automation tasks and manages local resource requirements."| 3__3_2
    3__3_1 -->|"Routes API-based tasks for template resolution and network execution."| 3__3_3
    3__3_1 -->|"Forwards final execution states and logs for platform synchronization."| 3__3_5
    3__3_1 -->|"Triggers telemetry recording for task start, end, and duration."| 3__3_4
    3__3_2 -->|"Reports specific Git operation latencies and script execution status."| 3__3_4
    3__3_3 -->|"Records HTTP status codes and request latencies for outbound integrations."| 3__3_4
    3__3_2 -->|"calls"| 3__3_3
    3__3_2 -->|"calls"| 3__3_5
    3__3_4 -->|"calls"| 3__3_5
    3__3_5 -->|"calls"| 3__3_4
  end
  1 -->|"Initializes the API client and starts the polling loop."| 2
  1 -->|"Provides validated action configurations and initializes the Git manager."| 3
  2 -->|"Dispatches fetched events to the executor via the worker pool."| 3
  3 -->|"Uses the established API client to send execution reports and status updates back to Rootly."| 2
  3 -->|"calls"| 1
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The `rootly-edge-connector` follows a linear, secure execution pipeline designed for outbound-only communication. The process begins with the System Orchestrator, which loads and validates YAML configurations and initializes the internal services. Once active, the Connectivity & Dispatcher component maintains a long-polling connection to the Rootly API to retrieve automation events. These events are queued into a worker pool and handed off to the Execution & Observability Engine. This engine runs the specified logic—either via direct HTTP calls or by executing local scripts managed by a Git-backed resource manager. Finally, the execution results and performance metrics are reported back to Rootly, completing the feedback loop.

### System Orchestrator

Acts as the entry point and configuration authority. It is responsible for bootstrapping the application, parsing configuration files, validating security constraints, and wiring together the connectivity and execution components.

- **Bootstrapping & Lifecycle Manager** — Acts as the primary entry point for the application, managing CLI flag parsing, versioning, and the high-level startup sequence.
- **Configuration & Validation Engine** — Handles the ingestion of YAML configuration files and environment variables, applying default values to ensure a consistent system state.
- **API Registration & Connectivity** — Manages the transformation of internal configuration models into API-compatible formats required by the Rootly platform.
- **Subsystem Assembler** — The "glue" component that instantiates and interconnects the functional subsystems.

### Connectivity & Dispatcher

Manages the "Outbound Polling" pattern. It handles the lifecycle of the connection to Rootly, fetches pending events, and uses a worker pool to manage concurrency and task distribution.

- **Polling Engine** — Orchestrates the core execution loop of the agent.
- **API Communication Gateway** — Manages the secure, authenticated connection to the Rootly platform.
- **Task Dispatcher** — Provides the concurrency layer for the subsystem.

### Execution & Observability Engine

The core execution unit that processes automation tasks. it handles script execution (interfacing with Git for resource management), HTTP requests, and records telemetry. It also ensures that execution outcomes are reported back to the Rootly platform.

- **Execution Orchestrator** — Acts as the central brain of the engine, managing the high-level lifecycle of every automation task.
- **Script & Git Manager** — Manages the retrieval and execution of script-based automations.
- **HTTP Action Executor** — Specialized component for network-based automations.
- **Observability & Metrics** — Provides real-time monitoring and telemetry for the execution engine.
- **Outcome Reporter** — The final stage of the execution pipeline, responsible for synchronizing results with the Rootly platform.

