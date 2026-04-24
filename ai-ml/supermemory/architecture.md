```mermaid
graph LR
  subgraph 1["External Ingestion Layer"]
    1__1_1["Browser Ingestion Engine"]
    1__1_2["MCP & Agent Interface"]
    1__1_3["Programmatic SDKs & Middleware"]
    1__1_4["Desktop & Multimodal Ingestion"]
    1__1_1 -->|"Uses shared middleware logic and Python SDK wrappers to standardize and transmit captured browser d…"| 1__1_3
    1__1_2 -->|"Utilizes the underlying agent framework tools and middleware to resolve memory queries and execute …"| 1__1_3
    1__1_4 -->|"Employs core SDK tools to facilitate memory capture and search operations from non-web interfaces l…"| 1__1_3
  end
  subgraph 2["Core Memory Platform"]
    2__2_1["Core Application & SDK Framework"]
    2__2_2["AI Chat & Interaction Interface"]
    2__2_3["Memory Content & Lifecycle Manager"]
    2__2_4["Knowledge Graph & Context Engine"]
    2__2_5["External Ingestion & Connectivity"]
    2__2_1 -->|"Provides the authentication context and global state necessary for maintaining persistent chat sess…"| 2__2_2
    2__2_1 -->|"Manages the routing and layout containers for document viewing, editing, and bulk management operat…"| 2__2_3
    2__2_2 -->|"Queries the knowledge graph and context provider to enrich AI responses with relevant semantic cont…"| 2__2_4
    2__2_2 -->|"Persists chat history and allows AI tools to create, modify, or summarize stored memories."| 2__2_3
    2__2_5 -->|"Feeds validated data from external sources into the document management pipeline for indexing and s…"| 2__2_3
    2__2_4 -->|"Maps graph nodes to specific document content and metadata, enabling detailed retrieval from the vi…"| 2__2_3
  end
  subgraph 3["Semantic Visualization Engine"]
    3__3_1["Graph Data & State Orchestrator"]
    3__3_2["Spatial Simulation Engine"]
    3__3_3["Interactive Viewport Controller"]
    3__3_4["Multi-Backend Rendering Layer"]
    3__3_1 -->|"Supplies prepared node and edge data to initialize or update the physics simulation."| 3__3_2
    3__3_3 -->|"Updates the ViewportState (zoom/pan) in response to user interaction events."| 3__3_2
    3__3_2 -->|"Provides calculated spatial coordinates and hit-test results for frame-by-frame rendering."| 3__3_4
    3__3_1 -->|"Passes visual metadata, such as theme colors and selection highlights, for node styling."| 3__3_4
    3__3_3 -->|"Triggers node selection or navigation changes based on user clicks and spatial hit-tests."| 3__3_1
    3__3_1 -->|"Commands the viewport to 'auto-fit' or center on a specific node when the data or selection changes."| 3__3_3
  end
  subgraph 4["AI Integration & Retrieval SDKs"]
    4__4_1["Python Core AI Middleware"]
    4__4_2["Python Real-time & Multimodal SDKs"]
    4__4_3["TypeScript AI SDK Middleware"]
    4__4_4["TypeScript Retrieval Engine & Specialized Tools"]
    4__4_3 -->|"delegates semantic search and query extraction tasks to"| 4__4_4
    4__4_1 -->|"provides foundational tool definitions and connection logic that are extended by"| 4__4_2
    4__4_4 -->|"returns formatted memory snippets and tool execution results to be injected into the message stream…"| 4__4_3
  end
  subgraph 5["Lifecycle & Migration Utilities"]
    5__5_1["Migration Engine"]
    5__5_2["Documentation Test Orchestrator"]
    5__5_3["SDK & Integration Validation Suite"]
    5__5_2 -->|"Discovers and spawns child processes to execute specific SDK and integration test cases across mult…"| 5__5_3
    5__5_1 -->|"Utilizes standardized SDK wrappers and validation logic to verify the integrity of imported data du…"| 5__5_3
    5__5_1 -->|"calls"| 5__5_2
  end
  1 -->|"Streams captured content, links, and metadata for indexing and storage."| 2
  4 -->|"Queries for semantically relevant context and submits new memories generated during AI conversation…"| 2
  2 -->|"Provides the graph topology (nodes and edges) and document metadata for spatial rendering."| 3
  5 -->|"Performs bulk data imports and validates API endpoint integrity during maintenance cycles."| 2
  2 -->|"Returns filtered memory chunks and context windows to be injected into LLM prompts."| 4
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

Supermemory operates as a centralized intelligence hub that transforms unstructured data from various sources into a structured, queryable semantic graph. The data flow begins at the External Ingestion Layer, where browser extensions and MCP servers capture user activity and external content. This data is streamed to the Core Memory Platform, which handles authentication, document processing (chunking/embedding), and persistence in a hybrid relational-vector store. The Semantic Visualization Engine consumes this structured data to render an interactive memory graph, allowing users to explore knowledge spatially. Simultaneously, the AI Integration & Retrieval SDKs act as a middleware layer for external LLMs, querying the Core Platform to inject relevant context into AI conversations (RAG) and capturing new insights back into the memory store.

### External Ingestion Layer

The primary entry point for data, responsible for capturing content directly from the user's workflow via browser extensions and providing a standardized interface for external AI clients through the Model Context Protocol (MCP).

- **Browser Ingestion Engine** — Manages the lifecycle of the browser extension, including background synchronization, authentication, and site-specific content scripts (ChatGPT, Claude, Twitter) that capture user interactions and data directly from the DOM.
- **MCP & Agent Interface** — Implements the Model Context Protocol (MCP) to expose Supermemory as a resource and toolset for external AI clients (e.g., Claude Desktop).
- **Programmatic SDKs & Middleware** — Provides a suite of wrappers and middleware for popular AI development frameworks (Vercel AI SDK, Mastra, VoltAgent).
- **Desktop & Multimodal Ingestion** — Extends ingestion capabilities to desktop environments via Raycast and voice-based interactions via Pipecat, allowing for quick memory capture and retrieval outside of traditional browser or code-based workflows.

### Core Memory Platform

The central processing and management hub. It hosts the Next.js web application, the Hono-based API, and the core logic for document management, user authentication, and the primary chat interface. It coordinates the transformation of raw data into indexed memories.

- **Core Application & SDK Framework** — The foundational layer of the platform, providing the Next.js application structure, authentication context, and programmatic SDK interfaces.
- **AI Chat & Interaction Interface** — Manages the conversational AI experience, including the chat sidebar, message streaming, and the execution of AI tools.
- **Memory Content & Lifecycle Manager** — Handles the storage, viewing, and editing of individual memories (documents, notes, links).
- **Knowledge Graph & Context Engine** — Orchestrates the semantic relationships between memories, providing a visual graph representation and a context provider for AI agents.
- **External Ingestion & Connectivity** — Manages connections to external data sources (Notion, Google Drive) and implements protocols like MCP (Model Context Protocol) to ingest data.

### Semantic Visualization Engine

A specialized rendering engine that visualizes the memory graph. It uses force-directed simulations and WebGL/Canvas to represent semantic relationships between documents and memories as an interactive spatial map.

- **Graph Data & State Orchestrator** — Manages the lifecycle of graph data and the high-level application state.
- **Spatial Simulation Engine** — The mathematical core of the engine, responsible for calculating node positions and managing the spatial environment.
- **Interactive Viewport Controller** — Handles user input and translates physical gestures (mouse wheel, touch, drag) into viewport transformations.
- **Multi-Backend Rendering Layer** — An abstraction layer for drawing the graph to the screen.

### AI Integration & Retrieval SDKs

A cross-language middleware layer (Python and TypeScript) that integrates Supermemory into AI agent frameworks. It provides tools for semantic retrieval, prompt enhancement, and automated memory creation during LLM interactions.

- **Python Core AI Middleware** — Provides the primary integration for standard text-based AI agents and LLM clients in Python, implementing a wrapper pattern to inject memories and manage memory stores.
- **Python Real-time & Multimodal SDKs** — Specialized for low-latency and streaming environments, adapting retrieval logic for voice and multimodal pipelines to allow real-time agents to access semantic memories.
- **TypeScript AI SDK Middleware** — Implements the middleware layer for the TypeScript ecosystem, targeting Vercel AI SDK and VoltAgent to transform message arrays and inject retrieved memories.
- **TypeScript Retrieval Engine & Specialized Tools** — The underlying engine for TypeScript integrations, managing direct communication with the Supermemory API and providing shared utilities for semantic profile searching.

### Lifecycle & Migration Utilities

Supporting scripts and tools for system maintenance, including data migration from legacy platforms (like Mem0) and automated testing of SDK responses and documentation.

- **Migration Engine** — Manages the end-to-end data migration lifecycle, handling the extraction of memories from legacy platforms, transforming them into Supermemory-compatible formats, and performing post-migration verification.
- **Documentation Test Orchestrator** — The infrastructure layer responsible for discovering test files across the monorepo, managing execution environments (Bun, Python venvs), and aggregating results from documentation-based tests.
- **SDK & Integration Validation Suite** — A comprehensive collection of automated tests that validate the Supermemory SDKs and their compatibility with external AI frameworks and tool-calling standards.

