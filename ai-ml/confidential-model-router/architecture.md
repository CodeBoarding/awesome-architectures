```mermaid
graph LR
  subgraph 1["Enclave Gateway"]
    1__1_1["Gateway Orchestrator"]
    1__1_2["Secure Proxy & Resilience Engine"]
    1__1_3["Operational Monitor & Content Processor"]
    1__1_4["Admin & Diagnostic Interface"]
    1__1_1 -->|"Provides discovered enclave endpoints, routing policies, and rate-limiting state to the proxy layer."| 1__1_2
    1__1_3 -->|"Reports real-time enclave health status and performance metrics used for management and scaling dec…"| 1__1_1
    1__1_3 -->|"Supplies health signals to trigger circuit breakers and provides pre-processed content (e.g., markd…"| 1__1_2
    1__1_4 -->|"Queries the current system state, model availability, and enclave status for administrative reporti…"| 1__1_1
    1__1_4 -->|"Injects trace IDs and diagnostic logging into the request flow to facilitate troubleshooting of the…"| 1__1_2
    1__1_1 -->|"calls"| 1__1_3
    1__1_2 -->|"calls"| 1__1_1
    1__1_2 -->|"calls"| 1__1_3
  end
  subgraph 2["Inference Protocol Runtime"]
    2__2_1["Protocol Orchestrator"]
    2__2_2["Streaming Data Plane"]
    2__2_3["Request & Tool Transformer"]
    2__2_4["Citation & Metadata Engine"]
    2__2_1 -->|"Requests prompt construction and tool definitions for the current execution context."| 2__2_3
    2__2_1 -->|"Triggers the execution of streaming loops and manages the lifecycle of upstream connections."| 2__2_2
    2__2_2 -->|"Delegates the parsing of raw stream fragments into structured tool calls."| 2__2_3
    2__2_2 -->|"Feeds text deltas for citation detection and metadata enrichment."| 2__2_4
    2__2_2 -->|"calls"| 2__2_1
    2__2_3 -->|"calls"| 2__2_2
    2__2_4 -->|"calls"| 2__2_2
  end
  subgraph 3["Tool Execution Engine"]
    3__3_1["Tool Loop Orchestrator"]
    3__3_2["Execution & Progress Manager"]
    3__3_3["Tool Invocation & Normalization"]
    3__3_4["Security & Sanitization"]
    3__3_5["Model Request Synthesis"]
    3__3_1 -->|"Sends raw tool call arguments for cleansing and security filtering before execution."| 3__3_4
    3__3_1 -->|"Initiates the tool execution flow and manages the lifecycle of progress updates."| 3__3_2
    3__3_2 -->|"Delegates the actual tool call and result normalization to the invocation layer."| 3__3_3
    3__3_1 -->|"Provides collected tool results to synthesize the final prompt for the inference engine."| 3__3_5
    3__3_1 -->|"calls"| 3__3_3
    3__3_3 -->|"calls"| 3__3_2
    3__3_3 -->|"calls"| 3__3_4
  end
  subgraph 4["Data Transformation Service"]
    4__4_1["Schema Coercion Engine"]
    4__4_2["Multi-modal Payload Transformer"]
    4__4_3["Runtime Policy Enforcer"]
    4__4_2 -->|"Transformed markdown content and rewritten payloads are passed to the coercion engine to ensure the…"| 4__4_1
    4__4_1 -->|"Once tool arguments are coerced into the correct types, they are passed to the policy enforcer to a…"| 4__4_3
  end
  subgraph 5["Observability & Attribution"]
    5__5_1["Usage Attribution & Billing"]
    5__5_2["Citation & Source Management"]
    5__5_3["Tool Execution & Security Monitoring"]
    5__5_4["Operational Health & Metrics"]
    5__5_3 -->|"Queries the current citation state to enrich progress markers with source URLs and titles during to…"| 5__5_2
    5__5_1 -->|"Exports normalized token usage statistics and billing event counts to the global Prometheus monitor…"| 5__5_4
    5__5_1 -->|"calls"| 5__5_2
    5__5_2 -->|"calls"| 5__5_1
    5__5_2 -->|"calls"| 5__5_3
    5__5_2 -->|"calls"| 5__5_4
    5__5_4 -->|"calls"| 5__5_2
  end
  1 -->|"Routes verified requests to the protocol handler."| 2
  2 -->|"Triggers tool loops when tool calls are detected in the stream."| 3
  3 -->|"Requests argument coercion and file processing for tool inputs."| 4
  2 -->|"Passes stream chunks for token counting and citation extraction."| 5
  3 -->|"Reports tool-related events and progress for billing and logging."| 5
  1 -->|"calls"| 4
  1 -->|"calls"| 5
  2 -->|"calls"| 1
  3 -->|"calls"| 2
  4 -->|"calls"| 1
  5 -->|"calls"| 2
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The confidential-model-router acts as a secure gateway for AI inference, ensuring data privacy through TEE-based enclaves. It manages stateful SSE streams, intercepts tool calls for local or remote execution via MCP, and provides robust observability for billing and citations.

### Enclave Gateway

Acts as the secure entry point, managing TEE-based backend enclaves, circuit breaking, and initial request proxying.

- **Gateway Orchestrator** — Manages the lifecycle of the gateway, including configuration loading, enclave discovery, and stateful tracking of quotas and billing.
- **Secure Proxy & Resilience Engine** — Handles the high-performance routing and proxying of requests to verified enclaves.
- **Operational Monitor & Content Processor** — Continuously evaluates enclave health (e.g., queue depth, latency) to inform routing decisions and performs specialized pre-processing, such as converting multipart file uploads into markdown for model consumption.
- **Admin & Diagnostic Interface** — Provides the external CLI for administrative tasks (e.g., listing models) and internal diagnostic utilities for tracing and debugging the tool runtime during request execution.

### Inference Protocol Runtime

The core state machine for handling streaming AI protocols (Chat and Responses), managing the SSE pump and upstream communication.

- **Protocol Orchestrator** — Acts as the high-level state machine and entry point for the runtime.
- **Streaming Data Plane** — The low-level I/O engine responsible for establishing SSE connections to upstream model enclaves.
- **Request & Tool Transformer** — A translation layer that converts generic API requests into model-specific prompts and tool definitions.
- **Citation & Metadata Engine** — A specialized stream processor that monitors text deltas for markdown links and citations.

### Tool Execution Engine

Orchestrates the "Tool Loop" by intercepting model requests, executing external tools (e.g., via MCP), and feeding results back into the inference stream.

- **Tool Loop Orchestrator** — Acts as the central state machine for the tool execution lifecycle.
- **Execution & Progress Manager** — Manages the active execution phase of tools and provides real-time feedback to the client.
- **Tool Invocation & Normalization** — Handles the low-level mechanics of calling external tools (like MCP servers) and normalizing their outputs.
- **Security & Sanitization** — A security-focused layer that cleanses data passing between the model and tools.
- **Model Request Synthesis** — Constructs the final payloads sent back to the inference engine.

### Data Transformation Service

Provides specialized utilities for coercing data types, processing file inputs into markdown, and sanitizing tool arguments.

- **Schema Coercion Engine** — Provides recursive type validation and coercion to ensure input data (primarily tool arguments) conforms to expected schemas.
- **Multi-modal Payload Transformer** — Intercepts chat completion requests to decode base64-encoded file attachments and render them into markdown.
- **Runtime Policy Enforcer** — Adjusts and sanitizes tool arguments based on runtime configurations and user tiers.

### Observability & Attribution

Monitors the inference flow to perform token counting for billing, manage citation states, and record security-related events.

- **Usage Attribution & Billing** — Responsible for the extraction, normalization, and reporting of token usage from both standard and streaming (SSE) inference responses.
- **Citation & Source Management** — Manages the state of external sources (e.g., web search results) retrieved during tool execution.
- **Tool Execution & Security Monitoring** — Monitors the execution of router-owned tools to emit progress updates and security-related event markers.
- **Operational Health & Metrics** — Provides system-level telemetry by polling backend enclaves for performance metrics (like queue depth) and updating Prometheus counters for request success rates, latencies, and circuit breaker states.

