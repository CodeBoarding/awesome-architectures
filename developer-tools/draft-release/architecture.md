```mermaid
graph LR
  subgraph 1["Workflow Orchestrator"]
    1__1_1["Workflow Orchestrator"]
    1__1_2["Version & Configuration Engine"]
    1__1_3["Release Content Processor"]
    1__1_4["GitHub API Gateway"]
    1__1_1 -->|"Requests current release data and submits the final draft update."| 1__1_4
    1__1_1 -->|"Triggers the generation of release notes using the context and inputs gathered during initializatio…"| 1__1_3
    1__1_1 -->|"Requests the next semantic version and configuration metadata to guide the release process."| 1__1_2
    1__1_3 -->|"References category mappings and label configurations to correctly group and format markdown sectio…"| 1__1_2
    1__1_2 -->|"calls"| 1__1_1
    1__1_2 -->|"calls"| 1__1_3
    1__1_3 -->|"calls"| 1__1_1
    1__1_4 -->|"calls"| 1__1_1
  end
  subgraph 2["Release Notes Engine"]
    2__2_1["Action Lifecycle & API Gateway"]
    2__2_2["Release Notes Orchestrator"]
    2__2_3["Dependency Aggregator"]
    2__2_4["Markdown Assembler"]
    2__2_1 -->|"Initiates the generation process by providing raw GitHub context and commit history."| 2__2_2
    2__2_2 -->|"Delegates the identification and grouping of dependency-related commits to reduce document noise."| 2__2_3
    2__2_2 -->|"Provides categorized and cleaned content for final document formatting and template application."| 2__2_4
    2__2_1 -->|"Uses internal versioning logic to determine the next release tag before updating the GitHub release."| 2__2_1
  end
  subgraph 3["GitHub Release Manager"]
    3__3_1["Release State Discovery"]
    3__3_2["Release Mutation Engine"]
    3__3_3["GitHub API Client Integration"]
    3__3_2 -->|"Queries the discovery component to determine if the current operation should be a create or an upda…"| 3__3_1
    3__3_1 -->|"Utilizes the authenticated client to perform read-only GET requests against the GitHub Release API."| 3__3_3
    3__3_2 -->|"Utilizes the authenticated client to perform state-changing POST and PATCH requests to the GitHub R…"| 3__3_3
  end
  1 -->|"Passes collected Pull Request data and configuration settings to generate the formatted Markdown bo…"| 2
  1 -->|"Provides the calculated version and generated notes to be persisted as a draft on GitHub."| 3
  3 -->|"Returns existing release metadata (e.g., tag names, draft status) to inform the versioning and upda…"| 1
  2 -->|"Internally utilizes specialized patterns to group and deduplicate dependency update entries before …"| 2
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The `draft-release` GitHub Action follows a structured pipeline pattern designed to automate the maintenance of release drafts. The process begins with the Workflow Orchestrator, which ingests GitHub event data and configuration to establish the execution context and determine versioning logic. It then delegates the transformation of repository history (Pull Requests and commits) to the Release Notes Engine, which applies complex grouping and formatting rules. Finally, the GitHub Release Manager interfaces with the GitHub API to reconcile the generated content with the existing repository state, either creating a new draft or updating an existing one to ensure the release notes are always up-to-date before a manual publish.

### Workflow Orchestrator

Acts as the central entry point and controller for the action. It parses inputs, fetches the execution context (repo, owner, event details), and calculates the version increment based on labels or configuration.

- **Workflow Orchestrator** — Acts as the central controller and entry point.
- **Version & Configuration Engine** — Responsible for interpreting the repository's configuration (YAML) and applying semantic versioning logic.
- **Release Content Processor** — A complex engine dedicated to generating and formatting the release body.
- **GitHub API Gateway** — Encapsulates all external communication with GitHub's REST and GraphQL APIs.

### Release Notes Engine

The core logic engine responsible for transforming raw GitHub data into structured Markdown. it handles the grouping of dependency updates (e.g., from Dependabot), strips conventional commit prefixes, and applies Handlebars templates to generate the final release body.

- **Action Lifecycle & API Gateway** — Acts as the external boundary of the subsystem, managing the execution lifecycle of the GitHub Action.
- **Release Notes Orchestrator** — The central logic hub responsible for coordinating the transformation of raw commit data into categorized release sections.
- **Dependency Aggregator** — A specialized logic engine that processes automated dependency updates (primarily from Dependabot).
- **Markdown Assembler** — Manages the physical structure and assembly of the final Markdown document.

### GitHub Release Manager

Manages the stateful interactions with the GitHub REST/GraphQL APIs. It identifies the current "latest" release versus the "draft" release and performs the actual mutations (create/update) on the repository's release resources.

- **Release State Discovery** — Responsible for querying the GitHub API to determine the current state of releases within the repository.
- **Release Mutation Engine** — Handles the actual creation and modification of release resources on GitHub.
- **GitHub API Client Integration** — The low-level infrastructure layer that manages the @actions/github Octokit client.

