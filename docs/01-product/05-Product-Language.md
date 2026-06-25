# Product Language

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Official Vocabulary

This section defines the official vocabulary of the Rifqi platform. Consistency in naming prevents communication confusion and guarantees that the database schemas, TypeScript interfaces, and UI elements match the exact domain models.

### 1. Digital Headquarters
- **Definition**: The complete personal operating system repository, including both the private studio application and the public web portal.
- **Allowed**: Digital Headquarters, HQ.
- **Forbidden**: Site, Website, System, Platform, Suite.

### 2. Workspace
- **Definition**: The private administrative environment (named Studio) where the owner ingests data, manages projects, and curates knowledge.
- **Allowed**: Workspace, Studio.
- **Forbidden**: Admin, Admin Panel, Backoffice, Dashboard.

### 3. Web
- **Definition**: The public-facing presentation application that displays curated data from the Digital Headquarters.
- **Allowed**: Web, Public Portal.
- **Forbidden**: Frontend, Website, Blog, Portfolio.

### 4. Project
- **Definition**: A structured, long-term initiative with a specific objective, containing tasks, milestones, and links to other concepts.
- **Allowed**: Project.
- **Forbidden**: Epic, Campaign, Initiative.

### 5. Task
- **Definition**: A single, actionable execution unit belonging to a Project or Goal.
- **Allowed**: Task.
- **Forbidden**: Todo, Item, Issue, Ticket.

### 6. Goal
- **Definition**: A high-level, long-term aspirational milestone that coordinates multiple Projects and Learnings.
- **Allowed**: Goal.
- **Forbidden**: Objective, Target, Milestone.

### 7. Article
- **Definition**: A highly polished, written piece of work destined for public reading on the Web application.
- **Allowed**: Article.
- **Forbidden**: Blog, Post, Writing, Newsletter.

### 8. Learning
- **Definition**: A structured documentation node representing verified personal knowledge, synthesized from books, courses, or experiments.
- **Allowed**: Learning.
- **Forbidden**: Note, Snippet, Memo, Fact.

### 9. Book
- **Definition**: A record of a physical or digital publication read by the owner, serving as a primary source for Ideas and Learnings.
- **Allowed**: Book.
- **Forbidden**: Reading, Reference, Source.

### 10. Idea
- **Definition**: A raw, unrefined thought or draft note capturing an inspiration before it is graduated into a Learning, Project, or Article.
- **Allowed**: Idea.
- **Forbidden**: Scratchpad, Draft, Thought, Clip.

### 11. Technology
- **Definition**: A specific programming language, library, tool, or framework used in Projects or studied in Learnings.
- **Allowed**: Technology, Stack.
- **Forbidden**: Tool, Library, Skill.

### 12. Journey Event
- **Definition**: A timeline log entry capturing a significant real-world event, milestone, or transition in the owner's life.
- **Allowed**: Journey Event.
- **Forbidden**: Timeline, Event, Milestone, Log.

### 13. Media
- **Definition**: Static assets (images, videos, documents, audio clips) linked to entities.
- **Allowed**: Media, Asset.
- **Forbidden**: Image, File, Upload, Attachment.

---

## Vocabulary Validation Rules

1. **Database Schema Naming**: Tables must match singular lowercase names of the core entities (e.g. `project`, `article`, `learning`, `journey_event`, `book`, `goal`, `idea`, `technology`, `task`, `media`).
2. **Component & Class Naming**: All software classes, interfaces, and UI directories must use the singular title case equivalent (e.g. `ProjectService`, `ArticleCard`, `JourneyEvent`).
3. **UI Text Constraints**: The public website and private workspace must never display the forbidden terms. For instance, the button to publish an Article must say "Publish Article", never "Post Blog" or "Publish Writing".

---

## References
- [Masterplan](file:///e:/rifqi.id/docs/00-masterplan/MASTERPLAN.md)
- [PRD](file:///e:/rifqi.id/docs/01-product/03-PRD.md)

## Decision Log
- **2026-06-26**: Initialization of the official Product Language definitions by CTO. Status set to Approved.
