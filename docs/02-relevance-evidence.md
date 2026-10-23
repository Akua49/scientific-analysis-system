# 2. Evidence of Relevance

Status of each claim: **V** – verified (source given), **A** – assumption (verification method given). **R** – rejected after verification.

## 2.1 Evidence collection plan

| \#  | Method                                               | Participant / source                                                                       | Date                    | Status    |
|-----|------------------------------------------------------|--------------------------------------------------------------------------------------------|-------------------------|-----------|
| S-1 | Online survey (Google Forms, 9 questions, anonymous) | AITU students and academic staff; N = 26 (21 undergraduate, 1 master’s, 2 PhD, 1 lecturer, 1 other) | 23.10.2026              | Done      |
| I-1 | Interview                                            | Supervisor of diploma projects, School of SE                                               | by 15.11.2026           | Planned   |
| I-2 | Interview                                            | Lecturer who reviews theses                                                                | by 15.11.2026           | Planned   |
| I-3 | Interview                                            | Norm-control / topic approval staff                                                        | by 15.11.2026           | Planned   |
| O-1 | Observation                                          | Supervisor checking a thesis reference list (time measured)                                | by 15.11.2026           | Planned   |
| D-1 | Data analysis                                        | 10 past theses: share of broken links, references without DOI, citation style              | by 20.12.2026 (with E1) | Planned   |
| D-2 | Data                                                 | Archive of past thesis topics from the School                                              | 24.10.2026              | Requested |
| C-1 | Agreement                                            | Supervisor / School confirms scope and access to control sample                            | 24.10.2026              | Requested |

Questionnaire: [evidence/survey-S1-questionnaire.md](evidence/survey-S1-questionnaire.md); interview guide: Appendix B.2 of the pre-defense report (docs/report/). Raw anonymised responses: docs/evidence/survey-S1.csv. The survey was conducted under the working name SciCheck.

## 2.2 Claims register

| ID  | Claim                                                                                          | Status                  | Evidence / verification                                                                                                                                                             |
|-----|------------------------------------------------------------------------------------------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| C1  | A notable share of web references in scholarly texts become broken or point to changed content | V (literature + survey) | Klein et al. 2014; Jones et al. 2016; S-1 Q6: 58% (15/26) have encountered broken or unverifiable references; Q5: 46% (12/26) name broken links / incorrect DOIs as the hardest part |
| C2  | Citations frequently misrepresent the cited source                                             | V (literature + survey) | Jergas & Baethge 2015; Mogull 2017; S-1 Q5: 58% (15/26) name “checking whether sources support citations” as the hardest task                                                       |
| C3  | LLM-assisted writing increases fabricated references                                           | V (literature + survey) | Walters & Wilder 2023; S-1 Q6: 58% (15/26) met references that could not be verified                                                                                                |
| C4  | Supervisors spend significant time checking references and citations manually                  | V (survey, partial)     | S-1 Q4: 65% (17/26) spend ≥15 min per document, 27% (7/26) more than 30 min; Q3: 62% (16/26) open links one by one; supervisor time to be measured in O-1                                   |
| C5  | Abstracts of student theses often do not reflect the content                                   | V (survey)              | S-1 Q5: 35% (9/26) find abstract accuracy hard to check; Q8: 35% (9/26) want abstract-vs-content comparison                                                                                |
| C6  | Requirements differ by programme / journal, so a fixed checklist is insufficient               | A (weak support)        | S-1 Q5: 23% (6/26) find requirement compliance hard; Q8: 27% (7/26) want it — to be confirmed in I-3                                                                                |
| C7  | Repeated or very similar topics occur across years and are detected manually                   | A (weak support)        | S-1 Q5: 19% (5/26); Q8: 23% (6/26) want similar-topic detection — to be confirmed in I-3 and D-2                                                                                    |
| C8  | Plagiarism systems used at AITU do not check citation correctness                              | V (survey, indirect)    | S-1 Q7: respondents rely on manual checking, DOI lookup or plagiarism tools; none of these verifies citation support                                                                |
| C9  | Users trust results only if the system shows evidence (source fragment, link status)           | A                       | Not covered by S-1; to be checked in the usability test (E7) and interviews I-1…I-3                                                                                                 |

## 2.3 Requirements traceability

| Requirements                      | Supported by                                                                                         |
|-----------------------------------|------------------------------------------------------------------------------------------------------|
| FR-10…FR-13 (references)          | C1, C3, C4 (S-1)                                                                                     |
| FR-20…FR-22 (citations)           | C2, C4, C8 (S-1: hardest task for 58%)                                                               |
| FR-30…FR-31 (abstract)            | C5 (S-1)                                                                                             |
| FR-40…FR-43 (requirements window) | Supervisor’s task (justification letter); C6 weakly supported by S-1, to be confirmed in I-3         |
| FR-50…FR-51 (topics)              | Supervisor’s task (justification letter); C7 weakly supported by S-1, to be confirmed in I-3 and D-2 |

## 2.4 Findings summary

- Confirmed: C1/C3 — 58% have met broken or unverifiable references; C4 — 65% spend 15+ minutes per document, mostly opening links manually; C5 — 35% struggle to check abstract accuracy; C8 — checking whether sources support citations is the most frequently named difficulty (58%), and no tool currently in use addresses it.
- Weak / not confirmed: C6 (requirements compliance, 23–27%) and C7 (similar topics, 19–23%). These checks remain in scope because they are part of the supervisor’s task, but they are to be confirmed with norm-control staff (I-3) before pre-defense 2. C9 was not covered by the survey.
- New needs (Q9): 10 of 26 open answers were substantive: (1) accuracy and source reliability (-\> FR-10…FR-22); (2) explained reports with recommendations for fixes (-\> FR-65); (3) multilingual support and detection of AI-generated text (-\> NFR-06, FR-64).
- Priorities (Q8): DOI and metadata verification 54%; link checking 42%; citation-support checking 42%; abstract-vs-content comparison 35%; requirements compliance 27%; similar topics 23%; issue report 8%.
- Limitations: small convenience sample (N = 26, one university, one day); 81% undergraduates, staff represented by one lecturer and two PhD students. Staff-specific claims (C4, C6, C7) will be confirmed by O-1 and I-1…I-3 before pre-defense 2.
