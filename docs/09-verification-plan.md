# 9. Verification and Evaluation Plan

## 9.1 How the aim is demonstrated

The aim is achieved if, on a control sample of real theses, Scirevia (a) detects reference, citation, abstract, requirement and topic problems with accuracy above the defined thresholds and above simple baselines, (b) processes a thesis within the time limit, and (c) is usable and saves reviewers’ time compared with manual checking.

## 9.2 Testing levels

| Level              | Client (AK)                                | Server (MK)                                                 | Analysis service (SS)                                   |
|--------------------|--------------------------------------------|-------------------------------------------------------------|---------------------------------------------------------|
| Unit               | Jest for UI logic                          | Jest: validation, link classifier, job state machine        | pytest: parsers, rules, scoring                         |
| Integration        | —                                          | supertest + MongoDB test container; mocked analysis service | recorded API responses (Crossref/OpenAlex)              |
| Contract           | —                                          | OpenAPI validation of requests/responses (both directions)  | same                                                    |
| End-to-end         | Playwright: 5 key scenarios from prototype | \<-                                                         | \<-                                                     |
| Performance        | —                                          | 10 concurrent checks (k6)                                   | profiling per check                                     |
| Security / privacy | —                                          | OWASP ZAP baseline; auth matrix                             | network capture: no outbound text when llmConsent=false |

CI: GitHub Actions on every pull request (NFR-08).

## 9.3 Control sample

- **Documents:** 20 theses of the School of SE (2022–2026, anonymised, with permission) + 5 published articles. *(dependency: School / supervisor)*
- **Topic archive:** list of past topics from the School (D-2).
- **Annotation:** two team members annotate independently, disagreements resolved with the supervisor; agreement reported as Cohen’s κ.

## 9.4 Experiments, metrics, baselines

| \#  | What is measured                  | Ground truth                                                                                     | Metric                                                       | Baseline                             | Target                                    |
|-----|-----------------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------|--------------------------------------|-------------------------------------------|
| E1  | Structure extraction (FR-02)      | Manually marked abstract, references, in-text citations in 20 docs                               | Precision / recall / F1 of reference entries; abstract found | GROBID only vs. rules only           | F1 \>= 0.85                               |
| E2  | Link & DOI check (FR-10, FR-11)   | 200 links + 100 references labelled manually (working / broken / redirected-changed / wrong DOI) | Accuracy, per-class F1                                       | HTTP-status-only check               | Accuracy \>= 0.90 and \> baseline         |
| E2b | Non-existent references (FR-12)   | 20 planted fabricated references + 80 real                                                       | Recall, precision                                            | —                                    | Recall \>= 0.8                            |
| E3  | Citation verification (FR-21)     | 150 citation–source pairs, labels: supported / partial / not supported                           | Macro-F1, confusion matrix; separately for RU, KZ, EN        | TF-IDF cosine with tuned threshold   | Macro-F1 \>= 0.70 and \>= baseline + 0.10 |
| E4  | Abstract assessment (FR-31)       | 2 experts rate abstract adequacy 1–5 for 20 theses                                               | Spearman ρ between system score and mean expert rating       | ROUGE-L between abstract and summary | ρ \>= 0.6 and \> baseline                 |
| E5  | Topic similarity (FR-50)          | 30 query topics with labelled similar topics in archive                                          | Precision@5, MRR                                             | Jaccard similarity of keywords       | P@5 \>= 0.6; MRR \>= baseline + 0.1       |
| E6  | Processing time (NFR-02)          | 20 docs, target server spec recorded                                                             | Median and max time per document                             | —                                    | \<= 5 min                                 |
| E7  | Usability and time saved (NFR-01) | 5 users; reviewer checks references/citations of one thesis manually vs. with Scirevia           | SUS; time on task; problems found                            | Manual check                         | SUS \>= 70; \>= 40 % time reduction       |

## 9.5 Conditions and threats to validity

Model versions and API snapshot dates are recorded; experiments repeated 3 times for LLM-based parts (temperature 0). Small sample from one School; annotators are team members (mitigated by supervisor adjudication and κ); limited open full texts -\> “source unavailable” share is reported separately rather than counted as errors.
