# 10. Project Management and Risks

- **YouTrack:** project key SCI — https://sergeyevasss.youtrack.cloud/projects/SCI; the backlog is maintained in YouTrack.
- **Git:** main = reviewed baseline; branch SCI-\<n\>-\<short-name\>; commit message SCI-\<n\>: \<description\>; every PR is reviewed by another team member; the supervisor reviews significant changes at meetings. Tags: pre-defense-1, pre-defense-2, final-pre-defense.
- **Meetings with supervisor:** twice a month (online/offline); each member reports on her part; decisions logged in [11-supervisor-feedback.md](11-supervisor-feedback.md).

## 10.1 Responsibilities

| Area                              | S. Sergeyeva (ML/Data) | A. Kuanyshbekova (Frontend, UX/UI) | M. Khairgeldinova (Backend) | Supervisor |
|-----------------------------------|------------------------|------------------------------------|-----------------------------|------------|
| Requirements, interviews          | R                      | R (scenarios)                      | C                           | A          |
| Literature review                 | R                      | C                                  | C                           | A          |
| System & technology comparison    | R (NLP)                | R (client)                         | R (server, DB)              | A          |
| Architecture, API contracts       | R (analysis API)       | C                                  | R (server API)              | A          |
| Prototype / Figma                 | C                      | R                                  | C                           | I          |
| Analysis service                  | R                      | I                                  | C                           | C          |
| Server, link check, storage       | C                      | I                                  | R                           | C          |
| Client                            | I                      | R                                  | C                           | I          |
| Integration & testing, evaluation | R (quality)            | R (usability)                      | R (E2E, perf.)              | A          |

R — responsible · A — approves · C — consulted · I — informed.

## 10.2 Milestones (aligned with the supervisor’s plan)

| \#  | Stage                          | Result                                                                                                          | Date                         |
|-----|--------------------------------|-----------------------------------------------------------------------------------------------------------------|------------------------------|
| M1  | Requirements and data analysis | Scenarios, survey S-1 (N = 26), request for topic archive and control sample; pre-defense 1 (tag pre-defense-1) | 24.10.2026                   |
| M2  | Design                         | Architecture, API specification, storage schema, UI mockups (Figma)                                             | 15.11.2026                   |
| M3  | Base version                   | Upload, reference list extraction, link checking (E1, E2)                                                       | 20.12.2026                   |
| M4  | Text analysis                  | Citation check, summary and abstract comparison (E3, E4)                                                        | 15.02.2027                   |
| M5  | Requirements & topics          | Requirements window, requirement checks, topic similarity (E5); **pre-defense 2**                               | March 2027 (School schedule) |
| M6  | Integration & testing          | Integrated system, evaluation on control sample (E6, E7)                                                        | 15.04.2027                   |
| M7  | Documentation                  | Explanatory note, presentation; **final pre-defense**                                                           | May 2027 (School schedule)   |

## 10.3 Risks

| ID  | Risk                                                              | P   | I   | Mitigation                                                                                   | Owner      |
|-----|-------------------------------------------------------------------|-----|-----|----------------------------------------------------------------------------------------------|------------|
| R1  | Topic archive / control sample not provided in time by the School | M   | H   | Request at M1 via supervisor; fallback — topics from public AITU repository / own collection | SS         |
| R2  | Open full texts unavailable for many sources                      | H   | M   | Use abstracts; explicit “source unavailable”; report share separately                        | SS         |
| R3  | Low quality for Kazakh texts                                      | M   | M   | Compare 3 multilingual models in E3; report per language                                     | SS         |
| R4  | GOST references parsed poorly                                     | M   | M   | Rule-based fallback; retrain/adjust on 20 annotated docs                                     | SS, MK     |
| R5  | Integration problems between JS and Python components             | M   | H   | OpenAPI contracts first (SCI-9); mocks; weekly integration build                             | all        |
| R6  | Websites block automated link checks (403/429)                    | M   | L   | Browser-like UA, retries, class “access restricted” instead of “broken”                      | MK         |
| R7  | Schedule slip in one component                                    | M   | H   | Bi-weekly control; Must/Should priorities; reserve time before defence                       | supervisor |
| R8  | Confidentiality of student theses                                 | L   | H   | Local processing by default, consent for LLM, retention 30 days, no theses in Git            | all        |
| R9  | LLM cost / API access                                             | M   | M   | LLM only optional; local models for core checks                                              | SS         |

## 10.4 Dependencies

- D1: archive of past topics and control sample from School of SE (blocks FR-50, E1–E5).
- D2: agreed API contracts (blocks parallel implementation).
- D3: server for deployment and model inference (to be requested from AITU IT at M2).
- D4: AITU official formatting requirements document (blocks template FR-43).

## YouTrack backlog (initial)

| ID     | Task                                                               | Assignee               | Priority | Due        |
|--------|--------------------------------------------------------------------|------------------------|----------|------------|
| SCI-1  | Create repository, README, structure, .gitignore                   | Meruert Khairgeldinova | Critical | 2026-10-20 |
| SCI-2  | Project proposal and scope                                         | Saltanat Sergeyeva     | Critical | 2026-10-21 |
| SCI-3  | Survey questionnaire (S-1) and interview guide                     | Alzira Kuanyshbekova   | Critical | 2026-10-21 |
| SCI-4  | Survey S-1 (Google Forms, N = 26); update claims register          | Alzira Kuanyshbekova   | Critical | 2026-10-23 |
| SCI-5  | Literature review (\>=12 sources, \>=8 scientific) + table         | Saltanat Sergeyeva     | Critical | 2026-10-22 |
| SCI-6  | Existing systems comparison (5 systems, 9 criteria)                | Alzira Kuanyshbekova   | Critical | 2026-10-22 |
| SCI-7  | Technology comparison + ADR-001…005                                | Meruert Khairgeldinova | Critical | 2026-10-22 |
| SCI-8  | Requirements v0.1 with acceptance criteria                         | Saltanat Sergeyeva     | Critical | 2026-10-23 |
| SCI-9  | API contracts: openapi-server.yaml, openapi-analysis.yaml          | Meruert Khairgeldinova | Critical | 2026-10-30 |
| SCI-10 | Diagrams: context, use case, component (sources + exports)         | Meruert Khairgeldinova | Critical | 2026-10-23 |
| SCI-11 | Data model and sequence diagram                                    | Meruert Khairgeldinova | Normal   | 2026-10-23 |
| SCI-12 | Clickable prototype + Figma mockups                                | Alzira Kuanyshbekova   | Critical | 2026-10-23 |
| SCI-13 | Verification and evaluation plan                                   | Saltanat Sergeyeva     | Critical | 2026-10-23 |
| SCI-14 | Project plan, RACI, risks; supervisor log                          | Alzira Kuanyshbekova   | Major    | 2026-10-23 |
| SCI-15 | Request topic archive and control sample from School               | Saltanat Sergeyeva     | Critical | 2026-10-24 |
| SCI-16 | Spike: reference parsing, DOI extraction, TF-IDF citation baseline | Saltanat Sergeyeva     | Major    | 2026-10-24 |
| SCI-17 | Tag pre-defense-1 and submission summary                           | Meruert Khairgeldinova | Critical | 2026-10-24 |
| SCI-18 | Server skeleton: Express, Mongoose, auth, Swagger, Docker Compose  | Meruert Khairgeldinova | Critical | 2026-11-15 |
| SCI-19 | Document upload and text extraction (FR-01, FR-02)                 | Meruert Khairgeldinova | Critical | 2026-12-01 |
| SCI-20 | Link checker and DOI resolution (FR-10, FR-11)                     | Meruert Khairgeldinova | Critical | 2026-12-20 |
| SCI-21 | Annotate control sample (references, citations, abstracts)         | Saltanat Sergeyeva     | Critical | 2026-12-10 |
| SCI-22 | Reference parsing incl. GOST; experiment E1                        | Saltanat Sergeyeva     | Critical | 2026-12-20 |
| SCI-23 | Metadata client + non-existent reference detection (FR-12)         | Saltanat Sergeyeva     | Critical | 2027-01-20 |
| SCI-24 | Citation verification: embeddings + NLI; experiment E3             | Saltanat Sergeyeva     | Critical | 2027-02-15 |
| SCI-25 | Summary and abstract comparison; experiment E4                     | Saltanat Sergeyeva     | Critical | 2027-02-28 |
| SCI-26 | Client: upload, check settings, progress                           | Alzira Kuanyshbekova   | Critical | 2026-12-20 |
| SCI-27 | Client: requirements window + templates                            | Alzira Kuanyshbekova   | Critical | 2027-02-15 |
| SCI-28 | Client: report views and charts                                    | Alzira Kuanyshbekova   | Critical | 2027-03-01 |
| SCI-29 | Requirement checks (rules + intelligent) and topic similarity; E5  | Saltanat Sergeyeva     | Critical | 2027-03-20 |
| SCI-30 | Integration, E2E tests, performance (E6), usability (E7)           | Meruert Khairgeldinova | Critical | 2027-04-15 |
