```mermaid
graph LR
  subgraph 1["Connector Registry & Documentation"]
    1__1_1["Registry Data & Metadata Orchestrator"]
    1__1_2["Content Transformation & Navigation"]
    1__1_3["Interactive Documentation UI"]
    1__1_4["Operational Services & Integrations"]
    1__1_1 -->|"Provides validated registry JSON and metadata for sidebar generation and content injection."| 1__1_2
    1__1_1 -->|"Supplies raw connector data and schemas for runtime rendering."| 1__1_3
    1__1_2 -->|"Defines page structure and mounts interactive React components during build."| 1__1_3
    1__1_3 -->|"Triggers and displays operational data (e.g., cloud status) within the UI."| 1__1_4
  end
  subgraph 2["Java Integration Engine"]
    2__2_1["Connector Runtime Orchestrator"]
    2__2_2["Relational & API Connectivity Layer"]
    2__2_3["NoSQL & CDC Processing Engine"]
    2__2_4["Warehouse Staging & Bulk Load Toolkit"]
    2__2_5["File Transformation & Local Storage"]
    2__2_6["Performance Benchmarking Suite"]
    2__2_1 -->|"Delegates SQL execution and connection management for structured data sources."| 2__2_2
    2__2_1 -->|"Triggers CDC event capture and manages state snapshots for non-relational sources."| 2__2_3
    2__2_1 -->|"Executes high-throughput data promotion to cloud warehouses via staging buffers."| 2__2_4
    2__2_4 -->|"Utilizes serialization logic to format data into Parquet or CSV for staging files."| 2__2_5
    2__2_6 -->|"Exercises core protocol methods to measure engine performance under load."| 2__2_1
    2__2_3 -->|"Streams mapped JSON records back to the core execution engine for protocol-compliant output."| 2__2_1
  end
  subgraph 3["Python CDK & Connector Framework"]
    3__3_1["CDK Core & Declarative Framework"]
    3__3_2["SaaS & API Source Integration Layer"]
    3__3_3["File & Bulk Storage Integration Layer"]
    3__3_4["Cloud & Vector Destination Layer"]
    3__3_5["Connector Testing & Mocking Framework"]
    3__3_1 -->|"Provides base classes and declarative engine for API-based record extraction."| 3__3_2
    3__3_1 -->|"Provides stream abstractions and protocol logic for file-based data reading."| 3__3_3
    3__3_1 -->|"Provides the foundational destination protocol implementation and shared write logic."| 3__3_4
    3__3_5 -->|"Validates source connector behavior by simulating external API responses."| 3__3_2
    3__3_5 -->|"Verifies data ingestion and indexing logic through integration test suites."| 3__3_4
  end
  subgraph 4["Connector Lifecycle & CI Tooling"]
    4__4_1["Connector Registry & Documentation"]
    4__4_2["CI/CD Orchestration & Secret Management"]
    4__4_3["Connector Validation & Benchmarking"]
    4__4_4["Connector Implementation Layer"]
    4__4_2 -->|"Orchestrates integration tests and injects rotated secrets into connector containers during the CI …"| 4__4_4
    4__4_2 -->|"Executes performance benchmarks and platform stability tests using specialized mock connectors."| 4__4_3
    4__4_1 -->|"Extracts JSON schemas and specifications from connector implementations to populate the registry an…"| 4__4_4
    4__4_2 -->|"Triggers registry metadata refreshes and documentation rebuilds upon successful connector deploymen…"| 4__4_1
  end
  subgraph 5["Integration Testing & Benchmarking"]
    5__5_1["Connector Registry & Metadata"]
    5__5_2["Test Execution & Secret Management"]
    5__5_3["Protocol Verification & Mocking"]
    5__5_4["Performance Benchmarking & Synthetic Sources"]
    5__5_1 -->|"Provides the connector manifests and versioning data that define the scope and targets for CI test …"| 5__5_2
    5__5_2 -->|"Injects authenticated credentials into the test environment and triggers the execution of protocol …"| 5__5_3
    5__5_2 -->|"Orchestrates the execution of benchmarking jobs and manages the environment variables required for …"| 5__5_4
    5__5_3 -->|"Validates that the synthetic data streams used for benchmarking are structurally compliant with the…"| 5__5_4
  end
  3 -->|"Publishes connector specifications and metadata for UI rendering and discovery."| 1
  2 -->|"Provides registry entries and configuration schemas for database and JDBC-based integrations."| 1
  4 -->|"Injects credentials and orchestrates automated integration tests during the connector build process."| 3
  5 -->|"Exercises Java-based sources and destinations with synthetic loads to ensure protocol compliance an…"| 2
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

Airbyte's architecture is a protocol-driven ecosystem designed for high extensibility and isolation. The platform's core data flow is orchestrated through specialized Connector Development Kits (CDK) for Java and Python, which standardize how data is ingested from sources and delivered to destinations. These connectors are validated by a dedicated testing and benchmarking layer to ensure protocol compliance, while a centralized CI/CD and secret management system handles the operational lifecycle. Finally, a registry and documentation layer serves as the discovery interface, consuming metadata from the connectors to provide a unified view of the integration ecosystem.

### Connector Registry & Documentation

Manages the public-facing catalog and technical documentation for all Airbyte connectors. It processes connector metadata and OpenAPI specifications to render the interactive registry and documentation site.

- **Registry Data & Metadata Orchestrator** — Acts as the "Source of Truth" manager for the subsystem, fetching remote registry definitions, extracting metadata from connectors, and validating OpenAPI specifications.
- **Content Transformation & Navigation** — Manages Docusaurus build-time logic, using Remark plugins to inject dynamic connector specifications into Markdown and programmatically generating navigation sidebars.
- **Interactive Documentation UI** — The frontend "View" layer consisting of React components that render the interactive connector catalog, searchable grids, and JSON schema viewers.
- **Operational Services & Integrations** — Handles runtime auxiliary features, including real-time Airbyte Cloud status updates and third-party integrations like Kapa.ai.

### Java Integration Engine

The high-performance runtime for database, warehouse, and streaming integrations. It handles complex SQL generation, connection pooling, and data serialization for Java-based sources and destinations.

- **Connector Runtime Orchestrator** — The central entry point that manages the lifecycle of connector execution.
- **Relational & API Connectivity Layer** — Handles low-level interactions with relational databases and specialized cloud management APIs.
- **NoSQL & CDC Processing Engine** — A specialized engine for handling non-relational data models and Change Data Capture (CDC).
- **Warehouse Staging & Bulk Load Toolkit** — Manages high-performance data loading patterns for cloud warehouses.
- **File Transformation & Local Storage** — Responsible for the serialization and deserialization of data from file-based sources and local storage destinations.
- **Performance Benchmarking Suite** — Provides tools for measuring the throughput and latency of the integration engine.

### Python CDK & Connector Framework

The primary development framework for SaaS and API-based connectors. It provides declarative and imperative patterns for authentication, record extraction, and schema transformation.

- **CDK Core & Declarative Framework** — The foundational framework providing the Airbyte protocol implementation, base classes for sources and streams, and a declarative engine for low-code connector development.
- **SaaS & API Source Integration Layer** — Implements source connectors for SaaS platforms and REST APIs.
- **File & Bulk Storage Integration Layer** — Specialized connectors for reading data from file systems and bulk storage services (S3, GCS, SFTP).
- **Cloud & Vector Destination Layer** — Manages the ingestion of data into modern cloud data lakes and vector databases.
- **Connector Testing & Mocking Framework** — Provides the infrastructure for integration testing of connectors.

### Connector Lifecycle & CI Tooling

Automates the operational aspects of the connector ecosystem, including secret rotation from Google Secret Manager and the orchestration of CI/CD pipelines for connector integration tests.

- **Connector Registry & Documentation** — Manages the discovery, cataloging, and presentation of the Airbyte connector ecosystem.
- **CI/CD Orchestration & Secret Management** — Automates the operational aspects of connector testing and deployment.
- **Connector Validation & Benchmarking** — Provides specialized internal tooling for validating platform stability and measuring connector performance.
- **Connector Implementation Layer** — Contains the core business logic for the various source and destination connectors.

### Integration Testing & Benchmarking

Provides the infrastructure for end-to-end validation and performance testing. It generates synthetic data streams to verify protocol compliance and measure connector throughput.

- **Connector Registry & Metadata** — Acts as the source of truth for the testing subsystem by maintaining the catalog of connectors and their versions.
- **Test Execution & Secret Management** — Provides the foundational infrastructure for running automated tests in a secure environment.
- **Protocol Verification & Mocking** — A dual-purpose component that simulates external API responses and validates internal protocol compliance.
- **Performance Benchmarking & Synthetic Sources** — Focuses on measuring connector throughput and resource utilization.

