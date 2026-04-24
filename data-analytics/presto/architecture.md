```mermaid
graph LR
  subgraph 1["REST Protocol & Session Manager"]
    1__1_1["REST Protocol Client"]
    1__1_2["Session State Manager"]
    1__1_3["Query UI Orchestrator"]
    1__1_3 -->|"Initiates query execution requests and subscribes to result stream updates for UI rendering."| 1__1_1
    1__1_3 -->|"Triggers session property modification views and retrieves the current session state to display act…"| 1__1_2
    1__1_1 -->|"Retrieves active session properties and configuration to populate the mandatory X-Presto-Session an…"| 1__1_2
  end
  subgraph 2["SQL Parser & Diagnostic Engine"]
    2__2_1["SQL Grammar & AST Foundation"]
    2__2_2["Client-Side SQL Editor & Validator"]
    2__2_3["Diagnostic Mapping & Thread Analysis"]
    2__2_4["Query Execution Dashboard & Orchestration"]
    2__2_2 -->|"Uses generated parser contexts to validate user input and generate syntax error markers."| 2__2_1
    2__2_3 -->|"Implements listeners that walk the AST nodes to associate execution metadata with specific SQL cons…"| 2__2_1
    2__2_4 -->|"Consumes mapped thread snapshots to populate the Live Plan and execution metrics views."| 2__2_3
    2__2_4 -->|"Retrieves the final SQL text from the editor to initiate query execution and link results back to t…"| 2__2_2
  end
  subgraph 3["Interactive Query Workspace"]
    3__3_1["SQL Development & Submission"]
    3__3_2["Query Execution Monitoring"]
    3__3_3["Plan Visualization Engine"]
    3__3_4["Cluster Health & Infrastructure"]
    3__3_5["UI Foundation & Shared Services"]
    3__3_1 -->|"Submitting a query via the StatementClient triggers the monitoring logic to track the new query's U…"| 3__3_2
    3__3_2 -->|"Detailed query state and stage metrics are passed to the visualization engine to update the D3 grap…"| 3__3_3
    3__3_2 -->|"Query performance issues (e.g., blocked splits) often trigger navigation to worker health views to …"| 3__3_4
    3__3_5 -->|"Provides session configuration and shared input components used to initialize the SQL editor enviro…"| 3__3_1
    3__3_5 -->|"Supplies standardized data formatters (e.g., for bytes and durations) used to render performance me…"| 3__3_2
  end
  subgraph 4["Cluster Monitoring & Resource Dashboard"]
    4__4_1["Cluster Health & Resource Monitor"]
    4__4_2["Query Discovery & Management"]
    4__4_3["Execution Analysis & Visualization"]
    4__4_4["Dashboard Framework"]
    4__4_2 -->|"Navigates to detailed execution statistics and visual plans when a user selects a specific query ID…"| 4__4_3
    4__4_1 -->|"Provides the resource group hierarchy and cluster state context used to filter and categorize the a…"| 4__4_2
    4__4_4 -->|"Orchestrates the global refresh loop that triggers periodic polling of cluster-wide health and work…"| 4__4_1
    4__4_3 -->|"Correlates stage-level performance issues with specific worker health metrics or resource group con…"| 4__4_1
  end
  3 -->|"Validates SQL syntax and provides grammar context for the editor and plan visualizers."| 2
  3 -->|"Submits SQL queries for execution and manages the lifecycle of the query session."| 1
  4 -->|"Polls the Coordinator's REST endpoints to retrieve cluster health, worker status, and query executi…"| 1
  2 -->|"Enriches worker-level diagnostic views with SQL-aware metadata for better troubleshooting."| 4
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

This system represents a Presto UI architecture designed for interactive query development, cluster monitoring, and real-time performance diagnostics. The main flow involves the Interactive Query Workspace submitting SQL queries via the REST Protocol & Session Manager, while the SQL Parser & Diagnostic Engine provides syntax validation and diagnostic context. Simultaneously, the Cluster Monitoring & Resource Dashboard polls the Coordinator to maintain a real-time view of system health and resource utilization, with the diagnostic engine enriching these views with SQL-aware metadata to facilitate troubleshooting.

### REST Protocol & Session Manager

Manages the low-level communication with the Presto Coordinator, implementing the Presto REST API protocol for query submission and result retrieval while maintaining session state.

- **REST Protocol Client** — Implements the asynchronous Presto REST protocol.
- **Session State Manager** — Manages the lifecycle and validation of Presto session properties, including filtering, highlighting altered settings, and preparing the session context for REST API calls.
- **Query UI Orchestrator** — Acts as the primary integration layer for the query interface, coordinating the display of query headers, progress bars, and results while providing the entry point for session configuration.

### SQL Parser & Diagnostic Engine

Uses ANTLR4-generated parsers to decompose SQL statements for client-side validation, syntax highlighting, and mapping worker execution threads to SQL constructs for diagnostics.

- **SQL Grammar & AST Foundation** — Contains the structural definition of the Presto SQL dialect.
- **Client-Side SQL Editor & Validator** — The user-facing interface for SQL input.
- **Diagnostic Mapping & Thread Analysis** — The core logic engine that bridges the static SQL structure with dynamic execution data.
- **Query Execution Dashboard & Orchestration** — Manages the lifecycle of query execution and the visualization of performance metrics.

### Interactive Query Workspace

The primary user interface for query development and performance tuning, providing a SQL editor and D3.js-based visualization of execution plans and data distribution.

- **SQL Development & Submission** — Manages the authoring environment and the lifecycle of query submission.
- **Query Execution Monitoring** — Responsible for tracking the lifecycle of queries across the cluster.
- **Plan Visualization Engine** — A specialized visualization layer that transforms complex execution plan data into interactive graphical representations.
- **Cluster Health & Infrastructure** — Provides a global view of the Presto cluster's state, independent of individual queries.
- **UI Foundation & Shared Services** — Provides the common architectural framework and reusable UI components for the workspace.

### Cluster Monitoring & Resource Dashboard

Aggregates high-level cluster metrics, providing views into worker health, query stage progress, and resource group management by polling the Coordinator.

- **Cluster Health & Resource Monitor** — Manages the high-level physical and logical state of the cluster, including real-time monitoring of workers, memory, CPU, and Resource Group hierarchies.
- **Query Discovery & Management** — Handles the primary query lifecycle, listing, and client-side SQL parsing, providing filtering and sorting for query discovery.
- **Execution Analysis & Visualization** — Provides granular deep-dive analysis of query performance, including task-level statistics and interactive execution plan visualization using D3.js.
- **Dashboard Framework** — The foundational orchestration layer defining the React component registry, routing, and shared utilities for API interaction.

