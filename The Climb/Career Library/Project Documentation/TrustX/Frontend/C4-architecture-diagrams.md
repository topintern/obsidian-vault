---
kind: "project-document"
title: "C4-architecture-diagrams"
collection: "TrustX"
topic: "Frontend"
source_status: "source-description-not-runtime-proof"
imported: "2026-10-13"
source_files: ["Samay + Trustx experience/TrustxRepos/trustx/docs/c4-architecture-diagrams.md"]
tags: ["career/library","career/project-docs"]
---

# C4-architecture-diagrams

[[Project Library]] · [[Career Library]]

Source documentation from an external project snapshot. It does not independently establish personal authorship, current deployment, or measured outcomes.

# TrustX C4 Architecture Diagrams

This document contains C4 model architecture diagrams for the TrustX application. The C4 model provides a hierarchical way to describe software architecture at different levels of detail.

## Color Legend

The diagrams use a consistent color scheme to represent different types of components:

| Color | Hex Code | Component Type |
|-------|----------|----------------|
| <span style="color:#3498db">■</span> Blue | #3498db | Primary components and main system |
| <span style="color:#2ecc71">■</span> Green | #2ecc71 | API services and middle-tier components |
| <span style="color:#9b59b6">■</span> Purple | #9b59b6 | External systems and authentication |
| <span style="color:#e74c3c">■</span> Red | #e74c3c | Data storage components |
| <span style="color:#e67e22">■</span> Orange | #e67e22 | Specialized components |
| <span style="color:#f1c40f">■</span> Yellow | #f1c40f | User roles |

## Level 1: System Context Diagram

The System Context diagram shows TrustX and its relationships with users and external systems.

[C4 Context Diagram](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/trustx/docs/images/c4-context-diagram.svg)

### Elements Description:

- **Compliance Officer**: Primary user responsible for managing compliance frameworks and policies
- **Security Team**: Users who implement and monitor security controls
- **Executive Management**: Users who review compliance status and reports
- **TrustX**: The main system that provides compliance management capabilities
- **Auth0**: External authentication and identity management service
- **Neo4j Database**: Graph database for storing and visualizing access relationships
- **Microsoft Entra ID**: External identity provider for user directory integration

## Level 2: Container Diagram

The Container diagram shows the high-level technical building blocks of the TrustX application.

[C4 Container Diagram](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/trustx/docs/images/c4-container-diagram.svg)

### Elements Description:

- **React Single-Page Application**: Frontend web application built with React
- **REST API Service**: Backend service providing REST endpoints for compliance data
- **GraphQL API Service**: Backend service providing GraphQL endpoints for SOC2 framework data
- **Auth0 Authentication Service**: External service handling user authentication
- **Relational Database**: Stores structured compliance data (policies, controls, etc.)
- **Neo4j Graph Database**: Stores and queries graph-based access relationships
- **Document Storage**: Stores compliance documents and evidence files

## Level 3: Component Diagram

The Component diagram shows the key components within the TrustX React application.

[C4 Component Diagram](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/trustx/docs/images/c4-component-diagram.svg)

### Elements Description:

- **Auth0 Provider**: Manages authentication state and provides auth methods
- **User Metadata Context**: Stores and provides user-specific metadata across components
- **Routing Component**: Handles application routing and navigation
- **Layout Component**: Provides consistent layout structure for all pages
- **Overview Component**: Dashboard showing compliance status and summaries
- **Compliance Components**: Components for policies, controls, documents, and frameworks
- **Neo4j Visualizer**: Component for visualizing and interacting with graph data
- **Chatbot Component**: AI-powered compliance assistant interface
- **API Service Clients**: Components for communicating with backend services

## Level 4: Compliance Components Detail

This diagram shows a more detailed view of the Compliance Components.

[C4 Compliance Components Diagram](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/trustx/docs/images/c4-compliance-components-diagram.svg)

### Elements Description:

- **Policies Component**: Manages the display and interaction with compliance policies
- **Controls Component**: Manages security controls and their implementation status
- **Documents Component**: Handles document management and editing
- **Policy API Client**: Communicates with the backend API for policy operations
- **Controls API Client**: Communicates with the backend API for controls operations
- **Documents API Client**: Communicates with the backend API for document operations
- **Policy Editor**: Interface for creating and editing policies
- **Control Details**: Interface for viewing and updating control implementation
- **Document Editor**: Rich text editor for creating and editing documents
- **SOC2 Dashboard**: Specialized dashboard for SOC2 compliance status

## Data Flow Diagrams

### Authentication Flow

```
+-------------+     +-------------+     +-------------+     +-------------+
|             |     |             |     |             |     |             |
|    User     | --> |   TrustX    | --> |    Auth0    | --> |   TrustX    |
|             |     |   Frontend  |     |             |     |   Frontend  |
|             |     |             |     |             |     |             |
+-------------+     +-------------+     +-------------+     +-------------+
                                              |
                                              v
                                        +-------------+
                                        |             |
                                        |    User     |
                                        |   Metadata  |
                                        |             |
                                        +-------------+
```

### API Request Flow

```
+-------------+     +-------------+     +-------------+     +-------------+
|             |     |             |     |             |     |             |
|   TrustX    | --> |    Auth     | --> |    API      | --> |  Database   |
|   Frontend  |     |   Headers   |     |   Service   |     |             |
|             |     |             |     |             |     |             |
+-------------+     +-------------+     +-------------+     +-------------+
                                              |
                                              v
                                        +-------------+
                                        |             |
                                        |   Response  |
                                        |    Data     |
                                        |             |
                                        +-------------+
                                              |
                                              v
                                        +-------------+
                                        |             |
                                        |   TrustX    |
                                        |   Frontend  |
                                        |             |
                                        +-------------+
```

## Technology Mapping

| C4 Element | Technology/Implementation |
|------------|---------------------------|
| Frontend SPA | React.js, React Router |
| Authentication | Auth0 |
| REST API | Node.js (assumed) |
| GraphQL API | GraphQL, AppSync |
| Graph Database | Neo4j |
| Document Storage | S3 or similar (assumed) |
| Relational Database | Not specified in code |

## Deployment View

```
+-------------------------------------------------------------------------+
|                                                                         |
|                          Cloud Environment                              |
|                                                                         |
|  +---------------+        +---------------+        +---------------+    |
|  |               |        |               |        |               |    |
|  | Static Web    |        | API Gateway   |        | Database      |    |
|  | Hosting       |        | Services      |        | Services      |    |
|  | (Frontend)    |        |               |        |               |    |
|  +---------------+        +---------------+        +---------------+    |
|                                                                         |
+-------------------------------------------------------------------------+
|                                                                         |
|                         External Services                               |
|                                                                         |
|  +---------------+        +---------------+        +---------------+    |
|  |               |        |               |        |               |    |
|  | Auth0         |        | Neo4j         |        | Microsoft     |    |
|  | Service       |        | Database      |        | Entra ID      |    |
|  |               |        |               |        |               |    |
|  +---------------+        +---------------+        +---------------+    |
|                                                                         |
+-------------------------------------------------------------------------+
```

## About the C4 Model

These diagrams follow the C4 model approach to documenting software architecture. The C4 model was created by Simon Brown and provides a way to create maps of your code at various levels of detail, similar to how we use maps in the real world (from country maps to city maps to street maps).

### The Four C's of the C4 Model

1. **Context (Level 1)**: Shows the big picture - what is the system we're building and what is the environment it operates in? Who are the users and what other systems does it interact with?

2. **Container (Level 2)**: Zooms in to show the high-level technical building blocks. A container is something like a web application, mobile app, database, file system, etc. This level shows how responsibilities are distributed across containers and how these containers communicate.

3. **Component (Level 3)**: Zooms in further to show the components inside each container. These are groups of related functionality encapsulated behind a well-defined interface.

4. **Code (Level 4)**: The lowest level of detail, showing how components are implemented. This might include class diagrams, entity relationship diagrams, etc. In our case, we've included a detailed view of the Compliance Components instead of actual code diagrams.

### Benefits of the C4 Model

- **Common Language**: Provides a common language for discussing and documenting architecture
- **Different Levels of Detail**: Allows you to create diagrams at different levels of abstraction
- **Simplicity**: Uses a simple notation that's easy to understand
- **Flexibility**: Can be adapted to different technologies and domains

For more information on the C4 model, visit [c4model.com](https://c4model.com/).


## Source provenance

[External original](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/Samay%20%2B%20Trustx%20experience/TrustxRepos/trustx/docs/c4-architecture-diagrams.md) · Samay + Trustx experience/TrustxRepos/trustx/docs/c4-architecture-diagrams.md

Project code and dependencies remain outside the vault. No source commands were executed.
