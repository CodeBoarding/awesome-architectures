```mermaid
graph LR
  subgraph 1["Compiler Core & Taglib Infrastructure"]
    1__1_1["Compiler Orchestrator & Parser"]
    1__1_2["Taglib Discovery & Resolution"]
    1__1_3["AST Transformation & Migration"]
    1__1_4["Environment Integration & Registration"]
    1__1_5["Translator & Runtime Target Interface"]
    1__1_6["Internal Build Tooling"]
    1__1_4 -->|"Triggers the compilation process when a .marko file is required or imported in a Node.js environmen…"| 1__1_1
    1__1_1 -->|"Queries the lookup mechanism during parsing to identify whether a tag is a native HTML element or a…"| 1__1_2
    1__1_1 -->|"Passes the initial AST to the transformation engine to apply Marko-specific logic and optimizations."| 1__1_3
    1__1_3 -->|"Retrieves metadata for custom tags to guide the transformation process."| 1__1_2
    1__1_3 -->|"Generates code that instantiates runtime components and records static dependencies discovered duri…"| 1__1_5
    1__1_1 -->|"Uses target-specific configurations to determine whether to generate code for HTML streaming or VDO…"| 1__1_5
  end
  subgraph 2["Legacy Translator (Class API)"]
    2__2_1["Class API Generator"]
    2__2_2["Legacy Tag & Expression Translator"]
    2__2_3["Static Content Optimizer"]
    2__2_3 -->|"Provides static analysis metadata used to generate optimized VDOM instructions for tags and text bl…"| 2__2_2
    2__2_2 -->|"Supplies the translated JavaScript logic and render function body to be embedded within the final c…"| 2__2_1
    2__2_1 -->|"Triggers the optimization pass during the initial phase of the class generation to determine the st…"| 2__2_3
  end
  subgraph 3["Legacy Runtime (VDOM & SSR)"]
    3__3_1["SSR & Streaming Engine"]
    3__3_2["Component Runtime & Lifecycle"]
    3__3_3["VDOM & DOM Reconciliation"]
    3__3_4["Hydration & State Serialization"]
    3__3_1 -->|"Embeds serialized component state and initialization metadata into the outgoing HTML stream."| 3__3_4
    3__3_4 -->|"Provides the initial state and configuration required to instantiate and hydrate components on the …"| 3__3_2
    3__3_2 -->|"Triggers VDOM diffing and DOM morphing when component state changes occur."| 3__3_3
    3__3_3 -->|"Invokes lifecycle hooks (like onMount or onUpdate) after the physical DOM has been successfully pat…"| 3__3_2
    3__3_1 -->|"Triggers initial server-side render logic and manages the execution of components within the stream…"| 3__3_2
  end
  subgraph 4["Modern Translator (Tags API)"]
    4__4_1["Static Analysis Engine"]
    4__4_2["Reactive Signal Generator"]
    4__4_3["Template Transformation Orchestrator"]
    4__4_4["Target-Specific Code Generator"]
    4__4_5["API Interop Layer"]
    4__4_6["Asset & Build Integration"]
    4__4_3 -->|"Initiates the pre-analysis phase and reference tracking during AST traversal to build the dependenc…"| 4__4_1
    4__4_1 -->|"Provides the finalized reference and section metadata required to generate reactive signals and sco…"| 4__4_2
    4__4_3 -->|"Injects generated signals and scope accessors into the transformed AST to enable runtime reactivity."| 4__4_2
    4__4_3 -->|"Delegates the final emission of code to target-specific visitors based on whether the output is for…"| 4__4_4
    4__4_5 -->|"Wraps the modern translator logic to allow legacy components to be processed within the new Tags AP…"| 4__4_3
    4__4_4 -->|"Triggers the resolution of external assets, such as CSS files, during the final code generation pha…"| 4__4_6
    4__4_1 -->|"calls"| 4__4_3
    4__4_1 -->|"calls"| 4__4_4
    4__4_2 -->|"calls"| 4__4_1
    4__4_2 -->|"calls"| 4__4_3
    4__4_2 -->|"calls"| 4__4_4
    4__4_4 -->|"calls"| 4__4_1
    4__4_4 -->|"calls"| 4__4_2
    4__4_4 -->|"calls"| 4__4_3
  end
  subgraph 5["Modern Runtime (Signals & Hydration)"]
    5__5_1["SSR & Streaming Engine"]
    5__5_2["Hydration & Resumption Bridge"]
    5__5_3["Reactive Signal Engine"]
    5__5_4["DOM Interaction Layer"]
    5__5_5["Runtime Metadata & Types"]
    5__5_1 -->|"Invokes the Serializer to encode component state and hydration markers into the streaming HTML outp…"| 5__5_2
    5__5_2 -->|"The _resume process decodes server-provided state to instantiate reactive scopes and initialize sig…"| 5__5_3
    5__5_3 -->|"Schedules fine-grained updates that are applied to the DOM via attribute and text mutation utilitie…"| 5__5_4
    5__5_4 -->|"Controllable form elements capture user input and propagate changes back into the signal system to …"| 5__5_3
    5__5_5 -->|"Provides the type definitions and tag metadata required for server-side template rendering."| 5__5_1
    5__5_5 -->|"Defines the structure of reactive inputs and scopes used by the signal runtime."| 5__5_3
    5__5_1 -->|"calls"| 5__5_3
    5__5_1 -->|"calls"| 5__5_4
    5__5_2 -->|"calls"| 5__5_1
    5__5_3 -->|"calls"| 5__5_2
    5__5_4 -->|"calls"| 5__5_1
  end
  6["Framework Build Tooling"]
  1 -->|"Provides the parsed AST and resolved tag metadata required for Class-API code generation."| 2
  1 -->|"Provides the parsed AST and metadata for reactive signal analysis and Tags-API transformation."| 4
  2 -->|"Generates code that targets the VDOM engine and AsyncStream for rendering."| 3
  4 -->|"Generates reactive signals and hydration metadata that the modern runtime executes."| 5
  6 -->|"Post-processes the runtime source code to optimize variable scoping and inject debug symbols."| 5
  5 -->|"calls"| 4
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

Marko's architecture is defined by a sophisticated build-time compiler that bridges the gap between high-level template syntax and optimized runtime execution. The Compiler Core serves as the central orchestrator, utilizing a Taglib System to resolve components and a Babel-based parser to generate an Abstract Syntax Tree (AST). Depending on the component style used, the flow bifurcates: the Legacy Class-API Pipeline transforms templates into VDOM-based render functions for the Legacy Runtime, while the Modern Tags-API Pipeline performs deep static analysis to generate fine-grained reactive "signals" for the Modern Runtime. This dual-path architecture allows Marko to provide a seamless transition from traditional VDOM rendering to a modern, signal-based reactive model with optimized partial hydration.

### Compiler Core & Taglib Infrastructure

The entry point for the Marko compilation process. It handles template parsing, manages the Taglib lookup mechanism for component discovery, and provides the shared Babel transformation infrastructure used by all translators.

- **Compiler Orchestrator & Parser** — The entry point for the compilation process, managing the MarkoFile state and using a Babel-based parser to convert Marko template syntax into a traversable AST.
- **Taglib Discovery & Resolution** — Scans the file system for marko.json definitions and custom components, building a TaglibLookup structure for resolving tag names.
- **AST Transformation & Migration** — Implements core logic for manipulating the Marko AST, including Babel visitors for attribute directives, syntax migration, and static analysis.
- **Environment Integration & Registration** — Handles integration into the execution environment, including Node.js require hooks, hot-reloading, and source map management.
- **Translator & Runtime Target Interface** — Bridges the compiler and runtime, providing dependency analysis utilities and defining target structures for HTML or VDOM generation.
- **Internal Build Tooling** — Internal scripts and utilities for maintaining infrastructure, such as generating TypeScript definitions from Babel types and managing package field overrides.

### Legacy Translator (Class API)

A specialized translation layer for Marko 4/5 (Class API). it converts template structures into JavaScript classes and VDOM-compatible render functions, applying optimizations for static content.

- **Class API Generator** — Serves as the primary orchestrator for the translation process, defining the structural skeleton of the generated JavaScript component and transforming template-level class blocks and lifecycle declarations into a formal class definition.
- **Legacy Tag & Expression Translator** — Handles the granular translation of Marko-specific tags and legacy syntax patterns, bridging the gap between the declarative template language and the imperative JavaScript required by the Class API.
- **Static Content Optimizer** — Implements performance-critical optimizations by analyzing the template's AST to identify and mark static nodes for optimized VDOM creation paths.

### Legacy Runtime (VDOM & SSR)

The execution engine for Class-API components. It manages the component lifecycle, handles server-side HTML streaming via AsyncStream, and performs client-side DOM updates using a VDOM morphing algorithm.

- **SSR & Streaming Engine** — Manages the asynchronous generation and flushing of HTML from the server to the client.
- **Component Runtime & Lifecycle** — The central management unit for component instances.
- **VDOM & DOM Reconciliation** — Provides the Virtual DOM infrastructure and the reconciliation logic used for client-side updates.
- **Hydration & State Serialization** — Facilitates the transfer of component state and metadata from the server to the client.

### Modern Translator (Tags API)

The advanced compiler for Marko 6 (Tags API). It performs sophisticated data-flow analysis to track variable references and template sections, generating reactive bindings instead of traditional VDOM logic.

- **Static Analysis Engine** — The "brain" of the translator; it performs data-flow analysis to identify variable references, create bindings, and organize the template into logical sections for reactive updates.
- **Reactive Signal Generator** — Translates static analysis metadata into executable runtime instructions, generating the "signals" and scope accessors that replace Virtual DOM diffing logic.
- **Template Transformation Orchestrator** — Manages the structural transformation of the Marko AST, orchestrating the traversal and dispatching translation tasks for control flow and custom tags.
- **Target-Specific Code Generator** — Adapts the translation output for specific environments (DOM vs.
- **API Interop Layer** — Facilitates the coexistence of the legacy Class API (Marko 5) and the new Tags API (Marko 6) by detecting features and merging translator visitors.
- **Asset & Build Integration** — Handles peripheral compiler tasks such as resolving associated style files and providing utilities for build-time size and performance analysis.

### Modern Runtime (Signals & Hydration)

A high-performance reactive runtime that uses a "Signal" system for fine-grained DOM updates. It includes a specialized serializer for efficient partial hydration, allowing the client to resume state from server-rendered HTML without re-rendering.

- **SSR & Streaming Engine** — Manages the server-side rendering lifecycle, focusing on streaming HTML generation and asynchronous fragment management.
- **Hydration & Resumption Bridge** — Acts as the link between server and client.
- **Reactive Signal Engine** — The core reactive runtime that manages the dependency graph between data and UI.
- **DOM Interaction Layer** — Provides low-level utilities for mutating the browser DOM.
- **Runtime Metadata & Types** — A collection of TypeScript definitions and metadata that define the contract between the compiler and the runtime, ensuring type safety for HTML tags and Marko-specific templates.

### Framework Build Tooling

Internal build-time utilities and plugins used to manage the Marko monorepo. These tools handle tasks like declaration hoisting and debug instrumentation during the framework's own build process.

