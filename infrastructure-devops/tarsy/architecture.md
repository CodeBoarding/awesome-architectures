```mermaid
graph LR
  subgraph 1["Core Orchestrator"]
    1__1_1["Core Orchestration Engine"]
    1__1_2["Persistence & State Management"]
    1__1_3["LLM Intelligence Gateway"]
    1__1_4["Configuration & Contextualizer"]
    1__1_1 -->|"Synchronizes session state, execution status, and audit logs to the database."| 1__1_2
    1__1_1 -->|"Dispatches agent tasks for reasoning, tool selection, and response generation via gRPC."| 1__1_3
    1__1_1 -->|"Resolves agent configurations and requests formatted context for prompt construction."| 1__1_4
    1__1_4 -->|"Provides structured tool definitions and formatted system prompts required for model inference."| 1__1_3
    1__1_2 -->|"Provides historical context and session state required for resuming or analyzing ongoing executions."| 1__1_1
  end
  subgraph 2["Persistence Layer"]
    2__2_1["Session Lifecycle Manager"]
    2__2_2["Agent Trace & Interaction Logger"]
    2__2_3["Cross-Session Memory Store"]
    2__2_4["Performance & Audit Store"]
    2__2_1 -->|"Provides the execution context (SessionID/ExecutionID) required to categorize and link granular logs"| 2__2_2
    2__2_1 -->|"Defines the investigation stages and sessions that are the subjects of performance scoring"| 2__2_4
    2__2_2 -->|"Supplies the raw interaction history used by the Reflector to synthesize new long-term memories"| 2__2_3
    2__2_3 -->|"Injects historical insights and 'memories' into active sessions based on alert similarity"| 2__2_1
  end
  subgraph 3["LLM Gateway"]
    3__3_1["Service Infrastructure & Routing"]
    3__3_2["Google Native Engine"]
    3__3_3["LangChain Multi-Provider Engine"]
    3__3_1 -->|"Routes requests to the native Google SDK when Gemini models are specified in the configuration."| 3__3_2
    3__3_1 -->|"Delegates generation tasks to the LangChain abstraction for Anthropic, OpenAI, and other non-native…"| 3__3_3
    3__3_2 -->|"calls"| 3__3_3
    3__3_3 -->|"calls"| 3__3_2
  end
  subgraph 4["SRE Dashboard"]
    4__4_1["Application Core & Real-time Engine"]
    4__4_2["Incident Triage & Alert Management"]
    4__4_3["Session Timeline & Content Engine"]
    4__4_4["Trace Analysis & MCP Configuration"]
    4__4_1 -->|"Streams processed events and state updates for real-time visualization of agent reasoning."| 4__4_3
    4__4_2 -->|"Routes the user to specific session views based on selected incidents or newly created alerts."| 4__4_3
    4__4_2 -->|"Passes tool selection and server configurations to the manual alert trigger flow."| 4__4_4
    4__4_3 -->|"Provides navigation links to deep-dive trace views for specific agent steps to facilitate debugging."| 4__4_4
  end
  4 -->|"Sends user commands and receives real-time execution traces via WebSockets"| 1
  1 -->|"Stores session metadata, agent execution history, and vector-based memories"| 2
  1 -->|"Dispatches reasoning tasks and tool-calling requests via gRPC"| 3
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

Tarsy is an agentic SRE platform designed to automate incident analysis and remediation. The system's workflow is centered around "Sessions," which are triggered by alerts or user requests from the SRE Dashboard. The Core Orchestrator (Go) manages these sessions by executing a chain of stages, each handled by specialized agents. These agents leverage the LLM Gateway (Python) for reasoning and tool-calling, while the Persistence Layer (Ent/Postgres) maintains the state of the analysis, logs agent interactions, and stores long-term memories for cross-session learning. The Orchestrator also integrates with external diagnostic and remediation tools via the Model Context Protocol (MCP). Real-time execution traces and agent "thinking" steps are streamed back to the dashboard via WebSockets, providing SREs with a transparent and interactive remediation experience.

### Core Orchestrator

The central Go-based engine that manages the lifecycle of incident analysis sessions. It handles API requests, manages a worker pool for parallel agent execution, and orchestrates complex workflows using the Model Context Protocol (MCP).

- **Core Orchestration Engine** — The primary execution engine that manages session lifecycles, worker allocation, and agent instantiation.
- **Persistence & State Management** — Manages the system's durable state using Ent ORM.
- **LLM Intelligence Gateway** — A gRPC-based bridge to the Python LLM service.
- **Configuration & Contextualizer** — Manages YAML-based agent definitions and formats execution context into structured prompts for the LLM Gateway.

### Persistence Layer

Manages the system's state and long-term memory using the Ent ORM and PostgreSQL. It stores alert sessions, agent execution logs, timeline events, and vector-based memories used for cross-session learning.

- **Session Lifecycle Manager** — Manages the structural "skeleton" of the system's state.
- **Agent Trace & Interaction Logger** — Acts as the "black box" recorder for the agentic workflow.
- **Cross-Session Memory Store** — Implements the "Reflector" system's storage layer.
- **Performance & Audit Store** — Manages the persistence of quality metrics and automated evaluation results.

### LLM Gateway

A Python-based microservice that abstracts interactions with various Large Language Models (Google Gemini, Anthropic, OpenAI). It provides a unified gRPC interface for the Go orchestrator, handling prompt construction and streaming responses.

- **Service Infrastructure & Routing** — Manages the gRPC server lifecycle and the central routing logic.
- **Google Native Engine** — A specialized provider that interacts directly with the Google Generative AI SDK.
- **LangChain Multi-Provider Engine** — Provides a unified interface for Anthropic, OpenAI, and other LLM backends using the LangChain framework.

### SRE Dashboard

A React-based frontend that provides SREs with a real-time view of incident analysis. It visualizes agent reasoning steps, tool executions, and final remediation summaries, allowing users to interact with the system via a chat interface.

- **Application Core & Real-time Engine** — Manages the React application lifecycle, authentication, and the critical WebSocket-driven event pipeline.
- **Incident Triage & Alert Management** — Provides the primary interface for SREs to monitor incoming incidents.
- **Session Timeline & Content Engine** — The central visualization component that transforms flat event streams into a hierarchical view of agent stages and tool executions.
- **Trace Analysis & MCP Configuration** — Facilitates advanced debugging and system setup.

