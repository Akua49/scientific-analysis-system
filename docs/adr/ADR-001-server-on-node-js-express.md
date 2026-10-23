# ADR-001: Server on Node.js + Express

- **Status:** Accepted · **Date:** 22.10.2026 · **Owner:** M. Khairgeldinova · reviewed by supervisor
- **Context:** The server handles upload, storage, link/DOI checking (I/O-bound, many concurrent requests) and orchestration of checks. ML code lives in a separate Python service (ADR-003). Alternatives: FastAPI, NestJS (Section 5, D1).
- **Decision:** Node.js (LTS) + Express; multer (upload), joi/zod (validation), Mongoose, swagger-jsdoc + swagger-ui (OpenAPI), undici/axios with concurrency limit (p-limit) for link checks; Jest + supertest for tests.
- **Consequences:** + matches team expertise, efficient async I/O. − two languages in the system -\> contracts must be explicit (OpenAPI, shared JSON schemas in docs/api/).
