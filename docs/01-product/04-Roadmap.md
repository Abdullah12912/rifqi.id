# Roadmap

- **Version**: 1.1
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Phase 1: Foundation
- **Objectives**: Establish the monorepo architecture, database schemas, styling tokens, and linting rules. Ensure that code validation runs automatically on every commit.
- **Deliverables**:
  - Unified pnpm workspace structure.
  - Core database schema migrations.
  - Centralized TypeScript types and configurations.
  - Git pre-commit hooks and testing infrastructure.
- **Success Criteria**: 100% build pass rate, automated formatting checks executed on commit, and empty packages successfully linking.

## Phase 2: Knowledge Engine
- **Objectives**: Build the system's core data-access and parsing engine. Implement Markdown ingestion and semantic linking databases.
- **Deliverables**:
  - Markdown parser capable of extracting structured frontmatter metadata.
  - Relational database schema for storing entity attributes and bidirectional links.
  - CLI tools for scanning notes and resolving broken entity references.
- **Success Criteria**: 100% accuracy in parsing document frontmatter; broken links are automatically detected and flagged by the CLI.

## Phase 3: Workspace (Studio)
- **Objectives**: Develop the private administrative interface. Allow the owner to manage their data, create nodes, and view their personal graph.
- **Deliverables**:
  - Secure studio app interface.
  - Form-based entity creation and editing interfaces.
  - Task board and project tracking dashboards.
  - Interactive visualization of the semantic knowledge graph.
- **Success Criteria**: Near-zero rendering latency for large boards; successfully creates and updates entities with proper relationships.

## Phase 4: Publishing Engine
- **Objectives**: Implement the workflow that converts internal drafts into public documents. Build compilation filters and image optimization pipelines.
- **Deliverables**:
  - State promotion services (transitions content from Draft to Published status).
  - Automated media optimizer (compresses and copies assets to the public directory).
  - Markdown compiler that converts links from internal references to public web slugs.
- **Success Criteria**: Automated publication checks run successfully, blocking the release of drafts or documents containing broken internal links.

## Phase 5: Public Experience (Web)
- **Objectives**: Build the high-performance public portal. Emphasize accessibility, SEO, readability, and design consistency.
- **Deliverables**:
  - Static site generation layouts for all public entities (Articles, Projects, Learnings, Journey Events).
  - Global Search search bar using unified indexes.
  - Clean CSS theme with standard typography scales.
- **Success Criteria**: 100% Lighthouse SEO score, load time under one second, and fully functional keyboard navigation.

## Phase 6: Intelligence
- **Objectives**: Integrate specialized context models to act as a personalized cognitive companion.
- **Deliverables**:
  - Vector embeddings generator for all documents.
  - Semantic search index and semantic similarity queries.
  - Contextual recommendation module (suggests related books or notes when writing).
- **Success Criteria**: Vector search returns semantically relevant documents with near-zero latency, and suggestions appear instantly.

## Phase 7: Automation
- **Objectives**: Streamline data capture and publishing.
- **Deliverables**:
  - Quick-capture APIs for ingestion from external devices (e.g. mobile bookmarks or voice logs).
  - Automated publishing pipeline triggered by status changes.
  - Automated backups and cloud sync scripts.
- **Success Criteria**: Quick-capture events resolve and save in under two seconds; data backups execute automatically with verification logs.

## Phase 8: Platform
- **Objectives**: Turn Rifqi into an extensible platform. Allow custom plugins, scripting environments, and multi-device views.
- **Deliverables**:
  - Plugin architecture for extending workspace dashboards.
  - Native runtime environment for custom user scripts.
  - Responsive desktop and mobile workspace interfaces.
- **Success Criteria**: Custom developer scripts can read and write to the database using clean, sandboxed API interfaces.

---

## References
- [Masterplan](file:///e:/rifqi.id/docs/00-masterplan/MASTERPLAN.md)
- [PRD](file:///e:/rifqi.id/docs/01-product/03-PRD.md)

## Decision Log
- **2026-06-26**: Initialization of the Roadmap document by CTO. Status set to Approved.
