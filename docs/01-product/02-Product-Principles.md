# Product Principles

- **Version**: 1.1
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Principle 1: Data Sovereignty First
- **Statement**: The owner must possess absolute control and ownership over all data, structures, and metadata.
- **Explanation**: The platform must store data in non-proprietary, standard, human-readable formats (such as markdown, JSON, or plain SQL files) that can be read, transferred, and parsed without depending on the Rifqi codebase or any proprietary third-party software.
- **Rationale**: Third-party SaaS companies and data formats will inevitably close down, change pricing, or deprecate APIs. Standard format files stored in owner-controlled repositories or standard databases can be read indefinitely.
- **Practical Example**: All notes are stored as standard flat files or structured database records containing frontmatter metadata. Even if the application layer of Rifqi is destroyed, the owner can query and read every note using any standard database viewer or file editor.

## Principle 2: Separation of Workspace and Presentation
- **Statement**: Private workspaces and public web interfaces must remain entirely decoupled.
- **Explanation**: The creation, curation, and management of data occur in a secure, private administrative workspace. The public web portal is a read-only mirror of a filtered subset of this data.
- **Rationale**: Decoupling prevents private drafts or experimental notes from being exposed, and allows modifying the public design without risk to the internal operational workflows.
- **Practical Example**: Creating an active project in the workspace does not publish it. Pushing it to the public web requires setting a specific status and criteria, which filters it through a distinct publishing service.

## Principle 3: Semantic Interconnectedness
- **Statement**: Information is not stored in isolation; it must exist as part of a connected knowledge graph.
- **Explanation**: No entity (Article, Project, Book) should be a terminal node. Every entity must define explicit relationships to other entities in the system.
- **Rationale**: Human memory is associative. By structuring the database as a semantic network, the system helps discover forgotten connections and makes searching intuitive.
- **Practical Example**: When writing an entry about a new project, the project must be programmatically linked to a Goal entity, a Technology entity, and any relevant Book or Learning notes.

## Principle 4: Metadata Excellence
- **Statement**: Raw content is secondary to structured metadata.
- **Explanation**: Every document and database record must possess rigorous, structured frontmatter or schema definitions that define its type, relations, states, and timeline.
- **Rationale**: Well-structured metadata allows for high-performance querying, search indexing, and automated processing by scripts and future AI modules.
- **Practical Example**: An Article must include frontmatter fields specifying its version, status, language constraints, primary domains, and related Project IDs before the publishing pipeline will accept it.

## Principle 5: Monorepo Single Source of Truth
- **Statement**: Everything related to the project—docs, tooling, applications, packages—must live in one codebase.
- **Explanation**: The repository acts as the complete history of both the product's structure and the owner's knowledge base.
- **Rationale**: Multi-repo architectures introduce dependency sync issues, coordinate fragmentation, and increase maintenance overhead over long timescales.
- **Practical Example**: Documentation, database migrations, common TypeScript interfaces, UI components, and studio apps are all co-located in the same workspace and managed under a single git commit history.

## Principle 6: Readability and Clarity Over Cleverness
- **Statement**: Design codebase patterns and data structures for maximum clarity, sacrificing hyper-optimization where it hurts readability.
- **Explanation**: Code, database queries, and structures must be written with the assumption that the maintainer has forgotten how they work. Avoid overly abstract design patterns or complex, undocumented framework features.
- **Rationale**: A project designed to run for decades will spend 99% of its life in maintenance mode. Clear, simple code is easy to upgrade or port to new systems.
- **Practical Example**: Standard SQL queries or basic fetch calls are preferred over heavily abstracted ORM queries, allowing developers in ten years to understand the query instantly.

## Principle 7: Longevity Over Modernity
- **Statement**: Prioritize architectural stability and long-term support over the latest software development trends.
- **Explanation**: Only introduce technologies, data structures, and packages that have demonstrated stability or have clear migration paths. Avoid experimental alpha or beta versions.
- **Rationale**: Chasing modern frameworks leads to constant refactoring cycles and security vulnerabilities, distracting from the core objective of the Digital Headquarters.
- **Practical Example**: Standardizing on Markdown and basic SQLite databases rather than proprietary cloud databases or experimental document stores.

## Principle 8: Structured Progression of Output
- **Statement**: Information must graduate through defined states from initial thought to public output.
- **Explanation**: Content creation follows a strict lifecycle: Idea -> Learning -> Project / Article. Thoughts are refined in stages rather than instantly dumped into a public blog.
- **Rationale**: Enforcing a progression model guarantees that public-facing content is highly polished, deeply researched, and linked to real historical progress.
- **Practical Example**: A raw note taken on a book starts as an Idea. It is then synthesized into a structured Learning, and finally cited in a public Article.

## Principle 9: Ubiquitous Searchability and Linkability
- **Statement**: Every entity in the system must be globally search-indexed and uniquely addressable.
- **Explanation**: The architecture must support deep linking to any specific entity or block, and allow global search across all content types simultaneously.
- **Rationale**: To function as an effective cognitive extension, retrieval times must be near-zero. Users should not navigate hierarchies; they should search or click direct links.
- **Practical Example**: The system assigns a unique, immutable slug or ID to every Goal, Article, and Book, allowing the user to search "database design" and find all linked items across domains.

## Principle 10: Cloud-Native Architecture
- **Statement**: The platform is built using a cloud-native model to ensure scalability, central coordination, and cross-device availability.
- **Explanation**: The primary source of truth resides on secure cloud infrastructure, allowing the owner to access and manage their Digital Headquarters from any location or device with consistent state synchronization.
- **Rationale**: A cloud-native foundation removes physical server dependencies, simplifies deployment, provides instant cross-device updates, and enables reliable integration of cloud-based APIs and systems.
- **Practical Example**: The studio workspace is deployed securely to a cloud environment. The owner can securely edit documents or track tasks from both a laptop and a mobile client, with all changes immediately synchronized to the central cloud database.

---

## References
- [Masterplan](file:///e:/rifqi.id/docs/00-masterplan/MASTERPLAN.md)
- [Engineering Constitution](file:///e:/rifqi.id/docs/01-product/07-Engineering-Constitution.md)

## Decision Log
- **2026-06-26**: Initialization of the ten Product Principles by CTO. Status set to Approved.
