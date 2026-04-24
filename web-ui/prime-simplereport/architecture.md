```mermaid
graph LR
  subgraph 1["Core Clinical API"]
    1__1_1["GraphQL API Gateway"]
    1__1_2["Clinical Domain & Business Logic"]
    1__1_3["Interoperability Engine"]
    1__1_4["Identity & Access Management"]
    1__1_5["Patient Experience (PXP)"]
    1__1_6["Bulk Data Services"]
    1__1_1 -->|"Enforces field-level permissions and multi-tenant context for all incoming requests."| 1__1_4
    1__1_1 -->|"Delegates clinical operations and state transitions to domain services."| 1__1_2
    1__1_2 -->|"Provides clinical data for transformation into FHIR and HL7 standards."| 1__1_3
    1__1_5 -->|"Accesses patient and test result data via secure, tokenized links."| 1__1_2
    1__1_4 -->|"Initializes organization and facility entities during the onboarding process."| 1__1_2
    1__1_6 -->|"Streams clinical datasets directly from the domain layer for CSV export."| 1__1_2
  end
  subgraph 2["Interoperability & Data Exchange"]
    2__2_1["Interoperability Standards & Context"]
    2__2_2["Universal Reporting Pipeline"]
    2__2_3["ReportStream Integration Gateway"]
    2__2_2 -->|"Uses standards and context for data transformation."| 2__2_1
    2__2_2 -->|"Sends transformed reports for external delivery."| 2__2_3
    2__2_3 -->|"Updates the status of reports submitted by the pipeline via callback processing."| 2__2_2
  end
  subgraph 3["Security & Identity Service"]
    3__3_1["Identity & Authentication Management"]
    3__3_2["Authorization & User Management"]
    3__3_3["Administrative Governance"]
    3__3_4["Security Infrastructure & Monitoring"]
    3__3_1 -->|"Provides verified user identities and security contexts required for role assignment and facility a…"| 3__3_2
    3__3_3 -->|"Facilitates the approval of new organizations and provides manual overrides for account security (e…"| 3__3_1
    3__3_3 -->|"Enables superusers to manage user roles across different organizations and control cross-tenant dat…"| 3__3_2
    3__3_4 -->|"Enforces access control policies at the application's entry points via protected routes and monitor…"| 3__3_2
  end
  subgraph 4["Clinical Workflow UI"]
    4__4_1["Application Infrastructure & Design System"]
    4__4_2["Patient & Clinical Workflow Engine"]
    4__4_3["Test Results & Clinical Insights"]
    4__4_4["Organization & Identity Administration"]
    4__4_5["Support & Interoperability Tools"]
    4__4_1 -->|"provides routing and data-fetching layer to"| 4__4_2
    4__4_4 -->|"defines facility and user permissions context for"| 4__4_2
    4__4_2 -->|"transitions completed test records into"| 4__4_3
    4__4_5 -->|"manages global device and test type definitions consumed by"| 4__4_2
    4__4_1 -->|"supplies reusable USWDS components to"| 4__4_5
  end
  subgraph 5["Admin & Onboarding Workflows"]
    5__5_1["Onboarding & Identity Services"]
    5__5_2["Organization & User Administration"]
    5__5_3["System Support & Global Catalog"]
    5__5_1 -->|"submits organization requests and identity verification results for administrative review and appro…"| 5__5_3
    5__5_3 -->|"approves pending organizations and maintains the global device catalog used for facility configurat…"| 5__5_2
    5__5_2 -->|"triggers user invitation and MFA enrollment workflows for new organization staff members"| 5__5_1
    5__5_3 -->|"provides administrative overrides and troubleshooting tools for users stuck in the identity verific…"| 5__5_1
  end
  subgraph 6["Analytics & Universal Reporting"]
    6__6_1["Universal Reporting Form Engine"]
    6__6_2["Pilot Navigation Shell"]
    6__6_3["Analytics Dashboard"]
    6__6_2 -->|"Hosts the form engine within a branded layout and provides the necessary user identity context."| 6__6_1
    6__6_1 -->|"Supplies the standardized lab report data that populates the aggregated metrics and trend visualiza…"| 6__6_3
  end
  4 -->|"Sends GraphQL queries and mutations for patient management and test result entry."| 1
  1 -->|"Passes clinical events for transformation into FHIR/HL7 and transmission to ReportStream."| 2
  1 -->|"Validates user permissions and tenant access context for every request."| 3
  5 -->|"Coordinates identity verification and MFA enrollment during user signup."| 3
  5 -->|"Updates organization and facility configurations."| 1
  6 -->|"Submits standardized lab reports via the universal reporting pilot."| 2
  6 -->|"Retrieves aggregate clinical data for visualization."| 1
```

[![CodeBoarding](https://img.shields.io/badge/Generated%20by-CodeBoarding-9cf?style=flat-square)](https://github.com/CodeBoarding/CodeBoarding)

## Details

The `prime-simplereport` system is a modular monolith healthcare interoperability hub that bridges a React-based frontend with a Spring Boot backend. It is organized into six logical components—Core Clinical API, Interoperability & Data Exchange, Security & Identity Service, Clinical Workflow UI, Admin & Onboarding Workflows, and Analytics & Universal Reporting—which collectively manage clinical data, ensure regulatory compliance through data standardization, enforce fine-grained security, and provide administrative and analytical tools for healthcare organizations.

### Core Clinical API

The central backend engine managing clinical data entities (patients, facilities, test orders) via a GraphQL API. It handles business logic, data persistence, and domain-specific exceptions, serving as the primary source of truth for clinical operations.

- **GraphQL API Gateway** — The primary entry point for the web application, coordinating complex mutations and queries across clinical entities like patients, facilities, and test orders.
- **Clinical Domain & Business Logic** — The core engine managing the state and lifecycle of patients, facilities, and test orders, governed by strict clinical validation rules and data retention policies.
- **Interoperability Engine** — Responsible for translating internal domain models into standardized healthcare formats (FHIR/HL7) for public health reporting and external integrations.
- **Identity & Access Management** — Manages the security context, multi-tenant isolation, and the onboarding workflow for new clinical organizations, including identity verification and MFA.
- **Patient Experience (PXP)** — A specialized, token-based access layer for patient-facing interactions such as self-registration and unauthenticated test result retrieval.
- **Bulk Data Services** — REST-based controllers designed for high-volume data export and reporting, bypassing the GraphQL layer to stream clinical datasets directly to users.

### Interoperability & Data Exchange

A dedicated layer for healthcare data standards (FHIR, HL7 v2). It transforms internal models into interoperable formats and manages communication with external public health nodes like CDC's ReportStream, ensuring compliance with federal reporting requirements.

- **Interoperability Standards & Context** — Provides the foundational metadata, constants, and processing context required for healthcare data standards.
- **Universal Reporting Pipeline** — Acts as the primary ingestion and transformation engine for clinical data.
- **ReportStream Integration Gateway** — Manages the outbound communication and inbound feedback loop with the CDC's ReportStream platform.

### Security & Identity Service

Manages authentication, authorization, and system health. It integrates with Okta for identity management and provides custom GraphQL directives to enforce fine-grained access control based on user roles and organization membership.

- **Identity & Authentication Management** — Handles the initial onboarding of organizations and the security posture of individual user accounts.
- **Authorization & User Management** — Manages the internal organizational structure, defining roles and facility-level access permissions.
- **Administrative Governance** — Provides high-privilege tools for system administrators to perform cross-tenant operations, approve pending organizations, and provide support functions like MFA resets or user impersonation for troubleshooting.
- **Security Infrastructure & Monitoring** — The foundational layer that provides telemetry, system health monitoring, and core security routing logic.

### Clinical Workflow UI

The primary React-based user interface for clinicians and staff. It manages the test queue, patient management, and facility dashboards, utilizing Apollo Client for state management and backend synchronization.

- **Application Infrastructure & Design System** — Provides the foundational framework, routing, and visual language for the entire application.
- **Patient & Clinical Workflow Engine** — The core operational hub where clinicians manage the lifecycle of a testing encounter.
- **Test Results & Clinical Insights** — Manages the post-testing phase, providing clinicians with a searchable history of results and actionable clinical guidance.
- **Organization & Identity Administration** — Handles the governance and security context of the application.
- **Support & Interoperability Tools** — A high-privilege module used for system-wide maintenance and data interoperability.

### Admin & Onboarding Workflows

Manages the lifecycle of organizations and users, including multi-step signup processes, identity verification, and administrative tools for managing facilities, device types, and user permissions.

- **Onboarding & Identity Services** — Handles the "front door" logic, including organization signup, Experian-based identity proofing, and the user activation/MFA flow for invited staff.
- **Organization & User Administration** — Provides administrative interfaces for active organizations to manage their internal structure, including facility metadata (CLIA numbers, addresses), user roles, and permissions.
- **System Support & Global Catalog** — Facilitates system-wide administration by CDC or support staff, including the review of pending organizations and maintenance of the global registry of supported testing devices.

### Analytics & Universal Reporting

Provides specialized reporting tools and data visualizations. It includes the 'Universal Reporting' pilot for lab results and high-level analytics dashboards for monitoring testing trends across organizations.

- **Universal Reporting Form Engine** — Manages the complex, multi-step manual reporting workflow for the Universal Reporting pilot.
- **Pilot Navigation Shell** — Provides the specialized navigation framework and federal branding for the Universal Reporting pilot.
- **Analytics Dashboard** — Provides high-level data visualizations and monitoring tools for tracking testing trends across organizations.

