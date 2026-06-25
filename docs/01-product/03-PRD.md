# Product Requirement Document (PRD)

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Product Overview

Rifqi is a Personal Operating System structured as a monorepo. It contains two primary applications: a private administrative workspace (Studio) and a public presentation portal (Web), powered by shared, domain-driven packages. It serves as a unified digital environment for the owner to organize knowledge, map learnings, track projects and goals, draft articles, and deploy a personal brand portfolio.

## Problem Statement

Modern knowledge work is highly fragmented. Notes are kept in one app, tasks in another, book highlights in a third, and portfolio content on a separate blogging host. This fragmentation leads to:
1. **Cognitive Leakage**: Valuable ideas are written down but lost because they aren't connected to active projects or goals.
2. **Data Vulnerability**: Reliance on commercial SaaS platforms exposes the owner's lifetime intellectual output to data loss, vendor lock-in, and interface changes.
3. **High Maintenance Overhead**: Running separate systems for personal knowledge management, work tracking, and public portfolio publishing requires constant integration work.

## Product Goals

- **Single Source of Truth**: Centralize all cognitive assets (notes, ideas, books, projects, learnings) in one permanent database.
- **Cognitive Compounding**: Ensure that every new piece of information is linked to existing information, building a compound interest engine of knowledge.
- **Operational Simplicity**: Minimize the friction of publishing internal insights to the public web by building a direct pipeline.
- **Architectural Longevity**: Implement a codebase that requires minimal maintenance and remains easily readable for over ten years.

## Target Users

The primary user of the private Workspace is the owner (creator, researcher, developer). The secondary users of the Public Web are visitors: hiring managers, collaborators, readers, and automated web indexing agents seeking structured information on the owner's expertise.

## User Problems

- "I read books and take highlights, but I never review them when executing actual projects."
- "I want to publish my learning progress publicly, but the process of copying notes from my personal workspace to a blog platform is too high-friction."
- "I want a clean, lightning-fast personal website, but I don't want to maintain a separate CMS database."
- "I want to write scripts to analyze my productivity or reading habits, but my data is locked behind proprietary APIs."

## Product Capabilities

Rifqi's capabilities are organized by functional domains rather than layout pages.

### Create
- **Content Ingestion**: The system must ingest raw markdown files, text notes, and structured database entries representing new thoughts, book annotations, or tasks.
- **Entity Initialization**: The system must support the initialization of core entities (Ideas, Learnings, Projects, Articles, Books, Goals, Journey Events) with standardized metadata schema.

### Organize
- **Taxonomy Mapping**: The system must allow categorizing entities using a strict taxonomy (such as Domains, Tags, and Statuses).
- **Work Management**: The system must support managing task execution workflows, linking sub-tasks to parent projects and overarching goals.

### Connect
- **Semantic Relationship Modeling**: The system must support the creation of explicit, typed relationships between entities (e.g., Book *inspires* Idea, Article *references* Project).
- **Backlink Generation**: The system must automatically compute and display bidirectional links (backlinks) between all connected nodes in the knowledge graph.

### Discover & Search
- **Unified Global Search**: The system must index all content and metadata to provide full-text search capabilities with near-zero latency.
- **Graph Traversal**: The system must support traversing related entities programmatically, allowing users to navigate from a Technology entity to all linked Projects, Learnings, and Articles.

### Analyze
- **Semantic Connectivity Auditing**: The system must calculate and report metrics on the health of the knowledge graph (e.g., identifying orphaned notes, measuring metadata completion, auditing link density).
- **Execution Tracking**: The system must calculate progress metrics for Projects and Goals based on completed sub-tasks and milestones.

### Publish
- **State Promotion Pipeline**: The system must manage a state pipeline that transitions drafts from private workspace configurations to public-ready assets.
- **Static Site Compilation**: The system must compile public entities into high-performance, SEO-optimized web structures.

## Product Scope

### In-Scope
- The private administrative Studio workspace application.
- The public-facing Web presentation application.
- Shared packages for database migrations, authentication validation, shared UI components, typescript definitions, and utility tools.
- Strict Markdown parsing pipeline with custom metadata processing.
- Graph relationships stored in a relational database.

### Out-of-Scope (in Sprint 0)
- Multi-user support (the platform is strictly single-tenant).
- Social networking features (comments, likes, shares, user accounts).
- Rich-text WYSIWYG editors (all text editing is done in Markdown).
- Direct external app integrations (e.g., syncing with Notion, Todoist, or Jira).
- Automated AI generation (AI features will be focused on retrieval and search optimization in later phases).

## Success Criteria

- **Zero Data Loss**: Database migrations and updates must not result in the corruption or loss of Markdown notes or entity relations.
- **100% SEO Compliance**: All public pages must meet standard accessibility and search crawler optimization practices automatically.
- **Zero Orphaned Entities**: The knowledge connectivity analyzer must prove that every entity added is linkable.

---

## References
- [Masterplan](file:///e:/rifqi.id/docs/00-masterplan/MASTERPLAN.md)
- [Product Principles](file:///e:/rifqi.id/docs/01-product/02-Product-Principles.md)

## Decision Log
- **2026-06-26**: Initialization of the PRD by CTO. Status set to Approved.
