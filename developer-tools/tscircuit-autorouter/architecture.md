```mermaid
graph LR
  subgraph 1["Pipeline Orchestration Engine"]
    1__1_1["Pipeline Orchestration & State Management"]
    1__1_2["Spatial Infrastructure & Topology Engine"]
    1__1_3["Global Pathfinding & Port Optimization"]
    1__1_4["Detailed Routing & Constraint Solvers"]
    1__1_1 -->|"Initializes the spatial context, obstacle trees, and initial net connectivity (MST)"| 1__1_2
    1__1_1 -->|"Triggers the high-level pathfinding sequence across the generated mesh"| 1__1_3
    1__1_1 -->|"Triggers local refinement, via placement, and high-density intra-node solving"| 1__1_4
    1__1_2 -->|"Provides the capacity mesh graph and net-to-point pair definitions required for A* pathfinding"| 1__1_3
    1__1_3 -->|"Passes the sequence of nodes and optimized port point coordinates that define the local routing bou…"| 1__1_4
    1__1_4 -->|"Updates the mesh with final trace geometry and utilizes stitching solvers to merge fragmented segme…"| 1__1_2
  end
  subgraph 2["Algorithmic Solver Core"]
    2__2_1["Port & Constraint Pre-processor"]
    2__2_2["Hypergraph Pathfinding Engine"]
    2__2_3["Topological Unraveling & HD Solver"]
    2__2_4["Layer Transition & Via Manager"]
    2__2_5["Geometric Refinement & Stitcher"]
    2__2_1 -->|"Provides validated start/end points and spatial constraints for path calculation."| 2__2_2
    2__2_2 -->|"Passes initial path segments for resolution of crossings in high-density areas."| 2__2_3
    2__2_2 -->|"Requests via placement or jumper patterns when planar routing is blocked."| 2__2_4
    2__2_3 -->|"Sends resolved, untangled trace segments for final geometric simplification."| 2__2_5
    2__2_4 -->|"Provides via coordinates and layer-jump points to be integrated into the final trace geometry."| 2__2_5
  end
  subgraph 3["Spatial & Geometric Foundation"]
    3__3_1["Spatial Infrastructure & Topological Analysis"]
    3__3_2["Route Transformation & Geometric Utilities"]
    3__3_1 -->|"constrains geometric calculations and pathing logic of"| 3__3_2
    3__3_1 -->|"transforms raw geometric points into structured route data based on constraints from"| 3__3_2
  end
  subgraph 4["Benchmarking & Performance Suite"]
    4__4_1["Parallel Execution Engine"]
    4__4_2["Benchmarking & Profiling Orchestrator"]
    4__4_3["Scenario Management"]
    4__4_4["Validation & DRC Tooling"]
    4__4_3 -->|"Supplies filtered datasets and test scenarios for bulk performance evaluation."| 4__4_2
    4__4_3 -->|"Supplies specific scenarios for targeted debugging and individual sample execution."| 4__4_4
    4__4_2 -->|"Dispatches routing tasks to the worker pool for concurrent execution across multiple CPU cores."| 4__4_1
    4__4_2 -->|"Utilizes DRC validation logic and error location utilities to determine the success rate and correc…"| 4__4_4
  end
  subgraph 5["Experimental Tuning & Debugging"]
    5__5_1["Tuning Orchestrator"]
    5__5_2["Parallel Test Runner"]
    5__5_3["Result Manager & Aggregator"]
    5__5_1 -->|"Dispatches generated parameter schedules and configuration strings for execution in isolated enviro…"| 5__5_2
    5__5_2 -->|"Streams solver performance metrics, JSON-formatted logs, and process exit codes for persistence and…"| 5__5_3
  end
  1 -->|"Orchestrates the execution of specific routing algorithms and solvers in a defined sequence."| 2
  1 -->|"Initializes and manages the spatial context, including obstacle and capacity trees, for the routing…"| 3
  2 -->|"Utilizes spatial indexing and geometric utilities to perform collision detection and path calculati…"| 3
  4 -->|"Executes routing pipelines against various scenarios to measure performance and success rates."| 1
  5 -->|"Runs specific pipeline configurations to reproduce bugs and optimize solver parameters."| 1
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The `tscircuit-autorouter` architecture is organized as a multi-stage pipeline that transforms high-level routing requirements into precise geometric traces. The system centers on a Pipeline Orchestration Engine that sequences specialized Algorithmic Solvers (handling pathing, via placement, and density) while leveraging a Spatial & Geometric Foundation for efficient collision detection and mathematical utilities. This core logic is supported by a Benchmarking & Performance Suite for regression testing and an Experimental Tuning & Debugging layer for resolving complex edge cases and optimizing solver parameters.

### Pipeline Orchestration Engine

The central entry point and management layer that defines and executes routing pipelines. It handles input validation, initializes global state, and sequences the execution of specialized solvers.

- **Pipeline Orchestration & State Management** — The central control layer that receives routing requests, validates inputs, and sequences the execution of various solvers.
- **Spatial Infrastructure & Topology Engine** — Responsible for the physical-to-logical mapping of the PCB.
- **Global Pathfinding & Port Optimization** — Determines the high-level routes for nets across the capacity mesh.
- **Detailed Routing & Constraint Solvers** — Executes the final, detailed routing within individual capacity nodes, particularly in high-density areas.

### Algorithmic Solver Core

A collection of specialized solvers that implement deep routing logic, including capacity-based pathing, high-density trace generation, and jumper/via placement strategies.

- **Port & Constraint Pre-processor** — Manages the spatial distribution of ports and handles "cramped" scenarios where port placement is highly restricted, ensuring uniform entry/exit points for the pathfinder.
- **Hypergraph Pathfinding Engine** — The primary engine for determining signal movement across the PCB mesh using hypergraph abstractions and capacity-based pathing logic.
- **Topological Unraveling & HD Solver** — Resolves complex intersections and trace crossings in high-density routing corridors by breaking problems into sections and untangling them.
- **Layer Transition & Via Manager** — Evaluates and places vias or jumper patterns to facilitate transitions between different PCB layers or to bypass obstacles.
- **Geometric Refinement & Stitcher** — Consolidates route fragments and simplifies jagged algorithmic paths into geometrically valid 45-degree PCB traces.

### Spatial & Geometric Foundation

Provides the mathematical and spatial infrastructure for the router. It manages obstacle detection via spatial trees and provides geometric utilities for 45-degree pathing and intersection checks.

- **Spatial Infrastructure & Topological Analysis** — Manages spatial indexing and the analysis of geometric relationships between segments and nodes.
- **Route Transformation & Geometric Utilities** — Provides geometric utility functions for path construction and handles the conversion of internal route representations.

### Benchmarking & Performance Suite

Infrastructure for performance testing and validation. It includes worker pools for parallel execution of routing scenarios and tools for measuring DRC success and execution time.

- **Parallel Execution Engine** — Manages the lifecycle of worker processes for high-density routing tasks.
- **Benchmarking & Profiling Orchestrator** — Coordinates large-scale test runs and fine-grained performance analysis.
- **Scenario Management** — Responsible for loading, filtering, and sorting PCB routing datasets (scenarios).
- **Validation & DRC Tooling** — Executes individual routing samples and performs Design Rule Checks (DRC) to ensure geometric validity.

### Experimental Tuning & Debugging

Specialized tools for investigating specific bug reports and fine-tuning solver parameters. It performs parameter sweeps and focused searches to optimize routing schedules for difficult cases.

- **Tuning Orchestrator** — Defines the experimental search space and generates combinatorial parameter schedules.
- **Parallel Test Runner** — Manages the lifecycle of individual solver tests executed in isolated child processes.
- **Result Manager & Aggregator** — Responsible for collecting, sorting, and persisting the results of experimental runs.

