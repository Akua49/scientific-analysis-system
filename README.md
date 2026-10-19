# Scientific Analysis System

Development of a system for comprehensive analysis and evaluation of scientific information using digital and intelligent technologies.

Diploma project, Astana IT University, School of Software Engineering.

## Description

The system helps to check scientific texts (diploma theses, projects, and articles). It includes the following features:

- reference check: whether a link from the reference list is available and leads to the stated source;
- citation check: whether a quotation in the work matches the text of the source;
- summarization of the work and comparison of the summary with the author's abstract;
- document check against requirements that the user sets in a separate window;
- check of the topic for overlap and similarity with topics of previous years' works.

## Problem, Target Users, Expected Outcomes

- **Problem:** when preparing scientific works, links in the reference list often do not open or lead to the wrong source, quotations do not match the source text, the abstract does not reflect the content of the work, the document does not meet the requirements, and the topic repeats works from previous years. At present, all of this is checked manually by supervisors and those responsible for formatting control, which takes a significant amount of time.
- **Target users:** bachelor's and master's students, academic supervisors, staff responsible for formatting control and topic approval, authors and editors of scientific articles.
- **Expected outcomes:** a working web system with an analytical module, a server side, a client side, and documentation. The system generates a report on the checks for the author and the reviewer.

## Team

| Team member | Role |
|---|---|
| Saltanat Sergeyeva | ML/Data engineer (analytical module) |
| Alzira Kuanyshbekova | Frontend developer, UX/UI designer |
| Meruert Khairgeldinova | Backend developer |

**Supervisor:** Almas Bakhytuly Myrzakhmetov

## Project Scope and Status

- **In scope:** reference check, citation check, summarization and comparison with the abstract, document check against requirements, comparison of the topic with topics of previous years, web interface with a report.
- **Out of scope:** mobile application, plagiarism check against the whole internet.
- **Status:** analysis and design stage. A complete application is not required at this stage.

## Technologies

- **Analytical module:** Python, FastAPI, spaCy or NLTK, scikit-learn, Hugging Face Transformers, Pandas.
- **Server side:** Node.js, Express.js, MongoDB, REST API.
- **Client side:** HTML, CSS, JavaScript, Figma.
- **Version control:** Git, GitHub.

## Repository Structure

- `docs/`: project proposal, literature review, comparisons, requirements, architectural decisions;
- `diagrams/`: diagrams (editable source files and exports);
- `src/`: source code organized by component;
- `tests/`: automated tests and supporting test materials;
- `config/`: dependency definitions and configuration examples (no passwords or keys).

## Links

- YouTrack: *link will be added*
- Documentation: [`docs/`](docs/) folder

## Setup, Execution, and Testing

Instructions for installation, running, and testing will be added when runnable code is available.
