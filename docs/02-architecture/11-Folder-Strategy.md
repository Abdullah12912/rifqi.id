# Folder Strategy

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Purpose

The Folder Strategy document defines the repository organization, directory guidelines, and package ownership models for the Rifqi monorepo. It establishes strict rules governing where files must live, preventing structural decay and ensuring long-term code maintainability.

## Context

As a monorepo, Rifqi houses multiple applications (the private Studio workspace, the public Web portal) and supporting packages (auth, config, database, types, UI, utils). Without a clear folder strategy, code boundaries quickly blur, leading to circular imports, untracked configuration drifts, and complex refactoring cycles.

---

## Directory Organization Strategy

```text
rifqi/
├── apps/
│   ├── studio/       # Private administrative workspace application.
│   └── web/          # Public presentation portal application.
│
├── packages/
│   ├── auth/         # Shared security validation models and session handlers.
│   ├── config/       # Shared compiler, linting, and build configuration profiles.
│   ├── database/     # Core persistent schema models and repository operations.
│   ├── shared/       # Reusable domain-agnostic helpers and interfaces.
│   ├── types/        # Authoritative TypeScript types and core entity declarations.
│   ├── ui/           # Design system tokens and shared UI components.
│   └── utils/        # Generic developer helpers (date formats, mathematical units).
│
├── docs/             # Technical specifications, product documentation, roadmap.
├── scripts/          # Workspace operational utilities and developer scripts.
└── tooling/          # Core monorepo build tools and CI/CD pipelines.
```

---

## Folder Owners and Responsibilities

### 1. `apps/`
- **Owner**: Application Developers.
- **Rules**:
  - Contains deployable applications only.
  - Applications must not import code directly from other applications (e.g. `apps/web` cannot import from `apps/studio`).
  - Shared logic must be extracted to the `packages/` directory.

### 2. `packages/`
- **Owner**: Core Architects.
- **Rules**:
  - Contains modular, reusable packages imported by applications.
  - Packages should maintain clean, distinct boundaries.
  - **`packages/database`**: Direct owner of persistent entities, migration logic, and relational queries.
  - **`packages/types`**: The single source of truth for conceptual schema definitions and interfaces.
  - **`packages/ui`**: Enforces styling consistency and owns visual tokens.

### 3. `docs/`
- **Owner**: CTO and Architects.
- **Rules**:
  - The repository's documentation directory.
  - No application code or compiled assets are allowed here.
  - All architecture decisions and product specifications are finalized here before code implementation.

### 4. `scripts/`
- **Owner**: DevOps and System Engineers.
- **Rules**:
  - Houses utilities for repository tasks, migrations, and backups.
  - No business logic or application routines belong here.

### 5. `tooling/`
- **Owner**: DevOps and Build Engineers.
- **Rules**:
  - Stores unified configurations for compilers, linters, code formatting, and testing wrappers.

---

## Dependency Rules

To prevent compilation failures and circular dependency chains, imports must adhere to the following constraints:
- **`apps/studio`** can import from any package in `packages/`.
- **`apps/web`** can import from `packages/ui`, `packages/config`, `packages/types`, `packages/utils`, and `packages/shared`. It **cannot** import from `packages/database` (write pathways) or `packages/auth` (administrative authentication).
- Packages in `packages/` cannot import from `apps/`.
- Circular package imports (e.g. `packages/database` importing `packages/ui`, while `packages/ui` imports `packages/database`) are strictly prohibited and blocked during builds.

---

## References
- [System Architecture](file:///e:/rifqi.id/docs/02-architecture/10-System-Architecture.md)
- [Bounded Contexts](file:///e:/rifqi.id/docs/02-architecture/04-Bounded-Contexts.md)

## Decision Log
- **2026-06-26**: Monorepo directory strategies and import dependency guidelines approved by Senior Software Engineer. Status set to Approved.
