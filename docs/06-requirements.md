# 6. Requirements Specification

Priority: **M** must · **S** should · **C** could. Every M requirement has an acceptance criterion (AC) verifiable by a test or experiment in the verification plan. Owner: **SS** — Sergeyeva (analysis), **AK** — Kuanyshbekova (client), **MK** — Khairgeldinova (server).

## 6.1 Functional requirements

### Document upload and structure

| ID    | Requirement                                                                               | Pr. | Acceptance criterion                                                                         | Owner  |
|-------|-------------------------------------------------------------------------------------------|-----|----------------------------------------------------------------------------------------------|--------|
| FR-01 | Upload DOCX or text PDF (\<= 20 MB) and select which checks to run                        | M   | Valid files accepted; other types rejected with message; test with 10 files                  | MK, AK |
| FR-02 | Extract title, abstract, body, in-text citations and reference list                       | M   | On control sample (E1): reference entries F1 \>= 0.85, abstract found in \>= 18/20 documents | MK, SS |
| FR-03 | Show extracted structure to the user and allow correcting abstract / reference boundaries | S   | User edit is used in subsequent checks (E2E test)                                            | AK     |

### Reference check

| ID    | Requirement                                                                                                   | Pr. | Acceptance criterion                                                     | Owner  |
|-------|---------------------------------------------------------------------------------------------------------------|-----|--------------------------------------------------------------------------|--------|
| FR-10 | For each URL: status (working / broken / redirected / access restricted / timeout), final URL, HTTP code      | M   | On 200 labelled links (E2): accuracy \>= 0.90; timeout per link \<= 10 s | MK     |
| FR-11 | Resolve DOI and compare retrieved metadata (title, authors, year) with the reference entry; match score       | M   | On 100 labelled references: correct “matches / does not match” \>= 0.90  | MK, SS |
| FR-12 | For references without DOI/URL, search Crossref / OpenAlex / Semantic Scholar; flag “not found in any source” | M   | Recall of planted fabricated references \>= 0.8 (E2b)                    | SS     |
| FR-13 | Check consistency of in-text citations and reference list (unused entries, missing entries)                   | S   | Synthetic test with 5 planted inconsistencies — all found                | SS     |

### Citation check

| ID    | Requirement                                                                                                                              | Pr. | Acceptance criterion                                                              | Owner |
|-------|------------------------------------------------------------------------------------------------------------------------------------------|-----|-----------------------------------------------------------------------------------|-------|
| FR-20 | For each citation, retrieve source text (OA full text or abstract)                                                                       | M   | Retrieval attempt logged per citation; status “source unavailable” when not found | SS    |
| FR-21 | Find the most similar source fragment and assign label: supported / partially supported / not supported / source unavailable, with score | M   | E3: macro-F1 \>= 0.70 and \>= +0.10 over TF-IDF baseline                          | SS    |
| FR-22 | Display citation and source fragment side by side with link to source                                                                    | M   | UI test: every label has fragment or reason                                       | AK    |

### Abstract check

| ID    | Requirement                                                                                                                                | Pr. | Acceptance criterion                                          | Owner |
|-------|--------------------------------------------------------------------------------------------------------------------------------------------|-----|---------------------------------------------------------------|-------|
| FR-30 | Generate a summary of the document body                                                                                                    | M   | Summary produced for 20/20 control documents \<= 2 min each   | SS    |
| FR-31 | Compare author’s abstract with content: coverage score, key points missing from the abstract, abstract sentences not supported by the body | M   | E4: Spearman ρ \>= 0.6 between system score and expert rating | SS    |

### Requirements window

| ID    | Requirement                                                                                                                                                     | Pr. | Acceptance criterion                                                                | Owner  |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|-------------------------------------------------------------------------------------|--------|
| FR-40 | User enters requirements in a separate window: free text or structured items (sections, volume, number and age of references, style, keywords, abstract length) | M   | Requirements saved with the check; UI test                                          | AK, MK |
| FR-41 | Measurable requirements are checked by rules                                                                                                                    | M   | 10 rule types; unit tests per rule; precision = recall = 1.0 on synthetic documents | SS     |
| FR-42 | Qualitative requirements (e.g. “aim and objectives are stated”) are checked intelligently and each verdict includes a quote from the document                   | S   | 100 % of verdicts contain a quote existing verbatim in the document                 | SS     |
| FR-43 | Save and reuse requirement templates (e.g. “AITU diploma project”)                                                                                              | S   | Template applied to a new check without re-entry                                    | MK, AK |

### Topic check

| ID    | Requirement                                                                                       | Pr. | Acceptance criterion                             | Owner |
|-------|---------------------------------------------------------------------------------------------------|-----|--------------------------------------------------|-------|
| FR-50 | Compare topic (title + abstract) with archive of past topics; show top-5 similar with score, year | M   | E5: Precision@5 \>= 0.6, MRR \>= baseline + 0.1  | SS    |
| FR-51 | Admin uploads / updates archive (CSV / XLSX)                                                      | M   | 1 000-row file imported \<= 1 min; index rebuilt | MK    |

### Report, users, history

| ID    | Requirement                                                                          | Pr. | Acceptance criterion                                | Owner  |
|-------|--------------------------------------------------------------------------------------|-----|-----------------------------------------------------|--------|
| FR-60 | Single report: summary panel + section per check with statuses                       | M   | All selected checks present; matches API data (E2E) | AK     |
| FR-61 | Export report to PDF                                                                 | S   | PDF opens; content equals on-screen report          | MK     |
| FR-62 | History of checks per user; compare two versions of the same document                | C   | —                                                   | MK, AK |
| FR-64 | Flag passages that are possibly AI-generated for the reviewer (from S-1, Q9)         | C   | —                                                   | SS     |
| FR-65 | For each detected issue, show a short recommendation on how to fix it (from S-1, Q9) | C   | —                                                   | AK, SS |
| FR-63 | Progress of running checks                                                           | M   | Status updates at least every 5 s                   | MK, AK |
| FR-70 | Roles: student, supervisor, admin; registration/login with AITU e-mail               | M   | Access matrix tests: forbidden actions -\> 403      | MK     |
| FR-71 | Supervisor sees reports of documents shared by students                              | S   | Sharing test                                        | MK, AK |

## 6.2 Non-functional requirements

| ID     | Requirement                                                      | Pr. | Acceptance criterion                                                                                          |
|--------|------------------------------------------------------------------|-----|---------------------------------------------------------------------------------------------------------------|
| NFR-01 | Usability                                                        | M   | SUS \>= 70 with 5 users (E7)                                                                                  |
| NFR-02 | Performance: full check of 80-page thesis with \<= 60 references | M   | \<= 5 min on target server (E6)                                                                               |
| NFR-03 | Politeness to external services                                  | M   | Concurrency \<= 10 per host; User-Agent with contact; Crossref/OpenAlex mailto set                            |
| NFR-04 | Reliability                                                      | S   | Failure of one check does not fail the report (fault-injection test)                                          |
| NFR-05 | Privacy                                                          | M   | Documents not sent to external LLM without consent (network test); files deleted after 30 days (configurable) |
| NFR-06 | Languages                                                        | M   | Documents in RU, KZ, EN processed; UI in RU/EN (KZ — Should)                                                  |
| NFR-07 | API documentation                                                | M   | OpenAPI for server and analysis service; contract tests pass                                                  |
| NFR-08 | Maintainability                                                  | S   | Test coverage \>= 60 % per component; CI on every PR                                                          |
| NFR-09 | Security                                                         | M   | Passwords hashed (bcrypt), JWT, input validation, upload type checks; no secrets in Git                       |
