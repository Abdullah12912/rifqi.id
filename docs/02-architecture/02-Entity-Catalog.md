# Entity Catalog

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Purpose

The Entity Catalog defines the canonical conceptual models of the Rifqi platform. It acts as the single source of truth for database design, API design, and type definitions. It establishes the purpose, capabilities, lifecycles, and relational constraints of every system entity, ensuring architectural alignment without declaring database fields or technology-specific types.

---

## 1. Workspace
- **Identity**: Unique workspace identifier (UUID/slug).
- **Purpose**: Represents the root administrative container and config context for the owner's Digital Headquarters.
- **Description**: The top-level root configuration and operational environment holding all projects, entities, preferences, and data domains.
- **Lifecycle**: Active -> Archived.
- **Ownership**: System (Only one active Workspace exists per instance).
- **Visibility**: Private.
- **Relationships**: Owns all other entities in the system.
- **Capabilities**: Initializing system configuration, loading preferences, auditing integrity, orchestrating data sync.
- **Metadata**: Owner user reference, system settings, last verified timestamp.
- **Future Extensions**: Multi-workspace syncing, team-workspace collaboration bridges.

---

## 2. Project
- **Identity**: Unique project identifier (UUID/slug).
- **Purpose**: Models a structured initiative aimed at achieving a specific objective.
- **Description**: A primary workspace unit containing milestones, linked tasks, learnings, and technology declarations.
- **Lifecycle**: Draft -> Planning -> Active -> Paused -> Completed -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Private by default; promotes to Public when marked for publication and linked to a public milestone.
- **Relationships**: Owns Milestones and Tasks; references Goals, Technologies, Books, Learnings, and Media.
- **Capabilities**: Recalculating progress, archiving sub-tasks, exporting history, linking timeline milestones.
- **Metadata**: Target completion date, progress ratio, category, primary domains.
- **Future Extensions**: Auto-dependency mapping, interactive budget tracking.

---

## 3. Article
- **Identity**: Unique article slug/UUID.
- **Purpose**: Represents a polished written piece of content destined for public web readers.
- **Description**: Public-facing writing that presents conceptual insights, tutorials, or syntheses of the owner's work.
- **Lifecycle**: Draft -> Review -> Published -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Private in Draft/Review states; Public in Published state.
- **Relationships**: References Projects, Learnings, Books, Media, Tags, and Categories.
- **Capabilities**: Compiling to static web format, stripping private metadata, resolving internal entity slugs to public links.
- **Metadata**: Publication date, reading time estimate, SEO description, language code.
- **Future Extensions**: Cross-publishing pipelines (e.g. Medium, newsletter distribution).

---

## 4. Learning
- **Identity**: Unique learning slug/UUID.
- **Purpose**: Stores structured personal knowledge nodes synthesized from research, study, or project execution.
- **Description**: The verified core of the second brain, documenting lessons learned, conceptual definitions, and technical solutions.
- **Lifecycle**: Raw Draft -> Curated -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Private by default; can be individually marked for public viewing on the Web portal.
- **Relationships**: References Books, Ideas, Technologies, and Projects; references other Learnings.
- **Capabilities**: Semantic linking, self-auditing connection density, exposing content to search indexes.
- **Metadata**: Domain tag, revision count, verification source type.
- **Future Extensions**: Automated flashcard generation, concept spaced-repetition schedules.

---

## 5. Journey Event
- **Identity**: Unique event identifier (UUID/slug).
- **Purpose**: Logs a significant professional, personal, or educational milestone.
- **Description**: A chronological timeline item detailing key moments in the owner's life, career, or repository.
- **Lifecycle**: Draft -> Published -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Public by default when active; can be private for internal journaling.
- **Relationships**: References Projects, Technologies, and Media.
- **Capabilities**: Formatting to timeline layouts, compiling chronologically, linking portfolio items.
- **Metadata**: Event date, primary role, location, importance scale.
- **Future Extensions**: Interactive career timeline maps, resume PDF exports.

---

## 6. Goal
- **Identity**: Unique goal identifier (UUID/slug).
- **Purpose**: Establishes high-level long-term milestones that direct projects and learnings.
- **Description**: Strategic objectives representing target achievements in skill acquisition, project development, or personal milestones.
- **Lifecycle**: Active -> Suspended -> Achieved -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Private by default; public view optional.
- **Relationships**: Coordinates multiple Projects and Learnings; owns target metric check-ins.
- **Capabilities**: Aggregating project progress, evaluating metric completion, flagging delayed projects.
- **Metadata**: Target year, success metrics definition, importance tier.
- **Future Extensions**: Sub-goal nesting support, third-party metric sync.

---

## 7. Technology
- **Identity**: Unique technology slug.
- **Purpose**: Catalogs languages, libraries, tools, and frameworks used in projects.
- **Description**: A system-wide taxonomy node denoting expertise and stack configuration.
- **Lifecycle**: Active -> Deprecated.
- **Ownership**: Workspace.
- **Visibility**: Public (Acts as a system-wide tag).
- **Relationships**: References Projects, Learnings, Articles, and Goals.
- **Capabilities**: Generating stack catalogs, linking skill development timelines.
- **Metadata**: Category (Language, Framework, Tool), documentation URL, proficiency level.
- **Future Extensions**: Automated package dependency version checking in workspace.

---

## 8. Book
- **Identity**: Unique ISBN/UUID slug.
- **Purpose**: Records publications read by the owner that serve as source material for learnings.
- **Description**: Metadata record of books, academic papers, or major reference manuals.
- **Lifecycle**: To Read -> Reading -> Completed -> Abanadoned.
- **Ownership**: Workspace.
- **Visibility**: Private by default; public when linked to public reviews or articles.
- **Relationships**: Generates Ideas and Learnings; referenced by Projects and Articles.
- **Capabilities**: Importing citation metadata, calculating reading pace, logging reading logs.
- **Metadata**: Author, publisher, read dates, rating, book categories.
- **Future Extensions**: Syncing annotations from external reading applications.

---

## 9. Media
- **Identity**: Unique media identifier (UUID/hash).
- **Purpose**: Represents files, images, videos, or documents uploaded to the platform.
- **Description**: A wrapper entity containing the file binary metadata, sizing, and deployment paths.
- **Lifecycle**: Raw -> Processing -> Active -> Deleted.
- **Ownership**: Workspace.
- **Visibility**: Matches the visibility of the parent entity it is attached to.
- **Relationships**: Linked to Articles, Projects, Journey Events, and Books.
- **Capabilities**: Compressing images, generating responsive dimensions, verifying file hash signatures.
- **Metadata**: File size, mime type, dimensions, file hash, alt description text.
- **Future Extensions**: AI image search auto-tagging.

---

## 10. Research
- **Identity**: Unique research session UUID.
- **Purpose**: Models active research inquiries on specific concepts or queries.
- **Description**: An orchestrator entity tracking literature reviews, search logs, and citation networks.
- **Lifecycle**: Active -> Closed.
- **Ownership**: Workspace.
- **Visibility**: Private.
- **Relationships**: References Books, Learnings, Ideas, and Resources.
- **Capabilities**: Aggregating query history, tracking citations, exporting bibliography lists.
- **Metadata**: Query string, domain tag, research logs.
- **Future Extensions**: Automated literature search API fetches.

---

## 11. Idea
- **Identity**: Unique idea UUID.
- **Purpose**: Captures unrefined, quick-capture thoughts before they graduate to structured entities.
- **Description**: An ephemeral scratchpad entry recording insights, snippets, or draft ideas.
- **Lifecycle**: New -> Processing -> Graduated -> Dismissed.
- **Ownership**: Workspace.
- **Visibility**: Private.
- **Relationships**: Can graduate into a Learning, Project, or Article; references Books and Media.
- **Capabilities**: Quick-capture ingestion, markdown conversion, target entity graduation.
- **Metadata**: Capture source (Mobile, Web, Voice), draft content, primary tags.
- **Future Extensions**: Voice-to-text transcript auto-tagging.

---

## 12. Resource
- **Identity**: Unique resource URL/UUID.
- **Purpose**: References external URLs, documents, or tools relevant to projects and learnings.
- **Description**: A wrapper for external documentation links, assets, and websites.
- **Lifecycle**: Active -> Dead Link -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Private by default; public when linked to public Articles.
- **Relationships**: References Technologies, Projects, and Learnings.
- **Capabilities**: Link health checking, scraping page titles.
- **Metadata**: Target URL, page title, description, HTTP status log.
- **Future Extensions**: Webpage archiver integration (saving offline HTML snapshot).

---

## 13. Tag
- **Identity**: Unique tag slug.
- **Purpose**: Enforces ad-hoc semantic categorization across all content entities.
- **Description**: Lightweight label system representing specific keywords or topics.
- **Lifecycle**: Active -> Dormant.
- **Ownership**: Workspace.
- **Visibility**: Public/Private based on the entities it tags.
- **Relationships**: Applies to Articles, Learnings, Books, Ideas, and Projects.
- **Capabilities**: Aggregating tagged counts, merging tags, matching synonyms.
- **Metadata**: Title, color code, description.
- **Future Extensions**: AI tag suggestion.

---

## 14. Category
- **Identity**: Unique category slug.
- **Purpose**: Defines hierarchical primary classifications for entities.
- **Description**: Structured taxonomic categories forming tree structures (e.g. Software Development -> Backend -> Databases).
- **Lifecycle**: Active -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Public.
- **Relationships**: Categorizes Articles, Projects, and Books; owns parent/child categories.
- **Capabilities**: Rendering category trees, aggregating entity distributions.
- **Metadata**: Title, icon identifier, parent category reference.
- **Future Extensions**: Automatic classification based on content analysis.

---

## 15. Collection
- **Identity**: Unique collection identifier (UUID/slug).
- **Purpose**: Manually groups arbitrary entities around curated themes or portals.
- **Description**: A playlist-like entity allowing the owner to bundle learnings, projects, and articles into focused curriculum paths.
- **Lifecycle**: Draft -> Active -> Archived.
- **Ownership**: Workspace.
- **Visibility**: Private by default; public view toggleable.
- **Relationships**: Contains Articles, Learnings, Projects, and Media.
- **Capabilities**: Re-ordering list members, compiling collection overview layouts.
- **Metadata**: Title, thematic description, custom display order schema.
- **Future Extensions**: Collaborative shared collections.

---

## 16. Relationship
- **Identity**: Unique relationship identifier (UUID).
- **Purpose**: Models typed semantic edges between any two entities in the knowledge graph.
- **Description**: The relational glue of the system, defining how two entities are connected (e.g. Book *inspires* Learning).
- **Lifecycle**: Active -> Suspended.
- **Ownership**: Workspace.
- **Visibility**: Public if both connected entities are public; private if either is private.
- **Relationships**: Connects target source entity to destination entity.
- **Capabilities**: Validating relationship type constraints, updating graph edges, exporting link paths.
- **Metadata**: Relationship type code, weight parameter, bidirectional flags.
- **Future Extensions**: Automatic relation inference.

---

## 17. Permission
- **Identity**: Unique permission code slug.
- **Purpose**: Controls administrative and read access keys across system layers.
- **Description**: Security constraints mapping roles or tokens to operational capabilities in the Studio workspace.
- **Lifecycle**: Permanent.
- **Ownership**: System.
- **Visibility**: Private.
- **Relationships**: Applies to Users.
- **Capabilities**: Evaluating action authorization.
- **Metadata**: Permission rule definitions.
- **Future Extensions**: Multi-token programmatic API keys.

---

## 18. User
- **Identity**: Unique user identifier (UUID/email).
- **Purpose**: Models the identity of the owner and system administrator.
- **Description**: An operational actor entity holding security hashes, login history, and personal details.
- **Lifecycle**: Active -> Suspended.
- **Ownership**: System.
- **Visibility**: Private.
- **Relationships**: Owns Workspace; holds Permissions.
- **Capabilities**: Authentication, key generation, preference management.
- **Metadata**: Email address, password security hash, multi-factor settings, session tokens.
- **Future Extensions**: OAuth identity provider linkages.

---

## References
- [Product Language](file:///e:/rifqi.id/docs/01-product/05-Product-Language.md)
- [Bounded Context](file:///e:/rifqi.id/docs/01-product/08-Bounded-Context.md)

## Decision Log
- **2026-06-26**: Initialization of the 18 core entities of the Rifqi platform by Senior Software Engineer. Status set to Approved.
