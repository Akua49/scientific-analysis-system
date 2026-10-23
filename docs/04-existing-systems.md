# 4. Existing System Comparison

**Systems (5):** Turnitin, StrikePlagiarism, scite (Reference Check), Recite (ReciteWorks), SciSpace. **Criteria (9)** — the same for every system. Ratings: Yes full · Partly partial · No absent. Ratings were checked against vendor documentation on 23.10.2026.

| \#  | Criterion                                                  | Linked requirement |
|-----|------------------------------------------------------------|--------------------|
| K1  | Link availability check (URL status, redirects)            | FR-10              |
| K2  | DOI resolution and metadata match with the reference entry | FR-11, FR-12       |
| K3  | Citation content verification against source text          | FR-20…22           |
| K4  | In-text citation \<-\> reference list consistency          | FR-13              |
| K5  | Summary vs. author’s abstract                              | FR-30, FR-31       |
| K6  | User-defined requirements check                            | FR-40…43           |
| K7  | Topic similarity with a local archive of past theses       | FR-50              |
| K8  | Russian / Kazakh language support                          | NFR-06             |
| K9  | Cost and data privacy (self-hosting)                       | NFR-05             |

| Criterion               | Turnitin                                                               | StrikePlagiarism                                                                                    | scite Reference Check                                                                                | Recite                                                          | SciSpace                                                 | **Scirevia**                  |
|-------------------------|------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|----------------------------------------------------------|-------------------------------|
| K1 Links                | No                                                                     | No                                                                                                  | No *(not described in Reference Check documentation)*                                                | No                                                              | No                                                       | Yes                           |
| K2 DOI / metadata       | No                                                                     | No                                                                                                  | Yes checks references for retractions and editorial notices                                          | No                                                              | No                                                       | Yes                           |
| K3 Citation content     | No                                                                     | No                                                                                                  | Partly shows how others cite a paper (supporting / contrasting), not whether *your* citation matches | No                                                              | No                                                       | Yes                           |
| K4 Citation \<-\> list  | No                                                                     | No                                                                                                  | No                                                                                                   | Yes matches in-text citations with reference list (APA/Harvard) | No                                                       | Partly (Should)               |
| K5 Abstract vs. content | No                                                                     | No                                                                                                  | No                                                                                                   | No                                                              | Partly generates summaries, no comparison with abstract  | Yes                           |
| K6 Custom requirements  | No                                                                     | No                                                                                                  | No                                                                                                   | Partly style rules only                                         | No                                                       | Yes                           |
| K7 Topic archive        | Partly text similarity incl. institutional repository, not topic-level | Partly text similarity, institutional database *(incl. institutional archives, vendor information)* | No                                                                                                   | No                                                              | No                                                       | Yes                           |
| K8 RU / KZ              | Partly *(multilingual; Kazakh not documented)*                         | Yes *(multilingual; used by Kazakhstani universities)*                                              | No mostly English corpus                                                                             | No *(English-language styles only)*                             | Partly *(multilingual interface, mainly English corpus)* | Yes                           |
| K9 Cost / privacy       | No institutional licence, cloud                                        | No institutional licence, cloud                                                                     | Partly freemium, cloud                                                                               | Partly freemium, cloud                                          | Partly freemium, cloud                                   | Yes free, self-hosted at AITU |

## Conclusions

1.  Plagiarism systems (Turnitin, StrikePlagiarism) answer *“is the text copied?”*, not *“are the references and citations correct?”*. Scirevia complements, not replaces them.
2.  scite and Recite each cover one aspect of references (retractions; formatting consistency) and are oriented to English-language texts.
3.  No tool covers K1, K3, K5, K6 and K7 together or supports RU/KZ theses — this justifies Scirevia.

## Evidence (accessed 23.10.2026)

- scite: *How do I use the scite Reference Check?* — help.scite.ai; Nature Index news on scite’s retraction-flagging bot.
- Recite: reciteworks.com — product tour and FAQ.
- Turnitin: turnitin.com/products/similarity · StrikePlagiarism: strikeplagiarism.com · SciSpace: typeset.io
- Tools currently used by respondents (S-1, Q7): manual checking, DOI lookup and plagiarism-detection software; none of them verifies whether a source supports the citation.
