```mermaid
graph LR
  subgraph 1["Frontend Controller & Lifecycle"]
    1__1_1["Page Controllers & Routing"]
    1__1_2["Client Lifecycle & Persistence"]
    1__1_3["Static Data Orchestrator"]
    1__1_3 -->|"Provides pre-fetched and transformed data as props to page components during the Next.js build/requ…"| 1__1_1
    1__1_1 -->|"The global application wrapper (_app.tsx) initializes and consumes lifecycle hooks to determine the…"| 1__1_2
  end
  subgraph 2["UI Component System"]
    2__2_1["Blog Content & Infrastructure"]
    2__2_2["Syntax Highlighting System"]
    2__2_3["Interactive UI Components"]
    2__2_1 -->|"Blog renderers invoke the Highlighter and Shell components to display code snippets within post con…"| 2__2_2
    2__2_1 -->|"Blog posts and footers utilize interactive elements like Notes, ExternalLinks, and Stats for enhanc…"| 2__2_3
    2__2_3 -->|"The Stats component may be embedded within blog navigation or footers to provide context-aware enga…"| 2__2_1
  end
  subgraph 3["Content Management System"]
    3__3_1["Content Schema & Registry"]
    3__3_2["Content-as-Code Implementations"]
    3__3_3["Blog Presentation Layer"]
    3__3_2 -->|"Inherits from and registers into"| 3__3_1
    3__3_3 -->|"Consumes registry and serialization for display"| 3__3_1
    3__3_2 -->|"Utilizes rich content helpers in render methods"| 3__3_3
  end
  subgraph 4["Serverless API & Integrations"]
    4__4_1["API Foundation & Core Utilities"]
    4__4_2["Public API Controllers"]
    4__4_3["Integration & Messaging Services"]
    4__4_2 -->|"Inherits the standardized request/response lifecycle and utilizes the shared context for session va…"| 4__4_1
    4__4_3 -->|"Uses the centralized error handling and validation schemas to process incoming form submissions sec…"| 4__4_1
  end
  subgraph 5["Monzo Financial Dashboard"]
    5__5_1["OAuth & Session Manager"]
    5__5_2["Server-Side Data Orchestrator"]
    5__5_3["Dashboard View"]
    5__5_1 -->|"Provides the necessary session credentials and JWT tokens required to authenticate requests to the …"| 5__5_2
    5__5_2 -->|"Supplies the structured, aggregated financial data (accounts, pots, balances) as React props for fi…"| 5__5_3
    5__5_3 -->|"calls"| 5__5_1
  end
  subgraph 6["Interactive Experiments"]
    6__6_1["Visual & Generative Sandbox"]
    6__6_2["Integration & Protocol Showcases"]
    6__6_1 -->|"provides the primary navigation hub for experiments and data parsing tools"| 6__6_1
    6__6_1 -->|"operates as a specialized extension of the experiments philosophy, sharing design language and layo…"| 6__6_2
    6__6_1 -->|"utilizes internal state-generation logic to drive visual components, separating complex math from r…"| 6__6_1
  end
  3 -->|"Provides static blog content and metadata for page generation."| 1
  4 -->|"Supplies dynamic data (e.g., Discord status, real-time stats) via client-side fetching."| 1
  1 -->|"Orchestrates layout and passes state/props to render the user interface."| 2
  4 -->|"Handles secure backend communication and authentication for financial data."| 5
  5 -->|"Utilizes the design system and specialized components for data visualization."| 2
  6 -->|"Leverages shared hooks and UI components for technical demonstrations."| 2
  2 -->|"calls"| 1
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

This architecture follows a modern Next.js pattern where a central Frontend Controller manages the application lifecycle and routing, orchestrating data from a static Content Management System and a dynamic Serverless API layer. The UI Component System provides a unified design language used across the main site, the Monzo Financial Dashboard, and various Interactive Experiments. Data flows from the Content and API layers into the Controllers, which then populate the UI components to render the final user experience, while specialized features like the Monzo dashboard maintain their own server-side data fetching logic.

### Frontend Controller & Lifecycle

Manages the high-level routing, page entry points, and client-side application state. It coordinates data fetching via Next.js lifecycle methods and tracks user persistence.

- **Page Controllers & Routing** — Acts as the primary entry point for all web requests, defining the layout and routing structure of the application.
- **Client Lifecycle & Persistence** — Manages client-side state that persists across sessions.
- **Static Data Orchestrator** — Handles the server-side logic for fetching and transforming content during the build process (SSG).

### UI Component System

The visual building blocks of the application, including reusable UI elements, blog-specific renderers, and syntax highlighters.

- **Blog Content & Infrastructure** — Manages the lifecycle of the blog, implementing the "Content-as-Code" pattern, including post registry, sorting/filtering logic, and navigational UI elements.
- **Syntax Highlighting System** — A specialized rendering engine for technical content, wrapping react-syntax-highlighter to provide consistent, themed code blocks with terminal simulations and file tabs.
- **Interactive UI Components** — Provides reusable, stateful UI elements like visit stats, animated message bubbles, and specialized links/notes, often integrating with custom hooks for animations or state.

### Content Management System

Implements the 'Content-as-Code' pattern, defining data structures for blog posts and handling the sorting and serialization of static content.

- **Content Schema & Registry** — Defines the foundational Post model and manages the lifecycle of all blog content, including serialization and registry orchestration.
- **Content-as-Code Implementations** — Contains individual blog post implementations as TypeScript classes that encapsulate their own logic and React render methods.
- **Blog Presentation Layer** — Responsible for the visual delivery of the blog, including navigation components and rich content helpers used by posts.

### Serverless API & Integrations

The backend layer of the monolithic repository, handling external API integrations (Discord, Apple Maps), OAuth flows, and contact form processing.

- **API Foundation & Core Utilities** — This component serves as the architectural backbone for all serverless operations.
- **Public API Controllers** — This component acts as the primary entry point for dynamic features and external authentication flows.
- **Integration & Messaging Services** — Dedicated to processing user-initiated communications, this component manages the flow of data from the site's contact form to external notification platforms.

### Monzo Financial Dashboard

A specialized, data-heavy feature that uses Server-Side Rendering (SSR) to fetch, format, and display financial transaction data.

- **OAuth & Session Manager** — Manages the security lifecycle of the Monzo integration, including OAuth 2.0 flow, token exchange, and JWT-based session persistence.
- **Server-Side Data Orchestrator** — Executes within the getServerSideProps lifecycle to fetch and aggregate financial data from the Monzo API for server-side rendering.
- **Dashboard View** — The presentation layer that renders aggregated financial data, handles currency formatting, and manages UI logic for different account types.

### Interactive Experiments

Isolated technical demonstrations and visual experiments, such as morphing shapes and OAuth demos, showcasing advanced frontend capabilities.

- **Visual & Generative Sandbox** — Manages the discovery and execution of visual experiments and local data processing tools.
- **Integration & Protocol Showcases** — Dedicated to functional demonstrations of third-party integrations.

