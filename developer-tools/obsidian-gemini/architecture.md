```mermaid
graph LR
  subgraph 1["Agent Core & Orchestration"]
    1__1_1["Agent Runtime & Task Orchestration"]
    1__1_2["Lifecycle & Plugin Management"]
    1__1_3["Intelligence & Context Engine"]
    1__1_4["Tooling & MCP Framework"]
    1__1_5["Agent Interface & Interaction"]
    1__1_6["Build & Maintenance Utilities"]
    1__1_2 -->|"Instantiates and manages the lifecycle of the agent loop and background services."| 1__1_1
    1__1_5 -->|"Dispatches user messages to the loop and subscribes to the event bus for real-time UI updates."| 1__1_1
    1__1_1 -->|"Requests model completions and retrieves context-aware prompt templates for each turn."| 1__1_3
    1__1_1 -->|"Delegates the execution of tool calls identified by the LLM to the execution engine."| 1__1_4
    1__1_3 -->|"Provides tool schemas and skill definitions to the LLM to enable function calling capabilities."| 1__1_4
    1__1_2 -->|"Registers the custom Agent View and commands within the Obsidian workspace."| 1__1_5
  end
  subgraph 2["Session & Context Engine"]
    2__2_1["Session & History Manager"]
    2__2_2["Prompt & Template Engine"]
    2__2_3["Session & Prompt UI Layer"]
    2__2_1 -->|"Retrieves active templates to format the conversation history and system instructions before sendin…"| 2__2_2
    2__2_3 -->|"Triggers session lifecycle events such as loading a historical chat, deleting a session, or updatin…"| 2__2_1
    2__2_3 -->|"Queries the list of available system and custom prompts to allow users to switch templates within t…"| 2__2_2
    2__2_1 -->|"Uses internal ContextManager logic to summarize conversation history when the token limit is approa…"| 2__2_1
  end
  subgraph 3["Knowledge Engine"]
    3__3_1["Vault Discovery & Analysis"]
    3__3_2["RAG Pipeline (Indexing & Storage)"]
    3__3_3["Semantic Search Interface"]
    3__3_4["RAG Lifecycle & UI"]
    3__3_1 -->|"Supplies the list of files and structural metadata required to prioritize and execute the indexing …"| 3__3_2
    3__3_2 -->|"Populates and updates the vector index that the search tool queries for relevant context."| 3__3_3
    3__3_4 -->|"Triggers indexing jobs, updates configuration parameters (like chunk size), and manages error recov…"| 3__3_2
    3__3_3 -->|"Utilizes vault structural data to refine search results and apply folder-based or tag-based filters."| 3__3_1
  end
  subgraph 4["Tool & MCP Integration"]
    4__4_1["Tool Execution & Local Skills"]
    4__4_2["MCP Integration Service"]
    4__4_3["Extensibility & Governance UI"]
    4__4_1 -->|"Routes external tool requests to the MCP manager for execution when the agent calls a non-local too…"| 4__4_2
    4__4_3 -->|"Configures server connection parameters, manages server lifecycle (start/stop), and handles environ…"| 4__4_2
    4__4_3 -->|"Controls tool availability and modifies execution parameters (like search depth or result limits) v…"| 4__4_1
  end
  subgraph 5["AI Gateway"]
    5__5_1["Model Registry & Configuration Service"]
    5__5_2["Client Factory"]
    5__5_3["Gemini API Client"]
    5__5_1 -->|"Supplies validated model identifiers and configuration parameters required to instantiate a functio…"| 5__5_2
    5__5_2 -->|"Instantiates and configures the specific client implementation based on the requested model and use…"| 5__5_3
  end
  subgraph 6["UI & Safety Layer"]
    6__6_1["Agent Interaction & Context Manager"]
    6__6_2["Safety Gateways"]
    6__6_3["Configuration & Specialized Inputs"]
    6__6_1 -->|"Triggers confirmation modals when the Agent Loop attempts to execute a tool marked as 'high-risk' o…"| 6__6_2
    6__6_3 -->|"Persists user preferences and API configurations that dictate the behavior, model selection, and av…"| 6__6_1
    6__6_1 -->|"Invokes specialized input modals (e.g., for image generation) to gather refined parameters from the…"| 6__6_3
  end
  6 -->|"Triggers the agentic loop and passes user messages/commands."| 1
  1 -->|"Retrieves conversation history and persists new interactions."| 2
  1 -->|"Sends assembled prompts and receives model reasoning or tool calls."| 5
  1 -->|"Dispatches tool execution requests based on LLM instructions."| 4
  4 -->|"Queries indexed vault data to provide context for RAG-enabled tools."| 3
  6 -->|"Intercepts tool execution for user approval via Trusted Mode modals."| 4
  2 -->|"Provides formatted system prompts and context window management logic."| 5
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The obsidian-gemini architecture is built around a central Agentic Loop that orchestrates interactions between the user's local Obsidian vault and the Google Gemini AI. The flow begins in the UI & Safety Layer, where user inputs are captured and routed to the Agent Core. The Core manages the lifecycle of an "Agent Loop," coordinating with the Session & Context Engine to assemble conversation history and system prompts. These are sent via the AI Gateway to the LLM. When the model returns tool calls, the Tool & MCP Integration executes the requested actions—often querying the Knowledge Engine for RAG-based vault data—while the Safety Gates ensure that sensitive operations (like file deletions) are intercepted for user approval before completion.

### Agent Core & Orchestration

The central engine of the plugin that manages the lifecycle of agent instances and background tasks. It coordinates the flow of data between the LLM, the user interface, and the tool execution environment.

- **Agent Runtime & Task Orchestration** — The primary execution engine that drives the agentic loop and manages asynchronous background operations.
- **Lifecycle & Plugin Management** — Handles the initialization of the plugin within Obsidian and the creation/persistence of agent instances and chat sessions.
- **Intelligence & Context Engine** — Manages the "brain" of the agent, including LLM communication, prompt templating, and the RAG (Retrieval-Augmented Generation) infrastructure that indexes the vault for semantic search.
- **Tooling & MCP Framework** — Provides the "hands" of the agent, allowing it to interact with the local vault, the web, and external services via the Model Context Protocol (MCP).
- **Agent Interface & Interaction** — Orchestrates the user-facing components, translating user messages into loop triggers and rendering the agent's streaming responses and tool outputs.
- **Build & Maintenance Utilities** — Supporting infrastructure for model updates, build processes, and documentation management that ensures the plugin remains up-to-date with the Gemini API.

### Session & Context Engine

Manages the persistence of chat sessions, conversation history, and the assembly of context. It uses templates to format system instructions and user prompts for the LLM.

- **Session & History Manager** — Manages the persistence, retrieval, and optimization of chat sessions.
- **Prompt & Template Engine** — Handles the discovery, parsing, and management of prompt templates.
- **Session & Prompt UI Layer** — Provides the user interface components for interacting with the session and prompt systems.

### Knowledge Engine

Provides Retrieval-Augmented Generation (RAG) capabilities by indexing the Obsidian vault and performing semantic searches to ground the AI's responses in local data.

- **Vault Discovery & Analysis** — Responsible for the structural and semantic mapping of the Obsidian vault.
- **RAG Pipeline (Indexing & Storage)** — The core "write" engine of the subsystem.
- **Semantic Search Interface** — The "read" interface that exposes RAG capabilities to the Agent Loop.
- **RAG Lifecycle & UI** — Manages the user-facing aspects of the Knowledge Engine, including configuration settings, indexing progress visualization, and manual maintenance tasks like index cleanup or resumption.

### Tool & MCP Integration

The extensibility layer that allows the agent to perform actions. It manages local "Skills" (like file CRUD) and external tools via the Model Context Protocol (MCP).

- **Tool Execution & Local Skills** — The core execution engine and the library of built-in capabilities.
- **MCP Integration Service** — The bridge to external tool providers via the Model Context Protocol (MCP).
- **Extensibility & Governance UI** — The user-facing management layer for tools and MCP servers.

### AI Gateway

The technical interface to the Google Gemini API. It handles model configuration, request/response parsing, and manages the available model list.

- **Model Registry & Configuration Service** — Manages the catalog of available Gemini models and ensures their operational parameters are valid.
- **Client Factory** — Implements the Factory pattern to abstract the creation of Gemini clients.
- **Gemini API Client** — The technical implementation of the Gemini API interface.

### UI & Safety Layer

The user-facing component of the plugin, including chat views and settings. It incorporates "Safety Gates" that require human-in-the-loop confirmation for high-risk agent actions.

- **Agent Interaction & Context Manager** — The core user interface for the plugin, responsible for rendering the chat view, managing session history, and visualizing the context (files, images, and mentions) that the agent is currently processing.
- **Safety Gateways** — Implements the "Human-in-the-loop" pattern by intercepting high-risk agent actions.
- **Configuration & Specialized Inputs** — Manages the administrative and task-specific UI elements.

