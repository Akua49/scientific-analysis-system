# 1. Project Proposal

| Field                  | Value                                                                                                                                  |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Title (EN)             | Development of a System for Comprehensive Analysis and Evaluation of Scientific Information Using Digital and Intelligent Technologies |
| Title (RU)             | Разработка системы комплексного анализа и оценки научной информации с использованием цифровых и интеллектуальных технологий            |
| Short name             | Scirevia                                                                                                                               |
| Programme              | Software Engineering, AITU                                                                                                             |
| Team                   | Saltanat Sergeyeva (ML/Data), Alzira Kuanyshbekova (Frontend, UX/UI), Meruert Khairgeldinova (Backend)                                 |
| Supervisor             | Almas Myrzakhmetov, Senior Lecturer, School of Software Engineering                                                                    |
| Client / data provider | School of Software Engineering, AITU (archive of past thesis topics, control sample) — contact through the supervisor, A. Myrzakhmetov |

## 1.1 Problem statement

When diploma theses, projects, and scientific articles are prepared, the same problems recur:

- links in the reference list do not open or lead to a different source;
- quoted or paraphrased text does not correspond to the text of the cited source;
- the abstract does not reflect the actual content of the work;
- the document does not meet the established requirements;
- the topic repeats theses of previous years.

Today, supervisors and norm-control staff check these manually, which takes considerable time and depends on the reviewer. Plagiarism systems detect copied text but do not check whether citations and references are *correct*.

## 1.2 Aim

To develop a web system that automates checking references, citations, abstracts, user-defined requirements, and topic originality in scientific texts using NLP and open scholarly data, and produces a single report for the author and reviewer.

## 1.3 Objectives

1.  Collect and verify requirements through an online survey of students and academic staff (S-1, N = 26) and follow-up interviews with supervisors and norm-control staff; obtain the archive of past topics from the School.
2.  Review literature on reference rot, citation accuracy, reference parsing, semantic similarity, summarization, and factual-consistency evaluation.
3.  Compare existing tools (Turnitin, StrikePlagiarism, scite, Recite, SciSpace) against a consistent set of criteria.
4.  Specify functional and non-functional requirements with acceptance criteria.
5.  Design the architecture: client, server with REST API, analysis service, storage.
6.  Implement document upload and structure extraction, link and DOI checking (server).
7.  Implement citation verification, summarisation and abstract comparison, requirement checks and topic similarity (analysis service).
8.  Implement the user interface: upload, requirements window, report and visualisation (client).
9.  Evaluate quality on a control sample and measure processing time.

## 1.4 Expected outcomes

Working web system (client, server, analysis service) with documentation; evaluation results on the control sample; recommendations for use at the School.

## 1.5 Engineering complexity

- Extraction of document structure (abstract, body, in-text citations, reference list) from DOCX/PDF in different citation styles (GOST, APA, IEEE).
- Link checking with redirects, DOI resolution, timeouts, paywalls, and soft-404 pages; matching retrieved metadata to the reference entry.
- Semantic comparison of a citation with source text, including paraphrase and cross-lingual cases (RU / KZ / EN).
- Summarisation of long documents and assessment of abstract–content consistency.
- Checking user-defined requirements (rule-based + intelligent) and similarity search over the topic archive.
- Integration of three independently developed components (JS client, Node.js server, Python service) through agreed APIs.

## 1.6 Scope

In scope: DOCX and text-based PDF documents in Russian, Kazakh and English; five checks (references, citations, abstract, user-defined requirements, topic similarity); roles student / supervisor / admin; web client. Out of scope: plagiarism detection (covered by existing tools), retrieval of paywalled full texts, grammar and style checking, mobile app (Could). Pilot: theses of the School of Software Engineering, 2022–2026.

## 1.7 Assumptions and constraints

- Full texts of sources are available only for open-access works; otherwise, the abstract/metadata is used, and the result is marked accordingly.
- The archive of past topics is provided by the School (dependency D1).
- Documents are confidential: they are not sent to external LLM services without the user’s consent (NFR-05).
