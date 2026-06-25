# Success Metrics

- **Version**: 1.1
- **Status**: Approved
- **Owner**: CTO
- **Last Updated**: 2026-06-26

---

## Metric 1: Documentation Coverage
- **Metric Definition**: The percentage of modules, public packages, and APIs in the codebase that contain up-to-date documentation files (such as README files or architectural docs).
- **Measurement Method**: Calculated as:
  \[\text{Documentation Coverage} = \frac{\text{Modules with README or Docs}}{\text{Total Count of Modules}} \times 100\]
- **Target Threshold**: \(\ge 95\%\).
- **Actionable Correction**: If coverage drops, git validation pre-commit hooks or CI checks will trigger warning logs, block production builds, and flag undocumented modules during local compiles.

## Metric 2: Search Coverage
- **Metric Definition**: The percentage of entities (Articles, Learnings, Projects, Books) that are indexed and searchable via the global search functionality.
- **Measurement Method**: Verifying that the search index count matches the database record count. Calculated as:
  \[\text{Search Coverage} = \frac{\text{Indexed Entities}}{\text{Total Database Entities}} \times 100\]
- **Target Threshold**: \(100\%\).
- **Actionable Correction**: A local CLI script audit will identify database records missing from the search index and re-index them automatically.

## Metric 3: Connected Knowledge Growth (North Star Metric)
- **Metric Definition**: The net monthly expansion of semantically connected entities (entities with at least one active relation to another entity) within the database.
- **Measurement Method**: Calculated as:
  \[\text{Connected Knowledge Growth (CKG)} = C_t - C_{t-1}\]
  Where \(C_t\) is the count of connected entities at the end of the current month, and \(C_{t-1}\) is the count at the end of the previous month.
- **Target Threshold**: \(\ge 15\) new connected entities per month.
- **Actionable Correction**: If growth falls below the threshold, the Studio workspace will prompt the owner with content creation suggestions, highlighting partially drafted Ideas or unlinked Books to encourage completion and linking.

## Metric 4: Single Source of Truth
- **Metric Definition**: The percentage of data fields in the public Web application that are sourced directly from the private Workspace database, rather than hardcoded.
- **Measurement Method**: Auditing public web components for static, hardcoded text that should be fetched dynamically from the entity schemas.
- **Target Threshold**: \(100\%\).
- **Actionable Correction**: Code linting rules will prohibit hardcoding personal milestones, stack lists, or project summaries outside the database/markdown directory structure.

## Metric 5: Publish Coverage
- **Metric Definition**: The ratio of finished Articles and Projects created in the Workspace that are successfully translated and built to the Web application.
- **Measurement Method**: Calculated as:
  \[\text{Publish Coverage} = \frac{\text{Entities with 'Published' Status Sourced on Web}}{\text{Total Workspace Entities with 'Published' Status}} \times 100\]
- **Target Threshold**: \(100\%\).
- **Actionable Correction**: Build logs will alert the developer if an entity marked as published fails the compilation pipeline constraints.

## Metric 6: Knowledge Connectivity
- **Metric Definition**: The average number of links per individual Learning node.
- **Measurement Method**: Sum of links originating from or pointing to Learnings divided by the total count of Learnings.
- **Target Threshold**: \(\ge 3.0\) links per node.
- **Actionable Correction**: When creating or editing a Learning in the Studio, a sidebar will actively recommend linking the note to related Books, Technologies, or Projects.

## Metric 7: Maintainability
- **Metric Definition**: Code complexity and build performance metrics. Specifically, the time required to run a full clean compilation and build of the monorepo workspace.
- **Measurement Method**: Automated compilation time logging in the build runner.
- **Target Threshold**: \(\le 10\) seconds for local incremental builds; \(\le 45\) seconds for clean monorepo builds.
- **Actionable Correction**: If build times exceed thresholds, code architects must review build caches in the `turbo.json` config and prune redundant third-party package dependencies.

## Metric 8: User Adoption
- **Metric Definition**: The count of monthly active updates (adding or editing notes, tasks, or projects) performed by the owner in the private workspace.
- **Measurement Method**: Database logs tracking last-modified dates of entities.
- **Target Threshold**: \(\ge 20\) write operations per month.
- **Actionable Correction**: If adoption drops, it indicates the private workspace interface has become too high-friction, prompting a review of the Studio's creation and editor layouts.

---

## References
- [PRD](file:///e:/rifqi.id/docs/01-product/03-PRD.md)
- [Product Principles](file:///e:/rifqi.id/docs/01-product/02-Product-Principles.md)

## Decision Log
- **2026-06-26**: Initialization of success metrics and calculation formulas by CTO. Status set to Approved.
