```mermaid
graph LR
  subgraph 1["Agent Orchestrator"]
    1__1_1["Task Orchestrator"]
    1__1_2["LLM Gateway"]
    1__1_3["Browser Controller"]
    1__1_4["Flow Logger"]
    1__1_1 -->|"Delegates reasoning, planning, and tool selection"| 1__1_2
    1__1_1 -->|"Commands low-level browser interactions and requests semantic page snapshots"| 1__1_3
    1__1_1 -->|"Persists the agent's internal reasoning steps and execution history"| 1__1_4
    1__1_3 -->|"Supplies processed visual context and semantic DOM data"| 1__1_2
  end
  subgraph 2["Browser Automation Engine"]
    2__2_1["DOM Interaction & Resolution Engine"]
    2__2_2["Shadow DOM Runtime Environment"]
    2__2_3["Automation Script Build Infrastructure"]
    2__2_3 -->|"Provides the bundled IIFE scripts that are injected into the browser context for execution."| 2__2_1
    2__2_2 -->|"Exposes the StagehandV3Backdoor interface and patched DOM APIs, which the locator engine uses to re…"| 2__2_1
    2__2_1 -->|"Orchestrates the initialization of the browser context by triggering the installation of the shadow…"| 2__2_2
  end
  subgraph 3["Unified API Server"]
    3__3_1["V3 Session Engine"]
    3__3_2["V4 Persistent Engine"]
    3__3_3["Server Runtime Host"]
    3__3_4["API Contract & Documentation"]
    3__3_3 -->|"Bootstraps the in-memory session store and registers V3-specific request handlers."| 3__3_1
    3__3_3 -->|"Establishes the primary database connection and registers V4 Fastify controllers."| 3__3_2
    3__3_4 -->|"Introspects V3 Zod schemas and route definitions to generate OpenAPI specifications."| 3__3_1
    3__3_4 -->|"Introspects V4 controllers and database entity schemas for documentation synchronization."| 3__3_2
  end
  subgraph 4["CLI & Local Bridge"]
    4__4_1["Daemon Lifecycle Manager"]
    4__4_2["Browser Discovery Engine"]
    4__4_3["CDP Communication Bridge"]
    4__4_1 -->|"Triggers discovery to locate available browser targets during daemon initialization."| 4__4_2
    4__4_1 -->|"Orchestrates the setup and teardown of the transport channel for active sessions."| 4__4_3
    4__4_3 -->|"Utilizes validated WebSocket endpoints to establish the underlying CDP connection."| 4__4_2
  end
  subgraph 5["Evaluation Framework"]
    5__5_1["Evaluation Control Plane"]
    5__5_2["Agent Task Runtime"]
    5__5_3["Data Validation & Reporting"]
    5__5_1 -->|"Configures the execution environment and initiates specific benchmark tasks based on CLI arguments …"| 5__5_2
    5__5_2 -->|"Passes task execution results, captured screenshots, and extracted data for final verification and …"| 5__5_3
    5__5_1 -->|"Triggers the final aggregation of results into human-readable reports after all scheduled tasks hav…"| 5__5_3
    5__5_2 -->|"calls"| 5__5_1
  end
  1 -->|"Sends DOM commands and receives page state"| 2
  1 -->|"Synchronizes session state and metrics"| 3
  3 -->|"Orchestrates and dispatches agent instances"| 1
  4 -->|"Triggers agent workflows and manages lifecycle"| 1
  4 -->|"Establishes CDP connections for execution"| 2
  5 -->|"Executes agent tasks and monitors performance"| 1
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

Stagehand is an AI-driven web automation framework that decouples high-level reasoning (the "Brain") from low-level browser execution (the "Body"). The architecture is centered around the Agent Orchestrator, which manages the agent's lifecycle and translates user intent into executable actions using LLMs. These actions are carried out by the Browser Automation Engine, which abstracts browser control and DOM manipulation. The Unified API Server handles remote execution and persistence, while the CLI & Local Bridge supports local development, and the Evaluation Framework ensures reliability through automated benchmarking.

### Agent Orchestrator

The central intelligence of Stagehand. It manages the agent's lifecycle, processes high-level goals into executable actions (act, extract, observe) using LLMs, and orchestrates tool usage. It handles reasoning, planning, and self-correction while maintaining an observability log of the agent's "thought process."

- **Task Orchestrator** — Manages the high-level lifecycle of the agent, coordinating between user goals and executable actions.
- **LLM Gateway** — Abstracts and manages interactions with various LLM providers (OpenAI, Anthropic, Google).
- **Browser Controller** — Acts as the agent's "body" and "eyes," managing the low-level browser connection via CDP and providing semantic perception of the page.
- **Flow Logger** — Implements the observability layer of the subsystem, tracking the agent's internal state transitions and "thought process." It captures LLM requests, responses, and tool execution traces to provide a transparent audit trail of the agent's reasoning.

### Browser Automation Engine

The execution layer of the agent. It provides a unified interface to the browser, handling low-level DOM manipulation, script injection, and locator resolution. It includes specialized scripts for piercing shadow DOMs and interacting with complex web elements, as well as the build infrastructure for these injected scripts.

- **DOM Interaction & Resolution Engine** — The core execution logic that resolves element selectors and performs physical interactions.
- **Shadow DOM Runtime Environment** — A low-level patching layer that modifies the browser's internal DOM behavior.
- **Automation Script Build Infrastructure** — The development and build-time component responsible for compiling the engine's TypeScript logic into injectable browser scripts.

### Unified API Server

Manages remote execution, session persistence, and multi-version API support (V3 and V4). It provides REST/WebSocket interfaces for interacting with agents, handles database connections for long-term storage of agent steps, and manages LLM configurations across different providers.

- **V3 Session Engine** — Manages the lifecycle of V3 agent sessions using an in-memory store.
- **V4 Persistent Engine** — Provides a scalable, database-backed API for agent execution.
- **Server Runtime Host** — The infrastructure layer that bootstraps the API server.
- **API Contract & Documentation** — Manages the generation and synchronization of OpenAPI/Swagger documentation for the unified server.

### CLI & Local Bridge

Facilitates local development and interaction. It allows users to run Stagehand from the command line, discovers local browser instances via Chrome DevTools Protocol (CDP), and manages the local daemon for script-to-browser communication and cleanup.

- **Daemon Lifecycle Manager** — Orchestrates the background daemon process that acts as a persistent intermediary.
- **Browser Discovery Engine** — Responsible for identifying and validating local browser instances.
- **CDP Communication Bridge** — Manages the data transport layer between the CLI and the browser.

### Evaluation Framework

A dedicated framework for measuring and verifying agent performance. It runs standardized benchmarks (GAIA, Mind2Web, WebVoyager), scores agent actions using exact match and visual verification, and collects screenshots for debugging and quality assurance.

- **Evaluation Control Plane** — Manages the end-to-end evaluation lifecycle, including CLI interaction, benchmark suite construction, and framework self-testing.
- **Agent Task Runtime** — Executes the agentic workflow within the evaluation context.
- **Data Validation & Reporting** — Validates agent outputs against expected results using specialized data extraction verifiers (e.g., checking for specific entities or historical data).

