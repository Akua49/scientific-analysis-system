# 8. UX / Prototype

Clickable prototype in Figma (English version, 7 screens, fictional data) — https://www.figma.com/proto/Gu5Z6gvbep6zOqVz4ASxwa/Scirevia-%E2%80%94-Prototype?node-id=9-150 Screenshots: [prototype/screens/](https://github.com/Akua49/scientific-analysis-system/tree/main/prototype/screens). Figma design: A. Kuanyshbekova.

| Screen          | Scenario                                                                                                      | Use cases    |
|-----------------|---------------------------------------------------------------------------------------------------------------|--------------|
| New check       | Upload -\> choose checks -\> requirements window (template + free text) -\> consent for external AI -\> start | UC-01, UC-02 |
| Report overview | Summary of five checks -\> export / share                                                                     | UC-08…10     |
| References      | Status of each link / DOI, metadata match, possibly non-existent references                                   | UC-03        |
| Citations       | Citation and closest source fragment side by side, label and score                                            | UC-04        |
| Abstract        | Author’s abstract vs. generated summary, coverage, unsupported sentences                                      | UC-05        |
| Requirements    | Rule and intelligent checks with evidence                                                                     | UC-06        |
| Topic           | Top similar topics from the archive                                                                           | UC-07        |

## API examples (contract draft)

    POST /api/checks
    { "documentId": "6531…", "checks": ["references","citations","abstract","requirements","topic"],
      "templateId": "aitu-diploma", "customRequirements": ["Each objective has a result in the conclusion"],
      "llmConsent": false }
    → 202 { "jobId": "j_812", "status": "queued" }

    GET /api/checks/j_812
    → { "status": "running", "progress": { "references": "done", "citations": "running", "abstract": "queued", ... } }
    POST /analyze/citations           (server → analysis service)
    { "jobId": "j_812", "lang": "ru",
      "citations": [{ "id": "c14", "text": "Sentence-BERT позволяет …", "refIndex": 3 }],
      "references": [{ "index": 3, "doi": "10.18653/v1/D19-1410" }] }
    → 202

    callback  POST /internal/jobs/j_812/result
    { "check": "citations", "results": [
       { "id": "c14", "label": "supported", "score": 0.87,
         "sourceFragment": "…derive semantically meaningful sentence embeddings…",
         "sourceType": "abstract", "sourceUrl": "https://doi.org/10.18653/v1/D19-1410" } ] }

## Usability test

5 participants (2 students, 2 supervisors, 1 norm-control), tasks: run a check with a template; find a broken reference; explain why a citation is “not supported”; add a custom requirement; export the report. Think-aloud + SUS. Results -\> docs/evidence/usability-prototype.md.

## Prototype screens

Exported from Figma (English version, 7 screens, fictional data):

- `prototype/screens/01-new-check.png`
- `prototype/screens/02-overview.png`
- `prototype/screens/03-references.png`
- `prototype/screens/04-citations.png`
- `prototype/screens/05-abstract.png`
- `prototype/screens/06-requirements.png`
- `prototype/screens/07-topic.png`
