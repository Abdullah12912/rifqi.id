# Lifecycle Model

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Purpose

The Lifecycle Model document defines the state progression matrices for all major entities in the Rifqi platform. It establishes the allowed states, valid state transitions, and the system rules that govern each state transition, ensuring data consistency and lifecycle integrity.

## Context

Entities do not exist in static states; they graduate from inception (ideas, drafts) to completion (published, completed) and eventual preservation (archived). Defining state machines prevents invalid state transitions (e.g. publishing an unreviewed article, or completing a project with active blockages) and guides the implementation of event triggers.

---

## Entity Lifecycle Transitions

### 1. Workspace
- **States**: `Active` -> `Archived`
- **Transition Flow**: Only one Workspace exists. It can be archived during system deprecation or backups.
- **Rules**: Transitioning to `Archived` locks all database writes across the entire system.

### 2. Project
- **States**: `Draft` -> `Planning` -> `Active` -> `Paused` -> `Completed` -> `Archived`
- **Transition Flow**:
  - `Draft` to `Planning`: Initiated when objectives are defined.
  - `Planning` to `Active`: Set when execution tasks are initialized and stack technologies are linked.
  - `Active` to `Paused`: Triggered manually due to blockages.
  - `Active` to `Completed`: Allowed only when all mandatory child Tasks are checked completed.
  - `Completed` to `Archived`: Sets project to read-only history.
- **Rules**: Cannot move from `Draft` directly to `Completed`.

### 3. Article
- **States**: `Draft` -> `Review` -> `Published` -> `Archived`
- **Transition Flow**:
  - `Draft` to `Review`: Content writing is complete; ready for metadata auditing and preview checks.
  - `Review` to `Published`: Passes publication validation and is built to the public Web app.
  - `Published` to `Archived`: Removed from public views but preserved in the Workspace database.
- **Rules**: Moving to `Published` automatically triggers the Publishing Engine compilation.

### 4. Learning
- **States**: `Raw Draft` -> `Curated` -> `Archived`
- **Transition Flow**:
  - `Raw Draft` to `Curated`: Initiated when formatting, bibliography, and at least one semantic relationship link is saved.
  - `Curated` to `Archived`: Kept for historical reference but hidden from global workspace suggestion sidebars.
- **Rules**: A Learning must connect to at least one entity (Book, Project, Technology) to transition to `Curated`.

### 5. Journey Event
- **States**: `Draft` -> `Published` -> `Archived`
- **Transition Flow**:
  - `Draft` to `Published`: Commits the timeline log to the public Web portfolio.
  - `Published` to `Archived`: Hidden from public timeline view.

### 6. Goal
- **States**: `Active` -> `Suspended` -> `Achieved` -> `Archived`
- **Transition Flow**:
  - `Active` to `Suspended`: On-hold.
  - `Active` to `Achieved`: Triggered when related target metrics or linked projects are completed.
  - `Achieved` to `Archived`: Read-only historical cataloging.

### 7. Book
- **States**: `To Read` -> `Reading` -> `Completed` -> `Abandoned`
- **Transition Flow**:
  - `To Read` to `Reading`: Start reading logging is triggered.
  - `Reading` to `Completed`: Finished reading logged; prompts user to synthesize remaining Ideas into Learnings.
  - `Reading` to `Abandoned`: Halted reading.

### 8. Idea
- **States**: `New` -> `Processing` -> `Graduated` -> `Dismissed`
- **Transition Flow**:
  - `New` to `Processing`: Captured note is opened and evaluated in the Workspace.
  - `Processing` to `Graduated`: Transformed into a Learning, Project, or Article entity.
  - `Processing` to `Dismissed`: Deleted or archived without action.
- **Rules**: Graduation requires choosing a target entity type and mapping content to its schema.

### 9. Collection
- **States**: `Draft` -> `Active` -> `Archived`
- **Transition Flow**:
  - `Draft` to `Active`: Public catalog goes live on the Web.
  - `Active` to `Archived`: Collection page deprecated.

### 10. Media
- **States**: `Raw` -> `Processing` -> `Active` -> `Deleted`
- **Transition Flow**:
  - `Raw` to `Processing`: File uploaded; compression, optimization, and responsive sizing scripts running.
  - `Processing` to `Active`: File ready; CDN path generated.
  - `Active` to `Deleted`: Binary file removed from storage.
- **Rules**: Cannot use a Media asset in an Article while it is in the `Processing` state.

---

## State Transition Diagram (Examples)

```mermaid
stateDiagram-v2
    [*] --> ProjectDraft : Create Project
    ProjectDraft --> ProjectPlanning : Define Objectives
    ProjectPlanning --> ProjectActive : Start Tasks
    ProjectActive --> ProjectPaused : Blocked
    ProjectPaused --> ProjectActive : Resume
    ProjectActive --> ProjectCompleted : Tasks Complete
    ProjectCompleted --> ProjectArchived : Archive
    ProjectArchived --> [*]

    --
    [*] --> ArticleDraft : Create Note
    ArticleDraft --> ArticleReview : Complete Writing
    ArticleReview --> ArticlePublished : Publish Validation Pass
    ArticlePublished --> ArticleArchived : Deprecate
    ArticleArchived --> [*]
```

---

## References
- [Entity Catalog](file:///e:/rifqi.id/docs/02-architecture/02-Entity-Catalog.md)
- [Relationship Matrix](file:///e:/rifqi.id/docs/02-architecture/05-Relationship-Matrix.md)

## Decision Log
- **2026-06-26**: Defining lifecycle states and transition rules for all core entities by Senior Software Engineer. Status set to Approved.
