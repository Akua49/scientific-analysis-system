# ADR-002: MongoDB as main storage

- **Status:** Accepted · **Date:** 22.10.2026 · **Owner:** M. Khairgeldinova
- **Context:** Check reports are nested and evolve as checks are added; requirement templates are user-defined. Alternatives: PostgreSQL, PostgreSQL+JSONB (Section 5, D2).
- **Decision:** MongoDB with collections users, documents, checkJobs, reports, requirementTemplates, topics; files in GridFS; Mongoose schemas enforce structure. Topic embeddings are kept in the analysis service index, rebuilt when topics changes.
- **Consequences:** + flexible reports, team familiarity. − referential integrity in application code; indexes on documents.userId, checkJobs.status required.
