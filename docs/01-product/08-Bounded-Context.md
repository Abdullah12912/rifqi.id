# Bounded Context

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Purpose

The purpose of this document is to define the logical boundaries of the Rifqi platform. By explicitly defining what lies within the core domain model, what is deferred to future milestones, and what is permanently out of scope, we establish a rigid perimeter for the system's architecture. This serves as the foundational reference for Domain-Driven Design (DDD) during the subsequent Architecture Foundation phases, preventing scope creep and architectural decay.

## Context

In Domain-Driven Design, a bounded context defines the boundary within which a particular domain model applies. Rifqi acts as a Digital Headquarters, serving as the central coordinator for the owner's intellectual assets and projects. To keep the codebase maintainable across a multi-decade lifespan, the system must enforce strict conceptual boundaries. Every entity, service, and database schema must belong to exactly one defined domain, preventing cross-domain pollution and circular dependencies.

## Core Domains

These domains are the primary areas of focus for the initial releases of the Digital Headquarters. They represent the essential capabilities that the platform must deliver.

### 1. Knowledge
- **Entity Scope**: Books, Ideas, concepts, and reading notes.
- **Responsibility**: Ingestion, processing, storage, and semantic representation of intellectual research material.
- **Boundary**: Does not manage publishing statuses or layout styles; focuses strictly on conceptual storage and source mapping.

### 2. Project
- **Entity Scope**: Projects, milestones, and high-level deliverables.
- **Responsibility**: Orchestrating initiatives, mapping deliverables to timelines, and linking execution items to goals.
- **Boundary**: Tracks execution context, but does not implement low-level interactive daily task reminders or external calendar syncs.

### 3. Article
- **Entity Scope**: Articles, drafts, revisions, and public publications.
- **Responsibility**: The publishing pipeline, draft promotion, formatting compliance, and Web presentation output.
- **Boundary**: Governs public-facing text assets, distinct from raw ideas and internal learning notes.

### 4. Learning
- **Entity Scope**: Learnings, conceptual definitions, synthesis notes.
- **Responsibility**: Houses structured personal knowledge and expertise records, mapping what has been learned and verified through projects or study.
- **Boundary**: Represents validated personal facts and lessons, sitting between raw Ideas and published public Articles.

### 5. Journey
- **Entity Scope**: Journey Events, history records, personal timeline logs.
- **Responsibility**: Maintaining a verified historical ledger of the owner's professional milestones, projects, and life transitions.
- **Boundary**: Slices through history chronologically; does not manage active task tracking or project execution.

### 6. Goal
- **Entity Scope**: Goals, long-term objectives, aspirational metrics.
- **Responsibility**: Coordinating long-term achievements, mapping related Projects and Learnings to general directions.
- **Boundary**: High-level alignment layer; does not contain daily tasks or execution-level details.

### 7. Technology
- **Entity Scope**: Technologies, tools, frameworks, skills.
- **Responsibility**: Cataloging stack elements used across Projects and studied in Learnings, serving as a unified taxonomy tag.
- **Boundary**: Strictly taxonomy metadata; does not compile or interface with the tools themselves.

### 8. Media
- **Entity Scope**: Media assets, images, files, uploads.
- **Responsibility**: Organizing static binary resources, executing optimization/compression pipelines, and managing public CDN pathways.
- **Boundary**: Handles files and assets, decoupling content text formatting from raw binary storage.

### 9. Research
- **Entity Scope**: Bibliographies, search queries, external reference links.
- **Responsibility**: Managing research workflows, executing deep queries across internal knowledge, and mapping connections to external sources.
- **Boundary**: Captures research metadata and query indices; does not store external webpage copies.

---

## Future Domains

These domains are recognized as valuable extensions of the platform but are deferred to future milestones. Their architectures must be accommodated by the foundation, but no logic or database schemas will be built in the initial phase.

### 1. Calendar
- **Scope**: Scheduling, event tracking, and timeline coordination.
- **Deferred Reason**: Managing calendars requires complex time-zone, repeating event, and external calendar synchronization protocols.

### 2. Task Management
- **Scope**: Granular task lists, checklists, daily schedules, and interactive reminders.
- **Deferred Reason**: Micro-task tracking requires rapid interactive UI interfaces and push notifications, which are secondary to the core knowledge and project modeling layers.

### 3. Automation
- **Scope**: Workflow triggers, webhooks, automatic backups, and background data synchronization pipelines.
- **Deferred Reason**: Establishing a stable, static data layer must precede building active background automation routines.

### 4. Notifications
- **Scope**: Alerting services, system logs, email dispatchers, and workspace flags.
- **Deferred Reason**: Single-user platforms require minimal active notification systems in the initial phase; pull-based logs are sufficient.

---

## Explicitly Out of Scope

These domains are intentionally excluded from the Rifqi platform. Attempting to integrate them would introduce unnecessary complexity, bloat the codebase, and dilute the product's focus.

### 1. CRM (Customer Relationship Management)
- **Excluded Reason**: Rifqi is a Digital Headquarters for the owner's internal knowledge and projects, not a contact manager, lead pipeline, or sales tracker. Introducing CRM models introduces complex contact structures and communication logs that have no place in a personal second brain.

### 2. Accounting
- **Excluded Reason**: Financial ledger tracking, invoicing, tax calculations, and expense management are highly specialized domains that require strict regulatory compliance. These capabilities should be handled by specialized third-party software, not custom operating systems.

### 3. ERP (Enterprise Resource Planning)
- **Excluded Reason**: Rifqi is a personal workspace, not an enterprise resource manager. Multi-user role matrices, inventory flows, procurement systems, and human resource modules are fundamentally incompatible with the single-tenant scope of the project.

### 4. Social Network
- **Excluded Reason**: Interactive social features like user profiles, comments, likes, social feeds, and peer communication systems increase operational overhead, expose the server to malicious input, and deviate from the private, cognitive purpose of the Workspace.

### 5. Generic CMS (Content Management System)
- **Excluded Reason**: The publishing system is custom-tailored to the owner's structured entities (Articles, Projects, Learnings). Building a generic CMS that supports arbitrary schemas, user permission rings, or multi-tenant blogging blocks creates general-purpose software bloat.

---

## References
- [Masterplan](file:///e:/rifqi.id/docs/00-masterplan/MASTERPLAN.md)
- [PRD](file:///e:/rifqi.id/docs/01-product/03-PRD.md)
- [Product Language](file:///e:/rifqi.id/docs/01-product/05-Product-Language.md)

## Decision Log
- **2026-06-26**: Initialization of Bounded Context document following ECR-001 by CTO. Status set to Approved.
