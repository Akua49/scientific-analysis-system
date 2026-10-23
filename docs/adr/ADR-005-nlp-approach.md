# ADR-005: NLP approach for citation, abstract and topic checks

- **Status:** Proposed (model chosen after E3–E5) · **Owner:** S. Sergeyeva
- **Context:** Cross-lingual (RU/KZ/EN), paraphrase-aware comparison is required; documents are confidential.
- **Decision:**
  - Citation check: split source text into passages -\> retrieve top-k by multilingual embeddings (candidates: multilingual-e5-base, LaBSE, paraphrase-multilingual-mpnet) -\> NLI cross-encoder label (supported / partial / not supported) -\> show fragment and score. Baseline: TF-IDF cosine.
  - Abstract check: summary (LLM with consent, else extractive) + coverage (BERTScore-style) + NLI consistency of each abstract sentence against the body.
  - Topic check: embedding of title + abstract vs. archive; top-5 with cosine score; threshold calibrated on labelled pairs.
  - LLM: provider-agnostic interface; disabled unless the user consents per document.
- **Consequences:** + local, explainable, multilingual. − Kazakh quality uncertain -\> reported separately in evaluation.
