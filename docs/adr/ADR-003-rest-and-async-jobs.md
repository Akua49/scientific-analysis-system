# ADR-003: REST between components, asynchronous check jobs

- **Status:** Accepted · **Date:** 22.10.2026 · **Owners:** whole team
- **Context:** Three components are developed in parallel by different people in different languages; some checks take minutes. Alternatives: synchronous REST, message broker (Section 5, D3).
- **Decision:** Client \<-\> Server: REST/JSON. Server \<-\> Analysis service: REST/JSON; server creates a checkJob, calls POST /analyze/{check} on the analysis service, which returns 202 and later posts results to POST /internal/jobs/{id}/result (shared secret). Client polls GET /api/checks/{id}. Contracts in docs/api/openapi-\*.yaml, agreed before coding (task SCI-9).
- **Consequences:** + independent development and testing with mocks; no extra infrastructure. − must handle lost callbacks (timeout -\> retry/failed status).
