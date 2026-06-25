# Architecture Principles

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Purpose

This document defines the permanent architectural principles of the Rifqi platform. These principles establish the core constraints, design patterns, and behavioral rules that govern all future development, package segregation, database layouts, and implementation patterns.

## Context

A long-term project designed to run for decades requires an unyielding architectural foundation. Without clear, permanent principles, code bases inevitably decay due to incremental shortcuts, scope creep, and changing technology trends. This document acts as the primary architectural checkpoint, ensuring that every engineering decision prioritizes maintainability, modularity, and consistency.

## Architectural Principles

### Principle 1: Domain-Driven Design (DDD)
- **Statement**: The structure of the software must reflect the logical domains of the product.
- **Rationale**: Aligning code boundaries with conceptual domains makes the codebase easier to understand and isolates changes to specific functional areas.
- **Example**: Business logic, data models, and types related to the Knowledge domain are grouped into a designated package (`packages/database` or a dedicated package) and isolated from the UI presentation layer.

### Principle 2: Entity-First Design
- **Statement**: Entities and their conceptual relationships define the primary design layer; database schemas and APIs are secondary derivatives.
- **Rationale**: Designing around logical entities ensures that the data model remains clean and reflects the product's vocabulary, rather than database-specific indexing needs or API client formats.
- **Example**: The properties, lifecycles, and constraints of a Project entity are defined in the domain layer before creating relational database tables or API interfaces for projects.

### Principle 3: Knowledge-Graph Ready
- **Statement**: The platform must treat all data nodes as potential graph entities that can be semantically connected.
- **Rationale**: To support rich cognitive navigation, global search, and future AI reasoning, data cannot exist in isolated silos; it must be stored in a way that preserves connection metadata.
- **Example**: Links between Articles and books are modeled as explicit Relationship entities in the data layer, allowing traversal in either direction.

### Principle 4: Single Source of Truth (SSOT)
- **Statement**: Every conceptual property, data field, or system configuration must exist in exactly one authoritative location.
- **Rationale**: DRIFT (data/state inconsistency) is a major source of system failures. SSOT ensures that changes propagate cleanly and system behaviors are predictable.
- **Example**: Styling tokens and shared UI schemas are defined only in the UI package, imported as needed by the workspace and presentation applications.

### Principle 5: Decoupled Read and Write Interfaces
- **Statement**: The read paths and write paths of the system must be architectural separated.
- **Rationale**: The private workspace requires a write-heavy, highly secured interface, while the public website requires a read-heavy, high-performance, and publicly accessible presentation pipeline. Decoupling protects core databases and improves scalability.
- **Example**: Writing content occurs inside the secure Workspace (Studio), which compiles or replicates data to a read-only distribution target parsed by the public Web application.

### Principle 6: Cloud-Native by Default
- **Statement**: The system is designed to run on managed cloud infrastructure to ensure consistent cross-device synchronization and high availability.
- **Rationale**: Cloud deployment simplifies backups, guarantees that the owner can access the Digital Headquarters from any authenticated client, and facilitates API integrations with modern cloud services.
- **Example**: The primary database instance resides on secure cloud hosting, with API-based authentication managing write access from remote clients.

### Principle 7: Modular and Extensible Evolution
- **Statement**: Core services must expose clean boundary contracts, allowing new domains (e.g. AI or automation modules) to be added without rewriting existing features.
- **Rationale**: Future technologies and capabilities will emerge. A modular, decoupled architecture allows components to be upgraded or replaced with minimal disruption to the core foundation.
- **Example**: Adding vector search capabilities is done by subscribing to domain events (e.g., "Learning Created") and writing to a separate index, rather than altering the core CRUD service code.

### Principle 8: AI-Ready Data Structures
- **Statement**: All content, relations, and metadata must be stored in highly structured formats to easily support semantic embedding and LLM consumption.
- **Rationale**: Local AI models require clean, clean metadata, and clear relational context to provide relevant recommendations, summaries, and search completions.
- **Example**: Notes contain structured YAML frontmatter or relational schema parameters detailing references, goals, and categories, allowing an AI script to instantly understand the context of the document.

### Principle 9: Consistency Over Cleverness
- **Statement**: The codebase must prioritize simple, standard, and uniform engineering patterns over complex or highly optimized custom solutions.
- **Rationale**: Simple code is easy to maintain, test, and upgrade over a multi-decade lifecycle. Clever code introduces hidden dependencies and high cognitive overhead for future maintainers.
- **Example**: Preferring clear, sequential service calls and standard SQL-like data queries over complex, highly nested ORM abstract layers.

### Principle 10: Strict Layer Separation
- **Statement**: System logic must be strictly partitioned into layers: Interface, Application, Domain, and Infrastructure.
- **Rationale**: Preventing UI elements from executing database queries directly or infrastructure services from dictating business logic ensures that components can be swapped or refactored independently.
- **Example**: A database connection driver (Infrastructure) can only be accessed via the repository layer (Domain), which in turn feeds the controllers (Application) and finally the views (Interface).

---

## References
- [Product Principles](file:///e:/rifqi.id/docs/01-product/02-Product-Principles.md)
- [Engineering Constitution](file:///e:/rifqi.id/docs/01-product/07-Engineering-Constitution.md)

## Decision Log
- **2026-06-26**: Initialization of the Architecture Principles document by Senior Software Engineer. Status set to Approved.
