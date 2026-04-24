```mermaid
graph LR
  subgraph 1["Backend Orchestrator"]
    1__1_1["API Orchestration & Control Plane"]
    1__1_2["Code Host Integration Layer"]
    1__1_3["Indexing & Search Pipeline"]
    1__1_4["Data Management & Maintenance"]
    1__1_5["Client Interface Layer"]
    1__1_1 -->|"triggers discovery and sync of repositories"| 1__1_2
    1__1_1 -->|"delegates indexing tasks"| 1__1_3
    1__1_5 -->|"sends search queries and configuration requests"| 1__1_1
    1__1_3 -->|"provides processed search results back via the orchestrator"| 1__1_5
    1__1_4 -->|"operates directly on the shared database used by the orchestrator"| 1__1_1
    1__1_1 -->|"receives webhook triggers to initiate real-time updates"| 1__1_2
  end
  subgraph 2["Search Engine"]
    2__2_1["Query Parser & IR Generator"]
    2__2_2["Zoekt Search Client"]
    2__2_3["Result Transformer & Enricher"]
    2__2_1 -->|"Provides the structured QueryIR used to construct the final gRPC search parameters."| 2__2_2
    2__2_2 -->|"Passes raw gRPC response buffers and stream chunks for enrichment and model transformation."| 2__2_3
  end
  subgraph 3["AI Agent Layer"]
    3__3_1["Review Agent Engine"]
    3__3_2["Agentic Tooling System"]
    3__3_3["Chat Intelligence & UX"]
    3__3_3 -->|"invokes the glob tool to locate relevant files when answering user queries"| 3__3_2
    3__3_1 -->|"utilizes file discovery tools to resolve repository information and context for specific file diffs"| 3__3_2
    3__3_1 -->|"parsed review data and AI-generated feedback are passed to the UI components for rendering"| 3__3_3
    3__3_3 -->|"interacts with the internal Chat API routes to manage model state and fetch collaboration metadata"| 3__3_3
  end
  subgraph 4["Repository & Security Manager"]
    4__4_1["Identity & Credential Manager"]
    4__4_2["Permission & Access Controller"]
    4__4_3["Secure Repository Access Layer"]
    4__4_1 -->|"Provides the authenticated user context and validated API key metadata required to determine access…"| 4__4_2
    4__4_2 -->|"Injects repository-level permission filters into Git data retrieval queries to enforce row-level se…"| 4__4_3
  end
  subgraph 5["Web UI & Editor"]
    5__5_1["Global Application Shell & State"]
    5__5_2["Search Context & Scope Management"]
    5__5_3["Code Intelligence & Editor UI"]
    5__5_1 -->|"Provides the sidebar and navigation context for scope selection."| 5__5_2
    5__5_2 -->|"Supplies the selected repository context for code retrieval and display."| 5__5_3
    5__5_1 -->|"Manages the application shell and notification system for editor-related actions."| 5__5_3
  end
  subgraph 6["Enterprise Services"]
    6__6_1["Enterprise Analytics"]
    6__6_2["Compliance & Audit"]
    6__6_3["Identity & Access Management (IAM)"]
    6__6_4["Enterprise Infrastructure & Intelligence"]
    6__6_3 -->|"Records authentication attempts, permission changes, and administrative actions to the audit log."| 6__6_2
    6__6_3 -->|"Provides refreshed OAuth tokens and user identities required for organization-wide repository acces…"| 6__6_4
    6__6_3 -->|"Supplies user and organization context to scope and filter usage metrics."| 6__6_1
    6__6_4 -->|"Reports usage data related to advanced code navigation and search context features for adoption tra…"| 6__6_1
  end
  5 -->|"Sends search queries and repository management requests via API"| 1
  1 -->|"Triggers repository indexing and executes raw search queries"| 2
  3 -->|"Retrieves relevant code snippets and context for RAG workflows"| 2
  1 -->|"Validates user permissions and fetches Git metadata for indexing"| 4
  5 -->|"Initiates interactive chat sessions and agentic code analysis"| 3
  6 -->|"Queries system state for audit logs and usage analytics"| 1
  3 -->|"Persists chat history and manages agent state"| 1
  5 -->|"Authenticates users and manages session state"| 4
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

Sourcebot is a high-performance code search and intelligence platform where the Web UI & Editor serves as the entry point for user interaction, sending requests to the Backend Orchestrator. The Backend Orchestrator manages indexing and security by coordinating with the Search Engine for retrieval and the Repository & Security Manager for access control. The AI Agent Layer integrates with both the Search Engine for RAG-based context and the Backend Orchestrator for state persistence, while Enterprise Services provide additional auditing and analytics capabilities.

### Backend Orchestrator

The central server-side hub responsible for API orchestration, background job management, and system-wide utilities. It coordinates repository indexing and manages the lifecycle of connections to external code hosts.

- **API Orchestration & Control Plane** — The central management layer that coordinates all backend activities, handles server lifecycle, manages background worker stability, and provides the primary entry point for system-wide operations.
- **Code Host Integration Layer** — Implements the Adapter Pattern to interface with various version control systems, handling repository discovery, permission syncing, and filtering.
- **Indexing & Search Pipeline** — The data transformation engine that converts raw Git repository data into searchable Zoekt indices and provides query parsing logic.
- **Data Management & Maintenance** — Provides administrative utilities and maintenance scripts for the underlying PostgreSQL database, including migrations and data deduplication.
- **Client Interface Layer** — The "Northbound" consumer surface consisting of Next.js application routes and React components that translate user actions into API calls.

### Search Engine

The high-performance indexing and retrieval core. It interfaces with Zoekt via gRPC to execute complex regex searches and transforms raw search results into structured application models.

- **Query Parser & IR Generator** — Responsible for the lexical analysis and syntactic parsing of search queries.
- **Zoekt Search Client** — Manages the low-level gRPC lifecycle and protocol translation.
- **Result Transformer & Enricher** — Performs post-processing on raw search hits.

### AI Agent Layer

Powers the platform's intelligence features, including RAG-based chat, automated code reviews, and agentic tool use. it manages LLM provider selection and context window optimization.

- **Review Agent Engine** — Responsible for the ingestion and transformation of version control data into AI-ready context.
- **Agentic Tooling System** — Provides the "hands" for the AI agents, allowing them to interact with the codebase programmatically.
- **Chat Intelligence & UX** — Manages the end-to-end chat experience, including model selection, RAG source visualization, and collaborative metadata.

### Repository & Security Manager

Manages the security perimeter and data access layer. It handles user authentication, API key lifecycles, and enforces repository-level permissions at the database query level.

- **Identity & Credential Manager** — Manages the lifecycle of user identities and programmatic access credentials.
- **Permission & Access Controller** — The core logic engine responsible for enforcing the security perimeter.
- **Secure Repository Access Layer** — Provides the data access interface for Git repository structures.

### Web UI & Editor

The primary user interface, featuring a sophisticated code editor with syntax highlighting, navigation tools, and a global application shell for notifications and onboarding.

- **Global Application Shell & State** — Manages the persistent UI framework, including the global application shell, navigation sidebar, and cross-cutting state like notifications and user identity.
- **Search Context & Scope Management** — Handles the selection and management of search scopes (repositories and context) within the chat interface, allowing users to filter the AI's retrieval context.
- **Code Intelligence & Editor UI** — Implements the sophisticated code editor features, including code block rendering, syntax highlighting, code folding, and navigation through referenced source files.

### Enterprise Services

Provides specialized features for enterprise deployments, including usage analytics, audit logging, and license management.

- **Enterprise Analytics** — Aggregates and visualizes platform usage metrics, enabling administrators to monitor active users, search volume, and AI chat engagement across various interfaces.
- **Compliance & Audit** — Manages the recording and lifecycle of security-relevant events, providing an auditable history of user actions and automated log retention enforcement.
- **Identity & Access Management (IAM)** — Handles enterprise-grade authentication (SSO) and ensures that user repository permissions are continuously synchronized with external identity and code providers.
- **Enterprise Infrastructure & Intelligence** — Manages organization-wide integrations like GitHub Apps and provides advanced code intelligence features such as symbol-based exploration and search context synchronization.

