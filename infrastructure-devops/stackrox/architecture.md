```mermaid
graph LR
  subgraph 1["Central Management Plane"]
    1__1_1["API Gateway & Orchestration Hub"]
    1__1_2["Data Persistence & System Configuration"]
    1__1_3["Security Analysis & Compliance Engines"]
    1__1_4["External Connectivity & Notifiers"]
    1__1_5["Management Interfaces (UI & CLI)"]
    1__1_6["Operator & Deployment Logic"]
    1__1_5 -->|"sends API requests to"| 1__1_1
    1__1_1 -->|"performs database operations on"| 1__1_2
    1__1_1 -->|"orchestrates security tasks by delegating to"| 1__1_3
    1__1_3 -->|"reports security findings and compliance status back to"| 1__1_1
    1__1_1 -->|"dispatches security alerts and findings to external sinks via"| 1__1_4
    1__1_6 -->|"manages the deployment state and configuration of"| 1__1_1
  end
  subgraph 2["Sensor & Cluster Agent"]
    2__2_1["Cloud Integration Client"]
    2__2_2["Sensor Lifecycle Manager"]
    2__2_3["Environmental Scope Provider"]
    2__2_2 -->|"Queries cluster-specific labels and metadata to ensure the upgrader configuration is consistent wit…"| 2__2_3
    2__2_1 -->|"Correlates discovered cloud resources with local cluster identity and labels for unified reporting."| 2__2_3
    2__2_2 -->|"Uses cloud-specific identifiers to determine provider-specific upgrade paths (e.g., EKS vs GKE spec…"| 2__2_1
  end
  subgraph 3["Scanner Service"]
    3__3_1["Scanner Core & Definition Manager"]
    3__3_2["Vulnerability API & Search Engine"]
    3__3_3["Exception & Governance Controller"]
    3__3_4["Reporting & Export Service"]
    3__3_5["Security Context & Visualization"]
    3__3_1 -->|"Synchronizes the latest vulnerability definitions to the queryable database."| 3__3_2
    3__3_2 -->|"Provides the image and CVE context required to validate and scope exception requests."| 3__3_3
    3__3_2 -->|"Supplies the raw scan data and SBOM details for report generation and external distribution."| 3__3_4
    3__3_3 -->|"Updates the visual state of vulnerabilities (e.g., 'Snoozed' or 'Deferred') in the UI based on appr…"| 3__3_5
    3__3_5 -->|"Requests filtered vulnerability and image data based on user-applied search criteria and deployment…"| 3__3_2
    3__3_5 -->|"Triggers on-demand report generation and SBOM exports directly from the visualization dashboards."| 3__3_4
  end
  subgraph 4["roxctl CLI"]
    4__4_1["Command Execution Framework"]
    4__4_2["Secure Communication Layer"]
    4__4_3["Configuration Store"]
    4__4_1 -->|"Retrieves connection profiles and persists user-defined settings during command execution."| 4__4_3
    4__4_1 -->|"Utilizes the authenticated client to perform remote administrative and diagnostic operations on Cen…"| 4__4_2
    4__4_2 -->|"Accesses stored access tokens and endpoint URLs to configure the transport and authentication heade…"| 4__4_3
  end
  subgraph 5["StackRox Web UI"]
    5__5_1["UI Foundation & Security Context"]
    5__5_2["API Service Layer (Data Engine)"]
    5__5_3["Vulnerability & Risk Management"]
    5__5_4["Visualization & Reporting Engine"]
    5__5_5["Development & Build Infrastructure"]
    5__5_1 -->|"Provides authentication tokens and session context required for all backend API requests."| 5__5_2
    5__5_1 -->|"Distributes feature flags and user permissions that control access to specific security workflows."| 5__5_3
    5__5_2 -->|"Supplies the raw vulnerability, image, and workload data needed for risk assessment views."| 5__5_3
    5__5_2 -->|"Provides the structured data (e.g., network flows, event logs) used to render graphs and generate r…"| 5__5_4
    5__5_3 -->|"Utilizes visualization components to display vulnerability trends and risk distribution charts."| 5__5_4
    5__5_5 -->|"Configures the development proxy to allow the foundation's auth services to reach the backend durin…"| 5__5_1
  end
  subgraph 6["UI Testing Suite"]
    6__6_1["Search & Filter Framework Testing"]
    6__6_2["Vulnerability Management Workflow Testing"]
    6__6_3["Shared Utility Component Testing"]
    6__6_2 -->|"Domain-specific tests utilize the search framework to filter vulnerabilities and validate that the …"| 6__6_1
    6__6_2 -->|"Security workflow pages embed shared components (like the CodeViewer) to display technical details …"| 6__6_3
  end
  5 -->|"Fetches security data and manages system configuration via REST and GraphQL APIs."| 1
  4 -->|"Sends administrative commands and retrieves cluster-init bundles."| 1
  2 -->|"Streams real-time cluster events and resource state updates via mTLS-secured gRPC."| 1
  1 -->|"Dispatches policy enforcement actions and triggers automated agent upgrades."| 2
  1 -->|"Requests vulnerability scans for container images and workloads."| 3
  6 -->|"Executes automated interactions to validate frontend stability and feature correctness."| 5
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The StackRox architecture follows a Manager-Agent (Central-Sensor) pattern designed for multi-cluster Kubernetes security. The Central Management Plane acts as the brain of the system, handling data persistence, policy detection, and API orchestration. It communicates with Sensors deployed in secured clusters which monitor runtime activity and enforce policies. The Scanner Service provides specialized vulnerability analysis for container images, while users interact with the system via the StackRox Web UI or the roxctl CLI, both of which consume Central's APIs. The entire system is secured with mTLS and robust identity management to ensure safe cross-cluster communication.

### Central Management Plane

The core orchestration and data layer of StackRox. It manages the gRPC/HTTP API servers, the PostgreSQL database for persistence, and the central detection engine. It also handles identity provider integrations (OIDC/SAML) and the technical handshake logic for remote Sensors.

- **API Gateway & Orchestration Hub** — The central entry point and coordination engine for the subsystem.
- **Data Persistence & System Configuration** — The foundational data layer responsible for the persistence of all platform state.
- **Security Analysis & Compliance Engines** — Specialized engines that perform deep security analysis.
- **External Connectivity & Notifiers** — Manages all outbound communication from Central to external services.
- **Management Interfaces (UI & CLI)** — The user-facing layer of the platform, consisting of the React-based web console and the roxctl command-line tool.
- **Operator & Deployment Logic** — Handles the lifecycle and deployment of the Central Management Plane within Kubernetes.

### Sensor & Cluster Agent

The agent-side component deployed within each secured Kubernetes cluster. It manages the lifecycle of the local security stack, including cloud provider integrations and automated upgrades via the Sensor Upgrader.

- **Cloud Integration Client** — Manages authentication and communication with external cloud providers (AWS, GCP, Azure) to facilitate cluster discovery and metadata retrieval.
- **Sensor Lifecycle Manager** — Orchestrates the automated upgrade process and configuration management of the local Sensor stack.
- **Environmental Scope Provider** — Provides an abstraction layer for accessing Kubernetes-native metadata, such as cluster and namespace labels.

### Scanner Service

A specialized service dedicated to container image analysis and vulnerability management. It maintains its own update lifecycle for vulnerability definitions and provides scanning capabilities to Central.

- **Scanner Core & Definition Manager** — The foundational engine of the scanner, responsible for the lifecycle of vulnerability definitions and the operational health of the scanning service.
- **Vulnerability API & Search Engine** — The primary data access and processing layer that interfaces between the UI and the backend vulnerability database.
- **Exception & Governance Controller** — Manages the multi-step workflow for vulnerability exceptions, including deferrals and false positive markings.
- **Reporting & Export Service** — Handles the generation and distribution of security artifacts, including SBOMs and scheduled vulnerability reports.
- **Security Context & Visualization** — The presentation layer that contextualizes vulnerability data within the Kubernetes environment.

### roxctl CLI

The administrative command-line tool used for interacting with Central, managing configurations, and performing cluster initialization tasks.

- **Command Execution Framework** — Orchestrates the CLI lifecycle, including command hierarchy definition, flag parsing, and the execution of administrative tasks like database backups or diagnostics.
- **Secure Communication Layer** — Manages the low-level mechanics of interacting with the Central API.
- **Configuration Store** — Provides a persistence mechanism for roxctl local state, managing the storage and retrieval of Central endpoints and associated credentials in a YAML-based configuration file.

### StackRox Web UI

The React-based frontend application. It provides a comprehensive dashboard for security monitoring, network graphing, policy management, and vulnerability reporting. It includes its own session management and data-fetching engine.

- **UI Foundation & Security Context** — Provides the foundational environment for the application, including global state management, feature flagging, routing, and the security lifecycle (authentication, token management, and session persistence).
- **API Service Layer (Data Engine)** — The central data-fetching engine that abstracts gRPC and REST interactions with the StackRox Central API.
- **Vulnerability & Risk Management** — A specialized functional module focused on security posture, specifically managing CVEs (Common Vulnerabilities and Exposures) and the workflow for granting security exceptions or deferrals.
- **Visualization & Reporting Engine** — Handles complex data visualization requirements, including interactive network graphs, runtime event timelines, and the generation of downloadable PDF/CSV security reports.
- **Development & Build Infrastructure** — Contains the non-functional code required for the development environment, including proxy configurations for local API communication and global test setup utilities.

### UI Testing Suite

The Cypress-based testing framework used to validate the UI components and end-to-end user workflows.

- **Search & Filter Framework Testing** — Validates the core "Compound Search Filter" logic, which is the primary mechanism for data discovery in the platform.
- **Vulnerability Management Workflow Testing** — Tests end-to-end security workflows within the Vulnerability Management module.
- **Shared Utility Component Testing** — Focuses on the unit-level validation of reusable UI components that provide platform-wide utility, such as the CodeViewer for inspecting YAML configurations or policy definitions.

