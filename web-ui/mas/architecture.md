```mermaid
graph LR
  subgraph 1["M@S Studio (Authoring Environment)"]
    1__1_1["Studio Shell & Navigation"]
    1__1_2["Authoring Interface & Editors"]
    1__1_3["Data Repository & AEM Integration"]
    1__1_4["Localization & Global Settings"]
    1__1_1 -->|"Activates specific editor views and passes fragment state"| 1__1_2
    1__1_2 -->|"Commits fragment updates and retrieves hydrated data models"| 1__1_3
    1__1_1 -->|"Queries fragment lists, folder hierarchies, and search results"| 1__1_3
    1__1_4 -->|"Orchestrates creation, retrieval, and status tracking of localized variations"| 1__1_3
    1__1_2 -->|"Consumes global settings and locale-specific overrides"| 1__1_4
  end
  subgraph 2["Edge Data Pipeline (BFF)"]
    2__2_1["Pipeline Orchestrator"]
    2__2_2["Translation Execution Engine"]
    2__2_3["Data Integration Layer"]
    2__2_4["BFF Data Provider"]
    2__2_1 -->|"Initiates asynchronous translation and rollout jobs."| 2__2_2
    2__2_2 -->|"Persists job progress and final project summaries to the state store."| 2__2_1
    2__2_2 -->|"Executes batch fragment updates and versioning requests against AEM/Odin."| 2__2_3
    2__2_4 -->|"Fetches raw fragment and offer data for enrichment and UI consumption."| 2__2_3
    2__2_1 -->|"Verifies user permissions and resource availability before starting projects."| 2__2_3
  end
  subgraph 3["Merchandising Web Components"]
    3__3_1["Merch Card Engine"]
    3__3_2["Hydration & CMS Bridge"]
    3__3_3["Collection Orchestrator"]
    3__3_4["Commerce & Identity Provider"]
    3__3_5["UI Building Blocks & Mapping"]
    3__3_2 -->|"Instantiates and populates Merch Card instances from AEM fragment data."| 3__3_1
    3__3_2 -->|"Consults fragment mapping logic to determine which component variant to instantiate for a given dat…"| 3__3_5
    3__3_1 -->|"Requests real-time price resolution and checkout link generation during the update lifecycle."| 3__3_4
    3__3_1 -->|"Incorporates specialized elements like mnemonic lists and secure transaction signals into its shado…"| 3__3_5
    3__3_3 -->|"Manages the visibility, filtering, and layout of multiple Merch Card instances within a unified con…"| 3__3_1
    3__3_1 -->|"calls"| 3__3_2
    3__3_3 -->|"calls"| 3__3_2
    3__3_5 -->|"calls"| 3__3_2
    3__3_5 -->|"calls"| 3__3_3
  end
  subgraph 4["AEM/EDS Delivery Integration"]
    4__4_1["EDS Delivery Pipeline & Lifecycle Orchestrator"]
    4__4_2["Content Discovery & Navigation Service"]
    4__4_1 -->|"triggers the initialization and decoration of during the Lazy phase of the page loading sequence"| 4__4_2
    4__4_1 -->|"provides the execution context and environment configuration that the service relies on to resolve …"| 4__4_2
  end
  subgraph 5["Quality & Maintenance Suite"]
    5__5_1["Functional Automation Engine"]
    5__5_2["Test Lifecycle & Hygiene Manager"]
    5__5_3["System Integrity & Performance Auditor"]
    5__5_4["Administrative & Maintenance Suite"]
    5__5_1 -->|"Delegates environment setup and post-run cleanup of generated test artifacts."| 5__5_2
    5__5_4 -->|"Synchronizes user data and environment state required for executing authenticated functional test s…"| 5__5_1
    5__5_3 -->|"Identifies data inconsistencies or performance bottlenecks in production that trigger administrativ…"| 5__5_4
    5__5_2 -->|"Provides performance metrics and request counts from functional runs to supplement dedicated perfor…"| 5__5_3
  end
  subgraph 6["Build & Development System"]
    6__6_1["Orchestrator & Lifecycle Manager"]
    6__6_2["Build Execution Engine"]
    6__6_3["Local Development Server"]
    6__6_4["Hot Reload Service"]
    6__6_1 -->|"Triggers new build tasks whenever the file watcher detects source code modifications."| 6__6_2
    6__6_1 -->|"Spawns and monitors the long-running web server process during the initial startup sequence."| 6__6_3
    6__6_1 -->|"Initializes the refresh server and sends broadcast signals after the Build Execution Engine complet…"| 6__6_4
  end
  1 -->|"Triggers translation and versioning jobs"| 2
  1 -->|"Uses components for content preview and editing"| 3
  2 -->|"Provides processed data models and fragments"| 3
  4 -->|"Loads and hydrates components in the delivery environment"| 3
  5 -->|"Validates authoring workflows via automated tests"| 1
  5 -->|"Performs visual and performance audits on components"| 3
  6 -->|"Orchestrates the compilation and bundling of the library"| 3
  3 -->|"calls"| 1
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The M@S (Merchandising-as-a-Service) architecture is a high-performance content delivery and management ecosystem built on the Adobe stack. It features a clear separation between the authoring environment (M@S Studio), the data processing pipeline (Edge Data Pipeline), and the presentation layer (Merchandising Web Components). Content is authored in the Studio using a standardized data model, processed and versioned through an asynchronous Edge pipeline, and delivered via Lit-based web components that are hydrated in the AEM/EDS environment for optimal performance.

### M@S Studio (Authoring Environment)

The central authoring interface where users manage merchandising content, edit fragments, and coordinate translations. It utilizes a rich text editor (ProseMirror) and manages complex state through a repository pattern and reactive stores.

- **Studio Shell & Navigation** — The primary application container and orchestration layer.
- **Authoring Interface & Editors** — The workspace for content manipulation, integrating rich text editing with specialized property editors for merchandising.
- **Data Repository & AEM Integration** — Implements the Repository Pattern for fragment CRUD operations, bulk publishing, and AEM integration.
- **Localization & Global Settings** — Manages content localization, translation workflows, and global merchandising configuration settings.

### Edge Data Pipeline (BFF)

A backend-for-frontend layer that handles heavy data operations, translation project lifecycles, and versioning locks. It transforms raw AEM data into standardized models consumed by both the Studio and the Web Components.

- **Pipeline Orchestrator** — Manages the lifecycle of translation projects from initiation to completion.
- **Translation Execution Engine** — The core processing unit that executes translation and rollout logic.
- **Data Integration Layer** — Provides a standardized abstraction for interacting with external AEM and Odin services.
- **BFF Data Provider** — Tailors raw AEM data for the Studio UI.

### Merchandising Web Components

A library of Lit-based web components (cards, prices, buttons) used to render merchandising content. It integrates with commerce services (WCS) and handles hydration of static content for performance.

- **Merch Card Engine** — The core rendering engine for individual merchandising units.
- **Hydration & CMS Bridge** — Responsible for the "hydration" of server-rendered or static HTML into interactive web components.
- **Collection Orchestrator** — Manages groups of Merch Cards, providing high-level features such as filtering, sorting, and search.
- **Commerce & Identity Provider** — Handles integration with external Adobe services (WCS and IMS).
- **UI Building Blocks & Mapping** — Contains standalone UI elements (mnemonics, secure transaction icons) and the mapping logic that bridges AEM data structures to specific component implementations.

### AEM/EDS Delivery Integration

Integration scripts and blocks for Adobe Experience Manager (AEM) and Edge Delivery Services (EDS). It manages the delivery context, decorates blocks, and ensures components are correctly loaded in the production environment.

- **EDS Delivery Pipeline & Lifecycle Orchestrator** — Manages the Edge Delivery Services (EDS) page lifecycle, orchestrating the transition from initial request to fully interactive page.
- **Content Discovery & Navigation Service** — Responsible for generating the site's navigational structure by interacting with the EDS content index.

### Quality & Maintenance Suite

Automated testing frameworks (Nala/Playwright) and maintenance scripts for auditing data health, refreshing users, and validating system integrity across the Studio and Web Components.

- **Functional Automation Engine** — The core execution engine for end-to-end testing, combining low-level browser interaction utilities with high-level Page Objects.
- **Test Lifecycle & Hygiene Manager** — Manages the global state and observability of the functional test suite.
- **System Integrity & Performance Auditor** — A suite of tools focused on the health of the delivered content.
- **Administrative & Maintenance Suite** — A collection of operational scripts used for routine system maintenance.

### Build & Development System

Infrastructure for the development environment, including build orchestration with esbuild, file watching, and local development servers for the component library.

- **Orchestrator & Lifecycle Manager** — The central controller of the development environment.
- **Build Execution Engine** — Responsible for executing the transformation of source code into distributable web components.
- **Local Development Server** — A persistent background process that hosts the component library and documentation locally.
- **Hot Reload Service** — Provides real-time browser synchronization.

