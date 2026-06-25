# Engineering Constitution

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Article 1: Documentation Before Development
- **Rule**: No package, directory, database table, or major service may be created or refactored without first writing its specification documentation in the `docs/` folder.
- **Explanation**: Writing documentation forces developers to think through interfaces, dependencies, and requirements before executing code, preventing accidental complexity.
- **Example**: Before creating the database package, the database schema design must be fully documented in `docs/03-database/SCHEMA.md`.
- **Consequences**: Pull requests containing code modifications without corresponding documentation updates will be automatically rejected.

## Article 2: Architecture Before Implementation
- **Rule**: System design and file organization must follow strict architectural guidelines before writing operational logic.
- **Explanation**: Establishing structural layout rules (such as Monorepo packages and domain boundaries) ensures code remains modular, preventing the codebase from collapsing into a giant monolith.
- **Example**: Creating a shared utility requires placing it in `packages/utils` and setting up its package configuration before calling it from `apps/web`.
- **Consequences**: Any code written in an incorrect directory or violating dependency boundaries will be flagged and blocked during compilation.

## Article 3: Single Source of Truth
- **Rule**: Every piece of data, configuration, schema, or system rule must have exactly one authoritative source in the repository.
- **Explanation**: Duplicate configurations or data definitions inevitably drift apart, leading to runtime failures, sync bugs, and high maintenance costs.
- **Example**: The styling tokens (colors, font sizes) are defined exactly once in `packages/ui` and imported by both the `studio` and `web` apps.
- **Consequences**: Hardcoded copies of styles, constants, or types in other directories are strictly forbidden and will be cleaned up during refactoring.

## Article 4: Entity First
- **Rule**: All data structures must revolve around the official entities defined in the product language.
- **Explanation**: Designing database schemas and backend services to map 1:1 to defined product entities ensures that developers, database engines, and UI layers share the same mental model.
- **Example**: Database table names must be `project`, `article`, `learning`, etc., matching the exact singular names in `Product-Language.md`.
- **Consequences**: Developers cannot introduce ad-hoc data schemas or random collection names (e.g. `posts_collection`, `my_notes_table`) that deviate from official terminology.

## Article 5: Everything Linkable
- **Rule**: Every node in the database or filesystem must be accessible via a unique, stable, and immutable link or ID.
- **Explanation**: This allows for seamless traversal of the knowledge graph and enables precise internal and external links that never break when a document is moved.
- **Example**: A Learning entity possesses a persistent UUID or slug that remains unchanged even if the note's title is modified.
- **Consequences**: Moving a file or renaming a folder must not break existing references; the link resolver service must maintain mapping integrity.

## Article 6: Everything Searchable
- **Rule**: All contents, logs, documentation, metadata, and entities must be indexed and searchable globally.
- **Explanation**: Information is useless if it cannot be found. Fast, global search is the primary mechanism of cognitive retrieval.
- **Example**: The global search bar indexes Markdown file contents, YAML frontmatter, and relational database records.
- **Consequences**: Any new entity added to the codebase that does not implement the search indexing interface will be excluded from production compiles.

## Article 7: Decision by ADR (Architecture Decision Record)
- **Rule**: Significant architectural decisions, package additions, or database schema pivots must be proposed, debated, and approved using an ADR in `docs/decisions/`.
- **Explanation**: Documentation of decisions preserves the context and rationale for future maintainers, preventing the recurrence of discarded design patterns.
- **Example**: Deciding on a specific local database engine must be recorded in an ADR detailing the alternatives considered and consequences.
- **Consequences**: Architectural changes introduced without an approved ADR will be rolled back.

## Article 8: Consistency Over Cleverness
- **Rule**: Prefer simple, clear, standard code patterns over complex, clever, or highly abstracted optimizations.
- **Explanation**: A code block that is easy to read is easy to debug and maintain. Clever code is a liability over multi-decade lifecycles.
- **Example**: Using standard `fetch` statements or basic SQL queries instead of importing a heavy ORM package or complex abstraction layer.
- **Consequences**: Complex code abstractions will be rejected during peer review in favor of simpler, linear implementations.

## Article 9: Build for Decades
- **Rule**: Design every directory structure, configuration file, and data format to remain functional for at least ten years.
- **Explanation**: The repository is a lifelong Digital Headquarters. Avoid ephemeral packages, rapidly evolving frameworks, or vendor-locked APIs that require frequent rewrite cycles.
- **Example**: Relying on SQLite and flat Markdown files instead of closed proprietary databases.
- **Consequences**: Dependency selections will be heavily audited, favoring mature, widely adopted, and open-source standards.

## Article 10: Internal Workspace Owns the Data
- **Rule**: The private Workspace (Studio) is the absolute authority for data creation, mutation, and state management; the Web app is strictly a read-only viewer.
- **Explanation**: Decoupling the write and read interfaces protects the core data store from external security vulnerabilities and performance bottlenecks.
- **Example**: The Web app performs read queries on a compiled cache or read-only database replica, while write operations can only be executed within the secure, local Studio app.
- **Consequences**: Public Web routes will never contain logic that creates, updates, or deletes database records.

---

## References
- [Product Principles](file:///e:/rifqi.id/docs/01-product/02-Product-Principles.md)
- [Product Language](file:///e:/rifqi.id/docs/01-product/05-Product-Language.md)

## Decision Log
- **2026-06-26**: Initialization of the ten articles of the Engineering Constitution by CTO. Status set to Approved.
