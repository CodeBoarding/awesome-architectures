```mermaid
graph LR
  subgraph 1["CLI & Orchestration"]
    1__1_1["CLI Controller & Orchestrator"]
    1__1_2["Configuration Management"]
    1__1_3["Analysis Execution Engine"]
    1__1_4["Batch Processing Pipeline"]
    1__1_1 -->|"Queries the registry to identify which metrics and patterns are active for the current analysis run."| 1__1_2
    1__1_1 -->|"Dispatches file-level analysis tasks to the engine to generate ASTs and extract feature vectors."| 1__1_3
    1__1_4 -->|"Leverages the core AST and metric extraction logic for bulk processing of large code datasets."| 1__1_3
    1__1_2 -->|"Provides the metadata and parameter definitions required to instantiate and execute specific analys…"| 1__1_3
  end
  subgraph 2["AST Framework"]
    2__2_1["AST Core Model"]
    2__2_2["AST Factory & Parser"]
    2__2_3["Dynamic Property Engine"]
    2__2_4["Semantic Context Provider"]
    2__2_5["Analysis Engine"]
    2__2_2 -->|"Parses source code to instantiate and populate the structural AST."| 2__2_1
    2__2_1 -->|"ASTNode delegates attribute access to the registry for resolving computed fields."| 2__2_3
    2__2_1 -->|"Provides the structural tree used as input for scope extraction and CFG generation."| 2__2_4
    2__2_1 -->|"Provides the primary API (traversal, subtrees) for metrics and patterns."| 2__2_5
    2__2_4 -->|"Supplies lexical and flow context for complex pattern detection."| 2__2_5
    2__2_3 -->|"Provides high-level computed properties (e.g., methods, fields) used by analysis logic."| 2__2_5
    2__2_4 -->|"calls"| 2__2_1
    2__2_5 -->|"calls"| 2__2_1
  end
  subgraph 3["Static Analysis Engine"]
    3__3_1["Pattern Detection Engine"]
    3__3_2["Structural Metrics Engine"]
    3__3_3["Lexical Analysis Engine"]
    3__3_1 -->|"share the same AST traversal context and proxy nodes"| 3__3_2
    3__3_2 -->|"provide complementary feature sets (structural vs. textual) that are aggregated into a unified nume…"| 3__3_3
    3__3_2 -->|"calls"| 3__3_1
  end
  subgraph 4["ML Intelligence & Ranking"]
    4__4_1["Model Training & Lifecycle"]
    4__4_2["Statistical Analysis & Preprocessing"]
    4__4_3["Predictive Ranking Engine"]
    4__4_1 -->|"uses preprocessing logic to scale and normalize datasets before fitting the model"| 4__4_2
    4__4_1 -->|"orchestrates the training process that populates the internal regressor used by the ranking engine"| 4__4_3
    4__4_3 -->|"utilizes scaling functions during the inference phase to ensure input features match the training d…"| 4__4_2
    4__4_2 -->|"calls"| 4__4_3
  end
  subgraph 5["Data Engineering & Training Pipeline"]
    5__5_1["Source Code Sanitizer"]
    5__5_2["External Metrics Orchestrator"]
    5__5_3["Pattern Analysis Engine"]
    5__5_4["Data Synthesis & Splitter"]
    5__5_1 -->|"Provides the filtered list of valid Java source files for metric calculation."| 5__5_2
    5__5_1 -->|"Provides the filtered list of Java source files for internal pattern detection."| 5__5_3
    5__5_2 -->|"Supplies CSV files containing external static analysis metrics for integration."| 5__5_4
    5__5_3 -->|"Supplies CSV files containing internal pattern detection results for integration."| 5__5_4
    5__5_1 -->|"Passes the initial file-level split configuration to ensure consistent train/test separation across…"| 5__5_4
    5__5_2 -->|"calls"| 5__5_1
    5__5_2 -->|"calls"| 5__5_3
    5__5_3 -->|"calls"| 5__5_2
    5__5_4 -->|"calls"| 5__5_3
  end
  1 -->|"Initiates parsing of source files into AST objects."| 2
  2 -->|"Provides the navigable tree structure required for pattern matching and metric calculation."| 3
  3 -->|"Supplies the feature vectors (pattern counts and metric values) for scoring."| 4
  4 -->|"Returns ranked recommendations and impact scores for final reporting."| 1
  5 -->|"Produces the trained model weights and parameters used during the inference phase."| 4
  5 -->|"Utilizes the engine to extract features from large-scale datasets during the training phase."| 3
  1 -->|"calls"| 3
  1 -->|"calls"| 4
  3 -->|"calls"| 1
  3 -->|"calls"| 2
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The aibolit architecture follows a sophisticated ML-augmented Static Analysis Pipeline. The process begins with the CLI & Orchestration component, which manages configuration and triggers the AST Framework to parse Java source code into an enriched, navigable tree. This tree is then consumed by the Static Analysis Engine, which executes a suite of deterministic pattern detectors and complexity metrics to extract a high-dimensional feature vector. These features are passed to the ML Intelligence & Ranking component, where a pre-trained model scores and prioritizes the findings based on their predicted impact on code quality. Finally, the results are funneled back to the orchestrator for report generation. A separate Data Engineering & Training Pipeline exists to handle large-scale repository processing and model retraining, ensuring the tool's recommendations remain relevant.

### CLI & Orchestration

Acts as the system's brain and primary interface. It handles user input, manages global configuration, and orchestrates the sequential execution of parsing, analysis, and ranking. It is also responsible for formatting the final output into human-readable or machine-parsable reports (XML/Text).

- **CLI Controller & Orchestrator** — The primary entry point and execution manager.
- **Configuration Management** — Acts as the system's registry and metadata repository.
- **Analysis Execution Engine** — The functional core responsible for the transformation of source code into structured data.
- **Batch Processing Pipeline** — A set of auxiliary scripts designed for high-volume data processing tasks, such as calculating Halstead metrics or Ranking Scores (RS) for dataset preparation, complementing the main CLI tool.

### AST Framework

Provides the structural foundation for analysis by wrapping javalang to create an improved, queryable Abstract Syntax Tree (AST). It includes specialized logic for class decomposition, scope management, and Control Flow Graph (CFG) generation, allowing other components to traverse code structures efficiently.

- **AST Core Model** — Defines the fundamental data structures (AST, ASTNode) and navigation logic.
- **AST Factory & Parser** — Responsible for converting raw Java source code into the framework's internal AST representation.
- **Dynamic Property Engine** — An extensibility mechanism that allows for the registration and dynamic resolution of computed fields on AST nodes.
- **Semantic Context Provider** — Enriches the structural AST with semantic information, including lexical scope hierarchies and Control Flow Graphs (CFGs), to support advanced analysis patterns.
- **Analysis Engine** — The consumer layer of the framework, consisting of metrics and pattern detectors that utilize the AST and its semantic enrichments to identify code smells and calculate features.

### Static Analysis Engine

A modular engine implementing the Strategy pattern to detect "anti-patterns" and calculate software metrics. It traverses the AST to identify specific code smells (e.g., Null Assignment, Classic Getters) and computes complexity scores (Cyclomatic, Cognitive, NPath), transforming code into a numerical feature set.

- **Pattern Detection Engine** — Implements the Strategy pattern to identify discrete "anti-patterns" in the code.
- **Structural Metrics Engine** — Calculates quantitative measures of code complexity and internal class cohesion.
- **Lexical Analysis Engine** — Extracts features from the raw text and token stream of the source code.

### ML Intelligence & Ranking

The predictive core of the tool. It takes the raw features produced by the Static Analysis Engine and applies machine learning models (regressors) to rank identified patterns. It uses mathematical scoring to determine which code improvements should be prioritized for the developer.

- **Model Training & Lifecycle** — Manages the end-to-end offline process of creating the ranking models, including dataset collection, environment setup, and the execution of the training process.
- **Statistical Analysis & Preprocessing** — Provides the analytical foundation for the subsystem, handling data transformation tasks like scaling and normalization, and performing impact analysis.
- **Predictive Ranking Engine** — The runtime core that implements the mathematical scoring logic, exposing the primary API for inference and applying the trained model to rank patterns.

### Data Engineering & Training Pipeline

A suite of utilities designed for offline operations. It manages parallel processing of large Java datasets, filters source files, and extracts features at scale to facilitate the training and refinement of the ranking models.

- **Source Code Sanitizer** — Responsible for the initial ingestion and sanitization of the Java dataset.
- **External Metrics Orchestrator** — Manages the execution of external static analysis tools to enrich the feature set.
- **Pattern Analysis Engine** — The core feature extraction component that identifies specific code patterns using Aibolit's internal AST framework.
- **Data Synthesis & Splitter** — Finalizes the pipeline by merging CSV outputs from all extraction engines into a master dataset.

