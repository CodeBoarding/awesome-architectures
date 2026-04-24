```mermaid
graph LR
  subgraph 1["App Orchestrator & UI Shell"]
    1__1_1["Root Orchestrator & Layout"]
    1__1_2["Navigation & Workspace Manager"]
    1__1_3["Editor Shell & Block Registry"]
    1__1_4["AI Assistant Orchestrator"]
    1__1_5["Global State & Event Infrastructure"]
    1__1_1 -->|"renders"| 1__1_2
    1__1_2 -->|"determines active context for"| 1__1_3
    1__1_3 -->|"provides execution context and UI anchors to"| 1__1_4
    1__1_4 -->|"sends generated content back to"| 1__1_3
    1__1_5 -->|"broadcasts system-level events to"| 1__1_1
    1__1_1 -->|"invokes to manage modal dialogs"| 1__1_5
  end
  subgraph 2["Runbook Editor & Content Engine"]
    2__2_1["Editor Core & Layout"]
    2__2_2["Block Content Engines"]
    2__2_3["External Integration Previews"]
    2__2_4["History & Analytics Engine"]
    2__2_1 -->|"Orchestrates the rendering lifecycle and synchronizes the global runbook state with block-specific …"| 2__2_2
    2__2_1 -->|"Triggers data retrieval and embeds provider-specific UI components when external links are detected."| 2__2_3
    2__2_2 -->|"Streams execution results, exit codes, and performance metadata for persistence and analysis."| 2__2_4
    2__2_4 -->|"Supplies historical execution context and previous output data to the editor for comparison and re-…"| 2__2_1
    2__2_2 -->|"Utilizes shared infrastructure like PlayButton and ResizeHandle to maintain a consistent interactio…"| 2__2_1
  end
  subgraph 3["Workspace & Data Manager"]
    3__3_1["Workspace Orchestration & Lifecycle"]
    3__3_2["Local Persistence & Data Models"]
    3__3_3["Search & Indexing Service"]
    3__3_1 -->|"Persists and retrieves workspace metadata, configuration, and synchronization state."| 3__3_2
    3__3_1 -->|"Triggers incremental re-indexing of runbook content when file system changes are detected or manual…"| 3__3_3
    3__3_3 -->|"References persisted workspace IDs and metadata to scope search results and provide context for ind…"| 3__3_2
  end
  subgraph 4["System Execution Engine"]
    4__4_1["Terminal UI & Lifecycle Manager"]
    4__4_2["PTY Execution & Stream Engine"]
    4__4_3["Document Integration Bridge"]
    4__4_1 -->|"Binds interactive terminal instances to active backend PTY sessions and forwards user input/resize …"| 4__4_2
    4__4_2 -->|"Streams real-time stdout/stderr data and execution status updates for rendering in the terminal emu…"| 4__4_1
    4__4_2 -->|"Commits execution metadata, command lifecycle events, and final exit codes to the persistent docume…"| 4__4_3
    4__4_3 -->|"Provides the necessary block-level context and historical execution state required to restore termi…"| 4__4_1
  end
  subgraph 5["AI Orchestrator"]
    5__5_1["AI Session Orchestrator"]
    5__5_2["AI Interaction UI"]
    5__5_1 -->|"Provides synchronized session state and real-time event updates for rendering."| 5__5_2
    5__5_2 -->|"Triggers session selection and user-initiated actions (e.g., sending new prompts) that update the o…"| 5__5_1
  end
  subgraph 6["Sync & Connectivity Layer"]
    6__6_1["Socket & Connection Manager"]
    6__6_2["Channel & Messaging Abstraction"]
    6__6_1 -->|"Provides the active, authenticated socket instance required to instantiate and join specific commun…"| 6__6_2
    6__6_2 -->|"Reports protocol-level errors or join failures that may indicate a need for connection re-establish…"| 6__6_1
  end
  1 -->|"Instantiates and manages editor tabs and their associated state."| 2
  2 -->|"Triggers block execution and shell commands based on user interaction."| 4
  4 -->|"Streams terminal output and execution logs back to the main UI for display."| 1
  1 -->|"Requests file system operations and persists application-wide state."| 3
  3 -->|"Propagates local database changes for remote synchronization and collaboration."| 6
  1 -->|"Delegates AI-assisted tasks and manages specialized AI tool sessions."| 5
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The desktop application follows a local-first, block-based architecture where the App Orchestrator & UI Shell serves as the central coordinator for state and navigation. Users interact with the Runbook Editor & Content Engine to compose and execute workflows, which are processed by the System Execution Engine for local shell tasks or the AI Orchestrator for intelligent assistance. Data is managed by the Workspace & Data Manager, which handles local persistence and file system watching, while the Sync & Connectivity Layer ensures real-time collaboration and state synchronization with remote services via Phoenix channels. This structure separates high-level UI management from low-level system execution and network synchronization, ensuring a responsive and secure developer environment.

### App Orchestrator & UI Shell

The central hub of the application that manages the global state, windowing system, and navigation lifecycle. It coordinates between the UI, the AI assistant, and the execution engine while handling tab management and modal dialogs.

- **Root Orchestrator & Layout** — Primary entry point and layout coordinator.
- **Navigation & Workspace Manager** — Manages the hierarchical organization, workspace tree, and multi-tab interface.
- **Editor Shell & Block Registry** — Primary content container that manages the rendering of the block-based editor, coordinating block types and execution outputs.
- **AI Assistant Orchestrator** — Coordinates AI integration, managing the AI chat assistant state and inline generation hooks within the editor.
- **Global State & Event Infrastructure** — Provides low-level communication and state management, including the event bus and centralized dialog management.

### Runbook Editor & Content Engine

Manages the interactive block-based editor and rich content previews. It handles the granular state of different block types (HTTP, SQL, Script) and provides the UI for historical data and external integrations like GitHub/GitLab.

- **Editor Core & Layout** — Manages the foundational framework of the interactive editor, including the high-level state transitions, layout constraints, and generic execution triggers.
- **Block Content Engines** — Handles the complex internal logic and specialized UI requirements for specific block types.
- **External Integration Previews** — Provides a standardized mechanism for fetching and rendering rich metadata from external Git providers.
- **History & Analytics Engine** — Processes and visualizes post-execution data.

### Workspace & Data Manager

Responsible for the hierarchical organization of runbooks and folders. It manages local file system interactions, full-text search indexing, and data persistence to the local SQLite/KV stores.

- **Workspace Orchestration & Lifecycle** — Central controller for workspace operations, managing active state, file system watching via Tauri IPC, and synchronization strategies.
- **Local Persistence & Data Models** — Foundational storage layer using an Active Record pattern over SQLite for workspace metadata and application settings.
- **Search & Indexing Service** — Provides high-performance full-text search for runbooks using an in-memory index updated reactively.

### System Execution Engine

Handles the low-level execution of shell commands and the rendering of terminal outputs. It manages PTY (Pseudo-Terminal) instances and streams execution logs back to the UI via a document bridge.

- **Terminal UI & Lifecycle Manager** — Manages the visual terminal interface and its React lifecycle.
- **PTY Execution & Stream Engine** — Acts as the core execution controller, managing the global registry of PTY instances.
- **Document Integration Bridge** — Facilitates the synchronization of execution data with the application's local-first data layer.

### AI Orchestrator

Encapsulates the logic for AI session management and event streaming. It provides a dedicated interface for developer productivity tools, managing conversation history and real-time AI output.

- **AI Session Orchestrator** — Acts as the central controller for the subsystem, managing the initialization of the AI environment and the reactive synchronization of session data.
- **AI Interaction UI** — Responsible for the presentation layer of the AI experience.

### Sync & Connectivity Layer

Manages the low-level networking and socket management required for real-time collaboration. It handles Phoenix channel connections and ensures local-first data is synchronized with the Atuin Hub.

- **Socket & Connection Manager** — Manages the physical WebSocket connection and its lifecycle.
- **Channel & Messaging Abstraction** — Provides a high-level abstraction over Phoenix Channels, converting the standard callback-driven messaging into a modern async/await pattern.

