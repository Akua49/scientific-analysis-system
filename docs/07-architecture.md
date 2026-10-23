# 7. Architecture and Diagrams

Sources: [diagrams/src/](https://github.com/Akua49/scientific-analysis-system/tree/main/diagrams/src) (Mermaid .mmd, PlantUML .puml) · exports: [diagrams/export/](https://github.com/Akua49/scientific-analysis-system/tree/main/diagrams/export).

## 7.1 System context

![context](../diagrams/export/01-context.png)

Scirevia is used by students, article authors, supervisors and norm-control/admin staff of the School. It calls Crossref, OpenAlex and Semantic Scholar for metadata and source texts, performs HTTP requests to link targets and doi.org, imports the archive of past thesis topics provided by the School, and calls an LLM API **only** when the user consents (NFR-05).

## 7.2 Use cases

![use cases](../diagrams/export/02-use-case.png)

| Use case                                            | Requirements        | Prototype screen                  | Owner  |
|-----------------------------------------------------|---------------------|-----------------------------------|--------|
| UC-01 Upload document, choose checks                | FR-01, FR-02, FR-03 | New check                         | MK, AK |
| UC-02 Enter requirements                            | FR-40, FR-43        | New check -\> Requirements window | AK     |
| UC-03 Check references                              | FR-10…13            | Report -\> References             | MK, SS |
| UC-04 Check citations                               | FR-20…22            | Report -\> Citations              | SS     |
| UC-05 Check abstract                                | FR-30, FR-31        | Report -\> Abstract               | SS     |
| UC-06 Check requirements                            | FR-41, FR-42        | Report -\> Requirements           | SS     |
| UC-07 Check topic similarity                        | FR-50               | Report -\> Topic                  | SS     |
| UC-08 View report                                   | FR-60, FR-63        | Report -\> Overview               | AK     |
| UC-09 Export PDF                                    | FR-61               | Report -\> Export                 | MK     |
| UC-10 Share with supervisor                         | FR-71               | Report -\> Share                  | MK, AK |
| UC-11 Templates · UC-12 Topic archive · UC-13 Users | FR-43, FR-51, FR-70 | Admin                             | MK     |

## 7.3 Components (draft)

![components](../diagrams/export/03-components.png)

| Component          | Responsibility                                                  | Technology                                       | Owner             |
|--------------------|-----------------------------------------------------------------|--------------------------------------------------|-------------------|
| Client             | Upload, requirements window, report views, charts, history      | HTML/CSS/JS, Chart.js                            | A. Kuanyshbekova  |
| REST API           | Auth (JWT), roles, validation, Swagger                          | Express, joi, swagger-jsdoc                      | M. Khairgeldinova |
| DocumentService    | Upload, text extraction, reference list extraction              | multer, mammoth / call to analysis preprocessing | M. Khairgeldinova |
| LinkChecker        | URL status, redirects, timeouts, DOI resolution                 | undici/axios, p-limit                            | M. Khairgeldinova |
| JobOrchestrator    | checkJobs, progress, callbacks, retries                         | Express, MongoDB                                 | M. Khairgeldinova |
| ReportService      | Merge results, PDF export                                       | Puppeteer / pdfkit                               | M. Khairgeldinova |
| Preprocessing      | Sections, in-text citations, reference parsing, normalisation   | spaCy/NLTK, GROBID                               | S. Sergeyeva      |
| MetadataClient     | Crossref, OpenAlex, Semantic Scholar                            | httpx                                            | S. Sergeyeva      |
| CitationVerifier   | Retrieval of source fragment + NLI label                        | sentence-transformers, Transformers              | S. Sergeyeva      |
| AbstractChecker    | Summary, coverage, consistency                                  | Transformers / LLM API                           | S. Sergeyeva      |
| RequirementChecker | Rule checks + LLM checks with quotes                            | Python, LLM API                                  | S. Sergeyeva      |
| TopicSimilarity    | Embedding index of past topics                                  | sentence-transformers, FAISS / NumPy             | S. Sergeyeva      |
| MongoDB            | users, documents, checkJobs, reports, templates, topics, GridFS | MongoDB 7                                        | M. Khairgeldinova |

## 7.4 Additional views

- Data model: ![data](../diagrams/export/04-data-model.png)
- Check run sequence: ![sequence](../diagrams/export/05-sequence.png)

## 7.5 Interfaces between team members

| Interface             | Provider -\> Consumer | Contract file                  | Task  |
|-----------------------|-----------------------|--------------------------------|-------|
| Client \<-\> Server   | MK -\> AK             | docs/api/openapi-server.yaml   | SCI-9 |
| Server \<-\> Analysis | SS -\> MK             | docs/api/openapi-analysis.yaml | SCI-9 |

## 7.6 Consistency check

Every M requirement -\> \>= 1 use case (7.2) -\> \>= 1 component (7.3) -\> \>= 1 test/experiment (Section 9.2–9.3). Re-check after each requirements change.
