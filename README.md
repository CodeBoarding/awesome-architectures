# Awesome Architecture MDs

> Architecture diagrams for popular open-source repos. Auto-generated, markdown, drop-in-ready for your coding agent.

```mermaid
graph LR
  subgraph 1["Orchestration & Lifecycle"]
    1__1_1["CLI & Execution Orchestrator"]
    1__1_2["Environment & Tooling Manager"]
    1__1_3["Project Discovery & Context Builder"]
    1__1_4["Agentic Analysis Pipeline"]
    1__1_5["System Registry & Persistence"]
  end
  subgraph 2["Static Analysis Core"]
    2__2_1["Analysis Orchestrator & Cache Manager"]
    2__2_2["LSP Client & Language Adapters"]
    2__2_3["Semantic Graph Engine"]
    2__2_4["Architectural Clustering & Validation"]
  end
  subgraph 3["Change Analysis"]
    3__3_1["Change Detection & Context Manager"]
    3__3_2["Incremental State Orchestrator"]
    3__3_3["Analysis Serialization Layer"]
  end
  subgraph 4["AI Reasoning Layer"]
    4__4_1["Agentic Orchestration & Execution"]
    4__4_2["Structural Analysis & Health Engine"]
    4__4_3["Prompt Factory & Provider Abstraction"]
    4__4_4["Context Extraction & Persistence"]
  end
  subgraph 5["Health & Documentation"]
    5__5_1["Health Metrics Evaluator"]
    5__5_2["Documentation & Visualization Generator"]
    5__5_3["Unified Data Serializer"]
    5__5_4["Structural Analysis Engine"]
    5__5_5["Incremental Update Manager"]
    5__5_6["CLI & Repository Interface"]
  end
  subgraph 6["Persistence & Tooling"]
    6__6_1["Local Persistence Engine"]
    6__6_2["Repository Interaction Toolkit"]
    6__6_3["Execution Monitoring & Telemetry"]
  end
  1 -->|"Triggers change detection to determine the scope of the current run"| 3
  1 -->|"Initiates the full project scan and graph construction"| 2
  3 -->|"Provides diff context to enable partial updates of the call graph"| 2
  2 -->|"Provides structural graph data for semantic interpretation"| 4
  4 -->|"Uses the toolkit to read specific source code files for deep analysis"| 6
  2 -->|"Provides the call graph for metric calculation and diagram generation"| 5
  4 -->|"Provides semantic descriptions and component purposes for the final reports"| 5
  6 -->|"Provides access to cached analysis data and the local database"| 2
  1 -->|"calls"| 4
  1 -->|"calls"| 5
  1 -->|"calls"| 6
  2 -->|"calls"| 1
  2 -->|"calls"| 3
  3 -->|"calls"| 1
  3 -->|"calls"| 4
  4 -->|"calls"| 1
  4 -->|"calls"| 2
  5 -->|"calls"| 2
  5 -->|"calls"| 4
  6 -->|"calls"| 1
  3__3_1 -->|"Provides the `ChangeSet` and method-level diffs along with the cached `StaticAnalysisResults` from previous runs to initiate the delta computation."| 3__3_2
  3__3_2 -->|"Supplies the updated and validated `AnalysisInsights` to be transformed into structured LLM prompts and response models."| 3__3_3
  3__3_2 -->|"calls"| 3__3_1
  4__4_1 -->|"Requests formatted system and user messages tailored to the active LLM provider."| 4__4_3
  4__4_1 -->|"Invokes repository tools to ground LLM reasoning in actual source code and metadata."| 4__4_4
  4__4_1 -->|"Consumes code clusters and health insights to provide high-level architectural summaries."| 4__4_2
  4__4_2 -->|"Reads raw static analysis data and persists graph-based clustering results for future incremental runs."| 4__4_4
  4__4_2 -->|"calls"| 4__4_1
  4__4_4 -->|"calls"| 4__4_2
  6__6_3 -->|"Persists aggregated run statistics, token usage, and job status updates to the DuckDB/SQLite backend"| 6__6_1
  6__6_2 -->|"Queries the cache using file content hashes to determine if previous analysis results can be reused"| 6__6_1
  6__6_3 -->|"Instruments tool execution to track latency and frequency of filesystem interactions during an analysis run"| 6__6_2
  2__2_1 -->|"Orchestrates the startup and shutdown of language servers required for the current project"| 2__2_2
  2__2_1 -->|"Triggers the graph construction process and provides cached symbol data to minimize redundant LSP queries"| 2__2_3
  2__2_2 -->|"Supplies raw symbol locations and reference batches used to build graph edges"| 2__2_3
  2__2_3 -->|"Provides the completed call graph and hierarchy as input for community detection and logical grouping"| 2__2_4
  2__2_4 -->|"Returns the final clustered results and change metrics to be persisted in the analysis cache"| 2__2_1
  2__2_1 -->|"calls"| 2__2_4
  2__2_2 -->|"calls"| 2__2_1
  2__2_3 -->|"calls"| 2__2_2
  5__5_6 -->|"triggers"| 5__5_5
  5__5_5 -->|"coordinates with"| 5__5_4
  5__5_4 -->|"provides component boundaries to"| 5__5_1
  5__5_1 -->|"sends findings to"| 5__5_3
  5__5_4 -->|"feeds final architectural map into"| 5__5_3
  5__5_3 -->|"provides structured JSON to"| 5__5_2
  5__5_1 -->|"calls"| 5__5_4
  5__5_1 -->|"calls"| 5__5_5
  5__5_2 -->|"calls"| 5__5_3
  5__5_2 -->|"calls"| 5__5_6
  5__5_3 -->|"calls"| 5__5_4
  5__5_3 -->|"calls"| 5__5_5
  5__5_4 -->|"calls"| 5__5_5
  5__5_5 -->|"calls"| 5__5_3
  5__5_6 -->|"calls"| 5__5_2
  1__1_1 -->|"Verifies and prepares the local environment (LSP servers, Node.js) before any analysis begins."| 1__1_2
  1__1_1 -->|"Initiates the repository scanning process to identify the codebase structure and languages."| 1__1_3
  1__1_1 -->|"Triggers the high-level analysis workflow once the environment and project context are established."| 1__1_4
  1__1_3 -->|"Provides the structured project context and file-to-language mappings required for agentic reasoning."| 1__1_4
  1__1_4 -->|"Persists analysis results and retrieves cached signatures to support incremental analysis and reduce LLM token usage."| 1__1_5
  1__1_1 -->|"Uses the registry to dynamically load available tools and plugins during initialization."| 1__1_5
  1__1_3 -->|"calls"| 1__1_1
  1__1_3 -->|"calls"| 1__1_2
  1__1_3 -->|"calls"| 1__1_5
  1__1_4 -->|"calls"| 1__1_1
  1__1_4 -->|"calls"| 1__1_3
  1__1_5 -->|"calls"| 1__1_3
```
*Example: simplified view of a typical RAG stack. Real diagrams are generated from actual source, not drawn.*

![repos](https://img.shields.io/badge/repos-50-blue) ![languages](https://img.shields.io/badge/languages-8-green) ![updated](https://img.shields.io/badge/updated-weekly-brightgreen) ![license](https://img.shields.io/badge/license-MIT-lightgrey)

---

## Why

- **Onboard your AI agent.** Paste the markdown into your ARCHITECTURE.md so the agent onboards in fewer tokens.
- **Live mindmap as your agent codes.** Human readable to understand the changes your agent does.
- **Pattern literacy.** *"How do mature async runtimes structure their scheduler?"* Browse five of them side-by-side.

## Drop into your agent

```bash
# Cursor / Claude Code / Aider — load a repo's architecture as context
curl -sL https://raw.githubusercontent.com/<org>/awesome-architecture-mds/main/vllm/architecture.md \
  | pbcopy
```

Or reference it directly in your prompt:
```
@https://github.com/codeboarding/awesome-architecture-mds/blob/main/vllm/on_boarding.md
Using the architecture above, implement X without breaking module boundaries.
```

## Browse the atlas

All 1,036 repos with an `on_boarding.md`, grouped by what they do. Alphabetical within each group. Each link opens the top-level architecture diagram.

### Contents

- [AI & machine learning](#ai--machine-learning)
    - [LLM serving & inference](#llm-serving--inference)
    - [Agent frameworks & orchestration](#agent-frameworks--orchestration)
    - [AI coding tools](#ai-coding-tools)
    - [ML research & models](#ml-research--models)
    - [Training, evaluation & guardrails](#training-evaluation--guardrails)
- [Data & analytics](#data--analytics)
    - [ETL & workflow orchestration](#etl--workflow-orchestration)
    - [Databases & storage](#databases--storage)
    - [Data processing & analysis](#data-processing--analysis)
- [Web & UI](#web--ui)
    - [Frontend frameworks](#frontend-frameworks)
    - [UI libraries & no-code](#ui-libraries--no-code)
    - [Apps & platforms](#apps--platforms)
- [Infrastructure & DevOps](#infrastructure--devops)
    - [Configuration & automation](#configuration--automation)
    - [Observability & telemetry](#observability--telemetry)
    - [Media & real-time infra](#media--real-time-infra)
    - [Platform SDKs](#platform-sdks)
- [Developer tools](#developer-tools)
    - [Package & environment management](#package--environment-management)
    - [Language tooling (lint / types / format)](#language-tooling-lint--types--format)
    - [CLIs, docs & DX](#clis-docs--dx)
    - [Testing & load](#testing--load)
- [Scientific & research computing](#scientific--research-computing)
    - [Genomics & bioinformatics](#genomics--bioinformatics)
    - [Imaging, neuroscience & health](#imaging-neuroscience--health)
    - [Molecular dynamics & chemistry](#molecular-dynamics--chemistry)
- [Security & privacy](#security--privacy)
    - [App & supply-chain security](#app--supply-chain-security)
    - [Offensive / red team](#offensive--red-team)
- [Games, graphics & media](#games-graphics--media)
    - [Game engines & 3D](#game-engines--3d)
    - [Video, audio & downloaders](#video-audio--downloaders)
    - [Creative tooling](#creative-tooling)
- [Networking, APIs & protocols](#networking-apis--protocols)
    - [Platform SDKs & API clients](#platform-sdks--api-clients)
    - [Industrial & IoT protocols](#industrial--iot-protocols)
- [Learning codebases](#learning-codebases)
- [Uncategorized](#uncategorized)
- [Full index (A–Z)](./INDEX.md)

### AI & machine learning

#### LLM serving & inference

- [bella-openapi](./bella-openapi/on_boarding.md) - AI gateway routing and orchestrating requests to multiple large language models. _(Java)_
- [BitNet](./BitNet/on_boarding.md) - Efficient 1-bit LLM inference runtime with Python orchestration and C++/CUDA kernels. _(Python)_
- [FastChat](./FastChat/on_boarding.md) - Distributed platform for serving and evaluating chat-based large language models. _(Python)_
- [gpt4free](./gpt4free/on_boarding.md) - Proxy client library routing requests across free LLM providers. _(Python)_
- [koila](./koila/on_boarding.md) - PyTorch wrapper providing lazy evaluation to prevent GPU out-of-memory errors. _(Python)_
- [lightning-thunder](./lightning-thunder/on_boarding.md) - Source-to-source compiler for optimizing PyTorch model execution. _(Python)_
- [litellm](./litellm/on_boarding.md) - Unified LLM client and proxy supporting 100+ providers via OpenAI format. _(Python)_
- [mlc-llm](./mlc-llm/on_boarding.md) - Universal LLM compilation and deployment across hardware and platforms. _(Python)_
- [mlx-lm](./mlx-lm/on_boarding.md) - Apple MLX framework toolkit for running and fine-tuning language models. _(Python)_
- [mlx-vlm](./mlx-vlm/on_boarding.md) - Apple MLX toolkit for serving and interacting with vision-language models. _(Python)_
- [ollama-python](./ollama-python/on_boarding.md) - Official Python client library for the Ollama local LLM runtime API. _(Python)_
- [openai-python](./openai-python/on_boarding.md) - Official Python client library for the OpenAI API and models. _(Python)_
- [tinygrad](./tinygrad/on_boarding.md) - Minimalist deep learning framework between PyTorch and karpathy's micrograd. _(Python)_
- [transformer-deploy](./transformer-deploy/on_boarding.md) - Efficient transformer model deployment on ONNX Runtime TensorRT and Triton. _(Python)_
- [tvm](./tvm/on_boarding.md) - Apache TVM compiler stack for deploying deep learning models across hardware. _(Python)_
- [vllm](./vllm/on_boarding.md) - High-throughput memory-efficient inference and serving engine for LLMs. _(Python)_

#### Agent frameworks & orchestration

- [ABCs-of-control](./ABCs-of-control/on_boarding.md) - Conversational agent that parses queries, calls LLMs, and optionally invokes external tools. _(Python)_
- [AdalFlow](./AdalFlow/on_boarding.md) - Framework for building, training, and evaluating LLM-powered applications and pipelines. _(Python)_
- [ag2](./ag2/on_boarding.md) - Multi-agent LLM orchestration framework derived from AutoGen with tool and code execution. _(Python)_
- [agno](./agno/on_boarding.md) - Lightweight framework for building multimodal AI agents with memory and tool use. _(Python)_
- [arcade-ai](./arcade-ai/on_boarding.md) - Platform for developing and serving authenticated tools for AI agents. _(Python)_
- [Archon](./Archon/on_boarding.md) - Agent orchestration system that builds and refines other AI agents automatically. _(Python)_
- [AutoAgent](./AutoAgent/on_boarding.md) - Fully autonomous LLM agent framework with CLI, REPL, and tool management. _(Python)_
- [autogen](./autogen/on_boarding.md) - Microsoft framework for orchestrating multi-agent LLM conversations and task automation. _(Python)_
- [Bard](./Bard/on_boarding.md) - Conversational AI client for interacting with Google Bard language model. _(Python)_
- [browser-use](./browser-use/on_boarding.md) - AI agent framework giving LLMs control of a web browser for automation. _(Python)_
- [ChatGPT](./ChatGPT/on_boarding.md) - Unofficial CLI and API wrappers for interacting with ChatGPT conversational models. _(Python)_
- [ChatterBot](./ChatterBot/on_boarding.md) - Machine learning conversational bot engine with pluggable storage and logic adapters. _(Python)_
- [cognee](./cognee/on_boarding.md) - Memory and knowledge-graph layer for AI agents with ingestion and retrieval APIs. _(Python)_
- [composio](./composio/on_boarding.md) - Platform giving AI agents authenticated access to hundreds of external tools. _(Python)_
- [contextgem](./contextgem/on_boarding.md) - LLM-powered framework for structured information extraction from documents. _(Python)_
- [crawl4ai](./crawl4ai/on_boarding.md) - LLM-friendly web crawler producing clean markdown and structured data for RAG. _(Python)_
- [crewAI](./crewAI/on_boarding.md) - Framework for orchestrating role-playing autonomous AI agent crews. _(Python)_
- [dataproduct-mcp](./dataproduct-mcp/on_boarding.md) - MCP server exposing data products to LLMs with governance and guardrails. _(Python)_
- [dspy](./dspy/on_boarding.md) - Framework for programming with LLMs via modular signatures and automatic prompt optimization. _(Python)_
- [Flowise](./Flowise/on_boarding.md) - Drag-and-drop UI for building customized LLM flows and agent pipelines. _(TypeScript)_
- [genai-processors](./genai-processors/on_boarding.md) - Asynchronous pipeline library for building generative AI data processing workflows. _(Python)_
- [gpt-researcher](./gpt-researcher/on_boarding.md) - Autonomous agent that conducts comprehensive research with LLMs and citations. _(Python)_
- [graphrag](./graphrag/on_boarding.md) - Microsoft knowledge-graph-enhanced retrieval-augmented generation pipeline. _(Python)_
- [haystack](./haystack/on_boarding.md) - Modular framework for building LLM-powered search and RAG applications. _(Python)_
- [instructor](./instructor/on_boarding.md) - Library for extracting structured Pydantic outputs from large language models. _(Python)_
- [kor](./kor/on_boarding.md) - Schema-driven LLM library for structured information extraction. _(Python)_
- [kotaemon](./kotaemon/on_boarding.md) - Open-source clean UI RAG chatbot for document question answering. _(Python)_
- [langchain](./langchain/on_boarding.md) - Framework for building applications powered by language model chains and agents. _(Python)_
- [langextract](./langextract/on_boarding.md) - LLM-agnostic structured information extraction pipeline library. _(Python)_
- [langflow](./langflow/on_boarding.md) - Visual low-code UI for experimenting with LangChain workflows. _(Python)_
- [langgraph](./langgraph/on_boarding.md) - Library for building stateful, multi-actor LLM agent applications as graphs. _(Python)_
- [llama_index](./llama_index/on_boarding.md) - Data framework for indexing and querying data with LLMs for RAG. _(Python)_
- [llm-graph-builder](./llm-graph-builder/on_boarding.md) - LLM-powered pipeline that builds Neo4j knowledge graphs from unstructured data. _(Python)_
- [lmql](./lmql/on_boarding.md) - Query language for large language models with constrained generation. _(Python)_
- [MaiBot](./MaiBot/on_boarding.md) - Modular AI conversational agent with pluggable NLP and communication adapters. _(Python)_
- [mcp-agent](./mcp-agent/on_boarding.md) - Framework for building AI agents with MCP integration and workflow patterns. _(Python)_
- [mcp-agent-discussion](./mcp-agent-discussion/on_boarding.md) - Multi-agent system orchestrating complex AI workflows with MCP integration. _(Python)_
- [mcp-context-forge](./mcp-context-forge/on_boarding.md) - API gateway for managing MCP servers, tools, and resources across protocols. _(Python)_
- [mcp-use](./mcp-use/on_boarding.md) - Library for building LLM agents that use MCP tools and servers. _(Python)_
- [mem0](./mem0/on_boarding.md) - Memory layer for AI agents integrating LLMs, embeddings, and vector stores. _(Python)_
- [MetaGPT](./MetaGPT/on_boarding.md) - Multi-agent framework assigning software roles to collaborative LLM agents. _(Python)_
- [mongodb-mcp-server](./mongodb-mcp-server/on_boarding.md) - MCP server exposing MongoDB operations as tools for LLM agents. _(TypeScript)_
- [Open-Assistant](./Open-Assistant/on_boarding.md) - Open-source conversational AI assistant with human feedback training pipeline. _(Python)_
- [openai-agents-python](./openai-agents-python/on_boarding.md) - OpenAI's lightweight SDK for building multi-agent workflows with tools and handoffs. _(Python)_
- [OpenCopilot-PikoAi](./OpenCopilot-PikoAi/on_boarding.md) - Terminal-based AI copilot CLI for task automation via natural language. _(Python)_
- [openr](./openr/on_boarding.md) - LLM reasoning framework combining reinforcement learning and process reward models. _(Python)_
- [OS-Copilot](./OS-Copilot/on_boarding.md) - Self-improving AI agent framework for autonomous OS task execution. _(Python)_
- [paper-search-mcp](./paper-search-mcp/on_boarding.md) - MCP server aggregating academic paper search across multiple research databases. _(Python)_
- [pipecat](./pipecat/on_boarding.md) - Open-source framework for building voice and multimodal conversational AI agents. _(Python)_
- [podcastfy](./podcastfy/on_boarding.md) - Converts content into AI-generated multilingual conversational podcasts. _(Python)_
- [poml](./poml/on_boarding.md) - Prompt-oriented markup language engine for structured LLM prompt authoring. _(Python)_
- [pywit](./pywit/on_boarding.md) - Python SDK for the Wit.ai natural language understanding service. _(Python)_
- [quivr](./quivr/on_boarding.md) - Retrieval-augmented generation framework for building second brain chatbots. _(Python)_
- [ragbits](./ragbits/on_boarding.md) - Framework for building and evaluating retrieval-augmented generation systems. _(Python)_
- [redis-vl-python](./redis-vl-python/on_boarding.md) - Redis vector library for building LLM-powered semantic search and RAG applications. _(Python)_
- [sample-app-aoai-chatGPT](./sample-app-aoai-chatGPT/on_boarding.md) - Microsoft sample chat app integrating Azure OpenAI with enterprise data sources. _(Python)_
- [Scrapegraph-ai](./Scrapegraph-ai/on_boarding.md) - LLM-powered web scraping library generating extraction pipelines from prompts. _(Python)_
- [SuperAGI](./SuperAGI/on_boarding.md) - Open-source autonomous AI agent framework for building and deploying agents. _(Python)_
- [symbolicai](./symbolicai/on_boarding.md) - Neuro-symbolic framework combining LLMs with symbolic reasoning operations. _(Python)_
- [thinkgpt](./thinkgpt/on_boarding.md) - LLM orchestrator adding memory long-term context and reasoning capabilities. _(Python)_
- [trt-llm-rag-linux](./trt-llm-rag-linux/on_boarding.md) - Linux reference RAG application using NVIDIA TensorRT-LLM for inference. _(Python)_
- [txtai](./txtai/on_boarding.md) - All-in-one embeddings database for semantic search and LLM workflows. _(Python)_
- [whatsapp-chatgpt](./whatsapp-chatgpt/on_boarding.md) - ChatGPT-powered WhatsApp bot integration. _(?)_

#### AI coding tools

- [aideml](./aideml/on_boarding.md) - Autonomous ML engineer that iteratively writes and improves data science code. _(Python)_
- [auto-code-rover](./auto-code-rover/on_boarding.md) - Autonomous program-repair agent that navigates repos and patches buggy code. _(Python)_
- [AutoGPT](./AutoGPT/on_boarding.md) - Autonomous GPT-powered agent platform for chaining goals into executable tasks. _(Python)_
- [cocode](./cocode/on_boarding.md) - CLI tool combining code analysis with AI for summarization and vulnerability detection. _(Python)_
- [crush](./crush/on_boarding.md) - Charm's terminal AI coding assistant for interactive code generation. _(Go)_
- [DeepCode](./DeepCode/on_boarding.md) - AI-powered code analysis and generation agent for document and code processing. _(Python)_
- [deepwiki-open](./deepwiki-open/on_boarding.md) - FastAPI+Next.js tool auto-generating interactive wikis and chat for GitHub repos. _(TypeScript)_
- [dyad](./dyad/on_boarding.md) - Local AI app builder with IPC-based UI for code generation workflows. _(TypeScript)_
- [gpt-engineer](./gpt-engineer/on_boarding.md) - CLI tool that generates entire codebases from natural-language prompts. _(Python)_
- [gpt_engineer](./gpt_engineer/on_boarding.md) - AI agent that writes and iterates on full software projects from prompts. _(Python)_
- [hai-build](./hai-build/on_boarding.md) - AI-driven software development lifecycle platform with orchestration services. _(Python)_
- [llama.vim](./llama.vim/on_boarding.md) - Vim/Neovim plugin providing LLM-powered local code completion. _(VimScript)_
- [open-interpreter](./open-interpreter/on_boarding.md) - LLM-powered interpreter that runs code locally via natural language instructions. _(Python)_
- [python_code_generator](./python_code_generator/on_boarding.md) - Multi-agent AI code generation platform with web interface. _(Python)_
- [ScreenCoder](./ScreenCoder/on_boarding.md) - Tool converting UI screenshots into front-end code using vision-language models. _(Python)_
- [stagehand](./stagehand/on_boarding.md) - AI framework for browser automation combining deterministic code and natural language. _(TypeScript)_
- [SWE-agent](./SWE-agent/on_boarding.md) - Autonomous software engineering agent that fixes bugs using language models. _(Python)_
- [SWE-ReX](./SWE-ReX/on_boarding.md) - Remote execution framework for SWE-agent running code in sandboxed environments. _(Python)_

#### ML research & models

- [addons](./addons/on_boarding.md) - TensorFlow Addons extending core TensorFlow with custom ops, layers, and utilities. _(Python)_
- [aitextgen](./aitextgen/on_boarding.md) - Python tool for training and generating text with GPT-2 transformer models. _(Python)_
- [albumentations](./albumentations/on_boarding.md) - Fast and flexible image augmentation library for computer vision training pipelines. _(Python)_
- [AlphaPy](./AlphaPy/on_boarding.md) - Machine learning framework for quantitative finance and sports analytics workflows. _(Python)_
- [antialiased-cnns](./antialiased-cnns/on_boarding.md) - PyTorch implementations of antialiased convolutional networks using blur-pooling layers. _(Python)_
- [AutoDL-Projects](./AutoDL-Projects/on_boarding.md) - Research toolkit for neural architecture search and hyperparameter optimization experiments. _(Python)_
- [avalanche](./avalanche/on_boarding.md) - PyTorch-based continual learning research library with strategies and benchmarks. _(Python)_
- [BasicTS](./BasicTS/on_boarding.md) - PyTorch benchmark and toolbox for time series forecasting deep learning models. _(Python)_
- [bayesian_meta_learning](./bayesian_meta_learning/on_boarding.md) - Research code exploring Bayesian meta-learning strategies for few-shot tasks. _(Python)_
- [BCEmbedding](./BCEmbedding/on_boarding.md) - Bilingual and crosslingual embedding and reranking models for retrieval and RAG. _(Python)_
- [benchmark_VAE](./benchmark_VAE/on_boarding.md) - Unified implementation and benchmarking of variational autoencoder generative models. _(Python)_
- [bert-extractive-summarizer](./bert-extractive-summarizer/on_boarding.md) - BERT-based extractive text summarization library with embedding-based sentence selection. _(Python)_
- [BERTopic](./BERTopic/on_boarding.md) - Topic modeling library combining transformer embeddings with c-TF-IDF clustering. _(Python)_
- [bindsnet](./bindsnet/on_boarding.md) - Spiking neural network simulation library built on PyTorch for biological modeling. _(Python)_
- [boruta_py](./boruta_py/on_boarding.md) - Python implementation of the Boruta all-relevant feature selection algorithm. _(Python)_
- [causal-learn](./causal-learn/on_boarding.md) - Python package for causal discovery algorithms and structure learning. _(Python)_
- [CBAM.PyTorch](./CBAM.PyTorch/on_boarding.md) - PyTorch implementation of the Convolutional Block Attention Module for CNNs. _(Python)_
- [ChatGLM-6B](./ChatGLM-6B/on_boarding.md) - Open bilingual chat model based on the GLM architecture with fine-tuning scripts. _(Python)_
- [chatterbox](./chatterbox/on_boarding.md) - Open-source text-to-speech and voice conversion deep learning model. _(Python)_
- [ChatTTS](./ChatTTS/on_boarding.md) - Generative text-to-speech model optimized for expressive dialogue synthesis. _(Python)_
- [ckiptagger](./ckiptagger/on_boarding.md) - Chinese NLP toolkit for word segmentation, POS tagging, and named entity recognition. _(Python)_
- [ClassyVision](./ClassyVision/on_boarding.md) - Facebook's modular end-to-end PyTorch image classification training framework. _(Python)_
- [clip-rt](./clip-rt/on_boarding.md) - Real-time CLIP-based visual understanding for robotics and perception. _(Python)_
- [clothes-virtual-try-on](./clothes-virtual-try-on/on_boarding.md) - Deep learning virtual clothing try-on system with Gradio interface. _(Python)_
- [CogDL](./CogDL/on_boarding.md) - Extensive graph deep learning research toolkit with many benchmarks and models. _(Python)_
- [compare_gan](./compare_gan/on_boarding.md) - Research framework for training and benchmarking GAN variants at scale. _(Python)_
- [CompressAI](./CompressAI/on_boarding.md) - PyTorch library for learned neural image and video compression models. _(Python)_
- [ConvNeXt-V2](./ConvNeXt-V2/on_boarding.md) - PyTorch implementation of ConvNeXt V2 vision backbone models. _(Python)_
- [CosyVoice](./CosyVoice/on_boarding.md) - Multilingual zero-shot text-to-speech synthesis model with voice cloning. _(Python)_
- [CTGAN](./CTGAN/on_boarding.md) - Conditional GAN for generating synthetic tabular data resembling real datasets. _(Python)_
- [datasets](./datasets/on_boarding.md) - Hugging Face library for loading, processing, and sharing ML datasets. _(Python)_
- [Deep-Live-Cam](./Deep-Live-Cam/on_boarding.md) - Real-time deepfake face-swap pipeline for live webcam video streams. _(Python)_
- [deepface](./deepface/on_boarding.md) - Lightweight face recognition and attribute analysis framework wrapping many models. _(Python)_
- [deepgaze](./deepgaze/on_boarding.md) - Computer vision library for head pose, gaze, and saliency estimation. _(Python)_
- [denoiser](./denoiser/on_boarding.md) - Real-time audio speech denoising using an encoder-decoder deep neural network. _(Python)_
- [Dense_OpticalFlow_and_CNN_based_Motion_Segmentation_and_Object_Recognition](./Dense_OpticalFlow_and_CNN_based_Motion_Segmentation_and_Object_Recognition/on_boarding.md) - Video pipeline combining dense optical flow with CNNs for motion segmentation. _(Python)_
- [detectron2](./detectron2/on_boarding.md) - Facebook's PyTorch object detection and segmentation research platform. _(Python)_
- [DeTikZify](./DeTikZify/on_boarding.md) - Generative model converting sketches and images into editable TikZ vector code. _(Python)_
- [dgl](./dgl/on_boarding.md) - Deep Graph Library providing graph neural network primitives for PyTorch and others. _(Python)_
- [diffusers](./diffusers/on_boarding.md) - Hugging Face library of state-of-the-art diffusion models for image and audio generation. _(Python)_
- [DocLayout-YOLO](./DocLayout-YOLO/on_boarding.md) - YOLO-based deep learning model for document layout analysis. _(Python)_
- [DPR](./DPR/on_boarding.md) - Facebook Dense Passage Retrieval bi-encoder for open-domain question answering. _(Python)_
- [EasyOCR](./EasyOCR/on_boarding.md) - Ready-to-use OCR toolkit supporting 80+ languages with deep learning models. _(Python)_
- [EasyRec](./EasyRec/on_boarding.md) - Configurable deep learning recommendation model training and serving framework. _(Python)_
- [efficientnet](./efficientnet/on_boarding.md) - Keras/TensorFlow implementation of EfficientNet convolutional image classification models. _(Python)_
- [elephas](./elephas/on_boarding.md) - Distributed deep learning with Keras on Apache Spark clusters. _(Python)_
- [ERNIE](./ERNIE/on_boarding.md) - Large-scale pretrained NLP model from Baidu with knowledge integration. _(Python)_
- [face_recognition](./face_recognition/on_boarding.md) - Simple Python library for face recognition with CLI tools. _(Python)_
- [fairseq](./fairseq/on_boarding.md) - PyTorch sequence modeling toolkit for translation, summarization, and language modeling. _(Python)_
- [fast-bert](./fast-bert/on_boarding.md) - Easy-to-use library for BERT-based NLP classification and NER. _(Python)_
- [fastdup](./fastdup/on_boarding.md) - Tool for finding duplicates and anomalies in large image datasets. _(Python)_
- [FastVideo](./FastVideo/on_boarding.md) - High-performance toolkit for training and inference of video generation models. _(Python)_
- [flair](./flair/on_boarding.md) - PyTorch-based NLP library for state-of-the-art text embeddings and tagging. _(Python)_
- [flow_matching](./flow_matching/on_boarding.md) - Reference implementation of flow matching generative models for text and images. _(Python)_
- [fold](./fold/on_boarding.md) - TensorFlow library for processing dynamically-structured deep learning inputs. _(Python)_
- [FoolNLTK](./FoolNLTK/on_boarding.md) - Chinese natural language processing toolkit for segmentation, POS, and NER. _(Python)_
- [gae](./gae/on_boarding.md) - Graph autoencoder reference implementation for learning graph representations. _(Python)_
- [geatpy](./geatpy/on_boarding.md) - Python evolutionary algorithms framework with population-based optimization. _(Python)_
- [gemma_pytorch](./gemma_pytorch/on_boarding.md) - Official PyTorch implementation of Google Gemma open language models. _(Python)_
- [gflownet](./gflownet/on_boarding.md) - Framework for GFlowNet generative flow networks on structured data. _(Python)_
- [GFPGAN](./GFPGAN/on_boarding.md) - GAN-based algorithm for real-world blind face restoration. _(Python)_
- [gplearn](./gplearn/on_boarding.md) - Scikit-learn compatible genetic programming for symbolic regression. _(Python)_
- [gradslam](./gradslam/on_boarding.md) - Differentiable SLAM library for 3D reconstruction in PyTorch. _(Python)_
- [graph4nlp](./graph4nlp/on_boarding.md) - Library for NLP tasks using graph neural networks. _(Python)_
- [GraphGym](./GraphGym/on_boarding.md) - Platform for systematic design and evaluation of graph neural networks. _(Python)_
- [gym](./gym/on_boarding.md) - OpenAI toolkit providing reinforcement learning environments and the Env API. _(Python)_
- [gym-pybullet-drones](./gym-pybullet-drones/on_boarding.md) - PyBullet-based Gym environments for quadcopter reinforcement learning. _(Python)_
- [HanLP](./HanLP/on_boarding.md) - Multilingual NLP toolkit supporting tokenization, parsing, and named entity recognition. _(Python)_
- [hiddenlayer](./hiddenlayer/on_boarding.md) - Neural network graph visualization library for PyTorch and TensorFlow. _(Python)_
- [hls4ml](./hls4ml/on_boarding.md) - Translates deep learning models to FPGA high-level synthesis code. _(Python)_
- [hopfield-layers](./hopfield-layers/on_boarding.md) - PyTorch implementation of modern Hopfield networks as attention layers. _(Python)_
- [Hunyuan3D-2.1](./Hunyuan3D-2.1/on_boarding.md) - Tencent model pipeline for generating 3D shapes and textures from inputs. _(Python)_
- [jax](./jax/on_boarding.md) - Composable transformations of NumPy programs with autodiff and JIT for accelerators. _(Python)_
- [jieba](./jieba/on_boarding.md) - Popular Chinese text segmentation library with dictionary-based tokenization. _(Python)_
- [keras](./keras/on_boarding.md) - High-level deep learning API running on TensorFlow, JAX, or PyTorch. _(Python)_
- [keras-resnet](./keras-resnet/on_boarding.md) - Keras implementation of ResNet architectures for image classification. _(Python)_
- [Keras-TextClassification](./Keras-TextClassification/on_boarding.md) - Keras toolkit with many text classification model implementations. _(Python)_
- [khaiii](./khaiii/on_boarding.md) - Kakao Korean morphological analyzer using a CNN-based model. _(Python)_
- [KoBERT](./KoBERT/on_boarding.md) - Korean BERT pretrained language model with tokenizer and utilities. _(Python)_
- [kornia](./kornia/on_boarding.md) - Differentiable computer vision library for PyTorch with classical CV operators. _(Python)_
- [labelme](./labelme/on_boarding.md) - Qt-based image polygonal annotation tool for computer vision datasets. _(Python)_
- [langdetect](./langdetect/on_boarding.md) - Port of Google language-detection library for Python. _(Python)_
- [LaTeX-OCR](./LaTeX-OCR/on_boarding.md) - Neural OCR model that converts images of math formulas to LaTeX. _(Python)_
- [libra](./libra/on_boarding.md) - High-level facade library that automates end-to-end ML workflows. _(Python)_
- [Lidar_AI_Solution](./Lidar_AI_Solution/on_boarding.md) - NVIDIA LiDAR and multi-modal perception pipeline for autonomous driving. _(Python)_
- [lightning](./lightning/on_boarding.md) - PyTorch Lightning framework for organized, scalable deep learning training. _(Python)_
- [lightweight-gan](./lightweight-gan/on_boarding.md) - Minimal implementation of lightweight GAN for one-GPU image generation. _(Python)_
- [LightZero](./LightZero/on_boarding.md) - MCTS-based reinforcement learning framework with AlphaZero and MuZero. _(Python)_
- [llama](./llama/on_boarding.md) - Inference code for Meta's Llama family of open foundation language models. _(Python)_
- [llama3](./llama3/on_boarding.md) - Reference inference pipeline for Meta's Llama 3 language models. _(Python)_
- [LLaVA](./LLaVA/on_boarding.md) - Multimodal LLM combining vision and language for visual instruction following. _(Python)_
- [ManiSkill](./ManiSkill/on_boarding.md) - GPU-parallelized robotic manipulation simulation and benchmark suite. _(Python)_
- [metric-learn](./metric-learn/on_boarding.md) - Scikit-learn compatible Python library for supervised metric learning. _(Python)_
- [micro_diffusion](./micro_diffusion/on_boarding.md) - Compact latent diffusion transformer implementation with training pipeline. _(Python)_
- [MinerU](./MinerU/on_boarding.md) - PDF and document extraction toolkit converting content to machine-readable formats. _(Python)_
- [ml-cvnets](./ml-cvnets/on_boarding.md) - Apple computer vision network training library for mobile models. _(Python)_
- [ml-fastvit](./ml-fastvit/on_boarding.md) - Apple FastViT hybrid vision transformer reference implementation. _(Python)_
- [ml4a](./ml4a/on_boarding.md) - Machine learning for artists library bundling creative deep learning models. _(Python)_
- [MLBox](./MLBox/on_boarding.md) - Automated machine learning library for preprocessing and model stacking. _(Python)_
- [mmdetection](./mmdetection/on_boarding.md) - Modular PyTorch toolbox for object detection and instance segmentation research. _(Python)_
- [model2vec](./model2vec/on_boarding.md) - Toolkit for distilling static embedding models from transformer encoders. _(Python)_
- [models](./models/on_boarding.md) - Collection of reference neural network model implementations and training pipelines. _(Python)_
- [nano-llama31](./nano-llama31/on_boarding.md) - Minimal from-scratch reference implementation of the Llama 3.1 model. _(Python)_
- [neat-python](./neat-python/on_boarding.md) - Python implementation of NeuroEvolution of Augmenting Topologies (NEAT) algorithm. _(Python)_
- [nerfacc](./nerfacc/on_boarding.md) - Accelerated neural radiance fields library with efficient volumetric ray marching. _(Python)_
- [nltk](./nltk/on_boarding.md) - Comprehensive natural language processing toolkit with corpora and algorithms. _(Python)_
- [nsfw_model](./nsfw_model/on_boarding.md) - Pretrained deep learning model for classifying NSFW images and video. _(Python)_
- [omnizart](./omnizart/on_boarding.md) - Automatic music transcription toolkit with deep learning models. _(Python)_
- [once-for-all](./once-for-all/on_boarding.md) - Train one elastic supernet that specializes into efficient subnets for deployment. _(Python)_
- [Open3D-ML](./Open3D-ML/on_boarding.md) - Open3D extension for 3D machine learning tasks on point clouds and meshes. _(Python)_
- [OpenNE](./OpenNE/on_boarding.md) - Toolkit of graph network embedding algorithms for representation learning. _(Python)_
- [openWakeWord-cpp](./openWakeWord-cpp/on_boarding.md) - Real-time wake word detection engine with streaming audio processing. _(C++)_
- [PaddleOCR](./PaddleOCR/on_boarding.md) - PaddlePaddle toolkit for multilingual optical character recognition and document understanding. _(Python)_
- [penzai](./penzai/on_boarding.md) - JAX research toolkit treating neural networks as manipulable pytrees. _(Python)_
- [Personae](./Personae/on_boarding.md) - Reinforcement and supervised learning experiments for financial market trading. _(Python)_
- [PGL](./PGL/on_boarding.md) - PaddlePaddle graph learning framework for GNN development. _(Python)_
- [PGPortfolio](./PGPortfolio/on_boarding.md) - Deep reinforcement learning framework for cryptocurrency portfolio management. _(Python)_
- [phonemizer](./phonemizer/on_boarding.md) - Multilingual text-to-phoneme conversion library for speech applications. _(Python)_
- [pke](./pke/on_boarding.md) - Python keyphrase extraction toolkit with unsupervised and supervised methods. _(Python)_
- [Pointnet2_PyTorch](./Pointnet2_PyTorch/on_boarding.md) - PyTorch implementation of PointNet++ for 3D point cloud deep learning. _(Python)_
- [poker_ai](./poker_ai/on_boarding.md) - Poker AI research codebase with counterfactual regret minimization training. _(Python)_
- [pseudo](./pseudo/on_boarding.md) - Deep learning prototype of graph neural networks for scientific machine learning. _(Python)_
- [PVT](./PVT/on_boarding.md) - Pyramid Vision Transformer implementation for various computer vision tasks. _(Python)_
- [pygod](./pygod/on_boarding.md) - Graph anomaly detection library built on PyTorch Geometric. _(Python)_
- [pymarl](./pymarl/on_boarding.md) - PyTorch framework for multi-agent reinforcement learning research. _(Python)_
- [pyserini](./pyserini/on_boarding.md) - Python toolkit for reproducible information retrieval research with dense/sparse retrieval. _(Python)_
- [pytorch](./pytorch/on_boarding.md) - Deep learning framework with dynamic computation graphs and GPU acceleration. _(Python)_
- [PyTorch-Encoding](./PyTorch-Encoding/on_boarding.md) - PyTorch toolkit for semantic segmentation with synchronized batch normalization. _(Python)_
- [pytorch3d](./pytorch3d/on_boarding.md) - PyTorch library for 3D deep learning on meshes, point clouds and volumes. _(Python)_
- [pytorch_geometric](./pytorch_geometric/on_boarding.md) - PyTorch library for deep learning on graphs and irregular structures. _(Python)_
- [PyTorch_YOLOv4](./PyTorch_YOLOv4/on_boarding.md) - PyTorch implementation of the YOLOv4 object detection model. _(Python)_
- [qlib](./qlib/on_boarding.md) - AI-oriented quantitative investment research platform with reinforcement learning. _(Python)_
- [Real-ESRGAN](./Real-ESRGAN/on_boarding.md) - Practical image and video super-resolution using enhanced GAN models. _(Python)_
- [Real-Time-Voice-Cloning](./Real-Time-Voice-Cloning/on_boarding.md) - Real-time voice cloning toolkit using speaker encoder and neural vocoder. _(Python)_
- [RecLearn](./RecLearn/on_boarding.md) - Modular recommender systems research library for deep learning models. _(Python)_
- [recommenders](./recommenders/on_boarding.md) - Microsoft toolkit with examples and best practices for building recommender systems. _(Python)_
- [rembg](./rembg/on_boarding.md) - Tool to remove backgrounds from images using deep learning segmentation models. _(Python)_
- [rerankers](./rerankers/on_boarding.md) - Unified Python interface for document reranking models used in retrieval pipelines. _(Python)_
- [rf-detr](./rf-detr/on_boarding.md) - Real-time DETR-based object detection framework with modular components. _(Python)_
- [RLBench](./RLBench/on_boarding.md) - Robot learning benchmark and environment for reinforcement learning research. _(Python)_
- [ROMP](./ROMP/on_boarding.md) - Deep learning pipeline for 3D multi-person pose and shape estimation from images. _(Python)_
- [rsl_rl](./rsl_rl/on_boarding.md) - Fast PyTorch reinforcement learning library focused on robotics training loops. _(Python)_
- [sam](./sam/on_boarding.md) - PyTorch implementation of Sharpness-Aware Minimization optimizer for better generalization. _(Python)_
- [Sapiens](./Sapiens/on_boarding.md) - Meta foundation model for human-centric vision tasks like pose and segmentation. _(Python)_
- [sdfstudio](./sdfstudio/on_boarding.md) - Unified framework for neural implicit surface reconstruction and rendering. _(Python)_
- [Semi-supervised-learning](./Semi-supervised-learning/on_boarding.md) - Unified PyTorch codebase for semi-supervised and imbalanced learning algorithms. _(Python)_
- [ShuffleNet-Series](./ShuffleNet-Series/on_boarding.md) - Reference implementations of ShuffleNet and related efficient neural architectures. _(Python)_
- [skip-thoughts](./skip-thoughts/on_boarding.md) - Reference implementation of skip-thought sentence embedding vectors. _(Python)_
- [skrub](./skrub/on_boarding.md) - Data cleaning and feature engineering library for tabular machine learning. _(Python)_
- [sktime](./sktime/on_boarding.md) - Unified Python framework for machine learning with time series data. _(Python)_
- [snntorch](./snntorch/on_boarding.md) - PyTorch-based framework for training and simulating spiking neural networks. _(Python)_
- [solo-learn](./solo-learn/on_boarding.md) - Self-supervised learning methods library in PyTorch Lightning. _(Python)_
- [spaCy](./spaCy/on_boarding.md) - Industrial-strength natural language processing library in Python and Cython. _(Python)_
- [sparse_attention](./sparse_attention/on_boarding.md) - OpenAI reference implementation of sparse attention mechanisms for transformers. _(Python)_
- [spikingjelly](./spikingjelly/on_boarding.md) - PyTorch-based deep learning framework for spiking neural networks. _(Python)_
- [sru](./sru/on_boarding.md) - Simple recurrent unit PyTorch implementation with CUDA acceleration. _(Python)_
- [stable-diffusion-tensorflow](./stable-diffusion-tensorflow/on_boarding.md) - TensorFlow and Keras implementation of the Stable Diffusion image generation model. _(Python)_
- [stable-ts](./stable-ts/on_boarding.md) - Whisper wrapper providing stable word-level timestamps for audio transcription. _(Python)_
- [super-resolution](./super-resolution/on_boarding.md) - Reference PyTorch implementations of image super-resolution deep learning models. _(Python)_
- [supervision](./supervision/on_boarding.md) - Reusable computer vision utilities for detection tracking and visualization. _(Python)_
- [Synchronized-BatchNorm-PyTorch](./Synchronized-BatchNorm-PyTorch/on_boarding.md) - Synchronized batch normalization PyTorch module for multi-GPU distributed training. _(Python)_
- [tensorflow](./tensorflow/on_boarding.md) - End-to-end open-source machine learning platform for research and production. _(Python)_
- [tensorflow-DeepFM](./tensorflow-DeepFM/on_boarding.md) - TensorFlow implementation of the DeepFM factorization machine recommendation model. _(Python)_
- [TensorFlowTTS](./TensorFlowTTS/on_boarding.md) - Real-time state-of-the-art speech synthesis toolkit built on TensorFlow. _(Python)_
- [TextGrapher](./TextGrapher/on_boarding.md) - Tool for converting raw text into interactive knowledge graphs. _(Python)_
- [tf_unet](./tf_unet/on_boarding.md) - TensorFlow implementation of the U-Net convolutional network for image segmentation. _(Python)_
- [theseus](./theseus/on_boarding.md) - Differentiable nonlinear optimization library for robotics and computer vision. _(Python)_
- [THULAC-Python](./THULAC-Python/on_boarding.md) - Chinese lexical analyzer for segmentation and part-of-speech tagging. _(Python)_
- [TimeMixer](./TimeMixer/on_boarding.md) - Time series forecasting model using decomposable multiscale mixing architecture. _(Python)_
- [tods](./tods/on_boarding.md) - Automated machine learning system for outlier detection on time series data. _(Python)_
- [torchgan](./torchgan/on_boarding.md) - PyTorch-based framework for designing and training generative adversarial networks. _(Python)_
- [torchgfn](./torchgfn/on_boarding.md) - PyTorch library for generative flow network research and implementation. _(Python)_
- [torchsde](./torchsde/on_boarding.md) - Differentiable stochastic differential equation solvers for PyTorch. _(Python)_
- [torchstat](./torchstat/on_boarding.md) - Lightweight neural network analyzer reporting flops parameters and memory usage. _(Python)_
- [torchsurv](./torchsurv/on_boarding.md) - PyTorch library for deep learning survival analysis. _(Python)_
- [trackers](./trackers/on_boarding.md) - Object tracking library implementing SORT and DeepSORT algorithms. _(Python)_
- [TradingGym](./TradingGym/on_boarding.md) - Reinforcement learning environment for backtesting and developing trading strategies. _(Python)_
- [transformers](./transformers/on_boarding.md) - State-of-the-art pretrained models for NLP vision and audio from Hugging Face. _(Python)_
- [TTS](./TTS/on_boarding.md) - Deep learning toolkit for text-to-speech with pretrained voice models. _(Python)_
- [uis-rnn](./uis-rnn/on_boarding.md) - Unbounded interleaved-state recurrent neural network for speaker diarization. _(Python)_
- [ultralytics](./ultralytics/on_boarding.md) - YOLO computer vision framework for object detection segmentation and classification. _(Python)_
- [unidiffuser](./unidiffuser/on_boarding.md) - Unified multi-modal diffusion model for generating images text and joint samples. _(Python)_
- [vit-pytorch](./vit-pytorch/on_boarding.md) - PyTorch implementations of vision transformer variants and related models. _(Python)_
- [vits](./vits/on_boarding.md) - Conditional variational autoencoder with adversarial learning for end-to-end speech synthesis. _(Python)_
- [VLA-OS](./VLA-OS/on_boarding.md) - Research framework for vision-language-action foundation models in robotics. _(Python)_
- [webdataset](./webdataset/on_boarding.md) - High-performance I/O library for PyTorch using tar archives for training data. _(Python)_
- [whisper](./whisper/on_boarding.md) - OpenAI speech recognition model for multilingual audio transcription and translation. _(Python)_
- [WildGS-SLAM](./WildGS-SLAM/on_boarding.md) - Gaussian splatting-based SLAM system for 3D mapping and camera pose tracking. _(Python)_
- [xlstm](./xlstm/on_boarding.md) - Extended LSTM architecture research toolkit for language modeling. _(Python)_
- [YOLO_tensorflow](./YOLO_tensorflow/on_boarding.md) - TensorFlow implementation of the YOLO real-time object detection network. _(Python)_
- [yolov5](./yolov5/on_boarding.md) - PyTorch implementation of YOLOv5 real-time object detection model. _(Python)_
- [Yolov5-deepsort-inference](./Yolov5-deepsort-inference/on_boarding.md) - Real-time object detection and tracking pipeline combining YOLOv5 with DeepSORT. _(Python)_

#### Training, evaluation & guardrails

- [agentdojo](./agentdojo/on_boarding.md) - Benchmark suite for evaluating LLM agent robustness against prompt-injection attacks. _(Python)_
- [AIX360](./AIX360/on_boarding.md) - IBM toolkit providing algorithms and metrics for AI explainability and interpretability. _(Python)_
- [Alien](./Alien/on_boarding.md) - Active learning toolkit for iteratively selecting informative samples and training models. _(Python)_
- [async_rlhf](./async_rlhf/on_boarding.md) - Asynchronous reinforcement learning from human feedback training with DPO and PPO. _(Python)_
- [baxbench](./baxbench/on_boarding.md) - Benchmark system for evaluating security of code generated by large language models. _(Python)_
- [beir](./beir/on_boarding.md) - Heterogeneous benchmark for zero-shot evaluation of information retrieval models. _(Python)_
- [chatarena](./chatarena/on_boarding.md) - Multi-agent language game environment for evaluating LLMs in interactive settings. _(Python)_
- [deepeval](./deepeval/on_boarding.md) - Unit-testing framework for evaluating and benchmarking LLM outputs with metrics. _(Python)_
- [DeepSpeed](./DeepSpeed/on_boarding.md) - Microsoft library optimizing large-scale distributed deep learning training and inference. _(Python)_
- [DiCE](./DiCE/on_boarding.md) - Microsoft library generating diverse counterfactual explanations for classifiers. _(Python)_
- [dlrover](./dlrover/on_boarding.md) - Distributed deep learning training orchestrator with elastic scheduling and fault tolerance. _(Python)_
- [finetuner](./finetuner/on_boarding.md) - Jina AI Cloud library for fine-tuning deep learning embedding models. _(Python)_
- [fitlog](./fitlog/on_boarding.md) - ML experiment logging tool with Git integration and web dashboard. _(Python)_
- [GaLore](./GaLore/on_boarding.md) - Memory-efficient LLM training via gradient low-rank projection. _(Python)_
- [ImageReward](./ImageReward/on_boarding.md) - Reward model for evaluating and fine-tuning text-to-image generation. _(Python)_
- [inspect_ai](./inspect_ai/on_boarding.md) - LLM evaluation framework for building and running safety and capability evals. _(Python)_
- [invariant](./invariant/on_boarding.md) - Policy engine and language for analyzing and enforcing LLM agent behavior. _(Python)_
- [invariant-gateway](./invariant-gateway/on_boarding.md) - LLM proxy gateway with guardrails, monitoring, and multi-provider routing. _(Python)_
- [jiant](./jiant/on_boarding.md) - NLP experiment framework for multitask and transfer learning benchmarks. _(Python)_
- [LAMA](./LAMA/on_boarding.md) - Framework for probing language models for factual and commonsense knowledge. _(Python)_
- [lighteval](./lighteval/on_boarding.md) - Hugging Face LLM evaluation suite with configurable task registry. _(Python)_
- [llm-guard](./llm-guard/on_boarding.md) - Content-scanning toolkit providing input/output safety scanners for LLMs. _(Python)_
- [matharena](./matharena/on_boarding.md) - Evaluation framework for testing LLM performance on mathematical problems. _(Python)_
- [Megatron-LM](./Megatron-LM/on_boarding.md) - NVIDIA framework for large-scale distributed language model training. _(Python)_
- [mlflow](./mlflow/on_boarding.md) - Open-source platform for managing the end-to-end machine learning lifecycle. _(Python)_
- [Olive](./Olive/on_boarding.md) - Hardware-aware AI model optimization toolkit with pluggable compression techniques. _(Python)_
- [optuna](./optuna/on_boarding.md) - Hyperparameter optimization framework with define-by-run API and pruning. _(Python)_
- [PaddleSlim](./PaddleSlim/on_boarding.md) - PaddlePaddle model compression toolkit with pruning, quantization, and NAS. _(Python)_
- [piq](./piq/on_boarding.md) - PyTorch image quality assessment metrics collection for model evaluation. _(Python)_
- [pyreft](./pyreft/on_boarding.md) - Library for fine-tuning LLMs with representation finetuning interventions. _(Python)_
- [pytorch-lightning](./pytorch-lightning/on_boarding.md) - Lightweight PyTorch wrapper organizing training code for scale and reproducibility. _(Python)_
- [RagaAI-Catalyst](./RagaAI-Catalyst/on_boarding.md) - Platform for LLM observability, evaluation, and experiment tracking. _(Python)_
- [rexmex](./rexmex/on_boarding.md) - Recommender system evaluation metrics library for machine learning researchers. _(Python)_
- [RL](./RL/on_boarding.md) - RLHF training framework for large language models with distributed computing. _(Python)_
- [ROLL](./ROLL/on_boarding.md) - Distributed RLHF training framework built on Ray for LLM post-training. _(Python)_
- [Ruli](./Ruli/on_boarding.md) - Research toolkit for machine unlearning and privacy attack experiments. _(Python)_
- [safe-rlhf](./safe-rlhf/on_boarding.md) - Safe reinforcement learning from human feedback framework for language model alignment. _(Python)_
- [smollm3_finetune](./smollm3_finetune/on_boarding.md) - Fine-tuning scripts and utilities for the SmolLM3 small language model. _(Python)_
- [SWE-bench](./SWE-bench/on_boarding.md) - Benchmark evaluating language models on real-world GitHub issue resolution. _(Python)_
- [SWEBench](./SWEBench/on_boarding.md) - Benchmark for evaluating software engineering tasks with code generation models. _(Python)_
- [TextBrewer](./TextBrewer/on_boarding.md) - Knowledge distillation toolkit for compressing NLP models from teacher to student. _(Python)_
- [ToolFuzz](./ToolFuzz/on_boarding.md) - Fuzzing framework for testing tools used by AI agents like LangChain and AutoGen. _(Python)_
- [trojai-submission-all](./trojai-submission-all/on_boarding.md) - Repository aggregating TrojAI challenge submissions for AI trojan detection. _(Python)_
- [uncertainty-toolbox](./uncertainty-toolbox/on_boarding.md) - Toolbox for predictive uncertainty quantification calibration and visualization. _(Python)_
- [unsloth](./unsloth/on_boarding.md) - Fast LLM fine-tuning library with optimized kernels and memory efficiency. _(Python)_
- [verl](./verl/on_boarding.md) - Volcano Engine reinforcement learning library for post-training large language models. _(Python)_
- [vizier](./vizier/on_boarding.md) - Google's scalable black-box optimization service for hyperparameter tuning. _(Python)_
- [zenml](./zenml/on_boarding.md) - Extensible MLOps framework for creating production-ready machine learning pipelines. _(Python)_

### Data & analytics

#### ETL & workflow orchestration

- [airflow](./airflow/on_boarding.md) - Platform to programmatically author, schedule, and monitor DAG-based data workflows. _(Python)_
- [BayerCLAW](./BayerCLAW/on_boarding.md) - AWS-based workflow orchestrator for running containerized bioinformatics pipelines. _(Python)_
- [bonobo](./bonobo/on_boarding.md) - Lightweight Python ETL framework for building functional data transformation graphs. _(Python)_
- [bytewax](./bytewax/on_boarding.md) - Python stream processing framework built on top of Rust's Timely Dataflow. _(Python)_
- [celery](./celery/on_boarding.md) - Distributed task queue for running asynchronous background jobs with message brokers. _(Python)_
- [conductor](./conductor/on_boarding.md) - Netflix distributed workflow orchestration engine for microservices. _(Java)_
- [django-celery-beat](./django-celery-beat/on_boarding.md) - Database-backed periodic task scheduler for Celery managed through Django admin. _(Python)_
- [faust](./faust/on_boarding.md) - Python stream processing library for Kafka with declarative agents. _(Python)_
- [fugue](./fugue/on_boarding.md) - Unified distributed computing interface for Spark, Dask, and Ray workflows. _(Python)_
- [lea](./lea/on_boarding.md) - Minimalist SQL-based data transformation tool that orchestrates DAGs. _(Python)_
- [metaflow](./metaflow/on_boarding.md) - Netflix human-centric framework for building and deploying data science workflows. _(Python)_
- [prefect](./prefect/on_boarding.md) - Modern Python workflow orchestration engine for data pipelines. _(Python)_
- [quix-streams](./quix-streams/on_boarding.md) - Python streaming framework for Kafka-based real-time data pipelines. _(Python)_
- [redbeat](./redbeat/on_boarding.md) - Redis-backed scheduler for Celery enabling dynamic periodic task management and persistence. _(Python)_
- [redun](./redun/on_boarding.md) - Expressive workflow framework using functional reactive programming for task orchestration. _(Python)_
- [rq-scheduler](./rq-scheduler/on_boarding.md) - Job scheduler extension for Redis Queue enabling periodic and future-dated tasks. _(Python)_
- [saga](./saga/on_boarding.md) - Saga pattern implementation for distributed transaction orchestration across services. _(Python)_
- [snakemake](./snakemake/on_boarding.md) - Python-based workflow management system for scientific reproducible pipelines. _(Python)_
- [SpiffWorkflow](./SpiffWorkflow/on_boarding.md) - Python-based workflow engine implementing BPMN business process management. _(Python)_
- [streamparse](./streamparse/on_boarding.md) - Python tools for running and managing Apache Storm topologies. _(Python)_
- [submitit](./submitit/on_boarding.md) - Python tool for submitting and managing jobs on SLURM clusters. _(Python)_
- [taskiq](./taskiq/on_boarding.md) - Python asynchronous distributed task queue inspired by Celery. _(Python)_

#### Databases & storage

- [aiomysql](./aiomysql/on_boarding.md) - Asynchronous MySQL driver for Python asyncio applications with connection pooling. _(Python)_
- [aiosqlite](./aiosqlite/on_boarding.md) - Asynchronous wrapper around Python's sqlite3 for use in asyncio code. _(Python)_
- [btree](./btree/on_boarding.md) - In-memory B-tree data structure implementation for ordered key storage. _(Python)_
- [djongo](./djongo/on_boarding.md) - Django ORM connector translating relational queries into MongoDB operations. _(Python)_
- [godror](./godror/on_boarding.md) - Go database/sql driver for Oracle Database using ODPI-C. _(Go)_
- [influxdb-python](./influxdb-python/on_boarding.md) - Official Python client library for InfluxDB time-series database. _(Python)_
- [mongo-python-driver](./mongo-python-driver/on_boarding.md) - Official Python driver for connecting to and querying MongoDB databases. _(Python)_
- [orator](./orator/on_boarding.md) - ActiveRecord-style ORM for Python inspired by Laravel's Eloquent. _(Python)_
- [orm](./orm/on_boarding.md) - Async ORM for Python built on SQLAlchemy Core with typed models. _(Python)_
- [piccolo](./piccolo/on_boarding.md) - Async Python ORM and query builder supporting multiple database backends. _(Python)_
- [pokedex](./pokedex/on_boarding.md) - Relational database of Pokemon data with CLI for export and queries. _(Python)_
- [psycopg2](./psycopg2/on_boarding.md) - PostgreSQL database adapter for Python with full DB-API 2.0 compliance. _(Python)_
- [PyHive](./PyHive/on_boarding.md) - Python DBAPI and SQLAlchemy dialect for Hive, Presto and Trino. _(Python)_
- [pymemcache](./pymemcache/on_boarding.md) - Comprehensive pure-Python memcached client library. _(Python)_
- [pymodm](./pymodm/on_boarding.md) - Object-document mapper for MongoDB providing declarative model definitions. _(Python)_
- [python-driver](./python-driver/on_boarding.md) - Official Python driver for Apache Cassandra and DataStax Enterprise clusters. _(Python)_
- [python-irodsclient](./python-irodsclient/on_boarding.md) - Python client library for the iRODS data management system. _(Python)_
- [python-oracledb](./python-oracledb/on_boarding.md) - Python driver for Oracle Database with async support and connection pooling. _(Python)_
- [redis-py](./redis-py/on_boarding.md) - Official Python client library for the Redis key-value store. _(Python)_
- [sqlalchemy](./sqlalchemy/on_boarding.md) - Python SQL toolkit and Object Relational Mapper for database abstraction. _(Python)_
- [sqlalchemy-crud-plus](./sqlalchemy-crud-plus/on_boarding.md) - Enhanced CRUD operations helper library built on top of SQLAlchemy. _(Python)_
- [theine](./theine/on_boarding.md) - High-performance Python caching library with adaptive eviction policies. _(Python)_
- [tidb](./tidb/on_boarding.md) - Distributed SQL database compatible with MySQL protocol and horizontally scalable. _(Go)_
- [valkey-py](./valkey-py/on_boarding.md) - Python client library for the Valkey key-value store with cluster support. _(Python)_
- [valkey-timeseries](./valkey-timeseries/on_boarding.md) - Time series data extension module for the Valkey key-value store. _(Rust)_

#### Data processing & analysis

- [abu](./abu/on_boarding.md) - Modular quantitative trading and backtesting platform for developing and optimizing strategies. _(Python)_
- [academic-keyword-occurrence](./academic-keyword-occurrence/on_boarding.md) - Command-line web scraper that tracks academic keyword occurrence trends over time. _(Python)_
- [akshare](./akshare/on_boarding.md) - Python library fetching Chinese financial and economic market data from many sources. _(Python)_
- [asammdf](./asammdf/on_boarding.md) - Parser and editor for ASAM MDF automotive measurement data files. _(Python)_
- [AutoViz](./AutoViz/on_boarding.md) - Automated exploratory data visualization library generating charts from any dataset. _(Python)_
- [backtrader](./backtrader/on_boarding.md) - Python framework for backtesting and live trading of algorithmic investment strategies. _(Python)_
- [bt](./bt/on_boarding.md) - Flexible backtesting framework for Python with tree-structured trading strategies. _(Python)_
- [cartopy](./cartopy/on_boarding.md) - Cartographic Python library for geospatial data processing and map projection plotting. _(Python)_
- [common-pile](./common-pile/on_boarding.md) - Tooling for ingesting and processing large-scale openly-licensed text corpora. _(Python)_
- [d3py](./d3py/on_boarding.md) - Python library generating interactive D3.js and Vega visualizations from dataframes. _(Python)_
- [dask](./dask/on_boarding.md) - Parallel computing library scaling NumPy and pandas workflows across clusters. _(Python)_
- [DataProfiler](./DataProfiler/on_boarding.md) - Library for profiling, labeling, and generating reports on diverse datasets. _(Python)_
- [docling](./docling/on_boarding.md) - IBM library converting documents in many formats into structured data. _(Python)_
- [dtale](./dtale/on_boarding.md) - Web-based interactive visualizer and editor for pandas DataFrames. _(Python)_
- [explorer](./explorer/on_boarding.md) - Dataset management and trace exploration tool with policy enforcement. _(Python)_
- [FinQuant](./FinQuant/on_boarding.md) - Python library for portfolio optimization and financial quantitative analysis. _(Python)_
- [freqtrade](./freqtrade/on_boarding.md) - Open-source cryptocurrency algorithmic trading bot with backtesting. _(Python)_
- [glom](./glom/on_boarding.md) - Declarative Python library for restructuring and transforming nested data. _(Python)_
- [h3-py](./h3-py/on_boarding.md) - Python bindings for Uber H3 hexagonal geospatial indexing system. _(Python)_
- [hummingbot](./hummingbot/on_boarding.md) - Open-source framework for building high-frequency crypto market making bots. _(Python)_
- [ijson](./ijson/on_boarding.md) - Iterative JSON parser for Python handling large files without full loading. _(Python)_
- [matplotlib](./matplotlib/on_boarding.md) - Comprehensive Python library for creating static and interactive visualizations. _(Python)_
- [numpy](./numpy/on_boarding.md) - Fundamental N-dimensional array package for scientific computing in Python. _(Python)_
- [OpenBB](./OpenBB/on_boarding.md) - Open source financial investment research and data analysis platform. _(Python)_
- [optimus](./optimus/on_boarding.md) - Unified data cleaning and transformation API over Pandas, Spark and Dask. _(Python)_
- [order_book_server](./order_book_server/on_boarding.md) - Real-time order book server consuming Hyperliquid market data streams. _(Rust)_
- [pandas](./pandas/on_boarding.md) - High-performance DataFrame library for data analysis and manipulation in Python. _(Python)_
- [pathway](./pathway/on_boarding.md) - High-performance real-time streaming data processing framework with Rust engine. _(Python)_
- [pingouin](./pingouin/on_boarding.md) - Statistical package for Python built on top of Pandas and NumPy. _(Python)_
- [plotly.py](./plotly.py/on_boarding.md) - Interactive graphing library for Python creating publication-quality charts. _(Python)_
- [polars](./polars/on_boarding.md) - Fast DataFrame library with Rust engine and Python bindings. _(Rust)_
- [prettyplotlib](./prettyplotlib/on_boarding.md) - Matplotlib wrapper producing publication-ready plots with sensible defaults. _(Python)_
- [prince](./prince/on_boarding.md) - Python multivariate exploratory data analysis library for PCA and related methods. _(Python)_
- [pypeln](./pypeln/on_boarding.md) - Concurrent data pipeline library with thread, process, and asyncio backends. _(Python)_
- [pyreadstat](./pyreadstat/on_boarding.md) - Python interface reading SPSS, SAS, and Stata statistical files via C library. _(Python)_
- [python-benedict](./python-benedict/on_boarding.md) - Python dictionary subclass with keylist/keypath and serialization helpers. _(Python)_
- [qstock](./qstock/on_boarding.md) - Quantitative stock analysis toolkit with data acquisition and backtesting. _(Python)_
- [riko](./riko/on_boarding.md) - Stream processing library for creating modular data pipelines and feed aggregation. _(Python)_
- [scipy](./scipy/on_boarding.md) - Fundamental scientific computing library providing mathematics, science, and engineering algorithms. _(Python)_
- [scrapy](./scrapy/on_boarding.md) - High-level Python web crawling and scraping framework for structured data extraction. _(Python)_
- [scrapy-proxies](./scrapy-proxies/on_boarding.md) - Random proxy middleware for rotating IPs in Scrapy crawlers. _(Python)_
- [seaborn](./seaborn/on_boarding.md) - Statistical data visualization library built on matplotlib with attractive defaults. _(Python)_
- [skfolio](./skfolio/on_boarding.md) - Portfolio optimization library building on scikit-learn for quantitative finance. _(Python)_
- [splink](./splink/on_boarding.md) - Python record linkage library for deduplication across large datasets. _(Python)_
- [sqllineage](./sqllineage/on_boarding.md) - SQL lineage analysis tool tracing column and table dependencies. _(Python)_
- [superset](./superset/on_boarding.md) - Modern data exploration and visualization platform with rich dashboards. _(Python)_
- [textfilter](./textfilter/on_boarding.md) - Pipeline-based text content filtering tool for keyword-based moderation. _(Python)_
- [tika-python](./tika-python/on_boarding.md) - Python binding to Apache Tika REST services for content extraction from documents. _(Python)_
- [tushare](./tushare/on_boarding.md) - Python library for retrieving Chinese financial market data. _(Python)_
- [usaddress](./usaddress/on_boarding.md) - Python library using CRFs for parsing unstructured US address strings. _(Python)_
- [vnpy](./vnpy/on_boarding.md) - Python-based quantitative trading platform with event-driven architecture. _(Python)_
- [webscraping](./webscraping/on_boarding.md) - Web scraping pipeline for extracting job listings from online portals. _(Python)_
- [zipline](./zipline/on_boarding.md) - Pythonic algorithmic trading library for backtesting quantitative strategies. _(Python)_

### Web & UI

#### Frontend frameworks

- [angular](./angular/on_boarding.md) - Google's TypeScript framework for building scalable single-page web applications. _(TypeScript)_
- [babel](./babel/on_boarding.md) - Internationalization library providing locale data, translations, and formatting utilities. _(Python)_
- [dominate](./dominate/on_boarding.md) - Python library generating HTML documents programmatically using context managers. _(Python)_
- [fastapi](./fastapi/on_boarding.md) - Modern Python web framework for building fast APIs with type hints. _(Python)_
- [fastapi-pagination](./fastapi-pagination/on_boarding.md) - Pagination extension library for FastAPI applications. _(Python)_
- [flask](./flask/on_boarding.md) - Lightweight Python WSGI web framework with routing and templating. _(Python)_
- [flask-ask](./flask-ask/on_boarding.md) - Flask extension for rapidly building Amazon Alexa skills. _(Python)_
- [flask-jwt-extended](./flask-jwt-extended/on_boarding.md) - Flask extension for JWT-based authentication and authorization. _(Python)_
- [flask-wtf](./flask-wtf/on_boarding.md) - Flask integration for WTForms form handling with CSRF protection. _(Python)_
- [gpfjs](./gpfjs/on_boarding.md) - Angular frontend for GPF genomic and phenotypic data exploration. _(TypeScript)_
- [kivy](./kivy/on_boarding.md) - Open-source Python framework for cross-platform multi-touch GUI applications. _(Python)_
- [mangum](./mangum/on_boarding.md) - Adapter for running ASGI Python applications on AWS Lambda. _(Python)_
- [microdot](./microdot/on_boarding.md) - Minimalistic Python web framework for MicroPython and CPython servers. _(Python)_
- [nicegui](./nicegui/on_boarding.md) - Python framework for creating web-based user interfaces with minimal boilerplate. _(Python)_
- [paypal-js](./paypal-js/on_boarding.md) - React wrapper components for loading the PayPal JavaScript SDK. _(JavaScript)_
- [pyramid](./pyramid/on_boarding.md) - Flexible Python web framework scaling from small apps to large applications. _(Python)_
- [react](./react/on_boarding.md) - Declarative JavaScript library for building user interfaces with components. _(JavaScript)_
- [reflex](./reflex/on_boarding.md) - Pure-Python framework for building full-stack reactive web applications. _(Python)_
- [sanic](./sanic/on_boarding.md) - High-performance async Python web framework built for speed and extensibility. _(Python)_
- [spring-boot](./spring-boot/on_boarding.md) - Framework for building standalone production-grade Spring-based Java applications. _(Java)_
- [streamlit](./streamlit/on_boarding.md) - Python framework for quickly building interactive data apps and dashboards. _(Python)_
- [tornado](./tornado/on_boarding.md) - Python web framework and asynchronous networking library for high-concurrency. _(Python)_
- [tsoa](./tsoa/on_boarding.md) - TypeScript OpenAPI framework generating routes and specs from decorators. _(TypeScript)_
- [vue](./vue/on_boarding.md) - Progressive JavaScript framework for building reactive user interfaces. _(TypeScript)_
- [XgagSPA](./XgagSPA/on_boarding.md) - React single-page application displaying user posts and statistics. _(JavaScript)_

#### UI libraries & no-code

- [ant-design](./ant-design/on_boarding.md) - Enterprise-class React UI component library with consistent design language. _(TypeScript)_
- [carbon](./carbon/on_boarding.md) - IBM's Carbon design system React and web component library for enterprise UIs. _(JavaScript)_
- [CopilotKit](./CopilotKit/on_boarding.md) - React SDK for embedding in-app AI copilots, chatbots, and agents. _(TypeScript)_
- [CustomTkinter](./CustomTkinter/on_boarding.md) - Modern customizable widget library extending Python's tkinter GUI toolkit. _(Python)_
- [dash](./dash/on_boarding.md) - Plotly framework for building analytical web applications in pure Python. _(Python)_
- [deep-chat](./deep-chat/on_boarding.md) - Customizable chat component embedding AI conversations into any web application. _(TypeScript)_
- [formio](./formio/on_boarding.md) - API-driven platform for dynamic form building and data management. _(JavaScript)_
- [gradio](./gradio/on_boarding.md) - Python library to build web demos for machine learning models. _(Python)_
- [NodeGraphQt](./NodeGraphQt/on_boarding.md) - PyQt-based node graph framework for building visual programming interfaces. _(Python)_
- [PySimpleGUI](./PySimpleGUI/on_boarding.md) - Simplified wrapper creating GUIs across Tkinter, Qt and web frameworks. _(Python)_
- [Tkinter-Designer](./Tkinter-Designer/on_boarding.md) - Tool for converting Figma designs into Python Tkinter GUI code. _(Python)_
- [vuestic-admin](./vuestic-admin/on_boarding.md) - Open-source Vue 3 admin dashboard template with Vuestic UI components. _(TypeScript)_

#### Apps & platforms

- [appsmith](./appsmith/on_boarding.md) - Low-code platform for building internal tools, dashboards, and admin panels. _(TypeScript)_
- [arxiv-base](./arxiv-base/on_boarding.md) - Core Flask application infrastructure powering the arXiv preprint platform. _(Python)_
- [asgiref](./asgiref/on_boarding.md) - ASGI reference utilities bridging synchronous and asynchronous Python web code. _(Python)_
- [atlassian-connect-example-app-node](./atlassian-connect-example-app-node/on_boarding.md) - Example Atlassian Connect app with React frontend and Node.js Express backend. _(JavaScript)_
- [Caly](./Caly/on_boarding.md) - Avalonia-based cross-platform calendar desktop application using MVVM patterns. _(C#)_
- [cherrypy](./cherrypy/on_boarding.md) - Minimalist object-oriented Python web framework with built-in HTTP server. _(Python)_
- [claude-code-testing](./claude-code-testing/on_boarding.md) - Web application rendering markdown onboarding guides as interactive CodeBoarding docs. _(TypeScript)_
- [codeforlife-portal](./codeforlife-portal/on_boarding.md) - Django-based educational portal delivering coding lessons to students and teachers. _(Python)_
- [copyparty](./copyparty/on_boarding.md) - Self-hosted multi-protocol file server supporting HTTP, FTP, SMB, and more. _(Python)_
- [core](./core/on_boarding.md) - Home Assistant core home-automation platform integrating smart-home devices. _(Python)_
- [cvimprover-api](./cvimprover-api/on_boarding.md) - Django application that improves resumes using AI with Stripe-based payments. _(Python)_
- [dispatch](./dispatch/on_boarding.md) - Netflix's open-source security incident and case management platform. _(Python)_
- [dj-rest-auth](./dj-rest-auth/on_boarding.md) - Django REST framework package providing authentication and registration endpoints. _(Python)_
- [dj-stripe](./dj-stripe/on_boarding.md) - Django package syncing Stripe subscription and payment objects into local models. _(Python)_
- [django](./django/on_boarding.md) - High-level Python web framework encouraging rapid development and clean design. _(Python)_
- [django-anymail](./django-anymail/on_boarding.md) - Django email backend sending mail via multiple transactional ESP providers. _(Python)_
- [django-crm](./django-crm/on_boarding.md) - Modular Django customer relationship management application for leads and deals. _(Python)_
- [Django-facebook](./Django-facebook/on_boarding.md) - Django extension for Facebook OAuth login and user profile synchronization. _(Python)_
- [django-filer](./django-filer/on_boarding.md) - Django digital asset management app handling files, folders, and image metadata. _(Python)_
- [django-lifecycle](./django-lifecycle/on_boarding.md) - Django mixin adding declarative save/delete lifecycle hooks to ORM models. _(Python)_
- [django-modeltranslation](./django-modeltranslation/on_boarding.md) - Django extension enabling translation of model field content into multiple languages. _(Python)_
- [django-ninja](./django-ninja/on_boarding.md) - Fast Django web framework for building type-hinted REST APIs. _(Python)_
- [django-notifications](./django-notifications/on_boarding.md) - Django app providing a reusable GitHub-style user notifications framework. _(Python)_
- [django-postgres-docker-skeleton](./django-postgres-docker-skeleton/on_boarding.md) - Boilerplate Django project skeleton with PostgreSQL and Docker configuration. _(Python)_
- [django-react-typescript](./django-react-typescript/on_boarding.md) - Full-stack starter combining Django backend with React TypeScript frontend. _(Python)_
- [django-rest-framework](./django-rest-framework/on_boarding.md) - Powerful and flexible toolkit for building Web APIs with Django. _(Python)_
- [django-rules](./django-rules/on_boarding.md) - Tiny Django authorization library based on predicate rule composition. _(Python)_
- [django-tenant-schemas](./django-tenant-schemas/on_boarding.md) - Django app providing PostgreSQL-schema-based multi-tenancy for SaaS applications. _(Python)_
- [erpnext](./erpnext/on_boarding.md) - Open-source enterprise resource planning platform for managing businesses. _(Python)_
- [eShop](./eShop/on_boarding.md) - Reference microservices-based e-commerce sample application on .NET. _(C#)_
- [EShopMicroservices](./EShopMicroservices/on_boarding.md) - Microservices e-commerce reference with API gateway and event-driven services. _(C#)_
- [eShopOnAzure](./eShopOnAzure/on_boarding.md) - Azure-deployed microservices e-commerce reference application. _(C#)_
- [eShopOnWeb](./eShopOnWeb/on_boarding.md) - Monolithic ASP.NET Core e-commerce sample demonstrating clean architecture. _(C#)_
- [Fashion-Brand](./Fashion-Brand/on_boarding.md) - Static frontend website for a fashion brand with HTML, CSS, and JavaScript. _(HTML/JS)_
- [Flyerscord-Bot](./Flyerscord-Bot/on_boarding.md) - Discord bot application for the Philadelphia Flyers community. _(JavaScript)_
- [foodgram-project](./foodgram-project/on_boarding.md) - Dockerized web application for sharing recipes with Django backend and NGINX. _(Python)_
- [ForestBlog](./ForestBlog/on_boarding.md) - Java-based Spring MVC blog system with admin panel. _(Java)_
- [HR-SM](./HR-SM/on_boarding.md) - HR management web app with React frontend and Node.js/MongoDB backend. _(JavaScript)_
- [hrms](./hrms/on_boarding.md) - Open-source Frappe-based human resources management system. _(Python)_
- [jellyfin](./jellyfin/on_boarding.md) - Free open-source media server for streaming and managing personal media. _(C#)_
- [jovvix](./jovvix/on_boarding.md) - Polyglot interactive quiz application with web frontend and services. _(JavaScript)_
- [laudspeaker](./laudspeaker/on_boarding.md) - Open-source multichannel customer messaging and marketing automation platform. _(TypeScript)_
- [MayarDataScienceLab](./MayarDataScienceLab/on_boarding.md) - Static informational website for Mayar data science lab. _(HTML/JS)_
- [nest](./nest/on_boarding.md) - Progressive Node.js framework for building scalable server-side applications. _(TypeScript)_
- [obsidian-spaced-repetition](./obsidian-spaced-repetition/on_boarding.md) - Obsidian plugin for spaced repetition flashcard review over notes. _(TypeScript)_
- [OctoPrint](./OctoPrint/on_boarding.md) - Web interface for controlling, monitoring, and managing 3D printers. _(Python)_
- [odoo](./odoo/on_boarding.md) - Open source ERP and business application suite covering CRM, sales, inventory. _(Python)_
- [OpenUpgrade](./OpenUpgrade/on_boarding.md) - Framework for upgrading Odoo ERP deployments across major versions. _(Python)_
- [payload](./payload/on_boarding.md) - TypeScript-first headless CMS and application framework. _(TypeScript)_
- [pelican-plugins](./pelican-plugins/on_boarding.md) - Collection of plugins extending the Pelican static site generator. _(Python)_
- [PharmaSage](./PharmaSage/on_boarding.md) - Next.js pharma-themed web application with component-based architecture. _(TypeScript)_
- [quick-notes-extension](./quick-notes-extension/on_boarding.md) - Browser extension for taking and managing quick notes. _(JavaScript)_
- [RuoYi](./RuoYi/on_boarding.md) - Spring Boot admin dashboard system with role-based access control. _(Java)_
- [saleor](./saleor/on_boarding.md) - GraphQL-first headless e-commerce platform built with Django. _(Python)_
- [sdos-orchestration-flow-designer](./sdos-orchestration-flow-designer/on_boarding.md) - Visual flow designer for the SDOS orchestration platform with React frontend. _(TypeScript)_
- [snappass](./snappass/on_boarding.md) - Flask-based web application for sharing passwords and secrets with expiring URLs. _(Python)_
- [social-app-django](./social-app-django/on_boarding.md) - Django integration for python-social-auth providing social authentication flows. _(Python)_
- [StructureBlock](./StructureBlock/on_boarding.md) - Minecraft server management application with CLI and web GUI. _(?)_
- [synapse](./synapse/on_boarding.md) - Matrix homeserver reference implementation for decentralized real-time communication. _(Python)_
- [timetagger](./timetagger/on_boarding.md) - Tag-based time tracking web application for individuals and small teams. _(Python)_
- [warehouse](./warehouse/on_boarding.md) - Codebase powering the Python Package Index at pypi.org. _(Python)_
- [winboat](./winboat/on_boarding.md) - Electron desktop app running Windows VMs on Linux hosts. _(TypeScript)_
- [zulip](./zulip/on_boarding.md) - Open-source team chat application with threaded conversations and integrations. _(Python)_

### Infrastructure & DevOps

#### Configuration & automation

- [ansible](./ansible/on_boarding.md) - Agentless IT automation platform for configuration management and application deployment. _(Python)_
- [archinstall](./archinstall/on_boarding.md) - Guided installer automating Arch Linux setup with interactive and scripted modes. _(Python)_
- [AYABInterface](./AYABInterface/on_boarding.md) - Python library controlling AYAB-modified knitting machines over serial communication. _(Python)_
- [charmcraft](./charmcraft/on_boarding.md) - CLI tool for building, packaging, and publishing Juju charms and bundles. _(Python)_
- [dellemc-openmanage-ansible-modules](./dellemc-openmanage-ansible-modules/on_boarding.md) - Ansible collection automating Dell EMC server and iDRAC management tasks. _(Python)_
- [fabric](./fabric/on_boarding.md) - High-level Python library for SSH-based remote execution and deployment. _(Python)_
- [foxops](./foxops/on_boarding.md) - DevOps/GitOps automation tool for templating and managing infrastructure repositories. _(Python)_
- [irods_capability_automated_ingest](./irods_capability_automated_ingest/on_boarding.md) - Distributed asynchronous framework for automated iRODS data ingest. _(Python)_
- [kalico](./kalico/on_boarding.md) - 3D printer firmware host (Klipper fork) for microcontroller motion control. _(Python)_
- [nginxconfig.io](./nginxconfig.io/on_boarding.md) - Web tool for generating optimized NGINX and Docker Compose configurations. _(JavaScript)_
- [nornir](./nornir/on_boarding.md) - Pluggable Python network automation framework for multi-device orchestration. _(Python)_
- [sceptre](./sceptre/on_boarding.md) - CLI tool for managing and orchestrating AWS CloudFormation stacks. _(Python)_
- [stackstorm_pack_ansible](./stackstorm_pack_ansible/on_boarding.md) - StackStorm integration pack exposing Ansible operations as automation actions. _(Python)_
- [turborepo-remote-cache-cloudflare](./turborepo-remote-cache-cloudflare/on_boarding.md) - Turborepo remote cache implementation running on Cloudflare Workers. _(TypeScript)_
- [VertFlow](./VertFlow/on_boarding.md) - Airflow operator for running Cloud Run jobs across regions optimizing for green compute. _(Python)_

#### Observability & telemetry

- [datadogpy](./datadogpy/on_boarding.md) - Official Python client for Datadog metrics, events, and API interactions. _(Python)_
- [dd-agent](./dd-agent/on_boarding.md) - Datadog host agent collecting system and application metrics for monitoring. _(Python)_
- [dd-trace-py](./dd-trace-py/on_boarding.md) - Datadog APM Python tracer instrumenting applications with distributed traces. _(Python)_
- [django-prometheus](./django-prometheus/on_boarding.md) - Django library exporting application metrics in Prometheus format. _(Python)_
- [grafanalib](./grafanalib/on_boarding.md) - Python library for defining Grafana dashboards as code. _(Python)_
- [insights-core](./insights-core/on_boarding.md) - Red Hat framework for collecting and analyzing system data for insights. _(Python)_
- [logparser](./logparser/on_boarding.md) - Toolkit of automated log parsing algorithms for log analytics research. _(Python)_
- [logster](./logster/on_boarding.md) - Utility for reading log files and generating metrics for monitoring systems. _(Python)_
- [newrelic-python-agent](./newrelic-python-agent/on_boarding.md) - New Relic APM agent for instrumenting Python applications and collecting telemetry. _(Python)_
- [opentelemetry-go](./opentelemetry-go/on_boarding.md) - OpenTelemetry SDK and API for instrumenting Go applications with traces and metrics. _(Go)_
- [opentelemetry-python](./opentelemetry-python/on_boarding.md) - OpenTelemetry API and SDK for Python application observability instrumentation. _(Python)_
- [raven-python](./raven-python/on_boarding.md) - Legacy Sentry SDK for capturing Python application errors and events. _(Python)_
- [sentry-python](./sentry-python/on_boarding.md) - Official Sentry SDK for Python error tracking and performance monitoring. _(Python)_
- [simplemonitor](./simplemonitor/on_boarding.md) - Simple Python-based monitoring framework checking hosts and services with alerting. _(Python)_

#### Media & real-time infra

- [livekit](./livekit/on_boarding.md) - Open-source WebRTC SFU for scalable real-time audio, video, and data. _(Go)_

#### Platform SDKs

- [cluster-api](./cluster-api/on_boarding.md) - Kubernetes project providing declarative APIs and controllers for cluster lifecycle management. _(Go)_
- [docker-py](./docker-py/on_boarding.md) - Official Python SDK for interacting with the Docker Engine API. _(Python)_
- [localstack](./localstack/on_boarding.md) - Fully functional local AWS cloud stack for testing and development. _(Python)_
- [moby](./moby/on_boarding.md) - Container toolkit and runtime powering Docker and related projects. _(Go)_
- [nginx](./nginx/on_boarding.md) - High-performance HTTP server and reverse proxy with modular architecture. _(C)_
- [python-lambda](./python-lambda/on_boarding.md) - CLI tool for developing and deploying AWS Lambda functions. _(Python)_

### Developer tools

#### Package & environment management

- [cibuildwheel](./cibuildwheel/on_boarding.md) - CI tool building Python wheels for CPython and PyPy across many platforms. _(Python)_
- [pipenv](./pipenv/on_boarding.md) - Python dependency management tool combining pip and virtualenv workflows. _(Python)_
- [poetry](./poetry/on_boarding.md) - Modern Python packaging and dependency management tool. _(Python)_
- [poetry-multiproject-plugin](./poetry-multiproject-plugin/on_boarding.md) - Poetry plugin enabling monorepo-style multi-project workflows. _(Python)_
- [proxpi](./proxpi/on_boarding.md) - Caching proxy server for PyPI reducing package download latency. _(Python)_
- [pybuilder](./pybuilder/on_boarding.md) - Continuous build tool for Python projects with declarative configuration. _(Python)_

#### Language tooling (lint / types / format)

- [cloudpickle](./cloudpickle/on_boarding.md) - Extended pickle module serializing closures, lambdas, and dynamically-defined Python objects. _(Python)_
- [codon](./codon/on_boarding.md) - High-performance Python compiler using JIT and AOT to generate native code. _(C++)_
- [cuda-python](./cuda-python/on_boarding.md) - NVIDIA's official Python bindings for the CUDA driver and runtime APIs. _(Python)_
- [dacite](./dacite/on_boarding.md) - Small utility converting nested dictionaries into strongly-typed Python dataclasses. _(Python)_
- [deco](./deco/on_boarding.md) - Decorator-based automatic parallelization of Python functions via AST rewriting. _(Python)_
- [injector](./injector/on_boarding.md) - Python dependency injection framework inspired by Google Guice. _(Python)_
- [mypy](./mypy/on_boarding.md) - Static type checker for Python with a compiler for optimizing type-checked code. _(Python)_
- [pre-commit](./pre-commit/on_boarding.md) - Framework for managing and running multi-language pre-commit git hooks. _(Python)_
- [pyannotate](./pyannotate/on_boarding.md) - Auto-generates PEP 484 type annotations by observing Python runtime behavior. _(Python)_
- [pydantic](./pydantic/on_boarding.md) - Data validation library using Python type hints for runtime checking. _(Python)_
- [pyflakes](./pyflakes/on_boarding.md) - Lightweight passive Python source static analyzer for error detection. _(Python)_
- [python-betterproto](./python-betterproto/on_boarding.md) - Protobuf code generator producing modern idiomatic Python dataclasses and gRPC. _(Python)_
- [rope](./rope/on_boarding.md) - Python refactoring library providing AST-based code analysis and transformation. _(Python)_
- [ruff-lsp](./ruff-lsp/on_boarding.md) - Language server protocol wrapper for the Ruff Python linter and formatter. _(Python)_
- [shopify_python](./shopify_python/on_boarding.md) - Shopify Python style guide enforcement tools extending Pylint and AST utilities. _(Python)_
- [stm32-rs](./stm32-rs/on_boarding.md) - Generator for Rust peripheral access crates for STM32 microcontrollers. _(Rust)_
- [torchtyping](./torchtyping/on_boarding.md) - Runtime type annotations for PyTorch tensor shapes and dtypes. _(Python)_
- [typeguard](./typeguard/on_boarding.md) - Runtime type checker for Python function annotations using AST transformation. _(Python)_
- [TypeScript](./TypeScript/on_boarding.md) - Strongly typed programming language that builds on JavaScript with compile-time types. _(TypeScript)_
- [typescript-language-server](./typescript-language-server/on_boarding.md) - Language server protocol implementation for TypeScript and JavaScript. _(TypeScript)_
- [typeshed](./typeshed/on_boarding.md) - Collection of library stubs for Python used by type checkers like mypy. _(Python)_
- [voluptuous](./voluptuous/on_boarding.md) - Python data validation library with schema definition and compilation. _(Python)_
- [vscode-xslt-tokenizer](./vscode-xslt-tokenizer/on_boarding.md) - VS Code extension for XSLT and XPath syntax highlighting and language features. _(TypeScript)_
- [xed](./xed/on_boarding.md) - Intel x86 encoder decoder library and disassembler. _(C)_
- [zls](./zls/on_boarding.md) - Zig language server providing autocompletion and IDE features. _(Zig)_

#### CLIs, docs & DX

- [aiomultiprocess](./aiomultiprocess/on_boarding.md) - Asynchronous multiprocessing pool for running async tasks across worker processes. _(Python)_
- [amazing-qr](./amazing-qr/on_boarding.md) - Generator for artistic QR codes with custom images, GIFs, and colors. _(Python)_
- [argcomplete](./argcomplete/on_boarding.md) - Bash/zsh tab completion provider for Python argparse command-line programs. _(Python)_
- [bashplotlib](./bashplotlib/on_boarding.md) - Library for plotting basic histograms and scatterplots directly in the terminal. _(Python)_
- [blinker](./blinker/on_boarding.md) - Fast in-process signal/event dispatching library for decoupled Python applications. _(Python)_
- [cli](./cli/on_boarding.md) - Snyk's command-line interface for scanning code and dependencies for vulnerabilities. _(TypeScript)_
- [cobra](./cobra/on_boarding.md) - Go library for building modern CLI applications with nested commands and flags. _(Go)_
- [CodeBoarding-vscode](./CodeBoarding-vscode/on_boarding.md) - VSCode extension visualizing code architecture with control flow graph diagrams. _(TypeScript)_
- [cookiecutter](./cookiecutter/on_boarding.md) - CLI utility creating new projects from templated cookiecutter directories. _(Python)_
- [craft-application](./craft-application/on_boarding.md) - Framework for Canonical's craft-family CLI tools providing shared lifecycle scaffolding. _(Python)_
- [delegator.py](./delegator.py/on_boarding.md) - Simplified subprocess wrapper providing a friendly API for shell command execution. _(Python)_
- [delorean](./delorean/on_boarding.md) - Python library making timezone-aware datetime manipulation simpler and safer. _(Python)_
- [DirLink](./DirLink/on_boarding.md) - Command-line utility for creating and managing directory symlinks. _(Python)_
- [dive](./dive/on_boarding.md) - CLI tool exploring Docker image layers and analyzing wasted space. _(Go)_
- [drgn](./drgn/on_boarding.md) - Programmable debugger for introspecting the Linux kernel and user processes. _(Python)_
- [ebooklib](./ebooklib/on_boarding.md) - Python library for reading and writing EPUB ebook files. _(Python)_
- [eventsourcing](./eventsourcing/on_boarding.md) - Python library implementing the event sourcing pattern for domain-driven design. _(Python)_
- [ganda](./ganda/on_boarding.md) - Go CLI utility for making parallel HTTP requests from a URL list. _(Go)_
- [gaphor](./gaphor/on_boarding.md) - Simple yet powerful UML and SysML modeling application. _(Python)_
- [git-stacktrace](./git-stacktrace/on_boarding.md) - Tool that parses Python stack traces and maps them to git blame information. _(Python)_
- [gitdiagram](./gitdiagram/on_boarding.md) - Tool for generating interactive architecture diagrams from GitHub repositories. _(TypeScript)_
- [GitHubPoster](./GitHubPoster/on_boarding.md) - CLI tool to generate visual posters from GitHub and activity data. _(Python)_
- [Gooey](./Gooey/on_boarding.md) - Library that turns Python command-line programs into full GUI applications. _(Python)_
- [guietta](./guietta/on_boarding.md) - Simple Python library for declaratively creating PyQt GUIs in few lines. _(Python)_
- [gydnc](./gydnc/on_boarding.md) - CLI for managing guidance entities with storage and service layers. _(Go)_
- [hashids-python](./hashids-python/on_boarding.md) - Python library to generate short, unique, non-sequential IDs from numbers. _(Python)_
- [heartrate](./heartrate/on_boarding.md) - Real-time visualization of Python program execution in the browser. _(Python)_
- [holidays](./holidays/on_boarding.md) - Python library generating holiday dates for many countries and regions. _(Python)_
- [honcho](./honcho/on_boarding.md) - Python port of Foreman process manager for Procfile-based applications. _(Python)_
- [humanize](./humanize/on_boarding.md) - Python library for converting numbers, dates, and sizes to human-readable strings. _(Python)_
- [ipdb](./ipdb/on_boarding.md) - IPython-powered interactive Python debugger. _(Python)_
- [ipython](./ipython/on_boarding.md) - Enhanced interactive Python shell with rich display and magic commands. _(Python)_
- [itermplot](./itermplot/on_boarding.md) - Matplotlib backend that renders plots inline in iTerm2 terminals. _(Python)_
- [jupyterlab](./jupyterlab/on_boarding.md) - Next-generation web-based user interface for Project Jupyter notebooks. _(Python)_
- [KiKit](./KiKit/on_boarding.md) - KiCad automation tool for PCB panelization and manufacturing outputs. _(Python)_
- [knittingpattern](./knittingpattern/on_boarding.md) - Python library for parsing and converting knitting pattern DSL files. _(Python)_
- [loguru](./loguru/on_boarding.md) - Python logging library designed to be stupidly simple to use. _(Python)_
- [markitdown](./markitdown/on_boarding.md) - Microsoft CLI tool that converts documents and files to Markdown. _(Python)_
- [mkdocs](./mkdocs/on_boarding.md) - Static site generator geared towards building project documentation from Markdown. _(Python)_
- [mkdocstrings](./mkdocstrings/on_boarding.md) - MkDocs plugin for auto-generating API documentation from docstrings. _(Python)_
- [mtkclient](./mtkclient/on_boarding.md) - CLI and GUI client for flashing and interacting with MediaTek devices. _(Python)_
- [napi](./napi/on_boarding.md) - CLI framework built on yargs with middleware and manifest generation. _(TypeScript)_
- [notebook](./notebook/on_boarding.md) - Jupyter Notebook web application for interactive computing and data analysis. _(Python)_
- [Pipe](./Pipe/on_boarding.md) - Small Python library enabling fluent function composition through pipe operators. _(Python)_
- [poco](./poco/on_boarding.md) - Project management CLI for bootstrapping and managing multi-repo projects. _(Python)_
- [poethepoet](./poethepoet/on_boarding.md) - Task runner for Python projects configured via pyproject.toml. _(Python)_
- [posting](./posting/on_boarding.md) - Terminal-based HTTP client for API development and testing. _(Python)_
- [pyautogui](./pyautogui/on_boarding.md) - Cross-platform Python library for GUI automation of mouse and keyboard. _(Python)_
- [pydash](./pydash/on_boarding.md) - Functional utility library for Python inspired by lodash. _(Python)_
- [python-adb](./python-adb/on_boarding.md) - Pure Python ADB and Fastboot implementation for Android device communication. _(Python)_
- [python-fire](./python-fire/on_boarding.md) - Google library for automatically generating CLIs from Python objects. _(Python)_
- [python-nubia](./python-nubia/on_boarding.md) - Facebook framework for building interactive CLIs with REPL and autocomplete. _(Python)_
- [PyWhatKit](./PyWhatKit/on_boarding.md) - Python helper library for WhatsApp messaging and desktop automation tasks. _(Python)_
- [questionary](./questionary/on_boarding.md) - Python library for building interactive command line prompts and forms. _(Python)_
- [railroad-diagrams](./railroad-diagrams/on_boarding.md) - Library for generating SVG railroad diagrams from grammar definitions. _(Python)_
- [retrying](./retrying/on_boarding.md) - Python decorator library for adding configurable retry logic to functions. _(Python)_
- [rich](./rich/on_boarding.md) - Library for rich text and beautiful formatting in the terminal. _(Python)_
- [simplejson](./simplejson/on_boarding.md) - Simple fast extensible JSON encoder and decoder for Python. _(Python)_
- [terminal_markdown_viewer](./terminal_markdown_viewer/on_boarding.md) - Command-line tool for rendering markdown files beautifully in the terminal. _(Python)_
- [textual](./textual/on_boarding.md) - Python framework for building rich interactive terminal user interfaces. _(Python)_
- [tools](./tools/on_boarding.md) - Nextflow tooling for managing pipelines modules and subworkflows. _(Python)_
- [tqdm](./tqdm/on_boarding.md) - Fast extensible progress bar library for Python and command line. _(Python)_
- [tuna](./tuna/on_boarding.md) - Visualization tool for Python profile and import time data. _(Python)_
- [vscode](./vscode/on_boarding.md) - Microsoft Visual Studio Code source editor for modern web and cloud applications. _(TypeScript)_
- [wdb](./wdb/on_boarding.md) - Web-based remote Python debugger with real-time breakpoint interface. _(Python)_
- [XKCD-password-generator](./XKCD-password-generator/on_boarding.md) - CLI tool generating memorable passwords following the XKCD passphrase method. _(Python)_

#### Testing & load

- [appium](./appium/on_boarding.md) - Cross-platform mobile automation framework for testing native and web apps. _(JavaScript)_
- [AsyncFlow](./AsyncFlow/on_boarding.md) - Discrete-event simulation framework for modeling asynchronous request-response systems. _(Python)_
- [atheris](./atheris/on_boarding.md) - Coverage-guided fuzzing engine for Python with native extension instrumentation. _(Python)_
- [behave](./behave/on_boarding.md) - Behavior-driven development framework executing Gherkin feature files as tests. _(Python)_
- [chromeless](./chromeless/on_boarding.md) - Serverless headless Chrome automation running browser sessions on AWS Lambda. _(JavaScript)_
- [facebook-wda](./facebook-wda/on_boarding.md) - Python client for WebDriverAgent to automate iOS device UI testing. _(Python)_
- [hypothesis-torch](./hypothesis-torch/on_boarding.md) - Property-based testing extension for PyTorch models via Hypothesis. _(Python)_
- [IOS13-SimulateTouch](./IOS13-SimulateTouch/on_boarding.md) - iOS automation framework with Python client and on-device tweak for touch simulation. _(Python)_
- [locust](./locust/on_boarding.md) - Python load testing framework where users write scenarios as code. _(Python)_
- [openhtf](./openhtf/on_boarding.md) - Python framework for building scalable manufacturing hardware test automation. _(Python)_
- [optics-framework](./optics-framework/on_boarding.md) - Automated testing framework for building and running test suites. _(Python)_
- [perfplot](./perfplot/on_boarding.md) - Python micro-benchmarking library with automatic runtime plotting. _(Python)_
- [pytest](./pytest/on_boarding.md) - Plugin-driven Python testing framework for writing expressive tests. _(Python)_
- [pytest-xdist](./pytest-xdist/on_boarding.md) - Pytest plugin for distributed parallel test execution across workers. _(Python)_
- [python-client](./python-client/on_boarding.md) - Appium Python client for mobile application test automation via WebDriver. _(Python)_
- [requestium](./requestium/on_boarding.md) - Library merging Requests, Selenium, and Parsel for robust web scraping automation. _(Python)_
- [RIDE](./RIDE/on_boarding.md) - Robot Framework test data editor with a graphical user interface. _(Python)_
- [robotframework](./robotframework/on_boarding.md) - Generic open-source automation framework for acceptance testing and RPA. _(Python)_
- [scanapi](./scanapi/on_boarding.md) - Automated integration and contract testing tool for REST APIs using YAML specs. _(Python)_
- [selenium-wire](./selenium-wire/on_boarding.md) - Selenium extension adding request inspection and interception to browser automation. _(Python)_
- [testcontainers-python](./testcontainers-python/on_boarding.md) - Python library for running throwaway Docker containers during integration tests. _(Python)_
- [uiautomator2](./uiautomator2/on_boarding.md) - Python wrapper for Android UIAutomator2 enabling mobile UI automation and testing. _(Python)_
- [undetected-chromedriver](./undetected-chromedriver/on_boarding.md) - Patched Selenium ChromeDriver bypassing Cloudflare Distil and other bot detection. _(Python)_

### Scientific & research computing

#### Genomics & bioinformatics

- [aestetik](./aestetik/on_boarding.md) - Spatial transcriptomics analysis library using deep learning embeddings on tissue data. _(Python)_
- [AfterQC](./AfterQC/on_boarding.md) - Quality control and preprocessing tool for next-generation sequencing FASTQ data. _(Python)_
- [alphafold](./alphafold/on_boarding.md) - DeepMind protein structure prediction pipeline producing accurate 3D protein models. _(Python)_
- [alphagenome](./alphagenome/on_boarding.md) - Python SDK applying deep learning to genomics sequence and regulatory analysis. _(Python)_
- [anndata](./anndata/on_boarding.md) - Annotated data container for storing large single-cell gene expression datasets. _(Python)_
- [annofilter-junctions](./annofilter-junctions/on_boarding.md) - Bioinformatics pipeline annotating and filtering RNA-seq splice junction calls. _(Python)_
- [augur](./augur/on_boarding.md) - Bioinformatics pipeline toolkit for phylogenetic analysis of pathogen sequences. _(Python)_
- [BeadArrayFiles](./BeadArrayFiles/on_boarding.md) - Parser library for Illumina BeadArray BPM, cluster, and GTC genotyping files. _(Python)_
- [bigwig-loader](./bigwig-loader/on_boarding.md) - GPU-accelerated data loader for streaming BigWig genomic signal tracks into deep learning. _(Python)_
- [BioPhi](./BioPhi/on_boarding.md) - Web platform for antibody design, humanization, and humanness evaluation. _(Python)_
- [biopython](./biopython/on_boarding.md) - Comprehensive toolkit for computational biology, sequence analysis, and biological I/O. _(Python)_
- [CoSpred](./CoSpred/on_boarding.md) - Deep learning predictor of mass spectrometry spectra for peptide identification. _(Python)_
- [decima](./decima/on_boarding.md) - Neural network for analyzing gene expression and biological sequence data. _(Python)_
- [DeepSpot](./DeepSpot/on_boarding.md) - Spatial transcriptomics deep learning predictor from histology images. _(Python)_
- [deeptools](./deeptools/on_boarding.md) - Command-line suite for analyzing and visualizing high-throughput sequencing data. _(Python)_
- [digest](./digest/on_boarding.md) - High-performance ntHash bioinformatics sequence hashing library with Python bindings. _(C++)_
- [EFAAR_benchmarking](./EFAAR_benchmarking/on_boarding.md) - Benchmarking toolkit for evaluating biological perturbation representation methods. _(Python)_
- [enact-pipeline](./enact-pipeline/on_boarding.md) - Pipeline for processing and analyzing spatial transcriptomics data. _(Python)_
- [equifold](./equifold/on_boarding.md) - Machine learning pipeline for protein structure prediction and computational biology. _(Python)_
- [esm](./esm/on_boarding.md) - Protein language models for structure prediction and sequence embedding. _(Python)_
- [GearNet](./GearNet/on_boarding.md) - Deep learning framework for protein structure representation learning. _(Python)_
- [GeneAgent](./GeneAgent/on_boarding.md) - Self-verifying LLM agent for bioinformatics gene set analysis. _(Python)_
- [genie](./genie/on_boarding.md) - Deep learning framework for generative protein structure design. _(Python)_
- [genome-manager](./genome-manager/on_boarding.md) - Bioinformatics data management system with Nextflow workflow automation. _(Python)_
- [gnomAD_DB](./gnomAD_DB/on_boarding.md) - SQLite-backed database for querying gnomAD genomic variant data. _(Python)_
- [gpf](./gpf/on_boarding.md) - Genomic data management and analysis platform for genetics research. _(Python)_
- [gpf_flash](./gpf_flash/on_boarding.md) - Layered bioinformatics data platform for genomic and phenotypic data. _(Python)_
- [gpf_old](./gpf_old/on_boarding.md) - Legacy Genomic data management platform with web interface. _(Python)_
- [gpf_small](./gpf_small/on_boarding.md) - Scalable framework for managing and querying large-scale genomic variants. _(Python)_
- [gReLU](./gReLU/on_boarding.md) - Deep learning framework for biological sequence analysis and interpretation. _(Python)_
- [HLAIIPred](./HLAIIPred/on_boarding.md) - HLA class II peptide binding prediction tool for immunology research. _(Python)_
- [jump_hub](./jump_hub/on_boarding.md) - Biological data processing and analysis hub for JUMP Cell Painting. _(Python)_
- [KAZU](./KAZU/on_boarding.md) - Biomedical NLP framework for named entity recognition and ontology linking. _(Python)_
- [kipoiseq](./kipoiseq/on_boarding.md) - Standard dataloaders for genomic sequence and variant machine learning models. _(Python)_
- [LISTT](./LISTT/on_boarding.md) - CLI bioinformatics pipeline orchestrating external tools for genomic analysis. _(Python)_
- [MultiQC](./MultiQC/on_boarding.md) - Aggregates bioinformatics tool outputs into a single summary report. _(Python)_
- [Muon](./Muon/on_boarding.md) - Multi-omics data analysis framework built around the MuData object. _(Python)_
- [neusomatic](./neusomatic/on_boarding.md) - Deep learning-based somatic variant caller for long-read sequencing data. _(Python)_
- [nf-crispr-primer-design](./nf-crispr-primer-design/on_boarding.md) - Nextflow bioinformatics pipeline for designing primers for CRISPR experiments. _(Python)_
- [omnibenchmark](./omnibenchmark/on_boarding.md) - Framework for automating and standardizing benchmarking of bioinformatics tools. _(Python)_
- [openfold](./openfold/on_boarding.md) - Open-source PyTorch reimplementation of DeepMind's AlphaFold 2 protein prediction. _(Python)_
- [ProteinFlow](./ProteinFlow/on_boarding.md) - Pipeline for processing protein structure data for machine learning tasks. _(Python)_
- [PyDESeq2](./PyDESeq2/on_boarding.md) - Python implementation of DESeq2 for RNA-seq differential expression analysis. _(Python)_
- [pysam](./pysam/on_boarding.md) - Python interface to SAMtools for manipulating genomic sequencing files. _(Python)_
- [railroadtracks](./railroadtracks/on_boarding.md) - Framework for defining and executing bioinformatics workflows with provenance. _(Python)_
- [scanpy](./scanpy/on_boarding.md) - Scalable Python toolkit for single-cell gene expression data analysis. _(Python)_
- [scikit-bio](./scikit-bio/on_boarding.md) - Bioinformatics data structures, algorithms, and educational resources in Python. _(Python)_
- [scimilarity](./scimilarity/on_boarding.md) - Metric learning framework for single-cell RNA-seq similarity search and annotation. _(Python)_
- [scirpy](./scirpy/on_boarding.md) - Scanpy-based toolkit for single-cell T-cell and B-cell receptor repertoire analysis. _(Python)_
- [scispacy](./scispacy/on_boarding.md) - spaCy NLP models and pipelines for biomedical and scientific text processing. _(Python)_
- [scvi-tools](./scvi-tools/on_boarding.md) - Deep probabilistic models for single-cell omics data analysis. _(Python)_
- [seqlike](./seqlike/on_boarding.md) - Unified Python interface for biological sequence manipulation and analysis. _(Python)_
- [somaticseq](./somaticseq/on_boarding.md) - Ensemble pipeline combining somatic variant callers with machine learning classification. _(Python)_
- [spatialone-pipeline](./spatialone-pipeline/on_boarding.md) - Spatial transcriptomics pipeline for Visium platform data processing. _(Python)_
- [SRAgent](./SRAgent/on_boarding.md) - AI agent system for curating and retrieving Sequence Read Archive bioinformatics data. _(Python)_
- [starfish](./starfish/on_boarding.md) - Pipeline toolkit for image-based spatial transcriptomics analysis. _(Python)_

#### Imaging, neuroscience & health

- [AllenSDK](./AllenSDK/on_boarding.md) - Allen Institute SDK for accessing and analyzing neuroscience brain observatory data. _(Python)_
- [arviz](./arviz/on_boarding.md) - Exploratory analysis and visualization library for Bayesian statistical models. _(Python)_
- [bagel-cli](./bagel-cli/on_boarding.md) - CLI for annotating neuroimaging datasets with harmonized BIDS-compatible metadata. _(Python)_
- [BIC-megaplots](./BIC-megaplots/on_boarding.md) - Neuroimaging visualization tool producing composite megaplots from brain scan data. _(Python)_
- [cellpose](./cellpose/on_boarding.md) - Generalist deep learning model for segmenting cells in biomedical images. _(Python)_
- [DeepLabCut](./DeepLabCut/on_boarding.md) - Markerless animal pose estimation tool for neuroscience and behavioral research. _(Python)_
- [dipy](./dipy/on_boarding.md) - Python library for diffusion MRI analysis, tractography, and neuroimaging workflows. _(Python)_
- [fmriprep](./fmriprep/on_boarding.md) - Robust preprocessing pipeline for fMRI neuroimaging data following BIDS standards. _(Python)_
- [h5bench](./h5bench/on_boarding.md) - HDF5 I/O performance benchmarking suite for scientific computing. _(C)_
- [improver](./improver/on_boarding.md) - UK Met Office modular post-processing toolkit for meteorological forecasts. _(Python)_
- [iris](./iris/on_boarding.md) - Python library for analyzing and visualizing Earth science data. _(Python)_
- [lyse](./lyse/on_boarding.md) - Labscript suite analysis component for scientific experiment data. _(Python)_
- [MEA-NAP](./MEA-NAP/on_boarding.md) - MATLAB pipeline for microelectrode array neural activity analysis. _(MATLAB)_
- [medconb](./medconb/on_boarding.md) - GraphQL service for managing medical concepts, codelists, and phenotypes. _(Python)_
- [MedicalNet](./MedicalNet/on_boarding.md) - Pretrained 3D CNN models for medical image transfer learning. _(Python)_
- [mne-python](./mne-python/on_boarding.md) - Neuroscience library for MEG, EEG and neurophysiological signal analysis. _(Python)_
- [mouse-echo-neural-net](./mouse-echo-neural-net/on_boarding.md) - Desktop deep learning app for biomedical mouse echocardiography image analysis. _(Python)_
- [MS-lesion-segmentation](./MS-lesion-segmentation/on_boarding.md) - Deep learning pipeline for multiple sclerosis lesion segmentation in MRI. _(Python)_
- [neuro-forestwalk](./neuro-forestwalk/on_boarding.md) - Machine learning pipeline for behavioral phenotyping on HPC environments. _(Python)_
- [neuro-green](./neuro-green/on_boarding.md) - Deep learning research library for computational neuroscience applications. _(Python)_
- [neuro-meeglet-paper](./neuro-meeglet-paper/on_boarding.md) - Research code accompanying a neuroscience MEG/EEG wavelet analysis paper. _(Python)_
- [NiftyNet](./NiftyNet/on_boarding.md) - Deep learning platform for medical image analysis and research. _(Python)_
- [nilearn](./nilearn/on_boarding.md) - Scientific Python library for statistical learning on neuroimaging data. _(Python)_
- [nipype](./nipype/on_boarding.md) - Neuroimaging pipeline framework uniting heterogeneous analysis packages under one API. _(Python)_
- [ome-zarr-py](./ome-zarr-py/on_boarding.md) - Python library for reading and writing OME-Zarr bioimaging data format. _(Python)_
- [PhenEx](./PhenEx/on_boarding.md) - Defines and computes patient phenotypes and cohorts from clinical databases. _(Python)_
- [pvlib-python](./pvlib-python/on_boarding.md) - Scientific library for simulating photovoltaic energy system performance. _(Python)_
- [pybalance](./pybalance/on_boarding.md) - Causal inference matching library for balancing treatment and control groups. _(Python)_
- [PyHealth](./PyHealth/on_boarding.md) - Deep learning toolkit for healthcare predictive modeling on EHR data. _(Python)_
- [pymedphys](./pymedphys/on_boarding.md) - Medical physics toolkit for radiotherapy and diagnostic imaging calculations. _(Python)_
- [scikit-image](./scikit-image/on_boarding.md) - Collection of image processing algorithms for scientific Python applications. _(Python)_
- [sit2standpy](./sit2standpy/on_boarding.md) - Python library for detecting sit-to-stand transitions from wearable sensor data. _(Python)_
- [TotalSegmentator](./TotalSegmentator/on_boarding.md) - Deep learning tool for automatic segmentation of anatomical structures in CT scans. _(Python)_
- [WUCSS](./WUCSS/on_boarding.md) - Scientific pipeline for sleep state classification from physiological signals. _(Python)_

#### Molecular dynamics & chemistry

- [aizynthfinder](./aizynthfinder/on_boarding.md) - Retrosynthetic planning tool predicting synthesis routes for target molecules using AI. _(Python)_
- [beignet](./beignet/on_boarding.md) - Scientific computing library for molecular modeling, polynomials, and 3D rotations. _(Python)_
- [boltz](./boltz/on_boarding.md) - Diffusion-based molecular structure and binding affinity prediction model. _(Python)_
- [ccdutils](./ccdutils/on_boarding.md) - PDB Chemical Component Dictionary utilities for processing and analyzing small molecules. _(Python)_
- [ChEMBL_Structure_Pipeline](./ChEMBL_Structure_Pipeline/on_boarding.md) - Chemical structure standardization and validation pipeline used by ChEMBL. _(Python)_
- [chemicalx](./chemicalx/on_boarding.md) - PyTorch library for drug-drug interaction prediction using graph neural networks. _(Python)_
- [ConfGF](./ConfGF/on_boarding.md) - Score-based generative model for 3D molecular conformation generation. _(Python)_
- [ddi-designer](./ddi-designer/on_boarding.md) - Tool for designing drug-drug interaction studies in pharmacology research. _(Python)_
- [deep-molecular-optimization](./deep-molecular-optimization/on_boarding.md) - Deep generative models for optimizing molecular structures against target properties. _(Python)_
- [deepchem](./deepchem/on_boarding.md) - Machine learning library for drug discovery, materials, and quantum chemistry. _(Python)_
- [DeeplyTough](./DeeplyTough/on_boarding.md) - Deep learning comparison of protein binding pockets for drug discovery. _(Python)_
- [diffrax](./diffrax/on_boarding.md) - JAX library for numerical differential equation solvers with autodiff support. _(Python)_
- [drcHelper](./drcHelper/on_boarding.md) - R toolkit helping dose-response analyses in toxicology and pharmacology. _(R)_
- [geomstats](./geomstats/on_boarding.md) - Python library for computations and statistics on Riemannian manifolds. _(Python)_
- [insitro-research](./insitro-research/on_boarding.md) - Research code for molecular docking and predictive drug modeling. _(Python)_
- [mlr-xai-selfies](./mlr-xai-selfies/on_boarding.md) - Explainable AI for SELFIES-based molecular property prediction models. _(Python)_
- [mmpdb](./mmpdb/on_boarding.md) - Matched molecular pair database tool for cheminformatics and drug discovery. _(Python)_
- [MOCCA](./MOCCA/on_boarding.md) - Chromatographic data analysis framework for peak detection and deconvolution. _(Python)_
- [NonadditivityAnalysis](./NonadditivityAnalysis/on_boarding.md) - Tool for detecting non-additive structure-activity relationships in chemistry data. _(Python)_
- [openmc](./openmc/on_boarding.md) - Monte Carlo neutron and photon transport simulation code for nuclear physics. _(Python)_
- [psych.js](./psych.js/on_boarding.md) - JavaScript library for psychrometric calculations with interactive chart viewer. _(JavaScript)_
- [pyemma](./pyemma/on_boarding.md) - Molecular dynamics analysis library for Markov model estimation. _(Python)_
- [pymatgen](./pymatgen/on_boarding.md) - Materials science library for structure analysis and high-throughput computation. _(Python)_
- [PyPSA](./PyPSA/on_boarding.md) - Power system analysis toolbox for energy network optimization. _(Python)_
- [python-skyfield](./python-skyfield/on_boarding.md) - Astronomy library computing positions of stars, planets, and satellites. _(Python)_
- [rdkit](./rdkit/on_boarding.md) - Open-source cheminformatics library for molecular operations and drug discovery. _(C++)_
- [synflownet-boltz](./synflownet-boltz/on_boarding.md) - GFlowNet-based generative machine learning framework for chemistry design. _(Python)_
- [torsional-strain](./torsional-strain/on_boarding.md) - Computational chemistry workflow for calculating torsional strain in molecules. _(Python)_

### Security & privacy

#### App & supply-chain security

- [bandit](./bandit/on_boarding.md) - Static security linter finding common vulnerabilities in Python code via AST analysis. _(Python)_
- [bcrypt](./bcrypt/on_boarding.md) - Python bindings for the bcrypt password hashing algorithm with native speedups. _(Python)_
- [chainguard](./chainguard/on_boarding.md) - Lakera guardrails library adding prompt and response safety checks to LLMs. _(Python)_
- [credential-digger](./credential-digger/on_boarding.md) - Scanner that hunts for secrets and credentials in source code repositories. _(Python)_
- [django-axes](./django-axes/on_boarding.md) - Django middleware tracking failed login attempts and locking out attackers. _(Python)_
- [django-two-factor-auth](./django-two-factor-auth/on_boarding.md) - Pluggable two-factor authentication system for Django web applications. _(Python)_
- [fail2ban](./fail2ban/on_boarding.md) - Daemon that bans IPs after repeated authentication failures via log analysis. _(Python)_
- [garak](./garak/on_boarding.md) - LLM vulnerability scanner probing for prompt injection and content issues. _(Python)_
- [hpn-ssh](./hpn-ssh/on_boarding.md) - High-performance patched OpenSSH for high-bandwidth network transfers. _(C)_
- [jumpserver](./jumpserver/on_boarding.md) - Open-source bastion host for managing SSH, RDP, and database access. _(Python)_
- [lemur](./lemur/on_boarding.md) - TLS certificate management and lifecycle automation service from Netflix. _(Python)_
- [mcp-scan](./mcp-scan/on_boarding.md) - CLI that scans MCP server configurations and verifies entities against whitelists. _(Python)_
- [microsoft-authentication-library-for-python](./microsoft-authentication-library-for-python/on_boarding.md) - MSAL Python library for acquiring tokens from Microsoft identity platform. _(Python)_
- [Name-That-Hash](./Name-That-Hash/on_boarding.md) - CLI tool to identify hash types from unknown hash strings. _(Python)_
- [PMapper](./PMapper/on_boarding.md) - Graph-based tool for mapping and analyzing AWS IAM privilege escalation paths. _(Python)_
- [policy_sentry](./policy_sentry/on_boarding.md) - CLI for generating least-privilege AWS IAM policies from templates. _(Python)_
- [prowler](./prowler/on_boarding.md) - Cloud security assessment tool auditing AWS, Azure, GCP and Kubernetes. _(Python)_
- [pycasbin](./pycasbin/on_boarding.md) - Policy-based access control library supporting RBAC, ABAC and custom models. _(Python)_
- [python-tuf](./python-tuf/on_boarding.md) - Reference implementation of The Update Framework for secure software updates. _(Python)_
- [safe-chain](./safe-chain/on_boarding.md) - Security gateway for JavaScript and Python package managers blocking malicious dependencies. _(Python)_
- [safety](./safety/on_boarding.md) - Python dependency vulnerability scanner checking packages against security databases. _(Python)_
- [text_blind_watermark](./text_blind_watermark/on_boarding.md) - Text steganography library embedding invisible watermarks in strings. _(Python)_

#### Offensive / red team

- [Bashfuscator](./Bashfuscator/on_boarding.md) - Modular Bash script obfuscator for offensive security and red-team operations. _(Python)_
- [CobaltStrikeBeaconCppSource](./CobaltStrikeBeaconCppSource/on_boarding.md) - Leaked Cobalt Strike beacon C++ source code used for offensive security. _(C++)_
- [GhostTrack](./GhostTrack/on_boarding.md) - CLI tool for open-source intelligence gathering and tracking. _(Python)_
- [MHDDoS](./MHDDoS/on_boarding.md) - Python DDoS attack tool with many protocol methods. _(Python)_
- [pyrdp](./pyrdp/on_boarding.md) - Man-in-the-middle RDP proxy for session interception and analysis. _(Python)_
- [QBDI](./QBDI/on_boarding.md) - Dynamic binary instrumentation framework for reverse engineering and analysis. _(C++)_
- [rdpy](./rdpy/on_boarding.md) - Python RDP and VNC implementation for remote desktop protocol tools. _(Python)_
- [sulley](./sulley/on_boarding.md) - Fuzzing framework for discovering vulnerabilities in network protocols. _(Python)_
- [WhatWaf](./WhatWaf/on_boarding.md) - Tool detecting and identifying web application firewalls via payload fingerprinting. _(Python)_

### Games, graphics & media

#### Game engines & 3D

- [evennia](./evennia/on_boarding.md) - Python framework for building text-based multiplayer online games (MUDs). _(Python)_
- [g3m](./g3m/on_boarding.md) - Multi-platform 3D/4D geographic rendering and visualization engine. _(C++)_
- [openage](./openage/on_boarding.md) - Open-source clone of the Age of Empires II real-time strategy engine. _(C++)_
- [panda3d](./panda3d/on_boarding.md) - 3D game engine with Python bindings for interactive application development. _(C++)_
- [pygame](./pygame/on_boarding.md) - Python library for writing 2D games and multimedia applications. _(Python)_
- [pygame-menu](./pygame-menu/on_boarding.md) - Menu creation and management library for Pygame applications. _(Python)_
- [pyglet](./pyglet/on_boarding.md) - Cross-platform windowing and multimedia library for Python games. _(Python)_
- [pyrender](./pyrender/on_boarding.md) - Physically-based OpenGL renderer for 3D scenes and meshes in Python. _(Python)_
- [pyunity](./pyunity/on_boarding.md) - Python-based Unity-style 2D/3D game engine with scene management. _(Python)_
- [Quake-2](./Quake-2/on_boarding.md) - Classic Quake 2 game engine source code. _(C)_
- [sdf](./sdf/on_boarding.md) - Library for generating 3D meshes from signed distance functions. _(Python)_
- [Solitaire](./Solitaire/on_boarding.md) - Solitaire card game implementation. _(?)_
- [Sudoku](./Sudoku/on_boarding.md) - Sudoku puzzle generator and solver implementation. _(?)_
- [TA](./TA/on_boarding.md) - Game project component abstractions. _(?)_

#### Video, audio & downloaders

- [anime-downloader](./anime-downloader/on_boarding.md) - CLI tool for searching and downloading anime from various streaming sites. _(Python)_
- [moviepy](./moviepy/on_boarding.md) - Python library for video editing, compositing, and FFmpeg-based media processing. _(Python)_
- [pyo](./pyo/on_boarding.md) - Real-time digital signal processing and audio synthesis library. _(Python)_
- [resemble-enhance](./resemble-enhance/on_boarding.md) - Deep learning toolkit for audio denoising and speech enhancement. _(Python)_
- [sms-tools](./sms-tools/on_boarding.md) - Audio analysis and synthesis tools for sound and music computing. _(Python)_
- [soundconverter](./soundconverter/on_boarding.md) - GNOME application for converting audio files between formats. _(Python)_
- [spleeter](./spleeter/on_boarding.md) - Deezer source separation library for splitting audio into stems. _(Python)_
- [syncedlyrics](./syncedlyrics/on_boarding.md) - Command-line utility for fetching time-synced lyrics from multiple providers. _(Python)_
- [versatile_audio_super_resolution](./versatile_audio_super_resolution/on_boarding.md) - Deep learning pipeline for audio super-resolution and quality enhancement. _(Python)_
- [ykdl](./ykdl/on_boarding.md) - Command-line video downloader supporting multiple Chinese video platforms. _(Python)_
- [youtube-dl](./youtube-dl/on_boarding.md) - Command-line program for downloading videos from YouTube and other sites. _(Python)_
- [yt-dlp](./yt-dlp/on_boarding.md) - Feature-rich youtube-dl fork with additional patches and extractors. _(Python)_

#### Creative tooling

- [AliceLG](./AliceLG/on_boarding.md) - Blender add-on for rendering 3D scenes to Looking Glass holographic displays. _(Python)_
- [AmberLG](./AmberLG/on_boarding.md) - Blender add-on integrating holographic displays for Looking Glass light-field rendering. _(Python)_
- [blender-mcp](./blender-mcp/on_boarding.md) - MCP server letting Claude AI drive Blender for 3D model generation and manipulation. _(Python)_
- [ComfyUI](./ComfyUI/on_boarding.md) - Node-based graphical interface for designing and executing Stable Diffusion workflows. _(Python)_
- [ComfyUI-Easy-Use](./ComfyUI-Easy-Use/on_boarding.md) - ComfyUI extension packaging generative AI workflows into simpler user-friendly nodes. _(Python)_
- [GrooveScribe](./GrooveScribe/on_boarding.md) - Web-based single-page application for writing and practicing drum grooves. _(JavaScript)_
- [manim](./manim/on_boarding.md) - Programmatic animation engine for creating precise mathematical visualizations. _(Python)_
- [OCRmyPDF](./OCRmyPDF/on_boarding.md) - Adds OCR text layer to scanned PDFs for searchability and indexing. _(Python)_
- [opencv](./opencv/on_boarding.md) - Comprehensive computer vision and image processing library with ML utilities. _(C++)_
- [opencv-python](./opencv-python/on_boarding.md) - Python bindings for the OpenCV computer vision and image processing library. _(Python)_
- [PCV](./PCV/on_boarding.md) - Python computer vision toolkit with feature extraction and image processing pipelines. _(Python)_
- [PDFMathTranslate](./PDFMathTranslate/on_boarding.md) - Translates math-heavy PDF documents while preserving formulas and layout. _(Python)_
- [Pillow](./Pillow/on_boarding.md) - Friendly fork of PIL providing image processing capabilities for Python. _(Python)_
- [PyPDF2](./PyPDF2/on_boarding.md) - Pure Python library for reading, writing, and manipulating PDF files. _(Python)_
- [pytheory](./pytheory/on_boarding.md) - Python music theory library for tones, chords, and temperament systems. _(Python)_
- [word_cloud](./word_cloud/on_boarding.md) - Python library for generating word cloud visualizations from text. _(Python)_

### Networking, APIs & protocols

#### Platform SDKs & API clients

- [analytics-python](./analytics-python/on_boarding.md) - Segment analytics client library for tracking events from Python applications. _(Python)_
- [atlassian-python-api](./atlassian-python-api/on_boarding.md) - Python client covering Jira, Confluence, Bitbucket and other Atlassian product APIs. _(Python)_
- [besu](./besu/on_boarding.md) - Enterprise Ethereum blockchain client implementing execution and consensus layers. _(Java)_
- [bioblend](./bioblend/on_boarding.md) - Python client for the Galaxy and ToolShed bioinformatics platform APIs. _(Python)_
- [boto3](./boto3/on_boarding.md) - Official AWS SDK for Python providing high-level resource and client interfaces. _(Python)_
- [botocore](./botocore/on_boarding.md) - Low-level foundation library for boto3 handling AWS request signing and transport. _(Python)_
- [check-if-email-exists](./check-if-email-exists/on_boarding.md) - Service verifying whether an email address actually exists without sending mail. _(Rust)_
- [chembl_webresource_client](./chembl_webresource_client/on_boarding.md) - Python client for the ChEMBL bioactivity database REST web services. _(Python)_
- [cian-protocol](./cian-protocol/on_boarding.md) - Decentralized finance automation protocol for scheduled and conditional on-chain actions. _(Solidity)_
- [cloudant-python-sdk](./cloudant-python-sdk/on_boarding.md) - IBM Cloudant Python SDK for managing documents, databases, and change feeds. _(Python)_
- [clubhouse-py](./clubhouse-py/on_boarding.md) - Unofficial Python client for the Clubhouse social audio application API. _(Python)_
- [coinbase-python](./coinbase-python/on_boarding.md) - Official Coinbase Python API client for cryptocurrency exchange operations. _(Python)_
- [datahowlab-sdk-python](./datahowlab-sdk-python/on_boarding.md) - Python SDK for DataHowLab's bioprocess experiments, products, and models. _(Python)_
- [deep-translator](./deep-translator/on_boarding.md) - Unified Python wrapper around multiple online translation service APIs. _(Python)_
- [discord](./discord/on_boarding.md) - Python library for interacting with the Discord chat platform's API. _(Python)_
- [discord.py](./discord.py/on_boarding.md) - Full-featured async Python wrapper around the Discord bot API. _(Python)_
- [dropbox-sdk-python](./dropbox-sdk-python/on_boarding.md) - Official Dropbox Python SDK for file, sharing, and team operations. _(Python)_
- [facebook-python-business-sdk](./facebook-python-business-sdk/on_boarding.md) - Python SDK for Facebook Marketing API ad campaign management. _(Python)_
- [foxops-client-python](./foxops-client-python/on_boarding.md) - Python SDK client library for interacting with the Foxops API. _(Python)_
- [friendli-python](./friendli-python/on_boarding.md) - Python SDK for interacting with the Friendli LLM inference API. _(Python)_
- [g2papi](./g2papi/on_boarding.md) - CLI client for the Gene to Protein API retrieving biological data. _(Python)_
- [gkeepapi](./gkeepapi/on_boarding.md) - Unofficial Python client library for interacting with Google Keep. _(Python)_
- [gmail](./gmail/on_boarding.md) - Python IMAP-based library for reading and managing Gmail messages. _(Python)_
- [go-micro](./go-micro/on_boarding.md) - Go framework for building distributed microservices with pluggable components. _(Go)_
- [hangups](./hangups/on_boarding.md) - Third-party Python client for the Google Hangouts chat protocol. _(Python)_
- [inbox.py](./inbox.py/on_boarding.md) - Lightweight asynchronous Python SMTP server library for email processing. _(Python)_
- [invariant-sdk](./invariant-sdk/on_boarding.md) - Python SDK for interacting with the Invariant trace and dataset API. _(Python)_
- [itchatmp](./itchatmp/on_boarding.md) - Python framework for building WeChat public/enterprise platform bots. _(Python)_
- [jira](./jira/on_boarding.md) - Python client library for the Atlassian Jira REST API. _(Python)_
- [JobSpy](./JobSpy/on_boarding.md) - Job scraping library for LinkedIn, Indeed, Glassdoor, and similar boards. _(Python)_
- [magic-wormhole](./magic-wormhole/on_boarding.md) - Secure peer-to-peer file transfer CLI and library using short codes. _(Python)_
- [mailin](./mailin/on_boarding.md) - Event-driven SMTP server that parses incoming mail into structured data. _(JavaScript)_
- [mixpanel-python](./mixpanel-python/on_boarding.md) - Official Python client for sending events to the Mixpanel analytics API. _(Python)_
- [paysafe_sdk_python](./paysafe_sdk_python/on_boarding.md) - Python SDK for the Paysafe payment processing APIs. _(Python)_
- [pinterest-python-sdk](./pinterest-python-sdk/on_boarding.md) - Official Python SDK for the Pinterest API. _(Python)_
- [pixivpy](./pixivpy/on_boarding.md) - Python API wrapper for the Pixiv illustration sharing service. _(Python)_
- [praw](./praw/on_boarding.md) - Python Reddit API Wrapper for interacting with the Reddit platform. _(Python)_
- [PSpider](./PSpider/on_boarding.md) - Concurrent multithreaded web crawling framework for scraping content. _(Python)_
- [py-trello](./py-trello/on_boarding.md) - Python library for interacting with the Trello REST API. _(Python)_
- [pycoin](./pycoin/on_boarding.md) - Python toolkit for Bitcoin and cryptocurrency key, wallet, and transaction operations. _(Python)_
- [pycord](./pycord/on_boarding.md) - Modern Python API wrapper for interacting with the Discord platform. _(Python)_
- [PyGithub](./PyGithub/on_boarding.md) - Python library for accessing the GitHub REST API. _(Python)_
- [Pyrebase](./Pyrebase/on_boarding.md) - Python wrapper for Firebase Auth, Realtime Database and Storage APIs. _(Python)_
- [pyrh](./pyrh/on_boarding.md) - Unofficial Python interface to the Robinhood trading API. _(Python)_
- [pysnowball](./pysnowball/on_boarding.md) - Python wrapper for the Xueqiu (Snowball) stock market API. _(Python)_
- [python-asana](./python-asana/on_boarding.md) - Official Python client library for the Asana REST API. _(Python)_
- [python-bitcoinlib](./python-bitcoinlib/on_boarding.md) - Python library for the Bitcoin protocol, data structures, and RPC. _(Python)_
- [python-connector-api](./python-connector-api/on_boarding.md) - Python connector for the Meteomatics weather data API. _(Python)_
- [python-digitalocean](./python-digitalocean/on_boarding.md) - Python library for managing DigitalOcean cloud resources via the API. _(Python)_
- [python-facebook](./python-facebook/on_boarding.md) - Python client for Facebook Graph, Instagram and Threads APIs. _(Python)_
- [python-gitlab](./python-gitlab/on_boarding.md) - Python library for interacting with the GitLab REST API. _(Python)_
- [python-linode-api](./python-linode-api/on_boarding.md) - Python client library for the Linode cloud hosting API. _(Python)_
- [python-nomad](./python-nomad/on_boarding.md) - Python client library for interacting with HashiCorp Nomad clusters. _(Python)_
- [python-o365](./python-o365/on_boarding.md) - Python library for interacting with Microsoft Graph and Office 365 APIs. _(Python)_
- [python-sdk-core](./python-sdk-core/on_boarding.md) - Foundational SDK core for IBM Cloud service Python libraries. _(Python)_
- [python-slack-sdk](./python-slack-sdk/on_boarding.md) - Official Python SDK for building Slack apps and integrations. _(Python)_
- [python-telegram-bot](./python-telegram-bot/on_boarding.md) - Python wrapper for the Telegram Bot API with a dispatcher framework. _(Python)_
- [python-twitch-client](./python-twitch-client/on_boarding.md) - Python interface to the Twitch APIs (v5 and Helix). _(Python)_
- [python-user-agents](./python-user-agents/on_boarding.md) - Python library for parsing user agent strings into structured data. _(Python)_
- [python-zeep](./python-zeep/on_boarding.md) - Modern Python SOAP client for interacting with web services. _(Python)_
- [quandl-python](./quandl-python/on_boarding.md) - Python client library for retrieving financial and economic data from Quandl. _(Python)_
- [rauth](./rauth/on_boarding.md) - Python library for OAuth 1.0/2.0 authentication with service providers. _(Python)_
- [requests](./requests/on_boarding.md) - Elegant and simple HTTP library for making web requests in Python. _(Python)_
- [requests-cache](./requests-cache/on_boarding.md) - Transparent persistent HTTP caching layer for the Python requests library. _(Python)_
- [requests-ip-rotator](./requests-ip-rotator/on_boarding.md) - Rotates IPs via AWS API Gateway to bypass rate limits on scraping. _(Python)_
- [Riot-Watcher](./Riot-Watcher/on_boarding.md) - Python wrapper for Riot Games APIs covering League of Legends and other titles. _(Python)_
- [robin_stocks](./robin_stocks/on_boarding.md) - Unified Python interface for Robinhood, Gemini, and TD Ameritrade trading APIs. _(Python)_
- [scholarly](./scholarly/on_boarding.md) - Python module retrieving author and publication information from Google Scholar. _(Python)_
- [sendgrid-python](./sendgrid-python/on_boarding.md) - Official Python client library for the SendGrid email delivery service. _(Python)_
- [shopify_django_app](./shopify_django_app/on_boarding.md) - Django starter template for building Shopify embedded applications. _(Python)_
- [shopify_python_api](./shopify_python_api/on_boarding.md) - Python gem for authenticating and interacting with the Shopify admin API. _(Python)_
- [simple-salesforce](./simple-salesforce/on_boarding.md) - Simple REST client library for Salesforce REST, Bulk, and Metadata APIs. _(Python)_
- [slacker](./slacker/on_boarding.md) - Full-featured Python interface for the Slack API. _(Python)_
- [slackminion](./slackminion/on_boarding.md) - Modular plugin-based Python bot framework for Slack. _(Python)_
- [solana-py](./solana-py/on_boarding.md) - Python client library for interacting with the Solana blockchain. _(Python)_
- [spotify](./spotify/on_boarding.md) - Python client library interfacing with the Spotify Web API. _(Python)_
- [spotipy](./spotipy/on_boarding.md) - Lightweight Python library for interacting with the Spotify Web API. _(Python)_
- [square-python-sdk](./square-python-sdk/on_boarding.md) - Official Python SDK for integrating with Square payment APIs. _(Python)_
- [stripe-python](./stripe-python/on_boarding.md) - Official Stripe Python library for payment processing API integration. _(Python)_
- [susi_api_wrapper](./susi_api_wrapper/on_boarding.md) - Python wrapper client for the SUSI AI conversational assistant API. _(Python)_
- [target-python-sdk](./target-python-sdk/on_boarding.md) - Python SDK for Adobe Target personalization and A/B testing platform. _(Python)_
- [twarc](./twarc/on_boarding.md) - Command-line tool and Python library for archiving Twitter JSON data. _(Python)_
- [tweepy](./tweepy/on_boarding.md) - Python library for easy access to the Twitter API. _(Python)_
- [twilio-python](./twilio-python/on_boarding.md) - Official Twilio Python library for communications APIs. _(Python)_
- [twitter-api-client](./twitter-api-client/on_boarding.md) - Python implementation of the Twitter GraphQL and REST APIs. _(Python)_
- [vsphere-automation-sdk-python](./vsphere-automation-sdk-python/on_boarding.md) - Python SDK samples for VMware vSphere and VMware Cloud automation APIs. _(Python)_
- [web3.py](./web3.py/on_boarding.md) - Python library for interacting with Ethereum blockchain and smart contracts. _(Python)_
- [WebWhatsapp-Wrapper](./WebWhatsapp-Wrapper/on_boarding.md) - Pythonic automation wrapper for WhatsApp Web using Selenium. _(Python)_
- [xhs](./xhs/on_boarding.md) - Python library for interacting with Xiaohongshu Little Red Book platform. _(Python)_
- [yarl](./yarl/on_boarding.md) - Fast URL parsing and manipulation library for Python. _(Python)_
- [yfinance](./yfinance/on_boarding.md) - Python library for downloading historical market data from Yahoo Finance. _(Python)_
- [yfinance_depth_2](./yfinance_depth_2/on_boarding.md) - Extended Yahoo Finance data library with caching and multi-asset support. _(Python)_

#### Industrial & IoT protocols

- [cantools](./cantools/on_boarding.md) - CAN bus database tools for parsing DBC files and encoding automotive signals. _(Python)_
- [DJITelloPy](./DJITelloPy/on_boarding.md) - Python interface for controlling DJI Tello drones and coordinating swarms. _(Python)_
- [mavlink](./mavlink/on_boarding.md) - Lightweight drone communication protocol with multi-language code generation. _(C/Python)_
- [pymodbus](./pymodbus/on_boarding.md) - Full Modbus protocol implementation for industrial control systems. _(Python)_
- [pyserial](./pyserial/on_boarding.md) - Cross-platform Python library for serial port communication. _(Python)_
- [python-can](./python-can/on_boarding.md) - Python library for controller area network (CAN) bus communication. _(Python)_
- [python-opcua](./python-opcua/on_boarding.md) - Pure Python OPC UA client and server implementation for industrial automation. _(Python)_
- [scapy](./scapy/on_boarding.md) - Interactive packet manipulation library for network protocol forgery and analysis. _(Python)_

### Learning codebases

- [30-Days-Of-Python](./30-Days-Of-Python/on_boarding.md) - Progressive 30-day curriculum teaching foundational Python concepts step-by-step with exercises. _(Python)_
- [algo](./algo/on_boarding.md) - Collection of algorithm implementations and learning resources for practicing programming. _(Python)_
- [algorithms](./algorithms/on_boarding.md) - Minimal examples of classic data structures and algorithms implemented for learning. _(Python)_
- [annotated_deep_learning_paper_implementations](./annotated_deep_learning_paper_implementations/on_boarding.md) - Collection of annotated PyTorch implementations of deep learning research papers. _(Python)_
- [awesome-llm-apps](./awesome-llm-apps/on_boarding.md) - Curated collection of example LLM applications demonstrating agents and RAG patterns. _(Python)_
- [awesome-python](./awesome-python/on_boarding.md) - Curated awesome list of Python libraries, frameworks, and software resources. _(Python)_
- [basic_verilog](./basic_verilog/on_boarding.md) - Collection of basic Verilog HDL modules and templates for FPGA designers. _(Verilog)_
- [BayesERbook](./BayesERbook/on_boarding.md) - Tutorial book on Bayesian exposure-response modeling for pharmacometrics. _(R)_
- [BookWorm](./BookWorm/on_boarding.md) - Book-reading and annotation study project exploring text analysis techniques. _(Python)_
- [CleanArchitecture](./CleanArchitecture/on_boarding.md) - Reference .NET solution template demonstrating clean architecture patterns. _(C#)_
- [d2l-zh](./d2l-zh/on_boarding.md) - Chinese-language interactive deep learning textbook with runnable framework examples. _(Python)_
- [deep-learning-for-image-processing](./deep-learning-for-image-processing/on_boarding.md) - Tutorial repo of deep learning image classification and detection implementations. _(Python)_
- [funNLP](./funNLP/on_boarding.md) - Chinese NLP resource collection with dictionaries, corpora, and datasets. _(Python)_
- [hacking-tutorial](./hacking-tutorial/on_boarding.md) - Educational scripts demonstrating network hacking techniques like ARP and WEP. _(Python)_
- [Hello-Python](./Hello-Python/on_boarding.md) - Beginner Python course demonstrating basic syntax and arithmetic. _(Python)_
- [Java](./Java/on_boarding.md) - Collection of Java sample projects including JspChat, SpringBoot-Shiro, and eStore. _(Java)_
- [Jetpack-Compose-Tutorials](./Jetpack-Compose-Tutorials/on_boarding.md) - Android tutorial project demonstrating Jetpack Compose UI fundamentals. _(Kotlin)_
- [learn-python](./learn-python/on_boarding.md) - Progressive Python tutorial repository covering syntax to OOP. _(Python)_
- [Learning-Journal](./Learning-Journal/on_boarding.md) - Django tutorial app for creating topics and entries with authentication. _(Python)_
- [micrograd](./micrograd/on_boarding.md) - Tiny autograd engine and neural net library for educational purposes. _(Python)_
- [minGPT](./minGPT/on_boarding.md) - Minimal PyTorch re-implementation of GPT for educational clarity. _(Python)_
- [mlcourse.ai](./mlcourse.ai/on_boarding.md) - Open machine learning course with Jupyter notebook lessons. _(Python)_
- [public-apis](./public-apis/on_boarding.md) - Curated list of free public APIs organized for developer reference. _(?)_
- [python-archetype](./python-archetype/on_boarding.md) - Python clean architecture template repository with CQRS and DDD patterns. _(Python)_
- [python-guide](./python-guide/on_boarding.md) - Opinionated best-practices guide for Python developers. _(Python)_
- [python-mastery](./python-mastery/on_boarding.md) - David Beazley's advanced Python programming course materials. _(Python)_
- [python-mini-projects](./python-mini-projects/on_boarding.md) - Collection of small independent Python project scripts and applications. _(Python)_
- [python-template-repository](./python-template-repository/on_boarding.md) - Template scaffold for structuring new Python projects. _(Python)_
- [python-weekly](./python-weekly/on_boarding.md) - Weekly curated content pipeline aggregating Python news and articles. _(Python)_
- [pytorch-tutorial](./pytorch-tutorial/on_boarding.md) - Beginner-friendly PyTorch tutorial series covering deep learning fundamentals. _(Python)_
- [spinningup](./spinningup/on_boarding.md) - Educational resource for learning deep reinforcement learning algorithms from scratch. _(Python)_
- [stanford-tensorflow-tutorials](./stanford-tensorflow-tutorials/on_boarding.md) - Collection of TensorFlow tutorials and examples from Stanford CS20 course. _(Python)_
- [system-design-primer](./system-design-primer/on_boarding.md) - Educational resource teaching system design and object-oriented design patterns. _(Python)_

### Uncategorized

- [mole_public](./mole_public/on_boarding.md) - Undetermined repository with minimal architectural description. _(?)_
- [newton](./newton/on_boarding.md) - Undetermined repository with minimal architectural description. _(?)_
- [OhunIslam](./OhunIslam/on_boarding.md) - Undetermined repository with no architectural description available. _(?)_
- [OtakuWorld](./OtakuWorld/on_boarding.md) - Undetermined Android anime-related application with minimal description. _(?)_
- [pdc](./pdc/on_boarding.md) - Undetermined repository with no architectural description available. _(?)_
- [PerforatedAI](./PerforatedAI/on_boarding.md) - Undetermined repository with no architectural description available. _(?)_
- [phase1b](./phase1b/on_boarding.md) - Undetermined repository with no architectural description available. _(?)_
- [product-attribute](./product-attribute/on_boarding.md) - Undetermined repository, likely Odoo product attribute addons. _(?)_
- [products](./products/on_boarding.md) - Likely .NET identity server sample rather than Python project. _(?)_
- [python_testbench](./python_testbench/on_boarding.md) - Undetermined repository with no architectural description available. _(?)_
- [snd-textmod](./snd-textmod/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_
- [snipsnap](./snipsnap/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_
- [sparrow](./sparrow/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_
- [the-matrix](./the-matrix/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_
- [trailarr](./trailarr/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_
- [tsh](./tsh/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_
- [unit-converter](./unit-converter/on_boarding.md) - Unit conversion utility library. _(?)_
- [unleash](./unleash/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_
- [website](./website/on_boarding.md) - Unclassified repository with insufficient description to place in taxonomy. _(?)_


## How diagrams are generated

```mermaid
flowchart LR
    Code[Source Code] --> CB
    subgraph CB [CodeBoarding]
        direction LR
        Clone[Clone repo] --> Static[Static analysis] --> LLM[LLM reasoning]
    end
    CB --> MD[architecture.md]
```

Every diagram is produced by running [**CodeBoarding**](https://github.com/CodeBoarding/CodeBoarding) — a local static-analysis + LLM-reasoning engine — over the repo at `--depth-level 2`. The engine parses real imports, call graphs, and module boundaries; the LLM only names and summarizes. No diagram is hand-drawn.

## Contribute

**Found a mistake?** Static analysis + LLMs aren't perfect. If a module is misnamed or a dependency is invented, open a PR on the `.md`.

**Want your repo in here?** Open an issue with:
- the GitHub URL
- one sentence on what the repo does
- primary language

We prioritize repos that are (a) actively maintained, (b) widely depended on, or (c) architecturally interesting.

**Running this on your own code?** [CodeBoarding](https://codeboarding.com) runs locally. Point it at any repo, public or private.

## License

[MIT](./LICENSE). Copy the diagrams into your own `README.md`, `ARCHITECTURE.md`, or `AGENT.md`. No attribution required.
