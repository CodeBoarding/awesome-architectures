```mermaid
graph LR
  subgraph 1["Core Kernel & LCEL"]
    1__1_1["Model & Message Abstractions"]
    1__1_2["Execution & Observability Engine"]
    1__1_3["Context & State Abstractions"]
    1__1_4["Tooling & Action Framework"]
    1__1_5["Integration & Compatibility Layer"]
    1__1_3 -->|"Supplies formatted BasePromptValue as the primary input for model generation."| 1__1_1
    1__1_1 -->|"Dispatches lifecycle events (e.g., handleLLMStart, handleLLMNewToken) to the CallbackManager during…"| 1__1_2
    1__1_4 -->|"Supplies tool schemas and validation logic for model-side function calling configuration."| 1__1_1
    1__1_1 -->|"Emits structured tool calls within AIMessage outputs for external execution."| 1__1_4
    1__1_2 -->|"Orchestrates the execution and monitoring of legacy chains and provider-specific adapters."| 1__1_5
  end
  subgraph 2["Orchestration & Execution"]
    2__2_1["Agentic Runtime"]
    2__2_2["Chain Execution Engine"]
    2__2_3["Tooling & Action Interface"]
    2__2_4["Context & Memory Management"]
    2__2_5["Retrieval & Data Infrastructure"]
    2__2_1 -->|"invokes tools and receives observations from"| 2__2_3
    2__2_1 -->|"reads and writes conversation history to"| 2__2_4
    2__2_1 -->|"encapsulates specialized chains for reasoning from"| 2__2_2
    2__2_2 -->|"fetches relevant context from"| 2__2_5
    2__2_2 -->|"persists intermediate states and outputs to"| 2__2_4
    2__2_4 -->|"utilizes retrievers for long-term history from"| 2__2_5
  end
  subgraph 3["Model Provider Adapters"]
    3__3_1["Google Core Adapter"]
    3__3_2["Google Specialized Services"]
    3__3_3["IBM Watsonx Adapter"]
    3__3_4["Mistral & Cohere Adapters"]
    3__3_5["OpenAI & Perplexity Adapters"]
    3__3_1 -->|"Provides foundational connection and auth context for media and embeddings."| 3__3_2
    3__3_1 -->|"Operates as a parallel, independent strategy implementing the same interface."| 3__3_3
  end
  subgraph 4["Retrieval & Data Pipeline"]
    4__4_1["Document Transformation"]
    4__4_2["Indexing & Record Management"]
    4__4_3["Vector Storage & Search"]
    4__4_4["Graph-Based Retrieval"]
    4__4_5["Retrieval Post-Processing"]
    4__4_1 -->|"Provides processed document chunks to the indexing logic for hashing and state tracking."| 4__4_2
    4__4_2 -->|"Commands the vector store to add, update, or delete documents based on the deduplication state."| 4__4_3
    4__4_3 -->|"Passes initial similarity search results to rerankers for relevance optimization."| 4__4_5
    4__4_4 -->|"Provides structured context or nodes to be refined or combined with vector results."| 4__4_5
    4__4_1 -->|"Supplies text segments for entity extraction and graph construction."| 4__4_4
  end
  subgraph 5["Tools & External Actions"]
    5__5_1["Structured Data & Database Tools"]
    5__5_2["Tavily Search & Research Integration"]
    5__5_3["Dall-E Image Generation Integration"]
    5__5_2 -->|"Parallel implementation of the core Tool interface"| 5__5_1
    5__5_2 -->|"Parallel implementation of the core Tool interface"| 5__5_3
    5__5_1 -->|"Parallel implementation of the core Tool interface"| 5__5_3
  end
  subgraph 6["Output Processing & Evaluation"]
    6__6_1["Structured Output Parsers"]
    6__6_2["Evaluation Strategies"]
    6__6_3["Evaluation Infrastructure"]
    6__6_1 -->|"Parsed structured data is passed to evaluators to verify schema compliance or accuracy."| 6__6_2
    6__6_2 -->|"Evaluator implementations are registered with the infrastructure to be invoked during dataset proce…"| 6__6_3
    6__6_3 -->|"The execution runner utilizes parsers to transform raw results into structured formats for evaluato…"| 6__6_1
  end
  2 -->|"Orchestrators use core interfaces and LCEL primitives to compose and execute logic."| 1
  2 -->|"Agents and Chains invoke standardized model interfaces to perform inference."| 3
  2 -->|"Orchestrators query retrievers to inject relevant context into prompts (RAG)."| 4
  2 -->|"Agents execute tools to perform side effects or fetch real-time data."| 5
  3 -->|"Raw responses from provider adapters are passed to parsers for structuring and validation."| 6
  4 -->|"Vector stores and retrievers implement the base interfaces defined in the core kernel."| 1
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

LangChain.js is an AI orchestration framework designed to build LLM-powered applications through a modular, interface-driven architecture. The system centers on the LangChain Expression Language (LCEL), which allows developers to compose complex chains of thought and action. Data flows from user inputs through orchestration layers (Chains and Agents), which leverage standardized adapters for various LLM providers and vector databases. The framework emphasizes "Composition over Inheritance," enabling seamless integration of external tools, document processing pipelines, and structured output parsing to transform raw model responses into actionable data.

### Core Kernel & LCEL

The foundational layer defining the abstract contracts and the declarative LangChain Expression Language (LCEL). It establishes how all components (Models, Prompts, Tools) interact via a unified interface.

- **Model & Message Abstractions** — Defines the core interfaces for LLMs and Chat Models, along with the schema for their outputs (Messages).
- **Execution & Observability Engine** — Manages the execution lifecycle of chains and runnables.
- **Context & State Abstractions** — Provides foundational abstractions for data inputs and persistence.
- **Tooling & Action Framework** — Establishes the contract for external tools and functions.
- **Integration & Compatibility Layer** — Bridges the core abstractions with specific third-party providers and maintains backward compatibility with legacy framework versions.

### Orchestration & Execution

The high-level engine responsible for managing the execution flow. It coordinates between agents that plan actions and chains that execute predefined sequences of LLM calls.

- **Agentic Runtime** — Responsible for the iterative "thought-action-observation" loop.
- **Chain Execution Engine** — Manages structured, sequential workflows where the output of one component serves as the input to the next.
- **Tooling & Action Interface** — Defines the interface for external capabilities (APIs, file systems, web search) that Agents can invoke.
- **Context & Memory Management** — Handles the persistence and retrieval of conversation history and execution state, allowing both Agents and Chains to maintain continuity across multiple interactions.
- **Retrieval & Data Infrastructure** — Provides the "Augmentation" in RAG (Retrieval-Augmented Generation).

### Model Provider Adapters

A collection of adapters that bridge the gap between LangChain's core interfaces and specific LLM provider APIs (OpenAI, Google, IBM, etc.), handling provider-specific authentication and message formatting.

- **Google Core Adapter** — Manages the primary lifecycle of Google-based model interactions (Gemini, Vertex AI), handling HTTP connection orchestration, GAuth-based authentication, and message transformation.
- **Google Specialized Services** — Extends the Google adapter suite with non-chat capabilities, including multimodal media management and vector/embedding services.
- **IBM Watsonx Adapter** — Dedicated adapter for the IBM Watsonx platform, handling gateway authentication, tool binding, and stream conversion.
- **Mistral & Cohere Adapters** — Provides integration for Mistral AI and Cohere models, mapping role-based messages and managing token usage metadata.
- **OpenAI & Perplexity Adapters** — Handles advanced response processing for OpenAI models and provides search-augmented chat for Perplexity AI.

### Retrieval & Data Pipeline

Manages the Retrieval Augmented Generation (RAG) lifecycle, including document ingestion, text splitting, embedding generation, and similarity search across various vector databases.

- **Document Transformation** — Responsible for the "Split" phase of the RAG pipeline.
- **Indexing & Record Management** — Acts as the stateful controller for the ingestion pipeline.
- **Vector Storage & Search** — Provides a unified interface for interacting with various vector databases and implements similarity search algorithms.
- **Graph-Based Retrieval** — An alternative storage and retrieval paradigm that focuses on structured relationships between entities.
- **Retrieval Post-Processing** — Enhances the quality of retrieved information after the initial search using rerankers and compressors.

### Tools & External Actions

Concrete implementations of tools that allow AI agents to interact with external systems, such as SQL databases, web search engines, and image generation APIs.

- **Structured Data & Database Tools** — Provides tools for agents to interact with structured data sources like SQL databases and JSON objects.
- **Tavily Search & Research Integration** — Encapsulates the integration with the Tavily API to provide advanced web search and AI-driven research capabilities.
- **Dall-E Image Generation Integration** — Facilitates creative multimedia tasks by wrapping OpenAI's Dall-E API.

### Output Processing & Evaluation

Responsible for transforming raw LLM string outputs into structured data (JSON/Zod) and providing utilities to evaluate the quality and accuracy of model responses.

- **Structured Output Parsers** — Transforms raw LLM responses into structured data formats, handling generic text-to-JSON conversion and model-specific tool calling.
- **Evaluation Strategies** — Defines the logic and interfaces for assessing model performance, including semantic string comparisons, pairwise ranking, and trajectory evaluation.
- **Evaluation Infrastructure** — Orchestrates the execution of evaluations across datasets, managing the lifecycle of runs and applying evaluation strategies.

