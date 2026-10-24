# 5. Technology Comparison

Scores 1–3 (3 = best) against criteria derived from requirements. Final decisions: adr/.

## D1. Server platform

Requirements: concurrent link checking with timeouts (FR-10, NFR-02), file upload (FR-01), REST API with documentation (NFR-07), team skills of the backend developer (JavaScript, REST, NoSQL).

| Criterion                                    | **Node.js + Express**                            | Python + FastAPI | NestJS (TypeScript) |
|----------------------------------------------|--------------------------------------------------|------------------|---------------------|
| Asynchronous I/O for hundreds of HTTP checks | 3                                                | 3                | 3                   |
| Team expertise (backend developer)           | 3                                                | 2                | 1                   |
| Simplicity / learning curve                  | 3                                                | 3                | 1                   |
| Upload, validation, Swagger ecosystem        | 3 (multer, joi, swagger-jsdoc)                   | 3                | 3                   |
| Access to ML libraries                       | 1 — not needed: ML is in a separate service (D3) | 3                | 1                   |
| **Total**                                    | **13**                                           | 14               | 9                   |

**Decision:** Node.js + Express. FastAPI scores one point higher only because of ML libraries, which the server does not need (they are isolated in the analysis service); team expertise outweighs this. -\> ADR-001

## D2. Data storage

Requirements: documents and nested check reports of variable structure (FR-60), requirement templates (FR-43), topic archive (FR-51), history (FR-62).

| Criterion                                      | **MongoDB**                                         | PostgreSQL   | PostgreSQL + JSONB |
|------------------------------------------------|-----------------------------------------------------|--------------|--------------------|
| Nested, evolving report structure              | 3                                                   | 1            | 3                  |
| Team expertise                                 | 3                                                   | 2            | 2                  |
| File storage (GridFS) or references            | 3                                                   | 2            | 2                  |
| Relational integrity (users–documents–reports) | 2                                                   | 3            | 3                  |
| Vector search for topics                       | 2 (Atlas only; we keep vectors in analysis service) | 2 (pgvector) | 2 (pgvector)       |
| **Total**                                      | **13**                                              | 10           | 12                 |

**Decision:** MongoDB with Mongoose schemas for validation; topic embeddings are stored and searched inside the analysis service (corpus of a few thousand topics fits in memory / FAISS). -\> ADR-002

## D3. Interaction between components

Requirements: long checks (citation verification may take minutes, NFR-02), progress visible to user (FR-63), independent development of three components.

| Criterion                  | Synchronous REST | **REST + asynchronous jobs (job record in MongoDB, status polling, callback from analysis service)** | Message broker (RabbitMQ / BullMQ + Redis) |
|----------------------------|------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------|
| No timeouts on long checks | 1                | 3                                                                                                    | 3                                          |
| Progress per check         | 1                | 3                                                                                                    | 3                                          |
| Extra infrastructure       | 3                | 3                                                                                                    | 1                                          |
| Complexity for the team    | 3                | 2                                                                                                    | 1                                          |
| **Total**                  | 8                | **11**                                                                                               | 8                                          |

**Decision:** REST/JSON between all components; checks run as asynchronous jobs. Upgrade path: BullMQ if load grows. API contracts are fixed in OpenAPI before implementation. -\> ADR-003

## D4. Document structure extraction

Requirements: abstract, body, in-text citations, reference list from DOCX and PDF; GOST/APA/IEEE styles (FR-02).

| Criterion                          | **python-docx / PyMuPDF + rules** | **GROBID**         | Apache Tika |
|------------------------------------|-----------------------------------|--------------------|-------------|
| Reference list parsing into fields | 1                                 | 3                  | 1           |
| DOCX support                       | 3                                 | 1 (PDF only)       | 3           |
| GOST / Russian references          | 2 (custom rules)                  | 1–2 *(test in E1)* | 1           |
| Deployment                         | 3                                 | 2 (Java service)   | 2           |
| **Total**                          | **9**                             | **7–8**            | **7**       |

**Decision:** hybrid — python-docx for DOCX (most theses), GROBID for PDF and for parsing reference strings; rule-based fallback for GOST. Chosen by E1 F1-score. -\> ADR-004 Rules + python-docx score highest in total (9) but cannot split reference strings into fields; GROBID covers exactly this gap, hence the hybrid.

## D5. Semantic comparison (citations, topics)

| Criterion                         | TF-IDF / BM25 | **Multilingual sentence embeddings (multilingual-e5 / LaBSE / paraphrase-multilingual)** | LLM API only |
|-----------------------------------|---------------|------------------------------------------------------------------------------------------|--------------|
| Detects paraphrase                | 1             | 3                                                                                        | 3            |
| Cross-lingual RU/KZ \<-\> EN      | 1             | 3                                                                                        | 3            |
| Cost / runs locally               | 3             | 3                                                                                        | 1            |
| Explainability (fragment + score) | 3             | 2                                                                                        | 2            |
| **Total**                         | **8**         | **11**                                                                                   | **9**        |

**Decision:** embeddings for retrieval of the most similar source fragment + NLI cross-encoder for the label; TF-IDF kept as the **baseline** in E3/E5. LLM optional for borderline cases (with consent). -\> ADR-005

## D6. Summarisation and abstract comparison

| Criterion                          | Extractive (TextRank) | Local abstractive model (mT5 / mBART) | **LLM API (with consent) + extractive fallback** |
|------------------------------------|-----------------------|---------------------------------------|--------------------------------------------------|
| Summary quality on long RU/KZ text | 1                     | 2                                     | 3                                                |
| Cost / hardware                    | 3                     | 1 (GPU)                               | 2                                                |
| Privacy                            | 3                     | 3                                     | 1 -\> mitigated by consent / local fallback      |
| **Total**                          | **7**                 | **6**                                 | **6**                                            |

**Decision:** LLM summary when the user consents; otherwise extractive summary. Abstract comparison uses embedding coverage + NLI consistency (independent of summariser). Extractive summarisation scores highest in total (7) because of cost and privacy, but lowest on quality for long RU/KZ texts; the hybrid keeps local processing by default (NFR-05) and uses the LLM only with consent.

## D7. Client

| Criterion                                            | **HTML/CSS/JavaScript + Chart.js** | React | Flutter (web + mobile) |
|------------------------------------------------------|------------------------------------|-------|------------------------|
| Team expertise (frontend developer)                  | 3                                  | 2     | 3                      |
| Complexity of report UI (tabs, tables, side-by-side) | 2                                  | 3     | 2                      |
| Build tooling / simplicity                           | 3                                  | 2     | 2                      |
| Mobile version                                       | 1                                  | 1     | 3                      |
| **Total**                                            | **9**                              | **8** | **10**                 |

**Decision:** HTML/CSS/JS (ES modules) for the web client; Flutter mobile version is optional (Could). Flutter scores one point higher only because of the mobile criterion, which is a Could requirement; for the Must web client, HTML/CSS/JS fits team expertise and has the simplest tooling.
