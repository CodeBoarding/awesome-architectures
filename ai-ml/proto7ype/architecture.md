```mermaid
graph LR
  subgraph 1["Global Layout & Navigation Shell"]
    1__1_1["Global Structural Shell"]
    1__1_2["Navigation & Routing Shell"]
    1__1_3["Landing & Feature Orchestrator"]
    1__1_1 -->|"Mounts the persistent header and provides the global layout context for navigation elements."| 1__1_2
    1__1_1 -->|"Injects the landing page content into the main layout slot via the React children pattern."| 1__1_3
    1__1_2 -->|"Facilitates user navigation to the home route and provides the interactive links that trigger featu…"| 1__1_3
  end
  subgraph 2["Game Arcade System"]
    2__2_1["Arcade Discovery Interface"]
    2__2_2["Dynamic Game Controller"]
    2__2_3["Arcade Integration Bridge"]
    2__2_1 -->|"Triggers navigation to specific game routes based on user selection from the catalog."| 2__2_2
    2__2_2 -->|"Passes the resolved game slug and configuration parameters to the embedder for execution."| 2__2_3
  end
  subgraph 3["XR/3D Rendering Engine"]
    3__3_1["Lifecycle Orchestrator"]
    3__3_2["Asset Pipeline"]
    3__3_3["Animation Engine"]
    3__3_4["XR & Environment Controller"]
    3__3_1 -->|"Triggers the asynchronous fetching of 3D models and textures"| 3__3_2
    3__3_1 -->|"Initializes and starts the requestAnimationFrame loop"| 3__3_3
    3__3_2 -->|"Supplies loaded animation clips to the mixers"| 3__3_3
    3__3_3 -->|"Updates dynamic lighting intensities and shader uniforms"| 3__3_4
    3__3_4 -->|"Configures the renderer's XR session state and applies environmental lighting"| 3__3_1
  end
  subgraph 4["Business Conversion Module"]
    4__4_1["Request Arcade Presentation Layer"]
    4__4_2["Inquiry Processing Engine"]
    4__4_1 -->|"Embeds and provides visual context for the inquiry form within the page layout."| 4__4_2
    4__4_2 -->|"Reports submission status (success/error) to trigger UI state changes in the parent container."| 4__4_1
  end
  1 -->|"Routes user to game gallery and specific game instances."| 2
  1 -->|"Triggers the immersive 3D experience route."| 3
  1 -->|"Directs potential clients to the inquiry form."| 4
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The application architecture is structured around a central Global Layout & Navigation Shell that orchestrates user flow to specialized functional modules, including a Game Arcade System for interactive content, an XR/3D Rendering Engine for immersive visual experiences, and a Business Conversion Module for lead generation. The purpose of this design is to provide a cohesive, themed user experience while decoupling core navigation from specific feature-rich interactive and business-oriented services.

### Global Layout & Navigation Shell

This component serves as the application's structural foundation and primary entry point. It manages the global state, persistent navigation, and the "Arcade-Rave" visual theme (neon pulses, glitch effects) that defines the user experience. It acts as the central router, dispatching users to specific feature modules.

- **Global Structural Shell** — Establishes the foundational HTML/Body structure and identity of the application.
- **Navigation & Routing Shell** — Manages user movement and interactive navigation.
- **Landing & Feature Orchestrator** — Orchestrates the primary entry point and visual storytelling of the application.

### Game Arcade System

The core interactive hub of the site, responsible for game discovery and execution. It utilizes a dynamic routing pattern to serve specific game instances and implements an "Iframe Integration Pattern" to host external game builds stored in the public arcade directory.

- **Arcade Discovery Interface** — Provides the user-facing catalog and navigation UI for the arcade.
- **Dynamic Game Controller** — Manages the routing logic and lifecycle of individual game instances.
- **Arcade Integration Bridge** — Implements the "Iframe Integration Pattern" to host external game builds stored in the `public/arcade/` directory.

### XR/3D Rendering Engine

A specialized component dedicated to high-performance 3D rendering and XR experiences. It encapsulates the Three.js lifecycle, including GLTF asset loading, animation mixing, and the main render loop, providing an immersive "Cline Runner" visual sequence.

- **Lifecycle Orchestrator** — Manages the integration of Three.js into the React component tree.
- **Asset Pipeline** — Responsible for the asynchronous loading and processing of 3D assets.
- **Animation Engine** — Drives the visual sequence through a high-performance render loop.
- **XR & Environment Controller** — Configures the immersive XR session and manages the "Arcade-Rave" visual atmosphere.

### Business Conversion Module

The functional endpoint for lead generation and studio inquiries. It manages the "Request Arcade" workflow, handling user input through validated forms and integrating with external services like Formspree for data persistence.

- **Request Arcade Presentation Layer** — Manages the structural layout, SEO metadata, and informational content blocks for the Request Arcade page.
- **Inquiry Processing Engine** — Handles the interactive lifecycle of the lead generation form.

