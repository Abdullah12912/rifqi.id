# Relationship Matrix

- **Version**: 1.0
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Purpose

The Relationship Matrix defines the precise semantic relationships connecting the conceptual entities of the Rifqi platform. By explicitly defining the connection types (Owns, Contains, References, Depends On, Generates, Publishes, Categorizes, Associates, Extends), we establish the constraints for database schemas and graph traversal pipelines.

## Context

In an entity-driven architecture, data is defined by its connections. An isolated note has limited utility; a note linked to a book, a technology, and a project becomes a valuable conceptual asset. This matrix acts as the design blueprint for foreign key constraints, relationship tables, and graph edges.

---

## Relationship Type Definitions

- **Owns**: Absolute parent-child ownership. If the parent is deleted, the child must cascade-delete (e.g. Project owns Tasks).
- **Contains**: Grouping without absolute lifetime coupling. Removing a container does not delete its children (e.g. Collection contains Articles).
- **References**: Directional lookup link. Non-cascading reference (e.g. Learning references Technology).
- **Depends On**: Functional requirement constraint (e.g. Project depends on Technology).
- **Generates**: Creative origin link (e.g. Book generates Ideas).
- **Publishes**: Compilation target promotion (e.g. Workspace publishes Web).
- **Categorizes**: Structural classification link (e.g. Category categorizes Articles).
- **Associates**: General semantic bidirectional edge (e.g. Idea associates with Idea).
- **Extends**: Subtype or expansion pattern (e.g. Goal extends Project outcomes).

---

## Entity Relationship Table

This table maps the key active semantic links between system entities.

| Source Entity | Target Entity | Relationship Type | Description |
|---|---|---|---|
| **Workspace** | Project, Article, Goal... | **Owns** | Workspace serves as the root container for all entities. |
| **Workspace** | User | **Contains** | Workspace contains authenticated system users. |
| **User** | Permission | **Owns** | User owns security permissions and access keys. |
| **Goal** | Project | **Extends** | Goal coordinates and extends multiple Projects' targets. |
| **Goal** | Learning | **References** | Goal references Learnings representing acquired competencies. |
| **Project** | Task | **Owns** | Project owns individual actionable Tasks (cascades). |
| **Project** | Technology | **Depends On** | Project execution depends on specific Technologies. |
| **Project** | Media | **Contains** | Project contains related design and illustration Media. |
| **Project** | Goal | **References** | Project references a parent Goal it contributes to. |
| **Article** | Media | **Contains** | Article embeds specific illustrated Media. |
| **Article** | Category | **References** | Category categorizes the published Article. |
| **Article** | Tag | **References** | Tag indexes the Article under specific keywords. |
| **Article** | Learning | **References** | Article references specific research Learnings. |
| **Article** | Project | **References** | Article references related Projects to show live progress. |
| **Learning** | Book | **References** | Learning references a source Book it was derived from. |
| **Learning** | Technology | **References** | Learning notes document details on specific Technologies. |
| **Learning** | Project | **References** | Learning links back to the Project where it was validated. |
| **Learning** | Idea | **Depends On** | Learning graduates and depends on initial Ideas. |
| **Book** | Idea | **Generates** | Book reading notes generate raw system Ideas. |
| **Book** | Media | **References** | Book references its cover design Media. |
| **Research** | Book | **References** | Research session references specific source Books. |
| **Research** | Learning | **Contains** | Research collects related Learnings. |
| **Idea** | Media | **Contains** | Raw Idea embeds quick-capture Media attachments. |
| **Idea** | Technology | **References** | Idea references targeted Technologies. |
| **Collection** | Article | **Contains** | Collection groups multiple compiled Articles. |
| **Collection** | Learning | **Contains** | Collection packages related Learnings into curricula. |
| **Relationship** | Any Entity | **Associates** | Relationship models semantic edges connecting any two nodes. |

---

## Conceptual Grid Matrix

A visual representation of allowed directional relationships between core entities.

```text
            WRK  USR  GOL  PRJ  ART  LRN  BOK  RES  IDA  MED  CAT  TAG  COL
WRK (Workspace)  O    O    O    O    O    O    O    O    O    O    O    O    O
USR (User)       .    .    O    .    .    .    .    .    .    .    .    .    .
GOL (Goal)       .    .    .    R    .    R    .    .    .    .    .    .    .
PRJ (Project)    .    .    R    .    .    .    .    .    .    C    .    .    .
ART (Article)    .    .    .    R    .    R    R    .    .    C    R    R    .
LRN (Learning)   .    .    .    R    .    .    R    .    D    .    R    R    .
BOK (Book)       .    .    .    .    .    .    .    .    G    R    .    .    .
RES (Research)   .    .    .    .    .    C    R    .    .    .    .    .    .
IDA (Idea)       .    .    .    .    .    .    .    .    .    C    .    .    .
MED (Media)      .    .    .    .    .    .    .    .    .    .    .    .    .
CAT (Category)   .    .    .    .    .    .    .    .    .    .    .    .    .
TAG (Tag)        .    .    .    .    .    .    .    .    .    .    .    .    .
COL (Collection) .    .    .    .    C    C    .    .    .    .    .    .    .
```
*Legend: **O** = Owns, **C** = Contains, **R** = References, **D** = Depends On, **G** = Generates, **.** = No Direct Relationship*

---

## References
- [Entity Catalog](file:///e:/rifqi.id/docs/02-architecture/02-Entity-Catalog.md)
- [Domain Model](file:///e:/rifqi.id/docs/02-architecture/03-Domain-Model.md)

## Decision Log
- **2026-06-26**: Creation of the grid matrix and relationship definitions by Senior Software Engineer. Status set to Approved.
