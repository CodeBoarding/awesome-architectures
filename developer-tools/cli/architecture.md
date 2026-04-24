```mermaid
graph LR
  subgraph 1["CLI Command Framework"]
    1__1_1["Framework Core & Configuration Engine"]
    1__1_2["Project Lifecycle & Scaffolding"]
    1__1_3["Content & Data Services"]
    1__1_4["Governance, Security & Integration"]
    1__1_1 -->|"Provides the SanityCommand base class and configuration loading mechanism required for project-leve…"| 1__1_2
    1__1_1 -->|"Supplies the authenticated API client and project context (e.g., dataset name) needed for data-inte…"| 1__1_3
    1__1_1 -->|"Provides the underlying request infrastructure and configuration for administrative and schema-rela…"| 1__1_4
    1__1_2 -->|"The initialization process (init) often triggers dataset creation and initial content imports to bo…"| 1__1_3
    1__1_4 -->|"Schema definitions and security rules (CORS) define the structure and access permissions for conten…"| 1__1_3
  end
  subgraph 2["Core Logic & Services"]
    2__2_1["Execution Engine & Context"]
    2__2_2["Identity & Client Services"]
    2__2_3["Domain Operations & Scaffolding"]
    2__2_4["Telemetry & Observability"]
    2__2_5["Development & Test Support"]
    2__2_1 -->|"provides configuration to"| 2__2_2
    2__2_2 -->|"supplies authenticated clients to"| 2__2_3
    2__2_3 -->|"emits events to"| 2__2_4
    2__2_1 -->|"records metadata to"| 2__2_4
    2__2_2 -->|"tracks auth metrics to"| 2__2_4
    2__2_1 -->|"resolves configuration for"| 2__2_3
    2__2_5 -->|"exercises flow through tests in"| 2__2_1
  end
  subgraph 3["Schema & Transformation Engine"]
    3__3_1["Orchestration & Codemod Layer"]
    3__3_2["Multi-Version GraphQL Engine"]
    3__3_3["Document Validation Engine"]
    3__3_4["Schema Extraction & Core Utilities"]
    3__3_1 -->|"Triggers the generation and deployment of GraphQL schemas based on CLI flags."| 3__3_2
    3__3_1 -->|"Initiates document integrity checks and manages worker lifecycle."| 3__3_3
    3__3_2 -->|"Consumes extracted schema definitions to map them to GraphQL types and filters."| 3__3_4
    3__3_3 -->|"Uses schema metadata to validate document fields and reference constraints."| 3__3_4
  end
  subgraph 4["Dev Runtime & Templates"]
    4__4_1["Dev Server Orchestrator"]
    4__4_2["Vite Plugin Engine"]
    4__4_3["Storefront Template Logic"]
    4__4_1 -->|"Injects Sanity-specific plugins into the Vite configuration during server initialization."| 4__4_2
    4__4_2 -->|"Monitors and analyzes template source files to extract schema metadata and generate TypeScript defi…"| 4__4_3
    4__4_1 -->|"Resolves and serves template-specific assets and logic to the client-side Studio application."| 4__4_3
  end
  subgraph 5["Integration & Support"]
    5__5_1["External Protocol Integration (MCP)"]
    5__5_2["Package & Environment Orchestrator"]
    5__5_3["Terminal UX & Presentation Layer"]
    5__5_4["Testing & Maintenance Suite"]
    5__5_5["CLI Foundation & System Utilities"]
    5__5_4 -->|"Uses package manager utilities to prepare isolated test environments and install dependencies for E…"| 5__5_2
    5__5_4 -->|"Spawns CLI processes to verify command behavior and framework integrity during testing."| 5__5_5
    5__5_1 -->|"Relies on system utilities to resolve project roots and read/write configuration files during the M…"| 5__5_5
    5__5_1 -->|"Triggers package installations when configuring the MCP server within a user's project."| 5__5_2
    5__5_5 -->|"Routes command execution results and progress updates to the UX layer for formatted terminal displa…"| 5__5_3
  end
  1 -->|"Delegates user-initiated actions to core business logic and API services."| 2
  1 -->|"Triggers local development servers and production build pipelines."| 4
  2 -->|"Supplies project and API context required for schema validation and generation."| 3
  3 -->|"Utilizes authenticated API clients to deploy generated schemas and GraphQL definitions."| 2
  4 -->|"Invokes schema extraction logic to provide metadata for the local Studio runtime."| 3
  2 -->|"Leverages external protocols (MCP) and terminal utilities for enhanced user interaction and AI inte…"| 5
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The Sanity CLI architecture follows a command-driven pattern where user interactions are parsed by a framework layer and delegated to specialized service modules. The flow typically begins with environment initialization and configuration resolution, followed by the execution of specific actions (such as dataset management, document validation, or schema deployment) that interact with the Sanity API. A dedicated development system manages local studio environments and build processes, while a schema engine handles complex data structure extraction and GraphQL generation.

### CLI Command Framework

Handles the CLI lifecycle, including argument parsing via oclif, project configuration loading, and environment initialization. It provides the base command structures that all CLI features inherit from.

- **Framework Core & Configuration Engine** — Provides the foundational infrastructure for the CLI, including the base command class, configuration discovery, and environment initialization.
- **Project Lifecycle & Scaffolding** — Orchestrates the primary developer workflows for Sanity projects, including initialization, local development, and production builds.
- **Content & Data Services** — Implements the command set for managing Sanity's content lake.
- **Governance, Security & Integration** — Manages the administrative and structural aspects of a Sanity project.

### Core Logic & Services

The central execution engine of the CLI, managing authentication, API client instantiation, and core business logic for project and data operations. It also integrates telemetry for usage tracking.

- **Execution Engine & Context** — Manages the CLI's runtime environment, including project root discovery, configuration parsing (e.g., sanity.config.ts), and the execution of scripts and workers.
- **Identity & Client Services** — Handles user authentication cycles (OAuth, provider selection) and manages the lifecycle of the Sanity API client, including token caching and request configuration.
- **Domain Operations & Scaffolding** — Implements the core business logic for Sanity resources (datasets, schemas, backups) and provides the templates and blueprints used during project initialization.
- **Telemetry & Observability** — Provides a persistent store and transmission mechanism for usage data, command traces, and error reporting, ensuring non-blocking event flushing to the backend.
- **Development & Test Support** — Contains internal utilities, E2E test setups, and CI tools used to ensure the quality and coverage of the CLI codebase during development.

### Schema & Transformation Engine

Manages the extraction, validation, and deployment of Sanity schemas. This component also handles automated code transformations (codemods) and GraphQL API generation across different versions.

- **Orchestration & Codemod Layer** — Acts as the primary entry point for schema-related CLI commands.
- **Multi-Version GraphQL Engine** — A versioned generation engine that translates Sanity schemas into GraphQL SDL.
- **Document Validation Engine** — Executes deep validation of Sanity documents against their defined schemas.
- **Schema Extraction & Core Utilities** — Provides the foundational logic for extracting schema definitions from the user's workspace.

### Dev Runtime & Templates

Provides the infrastructure for local development, including the Vite-based development server and build plugins. It also contains template-specific logic for specialized storefronts like Shopify.

- **Dev Server Orchestrator** — Manages the lifecycle of the development and preview servers.
- **Vite Plugin Engine** — A collection of Vite-specific plugins that extend the build process for Sanity Studio.
- **Storefront Template Logic** — Contains the domain-specific schemas, document actions, and UI logic for specialized storefronts like Shopify.

### Integration & Support

Encompasses external protocol integrations (like MCP), terminal UX utilities, package management helpers, and the end-to-end testing suite.

- **External Protocol Integration (MCP)** — Manages the Model Context Protocol (MCP) integration, allowing AI-enabled editors like VSCode, Cursor, and Zed to interact with Sanity projects.
- **Package & Environment Orchestrator** — Abstracts interactions with Node.js package managers (npm, yarn, pnpm, bun) and provides browser API mocks (DOM, observers) to enable the execution of browser-targeted Studio code within the Node.js CLI environment.
- **Terminal UX & Presentation Layer** — Responsible for the "View" layer of the CLI, transforming raw data into human-readable terminal output.
- **Testing & Maintenance Suite** — Provides the framework for end-to-end testing of the CLI in simulated environments using PTYs (Pseudo-Terminals), along with internal tools for documentation generation and project health checks.
- **CLI Foundation & System Utilities** — The foundational layer providing the oclif-based command loading framework and low-level utilities for file system operations, environment detection, and configuration resolution.

