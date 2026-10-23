# ADR-004: Hybrid document structure extraction

- **Status:** Proposed (final after experiment E1) · **Owners:** M. Khairgeldinova (upload, text extraction), S. Sergeyeva (reference/citation parsing)
- **Context:** Reference lists in AITU theses use GOST, APA and IEEE styles; documents are DOCX or PDF.
- **Decision:** DOCX -\> python-docx/mammoth; PDF -\> GROBID (TEI) with PyMuPDF fallback; reference strings -\> GROBID parser + rules for GOST; in-text citations -\> regex for \[n\], (Author, Year), \[n, p. x\].
- **Consequences:** + best available parser for PDFs (Tkaczyk et al. 2018). − Java service in Docker Compose; GOST quality must be measured (E1, target F1 \>= 0.85).
