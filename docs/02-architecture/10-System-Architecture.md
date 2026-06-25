# System Architecture

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Purpose

The System Architecture document defines the logical layering and structural boundaries of the Rifqi platform. It describes the responsibilities of each layer—Workspace, Application, Domain, Infrastructure, Publishing, Public Web, and AI—ensuring a clean separation of concerns and preventing circular dependencies in future development.

## Context

A long-term Digital Headquarters monorepo must be designed to withstand updates to framework components, database drivers, and styling libraries. By enforcing strict logical layer separations, we ensure that infrastructure implementations can be replaced or updated without modifying core domain rules or user interface configurations.

---

## Logical Architecture Layer Diagram

```text
+-----------------------------------------------------------------+
|                    1. Workspace (Studio UI)                     |
+-----------------------------------------------------------------+
                                |
                                v
+-----------------------------------------------------------------+
|                    2. Application Layer                         |
|    (Use Cases, DTOs, Command Handlers, Controllers)             |
+-----------------------------------------------------------------+
                                |
                                v
+-----------------------------------------------------------------+
|                    3. Domain Layer                              |
|    (Entity Definitions, Domain Logic, Repository Interfaces)    |
+-----------------------------------------------------------------+
            |                                         |
            v                                         v
+-----------------------+                 +-----------------------+
|  4. Infrastructure    |                 | 5. Publishing Layer   |
|  (DB Drivers, Auth,   |                 | (Markdown Compiler,   |
|   Search Indexers)    |                 |  Media Compressor)    |
+-----------------------+                 +-----------------------+
                                                      |
                                                      v
                                          +-----------------------+
                                          | 6. Public Web Portal  |
                                          | (Static Pages, UI)    |
                                          +-----------------------+

+-----------------------------------------------------------------+
|                    7. Future AI Layer                           |
|    (Vector Generators, Context Resolvers, Recommendation Engine)|
+-----------------------------------------------------------------+
```
*Note: Dependencies flow strictly downward. Lower layers cannot import or depend on upper layers.*

---

## Layer Responsibilities

### 1. Workspace Layer (Studio UI)
- **Role**: Exposes the administrative workspace user interfaces.
- **Responsibilities**:
  - Renders forms, interactive task boards, curation screens, and graph visualizations.
  - Manages frontend client state and authenticates workspace sessions.
  - Formats data inputs and dispatches commands to the Application Layer.

### 2. Application Layer
- **Role**: Coordinates workflows and implements specific use cases.
- **Responsibilities**:
  - Implements application entry points (e.g. controllers, CLI entry handlers).
  - Handles command and query routing (CQRS patterns if applicable).
  - Manages session validation, application log outputs, and transaction boundaries.
  - Converts data transfer objects (DTOs) from clients into domain entity models.

### 3. Domain Layer
- **Role**: The core business logic and rules processor of the system.
- **Responsibilities**:
  - Implements pure business logic, invariants, and validation rules (e.g., preventing invalid state transitions).
  - Defines the core entity models and their relationship behaviors.
  - Exposes abstract interfaces for data access (Repository Interfaces).
  - Dictates domain event definitions.

### 4. Infrastructure Layer
- **Role**: Implements external system and database drivers.
- **Responsibilities**:
  - Materializes abstract Domain repositories into actual database write/read queries.
  - Interfaces with filesystem modules, external networks, and security cryptography modules.
  - Manages search indexes, message brokers, and background task runners.

### 5. Publishing Layer
- **Role**: Orchestrates public presentation compilation.
- **Responsibilities**:
  - Intercepts domain events from the Application Layer.
  - Sanitizes private metadata properties from public entity records.
  - Compiles markdown source files into optimized static pages and directories.
  - Optimizes image/video media files for public deployment paths.

### 6. Public Web Portal Layer
- **Role**: Renders public presentation assets.
- **Responsibilities**:
  - Serves compiled static pages representing Articles, Projects, and Learnings.
  - Houses public typography layouts, styling systems, and client search elements.
  - Interacts exclusively with compiled static directories or read-only caches, keeping completely decoupled from write paths.

### 7. Future AI Layer
- **Role**: Provides semantic analysis and machine reasoning utilities.
- **Responsibilities**:
  - Subscribes to database mutations to generate vector embeddings.
  - Computes contextual similarity matrices across notes and books.
  - Feeds structured reference nodes to local reasoning models to synthesize draft layouts.

---

## References
- [System Context](file:///e:/rifqi.id/docs/02-architecture/01-System-Context.md)
- [Folder Strategy](file:///e:/rifqi.id/docs/02-architecture/11-Folder-Strategy.md)

## Decision Log
- **2026-06-26**: Logical architecture layering and upward-import restrictions approved by Senior Software Engineer. Status set to Approved.
