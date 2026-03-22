# CLAUDE.md — Project Template

Copy this file into a new project as `CLAUDE.md`. Fill in the relevant sections, delete the rest.
The rules and writing style from `CLAUDE-MASTER.md` apply to all projects automatically.

## Project Overview

<!-- Describe what the project is, who the authors are, and the core research question or purpose. -->

## Repository Structure

<!-- Folder layout as a table or tree diagram. -->

## Tech Stack

<!-- List languages, frameworks, and key libraries. -->

## Key Concepts

<!-- Domain-specific terminology, data definitions, and methodological foundations the assistant must understand. -->

## Conventions

<!-- File naming patterns, data formats, workflow rules. Examples:
- Notebook filenames are numbered sequentially (e.g., `01_`, `02_`) to indicate execution order.
- Data files use tab-delimited or comma-separated CSV, parquet for large datasets, and shapefiles/GeoJSON for spatial data.
- All document drafts in markdown, exported to PDF via pandoc.
- When regenerating PDFs, delete the old file first to avoid Preview caching issues on macOS.
- Scripts go in `scripts/`, raw data in `data/`, analysis outputs in `output/`.
-->

---

## Project-Type Sections

Include only the sections relevant to your project type.

### For Research Projects

#### Data Acquisition

<!-- Sourcing rules, ethics, rate limiting, anonymization. Example:
- Public documents only.
- Automated collection: identify as researchers, comply with terms of use, rate-limit requests.
- Anonymization: do not name individual agencies in published findings.
-->

#### Research Log

Maintain a running research log at `output/research-log.md`. Append timestamped entries for:

- Key decisions and their rationale
- Findings from scoping exercises
- Methodological insights from conversations
- Dead ends and why they were abandoned
- Questions that remain open

Write entries in the background as work progresses. Do not wait for the user to ask. Each entry should be brief (2-5 sentences) with a `### YYYY-MM-DD HH:MM` header.

#### Project Documentation

For every project, create a `FOR<PROJECTNAME>.md` file that explains the whole project in plain language. Include: technical architecture, codebase structure and how parts connect, technologies used, rationale behind technical decisions, and lessons learned (bugs encountered and fixes, pitfalls and how to avoid them). Write engagingly (analogies and anecdotes, not dry textbook prose).

### For Grant Proposals

#### Proposal Format

<!-- Describe the required structure (e.g., Part B1, Part B2, section documents). -->

#### Chart/Diagram Design Conventions

<!-- Visual identity rules. Example:
- Self-contained HTML (inline CSS, no external dependencies).
- Blue color scheme: headers #2c5282, step boxes #e6f2ff.
- Equations rendered in inline text using Unicode math symbols (not MathJax/LaTeX).
- Target width: 800px max-width for methodology charts.
-->

### For Teaching / Course Materials

#### Key Course Details

<!-- Assessment breakdown, pedagogy philosophy, schedule, holidays. -->

#### Presentation Defaults

<!-- Slide format and resolution. Example:
- Quarto reveal.js slides use 1920x1080 resolution.
-->
