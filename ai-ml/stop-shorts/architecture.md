```mermaid
graph LR
  subgraph 1["Video Loop Controller (Content Script)"]
    1__1_1["Lifecycle & State Controller"]
    1__1_2["DOM Observation Engine"]
    1__1_3["Loop Prevention Engine"]
    1__1_1 -->|"Triggers observation start/stop based on navigation state and user preferences."| 1__1_2
    1__1_2 -->|"Passes detected video elements to have loop prevention logic applied."| 1__1_3
    1__1_1 -->|"Provides the current 'enabled' state to gate the application of property overrides."| 1__1_3
    1__1_2 -->|"calls"| 1__1_1
    1__1_3 -->|"calls"| 1__1_1
    1__1_3 -->|"calls"| 1__1_2
  end
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The Video Loop Controller acts as the central engine for the browser extension, managing the prevention of automatic video looping on YouTube Shorts. Its main flow involves initializing upon page load or navigation, monitoring for video elements, and intercepting DOM properties to override YouTube's internal looping behavior, while simultaneously synchronizing with browser storage to apply user-defined settings.

### Video Loop Controller (Content Script)

The core logic of the extension, operating within the YouTube content script context. It orchestrates the detection of Shorts pages, manages the lifecycle of video elements, and applies property-level overrides to prevent automatic looping. It reacts to YouTube's SPA navigation events and synchronizes state with browser storage to ensure user preferences are respected in real-time.

- **Lifecycle & State Controller** — Acts as the central nervous system of the content script.
- **DOM Observation Engine** — Handles the "discovery" of video elements within YouTube's highly dynamic interface.
- **Loop Prevention Engine** — Executes the core technical intervention required to stop video looping.

